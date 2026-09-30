---
title: 选择收集汇总的使用情况统计数据
description: 了解如何选择汇总的使用情况统计数据。
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 410691eb-27a9-4f8e-b926-01027c7f84d4
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: c191041a-8b54-4bde-9e43-bc8d8f8cea74
    internal-label: Deploying
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 3%
---
# 选择加入汇总使用情况统计信息收集{#opting-into-aggregated-usage-statistics-collection}

## 简介 {#introduction}

您可以发送有关您如何与Adobe Experience Cloud (AEM)交互的Adobe统计数据，帮助改进Adobe Experience Manager。 此信息不包含有关贵公司网站访客的任何数据，并且仅用于帮助Adobe提供、支持和改善您的用户体验。

您可以使用触屏UI或Web控制台选择收集使用情况统计数据。

>[!NOTE]
>
>有各种数据保护与隐私条例；例如，包括GDPR和CCPA。 AEM Sites随时准备帮助客户履行其数据保护和隐私合规义务。 本页将指导客户完成选择加入（或退出）汇总使用情况统计信息收集的过程。
>
>有关详细信息，另请参阅[Adobe的隐私中心](https://www.adobe.com/cn/privacy.html)。

>[!NOTE]
>
>您可以随时选择退出，方法是使用[Web控制台]&#x200B;(#opt-in-by-using-the-web-console，或不选择AEM选择加入屏幕上的选择加入选项。

## 使用触屏UI选择加入 {#opt-in-by-using-the-touch-ui}

首次启动AEM时，您可以使用触屏UI选择加入，如下所示：

1. 在AEM导航屏幕上，单击&#x200B;**收件箱** （铃铛）图标。

   ![usage_statisticsnavigationscreen](assets/usage_statisticsnavigationscreen.png)

1. 在下拉列表中，单击&#x200B;**启用聚合使用情况统计信息收集**。

   ![usage_statisticsnavigationscreen2](assets/usage_statisticsnavigationscreen2.png)

1. 在选择加入屏幕上，单击选项&#x200B;**[!UICONTROL 允许收集汇总的使用情况统计数据]**。

   ![usage_statisticsopt-inscreen](assets/usage_statisticsopt-inscreen.png)

1. 单击&#x200B;**完成**。

## 使用Web控制台选择加入 {#opt-in-by-using-the-web-console}

您可以使用Web控制台选择加入（或选择退出），如下所示：

1. 在AEM导航屏幕上，单击&#x200B;**工具**，然后单击&#x200B;**操作**。

   ![usage_statisticssopssdashboard](assets/usage_statisticsopsdashboard.png)

1. 在“操作”窗口中，单击&#x200B;**Web控制台**。

   ![usage_statisticswebconsole](assets/usage_statisticswebconsole.png)

1. 搜索&#x200B;**汇总的使用情况统计信息集合**。
1. 单击&#x200B;**编辑**&#x200B;图标。

   ![usage_statisticscollectionedit](assets/usage_statisticscollectionedit.png)

1. 选中&#x200B;**启用**&#x200B;复选框。 或者，如果您希望选择退出使用统计信息收集，则可以取消选中该复选框。

   ![usage_statisticsselect](assets/usage_statisticsselect.png)

1. 单击&#x200B;**保存**。
