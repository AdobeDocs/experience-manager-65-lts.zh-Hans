---
title: 为 AEM Forms 应用程序设置环境
description: 用于构建和部署AEM Forms应用程序的硬件、软件和许可证。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 41799183-ef5a-4990-bd7b-7b58cafe3960
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%
---
# 为 AEM Forms 应用程序设置环境{#set-up-environment-for-aem-forms-app}

您需要以下硬件、软件和许可证来构建和部署AEM Forms应用程序：

## 对于Windows设备 {#for-windows-devices}

* ® Windows 10
* ® Visual Studio 2015
* ® Visual Studio Tools for Apache Cordova

## 对于iOS设备 {#for-ios-devices}

* 运行macOS X 10.9.5或更高版本的基于英特尔的Apple Mac
* iOS SDK 8.4或更高版本
* Xcode版本：适用于OS X或更高版本的Xcode 6.4
* iOS开发人员企业计划成员
* 用于分发内部iOS应用程序的企业证书
* Apple iPad与iOS 8.4或更高版本

## 对于™设备 {#for-android-devices}

* 可从[https://developer.android.com/studio](https://developer.android.com/studio)下载的Android™ Development Toolkit （ADT包）
* 如果在Mac系统上设置了环境，则ADT应安装在Applications文件夹中。
* 如果ADT安装在Mac上的任何其他位置，或者环境设置在Windows系统上，则必须在`local.properties`文件中更新ADT SDK路径。 此文件在提取的源存档`mobileworkspace-src.zip`的`src\android`文件夹中可用。 在此文件中，将`sdk.dir`变量指向桌面上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。 确保未预装PhoneGap SDK。
