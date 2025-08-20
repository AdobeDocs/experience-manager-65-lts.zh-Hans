---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS的发行说明'
description: 查找 Adobe Experience Manager 6.5 LTS 的当前版本信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 650c3659a451787539c8aac4aff38423a24262c3
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 95%

---

# Adobe Experience Manager 6.5 LTS 的最新发行说明 {#release-notes}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 LTS |
| 类型 | 主要版本 |
| 全面可用日期 | 2025 年 3 月 7 日 |

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS 是 [!DNL Adobe Experience Manager] 6.5 代码库的升级发行版本。它提供关键客户修复、高优先级客户增强功能以及增强产品稳定性的一般错误修复。它还包括达到 SP22 的 [!DNL Adobe Experience Manager] 6.5 Service Pack 发行版本。

下表提供了概述，接下来的页面列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 的平台的构建基础是更新版本的基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java™ 内容存储库：Apache Jackrabbit Oak 1.68.x。

Eclipse Jetty 11.0.x 被用作 Quickstart 的 servlet 引擎。

#### Java™ 支持  {#java-support}

* 支持 Java™ 17 和 Java™ 21。
* 为了获得最佳性能，请用其他值覆盖默认 GC 值。有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* 如果 Oracle 未公开提供，Adobe 会分配 Java™ 17 和 Java™ 21 维护更新，以便客户在 AEM 相关项目中使用。

#### Uberjar 包装 {#uber-jar-packaging}

* AEM 6.5 LTS 的 Uberjar 包装略有不同。有关详细信息，请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

#### 升级 {#upgrade}

* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 安装和更新 {#install-update}

有关设置要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 新安装 AEM 6.5 LTS 时，必须单独安装索引定义。有关详细信息，请参阅[本文](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 支持的平台 {#supported-platforms}

查找受支持平台的完整表格，包括 [AEM 6.5 LTS 技术要求](/help/sites-deploying/technical-requirements.md)的支持等级。

>[!NOTE]
>
>建议与 AEM 6.5 LTS 一起使用 Java™ 17/Java™ 21 版本。

## 已弃用和已移除的功能 {#deprecated-and-removed-features}

Adobe 不断审查产品功能，通过更新或取代旧功能来提高客户价值。这些改变都仔细考虑了向后兼容的情况。

沟通有关即将删除或取代 Adobe Experience Manager (AEM) 功能的消息时，适用以下规则：

1. 首先宣布弃用。已弃用的功能仍然可供使用，但不再继续改进。
1. 最早会在下一个主要版本中移除已弃用的功能。移除的实际目标日期会计划稍后公布。

在实际移除之前，此过程将为客户提供至少一个发布周期时间，使其实施适应已弃用功能的新版本或后续版本。

### 已弃用的功能  {#deprecated-features}

本节列出了 Adobe 在 AEM 6.5 LTS 中已弃用的功能。通常情况下，Adobe 在未来版本中移除某些功能之前，会先弃用这些功能并提供替代方案。


建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 区域 | 专题 | 替换 | 版本 (SP) |
|---|---|---|---|
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 管理 AEM 中的 Headless 内容时首选以下编辑器：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。 | 6.5 LTS GA |

### 已移除功能 {#removed-features}

此部分列出了 AEM 6.5 LTS 中已移除的功能。之前的版本中已将这些功能标记为已弃用。

| 区域 | 专题 | 替换 | 版本 (SP) |
|--- |--- |--- |--- |
| Commerce | 不支持 AEM CIF Classic。 | 迁移到 [AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解决方案 | 不支持社交/Communities。 | 没有替代功能可用。 | 6.5 LTS GA |
| Screens | 不支持 Screens。 | 没有替代功能可用。 | 6.5 LTS GA |
| 资产 | 不支持 `dam-pim` 和 `dam-rating`，因为捆绑包取决于社交。 | 没有替代功能可用。 | 6.5 LTS GA |
| 资产 | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` 已被移除。 | 使用已添加的替代 api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS GA |
| 门户 | 不支持 AEM Portal Director。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 捆绑包 `com.adobe.granite.socketio` 已被移除。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 不支持 `com.adobe.granite.crx-explorer`。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 不支持 `crx2oak`。 | 选择[Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)的相关版本 | 6.5 LTS GA |
| Adobe | 不支持 `com.adobe.cq.cq-searchpromote-integration`。 | 没有替代功能可用。 | 6.5 LTS GA |
| Guava | 现在，AEM 中的所有 guava 依赖项都已移除，因此 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 捆绑包不再是 AEM 的一部分。 | 如果客户依赖 guava，可以自行添加 guava，或者在可能的情况下用 Java 收藏集或其他替代功能取代 guava 代码。 | 6.5 LTS GA |
| `We.Retail` | 不支持`We-retail`示例站点。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 不支持 `oak-solr-osgi` 捆绑包。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 不支持 `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom` 和 `org.apache.sling.atom.taglib`。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 现在，`org.apache.commons.io` 包从 `org.apache.commons.commons-io` 导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | `javax.mail` 包正在从 `com.sun.javax.mail` 捆绑包中导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | `org.apache.jackrabbit.api` 包现在已从 `org.apache.jackrabbit.oak-jackrabbit-api` 捆绑包中导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | 不支持 `com.github.jknack.handlebars` | 选择相关[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS GA |

## 已知问题 {#known-issues}

### AEM 6.5.21-6.5.23 和 AEM 6.5 LTS GA 中的 JSP 脚本包问题

AEM 6.5.21、6.5.22、6.5.23 和 AEM 6.5 LTS GA 附带 `org.apache.sling.scripting.jsp:2.6.0` 捆绑包，其中包含一个已知问题。此问题经常在 AEM 实例处理许多并发请求而导致高负载的情况下发生。

发生此问题时，错误日志中可能会出现以下异常之一，并会引用 `org.apache.sling.scripting.jsp:2.6.0`：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

有一个热修复 [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) 可以解决这个问题。

### 使用仅 SSL 功能的情况下，Dispatcher 连接失败 {#ssl-only-feature}

在 AEM 部署中启用仅 SSL 功能后，会发生一个影响 Dispatcher 与 AEM 实例之间连接的已知问题。启用此功能后，健康检查可能会失败，并且 Dispatcher 和 AEM 实例之间的通信可能会中断。当客户尝试通过`https + IP`从Dispatcher连接到AEM实例时，会发生此问题。 它与SNI（服务器名称指示）验证问题有关。

**影响：** 

* 健康检查失败，出现 HTTP 400 响应码
* Dispatcher 与 AEM 实例之间的通信中断
* 无法通过 Dispatcher 正确提供内容
* 使用 HTTPS 与 Dispatcher 配置中的 IP 地址时连接失败
* 通过 HTTPS + IP 连接时出现 HTTP 400“SNI 无效”的错误

**受影响的环境：**

* 具有 Dispatcher 配置的 AEM 部署
* 启用了仅 SSL 功能的系统
* 使用 `https + IP` 方法与 AEM 实例连接的 Dispatcher 配置

**解决方法：**
如果您遇到此问题，请联系 Adobe 客户支持部门。有一个热修复 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 可以解决这个问题。采用必要的热修复之前，不要尝试启用仅 SSL 功能。

## 受限制的网站{#restricted-sites}

这些网站只提供给客户。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/customer-one/using/home)。

