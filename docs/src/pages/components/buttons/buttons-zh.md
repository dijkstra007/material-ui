---
title: React Button 按钮组件
components: Button, IconButton, ButtonBase
---

# Button 按钮

<p class="description">只需通过轻按一下按钮，用户即可采取行动并做出选择。</p>

[按钮](https://material.io/design/components/buttons.html) 传达了一系列用户可以执行的操作命令。 他们通常直接放置在您的用户界面中，例如：

- Dialogs 对话框
- Modal windows 模态窗口
- Forms 表单
- Cards 卡片
- Toolbars 工具栏

## Contained Buttons 实心按钮

[实心按钮](https://material.io/design/components/buttons.html#contained-button)表示高度的强调，你根据它们的立体效果和填充颜色来区分彼此。 它们用于触发应用程序所具有的主要功能。

{{"demo": "pages/components/buttons/ContainedButtons.js"}}

你也可以使用属性 `disableElevation` 属性来消除实心按钮的立体效果。

{{"demo": "pages/components/buttons/DisableElevation.js"}}

## Text Buttons 文本按钮

[文本按钮](https://material.io/design/components/buttons.html#text-button)通常用于不太明显的操作，包括那些存在于：

- 在 dialogs 对话框中的
- 在 cards 卡片中的

在卡片中，文本按钮有助于强调卡片的内容。

{{"demo": "pages/components/buttons/TextButtons.js"}}

## Outlined Buttons 描边按钮

[描边按钮](https://material.io/design/components/buttons.html#outlined-button)表示中等的强调。 它们包含了一些重要的操作，但不是一个 app 中的主要操作。

你也可以将描边按钮作为比实心按钮次要一点的替代方案，或者用来作为比文本按钮重要一点的展示。

{{"demo": "pages/components/buttons/OutlinedButtons.js"}}

## 一个上传按钮

{{"demo": "pages/components/buttons/UploadButtons.js"}}

## 尺寸

您想要一个大一点或者小一点的按钮吗？ 我们提供了 `size` 这个属性供您调整。

{{"demo": "pages/components/buttons/ButtonSizes.js"}}

## 带有 icons 图标和 label 标签的按钮

有时您可能想在特定一个按钮上添加图标以增强应用程序的用户体验，因为大多数情况下我们觉得图标比纯文本更有辨识度。 例如，如果您有删除按钮，则可以使用垃圾箱图标对其进行标记。

{{"demo": "pages/components/buttons/IconLabelButtons.js"}}

## Icon Buttons 图标按钮

图标按钮通常运用于应用栏和工具栏。

图标也适用于实现单个选项的选择和或取消选择的切换按钮，例如向一个元素添加或删除星标。

{{"demo": "pages/components/buttons/IconButtons.js"}}

## 自定义按钮

以下是自定义组件的一些例子。 您可以在[重写文档页](/customization/components/)中了解有关此内容的更多信息。

{{"demo": "pages/components/buttons/CustomizedButtons.js", "defaultCodeOpen": false}}

👑如果您还在寻找灵感，您可以查看一下 [MUI Treasury 自定义的例子](https://mui-treasury.com/components/button)。

## Complex Buttons 复杂按钮

文本按钮，包含按钮，浮动操作按钮和图标按钮都基于同一个组件：`ButtonBase`。 利用此较底层的组件，您可以创建一些自定义的交互操作。

{{"demo": "pages/components/buttons/ButtonBase.js"}}

## Third-party routing library 第三方路由库

我们发现的一个常用案例，是用按钮来导航用户到新的页面。 你可以用 `ButtonBase` 的 `component` 属性来处理这样的事件。 然而，一些针对 `ButtonBase` 的特定 polyfills 补丁则要求该组件的 DOM 节点。 您可以尝试在组件上附加一个 ref，并且预期此组件能够将这个 ref 传递到下层 DOM 节点，通过这样的方法可以实现。 鉴于许多我们的交互式组件都基于 `ButtonBase`，您可以在很多情况下受益。

这就有一个[与 react-router 交互的例子](/guides/composition/#button)。

## 局限性

### Cursor 鼠标悬浮的禁用

在 disabled 不可用的按钮上，ButtonBase 组件会有这个设置：`pointer-events: none;` ，这样一来不可用样式的鼠标悬浮就不会出现。

若您希望使用 `not-allowed`， 您有以下两种选择：

1. **CSS only**。 您可以移除作用在 `<button>` 元素上的指针事件的样式：

  ```css
  .MuiButtonBase-root:disabled {
    cursor: not-allowed;
    pointer-events: auto;
  }
  ```

然而：

- 若您仍旧需要在[禁用的元素上展示提示工具](/components/tooltips/#disabled-elements)，您需要恢复 `pointer-events: none;`。
- 若您加载除了一个 button 元素之外的元素， 例如，一个链接 `<a>` 元素，指针是不会改变的。

2. **改变 DOM**。 您可以这样封装按钮：

  ```jsx
  <span style={{ cursor: 'not-allowed' }}>
    <Button component={Link} disabled>
      disabled
    </Button>
  </span>
  ```

这样一来就可以支持任何元素，例如，一个 `<a>` 元素。