---
title: 增强型智能标记
description: 增强型智能标记
contentOwner: AG
feature: Smart Tags, Search
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 7a0d5502-8e1a-4396-a517-ea3767e228c2
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# 了解、应用和策划智能标记 {#enhanced-smart-tags}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包括员工、合作伙伴和客户通常用于引用和搜索特定类的数字资产的关键字列表。 使用分类控制的词汇标记资产可确保轻松识别和检索资产。

与自然语言词汇相比，根据业务分类标记数字资产有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以使用模型名称标记汽车图像，这样在搜索各种模型的图像以设计促销活动时，只显示相关图像。

要让智能内容服务应用正确的标记，请对其进行培训以识别您的分类。 要培训服务，首先要策划一组最能描述这些资源的资源和标记。 为帮助服务学习，请在资产上应用这些标记并运行培训工作流。

培训标记并准备就绪后，该服务现在可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei AI框架根据您的标记结构和业务分类培训其图像识别算法。 然后，此内容智能可用于将相关标记应用到其他资产集。

智能内容服务是托管在[!DNL Adobe Developer Console]上的云服务。 若要在[!DNL Adobe Experience Manager]中使用它，系统管理员必须将您的[!DNL Experience Manager]部署与[!DNL Adobe Developer Console]集成。

总之，以下是使用“智能内容服务”的主要步骤：

