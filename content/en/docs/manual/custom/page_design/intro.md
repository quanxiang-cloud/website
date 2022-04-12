---
title: "What is Page Engine"
description: "Introduction of QuanXiang Cloud Low-Code Platform Page Engine"
linkTitle: "What is Page Engine"
weight: 4261
---

QuanXiang Cloud low-code platform page engine provides common components, the components contain pre-set styles and encapsulate the basic event code, realizing out-of-the-box, avoiding users to write repeated styles and event code, and being able to focus on business scenario development.

## Page engine style

The structure of the platform page engine is similar to the layout of the design software, divided into three columns on the left, middle and right + top column layout.

- The left toolbar contains component libraries, page hierarchies, and data sources.
- The middle part is the canvas.
- On the right side is the properties configuration panel.
- On top is the Basic Operations section.

![intro1](/images/manual/custom/page_design/intro1.png)

## Top operation bar

QuanXiang Cloud low-code platform provides: Remove, Forward, ?  , Preview, Save, Save Exit and other shortcut buttons to provide convenience for page development.

![intro2](/images/manual/custom/page_design/intro2.png)

## Left tool bar

### Component Library

Components in the component library can be dragged and dropped directly to the canvas, and support operations such as adjusting the order and copying. QuanXiang Cloud currently supports the following components.

![intro3](/images/manual/custom/page_design/intro3.png)

### Page Level

The page level is used to view the page layout, and the page level supports viewing the outline view and the source view.

- Click on a component in the outline view to locate the corresponding component in the canvas.

  ![intro4](/images/manual/custom/page_design/intro4.png)

- The source view makes it easy to view detailed data on the page.

  ![intro5](/images/manual/custom/page_design/intro5.png)

### Data Sources

Data sources can declare variables and APIs for presenting dynamic data. Data binding to variable parameters can be performed on the control's property configuration.

![intro6](/images/manual/custom/page_design/intro6.png)

## Middle Canvas

The canvas is used to layout and configure the components to complete the page construction. Components can be dragged and dropped, copied and deleted in the canvas.

![intro7](/images/manual/custom/page_design/intro7.png)

## Right configuration bar

### Property

The property settings are used to configure the basic properties of the component, and the configuration effect can be viewed in real time in the canvas after the configuration is completed.

{{< alert tip >}}

**Instruction**

The effect of variable parameter binding needs to be viewed in the preview environment.

{{</ alert >}}

![intro8](/images/manual/custom/page_design/intro8.png)

### Style

Style settings support visual configuration, while supporting editing via source code.

![intro9](/images/manual/custom/page_design/intro9.png)

### Event

The event panel is used to bind the action initiation API. Each component supports didMount(load complete), willUnmount(unload) events, while other actions are exposed by the component itself. For example, the button component supports exposing onClick events.

![intro10](/images/manual/custom/page_design/intro10.png)

![intro11](/images/manual/custom/page_design/intro11.jpeg)

### Dynamic render

Dynamic rendering is used to show cyclic rendering of scenes.

![intro12](/images/manual/custom/page_design/intro12.png)
