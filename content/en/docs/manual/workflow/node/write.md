---
title: "fill node"
description: "QuanXiang Cloud Platform workflow: fill node introduction"
linkTitle: "fill node"
weight: 44211
---

fill nodes are used in business processes that require certain members to provide field information to advance the process. Set field permissions are supported when fill record content.

## Explanation of terms

**Any fill**: the same node set more than one person to fill in, when one of them **any one** fill in to pass the node.

**Full fill**: the same node set more than one person to fill in, **all responsible persons** fill in before you can pass the node.



## config steps

### 1 Add fill node

Click **+** in the workflow and drag **Fill Component** into the workflow from the pop-up component set.

{{< alert tip >}}

**Instruction**

fill node support renaming, click the node name **fill** to rename.

{{</ alert >}}

### 2 Add basic config

#### Add filler

Filler support: designated person, form field, supervisor, department head, process initiator.

- Designated person: click **Add Filler** to configure filler, support single or multiple people to fill.
- Form Fields: User can customize the filler, currently the form fields only support the person selector field.
- Supervisor: Designate the supervisor as the filler.
- Department Head: Designate the department head as the filler.
- Process initiator: Designate the process initiator as the filler.

![write1](/images/manual/workflow/node/write/write1.png)

#### Set the filling rules

Complete the following fill-in rule settings according to business requirements:

- When multiple people fill in: support the choice of filling in any and all.

- When there is no filler: support the option of automatically skipping the node and forwarding it to the administrator.

- Fill time limit: you can set the fill timeout rule after opening.

  - Time limit: After the process first enters this node, the workflow starts and then turn on filling in the timekeeping.

  - Reminder: You can set early reminder and repeat reminder.

  - Processing rules after timeout: support no processing, automatic processing (automatic pass or reject), jump to other nodes.

    ![write2](/images/manual/workflow/node/write/write2.png)

{{< alert tip >}}

**Instruction**

Jump to other nodes: Support re-triggering the process, ending the process, or jumping to any action node of the workflow.

{{</ alert >}}

### 3 Set field permissions

QuanXiang Cloud Platform supports separated front and back-end permission settings, and you can set form field permissions in the field permissions tab:

- Supports front-end display styles for configuring fields: read-only, edit, and hide.
- The back-end read and write function is turned on by default, if you need to modify it, please click **Data permission modification**. When back-end read or write is turned off, users of this node will not be able to read database data or write data. The vulnerability of calling interface to change data is blocked.

{{< alert tip >}}

**Instruction**

<li>Custom fields support assigning values to fields and setting data modification permissions; system fields only support setting read-only permissions.<li>If the process form contains a sub-table and the sub-table is hidden, then the fields within the sub-table are only supported to be set hidden.

{{</ alert >}}

![write3](/images/manual/workflow/node/write/write3.png)

### 4 Set operation rights

Set the operations that can be performed by the person in charge of the node when handling the workflow in the Operation Permissions tab. In addition to the default submit operation, the QuanXiang Cloud system also supports defining: forward, copy, and invite to review operations, which can be adapted to more complex business scenarios. See below for more details: **Operation permission parameter description**.

Translated with www.DeepL.com/Translator (free version)

![write4](/images/manual/workflow/node/write/write4.png)

## Description of operating authority parameters

### Forward

Transferring workflow tasks to others, only one person is supported, and you can enter the reason for the transfer.

![write5](/images/manual/workflow/node/write/write5.png)

### Copy

Copy workflow tasks to other people, support copy to multiple people, you can enter the reason for copy.

![write6](/images/manual/workflow/node/write/write6.png)

The copy task will be displayed in **Copy to Me**, you can click into the process to see the details.

![write7](/images/manual/workflow/node/write/write7.png)

### Review

Add reviewers for workflow tasks, support multiple reviewers, and enter the reason for review.

![write8](/images/manual/workflow/node/write/write8.png)

The tasks will be displayed in **to do** and can be viewed by clicking on the process details.

![write9](/images/manual/workflow/node/write/write9.png)

