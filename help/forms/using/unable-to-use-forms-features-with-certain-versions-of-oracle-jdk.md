---
title: 无法将Experience Manager Forms与Oracle JDK的某些版本一起使用
description: 无法将Experience Manager Forms与Oracle JDK的某些版本一起使用
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# 无法将Experience Manager Forms与Oracle JDK的某些版本一起使用 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

该问题适用于以下版本：

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 问题 {#issue}

用户遇到以下异常：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

当您运行版本高于或等于以下版本的Experience Manager Forms与Oracle JDK （Java开发工具包）时，会发生例外情况：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述及更高版本的Java在JVM（Java虚拟机）中包含新的XML处理限制，这些限制会导致某些Forms特定操作失败。

## 解决方法 {#workaround}

1. 停止Experience Manager Forms服务器。
1. 为应用程序服务器配置以下JVM参数：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它将JVM中的system属性设置为相当高的值，以便不达到默认限制。

1. 启动Experience Manager Forms服务器。
