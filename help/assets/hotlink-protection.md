---
title: 在Dynamic Media中激活热链接保护
description: 有关如何在Dynamic Media中激活热链接保护的信息。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
feature: Configuration
solution: Experience Manager, Experience Manager Assets
exl-id: 56eb956e-c6a8-464b-980a-28e0dab0da7c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 在Dynamic Media中激活热链接保护 {#activating-hotlink-protection-in-dynamic-media}

热链接是指第三方网站使用HTML代码显示您网站中的图像的情况。 每次请求图片时，他们都会使用您的带宽，因为访客的浏览器会直接从您的服务器访问图片。 热链接&#x200B;*保护*&#x200B;是一种方法，可阻止其他网站直接链接到您网页上的图片、CSS或JavaScript。 这种屏蔽有助于减少Dynamic Media帐户下不必要的带宽使用量。

[Experience Manager客户支持](https://experienceleague.adobe.com/zh-hans?support-solution=Experience+Manager#support)可以在CDN （内容分发网络）级别配置反向链接过滤器，以便仅将Dynamic Media内容提供给域中允许网站列表中的网站。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。 要激活热链接保护，管理员必须创建Adobe客户支持支持工单，以请求对您的Dynamic Media帐户进行配置更改。 激活热链接保护不需要额外付费。
