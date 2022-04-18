---
title: "Multi-line text"
description: "Single line text component definition and field properties"
linkTitle: "Multi-line text"
weight: 42212
---

## Component definition

Multi-line text is often used to enter long content information, such as: order details, notes, meeting notes, feedback, etc. It does not support interconversion with rich text components at the moment.

## Field Property

![多行文本_属性](/images/manual/component/多行文本_属性.png)

Please configure the following properties of the field according to your actual needs:

- Title name: field name, required.
- Placeholder tips: please fill in if required.
- Description of content: Please fill in if required.
- Format: a variety of data formats are supported, see Format below for details.
- Field property: support setting to normal, read-only, hidden, default is normal.
- Required or not: you can choose whether the field is required or not, the default is non-required.
- Data sources: support for customization, association of existing data.
- Default value: Enter if necessary.

### Format

In the multi-line text component, it supports preset data formatting, which plays the role of field validation. Currently, only China-wide data validation is supported:

- **None**: Chinese characters or numbers.
- **Telephone**: area code starting with 0 - landline number - extension number. Where the area code and extension number are optional.
- **Postal code**: 6 digits.
- **Mobile phone**: 11 digits starting with 1.
- **ID card**: verification using regular expressions.
  - The length of the ID card is 18 digits, with the first 17 digits necessarily being numeric.
  - The first two province figures are in the range of 11 to 82.
  - A six-digit birthday code starting from the seventh digit that matches the date check.
  - The last digit may be a number or a capital X.
- **Email**: xxx@xxx.xxx.

