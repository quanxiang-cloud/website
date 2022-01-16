---
title: 'Knative Autoscaler 自定义弹性伸缩'
tag: 'Knative,serverless kubernetes, 低代码'
keywords: 'Knative,serverless kubernetes, k8s, 后端, 低代码, low-code'
description: '如今各大云厂商都开始提供 Serverless Kubernetes 服务，简化集群管理，降低运维管理负担，让 Kubernetes 更加简单。那么问题来了，一个系统到底需要具备怎样的能力才能更好地支撑 Serverless 应用呢？'
createTime: '2021-09-03'
author: '唐磊'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Knative%20Autoscaler/cover.png'
---



## 背景

如今各大云厂商都开始提供 Serverless Kubernetes 服务，简化集群管理，降低运维管理负担，让 Kubernetes 更加简单。那么问题来了，一个系统到底需要具备怎样的能力才能更好地支撑 Serverless 应用呢？                          

Serverless 应用需要的是面向应用的管理功能，比如：升级、回滚、灰度发布、流量管理以及弹性伸缩等功能。

Knative 就是建立在 Kubernetes 之上的 Serverless 应用编排框架。Knative 的主要功能之一是自动缩放应用程序的副本，包括在没有收到流量时将应用程序缩放为`0`。 默认 Autoscaler 组件监视流向应用程序的流量，并根据配置的指标向上或向下扩展副本。本期主要讲解  Knative Autoscaler 的原理和使用。



