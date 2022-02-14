---
title: '可视化开发主流开源流程引擎与设计器研究对比'
tag: '开源, 可视化开发, 流程设计, 前端, 低代码, 流程引擎'
keywords: '开源, 可视化开发, 流程设计, 前端, 低代码, 流程引擎, low-code'
description: '开发低代码平台、工单系统、OA 系统和 BPM 软件等均需要可视化的业务流程设计器和业务流转功能，业务流程流转和可视化设计的核心是流程引擎和流程设计器。目前市面上主流的开源流程引擎主要有 Activiti、Flowable、Camunda、jBPM 和 osworkflow 等。主流的开源流程设计器主要有 bpmn-js、mxGraph、activiti-modeler、flowable-modeler 和 reactflow 等。现在我们对这些开源流程框架进行调研和分析。'
createTime: '2021-12-16'
author: '王志'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Visualization%20development%20open%20source%20process%20engine%20and%20designer%20comparison/cover.png'
---

## 背景

开发低代码平台、工单系统、OA 系统和 BPM 软件等均需要可视化的业务流程设计器和业务流转功能，业务流程流转和可视化设计的核心是流程引擎和流程设计器。目前市面上主流的开源流程引擎主要有 Activiti[1]、Flowable[2]、Camunda[3]、jBPM[4] 和 osworkflow[5] 等。主流的开源流程设计器主要有 bpmn-js[6]、mxGraph[7]、activiti-modeler[8]、flowable-modeler[9] 和 reactflow[10] 等。现在我们对这些开源流程框架进行调研和分析。

## 流程引擎调研

### Activiti

Activiti 由 Alfresco 公司开发，目前最高版本为 Activiti cloud 7.1.0。其中 activiti5 和 activiti6 的核心 leader 是 Tijs Rademakers，由于团队内部分歧，2017 年 Tijs Rademakers 离开团队，创建了后来的 Flowable。activiti6 以及 activiti5 代码则交接给 Salaboy 团队维护，activiti6 以及 activiti5 的代码官方已经暂停维护。往后 Salaboy 团队开发了 activiti7 框架，activiti7 内核使用的还是 activiti6，并没有为引擎注入更多的新特性，只是在 Activiti 之外的上层封装了一些应用。直到 Activiti cloud7.1.0 版本，Activiti cloud 将系统拆分为 Runtime Bundle、Audit Service、Query Service、Cloud Connectors、Application Service、Notification Service。这些工作的主要目的其实就是为了上云，减少对 Activiti 依赖的耦合，需要使用 Activiti 的系统只需要通过调用 http 接口的方式来实现工作流能力的整合，将工作流业务托管上云。



### Flowable

Flowable 是基于 activiti6 衍生出来的版本，目前最新版本是 v6.7.0。开发团队是从 Activiti 中分裂出来的，修复了一众 activiti6 的 bug，并在其基础上实现了 DMN 支持，BPEL 支持等。相对开源版，其商业版的功能会更强大。Flowable 是一个使用 Java 编写的轻量级业务流程引擎，使用 Apache V2 license 协议开源。2016 年 10 月，Activiti 工作流引擎的主要开发者离开 Alfresco 公司并在 Activiti 分支基础上开启了 Flowable 开源项目。Flowable 项目中包括 BPMN（Business Process Model and Notation）引擎、CMMN（Case Management Model and Notation）引擎、DMN（Decision Model and Notation）引擎和表单引擎（Form Engine）等模块。



### Camunda

Camunda 基于 activiti5，所以其保留了 PVM，最新版本 Camunda7.17，开发团队也是从 activiti 中分裂出来的，发展轨迹与 Flowable 相似。通过压力测试验证 Camunda BPMN 引擎性能和稳定性更好。功能比较完善，除了 BPMN，Camunda 还支持 CMMN（案例管理）和 DMN（决策自动化）。Camunda 不仅带有引擎，还带有非常强大的工具[11]，用于建模、任务管理、操作监控和用户管理。



### jBPM

jBPM 由 JBoss 公司开发，目前最高版本 7.61.0.Final，不过从  jBPM5 开始已经跟之前不是同一个产品了，jBPM5 的代码基础不是 jBPM4，而是从 Drools Flow 重新开始，基于 Drools Flow 技术在国内市场上用的很少，jBPM4 诞生的比较早，后来 jBPM4 创建者 Tom Baeyens 离开 JBoss 后，加入 Alfresco 后很快推出了新的基于 jBPM4 的开源工作流系统 Activiti，另外 jBPM 以 Hibernate 作为数据持久化 ORM，而 Hibernate 也已不是主流技术。



### osworkflow

osworkflow 是一个轻量化的流程引擎，基于状态机机制，数据库表很少，osworkflow 提供的工作流构成元素有：步骤（step）、条件（conditions）、循环（loops）、分支（spilts）、合并（joins）等，但不支持会签、跳转、退回、加签等这些操作，需要自己扩展开发，有一定难度。如果流程比较简单，osworkflow 是很好的选择。



