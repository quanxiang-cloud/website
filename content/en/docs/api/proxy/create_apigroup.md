---
title: "Creating API Groups"
description: "Introduction to the API group creation process"
keywords: "API Groups"
linkTitle: "Creating API Groups"
weight: 7315
---

A group is a management unit of an API, and the API provider manages all APIs within the API group as a unit.

Before you create the API, you need to create the API group.

## Create group

Create the API groups by following the steps below.

1. User account login to [QuanXiang Cloud Platform](https://portal.quanxiang.dev/).

2. In the console navigation bar, select **Application Management** > **My Applications**, select the application that needs to set up a third-party API proxy, and enter the application details page.

3. Click **Data Management** > **Third Party API Proxy** > **New Group** and the Create API Group pop-up window appears.

   ![create_apigroup1](/images/api/proxy/create_apigroup1.png)

4. Fill in the API grouping base information: group name, group identification, and description.

   {{< alert tip >}}

   **Instruction**

   The group identifier needs to be in English, as a unique identifier for the group, which cannot be repeated.

   {{</ alert >}}

## Configure groups

### Relationship between domain, grouping and API

- Users need to bind the domain they own to the API group to establish the mapping between the domain and the group.
- When the API receives an HTTP request from a client, it locates the API group to which the request belongs based on the domain in the HTTP request, and then determines the unique API by HTTPMethod and PATH.



### Operation steps

After the group information is filled in, enter the group configuration page.

1. Select the request protocol, configure the host address (domain) and port number.

   - The request protocol supports HTTP, HTTPS.
   - The host address and port number is the access address of the third-party API.

2. Configure the authentication method.

   - The authentication method supports no configuration, or configuration of signature. Configuration method see: [authentication method](../../authentication/).

   {{< alert tip >}}

   **Instruction**

   After configuring the authentication method, you need to configure [API key](/api/proxy/secretkey/). If no key is configured, the system will prompt to upload the key when calling.

   {{</ alert >}}

![create_apigroup2](/images/api/proxy/create_apigroup2.png)

## API List

### New API

Click **API List** > **New API** to enter the New API page, fill in the correct API information according to the page guidelines to create an API under this group. For detailed steps, please refer to [Create API](../create_api/create/).

![create_apigroup7](/images/api/proxy/create_apigroup7.png)

### View API List

All API information can be viewed in the API list.The API list will show: **API Name**, **Request Method**, **URL**, **Proxy Path** and its **Status**.

![create_apigroup3](/images/api/proxy/create_apigroup3.png)



## Manage groups

### Create subgroup

Click the Group Details button and click **New Subgroup**. The subgroup creation process is the same as the group.

![create_apigroup4](/images/api/proxy/create_apigroup4.png)

### Modify group information

Click the Group Details button > **Modify Group Information**, and the Modify Group Information pop-up window appears. Only the group name and description are supported to be modified.

![create_apigroup5](/images/api/proxy/create_apigroup5.png)





## 删除分组

如需删除分组，点击分组详情按钮 > **删除**，出现提示弹窗，请确认后删除分组。

![create_apigroup6](/images/api/proxy/create_apigroup6.png)
