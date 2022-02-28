---
title: "Deployment & Requirements"
keywords: 'Deployment, Service'
description: 'Platform deployment and service requirements'
linkTitle: "Deployment and Service Requirements"
weight: 1600
---

QuanXiang Cloud low-code platform at this stage **only supports private deployment**, the private deployment can be divided into private deployment on public cloud and localized private deployment.

- Deployment on public cloud: It is recommended to deploy directly using the container platform, database (relational, non-relational), cache, messaging, and other products provided by each cloud vendor. You can also use the public cloud to create cloud hosts for deployment.
- Localized private deployment: It requires users to purchase their own hardware servers and deploy them in their own data centers or host them in other data centers.

{{< alert tip >}}

**Description**

QuanXiang Cloud low-code platform is a cloud native system platform, all applications are developed based on container platform and deployed containerized. For better performance, it is recommended to use the host to deploy database, cache, messages, etc.

{{</ alert >}}

## Software Requirements

- System Requirements: Centos 7.0 +, Ubuntu 16.04 +, Debain 10 +, etc.
- Container Platform: Kubernetes 1.16 +
- Database: Mysql 5.7 +, Mango DB 3.4.5, Redis 5.0.8 cluster
- Search Engine: ElasticSearch 7.5.1
- Message Queues & Middleware: Kafka 2.3.1
- Big Data: Zookeeper 3.4.14

## Hardware Requirements

Server Configuration: A minimum of 4 servers are required for K8S cluster installation.

- CPU: Intel Xoen E-2254ME @2.60 GHz * 2
- RAM: 32GB or more
- ROM:
  - 600GB SAS disk*8 and 2 RAID1 system disks
  - Data disk: 6 pieces RAID50
- NIC: 10 Gigabit fiber*2

## Installation Requirements

- System shutdown Selinux
- System shutdown snap partition
- Start SSH service, Disable password login, Login with SSH key
- All servers are under the same vlan and the network interoperates
