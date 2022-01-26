---
title: "创建 API"
description: "API 创建流程介绍"
keywords: "API"
linkTitle: "创建 API"
weight: 7331
---

创建 API 即录入 API 的定义，需要设置 API 的基本信息、服务信息、请求信息、和返回信息等规则内容。本小节主要介绍如何快速创建 API 。

## 前提条件

- 已创建 API 分组。如果未创建 API 分组，参考[创建 API 分组](../../../proxy/create_apigroup/)进行创建。



## 新建 API

按照以下步骤，创建 API。

1. 选择需要新建 API 的 API 分组，点击 **API 列表** > **新建 API**。

   ![create1](/images/api/proxy/create_api/create1.png)

2. 进入新建 API 页面，填写如下信息。

   ![create2](/images/api/proxy/create_api/create2.png)

   **定义 API 基本信息**
   {{<table >}}

   | 参数     | 描述                                                         |
   | -------- | ------------------------------------------------------------ |
   | API 名称 | 所创建的 API 的名称，API 名称标识需在所属分组内具有唯一性。</br>**说明**：最多可填写 20 个字符，支持中文或英文字符。 |
   | API 路径 | 第三方 API 的原始路径，相对于根目录的相对路径，如：/api/v1/payment/xxx.php。</br>**说明**：分组配置中已完成主机域名配置（如：[http://qingcloud.com](http://qingcloud.com/) ），此处仅需补充 API 相对路径（如：/api/v1/payment/xxx.php）。</br>补充完成后，系统可获取此 API 全局唯一 URL（如：http://qingcloud.com/api/v1/getName）。非标准 |
   | 描述     | API 的相关描述。                                             |

   

   {{</table >}}

   **定义 API 请求信息**
   {{<table >}}

   | 参数     | 描述                                                         |
   | -------- | ------------------------------------------------------------ |
   | 请求方法 | 支持标准的 HTTP Method，可选择 GET、POST、PUT、DELETE、OPTION、PATCH。</br>**说明**：请求协议已在分组配置中配置，请求协议支持：HTTP、HTTPS。 |
   | 代理路径 | API 导入到全象云平台后，系统生成的虚拟访问路径。</br>此路径根据由平台分配给 APP 的唯一虚拟路径 + APP 内分组路径组成。可自动获得，无需手动配置。 |
   | API 标识 | API 在分组内唯一标识，需用英文标识。                         |
   | 请求参数 | API 的请求参数，即配置用户需要在什么位置传入什么参数。<br>可选位置有：Query、Header、Body、常量参数，常量参数定义规则参见下文：[常量参数说明](#常量参数说明)。<br>支持的参数类型有：string、number、boolean。其中 Body 还支持 object、array。 |

   {{</table >}}

   **定义 API 返回信息**
   {{<table >}}

   | 参数     | 描述                                                         |
   | -------- | ------------------------------------------------------------ |
   | 返回参数 | API 的返回参数。支持的参数类型包含：string、number、boolean、object、array。 |
   {{</table >}}

3. 点击 **确认新建** 即可。创建成功后 API 默认开启状态。

## 批量导入

[Swagger](https://swagger.io/docs/specification/about/?spm=a2c63.p38356.0.0.1f4726d3tHJcUC) 是一种描述 API 的规范，广泛应用于定义和描述后端应用服务的 API。全象云平台支持导入 Swagger2.0 的文件来创建 API。

按照以下步骤，批量导入创建 API。

1. 选择需要新建 API 的 API 分组，点击 **API 列表** > **批量导入**。

2. 进入批量导入页面，点击或拖拽上传，支持 Swagger2.0 数据导入。

   ![create3](/images/api/proxy/create_api/create3.png)

3. 点击 **确认导入** 即可。导入成功后 API 默认开启状态。

## 非标准 restful API 的创建方法

标准 restful 的 API 由 apiPath+method 组成，有确定的输入输出。

非标准的 API apiPath 则需要通过 action 参数决定输入和输出。因此，在平台中注册非标准 API 采用 `apiPath?action` 的格式定义 apiPath，系统可以识别前半部分为apiPath，后半部分为 action 参数。

## 常量参数说明

### swagger 文件中如何定义常量参数

对于输入值已固定的参数如： `version=1` ，用户不需要每次调用时指定，可在 swagger 中注入常量参数指定。
swagger 全局定义的 `x-consts` 为本文件内所有 api 共享的常量配置，`paths` 内定义的 `x-consts` 为本 API 独有。
polyapi 在解析每个 API 时，将合并每个 API 的两部分 `consts` 配置。
代理调用原生 API 或编排原生 API，polyapi 会自动 append 这些常量参数，无需手动输入。

```
{
 "swagger": "2.0",
 "x-consts": [
    {
      "name": "version",
      "type": "number",
      "in": "body",
      "description": "",
      "data": "1"
    }
 ],
 "paths": {
    "/api/v1/getData": {
    	"get":{
		  "x-consts": [
		    {
		      "name": "type",
		      "type": "string",
		      "in": "body",
		      "description": "",
		      "data": "foo"
		    }
		  ]
		}
   }
 }
}
```

#### 依赖的 swagger 参数

paths.operationId 用于生成 API 标识，要求分组内唯一，在 API 代理路径中显示。

### action 数据类型说明

该类型实际为 `string` 类型，无需填值，只需要指定 type、name、in，polyapi 会自动取 path 上 ? 之后的 action 参数作为常量填入。

### timestamp 数据类型说明

自动填入时间戳（UTC），value 配置为 format，支持空 value 作为默认 format 处理。
目前支持的时间戳格式：

- YYYY-MM-DDThh:mm:ssZ(default)
- YYYY-MM-DDThh:mm:ss+0000(ISO8601)

