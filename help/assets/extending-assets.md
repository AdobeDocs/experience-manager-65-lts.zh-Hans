---
title: 自定义和扩展 [!DNL Assets]
description: 了解自定义和扩展Asset Share和Asset Editor的方法，为用户提供专门定制的界面和功能集。
contentOwner: AG
role: Developer
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
exl-id: d4826314-a714-47b2-bf4d-029dc47982ce
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 自定义和扩展[!DNL Assets] {#customizing-and-extending-assets}

资产编辑器是Adobe Enterprise Manager网站的用户用于查找、查看和处理存储库中数字资产的主要访问点。

作为[!DNL Experience Manager]开发人员，您可以通过多种方式自定义和扩展资产编辑器，从而为用户提供量身定制的界面和功能集。

可以自定义或增强功能的以下方面：

* [扩展资产编辑器](asseteditorx.md)
* [扩展Assets搜索](searchx.md)
* [使用媒体处理程序和工作流处理Assets](media-handlers.md)
* [将Assets与活动流集成](extending-activity-stream.md)
* [Assets代理开发](proxy.md)
* [配置ImageMagick的最佳实践](best-practices-for-imagemagick.md)

## 自定义外观 {#customizing-the-look-and-feel}

Asset Editor的以下外观和风格是可自定义的：

* 徽标：您可以将您自己的组织的徽标添加到界面中。
* 颜色和字体：可以更改界面中使用的颜色和字体。
* HTML代码：要进行更全面的自定义，您可以更改用于定义界面的基础HTML代码。

## 自定义演绎版 {#customizing-renditions}

在[!DNL Experience Manager Assets]术语中，演绎版是用来展示资源的形式。 通常，特定资产可以具有多个演绎版。 例如，全色图像可能有一个原始大小的演绎版，另一个是按比例缩小大小的演绎版，另一个是按比例缩小并转换为灰度的演绎版。

可以自定义特定资源可用的演绎版并创建新演绎版。
