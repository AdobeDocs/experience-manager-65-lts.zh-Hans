---
title: 了解分段
description: 分段是创建营销活动时的主要考虑事项。通常，在开始营销活动之前必须已定义区段。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: f3755499-472b-4eb9-bc98-7918b77f7ab0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 49%

---

# 了解分段{#understanding-segmentation}

分段是创建营销活动时的主要考虑事项。通常，在开始营销活动之前必须已定义区段。

网站访客在访问网站时具有不同的兴趣和目标。 了解这些目标并满足期望是在线营销成功的重要因素。

分段可通过分析和描述访客的：

* 在网站上的活动
* 侧面像
* 在其他网站上的活动

然后，可以根据访客的需要和兴趣定位内容，具体取决于他们匹配的区段。

## 使用分段 {#using-segmentation}

区段是在[配置分段](/help/sites-administering/campaign-segmentation.md)中定义的。 它们用于控制特定目标受众看到的实际内容。

## 分段术语 {#segmentation-terminology}

在讨论分段时，会用到以下术语：

**访客** – 访客是访问网站的人。该人员的访问通常从反向链接页面开始，然后转到您自己的网站上的一个或多个页面查看次数。 可以根据该人员访问的详细信息创建行为配置文件。

**用户** – 用户是在网站中注册以接收帐户配置文件的访客。为生成用户档案，他们提供其他身份信息，如电子邮件地址和性别等。 此外，还可以收集其他信息，包括社区活动和购买模式等。 根据个人资料中提供的信息，可以创建人口统计个人资料。

**特征** – 特征是可用于确定特定区段中的成员资格的访客特点或属性。

**区段** – 区段是共享某些特征的访客的集合。区段应该与众不同，与其他区段之间具有尽可能少的重叠。

**行为特征** – 行为特征是与访客在网站上的行为相关的特征。其中包括：

* 在您的网站中的兴趣；包括访问的页面和购买的产品。
* 在引用网站中的兴趣；包括使用的搜索词或点击的广告。
* 在其他站点上的兴趣；使用Spyjax等工具确定。
* 访客忠诚度；访问的持续时间和访问频率。

**人口统计特征** – 这些是选定的人口特征，包括：

* 年龄
* 收入
* 家庭规模
* 婚姻状况
* 性别
* 位置

**派生的特征**

在未注册的情况下，某些人口统计特征很难确定，但可以通过组合行为和人口统计特征来推断。

例如，通过将引用 URL（作为行为特征）与人口统计数据（通过 [Google Ad Planner](https://www.google.com/adplanner/) 之类的工具获取）相结合，站点所有者可以推断出访客的人口统计特征。

**子区段** – 一个区段可以划分为若干个子区段。 这可以通过定义其他特征来完成。

**Teaser 页面** – Teaser 页面面向特定受众。它包含可在Teaser段落中使用的可重用内容。

**营销活动** – 营销活动是 Teaser 页面和电子邮件营销页面（如新闻稿或邀请）的集合。通常，营销活动只运行一段有限的时间，随后会被其他营销活动取代。

**Teaser 段落** – 这是一个从另一个依赖于选择战略的页面中提取内容的段落。此选择战略可以将区段和营销活动考虑在内。

**列表** – 将从已注册用户的区段中提取列表。 例如，用于控制 Teaser 段落内容的位置。

>[!NOTE]
>
>有关Adobe Experience Manager中的区段的详细信息，请参阅[分段](/help/sites-administering/campaign-segmentation.md)。
