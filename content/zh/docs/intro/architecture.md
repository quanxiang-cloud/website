---
title: "平台架构"
keywords: '架构,技术架构'
description: '全象云平台架构说明'
linkTitle: "平台架构"
weight: 1400
---

##  前后端分离

全象云平台将前端与后端分离，是一个云原生、完全容器化、微服务架构的软件平台。平台可以部署于所有基于 [Kubernetes](https://kubernetes.io/) 的开发的容器平台，同时支持原生 Kubernetes 系统。平台分为：应用层，对接层，数据处理层及基础层。 

- **应用层**：提供灵活的表单引擎，可视化流程引擎，复杂功能规则引擎等，同时支持多端适配，包括 WEB 端、Native APP、微信小程序、H5 等。

- **对接层**：用于实现前后端功能对接，同时支持第三方 API 接入，FaaS 插件及应用接入等。

- **数据处理层**：将前端业务请求数据处理成基础层需要的格式并存储。

- **基础层**：所有业务的基础支撑平台，包括数据库，存储，容器平台等。




![产品架构](/images/introduction/产品架构.png)
