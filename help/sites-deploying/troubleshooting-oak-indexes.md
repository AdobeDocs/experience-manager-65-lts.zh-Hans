---
title: Oak索引疑难解答
description: 了解如何识别索引速度是否较慢，找到原因并解决问题。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 6f92750a-4eaa-43cf-8f67-b1a65b1c6930
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Oak索引疑难解答{#troubleshooting-oak-indexes}

## 重新索引缓慢  {#slow-re-indexing}

AEM的内部重新索引过程会收集存储库数据并将其存储在Oak索引中，以支持对内容的高性能查询。 在特殊情况下，这一过程可能会变得缓慢甚至停滞。 本页作为疑难解答指南，可帮助确定索引速度是否较慢，找到原因并解决问题。

区分需要花费不恰当的大量时间的重新索引与需要很长时间重新索引很重要，因为重新索引需要大量内容。 例如，为内容编制索引所需的时间会随着内容量的增加而扩展，因此大型生产存储库重新编制索引的时间比小型开发存储库长。

有关何时以及如何重新索引内容的更多信息，请参阅[关于查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 初始检测 {#initial-detection}

初始检测索引缓慢需要查看`IndexStats` JMX MBean。 在受影响的AEM实例上，执行以下操作：

1. 打开Web控制台，然后单击JMX选项卡或转到https://&lt;host>：&lt;port>/system/console/jmx (例如，[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 导航到`IndexStats` Mbean。
1. 打开“`async`”和“`fulltext-async`”的`IndexStats` MBean。

1. 对于两个MBean，检查&#x200B;**Done**&#x200B;时间戳和&#x200B;**LastIndexTime**&#x200B;时间戳是否比当前时间少于45分钟。

1. 对于任一MBean，如果时间值（**Done**&#x200B;或&#x200B;**LastIndexedTime**）与当前时间相差45分钟以上，则索引作业失败或用时过长。 此问题会导致异步索引过时。

## 在强制关闭后暂停索引 {#indexing-is-paused-after-a-forced-shutdown}

强制关闭导致AEM在重新启动后暂停异步索引长达30分钟。 此外，它通常需要15分钟才能完成第一个重新索引阶段，总共大约需要45分钟（回溯到[初始检测](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection)的时间范围，即45分钟）。 如果索引在强制关闭后暂停：

1. 首先，确定AEM实例是否以强制方式关闭(AEM进程被强制终止，或发生电源故障)，然后重新启动。

   * [AEM日志记录](/help/sites-deploying/configure-logging.md)可以为此目的进行审核。

1. 如果发生强制关闭，则在重新启动时，AEM会自动暂停重新索引长达30分钟。
1. 请等待大约45分钟，以便AEM恢复正常的异步索引操作。

## 线程池过载 {#thread-pool-overloaded}

在特殊情况下，用于管理异步索引的线程池可能会变得过载。 为了隔离索引过程，可以配置线程池以防止其他AEM工作干扰Oak及时索引内容的能力。 在这种情况下，请执行以下操作：

1. 为Apache Sling调度程序定义新的独立线程池以用于异步索引：

   * 在受影响的AEM实例上，导航到AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler，或转到https://&lt;host>：&lt;port>/system/console/configMgr (例如，[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 向“允许的线程池”字段中添加一个值为“oak”的条目。
   * 要保存更改，请单击右下角的&#x200B;**保存**。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 验证新的Apache Sling计划程序线程池是否已注册，并显示在Apache Sling计划程序状态Web控制台中。

   * 导航到AEM OSGi Web Console>Status>Sling Scheduler，或转到https://&lt;host>：&lt;port>/system/console/status-slingscheduler(例如，[http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 验证以下池条目是否存在：

      * ApacheSlingoak
      * apacheslingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 观察队列已满 {#observation-queue-is-full}

如果在短时间内对存储库进行了太多更改和提交，则索引可能会由于观察队列已满而延迟。 首先，确定观察队列是否已满：

1. 转到Web控制台，然后单击JMX选项卡，或转到https://&lt;host>：&lt;port>/system/console/jmx (例如，[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 打开Oak存储库统计数据MBean并确定是否有任何`ObservationQueueMaxLength`值大于10,000。

   * 在正常操作中，此最大值最终必须始终减少到零（尤其是在`per second`部分中），因此请验证`ObservationQueueMaxLength`的秒量度是否为0。
   * 如果值为10,000或更多，并且稳步增加，则表示至少一个（可能更多）队列的处理速度不能像新更改（提交）发生一样快。
   * 每个观察队列都有一个限制（默认为10,000），如果队列点击了该限制，则其处理会降级。
   * 使用MongoMK时，随着队列长度增大，内部Oak缓存性能会降低。 可以在`Consolidated Cache`统计数据MBean中`DocChildren`缓存的增加`missRate`中看到此关联。

1. 为避免超出可接受的观察队列限制，建议：

   * 降低提交固定速率。 承诺量出现短峰值是可以接受的，但应降低恒定速率。
   * 按照[性能优化提示> Mongo存储优化>文档缓存大小](/help/sites-deploying/configuring-performance.md)中的说明增加`DiffCache`的大小。

## 识别和修复停滞的重新索引过程 {#identifying-and-remediating-a-stuck-re-indexing-process}

在以下两种情况下，可认为重新索引被“完全卡住”：

* 重新索引很慢，以至于日志文件未报告关于遍历的节点数的显着进展。

   * 例如，如果一小时内没有消息，或者进度太慢以至于需要一周或更长时间才能完成。

* 如果索引线程的日志文件（例如，`OutOfMemoryException`）中出现重复的异常，则重新索引会陷入无限循环。 日志中重复出现一个或多个相同的异常，表示Oak尝试重复索引相同的内容，但在同一问题上失败。

要识别和修复停滞的重新索引过程，请执行以下操作：

1. 要确定索引卡住的原因，必须收集以下信息：

   * 收集5分钟的线程转储，每2秒转储一次线程转储。
   * [设置附加器的DEBUG级别和日志](/help/sites-deploying/configure-logging.md)。

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * 从异步`IndexStats` MBean收集数据：

      * 导航至AEM OSGi Web Console>Main>JMX>IndexStat>async

        或转到[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * 使用[oak-run.jar的控制台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)收集* `/:async`*节点下存在的详细信息。
   * 使用`CheckpointManager` MBean收集存储库检查点的列表：

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

        或转到[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. 收集了步骤1中概述的所有信息后，请重新启动AEM。

   * 如果存在高并发负载（观察队列溢出或类似情况），重新启动AEM可能会解决问题。
   * 如果重启不能解决问题，请打开[Adobe客户关怀](https://experienceleague.adobe.com/zh-hans?support-solution=General&amp;support-tab=home#support)的问题，并提供在步骤1中收集的所有信息。

## 安全中止异步重新索引 {#safely-aborting-asynchronous-re-indexing}

可以通过`async, async-reindex`和`ulltext-async`索引通道(`IndexStats` Mbean)安全地中止重新索引（在完成之前停止）。 有关详细信息，另请参阅有关[如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex)的Apache Oak文档。 此外，请考虑以下事项：

* Lucene和Lucene属性索引的重新索引可以中止，因为它们是自然异步的。
* 只有通过`PropertyIndexAsyncReindexMBean`启动重新索引，才能中止Oak属性索引的重新索引。

要安全地中止重新索引，请执行以下步骤：

1. 确定控制必须停止的重新索引通道的IndexStats MBean。

   * 通过JMX控制台导航到相应的IndexStats MBean，方法是转到AEM OSGi Web Console>Main>JMX或https://&lt;host>：&lt;port>/system/console/jmx (例如，[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根据要停止的重新索引通道（`async`、`async-reindex`或`fulltext-async`）打开IndexStats MBean

      * 要确定适当的通道，从而确定IndexStats MBean实例，请查看Oak索引“异步”属性。 “async”属性包含通道名称： `async`、`async-reindex`或`fulltext-async`。
      * 此外，还可以通过访问“异步”列中的AEM索引管理器来使用此通道。 要访问索引管理器，请导航到“操作”>“诊断”>“索引管理器”。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在适当的`IndexStats` MBean上调用`abortAndPause()`命令。
1. 适当地标记Oak索引定义，以防止在索引领域恢复时恢复重新索引。

   * 重新索引&#x200B;**existing**&#x200B;索引时，将重新索引属性设置为false

      * `/oak:index/someExistingIndex@reindex=false`

   * 否则，对于&#x200B;**新**&#x200B;索引：

      * 将type属性设置为禁用

         * `/oak:index/someNewIndex@type=disabled`

      * 或完全删除索引定义

   完成后，将更改提交到存储库。

1. 最后，恢复在中止索引车道上的异步索引。

   * 在步骤2中发出`abortAndPause()`命令的`IndexStats` MBean中，调用`resume()`命令。

## 防止重新索引缓慢 {#preventing-slow-re-indexing}

最好在静默期（例如，在大型内容摄取期间不重新索引）以及理想情况下在已知并控制AEM负载的维护时段重新索引。 此外，请确保在其他维护活动中不会重新编制索引。
