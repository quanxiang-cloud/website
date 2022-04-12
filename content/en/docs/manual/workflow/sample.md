---
title: "Workflow Example"
description: "Workflow development example"
linkTitle: "Workflow Example"
weight: 4406
---

QuanXiang Cloud can design and develop some processes to handle complex work based on workflow functionality. Process development can be divided into business process design and automated process design.

- Business process mainly refers to the process related to human operation. For example, the leave approval process or the administrative approval process in the approval flow.
- Automated processes are mainly processes that are executed automatically by the system. For example, the process of sending emails or the process of notifying results.

## Business Process Design

In the design of workflow, there are many scenarios that require human participation in the business flow. Here, take the approval flow as an example, and create a workflow to perform leave approval work.

1. Select the triggered worksheet in the workflow and choose the desired trigger method. For details of the process, refer to: [trigger node](../trigger/).

2. Add an approval node in the next node, change the name to "Approval by higher level" node, configure the approver as the higher level leader, and configure the corresponding field permissions, then save the node.

   ![sample1](/images/manual/workflow/sample1.png)

The flow of this workflow is: fill out the work form to trigger the process > higher level for approval > approval completed process ends.

When building business processes, workflows also provide fill-in nodes that enable users to fill in form fields in the approval workflow.

## Automatic process design

In the design of workflow, there are some scenarios that need to be handled automatically by the system, such as: automatic sending of in-site mail, email, data update form data and Webhook call API scenarios. This section takes the information notification flow as an example to build a workflow to carry out the system notification work.

1. Select the worksheet to be triggered in the workflow and choose the desired trigger method, for details of the process see: [trigger node](../trigger/).

2. Add a data update node in the next node, then add a station letter node, and after configuring the corresponding node settings, a simple system notification process is complete.

   ![sample2](/images/manual/workflow/sample2.png)

The flow of the workflow is as follows: Fill in the worksheet to trigger the process > Update the form data > System message indicates that the update is successful > End of the process.
