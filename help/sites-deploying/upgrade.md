---
title: 升级到Adobe Experience Manager 6.5
description: 了解将旧版Adobe Experience Manager (AEM)安装升级到AEM 6.5的基础知识。
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: ebc34847-dc3d-41ed-b0d6-f004c3debcd9
source-git-commit: 4c3402aa813c115625d624f3b33ca73d31bed850
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 升级到Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>最后6个Service Pack支持升级到AEM 6.5 LTS。

本节介绍如何将AEM安装升级到AEM 6.5 LTS：

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

为便于引用这些过程中涉及的AEM实例，这些文章中使用了以下术语：

* *源*&#x200B;实例是从中升级的AEM实例。
* *target*&#x200B;实例是您要升级到的实例。

## 更改了哪些内容？ {#what-has-changed}

### 更新 {#updates}

基础层现在支持Java 17和Java 21，并包含来自Apache Sling、Felix和Jackrabbit Oak的最新开源捆绑包。 此外，AEM 6.5 LTS uber-jar的包装发生了变化。 此外，从AEM 6.5 LTS中删除了一些旧功能。 有关详细信息，请参阅[发行说明](/help/release-notes/release-notes.md#whats-new-what-s-new)和[升级后卸载的过时包列表](/help/sites-deploying/obsolete-bundles.md)

AEM 6.5 LTS非常重视功能的向后兼容性，并且附带分析器工具。 请参阅[使用AEM分析器评估升级复杂性](/help/sites-deploying/aem-analyzer.md)，以了解如何在开始[规划升级](/help/sites-deploying/upgrade-planning.md)时评估复杂性。
