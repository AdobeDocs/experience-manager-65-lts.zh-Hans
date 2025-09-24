---
title: 为AEM脱机重新编制索引
description: 了解如何使用离线重新索引方法为AEM存储库重新索引。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 076db19026a0992725062ec9965ff6c1cb84333e
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# 为AEM脱机重新编制索引 {#offline-reindexing-for-aem}

## 简介 {#introduction}

对于AEM Assets项目，通常具有大型数据存储和高水平资源上传，重新索引Oak索引可能需要大量时间。

本节介绍如何使用Oak-run工具执行离线重新索引。 所介绍的步骤可以应用于AEM 6.4及更高版本的[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)索引。

## 概述 {#overview}

由于索引定义更改、性能优化或内容发生重大更改等多种原因，AEM存储库通常需要重新索引。 由于资源中的文本(例如，PDF文件中的文本)被提取并编制索引，因此重新索引对于资源部署而言代价高昂。 使用MongoMK存储库，数据通过网络保留，从而进一步增加重新索引所花费的时间。 解决方案是使用Oak运行的工具对&#x200B;**脱机**&#x200B;执行重新索引，然后将预建索引导入正在运行的AEM实例中。 此方法可最大限度地缩短重新索引时间，并实现更好的资源管理。

## 方法 {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

其方法是使用[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)工具脱机创建索引，然后将其导入正在运行的AEM实例中。 上图显示了离线重新索引方法。

此外，这是方法中描述的步骤顺序：

1. 首先提取二进制文件中的文本
2. 创建或更新索引定义
3. 已创建脱机索引
4. 然后，索引将导入到正在运行的AEM实例中

### 文本提取 {#text-extraction}

要在AEM中启用完整索引，将提取二进制文件(如PDF)中的文本并将其添加到索引中。 在索引过程中，这通常是代价高昂的步骤。 文本提取是尤其建议用于重新索引资产存储库（因为它们存储大量二进制文件）的优化步骤。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

通过将oak-run工具与tika库结合使用，可以提取存储在系统中的二进制文件中的文本。 可以复制生产系统，并将其用于此文本提取过程。 然后，此过程将执行以下步骤来创建文本存储：

**1. 遍历存储库并收集二进制文件的详细信息**

此步骤会生成一个包含二进制文件元组的CSV文件，其中包含一个路径和一个blob ID。

从要创建索引的目录执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

其中`nodestore path`是`mongo_uri`或`crx-quickstart/repository/segmentstore/`

请使用`--fake-ds-path=temp`参数而不是`–fds-path`来加快进程。

**2. 重用现有索引**&#x200B;中可用的二进制文本存储

从现有系统中转储索引数据并提取文本存储。

可以使用以下命令转储现有的索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

其中`nodestore path`是`mongo_uri`或`crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中`oak-index-name`是全文索引的名称，例如“lucene”。

**3. 使用针对上述步骤**&#x200B;中遗漏的二进制文件的tika库运行文本提取进程

```
java -cp oak-run.jar:tika-app-*.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

>[!NOTE]
>
>使用与AEM中使用的相同版本的Tika。

其中`datastore path`是二进制数据存储的路径。

创建的文本存储可以更新，并重复用于未来的重新索引方案。

有关文本提取过程的更多详细信息，请参阅[Oak运行文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 脱机重新索引 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

脱机创建Lucene索引。 如果使用MongoMK，建议直接在某个MongoMK节点上运行它，因为这可避免网络开销。

要脱机创建索引，请执行以下步骤：

**1. 生成Oak Lucene索引定义**

转储现有的索引定义。 可以使用Adobe Granite存储库包和oak-run生成索引定义。

要从AEM实例转储索引定义，请运行此命令：

>[!NOTE]
>
>有关转储索引定义的更多详细信息，请参阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

其中`datastore path`和`nodestore path`来自AEM实例。

然后，使用适当的Granite存储库包生成索引定义。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>仅从`oak-run-1.12.0`版本开始支持上述索引定义创建过程。 使用Granite存储库包`com.adobe.granite.repository-x.x.xx.jar`完成定位。

上述步骤将创建一个名为`merge-index-definitions_target.json`的JSON文件，该文件包含索引定义。

**2. 在存储库**&#x200B;中创建检查点

在生产AEM实例中创建生命周期较长的检查点。 此操作应在克隆存储库之前完成。

通过位于`http://serveraddress:serverport/system/console/jmx`的JMX控制台，转到`CheckpointMBean`并创建一个具有足够长的生命周期（例如，200天）的检查点。 为此，调用`CheckpointMBean#createCheckpoint`，并将`17280000000`作为生命周期持续时间（以毫秒为单位）的参数。

完成此操作后，复制新创建的检查点ID并使用JMX `CheckpointMBean#listCheckpoints`验证生命周期。

>[!NOTE]
>
>此检查点将在稍后导入索引时删除。

有关更多详细信息，请参阅Oak文档中的[检查点创建](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)。

**为生成的索引定义执行脱机索引**

可以使用oak-run离线完成Lucene重新索引。 此进程在`indexing-result/indexes`下的磁盘上创建索引数据。 它&#x200B;**不会**&#x200B;写入存储库，因此不需要停止正在运行的AEM实例。 创建的文本存储将馈送到此进程：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

在MongoMK安装中使用`--doc-traversal-mode`参数非常方便，因为它通过将存储库内容假脱机到本地平面文件来显着缩短重新索引时间。 但是，它需要两倍于存储库大小的额外磁盘空间。

如果存在MongoMK，则如果在更靠近MongoDB实例的实例中执行此步骤，则可以加快此进程。 如果在同一台计算机上运行，则可以避免网络开销。

有关索引[的](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)Oak-run文档中可找到其他技术详细信息。

### 导入索引 {#importing-indexes}

通过AEM 6.4及更高版本，AEM具有在启动过程中从磁盘导入索引的内置功能。 启动期间观察文件夹`<repository>/indexing-result/indexes`是否存在索引数据。 在启动AEM实例之前，您可以将预创建的索引复制到上述位置。 AEM会将其导入存储库，并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答 {#troubleshooting}

在下方，您将找到一些有用的提示和故障排除说明。

### 减少对实时生产系统的影响 {#reduce-the-impact-on-the-live-production-system}

建议克隆生产系统并使用克隆创建离线索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook并试运行 {#prepare-a-runbook-and-trial-run}

建议先准备Runbook并执行一些试验，然后再在生产环境中运行重新索引过程。

### 带脱机索引的文档遍历模式 {#doc-traversal-mode-with-offline-indexing}

离线索引需要遍历整个存储库。 使用MongoMK安装时，通过网络访问存储库会影响索引过程的性能。 一种选择是在MongoDB副本本身上运行离线索引过程，这将消除网络开销。 另一个选项是使用文档遍历模式。

通过将命令行参数`—doc-traversal`添加到oak-run命令以离线编制索引，可以应用文档遍历模式。 此模式将本地磁盘中整个存储库的副本作为平面文件卷动，并使用它来运行索引。
