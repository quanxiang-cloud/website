---
title: "Basic operation guide"
description: "Component definition, form and field, field-component relationship"
linkTitle: "Basic operation guide"
weight: 4221
---

## Definition

The QuanXiang Cloud Platform packages fields with the same data characteristics into components, each with corresponding data format validation methods and attribute characteristics.

Currently provides 21 components such as basic fields, advanced fields, layout fields, etc. Developers can use these components to quickly build forms.

![basic_operation](/images/manual/form/basic_operation.png)

## Table and field, field and component relationships

**Tables and Fields**: Worksheets are used to store data sets of business objects. A data table will generate a record when it is completed and filled. Each object has many of the same attributes in the table that stores the data of these objects, and the attributes of the object are called fields. For example: [employee information table] contains: name, phone number, email, attribution department and other fields.

Translated with www.DeepL.com/Translator (free version)

{{<table >}}
| name | phone number | birth date   | ..   |
| ---- | -------- | ---------- | ---- |
| Jack | 18...    | 1990.01.01 | ..   |
| Jenny | 13...    | 1998.10.29 | ..   |
{{</table >}}


**Fields and Components**: For the specification and correct input of field data, the QuanXiang Cloud system has pre-set some formatted field types. For example: time and date component, radio box component, checkbox component, etc. When adding a field to a form, please select the appropriate component according to the data type of this field.

## Field Basic Operations

The field contains the following base settings:

- Add field
- Delete field
- Copy field
- Adapt position
- Property settings

### Add fields, property settings

Drag and drop the component to the form area to complete the field addition. After the field is added, configure the properties in the **Field Properties** column as needed.

![basic_operation1](/images/manual/form/basic_operation1.png)

{{< alert tip >}}

**Instruction**

Field properties settings include: title name, placeholder tips, description content, etc. Different field properties vary, for details of the base component properties see: [Base Component](../../component/basic_component/). For enhanced component properties, see: [Enhanced Components](../../../../manual/form/component/enhance/).

{{</ alert >}}

### Delete fields, copy fields, adapt position

- **Delete field**: click the Delete button to delete the field.
- **Copy field**: click the Copy button to copy the field.
- **Adapt Position**: Support for selected adapt field layout.

<img src="/images/manual/form/basic_operation2.png" alt="basic_operation2" style="zoom:67%;" />

{{< alert tip >}}

**Instruction**

Please be careful when delete a field, if the field has data, the data will be deleted with the field and cannot be recovered.

{{</ alert >}}