> 说明：
>
> 如需实践 Knative Autoscaler 的使用，您可以先了解以下内容。
>
> 1. Kubernetes：需要准备一个 [Kubernetes](https://kubernetes.io/docs/home) 的集群，并学习相关的命令。
> 2. knative serving：您可以按照入门指南安装 [Knative](https://knative.dev/docs/admin/install) 。



## Autoscaler 原理

Autoscaler 根据监控到的指标（concurrency、rps、cpu 等），并根据配置的指标来放大或缩小副本，从而实现自动扩缩容。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Knative%20Autoscaler/autoscaler.png" width = 60%/>

(来源：[kubernetes autoscaler](https://v1-17.docs.kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/))
</div>



## KPA VS HPA

Knative Serving 支持 Knative Pod Autoscaler（KPA）和 Kubernetes 的 Horizontal Pod Autoscaler（HPA）。以下是不同 scaler 的功能和局限性。

#####  KPA

- Knative Serving 核心的一部分，并且在安装 Knative Serving 后默认启用；
- 支持从 `0` 扩展功能；
- 不支持基于 CPU 的自动缩放。

##### HPA

- 不是 Knative Serving 核心的一部分，安装 kubernetes 后默认启动；
- 不支持从 `0` 扩展功能；
- 支持基于 CPU 的自动缩放。



## scaling 配置

通过以上介绍，我们初步了解了 Autoscaler 执行原理，接下来介绍如何配置 KPA 或 HPA。

scaling 配置用于指定放大和缩小的行为，可以为两个方向指定一个稳定窗口，以防止缩放目标中的副本数量波动。 类似地，指定扩展策略可以控制扩展时副本的变化率。

可以使用 annotations 配置 Autoscaler 实现的类型（KPA 或 HPA）；

- **Global settings key：** `pod-autoscaler-class`；

- **Per-revision annotation key：** `autoscaling.knative.dev/class`；

- **Possible values：** `"kpa.autoscaling.knative.dev"` or `"hpa.autoscaling.knative.dev"`；

- **Default：** `"kpa.autoscaling.knative.dev"`；

  配置示例：

  ```
  apiVersion: serving.knative.dev/v1
  kind: Service
  metadata:
    name: helloworld-go
    namespace: default
  spec:
    template:
      metadata:
        annotations:
          autoscaling.knative.dev/class: "kpa.autoscaling.knative.dev"
      spec:
        containers:
          - image: gcr.io/knative-samples/helloworld-go
  ```

  

  ### 配置指标说明

  度量标准配置定义自动定标器监视哪种度量标准类型，配置参数说明如下：

  - Setting metrics per revision: 对于 `per-revision` 配置，这是使用 `autoscaling.knative.dev/metric` 注解确定的。可以 `per-revision` 配置的可能的度量标准类型取决于使用的 Autoscaler 实现的类型：
    - 默认的 KPA Autoscaler 支持并发和 rps 指标；
    
    - HPA Autoscaler 支持 cpu 指标。
    
  - Targets： 配置 Targets 会为 Autoscaler 提供一个值，它会尝试为 `revsion` 的配置指标维护该值。

  - Configuring scale to zero：只有在使用 Knative Pod Autoscaler(KPA) 时才能启用缩放为零，并且只能全局配置。

  - Enable scale to zero： `scale to zero` 值控制 Knative 是否允许副本缩小到零（如果设置为 true），或者如果设置为 false 则停止在 `1` 个副本。

  - Scale to zero grace period： 指定一个上限时间限制，系统将在内部等待从零开始缩放的机器在删除最后一个副本之前就位。

  - Configuring concurrency：并发性决定了应用程序的每个副本在任何给定时间可以处理的并发请求数。

  - Soft versus hard concurrency limits： 可以设置软或硬并发限制。如果同时指定了软限制和硬限制，则将使用两个值中较小的一个。这可以防止 Autoscaler 具有硬限制值不允许的目标值。

  - Target utilization：指定 Autoscaler 实际应针对的先前指定目标的百分比。 这也称为指定副本运行的热度，这会导致Autoscaler在达到定义的硬限制之前扩展。

  - Configuring scale bounds： 配置上限和下限以控制自动缩放行为。还可以指定在创建后立即将 `revision` 缩放到的初始比例。

  - Lower bound： 每个修订版应具有的最小副本数。

  - Upper bound： 每个修订版应具有的最大副本数。

  - Initial scale： revision 在创建后必须立即达到的初始目标比例，然后再将其标记为就绪。

  - Scale Down Delay： 缩减延迟指定了一个时间窗口，在应用缩减决策之前，该时间窗口必须以降低的并发性通过。

  

  ## 配置示例

  在使用默认配置情况下的 Knative serving(KPA)

  1. 创建一个 demo 服务。

     ```bash
     cat <<-EOF | kubectl apply -f -
     apiVersion: serving.knative.dev/v1
     kind: Service
     metadata:
       name: test
     spec:
       template:
         metadata:
           annotations:
             initial-scale: "1"
             allow-zero-initial-scale: "false"
             enable-scale-to-zero: "false"
         spec:
           containers:
             - image: wentevill/demo:latest
     EOF
     ```
     
     
     
  2. 查看 pod 状态，在一段时间没有流量的情况下，scale 到 `0`。

     ```bash
     kubectl get pods
     ```

     ```bash
     NAME                                   READY   STATUS    RESTARTS   AGE
     test-00001-deployment-c4546964-mjwqm   2/2     Running   0          15s
     ```

     

  3. 查看 ksvc 状态。

     ```bash
     kubectl get ksvc
     ```

     ```bash
     NAME   URL                                           LATESTCREATED          LATESTREADY            READY   REASON
     test   http://test.default.172.31.162.220.sslip.io   test-00001             test-00001             True
     ```

     > 说明：
     >
     > 这里使用的是 `magicDNS`，使用其他的地址可能会不一样，请以实际使用为准。

  4. 访问 service 。

     ```bash
     curl http://test.default.172.31.162.220.sslip.io
     ```

     - pod 存在：执行并返回结果。
     - pod 不存在：autoscaler 扩容(冷启动)到 `1`，然后执行并返回结果。

     > 说明：
     >
     > 冷启动时长从毫秒到分钟级别，第一批流量可能会超时。





## 总结

以上就是 Knative Autoscale 的内容，通过 KPA 技术实现真正意义上的 Severless。

下期将为大家带来 API 编排的应用及痛点，请大家持续关注。



> **引用链接**
>
> [1] Knavtive serving: https://knative.dev/docs/serving
>
> [2] Horizontal Pod Autoscaler: https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale
>
> [3] Kubernete Autoscaler：https://v1-17.docs.kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/

