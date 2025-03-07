---
title: PDF Generator备份限制
description: 了解PDF Generator备份限制。 PDF Generator使用的临时目录无法备份，因为它以设定的时间间隔清除内容。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f76ce3be-6d50-4531-a982-2e902f866208
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator备份限制 {#pdf-generator-backup-limitations}

PDF Generator用于转换文件的临时目录无法备份。 即使服务已正确恢复，数据仍可能会丢失，因为PDF Generator会按设定的时间间隔查看和清除临时目录的内容。
