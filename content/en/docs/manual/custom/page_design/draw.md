---
title: "Dynamic Render"
description: "Create custom pages using the page engine in the QuanXiang Cloud low-code platform"
linkTitle: "Dynamic Render"
weight: 4266
---

This section describes how to configure dynamic render.

## Overview

The QuanXiang Cloud low-code platform supports dynamic looping. With dynamic rendering, you can loop to render multiple pieces of data, such as setting a text variable to an array.

["Hello","Thank you","Good morning","How are you?","Nice to meet you","You are welcome","Good bye","Good night"]

![draw1](/images/manual/custom/page_design/draw1.png)

## Operation steps

This article describes the dynamic loop configuration steps using the text variable as an example.

1. Drag a text component, set its dynamic rendering parameters, select the Text function you just defined, enter return {content: state} in the input box at the bottom right of the dynamic rendering, and click Preview to cycle through the rendering successfully.

   ![draw2](/images/manual/custom/page_design/draw2.png)

2. The rendering is as follows:

   ![draw3](/images/manual/custom/page_design/draw3.png)

