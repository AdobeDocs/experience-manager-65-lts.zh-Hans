---
title: 兼容包
description: 通过在AEM Forms 6.5 LTS上安装兼容包，您可以使用AEM Forms 6.5及更早版本中的通信管理资源以及已弃用的自适应表单模板和页面
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# 兼容包{#compatibility-package}

## 概述 {#overview}

在AEM Forms 6.5 LTS中，交互式通信是创建客户通信的默认和推荐方法。 若要继续使用AEM Forms 6.5 LTS中的字母，您需要安装最新的[AEMFD兼容包](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)。

AEMFD兼容包还允许您[在AEM Forms 6.5 LTS上使用AEM Forms 6.5.22.0、6.4、6.3和6.2中的以下资源](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 文档片段
* 书信
* 数据字典
* 自适应表单弃用的模板和页面

有关详细信息，请参阅通过安装兼容包[&#128279;](../../forms/using/compatibility-package.md#assetsmadecompatible)使与AEM Forms 6.5兼容的Assets。

## 在AEM Forms 6.5 LTS中添加对AEM Forms 6.5、6.4、6.3和6.2资源的支持 {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

执行升级后，请执行以下操作以安装AEMFD兼容包，并使您的资产与6.5兼容：

确保您已预安装[AEM兼容包](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)。

1. 安装最新的AEM 6.5 LTS [兼容包](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)。

   有关上载和安装包的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。

1. 在日志稳定后，重新启动服务器。
1. 使用迁移实用程序使您的资产与6.5 LTS兼容。

   >[!NOTE]
   >
   > 建议使用`Ctrl + C`命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。

   有关详细信息，请参阅[迁移实用程序](../../forms/using/migration-utility.md)。

## 通过安装兼容包，Assets与AEM Forms 6.5 LTS兼容 {#assetsmadecompatible}

通过安装兼容包，您可以使以下资源和模板与AEM Forms 6.5 LTS兼容：

* AEM 6.4及更早版本中的通信管理Assets：

   * [书信](../../forms/using/create-letter.md)
   * [数据字典](/help/forms/using/data-dictionary.md)
   * 文档片段

* 自适应表单已弃用的模板：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 自适应表单已弃用页面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
