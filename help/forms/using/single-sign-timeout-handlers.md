---
title: 单点登录和超时处理程序
description: 如何设置AEM Forms工作区的会话超时值。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: c6bdfa6f-0d9b-4473-a2e1-6cad73fbd1ed
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 单点登录和超时处理程序 {#single-sign-on-and-timeout-handlers}

AEM Forms工作区已启用SSO。 如果用户已登录到AEM Forms应用程序(如Forms Manager或PDF Generator用户界面)，并在同一浏览器会话中访问AEM Forms工作区，则用户将登录到AEM Forms工作区，反之亦然。

## 在AEM Forms工作区中处理服务器超时 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

可以在Administration Console中配置用户的会话超时。

要设置超时，请登录到`https://'[server]:[port]'/adminui`，导航到&#x200B;**设置>用户管理>配置>配置高级系统属性**，然后进行所需的设置。

在AEM Forms中，工作区超时的处理方式为：

* 用户的会话持续时间在响应`initialize`调用时可用，该调用初始化用户会话。
* 一个弹出对话框会通知用户会话即将过期，即在会话过期前15秒。

在此弹出对话框中：

* 单击“确定”结束用户会话。
* 单击“取消”重新初始化用户会话。

>[!NOTE]
>
>如果未执行任何操作，则会在会话到期前三秒自动将用户从AEM Forms工作区注销。
