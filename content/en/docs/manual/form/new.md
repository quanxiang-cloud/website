---
title: "Create Form"
description: "How to create a new form through QuanXiang Cloud Platform"
linkTitle: "Create Form"
weight: 4205
---

## Define

In QuanXiang Cloud Platform you can build data table models through form visualization and correspond directly to field types through controls. Implement the necessary relational data structures through linked sheets, linked sheet fields and summaries.

## Explanation of terms

- **Component**: For the specification and correct input of field data, the QuanXiang Cloud system pre-sets some formatted field types.
- **Field**: A single piece of data in a data sheet that stores data for a certain attribute, such as: name, age, address, etc.
- **Sheet**: Used to store and manage various business object data in enterprise activities. You can securely store and manage this data in the QuanXiang Cloud Platform.
- **Record**: When a data sheet is completed, a record is generated that contains data from multiple fields in the sheet.

## Usage Scenario

Forms are widely used in business data collection scenarios. For example: employee forms, customer forms, order forms, sales forms, inventory forms, product forms, work order forms, etc.



## Operation steps

### 1 Create Form

After the application page is created, click **New Form** to create the form required for your business. By dragging and dropping the form components on the left and configuring the field properties, you can complete the basic construction of the form.

![new1](/images/manual/form/new1.png)

### 2 Config form properties

Form properties currently support configuration: field title position, field show/hide rules, form submission validation rules.

Configuration portal: **Form Design** > **Form Configuration**. Please complete the form configuration according to the requirements and page guidelines, for more configuration steps and notes, please refer to [Form Properties](../../../../manual/form/attributes/)。

<img src="/images/manual/form/new2.png" alt="new2" style="zoom:80%;" />

### 3 Config form page

After the field design is completed, click **Page Configuration** to design the form page, and complete the form style settings according to the page guidelines, for more details, see [Page Configuration](../../../../manual/form/design/). Click **Save Page Configuration** when the settings are completed.

![new4](/images/manual/form/new4.png)

{{< alert tip >}}

**Instruction**

The page configuration supports real-time preview, and the form page can be previewed in real time on the left after the right configuration item is started.

{{</ alert >}}

### 4 Preview and save form

1. After the form page is configured, click **Preview** to preview the form and support mock form submission. The data will be displayed directly after the form is submitted.

   ![new3](/images/manual/form/new3.png)

2. Once the preview is correct, click **Save Form** to save the form.

   {{< alert tip >}}

   **Instruction**

   Please click Save Form immediately after form design or change design to avoid missing content.

   {{</ alert >}}

### 5 Set form permissions

Form access and data management permissions are designed through the [Access Control](../../../../manual/permission/) module. After configuring form permissions, users can access the form in the workbench and perform actions within the scope of the permissions allowed.

- Configuration portal: [Admin side application management](https://portal.quanxiang.dev/apps) > **Application Specific** > **Access Control**.
- Configuration steps and configuration items are described in detail in [Access Control](../../../../manual/permission/).


{{< alert warning >}}

**Attention**

After adding new fields to the form, you need to reconfigure the form permissions and configure the required permissions for the new fields under the **Configure Access Permissions** tab.

 {{</ alert >}}