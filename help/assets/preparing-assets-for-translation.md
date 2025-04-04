---
title: 准备要翻译的资产
description: 创建语言根文件夹以准备要翻译的资产以支持多语言资产。
contentOwner: AG
role: User, Admin
feature: Projects
solution: Experience Manager, Experience Manager Assets
exl-id: de9f266b-a167-4eba-be2c-8f6a0457265f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# 准备要翻译的资产 {#preparing-assets-for-translation}

多语言资源是指具有多种语言的二进制文件、元数据和标记的资源。 通常，资产的二进制文件、元数据和标记都以一种语言存在，然后会翻译成其他语言以用于多语言项目。

在[!DNL Adobe Experience Manager Assets]中，多语言资源包含在文件夹中，其中每个文件夹都包含采用不同语言的资源。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）标识了语言副本中内容的语言。 例如，*/content/dam/it*&#x200B;是意大利语副本的意大利语根。 语言副本必须使用[正确配置的语言根](preparing-assets-for-translation.md#creating-a-language-root)，以便在翻译源资源时定位正确的语言。

最初添加资产的语言副本是主要语言。 主要语言是翻译成其他语言的源。 示例文件夹层次结构包括几个语言根：

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

执行以下步骤可准备要翻译的资产：

1. 创建主要语言的语言根。 例如，示例文件夹层次结构中英语副本的语言根是`/content/dam/en`。 确保根据[创建语言根](preparing-assets-for-translation.md#creating-a-language-root)中的信息来正确配置语言根。

1. 将资源添加到您的主要语言。
1. 创建需要语言副本的每个目标语言的语言根。

## 创建语言根 {#creating-a-language-root}

要创建语言根，请创建一个文件夹并使用ISO语言代码作为Name属性的值。 创建语言根后，您可以在语言根的任何级别创建语言副本。

例如，示例层次结构的意大利语副本的根页面将`it`作为Name属性。 Name属性用作存储库中资产节点的名称，从而确定资产的路径。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 从[!DNL Assets]控制台中，单击&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择&#x200B;**[!UICONTROL 文件夹]**。

   ![创建文件夹](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL Name]**&#x200B;字段中，以`<language-code>`格式键入国家/地区代码。

   ![在文件夹中添加语言代码](assets/Add-language-code-in-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。语言根在[!DNL Assets]控制台中创建。

## 查看语言根 {#viewing-language-roots}

[!DNL Experience Manager]界面提供了一个&#x200B;**[!UICONTROL 引用]**&#x200B;面板，该面板显示已在[!DNL Assets]内创建的语言根的列表。

1. 在[!DNL Assets]控制台中，选择要为其创建语言副本的主要语言。
1. 从左边栏中，选择&#x200B;**[!UICONTROL 引用]**&#x200B;选项以打开[!UICONTROL 引用]窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在“引用”窗格中，单击&#x200B;**[!UICONTROL 语言副本]**。 [!UICONTROL 语言副本]面板显示资产的语言副本。

   ![语言副本](assets/lang-copy2.png)
