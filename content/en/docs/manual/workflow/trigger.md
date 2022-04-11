---
title: "Trigger Node"
description: "QuanXiang Cloud Platform Trigger Node Introduction"
linkTitle: "Trigger Node"
weight: 4410
---

The trigger node is a switch for workflow initiation and serves as the first node of the process. User-defined trigger rules, records that meet the trigger conditions can trigger the process. QuanXiang Cloud Platform workflow trigger node currently only supports: worksheet trigger.

## Worksheet Trigger

Sheet triggering means that the workflow is always "listening" to a sheet. When data changes occur on this sheet, a series of actions are performed according to predefined rules.

Triggering by worksheet requires 3 points to be configured: the triggering sheet, the triggering method, and the triggering conditions.

![trigger1](/images/manual/workflow/trigger/trigger1.png)

### Trigger Sheet

The worksheet trigger first requires selecting a worksheet.The trigger will "listen" to the recorded data of this sheet and automatically open the workflow when the data is changed in a preset way.

### Trigger Method

Worksheet trigger currently supports the following three trigger methods.

- When adding data: a new record is added to the worksheet, triggering a workflow.
- When modifying data: when the content of existing records in the worksheet is modified, the workflow is triggered, supporting the selection of trigger fields.
- When adding or modifying data: add a new record or modify an existing record in the worksheet, trigger the workflow and support selecting the trigger field.

{{< alert tip >}}

**Instruction**

The workflow is triggered when the specified data in an existing worksheet is modified. If you don't specify the trigger field, the workflow will be triggered by modifying any field by default.

{{</ alert >}}

### Trigger Condition

Filter eligible data into the process. Support adding "and", "or".

![trigger2](/images/manual/workflow/trigger/trigger2.png)



