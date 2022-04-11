---
title: "Style Description"
description: "Create custom pages using the page engine in the QuanXiang Cloud low-code platform"
linkTitle: "Style Description"
weight: 4264
---

This section introduces how to configure the component style and the detailed description of the parameters in the style.

## Overview

Style settings support visual configuration and source code editing.

![intro9](/images/manual/custom/page_design/intro9.png)

## Detail

### Source Code Editor

When some of the CSS styles cannot be configured in the setter, you can write custom CSS style code through the source code editor.

The source code editor and the setter are fully synchronized with the changes, the editing takes effect instantly, and the left canvas can preview the style in real time.

![style1](/images/manual/custom/page_design/style1.png)

### Canvas

The canvas can be configured with text box size and text box position. The canvas style is shown below.

![style2](/images/manual/custom/page_design/style2.png)

- padding: Inner Margins, used to set all inner margin attributes of an element in a single declaration. The setter can be filled directly with the top, bottom, left and right margins, or the design can be edited by the source code. As shown below, for more instructions see.[CSS padding property](https://www.w3school.com.cn/cssref/pr_padding.asp).

  ```css
  padding:10px 5px 15px 20px;
  ```

  - The top inner margin is 10px:
  - The right inner margin is 5px:
  - The bottom inner margin is 15px:
  - The left inner margin is 20px:

- margin: Outer Margins, used to set all outer margin properties of an element in a single declaration. The setter can be filled directly with the top, bottom, left and right margins, or the design can be edited by the source code. As shown below, for more instructions see.[CSS margin property](https://www.w3school.com.cn/cssref/pr_margin.asp).

  ```css
  margin:10px 5px 15px 20px;
  ```

  - The top inner margin is 10px:
  - The right inner margin is 5px:
  - The bottom inner margin is 15px:
  - The left inner margin is 20px:

### Display Layout

The fill types are divided into: block-level, in-line, in-line block, and flexible layout.

#### Block-level

Block-level elements, which always occupy a separate line, are shown as starting on a separate line, and subsequent elements must also be shown on a separate line.

#### In-line

An in-line element that is on the same line as an adjacent in-line element.

#### In-line block

An in-line block element, on the same line as an adjacent in-line element, behaves as a peer display.

#### Flexible layout

Flexible layout allows for easy, complete and responsive implementation of various page layouts.

![style3](/images/manual/custom/page_design/style3.png)

### Position

Positioning is used to lock the position of the component in the canvas and supports configuration of default, relative, absolute, and fixed.

### Font

The platform supports configuration of font size, height, weight (bold and thin), alignment, and color.

- Size: font size.
- Height: the line height of the text.
- Weight: the thickness of the text.
- Alignment: text alignment, support left alignment, centering, right alignment, and both ends alignment.
- Color: the color of the text.

![style4](/images/manual/custom/page_design/style4.png)

### Background

The background supports no fill, color fill, and image fill.

![style5](/images/manual/custom/page_design/style5.png)

### Border

Support borderless, solid line and dashed line. The solid line and dashed line support setting the width and the number of edge angle.

![style6](/images/manual/custom/page_design/style6.png)

### Shadow

Support configuring shadow color and position.

- X-axis: the shadow is shifted horizontally.
- Y-axis: the shadow is shifted in the vertical direction.
- Blur: shadow blurring distance. The larger the value the more blurred the edges of the shadows will be.
- Expand: the radius of the shadow expansion. If the value is positive, the shadows are expanded, and if the value is negative, the shadows are reduced.
- Color: The color of the shade.

![style7](/images/manual/custom/page_design/style7.png)

