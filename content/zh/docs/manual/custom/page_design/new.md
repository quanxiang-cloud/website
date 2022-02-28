---
title: "创建自定义页面"
description: "在全象云低代码平台使用页面引擎创建自定义页面"
linkTitle: "创建自定义页面"
weight: 4262
---

本小节主要介绍如何使用页面引擎创建自定义页面。

## 操作步骤

### 1、选择页面引擎

1. 登录 [全象云管理端](https://portal.quanxiang.dev/) ，点击 **应用管理** > **我的应用** > **具体应用** > **应用菜单页面**。

   ![intro2](/images/manual/custom/intro2.png)

2. 使用页面引擎构建自定义页面。

   ![intro1](/images/manual/custom/intro1.png)

### 2、选择组件

组件分为布局组件，和其他组件。基础组件和表单组件需要使用布局组件进行排版布局。

1. 点击布局组件中的容器，页面中出现容器组件，页面层级展示为容器。

   ![new1](/images/manual/custom/page_design/new1.png)

2. 拖动文本组件到刚放置的布局组件中，页面层级展示为容器 > 文本。

   ![new2](/images/manual/custom/page_design/new2.png)

   {{< alert tip >}}

   **说明**

   布局组件便于页面排版布局，且布局组件支持套用。

   {{</ alert >}}

### 3、配置组件属性

组件属性包含：属性、样式、事件、动态渲染。本文用文本组件为例描述如何配置组件属性。

1. 配置属性：点击配置，支持为文本组件配置变量参数。

   1. 点击**数据源** > **变量参数** > **+** ，新增参数，为参数赋值。

      ![new3](/images/manual/custom/page_design/new3.png)

   2. 绑定变量参数。

      ![new4](/images/manual/custom/page_design/new4.png)

2. 配置样式：样式设置支持可视化配置，同时支持通过源码编辑。此处选择可视化配置。详细内容参见：[样式说明](../style/)。

   - 画布：画布可配置文本框大小，文本框位置。
   - 显示布局：组件布局方式，支持配置块级、行内、行内块、弹性。
   - 定位：用于锁定组件在画布中的位置，支持配置默认、相对、绝对、固定。
   - 字体：支持配置字体大小、行高、字重（粗细）、对齐方式、颜色；
   - 背景：支持无填充、颜色填充、图片填充；
   - 边框：支持无边框、实线、虚线；
   - 阴影：支持配置阴影颜色、位置。

   ![new5](/images/manual/custom/page_design/new5.png)

3. 配置事件（可选）

4. 配置动态渲染（可选）

### 4、预览

组件的基础属性配置完成后画布中能够实时查看配置效果。变量参数绑定效果需在预览环境中查看。

点击顶部预览按钮，即可预览配置效果。

![new6](/images/manual/custom/page_design/new6.png)
