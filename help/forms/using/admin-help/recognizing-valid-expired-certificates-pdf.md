---
title: 识别 PDF 文档中的有效证书和过期证书
description: 了解如何在PDF文档中识别有效证书和过期的证书。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: f7402f0d-7c19-4a56-8630-208faa197f94
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
source-wordcount: '198'
ht-degree: 8%
---
# 识别 PDF 文档中的有效证书和过期证书 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中打开具有Reader扩展应用的使用权限的PDF文档时，将显示一个状态栏，其中描述在PDF文档中启用的特定使用权限。

当指定PDF文档使用权限的数字证书过期并在Adobe Reader中打开PDF文档时，会出现一个对话框，告知用户该PDF文档具有使用权限，但这些权限被禁用。 尽管消息表明PDF文档被更改或篡改，但情况不一定如此。 当证书过期或修改文档时，Adobe Reader会显示此消息。 在Adobe Reader 7.0.x或更高版本中，无法确定当前问题是哪种情况。

关闭对话框后，Adobe Reader将打开PDF文档。 使用Acrobat Reader DC扩展应用的使用权限无法按预期使用。 如果PDF文档是交互式表单，则表单字段会被锁定，用户无法更改表单数据。
