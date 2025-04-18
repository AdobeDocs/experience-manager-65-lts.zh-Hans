---
title: 更改字符集
description: 您可以指定用于编码输出流的字符集。 了解如何更改字符集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1d614736-5897-4fd3-9ca4-94b115139ba3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# 更改字符集 {#change-the-character-set}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以指定用于编码输出流的字符集。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>输出]**。
1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置依赖于通过API指定的`TransformationFormat`和`PrintFormat`。 要指定列出的字符集以外的字符集，请选择自定义，然后在显示的框中指定编码值。

   如果`TransformationFormat`是PDF，而PDF/A或`PrintFormat`是PCL、PostScript、Zebra标签、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，则仅支持特定字符集。

   字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击&#x200B;**[!UICONTROL 保存]**。
