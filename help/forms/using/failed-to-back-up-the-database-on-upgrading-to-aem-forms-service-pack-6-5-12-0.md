---
title: 在升级到MySQL的6.5.12.0期间备份数据库失败。
description: 当用户升级到Experience Manager 6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 升级到MySQL的6.5.12.0期间备份数据库失败 {#issue}

当用户升级到Experience Manager 6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库，它显示以下错误：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 应用于 {#applies-to}

* Experience Manager 6.5 Forms

## 解决方案 {#solution}

要解决此问题，请将数据库的max_packet_size增加到100 M，或者根据位于{AEM_HOME}/mysql的my.ini文件中的要求进行增加。
