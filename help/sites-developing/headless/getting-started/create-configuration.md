---
title: 创建配置Headless快速入门指南
description: 创建配置作为在AEM 6.5中开始使用Headless的第一步。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 6792f5c0-074e-4465-9b84-8be78abd6b8f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 68%

---

# 创建配置Headless快速入门指南 {#creating-configuration}

作为在AEM 6.5中开始使用Headless的第一步，您需要创建配置。

## 什么是配置？ {#what-is-a-configuration}

配置浏览器提供了通用配置 API、内容结构、针对 AEM 中配置的解析机制。

在 AEM 的 Headless 内容管理的上下文中，请将配置视为 AEM 中的工作区，您可以在其中创建内容模型，这将定义未来内容和内容片段的结构。您可以使用多个配置来分隔这些模型。

>[!NOTE]
>
>如果您熟悉[全栈 AEM 实施中的页面模板](/help/sites-authoring/templates.md)，使用配置进行内容模型的管理的过程非常相似。

## 如何创建配置 {#how-to-create-a-configuration}

管理员只需要创建配置一次，或者在极少数情况下，需要新工作区用于组织内容模型时进行创建。对于本指南快速入门，我们只需要创建一个配置。

1. 登录AEM，从主菜单选择&#x200B;**工具>常规>配置浏览器**。
1. 为您的配置提供&#x200B;**标题**。
   * 名称将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/sites-developing/naming-conventions.md)。它将成为存储库中的节点名称。
1. 查看以下选项：
   * **内容片段模型**
   * **GraphQL 持久查询**

   ![创建配置](assets/create-configuration.png)

1. 单击&#x200B;**创建**

如果需要，您可以创建多个配置。配置也可以嵌套。

>[!NOTE]
>
>根据您的实施请求，可能还需要&#x200B;**内容片段模型**&#x200B;和 **GraphQL 持久查询**&#x200B;之外的配置选项。

## 后续步骤 {#next-steps}

使用此配置，您现在可以转到快速入门指南的第二部分并[创建内容片段模型](create-content-model.md)。

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
