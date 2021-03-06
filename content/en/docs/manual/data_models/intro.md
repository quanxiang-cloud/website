---
title: "Overview"
description: "Introduction to the data model of QuanXiang Cloud Platform"
linkTitle: "Overview"
weight: 4310
---

The QuanXianf Cloud low-code platform provides an application internal data model management portal, through which you can manage the data model generated by the application form, the data model created by the user, and the data model composed of the parameters returned by Webhook.

## Data Model Classification

### Data model for form generation

The data model built by the form engine in QuanXiang Cloud Platform is automatically generated after the new form is created. You can view all the fields in the data model management module, which do not support modifying and deleting, but only viewing. If you need to modify the fields, please move to the form designer.

![intro1](/images/manual/data_models/intro1.png)

### Data models built by users

The data model created in the Data Model Management module can be customized with the required fields, defining attributes such as the field's code, name, format, whether it is allowed to be empty and whether it is used as a foreign key. After the data model is created, other parts of the application can be supplied for invocation. No new forms are added, only queries and references are provided.

![intro2](/images/manual/data_models/intro2.png)

## Usage Scenario

Data models are widely used in business data management scenarios. For example, users establish data models to manage the data of the stock system, get the corresponding data through API to generate data models, or create corresponding data models to be called when docking data.

