---
title: "Approval Node"
description: "QuanXiang Cloud Platform Workflow: Introduction to Approval Nodes"
linkTitle: "Approval Node"
weight: 44210
---

When the workflow involves the approval function, you need to use the approval node to change the data status after the approval or rejection. Support "or-sign" and "counter-sign" when multiple people are approving.

## Explanation of terms

**or-sign**: One approval node sets multiple approvers. Approval by any one of them can pass approval.

**counter-sign**: One approval node sets multiple approvers. Requires approval from all to pass approval.

## Config steps

### 1 Add Approval Node

Click **+** in the workflow and drag **Approval Component** into the workflow from the component set that pops up.

{{< alert tip >}}

**Instruction**

The approval node supports renaming, click the node name **approval** to rename it.

![approval1](/images/manual/workflow/node/approval/approval1.png)

{{</ alert >}}

### 2 Add basic configuration

#### Add Approver

Approver support selection: designated person, form field, supervisor, department head, and process initiator.

- Designated person: Click **Add Approver** to set the approver, and support designating a single person or multiple persons for approval.
- Form Fields: Users can customize the approver, currently the form fields only support the person selector field.
- Supervisor: Designate the supervisor as the approver.
- Department Head: Designate the department head as the approver.
- Process initiator: Designate the process initiator as the approver.

![approval2](/images/manual/workflow/node/approval/approval2.png)



#### Set approval rules

Complete the following approval rule settings based on business requirements:

- Multi-approval: Support to select "or-sign" and " counter-sign".

- When there is no approver: Support the option to automatically skip the node and transfer it to the administrator.

- Automatic approval rules: Support presetting the following scenarios, and the system automatically completes the approval when the presets are met.
  - When the approver is the initiator.
  - When the current approver is the same as the approver of the previous node.
  - When the current approver is the same as the predecessor node approver.
  
- Approval time limit: You can set the approval timeout rule when you turn it on.

  - Time limit: Turn on approval timekeeping after the process first enters the node or after the workflow starts.

  - Reminder: You can set early reminder and repeat reminder.

  - Dealing rules after timeout: support no deal, automatic deal (automatic pass or reject), jump to other nodes.

    ![approval3](/images/manual/workflow/node/approval/approval3.png)

{{< alert tip >}}

**Instruction**

Jump to other nodes: Support re-triggering the process, ending the process, or jumping to any action node of the workflow.

{{</ alert >}}

### 3 Set field permissions

QuanXiang Cloud Platform supports separate front-end and back-end permission settings, and you can set form field permissions in the field permissions tab.

- Supports front-end display styles for configuring fields: read-only, edit, and hide.
- The back-end read and write function is turned on by default, if you want to modify it, please click **Data permission modification**. When back-end read or write is turned off, users of this node will not be able to read database data or write data. The vulnerability of calling interface to change data is blocked.

{{< alert tip >}}

**Instruction**

<li>Custom fields support assigning values to fields and setting data modification permissions. System fields only support setting read-only permissions.<li>If the process form contains a sub-table and the sub-table is hidden, then the fields within the sub-table are only supported to be set hidden.

{{</ alert >}}

![approval4](/images/manual/workflow/node/approval/approval4.png)

### 4 Set operation permissions

In the operation permission tab, you can set the operations that can be performed by the person in charge of the node when handling the workflow. In addition to the default pass and reject operations, the QuanXiang Cloud system also supports defining: fallback, play back and refill, add signature, transfer, copy, and invite to review, which can be adapted to more complex business scenarios. See below for more details: **Operation permission parameter description**.

Translated with www.DeepL.com/Translator (free version)

![approval5](/images/manual/workflow/node/approval/approval5.png)

## Description of operating authority parameters

### Fallback

Backing up workflow tasks to nodes that have already been flowed, without interrupting the task except for the start node. Support to select the fallback node, and fill in the fallback reason when fallback the process.

![approval6](/images/manual/workflow/node/approval/approval6.png)

### Play back and refill

The workflow task will be played back to the initial node, and the initiator will continue the process after refilling, without interrupting the task, and need to fill in the reason for playing back and refilling.

![approval7](/images/manual/workflow/node/approval/approval7.png)

### Add signature

Support adding signatures before and after this node. When multiple people are approving, it supports selecting "or-sign" and "counter-sign".

![approval8](/images/manual/workflow/node/approval/approval8.png)

### Transfer

Transferring workflow tasks to other people, only one person is supported, and you need to enter the reason for the transfer.

![approval9](/images/manual/workflow/node/approval/approval9.png)

### Copy

Copy workflow tasks to other people, support copy to multiple people, you can enter the reason for copy.

![approval10](/images/manual/workflow/node/approval/approval10.png)

The copy task will be displayed in **Copy to Me**, you can click into the process to see the details.

![approval11](/images/manual/workflow/node/approval/approval11.png)

### Invite to review

Add reviewers for workflow tasks, support multiple reviewers, and enter the reason for review.

![approval12](/images/manual/workflow/node/approval/approval12.png)

The tasks will be displayed in **to do** and can be reviewed by clicking on the process details.

![approval13](/images/manual/workflow/node/approval/approval13.png)
