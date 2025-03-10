---
title: Oracle数据库最大打开游标阈值
description: 了解如何在Oracle中为打开游标配置最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Oracle数据库最大打开游标阈值 {#oracle-database-maximum-open-cursors-threshold}

要在Oracle中配置打开游标的最大值，可能必须将此值调整为适合您的应用程序的值。 显然，在中等负载下，平均打开游标为2700。 建议您从3000的上限开始。 有关详细信息，请转到[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
