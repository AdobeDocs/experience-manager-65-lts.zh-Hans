---
title: 自适应表单中的分隔符组件
description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 8b1a9626-6de1-4b19-bb93-ada667f24e83
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 10%

---

# 自适应表单中的分隔符组件{#separator-component-in-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。</span>

可使用分隔符组件以可视方式分隔表单的面板。 通过指定分隔符组件的以下属性，可以定义分隔符组件的整体外观和样式：

* **元素名称：**&#x200B;指定组件的名称。 SOM表达式使用在元素名称字段中指定的值寻址组件。
* **粗细：**&#x200B;指定分隔符组件的粗细（像素）。

* **CSS类：**&#x200B;指定分隔符组件的自定义CSS类

* **内联样式：**&#x200B;使用AEM Forms，您现在可以将内联CSS样式应用于各个自适应表单组件并实时预览更改。

您可以使用布局模式定义分隔符组件跨越的列数。 有关详细信息，请参阅[使用布局模式调整组件大小](../../forms/using/resize-using-layout-mode.md)。

要指定分隔符组件的属性，请执行以下操作：

1. 选择分隔符组件并选择![cmppr](assets/cmppr.png)。 这些属性将在侧栏中打开。
1. 单击“内联CSS属性”部分中的选项卡，以便指定CSS属性。 例如：a。在字段选项卡中，单击&#x200B;**添加项**。 将添加包含两个字段的行。
1. 在左侧的第一个字段中，指定要应用的CSS3属性。 例如，**边框**。 您还可以通过单击向下箭头按钮选择资产。 下拉列表并非详尽无遗，您可以在此字段中指定任何受支持的CSS3属性名称。
1. 在相邻的字段中，为指定的CSS3属性指定有效值。 例如，**3-px实心黑色**。
1. 单击&#x200B;**添加项**&#x200B;以指定另一个属性及其值。
1. 单击&#x200B;**预览**，以便预览表单中的更改。
1. 如果要确认更改，请单击&#x200B;**确定**，或单击&#x200B;**取消**&#x200B;退出对话框而不进行任何更改。
