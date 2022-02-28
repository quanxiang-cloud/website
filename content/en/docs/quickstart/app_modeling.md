---
title: "Getting Started"
description: "Help you build your application quickly with detailed illustrations."
# linkTitle: "Getting Started"
weight: 2100
---

Before using QuanXiang Cloud Platform, you need to prepare the account password of QuanXiang Cloud Platform, please refer to [Account Registration] for details.(..//registration/)。The platform supports **account secret login** or **login with verification code**. If the account fails to log in 5 times, it will be locked, you can contact the administrator to reset the password.

The quick build application steps are as follows:

<img src="/images/quick_start/quick_start1.png" alt="quick_start1" style="zoom:50%;" />

## Create Application

1. User account login [QuanXiang Cloud Platform](https://portal.quanxiang.dev)，click **Application Management** > **My Applications** > **New Application** to build the application.

2. According to the page prompts and application building requirements to complete the basic application configuration, click **OK** to finish the application creation.

   <img src="/images/quick_start/app_modeling1.png" alt="app_modeling1" style="zoom:50%;" />

## Create Menu

Usually an application consists of different menu pages, each of which can perform different functions. After the application is created, the navigation section creates the example page by default.

1. Click **View Management** > **New Menu**, the New Page pop-up window appears, fill in the page information.

   ![app_modeling2](/images/quick_start/app_modeling2.png)

2. The application page supports New Form, New Custom Page, and Upload Static Page, please choose according to your needs, see below for detailed steps.

   ![app_modeling3](/images/quick_start/app_modeling3.png)

{{< alert tip >}}

**Instruction**

The menu pages support grouping management for page classification, making it easy for developers to establish application hierarchies and for users to quickly locate the features they want to use.

![app_modeling4](/images/quick_start/app_modeling4.png)

{{</ alert >}}

### Create Form

After the application page is created, click **New Form** to create the form required for your business, and click **Save** when the design is finished. For form preview, please click **Preview Form** on the top right corner of the page. Developers can optimize the designed form in this page several times until the preview meets the business requirements. For detailed steps, please refer to [Form Design](../../manual/form/).

![newform](/images/quick_start/newform.gif)

{{< alert tip >}}

**Instruction**

The form preview page supports form simulation submission, and the submission results will be displayed on this page.

{{</ alert >}}

### Create Custom Page

To develop front-end pages for complex scenarios, you can click **Create Custom Page** to create them. The platform supports building custom pages through Schema editor or page engine. For detailed steps, refer to: [Create Custom Page](../../manual/custom/page_design/new/).

![app_modeling5](/images/quick_start/app_modeling5.png)

### Upload Static Page

After the application page is created, click **Upload Static Page** to upload it. Support uploading static page code, including html, javascript, css, images, etc. Custom pages can be generated after the zip archive is uploaded successfully, and preview or modification is supported. More instructions see: [Upload Static Page](../../manual/custom_page/).

![app_modeling6](/images/quick_start/app_modeling6.png)

{{< alert tip >}}

**Instruction**

Static page generation takes time, please be patient.

{{</ alert >}}

## Create Workflow (Optional)

A workflow is composed of a trigger and a sequence of action nodes. The workflow triggering method currently only supports worksheet triggering. In the action node, you can realize data query, update and other operations; you can also execute manual control processes such as approval and filling.

#### Create Portal

- Click [Admin side application management](https://portal.quanxiang.dev/apps) > **Specific Applications** > **Workflow**, jump to the workflow management page.

- Click **Form Page** > **Associated Workflow**, jump to the workflow management page.

![app_modeling7](/images/quick_start/app_modeling7.png)

#### Creation Steps

The workflow configuration mainly includes the selection of trigger method and the design of workflow function nodes. For detailed steps refer to: [Workflow Management](../../manual/workflow/).



## Application Rights Management

Enterprise applications often require multi-role user collaboration, and different permissions need to be assigned to different role users when performing data collection or analysis in order to secure enterprise data.

QuanXiang Cloud Platform currently supports configuring permissions by subdividing down through the application dimensions to achieve fine-grained management of permissions. Permission management dimensions include: **Application** > **Worksheet** > **Operation Permission**, **Field Permission**, **Data Permission**.

#### Configuration Portal

- [Console Application Management](https://portal.quanxiang.dev/apps) > **Application Specific** > **Access Control**, jump to the application permission management page.

- Click **Form Page/Custom Page** > **Authorized Roles**, jump to the application permission management page.

![app_modeling8](/images/quick_start/app_modeling8.png)

#### Configuration steps

Application rights management is divided into access-side rights and management-side rights, for more detailed configuration steps see: [Access Control](../../manual/permission/).



## Publish Application

After the application form is configured, the developer can click **Publish Application** in the upper right corner of the application. After the application is successfully published, you can click **Access Application Side** to view the published application. At this time, users with access rights can also access this application.

![app_modeling9](/images/quick_start/app_modeling9.png)

{{< alert tip >}}

**Instruction**

If you want to update the content of the application, please click **Offline Application** first and then update it, then click **Publish Application** again after the update is finished.

{{</ alert >}}

## View Application

After the application is released, users can visit [QuanXiang Cloud Platform Access Side](https://home.quanxiang.dev) to view the application.

![app_modeling10](/images/quick_start/app_modeling10.png)

## Offline Application

If the app needs to be taken offline, the developer can click **Offline App**.

{{< alert tip >}}

**Instruction**

After offline access side of this application is not available, if you want to use again please publish the application!

{{</ alert >}}

![app_modeling11](/images/quick_start/app_modeling11.png)

