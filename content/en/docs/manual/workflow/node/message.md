---
title: "message node"
description: "QuanXiang cloud platform workflow: introduction to message node"
linkTitle: "message node"
weight: 44212
---

The Message node is used for in-app notifications, through which messages can be sent to specified members in the form of system messages or notification announcements. Message content presentation styles are: support for adding hyperlinks, inline web pages, emoji, etc.

## Application Scenario

When a new lead is entered into the worksheet, the marketing department is notified to follow up as soon as possible and the marketing members can view the key notifications in time.

## config steps

### 1 Add message nodes

Click **+** in the workflow, and drag **Message Component** to the workflow from the pop-up component set.

{{< alert tip >}}

**Instruction**

The node can be renamed by clicking on the node name **Message**.

{{</ alert >}}



### 2 Add basic config

#### Add recipient

Message recipients support the selection of: designated person, form field, supervisor, department head, and process initiator.

- Designated person: Click **Add recipient** to set the recipient.
- Form Fields: User can customize the recipients, currently the form fields only support the person selector field.
- Supervisors: Designate supervisors as the recipients.
- Department Head: Designate the department head as the recipient.
- Process initiator: Designate the process initiator as the recipient.

![message1](/images/manual/workflow/node/message1.png)

{{< alert tip >}}

**Instruction**

You can set multiple recipients for the message.

{{</ alert >}}

#### Set message type

Message type support settings: notification announcement, system message.

#### Message Title

Fill in the message title according to the content of the message, the title should be concise and clear.

#### Message content

Message content presentation styles include: support for adding hyperlinks, inline web pages, emoji, etc. Fill in the message content as needed.







