---
title: 自适应表单组件的内联样式
description: 您可以在自适应表单中应用自定义样式，也可以在自适应表单的各个组件中应用内联CSS属性。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: c074afbb-33d1-4424-bbd2-2acdeeebe9d0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 13%

---

# 自适应表单组件的内联样式 {#inline-styling-of-adaptive-form-components}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

可以使用[主题编辑器](../../forms/using/themes.md)指定样式来定义自适应表单的整体外观和样式。 此外，您还可以将内联CSS样式应用于各个自适应表单组件并即时预览更改。 内联样式会覆盖主题中提供的样式。

## 应用内联CSS属性 {#apply-inline-css-properties}

要将内联样式添加到组件，请执行以下操作：

1. 在表单编辑器中打开表单，并将模式更改为样式模式。 要将模式更改为样式模式，请在页面工具栏中选择![画布下拉列表](assets/canvas-drop-down.png) > **样式**。
1. 在页面中选择组件，然后选择编辑按钮![edit-button](assets/edit-button.png)。 样式属性在侧栏中打开。

   您还可以从侧栏中的表单层次结构树中选择组件。 表单层次结构树在侧栏中可用作表单对象。

   您还可以从侧栏中选择组件。 在“样式”模式下，您可以看到列在“表单对象”下的组件。 但是，侧边栏中的表单对象列表列出了字段和面板等组件。 字段和面板是可以包含文本框和单选按钮等组件的常规组件。

   从侧栏中选择组件时，您将看到列出的所有子组件以及所选组件的属性。 您可以选择特定的子组件并设置其样式。

1. 单击侧边栏中的选项卡以指定CSS属性。 您可以指定属性，例如：

   * 尺寸和位置（显示设置、填充、高度、宽度、边距、位置、z索引、浮动、清除、溢出）
   * 文本（字体系列、粗细、颜色、大小、行高和对齐）
   * 背景（图像和渐变、背景颜色）
   * 边框（宽度、样式、颜色、半径）
   * 效果（阴影、不透明度）
   * 高级（允许您为组件编写自定义CSS）

1. 同样，可以为组件的其他部分（如小组件、标题和帮助）应用样式。
1. 选择&#x200B;**完成**&#x200B;以确认更改，或选择&#x200B;**取消**&#x200B;以放弃更改。

## 示例：字段组件的内联样式 {#example-inline-styles-for-a-field-component}

以下图像描述了应用内联样式之前和之后的文本字段。

应用内联样式之前的![文本框组件](assets/no-style.png)

应用内联样式属性之前的文本框组件

请注意应用以下CSS属性后文本框样式的更改，如下图所示。

<table>
 <tbody>
  <tr>
   <td><p>选择器</p> </td>
   <td><p>CSS属性</p> </td>
   <td><p>价值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>字段</p> </td>
   <td><p>边框</p> </td>
   <td><p>边框宽度=2像素</p> <p>边框样式=实线</p> <p>边框颜色=#1111</p> </td>
   <td><p>在字段周围创建黑色2px宽边框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>将背景颜色更改为CornflowerBlue (#6495ED)</p> <p>注意：您可以在值字段中指定颜色名称或其十六进制代码。</p> </td>
  </tr>
  <tr>
   <td><p>标签</p> </td>
   <td><p>维度和位置&gt;宽度</p> </td>
   <td><p>100像素</p> </td>
   <td><p>将标签的宽度固定为100px</p> </td>
  </tr>
  <tr>
   <td>字段帮助图标</td>
   <td>文本&gt;字体颜色</td>
   <td>#2ECC40</td>
   <td>更改帮助图标面部的颜色。</td>
  </tr>
  <tr>
   <td><p>详细描述</p> </td>
   <td><p>text-align</p> </td>
   <td><p>居中</p> </td>
   <td><p>将帮助的详细描述调整到中心</p> </td>
  </tr>
 </tbody>
</table>

应用内联样式后的![文本框样式](assets/applied-style.png)

应用内联样式属性后的文本框组件

按照上述步骤，您可以选择和设置其他组件的样式，如面板、提交按钮和单选按钮。

>[!NOTE]
>
>根据您选择的组件，样式属性会有所不同。
