---
title: 输出、Forms和（记录文档）DoR服务的连接问题
description: 解决SP19之后的AEM Forms连接错误。 停止，安装Microsoft Visual C++，重新启动服务器以获得无缝的解决方案。 排查输出故障、Forms、DoR服务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: c84ba536-a78d-4cf9-a480-59cb18e41076
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---

# 无法使用输出服务、Forms服务或记录文档(DoR)服务 {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 问题

安装AEM Forms 6.5 Service Pack 19后，尝试使用输出服务、Forms服务或记录文档(DoR)服务可能会导致`Connection to failed service`错误。

## 解决方案

要解决此问题：

1. 停止AEM 6.5 Forms实例。
1. 在安装了Microsoft 6.5 Forms的计算机上下载并安装适用于Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位版本的AEM Visual C++可再发行包。
1. 重新启动AEM Forms服务器。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。


>[!NOTE]
>
>
> 确保您安装了可再发行组件，即使安装了以前的版本也是如此。
