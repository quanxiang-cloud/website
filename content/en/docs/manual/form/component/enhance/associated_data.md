---
title: "关联数据"
description: "关联数据组件定义和字段属性"
linkTitle: "关联数据"
weight: 422391
---

## 组件定义

关联数据组件用于关联其他表的字段值，目前仅支持关联本应用的其他表单。



{{< alert tip >}}

**案例**

用户在【固定资产申请表】中申请显示器，在申请物品栏点击跳转到【库存表】中选择显示器，显示器名称将回显到【固定资产申请表】中。 

 {{</ alert >}}

## 字段属性

![associated_data](/images/manual/component/associated_data.png)

请根据实际需要配置字段的以下属性：

- 标题名称：字段名称，必填；
- 占位提示：如有需要请填写；
- 描述内容：如有需要请填写；
- 字段属性：支持设置成普通、只读，默认为普通；
- 是否必填：可选择字段是否必填，默认非必填；
- 关联记录表：选择关联记录表，目前仅支持选择本应用的其他表单；
- 显示字段：选择需显示的关联表中字段，不支持选择附件、图片、子表单、关联记录、关联数据；
- 数据过滤规则：设置关联记录表的可选数据范围，目前仅支持设置一条过滤规则。

{{< alert warning >}}

**注意**

数据过滤规则的可选数据范围必须遵循原表单的权限设计。

 {{</ alert >}}



## 关联数据与关联记录的区别

- 关联数据组件用于关联其他表的字段值。

- 关联记录组件用于关联其他表的数据。
