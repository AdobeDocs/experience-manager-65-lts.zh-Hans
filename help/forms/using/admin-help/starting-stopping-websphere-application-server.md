---
title: 启动和停止WebSphere应用程序服务器
description: 多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 启动和停止WebSphere应用程序服务器 {#starting-and-stopping-websphere-application-server}

多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，可以首先查看WebSphere应用程序服务器的状态。

## 查看WebSphere应用程序服务器的状态 {#view-the-status-of-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `serverStatus.bat`*服务器名称*
   * (Linux、UNIX) 。/ `serverStatus.sh`*服务器名称*

## 启动WebSphere应用程序服务器 {#start-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `startServer.bat`*服务器名称*
   * (Linux、UNIX) 。/ `startServer.sh`*服务器名称*

## 停止WebSphere应用程序服务器 {#stop-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `stopServer.bat`*服务器名称*
   * (Linux、UNIX) 。/ `stopServer.sh`*服务器名称*
