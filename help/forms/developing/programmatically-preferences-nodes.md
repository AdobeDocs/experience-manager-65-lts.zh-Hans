---
title: 以编程方式管理PreferencesNodes
description: 使用首选项管理器服务API (Java)以编程方式管理首选项节点。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 2%

---

# 以编程方式管理首选项节点 {#programmatically-managing-the-preferencesnodes}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

本主题介绍如何使用首选项管理器服务API (Java)以编程方式管理首选项节点。

您可以从管理员UI手动更改配置设置。 要更改选项，请导航到`Home>Settings>User Management> Configuration>Manual Configuration`。 进行更改后导入`config.xml`，您会注意到除了在节点`/Adobe/Adobe Experience Manager Forms/Config/UM persist`进行的更改之外的所有更改都将丢失。 用户管理导入和导出预览不支持更改其他组件的配置设置。 现在，可以使用`PreferencesManagerServiceClient` API进行这些更改。

**步骤摘要**
要以编程方式管理首选项节点，请执行以下操作：

1. 包括项目文件。
1. 创建`PreferencesManagerService`客户端。
1. 调用相应的角色或权限操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建`PreferencesManagerService`客户端**

您必须先创建`PreferencesManagerService`客户端，然后才能以编程方式执行用户管理`PreferencesManagerService`操作。 使用Java API创建一个`PreferencesManagerServiceClient`对象。

**调用适当的角色或权限操作**

创建服务客户端后，可以调用Preferences Manager操作。 服务客户端允许您读取和设置权限。