* 入门培训
* 审查资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 先决条件和支持的格式 {#prerequisites}

在使用智能内容服务之前，请确保满足以下条件，以便在[!DNL Adobe Developer Console]上创建集成：

* 具有组织管理员权限的Adobe ID帐户。
* 为您的组织启用智能内容服务服务。
* 要将Smart Content Services基本包添加到部署，请许可[!DNL Adobe Experience Manager Sites]基本包和[!DNL Assets]加载项。

该服务将智能标记应用于以下MIME类型的资产：

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

该服务将智能标记应用于以下MIME类型的资产演绎版：

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 入门培训 {#onboarding}

智能内容服务可作为[!DNL Experience Manager]的加载项购买。 购买后，会向组织的管理员发送一封电子邮件，其中包含指向[!DNL Adobe I/O]的链接。

管理员可以按照该链接将智能内容服务与[!DNL Experience Manager]集成。 要将服务与[!DNL Experience Manager Assets]集成，请参阅[配置智能标记](config-smart-tagging.md)。

管理员配置服务并在[!DNL Experience Manager]中添加用户后，载入过程即完成。

## 查看资源和标记 {#reviewing-assets-and-tags}

在您上线后，您首先要做的是确定一组最能描述您的业务背景中这些图像的标记。

接下来，查看图像以确定一组最能代表您的产品以满足特定业务需求的图像。 确保策划集中的资产符合[智能内容服务培训准则](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。

将资源添加到文件夹，并从属性页面将标记应用于每个资源。 然后，在此文件夹中运行培训工作流。 策划的资源集允许智能内容服务使用您的分类定义有效地培训更多资源。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在对智能内容服务进行标记培训之前，仔细查看策划的资源集中的标记。
>1. 在培训标记之前，请参阅[智能内容服务培训准则](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. 首次培训智能内容服务时，Adobe建议您至少在两个不同的标记上对其进行培训。

## 了解带有智能标记的[!DNL Experience Manager]搜索结果 {#understandsearch}

默认情况下，[!DNL Experience Manager]搜索将搜索词与`AND`子句组合在一起。 使用智能标记不会更改此默认行为。 使用智能标记可添加额外的`OR`子句以查找与智能标记相关的任何搜索词。 例如，考虑搜索`woman running`。 默认情况下，元数据中仅包含`woman`或仅包含`running`关键字的Assets不会出现在搜索结果中。 但是，使用智能标记标记为`woman`或`running`的资源会出现在此类搜索查询中。 所以搜索结果是，

* 元数据中包含`woman`和`running`关键字的Assets。

* 使用任一关键词标记的Assets智能标记。

首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 在上述示例中，搜索结果的大致显示顺序为：

1. 各种元数据字段中的`woman running`的匹配项。
1. 智能标记中的`woman running`的匹配项。
1. 在智能标记中匹配`woman`或`running`。

>[!CAUTION]
>
>如果Lucene索引在[!DNL Adobe Experience Manager]内完成，则基于智能标记的搜索无法按预期工作。

## 自动标记资产 {#tagging-assets-automatically}

培训智能内容服务后，您可以触发标记工作流，以自动将相应标记应用于一组不同的类似资产。

您可以定期或根据需要运行标记工作流。

>[!NOTE]
>
>标记工作流会在资源和文件夹上运行。

### 定期标记 {#periodic-tagging}

您可以启用智能内容服务以定期为文件夹中的资产添加标签。 打开资产文件夹的属性页面，在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡下选择&#x200B;**[!UICONTROL 启用智能标记]**，然后保存更改。

为文件夹选择此选项后，智能内容服务将自动标记文件夹中的资产。 默认情况下，标记工作流每天凌晨12:00运行。

### 按需标记 {#on-demand-tagging}

您可以从工作流控制台或时间轴触发标记工作流，以立即标记您的资产。

>[!NOTE]
>
>如果从时间线运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台中标记资产 {#tagging-assets-from-the-workflow-console}

1. 在[!DNL Experience Manager]界面中，转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL DAM智能标记Assets]**&#x200B;工作流，然后单击工具栏中的&#x200B;**[!UICONTROL 启动工作流]**。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在&#x200B;**[!UICONTROL 运行工作流]**&#x200B;对话框中，浏览到包含要自动应用标记的资源的有效负荷文件夹。
1. 指定工作流的标题和可选评论。 单击&#x200B;**[!UICONTROL 运行]**。

   ![标记对话框](assets/tagging_dialog.png)

   要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

#### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从[!DNL Assets]用户界面中，选择包含要应用智能标记的资源或特定资源的文件夹。
1. 从左上角，打开&#x200B;**[!UICONTROL 时间轴]**。
1. 从左侧边栏底部打开操作，然后单击&#x200B;**[!UICONTROL 启动工作流]**。

   ![start_workflow](assets/start_workflow.png)

1. 选择&#x200B;**[!UICONTROL DAM智能标记Assets]**&#x200B;工作流，并指定该工作流的标题。
1. 单击&#x200B;**[!UICONTROL 开始]**。 该工作流会在资产中应用标记。 要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

>[!NOTE]
>
>在后续的标记周期中，只有修改后的资产会再次使用新训练的标记进行标记。 但是，如果标记工作流的最后一个标记周期与当前标记周期之间的间隔超过24小时，则即使未更改的资产也会进行标记。 对于定期标记工作流，当时间间隔超过六个月时，将标记未更改的资产。

## 组织或审核应用的智能标记 {#manage-smart-tags}

您可以策划智能标记，以删除分配给品牌图像的任何不准确的标记，从而仅显示最相关的标记。

审核智能标记还可确保您的图像显示在最相关标记的搜索结果中，从而帮助优化基于标记的图像搜索。 基本上，它有助于消除无关图像出现在搜索结果中的机会。

您还可以为标记分配更高的排名，以提高其与图像的相关性。 当搜索特定标记时，提升图像的标记会增加搜索结果中出现该图像的机会。

1. 在搜索框中，使用标记作为关键词来搜索资产。
1. 要识别与搜索不相关的图像，请查看搜索结果。
1. 选择图像，然后单击工具栏中的&#x200B;**[!UICONTROL 管理标记]**。
1. 从&#x200B;**[!UICONTROL 管理标记]**&#x200B;页面，查看标记。 如果不希望根据特定标记搜索图像，请选择该标记，然后单击工具栏中的&#x200B;**[!UICONTROL 删除]**。 或者，单击标签旁边显示的`x`符号。
1. 或者，若要为标记分配更高的排名，请选择该标记，然后单击工具栏中的&#x200B;**[!UICONTROL 提升]**。 您提升的标记将移至&#x200B;**[!UICONTROL 标记]**&#x200B;部分。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 确定]**
1. 导航到图像的&#x200B;**[!UICONTROL 属性]**&#x200B;页面。 请注意，您提升的标记被分配了更多的相关性，并且出现在搜索结果中的较早位置。

## 提示和限制 {#tips-best-practices-limitations}

* 要训练模型，请使用最合适的图像。 无法恢复训练或无法删除训练模型。 您的标记准确性取决于当前的训练，因此请仔细操作。
* 智能内容服务的使用限制为每年最多200万个标记图像。 任何经过处理和标记的重复图像均计为已标记的图像。
* 如果从时间线运行标记工作流，则一次最多可以对15个资产应用标记。
* 智能标记仅适用于PNG和JPG图像格式。 因此，如果支持的资源具有以这两种格式创建的演绎版，则会使用智能标记进行标记。

>[!MORELIKETHIS]
>
>* [概述以及如何培训智能标记](enhanced-smart-tags.md)
>* [配置智能标记](config-smart-tagging.md)
>* [OAuth凭据的智能标记疑难解答](config-oauth.md)
>* [有关智能标记的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=zh-Hans)
