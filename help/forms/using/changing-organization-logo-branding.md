---
title: 更换组织徽标以进行品牌化
description: 要打造AEM Forms工作区，请通过自定义默认徽标提供您组织的徽标。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
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
source-wordcount: '116'
ht-degree: 10%
---
# 更换组织徽标以进行品牌化 {#changing-the-organization-logo-for-branding}

组织徽标显示在AEM Forms工作区的左上角。 要更新徽标，请按照AEM Forms工作区自定义的[常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)操作，然后执行以下步骤。

1. 创建徽标并将文件命名为`NewWorkspace.png`。 使用WebDAV客户端将图像文件放置到/apps/ws/images文件夹中。

   >[!NOTE]
   >
   >徽标图像的推荐大小为218像素×20像素。

   >[!NOTE]
   >
   >有关详细信息，请参阅[WebDAV访问](/help/sites-administering/webdav-access.md)。

1. 通过添加以下样式，在/apps/ws/css/newStyle.css的样式表中引用新的徽标图像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
