---
title: 如何重新启动AEM SDK？
description: 重新启动AEM SDK的最佳实践
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: 68935045-89b1-4219-b111-88a4600200df
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# 重新启动AEM SDK

如果通过停止Java™进程来重新启动AEM SDK，可能会导致AEM开发环境不一致，并出现以下错误：

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![重新启动 — aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 解决方案

要重新启动AEM SDK，请转到活动命令窗口，然后按`Ctrl + C`命令重新启动SDK。

建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法(例如，停止Java™进程)重新启动AEM SDK可能会导致AEM开发环境不一致。
