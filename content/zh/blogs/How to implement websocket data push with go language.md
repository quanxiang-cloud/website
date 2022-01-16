---
title: 'go 语言实现 websocket 数据推送'
tag: '分布式系统, 后端, 低代码, go 语音, WebSocket'
keywords: '分布式系统, go 语音, WebSocket, 消息推送,WebSocket 消息推送, redis, 后端, 低代码, low-code'
description: '系统开发的过程中，我们经常需要实现消息推送的需求。单端单实例的情况下很好处理（网上有许多教程这里不做展开），但在分布式系统及多端需要推送的情况下该如何处理呢？'
createTime: '2021-08-20'
author: '周慧婷'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20implement%20websocket%20data%20push%20with%20go%20language/cover.png'
---

## 写在前面

系统开发的过程中，我们经常需要实现消息推送的需求。单端单实例的情况下很好处理（网上有许多教程这里不做展开），但在分布式系统及多端需要推送的情况下该如何处理呢？
在分布式系统中，消息推送服务端是多实例的。某系统中一个服务生成一条消息，这条消息需要实时推送到多个终端，此时该如何进行有效的 WebSocket 推送呢？首先一起看看如下场景：

> 假设推送消息由消息实例2产生，但是终端真正连接的消息实例是实例1和实例3，并没有连接到生产消息的实例2，系统是如何将实例2的消息同步推送到终端1和终端2的呢？下文将详细描述。


<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20implement%20websocket%20data%20push%20with%20go%20language/websocket1.png" width = 60%/>
</div>


## 基本原理

为了满足需求我们做了构想：使用 [redis](https://redis.io/) 做协同中间件，用来存储用户信息及用户使用的终端信息，消息的生产者实例通过订阅 redis 获取终端连接的消息实例，并将消息通知到消息实例，最终通过 WebSocket 将消息发推送到用户终端。具体流程如下图：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20implement%20websocket%20data%20push%20with%20go%20language/websocket2.png" width = 60%/>
</div>

为了实现构想，我们构造了两个组件：Client、ClientManager，实现逻辑如下。

## 服务端实现

### Client

Client 组件的作用，是当用户与消息服务中某个实例建立连接后，管理这个连接的信息，这里通过一个 Golang 结构体来定义：

```go
type Client struct {
    UUID   string 
    UserID string
    Socket *websocket.Conn
    Send   chan []byte
}
```

结构体中的数据类型说明如下：

- UUID：对连接进行唯一性的标识，通过此标识可以查找到连接信息。
- UserID：用户 ID。
- Socket：连接对象。
- Send：消息数据 channel。


我们为 Client 结构体实现了两个方法：Read、Write 来处理消息的接受和发送。

#### Read 方法

Read 方法比较简单，从终端接收请求消息后，消息实例通过 WebSocket 回应接收消息状态，并不返回请求结果。结果通过 Write 方法返回。

```go
func (c *Client) Read(close, renewal chan *Client) {
    defer func() {
        close <- c
    }()

for {
    _, message, err := c.Socket.ReadMessage()
    if err != nil {
        break
    }
  // ...
     // message logic
}
}
```



#### Write 方法

Write 方法将请求结果返回给终端。Client 会监听 send channel，当 channel 有数据时，通过 socket 连接将消息发送给终端。

```go
func (c *Client) Write(close chan *Client) {
    for {
        select {
        case message, ok := <-c.Send:
            if !ok {
                return
            }
            c.Socket.WriteMessage(websocket.TextMessage, message)
        case <-c.Ctx.Done():
      return
        }
    }
}
```



### ClientManger

ClientManager 组件相当于连接池，可以管理所有的终端连接，并提供注册、注销、续期功能。

```go
type ClientManager struct {
    sync.RWMutex
    Clients    map[string]*Client 
    Register   chan *Client
    Unregister chan *Client
    Renewal    chan *Client
}
```

结构体的数据类型说明如下：

- Clients：是一个集合，用于存储创建的 Client 对象。
- Register：注册的 channel。
  - 把连接注册到 Clients 中，并通过 key-value 加入 Client 集合中，key 是连接的唯一性标识 ，value 是连接本身。
  - 把连接的唯一性标识和用户的 ID 以及建立连接的 pod address 信息，存储到 redis 中。
- Unregister：注销的 channel。
  - 从 ClientManager 组件的 Clients 集合中移除连接对象。
  - 删除 redis 对应的缓存信息。
- 
  Renewal：续期的 channel，用于对 redis 的键续期。


ClientManager 只提供了一个 Start 方法，Start 方法提供监听注册、注销以及续期的 channel，通过监听这些 channel 来管理创建的连接对象。当这些 channel 有数据时，执行对应的操作。

```go
func (manager *ClientManager) Start(ctx context.Context) {
    for {
        select {
        case conn := <-manager.Register:
            manager.Lock()
            manager.Clients[conn.UUID] = conn
            manager.Unlock()
            _, err := manager.affair.Register(ctx, &RegisterReq{
                UserID: conn.UserID,
                UUID:   conn.UUID,
                IP:     manager.IP,
            })
        case conn := <-manager.Unregister:
            _, err := manager.affair.Unregister(ctx, &UnregisterReq{
                UserID: conn.UserID,
                UUID:   conn.UUID,
            })
            conn.Socket.Close()
            close(conn.Send)
            delete(manager.Clients, conn.UUID)
        case conn := <-manager.Renewal:
                    //...
            // Key renewal to redis
        }
    }
}
```

### 消息推送

当一个消息服务实例生产用户的消息，需要推送消息给终端时，推送步骤如下：

1. 根据 userID 从 redis 读取数据，得到连接唯一性标识和 pod address 地址，这些信息是在终端第一次与服务端建立连接的时候写入 redis 的。
2. 此时根据 pod address，向对应的服务器发送请求。
3. 服务端接收到请求。


服务端接收请求的处理逻辑如下：

1. 根据传递过来连接唯一性标识的参数，通过 ClientManager 找到对应的连接。

```go
func (manager *ClientManager) Write(message *Message) error {
  manager.RLock()
  client, ok := manager.Clients[message.Recipient]
  manager.RUnlock()
  if !ok {
     return errors.New("client miss [" + message.Recipient + "]")
  }
  return client.SendOut(message)
}
```

2. 往 Client 的 send channel 发送数据。

```go
func (c *Client) SendOut(message *Message) error {
    content, err := json.Marshal(message.Content)
    if err != nil {
        return err
    }
    c.Send <- content
    return nil
}
```

3. 发送数据给终端。在前文介绍 Client 组件中，已说明 Client 组件的 send channel 有数据时，会读取 channel 产生的数据，通过连接对象发送给对应的终端。

## 总结

以上就是 web socket 推送消息给终端的主要思路。首先借助 redis 把用户的信息以及连接的标识和 pod address 存储起来，当某个服务端产生消息，再从 redis 读取对应的信息，通知相关的服务端，由对应的服务端给终端发送消息。

下期我们将为大家带来 Knative Serving 自定义弹性伸缩，请大家持续关注。

