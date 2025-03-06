---
title: 配置远程端点
description: 了解如何配置远程端点。 本文档介绍如何使用AEM Forms Remoting启用使用Flex构建的应用程序以调用服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: d19b7265-42cc-41d9-9897-e7b044c4529c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# 配置远程端点 {#configuring-remoting-endpoints}

通过远程端点，使用Flex构建的应用程序可以使用(不推荐用于AEM表单)AEM Forms Remoting调用服务。 将为每个激活的服务自动创建远程端点。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的远程对象，以调用对相关服务的操作。

## 远程端点设置 {#remoting-endpoint-settings}

**Flex客户端身份验证方法：**&#x200B;确定在调用的服务启用了安全性、调用的操作不支持匿名调用，并且客户端未传递凭据或凭据无效时，服务器发送回客户端的响应类型。
