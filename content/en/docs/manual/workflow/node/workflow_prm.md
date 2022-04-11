---
title: "Change process parameter node"
description: "QuanXiang Cloud Platform Workflow: Introduction of Change Process Parameters Node"
linkTitle: "Change process parameter node"
weight: 44222
---

The Change Process Parameters node is used to define a parameter object in a business process. A parameter can hold the value of a field, the result of an arithmetic node, or receive a value passed in the process that is then referenced by other nodes in the process.

## Explanation of terms

Process parameters: The data source is workflow variables, and the process of defining workflow variables is described in [Workflow Variables](../../../../manual/workflow/variables/)。



## config steps

### 1 Add change process parameter node

Click **+** in the workflow and drag **Change Process Parameters component** to the workflow in the pop-up component set. If you don't have a process parameter to assign, please click **Workflow Variables** on the left side of the page to add it first.

![workflow_prm1](/images/manual/workflow/workflow_prm1.png)

{{< alert tip >}}

**Instruction**

The Change Process Parameters node supports renaming, click on the node name **Change Process Parameters** to rename it.

{{</ alert >}}

### 2 Add basic config

#### Add process parameters

Click **New Assignment Rules** to select process parameters and set process parameter data logic. Supports configuration of **form values**, **fixed values**.

- Form Value: Support for selecting worksheet fields.
- Fixed value: support data type as text type, numeric type, boolean type, date type.

![workflow_prm2](/images/manual/workflow/workflow_prm2.png)









