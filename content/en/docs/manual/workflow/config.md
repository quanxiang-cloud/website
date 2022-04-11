---
title: "Global Config"
description: "Introduction to Workflow Global Configuration"
linkTitle: "Global Config"
weight: 4430
---

The global configuration of the workflow can be customized for the entire process, and the global configuration items currently supported by the QuanXiang Cloud Platform are shown below.For detailed configuration process and client-side examples, please refer to [Configuration Item Description](#Configuration Item Description).

- Allow withdrawal: Allow the initiator to withdraw the workflow after the process is initiated. Effectively avoid error workflows.
- Allow initiator reminder: After the process initiator reminds the reminder, the reminder information will be displayed on the reminded person [Access Side](https://home.quanxiang.dev) > **Pending Items** > **Reminder**.
- Allow to view workflow status and messages: The right side of the workflow shows the process status and message information in real time.
- Allow node leaders to leave messages: When opened, node leaders can leave messages to enhance process interactivity and advance progress.
- Process instance title: The process title is instantiated to show the key information of the process directly and distinguish it from other processes.
- Process Summary: Select the process key field to directly display the key information of the process and distinguish it from other processes.

{{< alert tip >}}

**Instruction**

Process instance titles are usually used in conjunction with process summaries.

{{</ alert >}}

## Config Portal

**Workflow** > **Global Config**

![config1](/images/manual/workflow/config1.png)

## Config Descrption

### Allow withdrawal after process initiation

1. Config process:

   Click the Enable button in the configuration portal to enable the withdrawal function. After the workflow is triggered, allow the process initiator to withdraw the process.

2. How users can withdraw the process:

   Users only need to click [Visit Side](https://home.quanxiang.dev)> **I initiated** > **Process to be withdrawn**, enter the process details and click **Withdraw** to complete the withdrawal of the process.



### Allow workflow initiator reminders

1. Config process:

   Click the Enable button in the configuration portal to enable the reminder function. After the workflow is triggered, the process initiator is allowed to make a reminder. After a reminder is initiated, the reminder information will be displayed on the reminded person [Access Side](https://home.quanxiang.dev) > **Pending Items** > **Reminder**.

2. How the user initiates a reminder:

   Users only need to click [Access Side](https://home.quanxiang.dev) > **I initiated** > **Processes that need to be reminded**, go to the process details and click **Remind** to complete the withdrawal of the process.



### Allow viewing of workflow status and messages

1. Config process:

   Click the Enable button in the configuration portal to enable the viewing function. After the workflow is triggered, allow the process participants to view the workflow process and messages in real time.

2. How users can view workflow status and messages:

   Users just need to click [Access Side](https://home.quanxiang.dev) > **I initiated** > **Process needs to be viewed** to enter the process details, and the process status is displayed on the right side of the process.

   ![config2](/images/manual/workflow/config2.png)

### Allow the node leader to leave a message

1. Config process:

   Click the Enable button in the configuration portal to enable the message function. After the workflow is triggered, the node leader is allowed to leave a message to enhance process interactivity and advance progress.

2. How users can leave messages:

   Users only need to click [Access Side](https://home.quanxiang.dev) > **I initiated** > **Process need to see**, enter the process details, and click **Discussion** on the right side of the process to leave a message.

   ![config2](/images/manual/workflow/config2.png)

### Process instance title

1. Config process:

   Instantiate the process title in the configuration portal, the instance title needs to be concise and clear.

2. How users can view the process instance title:

   Users only need to click on [Access Side](https://home.quanxiang.dev) > **My Application** > **All** and the process title will be displayed after the user name.

### Process Summary

1. Config process:

   Select Process Summary in the configuration portal. Process Summary supports configuration of all fields of this form.

2. How users can view the process summary:

   Users only need to click on [Access Side](https://home.quanxiang.dev) > **My Application** > **All** and the process summary information will be displayed on the right side of the process.

