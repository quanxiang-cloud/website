---
title: "Sign up"
description: "Help you quickly register your account"
linkTitle: "Sign up"
weight: 2200
---

QuanXiang Cloud Platform account registration form according to the user role classification:

- **Administrator**: Visit QuanXiang Cloud Platform, and then complete the main account registration according to the page guide.

- **Ordinary member**: You can assign the platform account by contacting the administrator.  The platform provides a variety of account allocation methods to help enterprises quickly complete the construction of the organization.

{{< alert tip >}}

**Instruction**

For account security, it is highly recommended that you change your password after logging into the console for the first time. To change your password, please click on the top right corner of the platform **Personal Center** > **Reset Password**.

{{</ alert >}}

## Assign Account

### Account assignment portal

Administrator account login [Admin Side](https://portal.quanxiang.dev), click **Access Control** > **Enterprise Address Book** to assign platform account for enterprise employees. Allocation methods support: **excel batch import**, **single add employee**.

![registration1](/images/quick_start/registration1.png)

### Account assignment process

#### 1 excel batch import

Click **excel batch import** on the enterprise address book management page to import enterprise employee information with one click using excel batch import. The information you can import includes: employee name, cell phone number, email address, etc.

{{< alert tip >}}

**Instruction**

Please download the template for importing corporate address book first, then fill in and upload it correctly. The platform supports importing xls and xlsx format templates.

{{</ alert >}}

![registration2](/images/quick_start/registration2.png)

#### 2 single add employee

If you only need to enter the information of a certain employee, click **Enterprise Address Book Management Page** > **Add Employee** to import the information. Please follow the instructions on the page to complete the information.

- Employee information includes: employee name, cell phone number, email, department, immediate supervisor, and position.
- Employee account initial password sending methods are supported: via email, via SMS.

{{< alert tip >}}

**Instruction**<br>

1. Cell phone number/email, at least one required.<br>
2. Employee departments and immediate supervisors support direct correlation access.

 {{</ alert >}}

![registration3](/images/quick_start/registration3.png)



#### 3 Employee Information Management

Administrators can click **Employee Information Action Column** > **Capsule Button** to manage employee information, which is currently supported as follows:

- Modify employee information: Support to modify employee name, immediate supervisor and position.
- Set as supervisor: After the employee is set as supervisor, he/she will have the process approval authority.
  - 取消主管：员工若职业变更，可点击取消主管，取消主管后员工不在拥有主管的流程审批权限。
- Reset password: The system will automatically generate a random password and send it to the employee, the reset password can be sent via email or SMS. It is commonly used when the employee's account is locked after 5 failed login attempts.
- Disable Account: Once the account is disabled, employees will be unable to log in to the platform.
- Remove Account: Once the account is deleted, the employee data cannot be recovered within the platform, so you need to confirm whether to remove it.

![registration4](/images/quick_start/registration4.png)

#### 4 Export employee data

Administrators can click the capsule button on the right side of the added employee information, and the export format is ".xlsx". And support to choose export department.

![registration5](/images/quick_start/registration5.png)

## Manage account permissions

### Permission assignment portal

The administrator account logs into [Platform Admin](https://portal.quanxiang.dev) and clicks **Access Control** > **Role Management** to assign the required platform privileges to the enterprise employee account.



### Permission Management Process

Administrators can manage enterprise role permissions by simply clicking **Associated Employees and Departments** under the corresponding role list. Example of administration is as follows:

1. To add a viewing role for Enterprise Employee A, simply go to **Role List** > **Viewers** > **Associated Employees and Departments** and click it.

   ![registration6](/images/quick_start/registration6.png)

2. Enter the role association details page, the platform supports **by employee** and **by role** management account permissions. Among them, it supports searching employee's name by employee tab. Click **Confirm association** to grant employees access to the platform.

3. If you need to remove the employee's viewing privileges after a job change, just click the **Capsule button** in the step 1 image to cancel the association.

{{< alert tip >}}

**Instruction**

If you have any questions during the management process, please click **How to manage roles** in the upper right corner to view the reference document.

{{</ alert >}}

