---
title: 'Tailwind CSS 入门和实践'
tag: 'Tailwind CSS, 前端技术, 低代码'
keywords: 'Tailwind CSS, Tailwind, UI, HTML, 前端技术, 低代码, low-code'
description: 'Tailwind 是一个基于 Atomic/Utility-First 规范 CSS 框架，提供了基础的工具类 utility classes（如：内边距 padding、字体 text 和 font、动画 transition 等预设类），能直接在脚本标记语言中组合起来，构建出您想要的设计。'
createTime: '2021-11-05'
author: '康曾璐'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/cover.png'
---

# 背景

 [Tailwind](https://tailwindcss.com/) 是一个基于 Atomic/Utility-First 规范 CSS 框架，提供了基础的工具类 utility classes（如：内边距 padding、字体 text 和 font、动画 transition 等预设类），能直接在脚本标记语言中组合起来，构建出您想要的设计。

目前主流的 UI 框架，如 Ant-design，则采用直接提供现成组件（如：按钮 buttin、表单 form 等组件）的方式。开发者可以使用框架提供的组件快速进行页面构建，但由于组件的样式一般是提前预设并且封装好的，若要定制样式，需要大量覆盖组件的内置样式。

Tailwind 没有提供现成的组件，而是提供各种通用的样式类。开发者可以直接在 HTML 的 Tag 添加各种基础的 class 为元素设置相应的 UI 样式，通过各种基础的 class 的「叠加组合」构建出所需的外观，高效地进行定制化的网站开发。换言之，在 TailwindCSS 中，有许多小类代表 CSS 声明。当创建组件时，只需要引用其中的一些小类就可以创建您需要的组件。



# 1 Semantic CSS | Atomic/Utility-First CSS

## 1.1 Semantic CSS

要制作一个 button 按钮的样式，我们一般会在 html 或者 jsx 结构中添加富有语义化的 class 类名，随后在 css 样式中写入对应类的样式。例如：制作一个 danger 样式的 Button 按钮。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/danger-button.png" width = 30%/>
</div>

```html
  <div class="box">
    <button class="danger-button">Button</button>
  </div>

.danger-button {
  height: 32px;
  padding: 4px 15px;
  font-size: 14px;
  border-radius: 2px;
  color: #fff;
  border-color: #ff4d4f;
  background: #ff4d4f;
  text-shadow: 0 -1px 0 rgb(0 0 0 / 12%);
  box-shadow: 0 2px #0000000b;
}
```

以上是最常见、最常规的写法，被称作 `Semantic CSS`（语义化 CSS）规范。在这种规范下，追求关注点分离，让结构与样式各司其职，使结构更具语义化。但这样一来，也面临着许多问题：

* 给标签添加一个样式需要绞尽脑汁想类名，既要语义化，又要符合代码规范，还要和它作用相符合；
* 每个类中往往会有很多个样式规则，只有结构的语义、样式完全相同时才能做到真正的复用，若存在差异，就难以实现样式复用；
* 如果将 html 或 jsx 结构做迁移，我们同时还要将相应的 css 迁移，迁移后的样式也可能随上下文环境变得错乱。
* ......

## 1.2 Atomic/Utility-First CSS

Atomic/Utility-First CSS 与 Semantic CSS 相对，Utility-First CSS（功能类优先 css）不像 Semantic CSS 那样将组件样式放在一个类中，而是为我们提供一个由不同功能类组成的工具箱，我们可以将它们混合在一起应用在 html 元素上。在物理世界中， 原子是构成一般物质的最小单位，而在 css 世界中，遵循一个类中只有唯一的 css 规则。

`Tailwind CSS` ，用法与 Bootstrap 类似，都是通过类名来引用样式。最大的区别，也是 Tailwind CSS 的核心，即它是一套以 Atomic/Utility-First CSS 为基础 CSS 框架。

#  2.Tailwind CSS 优点

- 可定制化程度极高：

  Tailwind 带有一个默认配置，你可以使用项目中的 “tailwind.config.js” 来覆盖默认配置。从颜色、间距大小到字体的所有内容都可以使用配置文件轻松定制。且配置文件的每个部分都是可选的，您只需指定要更改的内容，缺失的部分将使用 Tailwind 的默认配置。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/config.png" width = 60%/>
</div>

- 减少为 class 取名字的苦恼。

- 无需切换上下文：Tailwind 提供了几乎所有需要的开箱即用，开发者不再需要数百次从 HTML 切换到 CSS 。

- 响应式设计

  - Tailwind CSS 遵循移动优先的设计模式，断点系统很灵活。比如实现一个媒体查询，要求根据不同的屏幕宽度实现不同的图片宽度。传统写法如下：

```css
@media only screen and (max-width:1280px) {
    .content {
     	width:196px;
    }
}
@media only screen and (max-width: 760px) {
    .content {
    	width:128px;
    }
}
```

在 Tailwind CSS 中表述如下：

```js
<div class="w-16 md:w-32 lg:w-48" src="...">
```



# 3.使用技巧

## 3.1 选择数字标签而不是语义标签

`TailwindCss` 具有较好的语义化，但使用默认的命名方案，会大大增加开发者的记忆成本，例如：字体粗细值从 `thin`（100） 定义到了 `black`（900）。
使用数字标签的方式可以减少 UI 工具的值转换为 `TailwindCss` 类的成本。例如：`font-weight: 600` 不清楚对应 `font-bold` 还是 `font-semibold`，但 `font-600`就很明确。

语义标签总是不好的，但数字标签也不能覆盖所有场景，需要确定哪种方式让我们使用起来更加受益。

```
fontWeight: {
    thin: '100',
    extralight: '200',
    light: '300',
    normal: '400',
    medium: '500',
    semibold: '600',
    bold: '700',
    extrabold: '800',
    black: '900',
}

fontWeight: {
    100: '100', 
    200: '200',
    300: '300',
    400: '400',
    500: '500',
    600: '600',
    700: '700',
    800: '800',
    900: '900',
}
```

## 3.2 不建议使用 @apply

### 提取组件

Tailwind 是实用程序优先的框架，因此创建的组件将包含实用工具类的集合。这意味创建相同的组件时，将编写相同的实用工具类集。即当您想为该组件更改一个实用工具类时，就需要更改所有具有相同“意图”的组件。

**为了克服这个问题，Tailwind 提供了一种解决方案，即“提取组件”**。 Tailwind 提供了伪指令**@apply**，**它允许一次组合多个实用工具类**。例如，您有一个按钮组件，其结构如下：

```
<button class="button">   
    Button
</button>
<style> 
.button { 
  @apply bg-blue-600 text-white px-4 py-2 rounded; 
} 
</style>
```

从功能上来说，使用 @apply 生成新的功能类，会产生多余的 css，我们应尽量不使用它，这与 `TailwindCss` 设计背道而驰。

# 4. 使用 Tailwind

## 4.1 制作一个基础按钮

```jsx
<button type="button" class="py-2 px-4 bg-red-500 text-white font-semibold rounded-lg shadow-md">
  button
</button>
```

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/button.png" width = 30%/>
</div>


## 4.2 响应式布局

Tailwind 中的每个实用程序类都可以在不同的断点处有条件地应用，这使得在不离开 HTML 的情况下构建复杂的响应式界面变得简单。

受常见设备分辨率的启发，Tailwind 提供 5 个断点：

- **sm** 适用于最小宽度为 640px 的设备；
- **md** 适用于最小宽度为 768px 的设备；
- **lg** 适用于最小宽度为 1024px 的设备；
- **xl** 适用于最小宽度为 1280px 的设备；
- **2xl **适用于最小宽度为 1536px 的设备。

以下是一个营销页面组件的简单示例，它在小屏幕上使用堆叠布局，在大屏幕上使用并排布局*（调整浏览器大小以查看其实际效果）*：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/layout.png" width = 60%/>
</div>


```jsx
<div class="max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl">
  <div class="md:flex">
    <div class="md:flex-shrink-0">
     <img class="h-48 w-full object-cover md:h-full md:w-48" src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic.5tu.cn%2Fuploads%2Fallimg%2F1706%2Fpic_5tu_big_201705201558243571.jpg&refer=http%3A%2F%2Fpic.5tu.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1637733958&t=28299dabd6e0330e876dcf7195742f1f" alt="Man looking at item at a store">
    </div>
    <div class="p-8">
      <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">Case study</div>
      <a href="#" class="block mt-1 text-lg leading-tight font-medium text-black hover:underline">
        Finding customers for your new business
      </a>
      <p class="mt-2 text-gray-500">Getting a new business off the ground is a lot of hard work. Here are five ideas you can use to find your first customers.
      </p>
    </div>
  </div>
</div>
```

## 4.3 添加按钮状态

类似于 Tailwind 处理响应式设计的方式，悬停、焦点等的样式元素可以通过在实用程序前面加上适当的状态变量来实现。例如：添加悬浮状态`hover:bg-red-700`。

```jsx
<button class="... hover:bg-red-700">
    Button
</button>
```

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/blogs/Tailwind%20CSS%20Introduction%20and%20Practice/hover-button.png" width = 30%/>
</div>

# 总结
以上就是本期 Tailwind CSS 入门和实践分享。后期文章，我们将继续探讨如何使用全象云低代码平台搭建一个固资管理系统。敬请期待。






