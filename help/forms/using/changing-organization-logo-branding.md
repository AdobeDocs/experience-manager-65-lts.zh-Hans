---
title: 更改品牌推广的组织徽标
description: 要打造AEM Forms工作区，请通过自定义默认徽标提供您组织的徽标。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 更改品牌推广的组织徽标 {#changing-the-organization-logo-for-branding}

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
