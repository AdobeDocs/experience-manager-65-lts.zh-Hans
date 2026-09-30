---
title: 配置通信管理解决方案
description: 了解如何在AEM Forms环境中配置通信管理解决方案。
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: da668935-9d16-49e1-8e7a-772fc4040c1d
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%
---
# 配置通信管理解决方案 {#configuring-a-correspondence-management-solution}

## 为VersionRestoreManagerImpl定义创作实例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步骤可为创作实例版本还原定义创作实例URL：

1. 转到&#x200B;*https://：&lt;PublishHost>：&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**&#x200B;设置旁边的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL VersionRestoreManager创作URL]**&#x200B;字段中，指定VersionRestoreManager的创作实例的URL。

   **URL字符串**：

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果有多个作者实例（群集的）由负载平衡器提前，请在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;字段中指定指向负载平衡器的URL。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 定义ActivationManagerImpl（公共实例激活管理器）的发布实例URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

请按照以下步骤操作，以便您能够为公共实例激活管理器定义发布实例URL：

1. 转到&#x200B;*https://：&lt;authorHost>：&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**&#x200B;设置旁边的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL ActivationManager发布URL]**&#x200B;字段中，指定用于访问发布实例ActivationManager的URL。 您可以提供以下URL。

   * **负载平衡器URL（推荐）**：提供负载平衡器URL，如果您的Web服务器在发布场前面充当负载平衡器（多个非群集发布实例）。
   * **发布实例URL**：提供任意发布实例URL，如果您只有一个发布实例，或者由于任何限制而无法从创作环境访问发布场前的Web服务器。 如果指定的发布实例出现故障，创作端会有一个回退机制来处理。
   * **URL字符串**：

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击&#x200B;**[!UICONTROL 保存]**。

有关配置通信管理的详细信息，请参阅[通信管理配置属性](https://helpx.adobe.com/cn/aem-forms/6-2/cm-configuration-properties.html)。
