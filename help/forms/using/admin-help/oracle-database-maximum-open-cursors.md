---
title: Oracle 数据库最大打开游标阈值
description: 了解如何在Oracle中为打开游标配置最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 13%
---
# Oracle 数据库最大打开游标阈值 {#oracle-database-maximum-open-cursors-threshold}

要在Oracle中配置打开游标的最大值，可能必须将此值调整为适合您的应用程序的值。 显然，在中等负载下，平均打开游标为2700。 建议您从3000的上限开始。 有关详细信息，请转到[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
