---
title: 日志文件
description: 诸如运行时错误或启动错误等事件将记录到应用程序服务器日志文件中，这些文件可以使用任何文本编辑器打开。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# 日志文件 {#log-files}

诸如运行时错误或启动错误等事件将记录到应用程序服务器日志文件中。 如果在部署到应用程序服务器时遇到任何问题，可以使用日志文件来帮助您查找问题。 您可以使用任何文本编辑器打开日志文件。

(JBoss)以下日志文件位于`[appserver root]/server/'server'/log`目录中：

* 启动日志
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)域日志文件位于`[appserverdomain]`目录中，服务器日志文件位于`[appserverdomain]/servers/[appserver name]/logs`目录中：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)以下日志文件位于`[appserver root]/profiles/default/logs/[appserver name]`目录中：

* 系统错误日志
* SystemOut.log
* StartServer.log
