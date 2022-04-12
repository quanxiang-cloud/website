---
title: "Form Attributes"
description: "Form attributes introduction and basic setup process description"
keywords: "Field title position, Field show/hide rules, Form submission validation rules"
linkTitle: "Form Attributes"
weight: 4230
---

Form attributes are global settings for the form, as opposed to setting individual fields.

QuanXiang Cloud Platform currently supports setting: field title position, field show/hide rules, and form submission validation rules. Please look forward to more global configuration rules for forms.

## Operation steps

Setting portal: **Form Design** > **Form Configuration**.

<img src="/images/manual/form/new2.png" alt="new2" style="zoom:80%;" />

### 1 Set field title position

The field title position supports left and right, top and bottom, and the system default setting is left and right. Please choose the field title position according to your actual needs.

{{< alert tip >}}

**Instruction**

The field title position setting supports real-time preview, and the corresponding style is displayed on the left form page immediately after selecting the style.

{{</ alert >}}

{{< alert tip >}}

**Instruction**

The position of field title can be chosen according to the space position of the form: when the vertical space is abundant and the horizontal space is restricted, it is recommended to give priority to the top and bottom structure; when the horizontal space is abundant and the vertical space is restricted, it is recommended to give priority to the left and right structure.

{{</ alert >}}

### 2 Set the field show/hide rules

Click on **+ show/hide rules** to immediately configure form field show/hide rules. Supports setting a merge-set (when all conditions are met), or-set (when any condition is met).

1. Select field show/hide rule base configuration.
   - merge-set: fields are shown (hidden) when all conditions are met.
   - or-set: fields are shown (hidden) when any of the conditions are met.
2. Configuring the condition sheets according to business requirements.
3. Set the field to show or hide.

![attributes](/images/manual/form/attributes.png)

### 3 Set form submission validation rules

When the form submission validation rules are met, the data will be submitted; if not, the form will not support submission and an error message will be prompted.

1. Fill in the name of the rule: set up according to business needs and set up principles that are easy to understand.
2. Select the form fields to be validated.
3. Set up form validation formulas that combine comparison symbols and functions to configure form validation formulas. The currently supported comparison symbols and functions are as follows:

{{<table >}}
| not equal | equal | Include | not include | less | less or equal | more | more or equal |
| ------ | ---- | ---- | ------ | ---- | -------- | ---- | -------- |
| !=     | ==   | ∈    | ∉      | <    | ≤        | >    | ≥        |
{{</table >}}
4. Set error alert: If the form submission does not meet the validation rules, the corresponding alert will be displayed.

