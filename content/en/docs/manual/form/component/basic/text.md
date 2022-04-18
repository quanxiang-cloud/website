---
title: "Single-line text"
description: "Single line text component definition and field properties"
linkTitle: "Single-line text"
weight: 42211
---

## Component definition

Single line text is the most basic and common component that can be used to collect text, numbers and other information. It is commonly used to enter basic user information, such as name, cell phone number, email address, etc.

## Field Property

![单行文本_属性](/images/manual/component/单行文本_属性.png)

Please configure the following properties of the field according to your actual needs:

- Title name: field name, required.
- Placeholder tips: please fill in if required.
- Description of content: Please fill in if required.
- Format: a variety of data formats are supported, see Format below for details.
- Field property: support setting to normal, read-only, hidden, default is normal.
- List sorting: support for list sorting, no sorting by default.
- Required or not: you can choose whether the field is required or not, the default is non-required.
- Data sources: support for customization, association of the existing data.
- Default value: Enter if necessary.

#### Format

In the single line text component, it supports preset data formatting and plays the role of field validation. Currently, only China-wide data validation is supported.

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

