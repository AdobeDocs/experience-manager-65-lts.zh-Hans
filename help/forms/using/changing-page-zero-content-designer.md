---
title: 在 Designer 中更改 Page Zero 内容
description: 在非Adobe PDF查看器中查看XFA PDF时，您知道如何更改在该页面的第0页上显示的消息吗？
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: f966f5fb-338a-4d8e-91c6-aa0eddd03420
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# 在 Designer 中更改 Page Zero 内容 {#changing-page-zero-content-in-designer}

如果非Adobe PDF查看器(如[!DNL Chrome]或[!DNL Firefox]中的默认PDF查看器)无法读取PDF/XFA表单的内容，则默认显示零页内容。 默认的Page Zero消息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms]版本的Designer允许您更改在第0页上显示的消息。 要更改Page Zero消息，请执行以下步骤：

1. 确保您已安装[!DNL AEM Forms]版本的Designer。 您可以从设计器的“关于”屏幕中检查版本。

1. 打开要为其更改“页面零”内容的表单。

1. 单击&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 表单属性]**。

1. 在[!UICONTROL 表单属性]对话框中，单击![加号](assets/plus.png)（加号图标）以添加自定义属性。

1. 将&#x200B;**_pagezerocontent**&#x200B;指定为属性的名称。
1. 以富文本格式添加新的“页面零”消息作为值。 例如：


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download_cn.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader_cn.</p></body>`

1. 将表单另存为PDF。

1. 在浏览器中查看PDF表单，确认消息已更新。 上面的示例值如下所示：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>重新打开表单时，您创建的自定义属性可能无法正确显示在表单属性对话框中。 但是，它可正常使用，并且表单会显示更新的零页消息。
