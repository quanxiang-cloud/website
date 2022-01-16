---
title: '如何快速搭建固资管理系统'
tag: '固定资产, 管理系统, 低代码, 可视化开发'
keywords: '固定资产, 管理系统, 低代码, 可视化开发, 快速开发, 低代码, low-code'
description: '固定资产对于公司而言，相当于物质基石。通过固定资产的管理，管理者不仅能了解公司固定资产的整体状况，提升公司资产的使用效率，同时还能提升员工的办公体验。互联网时代发展至今，管理者们期望一款更加灵活、易用、便捷的固定资产管理平台。那么这样一款应用，能够通过低代码平台快速构建吗？'
createTime: '2021-12-09'
author: '李俊频、邓晓阳'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/cover.png'
---

## 背景

固定资产对于公司而言，相当于物质基石。通过固定资产的管理，管理者不仅能了解公司固定资产的整体状况，提升公司资产的使用效率，同时还能提升员工的办公体验。互联网时代发展至今，管理者们期望一款更加灵活、易用、便捷的固定资产管理平台。那么这样一款应用，能够通过低代码平台快速构建吗？

今天，我们以全象云平台为例，通过可视化方式构建一个固资管理系统中的服务器预到货流程。

## 全象云平台

全象云平台是一个基于云原生的、完全容器化的工具和平台，适用于辅助构建企业各类数字化应用。全象云平台能够支持快速构建应用、便捷维护管理应用、企业存量业务与全象云构建业务的集成。

平台目前提供了以下功能，能够支持可视化构建基础的管理系统：

* 🚀 **快速应用开发**
  * 可视化设计器：通过简单的拖拽、参数配置等方式即可完成页面设计、工作流编排、数据模型设计及角色权限的定义。
  * 表单引擎： 系统提供丰富的页面组件，能够满足页面呈现的自定义组件需求。
  * 工作流引擎： 包含灵活的触发方式和丰富的流程组件，支持多种触发方式，表单数据触发、时间触发、表单时间触发等。同时提供审批、填写等人为节点处理，同时支持数据新增、数据更新等自动流程节点处理。同时提供规则引擎的能力，满足复杂业务下的逻辑定义。
* 🧑‍💻 **灵活组织管理**
  * 企业通讯录：提供多种管理通讯录方式，帮助企业快速完成组织的构建。
  * 角色管理：企业角色权限按需细分，保障平台账户访问安全和数据安全。
* ☁️**多云部署和运维**

更多功能参见：[官方文档](https://docs.clouden.io/intro/features/)。在简单了解了全象云平台的功能后，我们就可以开始构思，搭建一个简单的固资管理系统。



## 固资管理业务流程概要

本文以固定资产系统中的服务器管理的一个流程为例：服务器预到货流程。

服务器预到货指一批服务器，从供货商的仓库运送到公司后，实现服务器可用化的流程。在此流程中，可能会涉及不同的人员，最后需要将层层处理的结果放入公司的资产列表中，完成资产的入库。

我们的需求是，通过一张表单传递服务器在申请、发货、审批、上架等流程节点中的信息，最后完成预定一个服务器并入库上架的数字化流程。



## 快速开始

厘清需求后，即可进入平台，搭建想要的系统。

> **说明**
>
> 如需申请试用全象云平台，请联系邮箱：[quanxiangcloud@yunify.com](mailto:quanxiangcloud@yunify.com)。

### 创建应用

使用账号登录平台管理端，在应用管理内点击 **新建应用** 完成应用创建。


<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/1.png" width = 60%/>
</div>

### 设计流程表单

在应用中添加页面，全象云平台支持添加表单设计页面，自定义页面。服务器预到货流程仅需通过搭建表单实现。

1. 首先我们需要构建三张表单：

   * **服务器库存表**：字段包含设备名称【单行文本】、设备型号【单行文本】、设备状态【下拉单选框】、设备位置【选项集】。

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/2.png" width = 60%/>
   </div>

   * **工单表**：字段包含工单相关申请表【关联记录】、工单负责人【人员选择器】、工单状态【单选框】、工单备注【多行文本】、【附件】。 

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/3.png" width = 60%/>
   </div>

   * **服务器预到货申请表**：
     * 字段设计为：申请人【人员选择器】、申请人部门【部门选择器】、申请时间【时间日期】、申请理由【多行文本】，新建一个分组：服务器发货表【从空白创建】、工单表【连接到工单表】。其中服务器发货表字段为：设备名称【单行文本】、设备型号【单行文本】、设备状态【下拉单选框】、设备位置【选项集】 （与服务器库存表相同，只是作为一个入库前的中间表）；

     * 服务器预到货申请表包含一个子表：工单表（直接拉取外部的工单表的字段）。

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/4.png" width = 60%/>
   </div>

​				

2. 工作流设计：整体可以顺序分为以下几个节点：
   1. 触发流程： 不可见服务器发货表与工单表，只可见基本信息。
   2. 上级审批【审批】：上级领导可进行查看服务器预到货申请表的字段，不可见服务器发货表与工单表两个子表。
   3. 发货节点【填写】：供应商可以查看服务器预到货申请表的字段，可编辑服务器发货表子表单，不可见工单表。
   4. 验货【审批】管理员进行确认，并下发施工入库工单，可编辑工单表字段，只读其他所有字段。
   5. 上架、安装系统【审批】：工单负责人进行安装系统，可编辑工单表字段，只读其他所有字段。
   6. 数据入库【数据新增】：在安装系统完成后，将申请表内的数据一一对应写入库存表。
   7. 站内信【站内信】：审批通过后，通过站内信通知申请人。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/5.png" width = 60%/>
</div>

3. 工作流设计完成后，点击发布按钮，使工作流生效。
4. 最后，点击发布应用，即可进入访问端验证使用。



## 使用

用户账号登录到访问端，点击固资管理应用，选择发起流程的页面，新建数据。

1. 流程发起：输入相关信息，提交申请，同时生成一条新数据与流程待办 。

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/6.png" width = 60%/>
   </div>

2. 上级查看，进行审批。 

3. 供应商进行填写。

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/7.png" width = 60%/>
   </div>

 

4. 管理员查看信息，分配工单。

   <div align=center>
   <img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/8.png" width = 60%/>
   </div>

5. 工单负责人进行施工。 

6. 成功入库一条数据。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/How%20to%20build%20a%20fixed%20asset%20management%20system%20in%20a%20short%20time/9.png" width = 60%/>
</div>

至此，成功完成一台服务器预到货申请。大家可以参考此流程完成其他固定资产的入库与领用流程设计，搭建完整的固定资产的管理系统。



## 总结

以上就是在全象云平台中搭建固定资产管理系统的简单示例，其中的表单相对来说也比较简单，使用到的功能也相对较少。全象云平台还提供了 API 等一些高级的功能给应用开发者，使得满足复杂场景的需求。后续我们也将持续新增更多功能，来应对不同的业务场景，敬请期待。