## 流程设计器调研

### bpmn-js

bpmn-js 是 BPMN 2.0 渲染工具包和 Web 模型。bpmn-js 正在努力成为 Camunda BPM[12] 的一部分。bpmn-js 使用 Web 建模工具可以很方便的构建 BPMN 图表，可以把 BPMN 图表嵌入到你的项目中，容易扩展。bpmn-js 是基于原生 js 开发，支持集成到 vue、react 等开源框架中。



### mxGraph

mxGraph 是一个强大的 JavaScript 流程图前端库，可以快速创建交互式图表和图表应用程序，国内外著名的 ProcessOn[13] 和 draw.io[14]都是使用该库创建的强大的在线流程图绘制网站。由于 mxGraph 是一个开放的 js 绘图开发框架，可以开发出很炫的样式，或者完全按照项目需求定制。



### activiti-modeler

Activiti 开源版本中带了 web 版流程设计器，在 Activiti-explorer 项目中有 activiti-modeler，优点是集成简单，开发工作量小，缺点是界面不美观，用户体验差。



### flowable-modeler

Flowable 开源版本中带了 web 版流程设计器，展示风格和功能基本跟 activiti-modeler 一样，优点是集成简单，开发工作量小，缺点是界面不美观，用户体验差。



### react-flow

react-flow 是一个用于构建基于节点的应用程序的库。这些可以是简单的静态图或复杂的基于节点的编辑器。同时 react-flow 支持自定义节点类型和边线类型，并且它附带一些组件，可以查看缩略图的 Mini Map 和悬浮控制器 Controls。基于 react 生态开发，图形高度自定义，任何 ReactElement 都可以作为节点，但是不支持 bpmn 图表。



## 开源框架对比

经过对比，camunda 在功能方面比 flowable、activiti 流程引擎强大，性能和稳定性更突出。在开源流程引擎选型方面，camunda 是很好的方案之一。bpmn-js 使用 Web 建模工具可以很方便的构建 BPMN 图表，并且是基于原生 js 开发，可以很方便的集成到 vue、react等开源框架中。React-flow 是基于 react 生态开发的，节点可以高度自定义，任何 ReactElement 都可以作为节点，在流程图的呈现上是高度自由，可以满足复杂的流程图形需求。bpmn-js 和 react-flow 各有所长，bpmn-js 支持 BPMN 图表，而 react-flow 图形高度自定义，这两个框架均能很好的进行集成开发。在流程设计器框架选型方面 bpmn-js 和 reactflow 均为不错的选择。

## 展望

未来的技术方向基本都是上云，业务系统需要先微服务化，将工作流业务托管上云。原来的 workflow core 的流程引擎模式对流程引擎框架耦合太多，需要减少对流程引擎依赖的耦合。对于解耦之后的流程引擎，需要集成 workflow 的系统只需要通过调用 http 接口的方式来实现工作流能力的整合。

随着 AI 技术与 RPA 的融合，RPA 的优势逐渐显露，使得很多企业在业务流程自动化上开始追捧 RPA。BPM 与 RPA 之间，本来是包含与被包含的关系。但现在随着 RPA 的功能越发强大，在云计算、大数据、AI 等技术的加持下，基于 RPA 的智能业务流程平台正在不断诞生。在 BPM 借助 AI 与 RPA 横向发展的同时，RPA 也在某些应用场景中开始替代并介入 BPM。两者，出现了融合发展的趋势。RPA 已经逐步成为 BPM 中自动化环节不可或缺的部分。

基于以上发展趋势以及低代码平台自身需要满足业务多元化，流程引擎框架必定会微服务化，RPA 能力也必将是流程引擎框架的必备能力之一。

全象低代码平台将采用 golang 语言重新设计工作流框架，拆分传统模式的流程引擎框架，将业务流程服务拆分解耦。同时在流程设计器的选择上会选择支持高度可定制的框架，流程设计器是重要的支撑工具。全象低代码平台将呈现可操作性强并且美观的流程设计器，敬请期待。



 ## 引用链接

[1] Activiti ：https://www.activiti.org/

[2] Flowable：https://www.flowable.com/

[3] Camunda：https://camunda.com/

[4] Jbpm：https://jbpm.org/

[5] osworkflow：https://gitee.com/mirrors/osworkflow

[6] bpmn-js：https://bpmn.io/toolkit/bpmn-js/

[7] mxGraph：http://jgraph.github.io/mxgraph/

[8] activiti-modeler：https://github.com/Activiti/activiti-modeling-app

[9] flowable-modeler：https://wwv.flowable.com/

[10] react-flow：https://gitee.com/mirrors/react-flow/

[11] Camunda 工具：https://camunda.com/products/

[12] Camunda BPM：https://www.oschina.net/p/camunda

[13] ProcessOn：https://www.processon.com/

[14] draw.io：https://app.diagrams.net/

