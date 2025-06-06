---
title: 配置翻译规则
description: 了解如何定义翻译规则，标识要翻译的内容。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
exl-id: 94534336-1e1f-40eb-8364-9358c1420616
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 91%

---

# 配置翻译规则 {#configure-translation-rules}

了解如何定义翻译规则，标识要翻译的内容。

## 迄今为止的故事 {#story-so-far}

您在 AEM Headless 翻译历程的上一个文档[配置翻译集成](configure-connector.md)中了解了如何安装和配置您的翻译集成，而现在应：

* 了解 AEM 中翻译集成框架的重要参数。
* 能够自行建立与翻译服务的连接。

现已设置您的集成，本文将引导您完成下一步，即确认需要翻译的内容。

## 目标 {#objective}

本文档可帮助您了解如何使用 AEM 的翻译规则来标识翻译内容。阅读本文档后，您应：

* 了解翻译规则的用途。
* 能够定义您自己的翻译规则。

## 翻译规则 {#translation-rules}

代表您的 Headless 内容的内容片段可以包含按结构化字段编排的许多信息。根据您的项目需求，可能不必翻译内容片段中的所有字段。

翻译规则标识翻译项目中包含或排除的内容。在翻译内容时，AEM 会根据这些规则提取或收集内容。这样一来，只会将必须翻译的内容发送到翻译服务。

翻译规则包含以下信息：

* 规则应用于的内容的路径
   * 规则也应用于内容的后代
* 包含要翻译的内容的属性的名称
   * 属性可以特定于某个特定的资源类型或所有资源类型

由于定义了内容片段结构的内容片段模型是您自己的项目所独有的，因此，设置翻译规则至关重要，这样一来，AEM 才能知道要翻译的内容模型元素。

>[!TIP]
>
>通常，内容架构师为翻译专家提供翻译所需的所有字段的&#x200B;**属性名称**。 需要使用这些名称才能配置翻译规则。作为翻译专家，您[可以自行查找这些&#x200B;**属性名称**](getting-started.md#content-models)，如本历程中前面所述。

## 创建翻译规则 {#creating-rules}

可以创建多个规则来支持复杂的翻译要求。例如，一个您可能正在处理的项目需要翻译模型的所有字段，但在另一个项目中，仅需翻译描述字段，而标题无需翻译。

翻译规则旨在处理此类情况。但在此示例中，我们通过关注一个简单的单一配置来说明如何创建规则。

提供了一个用于配置翻译规则的&#x200B;**翻译配置**&#x200B;控制台。要访问它，请执行以下操作：

1. 导航到&#x200B;**工具** > **常规**。
1. 单击&#x200B;**翻译配置**。

在&#x200B;**翻译配置** UI 中，有若干选项可用于您的翻译规则。下面我们重点介绍基本 Headless 本地化配置所需的最为必要和典型的步骤。

1. 单击&#x200B;**添加上下文**，以添加路径。 这是受规则影响的内容的路径。
   ![添加上下文](assets/add-translation-context.png)
1. 使用路径浏览器选择所需的路径，然后单击&#x200B;**确认**&#x200B;按钮进行保存。 请记住，包含 Headless 内容的内容片段通常位于 `/content/dam/<your-project>` 下。
   ![选择路径](assets/select-context.png)
1. AEM 将保存配置。
1. 选择您创建的上下文，然后单击&#x200B;**编辑**。 这将打开&#x200B;**翻译规则编辑器**&#x200B;以配置属性。
   ![翻译规则编辑器](assets/translation-rules-editor.png)
1. 默认情况下，所有配置都继承自父路径，在此示例中为 `/content/dam`。取消选中选项&#x200B;**从`/content/dam`**&#x200B;继承以向配置添加其他字段。
1. 取消选中后，在列表的&#x200B;**常规**&#x200B;部分下，添加您[之前标识为翻译字段](getting-started.md#content-models)的内容片段模型的属性名称。
   1. 在&#x200B;**新属性**&#x200B;字段中输入属性名称。
   1. 这将自动选中&#x200B;**翻译**&#x200B;和&#x200B;**继承**&#x200B;选项。
   1. 单击&#x200B;**添加**。
   1. 对您必须翻译的所有字段重复这些步骤。
   1. 单击&#x200B;**保存**。

      ![添加属性](assets/add-property.png)

您现在已配置翻译规则。

## 高级用法 {#advanced-usage}

有若干其他属性可配置为您的翻译规则的一部分。此外，还可手动将规则指定为 XML，而这可提高独特性和灵活性。

通常，无需此类功能即可开始本地化您的 Headless 内容，但如果您愿意，可以参阅[其他资源](#additional-resources)部分以了解详细信息。

## 后续内容 {#what-is-next}

现在，您已完成 Headless 翻译历程的这一部分，您应：

* 了解翻译规则的用途。
* 能够定义您自己的翻译规则。

在此知识的基础上继续您的 AEM Headless 翻译历程，接下来请查阅文档[翻译内容](translate-content.md)，您将从中了解您的集成和规则如何共同翻译 Headless 内容。

## 其他资源 {#additional-resources}

我们建议您查看文档[翻译内容](translate-content.md)来继续 Headless 翻译历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续 Headless 历程所必需的。

* [标识要翻译的内容](/help/sites-administering/tc-rules.md) – 了解翻译规则如何标识需要翻译的内容。
