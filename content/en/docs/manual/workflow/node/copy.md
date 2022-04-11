---
title: "Copy Node"
description: "QuanXiang Cloud Platform workflow: copy node introduction"
linkTitle: "Copy Node"
weight: 44214
---

The Copy node is used in business processes where members need to know the process information. After the copy event is triggered, the copied person will receive the copy information in [Access Side](https://home.quanxiang.dev) > **Copy to Me** in real time. Unlike the approval node, the copied member only needs to read or view it.

## Application Scenario

After the approval of leave request in the worksheet [Leave Request], add a copy for the leave seeker's leader or business-related cooperative members. Timely inform the relevant members of the leave information.

## Config steps

### 1 Add copy node

Click **+** in the workflow and drag **Copy component** into the workflow from the popup component set.

{{< alert tip >}}

**Instruction**

The copy node supports renaming, click **Copy** to rename it.

{{</ alert >}}

### 2 Add basic configuration

#### Add copy person

The recipients of the copy support the selection of: designated person, form field, supervisor, department head, and process initiator.

- Designated person: Click **Add recipient** to set the recipient.
- Form Fields: User can customize the receiving object, currently the form fields only support the person selector field.
- Supervisors: Designate supervisors as the recipients.
- Department Head: Designate the department head as the recipient.
- Process initiator: Designate the process initiator as the recipient.

![copy1](/images/manual/workflow/node/copy1.png)

{{< alert tip >}}

**Instruction**

You can set multiple recipients for the message.

{{</ alert >}}





