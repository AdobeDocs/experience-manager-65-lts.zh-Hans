---
title: 启动和停止 WebSphere 应用程序服务器
description: 多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 20cd6efb-edcf-4c87-b0f5-bdec5a0f6280
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
source-wordcount: '180'
ht-degree: 6%
---
# 启动和停止 WebSphere 应用程序服务器 {#starting-and-stopping-websphere-application-server}

多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，可以首先查看WebSphere应用程序服务器的状态。

## 查看WebSphere应用程序服务器的状态 {#view-the-status-of-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `serverStatus.bat`*服务器名称*
   * (Linux， UNIX) ./ `serverStatus.sh`*服务器名称*

## 启动WebSphere应用程序服务器 {#start-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `startServer.bat`*服务器名称*
   * (Linux， UNIX) ./ `startServer.sh`*服务器名称*

## 停止WebSphere应用程序服务器 {#stop-websphere-application-server}

1. 从命令提示符转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows) `stopServer.bat`*服务器名称*
   * (Linux， UNIX) ./ `stopServer.sh`*服务器名称*
