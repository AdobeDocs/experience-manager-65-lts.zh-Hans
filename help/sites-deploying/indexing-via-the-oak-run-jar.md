---
title: 通过Oak-run Jar编制索引
description: 了解如何通过Oak-run Jar执行索引。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: a6344463-7796-4ee3-8b2e-b3bfd2aec99a
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 通过Oak-run Jar编制索引 {#indexing-via-the-oak-run-jar}

Oak-run支持命令行上的所有索引用例，而无需从JMX级别操作。 oak-run方法的优点包括：

1. 这是自AEM 6.4以来新的索引工具集
1. 它缩短了重新索引时间，这有利地影响了大型存储库的重新索引时间
1. 它减少了在AEM中重新索引时的资源消耗，从而为其他AEM活动带来更好的系统性能
1. Oak-run提供带外支持：如果生产条件不允许您在生产实例上运行重新索引，则可以使用克隆的环境重新索引以避免关键的性能影响。

以下是通过`oak-run`工具执行索引操作时可以使用的用例列表。

## 索引一致性检查 {#indexconsistencychecks}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[用例1 — 索引一致性检查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)。

* `oak-run.jar`快速确定Lucene Oak索引是否损坏。
* 可以在正在使用的AEM实例上安全运行以进行一致性检查级别1和2。

![索引一致性检查](assets/screen_shot_2017-12-14at135758.png)

## 索引统计信息 {#indexstatistics}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[用例2 — 索引统计数据](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar`转储所有索引定义、重要索引统计信息以及索引内容以进行离线分析。
* 可在正在使用的AEM实例上安全执行。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 重新索引方法决策树 {#reindexingapproachdecisiontree}

此图表是何时使用各种重新索引方法的决策树。

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[用例3 — 重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)。

### SegmentNodeStore和DocumentNodeStore的文本预提取 {#textpre-extraction}

[文本预提取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction)(自AEM 6.3以来一直存在的功能)可用于减少重新索引的时间。 文本预提取可用于所有重新索引方法。

根据`oak-run.jar`索引方法，下图中的“执行重新索引”步骤的每一侧都有各种步骤。

SegmentNodeStore和DocumentNodeStore的![文本预提取](assets/4.png)

>[!NOTE]
>
>橙色表示AEM必须在维护时段中进行的活动。

### 使用oak-run.jar为MongoMK或RDBMK在线重新索引 {#onlinere-indexingformongomk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[重新索引 — DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore)。

这是重新索引MongoMK（和RDBMK） AEM安装的推荐方法。 不应使用其他方法。

请仅针对群集中的单个AEM实例运行此流程。

![使用oak-run.jar为MongoMK或RDBMK联机重新编制索引](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore)。

* **冷待机注意事项(TarMK)**

   * 冷备用没有特殊注意事项；冷备用实例同步会照常更改。

* **AEM发布场（AE发布场应始终为TarMK）**

   * 对于发布场，必须为全部完成或在单个发布上执行步骤。 然后，克隆其他人的设置(在克隆AEM实例时执行所有常规弃用；sling.id — 应链接到此处某些内容)。

### TarMK的在线重新索引 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[联机重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore)。

这是在引入oak-run.jar的新索引功能之前使用的方法。 此操作可通过在Oak索引中设置`reindex=true`属性来完成。

如果客户可以接受索引的时间和性能影响，则可以使用此方法。 对于中小型AEM安装而言，情况通常如此。

![为TarMK联机重新编制索引](assets/6.png)

### 使用oak-run.jar在线重新索引TarMK {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[联机重新索引 — SegmentNodeStore - AEM实例正在运行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)。

使用oak-run.jar对TarMK进行联机重新索引比上述[对TarMK进行联机重新索引](#onlinere-indexingfortarmk)更快。 但是，它还需要在维护时段内执行；提及时段较短，并且需要更多步骤来执行重新索引。

>[!NOTE]
>
>橙色表示在维护期间必须执行AEM的操作。

![使用oak-run.jar联机重新索引TarMK](assets/7.png)

### 使用oak-run.jar离线重新索引TarMK {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[联机重新索引 — SegmentNodeStore - AEM实例已关闭](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown)。

TarMK的离线重新索引是TarMK最简单的基于`oak-run.jar`的重新索引方法，因为它需要单个`oak-run.jar`注释。 但是，它需要关闭AEM实例。

>[!NOTE]
>
>红色表示必须关闭AEM的操作。

![使用oak-run.jar脱机重新索引TarMK](assets/8.png)

### 使用oak-run.jar进行带外重新索引TarMK  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[带外重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore)。

带外重新索引将重新索引对正在使用的AEM实例的影响降至最低。

>[!NOTE]
>
>红色表示可能关闭AEM的操作。

![使用oak-run.jar对TarMK进行带外重新索引](assets/9.png)

## 更新索引定义 {#updatingindexingdefinitions}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅[用例4 — 更新索引定义](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)。

### 使用ACS在TarMK上创建和更新索引定义确保索引 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS确保索引是社区支持的项目，并且不受Adobe支持。

这允许通过内容包来传送索引定义，这稍后通过将重新索引标志设置为`true`导致重新索引。 这适用于重新索引不需要很长的时间的较小设置。

有关详细信息，请参阅[ACS确保索引文档](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)。

### 使用oak-run.jar在TarMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

如果使用非`oak-run.jar`方法重新索引的时间或性能影响太大，则可在基于TarMK的AEM安装中使用以下基于`oak-run.jar`的方法导入和重新索引Lucene索引定义。

![使用oak-run.jar在TarMK上创建和更新索引定义](assets/10.png)

### 使用oak-run.jar在MonogMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

如果使用非`oak-run.jar`方法重新索引的时间或性能影响太大，则可在基于MongoMK的AEM安装中使用以下基于`oak-run.jar`的方法导入和重新索引Lucene索引定义。

![使用oak-run.jar在MonogMK上创建和更新索引定义](assets/11.png)
