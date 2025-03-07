---
title: 指定XCI配置选项
description: 了解如何指定XCI配置选项 您可以为自适应表单指定自定义XCI文件值，以便在表单渲染时使用该值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5fb6e6cc-6af7-4cf5-804b-bb3030079383
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# 指定XCI配置选项 {#specify-xci-configuration-options}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

输出允许您指定用于呈现的自定义XCI文件。 请参阅[指定输出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)的文件位置。

默认情况下，“输出”会覆盖XCI文件中指定的某些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上面所列选项覆盖的选项，在这种情况下，输出使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击&#x200B;**服务** >输出。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择该选项， Output将对数据包、创建者、生成者和compressObjectStream设置使用其默认值。 取消选择此选项时，输出使用自定义XCI文件中指定的值。
1. 单击&#x200B;**保存**。
