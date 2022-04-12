---
title: "Branch Nodes"
description: "QuanXiang Cloud Platform Workflow: Introduction to Branch Nodes"
linkTitle: "Branch Nodes"
weight: 44231
---

After setting the branch node, the data of the parent node will flow to different branches according to the filtering conditions, and when all branch nodes are executed, the aggregation will enter the common child node.

## Config steps

### 1 Add branch node

Click **+** in the workflow and drag **Branch component** to the workflow from the pop-up component set. The branch component has two branches by default, if you want to add more branches, click **Branch+**.

![branch](/images/manual/workflow/branch.png)

{{< alert tip >}}

**Instruction**

Branch nodes support renaming, click **Filter Criteria Settings** to rename.

{{</ alert >}}

### 2 Add filter criteria

Branch node filtering conditions support custom conditions, else conditions. Custom conditions support current form fields and process variable fields. The filter condition currently only supports defining the current form field filter condition.

- Custom conditions: meet the filtering conditions data into this branch node, you need to define the conditions formula.
- else condition: enter this branch node when all other branches are not satisfied.

<img src="/images/manual/workflow/branch1.png" alt="branch1" style="zoom:80%;" />

{{< alert warning >}}

**Instruction**

When the data flow does not satisfy any branch node, the whole process is automatically ended and the process status is: **Abnormally ended**.

 {{</ alert >}}

### 3 Set the next node of a branch node

After setting the branch filtering conditions, you can set the next node in the branch to execute the action. Click **+** under the branch to drag **action component** into the branch from the pop-up component set.

### 4 Delete branch (optional)

- When a branch is more than two, delete a branch condition node and the whole branch will be deleted. The other branches do not change.

- When the branch is equal to two, delete a branch condition node and the whole branch will be deleted. The other branch removes the filter condition and only the subsequent nodes are retained.



