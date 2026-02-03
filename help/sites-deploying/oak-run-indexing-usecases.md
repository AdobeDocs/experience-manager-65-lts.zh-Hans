---
title: Oak-run.jar 索引用例
description: 了解使用Oak运行的工具执行索引的各种用户案例。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: a7a8a20a-e513-43df-80b7-1e6daf957f20
source-git-commit: c714e51f0c0368988ce552969747ab5fce5c186f
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---

# Oak-run.jar 索引用例{#oak-run-jar-indexing-use-cases}

Oak-run支持在命令行上索引用例，而无需通过AEM的JMX控制台来协调这些用例的执行。

使用`oak-run.jar`索引命令方法管理Oak索引的总体优势如下：

* Oak-run index command提供了自AEM 6.4发布以来的新索引工具集。
* Oak-run缩短了重新索引时间，从而减少了大型存储库重新索引的时间。
* Oak-run可减少在AEM中重新索引时的资源消耗，从而提高整体系统性能。
* Oak-run提供带外重新索引功能，支持以下情况：生产必须可用，不能容忍维护或重新索引所需的停机时间。

以下各节提供了示例命令。 Oak-run index命令支持所有NodeStore和BlobStore设置。 以下提供的示例适用于具有FileDataStore和SegmentNodeStore的设置。

## 用例1 — 索引一致性检查 {#usercase1indexconsistencycheck}

此用例与索引损坏相关。 有时无法确定哪些索引已损坏。 因此，Adobe提供了以下工具：

* 对所有索引执行索引一致性检查，并提供关于哪些索引有效哪些索引无效的报告。
* 即使AEM不可访问，该工具也可以使用；
* 它易于使用。

使用`--index-consistency-check`检查损坏的索引：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

此操作在`indexing-result/index-consistency-check-report.txt`中生成报告。 有关示例报表，请参阅下文：

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### 好处 {#uc1benefits}

支持人员和系统管理员可以使用此工具快速识别损坏的索引并重新编制索引。

## 用例2 — 索引统计数据 {#usecase2indexstatistics}

为了诊断一些与查询性能有关的案例，Adobe通常需要客户设置提供的现有索引定义、索引相关统计信息。 为了更便于故障排除，Adobe创建了具有以下功能的工具：

1. 将系统上存在的所有索引定义转储到一个JSON文件中；

1. 从现有索引中转储重要统计信息；

1. 转储索引内容以供离线分析；

1. 即使AEM不可访问，它也可用

可以使用以下索引命令执行上述操作：

* `--index-info` — 收集并转储与索引相关的各种统计信息

* `--index-definitions` — 收集并转储索引定义

* `--index-dump` — 转储索引内容

请参见下面的命令在实践中的工作方式示例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

将在`indexing-result/index-info.txt`和`indexing-result/index-definitions.json`中生成报告

