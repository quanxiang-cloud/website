---
title: "Create Workflow"
description: "How to create workflows with QuanXiang Cloud Platform"
linkTitle: "Create Workflow"
weight: 4405
---

## Define

The workflow is composed of a trigger and multiple action node sequences. The workflow trigger method of QuanXiang Cloud Platform currently contains: worksheet trigger and work time trigger. In the action node, you can realize the operation of data query, update, locate, delete, etc.; you can also execute the manual control process such as approval and filling.

- **Trigger**: A switch to see if the workflow can be started. The process is automatically started when the conditions of the trigger are met.
- **Action Node**: The operation that is automatically executed in the process, the platform currently only supports filling and approval actions.



## Create Workflow

The workflow creation process is divided into the following steps.

<img src="/images/manual/workflow/workflow1.png" alt="workflow1" style="zoom:67%;" />

### Choose a workflow trigger method

1. To create a workflow, you need to go to the application management details page and click **Workflow** > **New Workflow** > **Worksheet Trigger**.
   - **Worksheet Trigger**: Triggered when a new record is added to a worksheet or when a change (update, delete) is made to an existing record.

![new1](/images/manual/workflow/new1.png)

{{< alert tip >}}

**Instruction**

Adding or deleting in a worksheet trigger refers to records, not to adding or clearing field values: <br>1 If the value of a field in an existing row was originally empty, and a new value is entered, the event is an update event rather than a add event.<br>2 If clearing the value of a field is an update event, not a delete event.

{{</ alert >}}

2. Click the Edit button to fill in the workflow name.

   <img src="/images/manual/workflow/new2.png" alt="new2" style="zoom:80%;" />

3. Select the corresponding worksheet and set the trigger method and trigger conditions.

   ![new3](/images/manual/workflow/new3.png)

### Design function nodes

1. Select the node function and pull into the workflow by dragging and dropping: you can achieve data addition, update and other operations by **Data Add**, **Data Update** nodes; you can also create **Approve**, **Fill** nodes to perform manual control processes such as approval and filling.
2. According to the page prompts to complete the information configuration of the function node, the function node configuration details steps and notes see: [Action Node](... /... /... /... /manual/workflow/node/).

![new4](/images/manual/workflow/new4.png)

{{< alert warning >}}

**Attention**

After each information configuration, please click **SAVE** to avoid the loss of the filled data.

 {{</ alert >}}

### Global Config

After the workflow design is completed, please click **Global Config** to configure the process. For detailed configuration process and more notes, see: [Global Config](... /... /... /... /manual/workflow/config/).

 ![new5](/images/manual/workflow/new5.png)

### Workflow Variable

Workflow variables are used to store a field value, a calculation result, or to receive values passed in other processes and then referenced by other nodes. For a detailed configuration process see: [Workflow Variable](../../../../manual/workflow/variables/).

![new6](/images/manual/workflow/new6.png)



## Publish Process

Once the workflow design is complete, click **Publish** for the process to take effect.

{{< alert tip >}}

**Instruction**

If you need to modify the workflow after it is published, please click **Downgrade** first. Workflows can be designed and optimized after they are taken down. The workflow will be invalidated and cannot be triggered after it is taken down; the triggered data is not affected.

{{</ alert >}}

## Test Process

Log in to [Access Side](https://home.quanxiang.dev) and verify that the workflow is executed correctly.

