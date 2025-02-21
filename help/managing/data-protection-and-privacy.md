---
title: 数据保护和数据隐私条例 — Adobe Experience Manager准备工作
description: 了解Adobe Experience Manager对各种数据保护和数据隐私条例的支持。 其中包括欧盟《通用数据保护条例》(GDPR)、《加州消费者隐私法案》，以及在实施新的AEM项目时如何实现合规性。
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
source-git-commit: d1297182b801ff4db163b8ae91332f5aebb94b9b
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 44%

---

# 用于数据保护和数据隐私法规的Adobe Experience Manager已准备就绪 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询您公司的法律部门，以获取关于数据保护和数据隐私条例的建议。

>[!NOTE]
>
>要详细了解 Adobe 对隐私问题的响应以及这对于您这样的 Adobe 客户的意义，请参阅 [Adobe 隐私中心。](https://www.adobe.com/cn/privacy.html)

Adobe为客户隐私管理员或AEM管理员提供文档和过程（在可用时通过API）以处理数据保护和数据隐私请求。 它可以帮助您遵守这些法规。 记录的过程允许客户从外部门户或服务手动运行监管请求，或者通过调用API（在可用时）来运行监管请求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager。
>
>其他 Adobe 按需插件的服务以及任何相关隐私请求需要在该服务上采取操作。
>
>有关更多信息，请参阅 [Adobe 隐私中心。](https://www.adobe.com/cn/privacy.html)

## 简介 {#introduction}

Adobe Experience Manager的实例以及其上运行的应用程序由Adobe客户负责和运营。

因此，GDPR、CCPA 及其他数据保护条例在很大程度上由客户负责。

作为一个简单的介绍，数据隐私和保护条例包括下列各方需要遵守的新规则：

* 业务实体 (CCPA) 和/或数据控制方 (GDPR)

* 服务提供商 (CCPA) 和/或数据处理商 (GDPR)

此类条例中的主要条款：

1. 扩展了个人数据的定义，以包括唯一 ID（在可直接和间接识别身份的数据中）。

2. 强化了对同意书的要求。

3. 增加了对删除权利的关注（数据清除）。

4. 数据销售的选择退出。

对于Adobe Experience Manager：

* 实例以及其上运行的应用程序由客户负责和运营。

   * 客户管理监管角色，包括业务实体和服务提供商、数据控制方和数据处理商等。

   * Adobe Experience Platform Privacy Service 不在 AEM 的工作流中，如下图所述。

* AEM 包括面向客户隐私管理员和/或 AEM 管理员的文档和过程，可手动或通过 API（在可用时）执行隐私监管请求。

* 未添加新的服务或 UI。

   * 而是记载了由处理隐私监管请求的客户 UI/门户使用的过程和 API。

* AEM 不包括任何现成的工具来支持隐私请求工作流。

   * Adobe为客户隐私管理员和AEM管理员提供了文档和过程，使他们能够手动运行与隐私法规相关的请求。

Adobe提供了用于处理与Adobe Experience Manager的访问、删除和选择退出相关的隐私请求的过程。 有时，可以从客户开发的门户或脚本中调用可用的API来帮助实现自动化。

下图说明了隐私请求工作流可能的样子（使用 Adobe Experience Manager 6.5 说明）：

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和监管准备工作 {#aem-and-regulatory-readiness}

有关AEM产品领域的监管文档，请参阅以下部分。

## AEM Foundation {#aem-foundation}

请参阅[处理AEM Foundation的数据保护和隐私请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## AEM选择收集汇总使用情况统计数据 {#aem-opting-into-aggregate-usage-statistics-collection}

请参阅[汇总的使用情况统计信息收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

## AEM Sites {#aem-sites}

请参阅[AEM Sites — 数据保护和隐私就绪。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM与Adobe Target和Adobe Analytics的集成 {#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager集成与支持数据保护和隐私（例如，GDPR或CCPA）的服务相集成。 Adobe Target或Adobe Analytics中的任何个人数据都不会存储在与集成相关的AEM中。

有关更多信息，请参阅以下内容：

* [Adobe Target - 隐私概述](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 数据隐私工作流](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Forms {#aem-forms}

AEM Forms包括捕获、处理和存储数据以编排业务流程和完成数字交易的组件和工作流。 不同的组件使用不同的数据存储，并允许与自定义数据存储集成。 以下文档介绍了访问和处理用户数据的过程和准则，以支持组件的数据保护和隐私（例如，GDPR或CCPA）工作流。

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [与Adobe Sign集成](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上以Forms为中心的工作流](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流](/help/forms/using/forms-workflow-jee-handling-user-data.md)(仅限AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md)(仅限AEM Forms JEE)
* [用户管理](/help/forms/using/user-management-handling-user-data.md)(仅限AEM Forms JEE)
