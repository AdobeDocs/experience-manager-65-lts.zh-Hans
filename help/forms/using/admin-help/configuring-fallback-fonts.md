---
title: 配置回退字体
description: 了解如何为AEM Forms配置后备字体。 可以使用FontManagerResources.properties文件将默认字体手动映射到回退字体。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d11bb8dc-d0fe-4182-88dd-9ef1ecf687db
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 配置回退字体 {#configuring-fallback-fonts}

您可以手动配置FontManagerResources.properties文件，以便在服务器上没有默认字体时，将默认的AEM Forms字体映射到回退（或替换）。 此属性文件位于adobe-fontmanager.jar文件中。

>[!NOTE]
>
>回退字体配置也适用于汇编程序服务。

1. 导航到&#x200B;*`[aem-forms root]`*/configurationManager/export目录中的adobe-livecycle-*`[appserver]`*.ear文件，制作备份副本，然后取消打包原始文件。
1. 找到adobe-fontmanager.jar文件并将其解包。
1. 找到FontManagerResources.properties文件并在文本编辑器中将其打开。
1. 根据需要修改“通用”和“后备”字体位置和名称，并保存文件。

   FontManagerResources.properties文件中的字体条目相对于&#x200B;*`[aem-forms root]`*/fonts目录。 如果指定的字体不是默认的AEM表单字体，则必须将这些字体安装在此目录结构内（在现有目录内或新创建的目录中）。

   >[!NOTE]
   >
   >如果指定的字体或默认字体不包含特定的Unicode字符，或者该字符不可用，则根据以下优先级从回退字体中获取该字符：

   * 区域设置特定的字体
   * 如果未设置区域设置，则为ROOT字体
   * 通用字体，按回退表中的顺序集搜索

1. 重新打包adobe-fontmanager.jar文件。
1. 重新打包adobe-livecycle-*`[appserver]`*.ear文件，然后手动或通过运行Configuration Manager重新部署该文件。

>[!NOTE]
>
>请勿使用Configuration Manager重新打包adobe-livecycle-`[appserver]`.ear文件，因为这将使用AEM表单默认值覆盖您的修改。
