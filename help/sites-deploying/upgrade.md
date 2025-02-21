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
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# 升级到Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>最后6个Service Pack支持升级到AEM 6.5 LTS。

本节介绍如何将AEM安装升级到AEM 6.5：

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

以下是AEM最近几个版本中的注释主要更改：

1. 基础层已升级为支持Java 17(它包含Apache Sling、Apache Felix和Apache Jackrabbit Oak的开源捆绑包层)

1. AEM 6.5 LTS jar打包现在支持Jarkarta Servlet API规范5，并且可以将战争打包部署到实施Jarta Servlet API规范5/6的servlet容器中

1. AEM 6.5 LTS uber-jar的包装已更改。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)。

### 已删除旧版功能/构件 {#removed-legacy-features-artifacts}

以下旧版解决方案已从AEM 6.5 LTS中删除。 有关详细信息，请参阅TBD：指向发行说明的链接和[升级后卸载的过时捆绑包列表](/help/sites-deploying/obsolete-bundles.md)

1. Social
1. 商务
1. Screens
1. We-retail
1. 搜索与提升的集成

**已删除项目**

1. CRX-explorer
1. Crx2oak
1. Google guava（由于安全漏洞而被删除）
1. Abdera-parser（由于安全漏洞而被删除）
1. jdom (`org.apache.servicemix.bundles.jdom`)（由于安全漏洞已删除）
1. `com.github.jknack.handlebars` （由于安全漏洞已删除）

AEM 6.5 LTS非常重视功能的向后兼容性，并且附带分析器工具。 请参阅[使用AEM分析器评估升级复杂性](/help/sites-deploying/pattern-detector.md)，了解开始规划升级时的复杂性评估。 有关其他更改的详细信息，请参阅此处的完整发行说明。 待定：AEM 6.5 LTS发行说明的链接