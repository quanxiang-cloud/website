---
title: "Platform Architecture"
keywords: 'Architecture, Technical Architecture'
description: 'The architecture of QuanXiang Cloud Platform'
linkTitle: "Platform Architecture"
weight: 1400
---

##  Front and back-end separation

QuanXiang Cloud Platform separates the front and back ends and is a cloud-native, fully containerized, microservice architecture software platform. The platform can be deployed on all container platforms developed based on [Kubernetes](https://kubernetes.io/), and supports native Kubernetes system. The platform is divided into: application layer, docking layer, data processing layer and foundation layer. 


- **Application layer**: It provides flexible form engine, visual flow engine, complex function rule engine, etc. and supports multi-end adaptations, including WEB, Native APP, WeChat applet, H5, etc.

- **Docking layer**: It is used to realize front-end and back-end function docking, and also supports third-party API access and application access, etc.

- **Data processing layer*: Processes front-end business request data into the format required by the base layer and stores it.

- **Foundation layer*: Basic support platform for all business, including database, storage, container platform, etc.




![Product Architecture](/images/introduction/产品架构.png)
