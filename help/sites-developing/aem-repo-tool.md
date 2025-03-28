---
title: AEM Repo 工具
description: AEM Repo Tool是一种简单的解决方案，可通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具类似于Jackrabbit FileVault工具，但速度更快，具有最小的依赖关系，并且是一个简单的bash脚本。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: c762e9dd-cd22-40f4-aee4-fd832032dea4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# AEM Repo 工具{#aem-repo-tool}

AEM Repo Tool是一种简单的解决方案，可通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo Tool类似于[Jackrabbit FileVault tool](/help/sites-developing/ht-vlttool.md)，但速度更快，具有最小的依赖关系，而且是一个简单的bash脚本。

此工具简化了开发人员的文件传输，并且还可以集成到IntelliJ和Eclipse中，以提高开发效率。

## 概述 {#overview}

对于文件系统上的`jcr_root`文件文件结构内的给定路径，AEM Repo Tool会为整个子树创建一个带有单个过滤器的包，并将该包推送到服务器（类似于FTP `put`），从服务器( `get`)获取该包，或者比较差异（`status`和`diff`）。

该工具不支持多个筛选器路径或FileVault的`filter.xml`。

>[!CAUTION]
>
>AEM Repo工具始终会覆盖指定的整个文件或目录。

## 下载和文档 {#download-and-documentation}

[AEM Repo Tool可通过此链接](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上获取，并附有详细的安装和使用说明。

如果要下载AEM Repo工具的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
