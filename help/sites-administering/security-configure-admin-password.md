---
title: 安装时配置管理员密码
description: 了解如何在Adobe Experience Manager安装时更改管理员密码。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 安装时配置管理员密码{#configure-the-admin-password-on-installation}

## 概述 {#overview}

从版本6.3开始，Adobe Experience Manager (AEM)允许在安装新实例时使用命令行设置管理员密码。

在AEM的早期版本中，安装后必须更改管理员帐户的密码以及各种其他控制台的密码。

此功能增加了在安装AEM实例期间为存储库和Servlet引擎设置新管理员密码的功能，因此无需在以后手动执行此操作。

>[!CAUTION]
>
>功能不包括Felix控制台，必须手动更改其密码。 有关详细信息，请参阅相关的[安全清单部分](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 如何使用它？ {#how-do-i-use-it}

如果您选择通过命令行安装AEM，而不是从文件系统资源管理器中双击JAR，则会自动触发此功能。

从命令行运行AEM实例的常规语法为：

```shell
java -jar aem6.3.jar
```

从命令行运行实例后，会为您提供在安装过程中更改管理员密码的选项：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安装新的AEM实例时，才会显示更改管理员密码的提示。

## 使用 — nointeractive标志 {#using-the-nointeractive-flag}

也可以选择从属性文件指定口令。 这是通过使用与`-Dadmin.password.file`系统属性结合使用的`-nointeractive`标记完成的。

示例如下：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties`文件内的密码必须具有以下格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只使用`-nointeractive`参数而不使用`-Dadmin.password.file`系统属性，AEM将使用默认管理员密码而不要求您进行更改，这实际上会复制早期版本的行为。 此非交互模式可用于在安装脚本中使用命令行进行自动安装。
