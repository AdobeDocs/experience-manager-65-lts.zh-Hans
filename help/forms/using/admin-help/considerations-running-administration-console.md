---
title: 运行Administration Console时的注意事项
description: 本文档列出了运行Administration Console时要考虑的一些要点。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: bdd884c4-ae12-4827-8251-01033cbc0185
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 运行Administration Console时的注意事项 {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

运行Administration Console时需要考虑以下几点：

* 如果使用URL `https://[hostname]:'port'/adminui`访问管理控制台，则指定的主机名不能包含下划线字符。 否则，指向管理控制台某些区域的链接可能无法正常工作。
* 如果在日语操作系统的Windows资源管理器中运行管理控制台，则可能会遇到以下问题：

   * 单击链接会返回登录页面，而不是预期的链接。
   * 单击链接会显示权限错误。

  最佳实践是从其他浏览器（如Mozilla Firefox）运行管理控制台，以确保没有任何链接失败。

* 在管理控制台中执行搜索时，请勿使用反斜杠字符()。
