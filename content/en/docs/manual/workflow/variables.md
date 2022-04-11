---
title: "Workflow Variables"
description: "Introduction to workflow variable definition and usage scenarios"
linkTitle: "Workflow Variables"
weight: 4440
---

Workflow variables are used to define parameter objects, which can hold the value of a field, the result of an arithmetic node, or receive the value passed in the process and then referenced by other nodes in the process.

- The parameter object data type currently supports: text type, numeric type, boolean type, and date type.
- Workflow variables are referenced as intermediate parameters in the Data Add node, the Data Update node, and the Change Process Parameters node.


{{< alert tip >}}

**Instruction**

The system variables include: process initiator, process initiation time, and process status.

{{</ alert >}}

## Config Portal

**Workflow** > **Workflow Variables**.

![variables1](/images/manual/workflow/variables1.png)

## Config Process

Click **Add Variable** to add the variable. Click **Confirm Add** after filling in the information.

- Variable name: Required, named according to the role of parameters, need to be concise and clear.

- Variable type: Required, supports text type, numeric type, boolean type, date type.

- Default value: Optional.

  ![variables2](/images/manual/workflow/variables2.png)
