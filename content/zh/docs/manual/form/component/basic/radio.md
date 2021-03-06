---
title: "单选框"
description: "单选框组件定义和字段属性"
linkTitle: "单选框"
weight: 42213
---

## 组件定义

单选框需预先设置好选项内容，用户可直接单项选择，适用于选项较少的选择场景。

## 字段属性

![radio](/images/manual/component/radio.png)

请根据实际需要配置字段的以下属性：

- 标题名称：字段名称，必填；

- 描述内容：如有需要请填写；

- 字段属性：支持设置成普通、只读、隐藏，默认为普通；

- 排列方式：支持横向排列、纵向排列；

- 是否必填：可选择字段是否必填，默认非必填；

- 允许自定义：支持设置自定义选项；

- 选项来源：支持自定义、选项集，支持点击设置选项默认值。

  - 自定义：需自定义选项列表，请填写选项名称，且每个选项不能超过 15 个字符；
  - 选项集：选择事先定义好的选项集。

{{< alert tip >}}

**说明**

选项集配置入口为 **应用管理** > **选项集**，配置步骤参考：[创建选项集](../../../../option_set/)。

{{</ alert >}}



