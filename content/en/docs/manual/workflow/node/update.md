---
title: "Data Update Node"
description: "QuanXiang Cloud Platform Workflow: Introduction to Data Update Node."
linkTitle: "Data Update Node"
weight: 44221
---

The data update node is used in business processes to update the value of one or more fields in a record. It supports updating fields in this form or associating fields in other forms.

## Application Scenario

- In the worksheet [Product Inventory], the inventory value of the current product in the inventory record is automatically reduced when the product is discharged.
- In the worksheet [Return Order Details], if the return request is approved, the product inventory value recorded in the worksheet [Product Inventory] will be updated.

## config steps

### 1 Add data update node

Click **+** in the workflow and drag **Data Update Component** into the workflow from the pop-up component set.

{{< alert tip >}}

**Instruction**

The data update node supports renaming, click the node name **Data Update** to rename it.

{{</ alert >}}

### 2 Add basic config

#### Select target data sheet

Select target data sheet according to business requirements. Switching data tables is supported in process design.

{{< alert warning >}}

**Attention**

After switching the data sheet, the configuration of the original data update will be cleared, please confirm and switch.

 {{</ alert >}}

![update1](/images/manual/workflow/update1.png)

#### Set whether form data triggers workflow execution

Set the relationship between form data and triggered workflow execution according to business requirements. The system is checked by default.

{{< alert tip >}}

**Example**

For the worksheet [Leave Statistics], whether you need to review the data after it is generated is determined by the company's business. If it is a relatively simple statistics, there is no need to trigger the workflow; if it is a calculation with amount, then it needs to be reviewed.

{{</ alert >}}

#### Set filter conditions

1. Select a filter condition relationship: satisfies all, any of the following.

2. Define the target field and support defining {equal to, not equal to, contains, does not contain}.

   ![update2](/images/manual/workflow/update2.png)

#### Set update rules

1. Select the target table to update the fields.
2. Set field update rules: Support setting field values, customization, formula calculation, and process variables.
   - Field value: select the corresponding field in the current data sheet.

   - Customization: value customization.

   - Formula calculation: support for editing formulas to set update rules.

   - Process variables: need to be defined in workflow variables in advance, and can be referenced directly after they are defined. Definition rules see: [Workflow Variables](../../../../manual/workflow/variables/)。

     ![update3](/images/manual/workflow/update3.png)



