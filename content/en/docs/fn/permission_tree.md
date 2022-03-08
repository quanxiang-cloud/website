---
title: "Role Permission Tree"
description: "The diagram helps you better understand the functional division of different roles in the QuanXiang Cloud Platform"
linkTitle: "Role Permission Tree"
weight: 3100
---

QuanXiang Cloud Platform divides the platform usage rights according to user roles, and divides the system into [Management Side](https://portal.quanxiang.dev) and [Access Side](https://home.quanxiang.dev) to improve user experience.The management side is mainly provided for operation and maintenance or system administrators to use.  The access side is mainly provided to the users who use the application.


- **Super Administrator** and **Administrator** perform system and application management through the management side.
- **Viewers** use the application by logging in to the access side to receive notification messages, view to-do items, and more.

{{< alert tip >}}

**Instruction**

Super Administrator: The default role of the platform, with all functional privileges and all data visible scope of the enterprise by default, and supports the management of other general administrators.

{{</ alert >}}

The role permission tree is shown in the table below.


{{<table >}}
<table>
    <tr>
    <th rowspan="2">Platform Permission</th>
    <th colspan="4">Application Management</th>
    <th colspan="4">Access Control</th>
    <th colspan="2">Platform Settings</th>
    <th colspan="2">System Settings</th>
    <th colspan="1">Operation Log</th>
    <th colspan="4">Dataset</th>
    <th colspan="2">Exception Process</th>
    </tr>
    <tr>
        <td>View Application</td>
        <td>New Application</td>
        <td>Modify Application</td>
        <td>Delete Application</td>
        <td>View Corporate Address Book</td>
        <td>Manage Corporate Address Book</td>
        <td>View Roles</td>
        <td>Manage Roles</td>
        <td>View Platform Settings</td>
        <td>Manage Platform Settings</td>
        <td>View Message</td>
        <td>Manage Message</td>
        <td>View Message</td>
        <td>View</td>
        <td>New</td>
        <td>Modify</td>
        <td>Delete</td>
        <td>View</td>
        <td>Manage</td>
    </tr>
    <tr>
        <td>Super Administrator</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
    </tr>
    <tr>
        <td>Administrator</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅</td>
    </tr>
    <tr>
        <td>Viewer</td>
        <td>✅</td>
        <td></td>
        <td></td>
        <td></td>
        <td>✅</td>
        <td></td>
        <td>✅</td>
        <td></td>
        <td>✅</td>
        <td></td>
        <td>✅</td>
        <td></td>
        <td>✅</td>
        <td>✅</td>
        <td></td>
        <td></td>
        <td></td>
        <td>✅</td>
        <td></td>
    </tr>
</table>
{{</table>}}



