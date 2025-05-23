---
title: 组件概述
description: 组件是模块化单元，可实施特定功能以在您的网站上展示您的内容
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 364eebca-b4cf-470b-994e-9e56ec68597b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 45%

---

# 组件概述{#components-overview}

此页面概述了 Adobe Experience Manager (AEM) 组件，例如那些[用于页面创作](/help/sites-authoring/default-components-foundation.md)的组件。

## 什么是组件？ {#what-exactly-is-a-component}

* 实现特定功能以在网站上展示内容的模块化单元。
* 可重用的。
* 作为存储库的一个文件夹中的独立单元开发。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系统中的任何位置运行。 它们还可以限制为在特定组件下运行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用使用基于Granite UI组件的子元素构建的对话框
* 使用[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hans)（推荐）或JSP开发。
* 可以开发以创建扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将它部署到测试环境。
* 将它部署到实时创作环境，作者和/或管理员可在该环境中添加和配置内容。
* 将其部署到您的实时发布环境，其中使用它们为网站的访客呈现内容。 某些组件（例如，Communities）也接受用户的输入。

每个 AEM 组件：

* 是一种资源类型。
* 是一个完全实施特定功能的脚本的集合。
* 可在&#x200B;*isolation*&#x200B;中运行，即在AEM或门户中运行。

## AEM中的现成组件 {#out-of-the-box-components-within-aem}

AEM附带各种[现成的组件](/help/sites-authoring/default-components.md)，可提供全面的功能，包括：

* 段落系统(`parsys`)
* 页面（`responsivegrid` — 仅限触控式UI）
* 文本
* 图像，带随附文本
* 工具栏

在[示例We.Retail网站](/help/sites-developing/we-retail.md)中提供的组件及其用法说明了如何实施和使用组件。 这些组件随所有源代码一起提供，可以按原样使用或用作已修改或扩展的组件的起点。

### 核心组件和基础组件 {#core-components-and-foundation-components}

提供了两组Adobe提供的AEM组件：

* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [Foundation 组件 ](/help/sites-authoring/default-components-foundation.md)

**核心组件**&#x200B;是随AEM 6.3引入的，它提供了灵活且丰富的创作功能。 [We.Retail参考网站](/help/sites-developing/we-retail.md)说明了如何使用核心组件，并代表了组件开发的当前最佳实践。

**Foundation组件**&#x200B;已在AEM中提供了多个版本，并且可在标准AEM安装中现成使用。 尽管仍受支持，但大多数技术已弃用，不再增强，并且基于旧版技术。

>[!NOTE]
>
>[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)表示组件设计和开发的当前最佳实践，并用作参考实施。
>
>[AEM现代化工具](modernization-tools.md)可以帮助迁移到核心组件。

### 查看可用组件 {#viewing-available-components}

有关AEM实例中所有可用组件的概述，请使用[组件控制台](/help/sites-authoring/default-components-console.md)。

或者，您也可以使用 CRXDE Lite 获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite]** 中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，这将打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡中，选择 `XPath` 作为&#x200B;**[!UICONTROL 类型]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**，这将列出组件。

## 其他资源 {#further-reading}

以下页面提供了有关开发这些组件及其他组件的更详细信息：

* [AEM组件 — 基础知识](/help/sites-developing/components-basics.md)
* [开发AEM组件](/help/sites-developing/developing-components.md)
* [开发AEM组件 — 代码示例](/help/sites-developing/developing-components-samples.md)
* [配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md)
* [开发人员模式](/help/sites-developing/developer-mode.md)
* [测试UI](/help/sites-developing/hobbes.md)
* [内容片段的组件](/help/sites-developing/components-content-fragments.md)
* [获取JSON格式的页面信息](/help/sites-developing/pageinfo.md)
* [国际化组件](/help/sites-developing/i18n.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)
* [使用隐藏条件](/help/sites-developing/hide-conditions.md)
* 经典 UI

   * [AEM组件（经典UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和扩展小组件（经典UI）](/help/sites-developing/widgets.md)
   * [使用xtype（经典UI）](/help/sites-developing/xtypes.md)
   * [开发Forms（经典UI）](/help/sites-developing/developing-forms.md)
