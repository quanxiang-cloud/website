---
title: "Create custom page"
description: "Create custom pages using the page engine in the QuanXiang Cloud low-code platform"
linkTitle: "Create custom page"
weight: 4262
---

This section describes how to create custom pages with the Page Engine.

## Operation steps

### 1 Select page engine

1. Log in to [QuanXiang Cloud Console](https://portal.quanxiang.dev/) and click **Application Management** > **My Applications** > **Specific Applications** > **Application Menu Page**.

   ![intro2](/images/manual/custom/intro2.png)

2. Use the page engine to build custom pages.

   ![intro1](/images/manual/custom/intro1.png)

### 2 Select component

Components are divided into layout components, and other components. The basic component and the form component need to be laid out using the layout component.

1. Click the container in the layout component, the container component appears in the page, and the page hierarchy is displayed as a container.

   ![new1](/images/manual/custom/page_design/new1.png)

2. Drag the text component to the just placed layout component, the page hierarchy is displayed as Container > Text.

   ![new2](/images/manual/custom/page_design/new2.png)

   {{< alert tip >}}

   **Instruction**

   Layout components facilitate page layout, and layout components support nesting.

   {{</ alert >}}

### 3 Configure component properties

Component properties include: properties, styles, events, and dynamic rendering. This article uses a text component as an example to describe how to configure component properties.

1. Configure Properties: Click Configure to support configuring variable parameters for text components.

   1. Click **Data Source** > **Variable Parameters** > **+** , add new parameters and assign values to the parameters.

      ![new3](/images/manual/custom/page_design/new3.png)

   2. Bind variable parameters.

      ![new4](/images/manual/custom/page_design/new4.png)

2. Configure style: Style settings support visual configuration, and also support editing by source code. Here select visual configuration. For details, see: [style description](. /style/).

   - Canvas: The canvas can be configured with text box size and text box position.
   - Display layout: component layout method, support configuration block level, in-line, in-line block, elasticity.
   - Positioning: Used to lock the position of the component in the canvas, supports configuring default, relative, absolute and fixed.
   - Fonts: support for configuration of font size, line height, font weight (bold and thin), alignment, color.
   - Backgrounds: support for no fill, color fill, picture fill.
   - Borders: support for borderless, solid and dashed lines.
   - Shadow: Support configuring shadow color and position.

   ![new5](/images/manual/custom/page_design/new5.png)

3. Configure events (optional)

4. Configure dynamic render (optional)

### 4 Preview

After the basic properties of the component are configured, the configuration effect can be viewed in real time in the canvas. The effect of variable parameter binding needs to be viewed in the preview environment.

Click the Preview button at the top to preview the configuration effect.

![new6](/images/manual/custom/page_design/new6.png)

