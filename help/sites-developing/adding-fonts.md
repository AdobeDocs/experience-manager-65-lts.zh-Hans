---
title: 添加用于图形渲染的字体
description: AEM允许您生成包含从内容中动态获取的文本的图形
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 5ceaa9f0-aba1-40a3-97ef-f5ade0c2a54a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---

# 添加用于图形渲染的字体{#adding-fonts-for-graphic-rendering}

AEM允许您生成包含从内容中动态获取的文本的图形。

为此，您还可以加载和使用自己的字体。

当前Java平台的所有实施都支持[TrueType](https://en.wikipedia.org/wiki/Truetype)字体。

1. 打开CRXDE Lite并导航到您的项目应用程序文件夹：

   `/apps/<your-project>/`

1. 在`/apps/<your-project>/`下创建节点：

   * **名称**：`fonts`
   * **类型**：`sling:Folder`

   保存所有更改。

1. 将字体文件复制到此文件夹中；例如，使用WebDAV。

   >[!NOTE]
   >
   >存储库中的字体文件必须具有后缀`*.ttf`或`*.TTF`。

1. 更新[Day Commons GFX字体帮助程序](/help/sites-deploying/osgi-configuration-settings.md)的[OSGi配置](/help/sites-deploying/configuring-osgi.md)。 添加字体文件夹的路径；即`/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 现在，您应该会在包含导入字体名称的文件夹中看到一个`.fontlist`节点。

   这些字体现在可以在Java API中使用。

有关如何将这些字体与Java API一起使用的完整详细信息，请参阅[有关Java API的Font类的文档](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)。
