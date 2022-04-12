---
title: "Introduction"
description: "Introduction of third-party API proxy function of QuanXiang Cloud Platform"
keywords: "API Proxy"
linkTitle: "Introduction"
weight: 7210
---

QuanXiang Cloud Platform API currently includes: Page Form API, Data Model API.

## Page Form API

After creating a form, the platform will automatically generate a page form API, which can be viewed by clicking **API Documentation** > **Page Form API**.

{{< alert tip >}}

**Instruction**

Only viewing API documentation is currently supported. Form API calls will be supported in the future.

{{</ alert >}}

### All Fields

Form API parameter descriptions are displayed in all fields, including: field name, field identifier, data format, whether null is allowed, and whether it is used as a foreign key.

![intro1](/images/api/platform/intro1.png)

### Call Example

The call examples include add, delete, update, query single item, and query multiple items. Take add as an example to demonstrate the form API call.

{{< alert tip >}}

**Instruction**

Currently supported languages include CURL, JavaScript, and Python.

{{</ alert >}}

#### Request Example

![intro2](/images/api/platform/intro2.png)

#### Return Example

![intro3](/images/api/platform/intro3.png)



## Data Model API

Once the data model is created, the platform will automatically generate the corresponding API, which can be viewed by clicking **API Documentation** > **Data Model API**.

{{< alert tip >}}

**Instruction**

For the data model creation process, see: [Create Data Model].(../../../manual/data_models/new/form/)。

{{</ alert >}}

### All Fields

Data model API parameter descriptions are presented in all fields, including: field name, field identifier, data format, whether null is allowed, and whether it is used as a foreign key.

![intro4](/images/api/platform/intro4.png)

### Call Example

The call examples include add, delete, update, query single item, and query multiple items. Take delete as an example to illustrate the data model API call method.

{{< alert tip >}}

**Instruction**

Currently supported languages include CURL, JavaScript, and Python.

{{</ alert >}}

#### Request Example

![intro5](/images/api/platform/intro5.png)

#### Return Example

![intro6](/images/api/platform/intro6.png)

