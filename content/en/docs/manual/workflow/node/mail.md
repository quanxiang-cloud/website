---
title: "Mail Node"
description: "QuanXiang Cloud Platform workflow: send email node introduction"
linkTitle: "Mail Node"
weight: 44213
---

The Send mail node is used to send emails to the specified email address in the workflow, and emails are automatically sent after the process is triggered. The content of the email supports dynamic filling, by way of form field selection.



## Application Scenario

When the leave approval in the worksheet [Leave Request] is approved, an approved notification email is automatically sent to the leave seeker.



## Config steps

### 1 Add send mail node

Click **+** in the workflow and drag **Send Email Component** into the workflow from the pop-up component set.

{{< alert tip >}}

**Instruction**

The send mail node supports renaming, click **Send Mail** to rename it.

{{</ alert >}}

### 2 Add basic configuration

#### Add recipient

Mail recipients support the selection of: designated person, form field, supervisor, department head, and process initiator.

- Designated person: Click **Add recipient** to set the recipient.
- Form Fields: User can customize the recipients, currently the form fields only support the person selector field.
- Supervisors: Designate supervisors as the recipients.
- Department Head: Designate the department head as the recipient.
- Process initiator: Designate the process initiator as the recipient.

After selecting the recipient, **the system automatically matches the recipient's mailbox account** and automatically sends the email content to the corresponding mailbox when the process is triggered.

![mail1](/images/manual/workflow/node/mail1.png)

{{< alert tip >}}

**Instruction**

You can set multiple recipients for the message.

{{</ alert >}}

#### Set email subject

Set the email subject according to the content of the email, and the subject should be concise and clear.

#### Mail body

The content of the email body can be expressed in various ways, such as adding hyperlinks, inline web pages, dynamic filling, etc. Dynamic filling is done by form field selection.

{{< alert tip >}}

**Example**

Send an email node in the worksheet [Purchase Request] dynamically set the applicant. After the purchase request is approved, a notification email is automatically sent to the applicant that it has been approved.

{{</ alert >}}

![mail2](/images/manual/workflow/node/mail2.png)

#### Add Attachment

Click upload to add attachments. Multiple attachment uploads are supported.











