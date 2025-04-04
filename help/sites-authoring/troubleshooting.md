---
title: 在AEM中进行创作时疑难解答
description: 您在使用AEM时可能会遇到的一些问题。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 1e735d57-834a-4251-9b92-ccc6d4712f2a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 41%

---

# 解决 AEM 中有关创作方面的问题{#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>如果遇到问题，也值得检查实例（发行版和Service Pack）的[已知问题](/help/release-notes/release-notes.md)列表。

>[!NOTE]
>
>具有管理员权限的用户以及希望对AEM问题进行故障排除的用户，可以使用[AEM故障排除（适用于管理员）](/help/sites-administering/troubleshoot.md)中所述的故障排除方法。 如果您没有足够的权限，请联系系统管理员来解决AEM问题。

## 发布站点上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：

   * 您已经更改了一个页面，并将该页面复制到发布站点，但该页面的&#x200B;*旧*&#x200B;版本仍显示在发布站点上。

* **原因**：

   * 这可能有多种原因，通常是缓存(本地浏览器或Dispatcher)，但有时也可能是复制队列问题。

* **解决方案**：

   * 下面提供了多种可能性：
   * 确认已正确复制该页面。 检查页面状态，并在必要时检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * 向页面 URL 的结尾处添加 `?`。例如：

      * `http://localhost:4502/sites.html/content?`
      * 这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。

   * 如果复制队列存在问题，请与系统管理员联系。

## 组件操作在工具栏上不可见 {#component-actions-not-visible-on-toolbar}

* **问题**：

   * 在创作环境中编辑内容页面时，所有适用的组件操作均不可见。

* **原因**：

   * 在极少数情况下，之前的操作可能会影响工具栏。

* **解决方案**：

   * 刷新页面。
