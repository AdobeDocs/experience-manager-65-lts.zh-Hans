---
title: 开发和页面差异
description: 了解如何开发和利用Adobe Experience Manager中的页面差异功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 74ac70c9-a774-4b35-b285-3feb425dac3a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# 开发和页面差异{#developing-and-page-diff}

## 功能概述 {#feature-overview}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够并排比较当前页面与先前版本，并突出显示差异。

页面差异允许用户将当前页面与启动项、先前版本等进行比较。 有关此用户功能的详细信息，请参阅[页面差异](/help/sites-authoring/page-diff.md)。

## 操作详细信息 {#operation-details}

在比较页面的版本时，用户希望比较的先前版本由AEM在后台重新创建，以促进差异。 为了能够呈现内容[以进行并排比较](/help/sites-developing/pagediff.md#operation-details)，需要此项。

此娱乐操作由AEM在内部完成，对用户透明，无需干预。 但是，管理员查看存储库(例如，在CRXDE Lite中)时，将在内容结构中看到这些重新创建的版本。

比较内容时，会于以下位置重新创建整个树，一直到要比较的页面：

`/tmp/versionhistory/`

自动运行清理任务以清理此临时内容。

## 权限 {#permissions}

以前，在经典UI中，必须特别考虑开发以便AEM差异（例如使用`cq:text`标记库，或者自定义将`DiffService` OSGi服务集成到组件中）。 新的diff功能不再需要此功能，因为差异是通过DOM比较在客户端发生的。

但是，开发人员必须考虑一些限制。

* 此功能使用的CSS类未与AEM产品进行命名空间。 如果页面上包含其他具有相同名称的自定义CSS类或第三方CSS类，则差异的显示可能会受到影响。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由于diff是客户端并在页面加载时执行，因此不会考虑在客户端差异服务运行后对DOM进行的任何调整。 这可能会影响

   * 使用AJAX包含内容的组件
   * 单页面应用程序
   * 基于JavaScript的组件，可在用户交互时处理DOM。

>[!NOTE]
>
>页面差异比较仅适用于具有有效cq：editConfig节点的组件。
