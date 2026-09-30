---
title: 设置系统信息服务
description: 了解如何设置系统信息服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: e31614a9-d670-4d22-88ba-8953797f6e14
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 10%
---
# 设置系统信息服务 {#set-up-the-system-information-service}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

系统信息服务提供REST API以检索信息。 要使用系统信息服务，请从管理控制台启用REST端点。 执行以下步骤以启用REST端点：

1. 登录到管理控制台。 管理控制台的默认URL为`https://[hostname]:'port'/adminui.`
1. 导航到“服务”>“应用程序和服务”>“服务管理”。
1. 在“服务管理”页面上，单击&#x200B;**SystemInfo**&#x200B;服务。
1. 在“端点”选项卡的列表中，选择REST，然后单击&#x200B;**添加**。
1. 在“添加REST终结点”屏幕上，单击&#x200B;**添加**。