此外，通过Web控制台提供相同的详细信息，这些详细信息将包含在配置转储zip中。 可在以下位置访问它们：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 好处 {#uc2benefits}

此工具能够快速收集与索引或查询问题相关的所有所需详细信息，并减少提取此信息所花费的时间。

## 用例3 — 重新索引 {#usecase3reindexing}

根据[方案](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，有时必须执行重新索引。 目前，通过使用CRXDE或索引管理器用户界面在索引定义节点中将`reindex`标志设置为`true`来重新索引。 设置标记后，重新索引将异步运行。 设置标记后，将异步完成重新索引。

关于重新索引需要注意以下几点：

* 与`DocumentNodeStore`设置（所有内容都是本地的）相比，`SegmentNodeStore`设置中的重新索引要慢得多；

* 使用当前设计，当发生重新索引时，异步索引器会被阻止，并且所有其他异步索引会陈旧并在索引期间不会更新。 因此，如果系统正在使用中，用户可能无法看到最新结果；
* 重新索引涉及遍历整个存储库，这会给AEM设置带来高负载，从而影响最终用户体验；
* 对于重新索引可能需要相当长时间的`DocumentNodeStore`安装，操作期间的Mongo数据库连接失败可能会中断索引。 在这种情况下，必须从头开始重新编制索引。


* 有时，由于文本提取的原因，重新索引可能需要很长时间。 当特定于具有大量PDF文件的设置时，可能会发生此类问题，因为在这些设置中，花费在文本提取上的时间可能会影响索引时间。

为了实现这些目标，Oak运行的索引工具支持根据需要使用的重新索引各种模式。 Oak-run index命令具有以下优点：

* **带外重新索引** - Oak运行的重新索引可以与正在运行的AEM设置分开完成，因此它最大限度地降低了对正在使用的AEM实例的影响；

* **非同道重新索引** — 重新索引在不影响索引操作的情况下进行。 异步索引器可以继续索引其他索引；

* **DocumentNodeStore安装的简化重新索引** — 对于`DocumentNodeStore`安装，可以使用单个命令完成重新索引，以确保以最佳方式完成重新索引；

* **支持更新索引定义和引入新索引定义**

### 重新索引 — DocumentNodeStore {#reindexdocumentnodestore}

对于`DocumentNodeStore`安装，您可以使用单个Oak-run命令执行重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

此操作具有以下优点：

* 对运行AEM实例的影响降至最低。 大多数读取可以从辅助服务器完成，并且运行AEM缓存不会因重新索引所需的所有遍历而受到不利影响；
* 用户还可以通过`--index-definitions-file`选项提供新索引或更新索引的JSON。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

对于`SegmentNodeStore`安装，可通过以下方式之一重新编制索引：

#### 联机重新索引 — SegmentNodeStore {#onlinereindexsegmentnodestore}

按照既定方式，通过设置`reindex`标志来完成重新索引。

#### 联机重新索引 — SegmentNodeStore - AEM实例正在运行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

对于`SegmentNodeStore`安装，只有一个进程能够以读写模式访问区段文件。 因此，Oak运行索引中的一些操作需要执行涉及以下内容的其他手动步骤：

1. 步骤文本。
1. 将`oak-run`连接到AEM以只读模式使用的同一存储库。
1. 使用以下内容作为示例执行索引：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最后，通过`IndexerMBean#importIndex`操作，从运行上述命令后Oak-run保存索引文件的路径导入创建的索引文件。

在此方案中，您不必停止AEM服务器或配置任何新实例。 但是，由于索引涉及遍历整个存储库，这会增加安装上的I/O负载，从而对运行时性能产生负面影响。

#### 联机重新索引 — SegmentNodeStore - AEM实例已关闭 {#onlinereindexsegmentnodestoreaeminstanceisdown}

对于`SegmentNodeStore`安装，您可以使用单个Oak-run命令执行重新索引。 但是，必须关闭AEM实例。

您可以使用以下命令触发重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

这种方法与上面解释的方法的不同之处在于，检查点创建和索引导入会自动完成。 不利的一面是，AEM在此过程中必须停机。

#### 带外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用案例中，您可以对克隆的设置执行重新索引，以将对正在运行的AEM实例的影响降至最低：

1. 通过JMX操作创建检查点。 转到[JMX控制台](/help/sites-administering/jmx-console.md)并搜索`CheckpointManager`。 然后，使用以秒为单位的高过期值(例如，**2592000**)单击&#x200B;**createCheckpoint(long p1)**&#x200B;操作。
1. 将`crx-quickstart`文件夹复制到新计算机。
1. 通过Oak-run index命令执行重新索引。

1. 将生成的索引文件复制到AEM服务器。

1. 通过JMX导入索引文件。

在此使用案例中，数据存储必须可从另一个实例访问，当`FileDataStore`驻留在基于云的存储解决方案（如EBS）上时，可能不可能执行此操作。 此情况不包括同时克隆`FileDataStore`的方案。 如果索引定义不执行全文索引，则不需要访问`DataStore`。

## 用例4 — 更新索引定义 {#usecase4updatingindexdefinitions}

目前，您可以通过[ACS确保索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)包来发送索引定义更改。 您可以在内容包中发送索引定义，然后通过将`reindex`标志设置为`true`来执行重新索引。


对于重新索引不需要很长的时间的较小安装，此方法非常有效。 但是，对于大型存储库，重新索引需要花费大量时间。 对于这种情况，您现在可以使用Oak运行的索引工具。

Oak-run现在支持以JSON格式提供索引定义，并支持在带外模式下创建索引，在这种模式下，不会对实时实例执行任何更改。

对于此用例，需要考虑的流程如下：

1. 开发人员将更新本地实例上的索引定义，然后通过`--index-definitions`选项生成索引定义JSON文件。
1. 更新后的JSON随后将提供给系统管理员。
1. 系统管理员遵循带外方法，在不同的安装上准备索引。
1. 完成后，生成的索引文件将在运行的AEM安装中导入。
