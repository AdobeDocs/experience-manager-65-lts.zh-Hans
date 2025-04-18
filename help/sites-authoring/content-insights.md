---
title: 内容分析
description: 内容分析提供了有关使用网站分析和SEO推荐的页面性能的信息
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 10bf533d-c0a8-43ac-8dd5-d4fa501b8726
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# 内容分析{#content-insight}

内容分析提供了有关使用Web分析和SEO推荐的页面性能的信息。 使用内容分析可做出有关如何修改页面的决策，或了解以前的更改如何更改性能。 对于您创作的每个页面，都可以打开“内容分析”来分析该页面。

![chlimage_1-311](assets/chlimage_1-311.png)

“内容分析”页面的布局会随着您使用的设备的屏幕维度和方向而发生更改。

## 报表数据

“内容分析”页面包含使用Adobe SiteCatalyst、Adobe Target、Adobe Social和BrightEdge数据的报表：

* SiteCatalyst：提供了以下量度的报表：

   * 页面查看次数
   * 页面平均逗留时间
   * 源

* Target：报告页面包含选件的促销活动。
* BrightEdge：报告提高搜索引擎查看页面可见性的页面功能，并推荐应实施的功能。

请参阅[打开页面的Analytics和建议](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page)。

## 报告时段

报表会显示您所控制的一段时间的数据。 在调整报告时段时，报表将自动刷新该时段的数据。 视觉提示指示页面版本发生更改的时间，以便您能够比较每个版本的性能。

>[!NOTE]
>
>内容分析仪表板的时间表在`GMT`之内。

您还可以指定报告数据的粒度，例如，您可以查看每日、每周、每月或每年数据。

请参阅[更改报告周期](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period)。

>[!NOTE]
>
>内容分析报表要求您的管理员将AEM与SiteCatalyst、Target和BrightEdge集成。 查看[与SightCatalyst集成](/help/sites-administering/adobeanalytics.md)、[与Adobe Target集成](/help/sites-administering/target.md)以及[与BrightEdge集成](/help/sites-administering/brightedge.md)。

## “查看次数”报表 {#the-views-report}

“查看次数”报表包括以下用于评估页面流量的功能：

* 报告期间页面查看的总数。
* 报告期内查看次数的图表：

   * 查看次数总计。
   * 独特访客。

![chlimage_1-312](assets/chlimage_1-312.png)

## 页面平均参与次数报表 {#the-page-average-engaged-report}

“页面平均参与次数”报表包括以下用于评估页面效用的功能：

* 页面在整个报告期内保持打开状态的平均时间。
* 报表时段内页面查看的平均长度图表。

![chlimage_1-313](assets/chlimage_1-313.png)

## “源”报表 {#the-sources-report}

“源”报表指示用户如何导航到页面，例如从搜索引擎结果或使用已知URL。

![chlimage_1-314](assets/chlimage_1-314.png)

## 退回报告 {#the-bounces-report}

“跳出次数”报表包括一个图表，该图表显示在选定报告期间某个页面发生的跳出次数。

![chlimage_1-315](assets/chlimage_1-315.png)

## 促销活动报表 {#the-campaign-activity-report}

对于页面处于活动状态的每个营销活动，都会显示一个名为&#x200B;*营销活动名称*&#x200B;活动的报表。 此报表显示提供了选件的每个区段的页面展示次数和转化次数。

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO推荐报表 {#the-seo-recommendations-report}

SEO推荐报表包含针对页面的BrightEdge分析的结果。 该报告是页面功能的核对清单，指示页面包含和不包含哪些功能，以便使用搜索引擎最大程度地提高查找能力。

通过报告可创建任务，以便做出改进来改善页面可查找性。 “建议”表示已创建用于实施建议的任务。 请参阅[为SEO推荐分配任务](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations)。

![chlimage_1-317](assets/chlimage_1-317.png)
