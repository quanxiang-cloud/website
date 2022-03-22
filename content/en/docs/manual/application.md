---
title: "Create Application"
description: "How to use QuanXiang Cloud Platform quickly build applications"
linkTitle: "Create Application"
weight: 4100
---

An application is a business management system consisting of several forms, workflows, reports, and custom pages. The platform currently supports only user-defined applications, and will support creating applications from template applications in the future.

QuanXiang Cloud Platform application management includes application full life cycle management: **application creation**, **application release**, **application offline** and other process management.



## Create portal

Log in to [QuanXiang Cloud Console](https://portal.quanxiang.dev) and click **Application Management** > **My Applications** > **New Application**.

![application1](/images/manual/application/application1.png)



## Create Application

The detailed steps for application creation are as follows:

### 1 New Application

1. On the My Apps page, click **New App** to start building a dedicated app.

2. According to the page prompts and application building requirements to complete the application base configuration, click **OK** to complete the new application.

   - Application name: The application name will be revealed in scenarios such as authorization and sharing, so please fill in accurately.

   - Application icon: represents the application and supports configuring the background color of the application icon.

     ![application2](/images/manual/application/application2.png)

{{< alert tip >}}

**Instruction**

To modify the application information, you can go to **Application Details Page** > **Application Management** > **Application Information** to modify the information.

{{</ alert >}}

### 2 Create application page

Usually an application consists of different application pages, each of which can implement different functions. After the application is created, the system creates the example page in the navigation column by default. Click **Navigation Bar** > **Add Page** to create the application page.

The application page supports creating forms, custom pages, etc. For detailed design process, please refer to: [Form Design](../../manual/form/), [Create custom page](../../manual/custom/page_design/new/), [upload static page](../../manual/custom_page/).

![application3](/images/manual/application/application3.png)

{{< alert tip >}}

**Instruction**

The application menu page supports group management, making it easy for developers to build application hierarchies and for users to quickly locate the functions they want to use.

{{</ alert >}}

### 3 Create workflow (optional)

1. After the form page is designed, go back to the application details page and click **Associated Workflow** or click **Workflow** on the left navigation bar to jump to the workflow management page.

   ![application4](/images/manual/application/application4.png)

   {{< alert tip >}}

   **Instruction**

   Only form page associated workflows are currently supported.

   {{</ alert >}}

2. Click **New Workflow**, for details see: [Workflow Management](https://docs.clouden.io/manual/workflow/).



### 4 Configuring Application Access Rights

1. After the application page design is completed, you need to configure the application page rights, click **Form Page/Custom Page** > **Authorized Role**, or click **Access Control** on the left navigation bar to jump to the application rights management page.

   ![application5](/images/manual/application/application5.png)

2. Application rights management is divided into access-side rights and management-side rights, for detailed configuration steps see: [Access Control](../../manual/permission/).

## Publish Application

After the application form is configured, the developer can click **Publish Application** in the upper right corner of the application. After the application is successfully published, you can click **Access Application Side** to view the published application. At this time, users with access rights can also access this application.

![app_modeling9](/images/quick_start/app_modeling9.png)

{{< alert tip >}}

**Instruction**

If you want to update the content of the application, please click **Offline Application** first and then update it. After updating, click **Publish Application** again.

{{</ alert >}}

## View Application

After the developer application is released, users can view the application by logging into [Access Side](https://home.quanxiang.dev).

![app_modeling10](/images/quick_start/app_modeling10.png)

## Offline Application

Developers click **Offline Application** to complete the application offline.

{{< alert tip >}}

**Instruction**

After going offline this application access side is not available, if you need to use again please publish the application!

{{</ alert >}}

![app_modeling11](/images/quick_start/app_modeling11.png)

