---
title: "Create option sets"
description: "How to create option sets and usage scenarios"
linkTitle: "Create option sets"
weight: 4150
---

When designing a form, it is common to pre-set radio or multiple choice boxes to provide users with options. For highly reusable options, it is recommended to maintain them as option sets, which can reduce configuration operations and improve efficiency.

The QuanXiang Cloud low-code platform supports the creation of single-tier and multi-tier option sets:

- **Single-level option set**: When designing a form, such option sets can be called in fields such as [radio box], [check box], [drop-down radio box], [drop-down check box], etc.
- **Multi-level option set**: When designing a form, such option sets can be used in the [Cascade Selection] field.

## Create Portal

Log in to [QuanXiang Cloud Console](https://portal.quanxiang.dev) and click **Application Management** > **Option Sets**.

![option_set1](/images/manual/option_set1.png)

## Add single-level option set

1. Click **Single Level** > **Add Option Set** and fill in the option set information in the pop-up box.

   ![option_set2](/images/manual/option_set2.png)

2. After clicking OK, jump to the option set detail page and add option data as needed.

   ![option_set3](/images/manual/option_set3.png)

   {{< alert tip >}}

   **Instruction**

   Option data names must not be repeated, and each option name is recommended to be no more than 20 characters.

   {{</ alert >}}

### Calling option sets

When designing a form, option sets can be called in fields such as [radio box], [check box], [drop-down radio box], [drop-down checkbox], etc.

![option_set4](/images/manual/option_set4.png)

## Add multi-level option set

1. Click **Multilevel** > **Add option set** and fill in the option set information in the pop-up box.

   ![option_set2](/images/manual/option_set2.png)

2. After clicking OK, jump to the option set detail page and add option data as needed. The lower level options need to be filled in after checking the upper level options.

   ![option_set5](/images/manual/option_set5.png)

   {{< alert tip >}}

   **Instruction**

   Option data names must not be repeated, and each option name is recommended to be no more than 20 characters.

   {{</ alert >}}

### Calling option sets

Such option sets can be used in the [Cascade Selection] field when designing forms.

![option_set6](/images/manual/option_set6.png)

## Single-level option set extended to multi-level option set

Single-level option sets are supported to be extended to multi-level option sets. Simply right-click and copy to complete the extension.

1. Select the single-level option set that needs to be expanded and click **Copy** to bring up the expansion popup.

   ![option_set7](/images/manual/option_set7.png)

2. Select Expand to multi-layer option set and click **OK**.

   ![option_set8](/images/manual/option_set8.png)

3. A successful copy will jump to the multi-level option set.

   ![option_set9](/images/manual/option_set9.png)

