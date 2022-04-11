---
title: "Data addition node"
description: "QuanXiang Cloud Platform Workflow: Introduction to data addition nodes"
linkTitle: "Data addition node"
weight: 44220
---

The Data addition node is used to automatically add a new row to the specified worksheet.



## Application Scenario

- When a new record is added to the worksheet [Contacts], the corresponding lead record is automatically added to the worksheet [Sales Leads].

- When a new record is added to the worksheet [Leave Request], the corresponding leave record is automatically added to the worksheet [Leave Request Statistics].




## Config steps

### 1 Add data addition node

Click **+** in the workflow and drag **Data Addition Component** into the workflow from the pop-up component set.

{{< alert tip >}}

**Instruction**

Data addition node supports renaming, click **Data addition** to rename.

{{</ alert >}}



### 2 Add basic configuration

#### Select target data sheet

Select the target data sheet according to business requirements, and switch data sheets are supported in process design.

{{< alert warning >}}

**Attention**

After switching the data sheet, the configuration added by the original data will be cleared, please confirm and switch.

 {{</ alert >}}

![insert1](/images/manual/workflow/insert1.png)

#### Set whether form data triggers workflow execution

Set the relationship between form data and triggered workflow execution according to business requirements. The system is checked by default.

{{< alert tip >}}

**Example**

For the worksheet [Leave Statistics], whether you need to review the data after it is generated is determined by the company's business. If it is a relatively simple statistics, there is no need to trigger the workflow; if it is a calculation with amount, then it needs to be reviewed.

{{</ alert >}}



#### Set worksheet record addition logic

Worksheet fields are displayed by default according to the target data sheet fields. You can define the logic for adding worksheet data in three ways: field values, customization, and process variables.

- Field value: select the corresponding field in the target data sheet.
- Customization: only numerical customization is currently supported.
- Process variables: need to be defined in workflow variables in advance, and can be referenced directly after they are defined. The definition rules see: [Workflow Variables](../../../../manual/workflow/variables/)。

![insert2](/images/manual/workflow/insert2.png)



