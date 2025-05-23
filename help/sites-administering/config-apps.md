---
title: 为AEM应用程序配置
description: 了解如何使用Adobe Experience Manager应用程序更新应用程序OTA（空中）的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: 4f36487c-45a2-4c18-b3cc-bb9284d68f49
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 为AEM应用程序配置{#configuring-for-aem-apps}

Adobe Experience Manager应用程序允许您更新应用程序OTA的内容（空中）。 更新的内容存储在发布实例上。 要允许设备上的应用程序连接到发布实例并检查更新，必须将发布实例配置为允许空的反向链接标头。

## 配置空反向链接标头 {#configuring-empty-referrer-header}

配置反向链接筛选服务：

* 在以下位置打开Apache Felix控制台（**配置**）：
* https://&lt;服务器>：&lt;端口号>/system/console/configMgr
* 以管理员身份登录。
* 在&#x200B;**配置**&#x200B;菜单中，选择： *Apache Sling引用过滤器*
* 选中允许空字段，以便您可以允许为空/缺少反向链接标头。
* 单击&#x200B;**保存**&#x200B;以保存更改。

![chlimage_1-58](assets/chlimage_1-58a.png)

有关更多详细信息，请参阅[OSGI配置设置](/help/sites-deploying/osgi-configuration-settings.md)和[安全核对清单 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。
