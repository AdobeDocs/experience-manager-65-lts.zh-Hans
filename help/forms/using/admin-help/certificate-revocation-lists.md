---
title: 管理证书吊销列表
description: 了解如何管理证书吊销列表。 您可以使用信任存储区管理导入、编辑和删除证书吊销列表(CRL)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5e49cc8-cd46-47e6-8ff3-655dcf23296a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 管理证书吊销列表{#managing-certificate-revocationlists}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

使用信任存储区管理，您可以导入、编辑和删除证书吊销列表(CRL)。 支持Base64和DER编码的证书吊销列表。

## 导入CRL {#import-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”，然后单击“导入”。
1. 在“别名”框中，键入CRL的标识符。
1. 单击“浏览”以找到CRL，然后单击“确定”。

## 导出CRL {#export-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 单击CRL的别名以便导出，然后单击“导出”。
1. 按照说明导出CRL。 CRL以Base64编码导出。
1. 单击“确定”。

## 删除CRL {#delete-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 选中要删除的CRL的复选框，单击“删除”，然后单击“确定”。
