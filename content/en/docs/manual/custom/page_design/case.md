---
title: "Practice"
description: "Customized page examples"
linkTitle: "Practice"
weight: 4267
---

This section introduces specific examples of custom pages, so you can quickly get started with the page engine.

## Public Variable

Public variables can be defined in **Data Sources** > **Variable Parameters**. The following is an example of how to refer to parameter variables with a text component.

1. Define public variables.

   ![case10](/images/manual/custom/page_design/case10.png)

2. Bind the public variable to the text component, select text in the variable list, and enter state in the input box to call the data directly.

   - If the text variable is an array, fill in the input box with the elements within the called array. For example: state[0].
   - If the text variable is an object, fill in the input box with the path element within the called object. For example: state.xxx or state.xxx[0].xx.

   ![case11](/images/manual/custom/page_design/case11.png)

3. The preview is shown below.

   ![case12](/images/manual/custom/page_design/case12.png)

## Component fetch and assignment

The passing of component values in the current page engine is usually done using variables. Take the example of getting the value of an input box and assigning its value to another text box.

{{< alert tip >}}

**Instruction**

Only input boxes support ID naming. ID naming for other components will be added later.

{{</ alert >}}

1. First, drag out the three required components: text, input box, and button, and set a public variable to text with the value "initial data". The preview is as follows:

   ![case20](/images/manual/custom/page_design/case20.png)

2. Click the event tab of the button component, add an onclick event, click edit. The reference code is as follows:

   ```javascript
    const input_elem = document.getElementById('input')
    const input_val = input_elem.value//Set the variable to get the value of the input box, input is the ID of the input box
    this.states['text'] = input_val//Clicking the button will assign the value of the input box to the variable text
   ```

   ![case21](/images/manual/custom/page_design/case21.png)

3. Bind the action and click Save. The preview effect is as follows.

   ![case22](/images/manual/custom/page_design/case22.png)

   

Passing, fetching and assigning values between two components can be done through variables and data. Binding can also be done through other events such as onchange, and different events are supported for different components.









