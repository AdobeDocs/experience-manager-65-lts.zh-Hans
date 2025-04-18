---
title: 定位您的Adobe Campaign
description: 设置分段后，您可以为Adobe Campaign创建定位体验。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: ce6ebfff-3a1d-4c9f-aa50-23d1c3afc852
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 定位Adobe Campaign{#targeting-your-adobe-campaign}

要定位Adobe Campaign新闻稿，您需要先设置仅在Classic UI（适用于客户端上下文）中提供的分段。 之后，您可以为Adobe Campaign创建定位体验。 本节将介绍这两种方法。

## 在AEM中设置分段 {#setting-up-segmentation-in-aem}

要设置分段，您需要使用经典UI设置区段。 其余步骤可以在标准UI中执行。

设置分段包括创建区段、品牌、营销活动和体验。

>[!NOTE]
>
>区段ID需要映射到Adobe Campaign端的ID。

### 创建区段 {#creating-segments}

要创建区段，请执行以下操作：

1. 在&#x200B;**&lt;host>：&lt;port>/miscadmin#/etc/segmentation**&#x200B;处打开[分段控制台](http://localhost:4502/miscadmin#/etc/segmentation)。
1. 创建页面并输入标题 — 例如&#x200B;**AC区段** — 并选择&#x200B;**区段(Adobe Campaign)**&#x200B;模板。
1. 在左侧的树视图中选择创建的页面。
1. 创建一个区段，例如，以男性用户为目标，方法是在您创建的名为“男性”的区段下创建一个页面，然后选择&#x200B;**区段(Adobe Campaign)**&#x200B;模板。
1. 打开创建的区段页面，并将&#x200B;**区段ID**&#x200B;从Sidekick拖放到页面上。
1. 双击该特征，输入表示在此例中为Adobe Campaign中定义的男性区段的ID，例如&#x200B;**MALE**，然后单击&#x200B;**确定**。 应显示以下消息： *`targetData.segmentCode == "MALE"`*
1. 对另一个区段重复这些步骤，例如，针对女性用户的区段。

### 创建品牌 {#creating-a-brand}

要创建品牌，请执行以下操作：

1. 在&#x200B;**Sites**&#x200B;中，导航到&#x200B;**Campaigns**&#x200B;文件夹（例如，在We.Retail中）。
1. 单击&#x200B;**创建页面**&#x200B;并输入页面的标题，例如We.Retail品牌，然后选择&#x200B;**品牌**&#x200B;模板。

### 创建活动 {#creating-a-campaign}

要创建活动，请执行以下操作：

1. 打开您创建的&#x200B;**品牌**&#x200B;页面。
1. 单击&#x200B;**创建页面**&#x200B;并为您的页面输入标题，例如We.Retail促销活动，选择&#x200B;**促销活动**&#x200B;模板，然后单击&#x200B;**创建**。

### 创建体验 {#creating-experiences}

要为区段创建体验，请执行以下操作：

1. 打开您创建的&#x200B;**Campaign**&#x200B;页面。
1. 通过单击&#x200B;**创建页面**&#x200B;并为页面输入标题（例如，在为“男性”区段创建体验时输入“男性”），为区段创建体验，然后选择&#x200B;**体验**&#x200B;模板。
1. 打开已创建的体验页面。
1. 单击&#x200B;**编辑**，然后在“区段”下方单击&#x200B;**添加项**。
1. 输入男性区段的路径，例如&#x200B;**/etc/segmentation/ac-segments/male**，然后单击&#x200B;**确定**。 应该显示以下消息：*体验面向：男性*
1. 重复上述步骤为所有区段（例如，女性目标）创建体验。

## 创建包含目标内容的新闻稿 {#creating-a-newsletter-with-targeted-content}

创建区段、品牌、营销活动和体验后，您可以创建包含目标内容的新闻稿。 创建体验后，您将体验链接到区段。

>[!NOTE]
>
>[电子邮件示例仅在Geometrixx](/help/sites-developing/we-retail.md)中可用。 从包共享下载示例Geometrixx内容。

要创建包含目标内容的新闻稿，请执行以下操作：

1. 创建包含目标内容的新闻稿：在Geometrixx Outdoors中的电子邮件促销活动下，单击&#x200B;**创建** > **页面**，然后选择一个Adobe Campaign邮件模板。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 在新闻稿中，添加文本和Personalization组件。
1. 将文本添加到文本和Personalization组件中，例如“这是默认设置”。
1. 单击&#x200B;**编辑**&#x200B;旁边的箭头并选择&#x200B;**定位**。
1. 从品牌下拉菜单中选择您的品牌，然后选择您的Campaign。 （这是您之前创建的品牌和营销活动）。
1. 单击&#x200B;**开始定位**。 此时，您的区段将显示在受众区域中。 如果没有定义的区段匹配，则使用默认体验。

   >[!NOTE]
   >
   >默认情况下，AEM中包含的电子邮件示例使用Adobe Campaign作为定位引擎。 对于自定义新闻稿，您可能需要选择Adobe Campaign作为定位引擎。 定位时，单击工具栏中的+ ，输入新活动的标题，然后选择&#x200B;**Adobe Campaign**&#x200B;作为定位引擎。

1. 单击&#x200B;**默认**，然后单击您添加的文本和Personalization组件，您会看到带有箭头的靶心。 单击图标以定位此组件。

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. 导航到其他区段（男性），然后单击&#x200B;**添加选件**&#x200B;并单击加号图标+。 然后编辑选件。
1. 导航到其他区段（女性）并单击&#x200B;**添加选件**&#x200B;和加号图标+。 然后编辑此选件。
1. 单击&#x200B;**下一步**&#x200B;查看映射，单击&#x200B;**下一步**&#x200B;查看不适用于Adobe Campaign的设置，然后单击&#x200B;**保存**。

   当Adobe Campaign内的投放中使用内容时，AEM会自动为Adobe Campaign生成正确的定位代码

1. 在Adobe Campaign中，创建投放 — 选择包含AEM内容的&#x200B;**电子邮件投放**，并根据需要选择本地AEM帐户，然后确认更改。

   在HTML视图中，目标组件的不同体验包含在Adobe Campaign定位代码中。

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >如果您还在Adobe Campaign中设置区段，则单击&#x200B;**预览**&#x200B;将显示每个区段的体验。
