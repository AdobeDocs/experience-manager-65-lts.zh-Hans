---
title: Adobe Experience Manager 6.5 LTS的最新发行说明
description: 查找Adobe Experience Manager 6.5 LTS的最新发行信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 02b9f90dc9ef504f04a9b1f692358089d4626094
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 18%

---

# Adobe Experience Manager 6.5 LTS的最新发行说明 {#release-notes}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5磅 |
| 类型 | 主要版本 |
| 正式发布日期 | 2025年3月7日 |

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS是[!DNL Adobe Experience Manager] 6.5代码库的升级版本。 它提供了关键客户修复、高优先级的客户增强功能，以及针对产品稳定性的一般错误修复。 它还包含最多SP22的[!DNL Adobe Experience Manager] 6.5 Service Pack版本。

下面的列表提供了概述，而后续页面列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS的平台基于基于OSGi的框架的更新版本（Apache Sling和Apache Felix）以及Java™内容存储库(Apache Jackrabbit Oak 1.68.x)构建。

Eclipse Jetty 11.0.x用作Quickstart的servlet引擎。

#### Java™支持  {#java-support}

* 支持Java™ 17和Java™ 21。
* 为获得最佳性能，请用其他值覆盖默认的GC值。 有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Adobe为在AEM相关项目中使用的客户分发Java™ 17和Java™ 21维护更新(如果Oracle不公开提供)。

#### Uberjar包装 {#uber-jar-packaging}

* AEM 6.5 LTS的Uberjar包装略有不同。 有关详细信息，请参阅[更新AEM Uber Jar版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

#### 升级 {#upgrade}

* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 安装和更新 {#install-update}

有关安装要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 支持的平台 {#supported-platforms}

查找支持的平台的完整列表，包括有关[AEM 6.5 LTS技术要求](/help/sites-deploying/technical-requirements.md)的支持级别。

>[!NOTE]
>
>推荐将Java™ 17/Java™ 21与AEM 6.5 LTS一起使用。

## 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe会不断检查产品功能，以便通过使旧功能现代化或替换旧功能来提高客户价值。 在进行这些更改时，请注意向后兼容性。

为了传达即将移除或替换的Adobe Experience Manager (AEM)功能，以下规则适用：

1. 首先宣布弃用。虽然已弃用，但功能仍然可用，但不会进一步增强。
1. 至少会在以下主要版本中移除已弃用的功能。 计划稍后公告实际移除日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

### 已弃用的功能 {#deprecated-features}

本部分列出Adobe在AEM 6.5 LTS中已弃用的特性和功能。 通常，在将来的版本中删除功能之前，Adobe会先弃用这些功能，并提供替代功能。


建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 区域 | 专题 | 替换 | 版本(SP) |
|---|---|---|---|
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 管理 AEM 中的 Headless 内容时首选以下编辑器：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。 | 6.5 LTS GA |

### 已删除功能 {#removed-features}

本部分列出从AEM 6.5 LTS中删除的特性和功能。 以前的版本中这些功能标记为已弃用。

| 区域 | 专题 | 替换 | 版本(SP) |
|--- |--- |--- |--- |
| 商务 | 不支持AEM CIF Classic。 | 迁移到[AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解决方案 | 不支持社交/社区。 | 没有可用的替换。 | 6.5 LTS GA |
| Screens | 不支持Screens。 | 没有可用的替换。 | 6.5 LTS GA |
| 资产 | 不支持`dam-pim`和`dam-rating`，因为捆绑包依赖于social。 | 没有可用的替换。 | 6.5 LTS GA |
| 资产 | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()`已删除。 | 使用已添加的替代API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS GA |
| 门户 | 不支持AEM Portal Director。 | 没有可用的替换。 | 6.5 LTS GA |
| Granite | 已删除包`com.adobe.granite.socketio`。 | 没有可用的替换。 | 6.5 LTS GA |
| Granite | 不支持`com.adobe.granite.crx-explorer`。 | 没有可用的替换。 | 6.5 LTS GA |
| Granite | 不支持`crx2oak`。 | 选择[oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)的相关版本 | 6.5 LTS GA |
| Adobe | 不支持`com.adobe.cq.cq-searchpromote-integration`。 | 没有可用的替换。 | 6.5 LTS GA |
| 瓜瓦 | AEM中的所有Guava依赖项现已删除，因此`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002`包不是AEM的一部分。 | 如果客户依赖瓜瓦，则可以自行添加瓜瓦；如果可能，还可以使用Java收藏集或其他替代项替换瓜瓦代码。 | 6.5 LTS GA |
| We.Retail | 不支持We-Retail示例站点。 | 没有可用的替换。 | 6.5 LTS GA |
| 开源 | 不支持`oak-solr-osgi`包。 | 没有可用的替换。 | 6.5 LTS GA |
| 开源 | 不支持`org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`和`org.apache.sling.atom.taglib`。 | 没有可用的替换。 | 6.5 LTS GA |
| 开源 | 现在从`org.apache.commons.commons-io`导出`org.apache.commons.io`个包。 | 无需更改。 | 6.5 LTS GA |
| 开源 | 正在从`com.sun.javax.mail`包中导出`javax.mail`个包。 | 无需更改。 | 6.5 LTS GA |
| 开源 | 现在从`org.apache.jackrabbit.oak-jackrabbit-api`包中导出`org.apache.jackrabbit.api`个包。 | 无需更改。 | 6.5 LTS GA |
| 开源 | 不支持`com.github.jknack.handlebars` | 选择相关的[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS GA |

## 已知问题 {#known-issues}

### AEM 6.5.21-6.5.23和AEM 6.5 LTS GA中的JSP脚本包问题

AEM 6.5.21、6.5.22、6.5.23和AEM 6.5 LTS GA随`org.apache.sling.scripting.jsp:2.6.0`捆绑包一起提供，其中包含已知问题。 当AEM实例处理许多并发请求时，高负载下通常会出现问题。

出现此问题时，错误日志中可能会出现以下异常之一，并伴有对`org.apache.sling.scripting.jsp:2.6.0`的引用：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

出现此错误时，唯一的恢复方法是重新启动AEM实例。

请联系Adobe客户支持并参考此发行说明以获得解决方案。

### Dispatcher连接失败及仅SSL功能 {#ssl-only-feature}

在AEM部署中启用仅SSL功能时，有一个已知问题会影响Dispatcher和AEM实例之间的连接。 启用此功能后，运行状况检查可能会失败，Dispatcher实例与AEM实例之间的通信可能会中断。

**影响：**

* HTTP 500响应代码的运行状况检查失败
* Dispatcher和AEM实例之间的流量中断
* 无法通过Dispatcher正确提供内容

**受影响的环境：**

* AEM部署和Dispatcher配置
* 启用了仅SSL功能的系统

**解决方案：**
如果您遇到此问题，请联系Adobe客户支持。 有修补程序[cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.0.zip)可用于解决此问题。 在应用必要的修补程序之前，请勿尝试启用仅SSL功能。

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载位于licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/zh-hans/docs/customer-one/using/home)。

