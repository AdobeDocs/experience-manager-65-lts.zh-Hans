---
title: 设置超时值以用于Acrobat Reader DC扩展
description: 了解如何设置超时值以用于Acrobat Reader DC扩展。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 设置超时值以用于Acrobat Reader DC扩展  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在Acrobat Reader DC Extensions中处理许多PDF文件时，请确保正确设置以下超时值，以防止作业超时和失败：

**文档处理超时**

可以在管理控制台中设置此值。 单击设置>核心系统设置>配置，并指定默认文档处理超时值。

**用户管理器AEM表单超时：**&#x200B;可以通过编辑config.xml文件来设置此值。 在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”，然后单击“导出”。 打开导出的config.xml文件并编辑以下行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

保存config.xml文件，然后将其导入管理控制台。

**应用程序服务器会话超时：**&#x200B;可以在应用程序服务器上设置此值。 有关详细信息，请参阅随应用程序服务器提供的文档。
