---
title: 面向AEM开发人员的最佳实践
description: Adobe工程和咨询团队开发了一组面向AEM开发人员的全面的最佳实践。
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: fc2aa62a-3fc4-491d-aff5-74896998d7d6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# 最佳实践{#best-practices}

## 开发人员最佳实践 — 快速入门 {#best-practices-for-developers-getting-started}

Adobe工程和咨询团队开发了一组面向AEM开发人员的全面的最佳实践。 Adobe开发人员在开发用于客户实施的核心AEM产品更新和客户代码时，应遵守这些最佳实践。

在开始AEM开发项目之前，请先查看以下最佳实践：

* [开发实践](/help/sites-developing/development-practices.md)
* [内容架构](/help/sites-developing/content-architecture.md)
* [软件体系结构](/help/sites-developing/software-architecture.md)
* [编码提示](/help/sites-developing/coding-tips.md)
* [代码陷阱](/help/sites-developing/code-pitfalls.md)
* [JCR交互](/help/sites-developing/jcr-integration.md)
* [OSGi包](/help/sites-developing/osgi-bundles.md)
* [Java API最佳实践](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=zh-Hans)

### 其他最佳实践信息 {#additional-best-practices-information}

以下区域提供了专门用于开发最佳实践的文档：

* [Sites](#sites)
* [工具/HTL](#tooling-htl)

下面的表格中介绍了特定文档并将其链接到该文档。

有关管理、部署和维护或创作的最佳实践，请参阅以下内容之一：

* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

## Sites {#sites}

管理和创作网站内容有一些最佳实践，如下所示：

<table>
 <tbody>
  <tr>
   <td>支持标准触屏UI的一些理论。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">触屏优化UI：概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">触屏优化UI：结构</a></p> </td>
   <td>这些文档概述了触屏UI的概念和结构。</td>
  </tr>
  <tr>
   <td>触屏优化UI：自定义控制台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自定义触屏UI控制台</a></td>
   <td>本文档介绍了扩展触屏UI控制台的最佳方法。</td>
  </tr>
  <tr>
   <td>触屏UI：自定义页面创作</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自定义触屏UI页面创作</a></td>
   <td>描述如何扩展触屏UI的页面创作。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">开发和扩展工作流</a></td>
   <td><p>借助工作流，您可以自动执行Adobe Experience Manager (AEM)活动，并且可以显示在AEM环境中发生的大量处理，因此强烈建议仔细规划工作流实施。</p> </td>
  </tr>
 </tbody>
</table>

## 工具/HTL {#tooling-htl}

HTML模板语言(HTL)是随AEM 6.0引入的新HTML模板系统。它取代了JSP和ESP作为AEM的首选模板系统。

|  |  |  |
|---|---|---|
| HTL 概述 | [HTL概述和语法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hans) | 本文档介绍HTL是什么、如何移动到HTL、示例项目、语法、表达式和语句 |
| 在Java中使用API | [HTL Java Use-API](https://helpx.adobe.com/cn/experience-manager/htl/using/use-api.html) | HTL Java Use-API让HTL文件可以访问自定义Java类中的Helper方法。 |

>[!NOTE]
>
>以下多部分教程可能与设置新AEM项目的最佳实践相关，其中详细介绍核心组件、可编辑模板、客户端库和组件开发：
>[AEM Sites快速入门 — WKND教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
