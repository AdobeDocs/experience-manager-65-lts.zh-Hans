---
title: 使用Oak将AEM 6.5迁移到AEM 6.5 LTS内容
description: 了解如何使用Oak升级工具将内容从AEM 6.5迁移到AEM 6.5 LTS
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# 使用Oak将AEM 6.5迁移到AEM 6.5 LTS内容 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

本文档介绍如何将Adobe Experience Manager从&#x200B;**6.5**&#x200B;升级到&#x200B;**6.5 LTS**，重点介绍如何迁移内容存储库。 它涵盖了使用Oak-upgrade工具在存储库之间传输内容时的精确性和控制性。

## 先决条件 {#prerequisites}

在开始迁移之前，请确保满足以下要求：

1. Java兼容性：必须安装并配置AEM 6.5 LTS才能与Java™ 17一起运行。 设置后，启动AEM实例，并验证所有捆绑包是否处于活动状态且运行正常，没有出现问题
1. 系统资源：确保在迁移过程中有足够的磁盘空间和内存来处理两个存储库
1. Oak-upgrade工具：从`oak-upgrade`官方Maven存储库[下载](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) jar。 确保版本与AEM 6.5 LTS中使用的Oak-core版本匹配。 Oak升级工具在Oracle® Java™ 11或更高版本上运行

## 迁移过程 {#step-by-step-migration-process}

### 停止AEM 6.5和AEM 6.5 LTS {#stopping-aem65-and-aem65lts}

在启动迁移之前，请停止AEM 6.5和AEM 6.5 LTS实例。 这样做可确保存储库处于稳定状态，在迁移期间不会发生额外的写入。

### 备份AEM 6.5实例 {#backing-up-the-aem65-instance}

对您的AEM 6.5实例进行完整备份（如果尚未进行）。

### 使用Oak-upgrade工具迁移内容 {#using-the-oak-upgrade-tool-for-content-migration}

Oak-Upgrade工具通过命令行执行，如下所示：

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

以下是基本命令和选项：

**键选项**

* `--include-paths`：指定要包含在迁移中的子树。 有关命令用法，请参见此示例：

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`：从迁移中排除特定路径。 使用此选项时请务必谨慎 — 如果目标系统上存在该路径，则会将其删除。 有关命令用法，请参见此示例：

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`：默认情况下，Oak-upgrade仅迁移对二进制文件的引用，将实际文件保留在原始blob/数据存储中。 因此，新的资料档案库仍依赖于二进制文件的源存储。 要将二进制文件与存储库内容一起迁移，请使用`--copy-binaries`参数将所有二进制数据复制到新存储，如下所示：

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### 迁移检查点 {#migratiing-checkpoints}

将旧的SegmentMK存储库(低于Oak 1.6版本)迁移到新的SegmentMK(Oak版本高于或等于1.6版本)时，也会迁移检查点。 首次在新存储库上运行Oak时，此过程可避免重新编制索引。 但是，在以下情况下不会迁移检查点：

1. 指定了自定义包括、排除或合并路径，或者
1. 系统通过引用复制二进制文件。 未指定源数据存储，两个不同的检查点在同一路径下包含不同的二进制文件。

对于第二种情况，Oak-upgrade会发送以下警告并中断：

```
Checkpoints are not copied, because no external datastore has been specified. This results in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

解决此问题的最简单方法是在命令行选项（例如`--src-datastore`或`--src-s3datastore`）中指定源数据存储。

也可以忽略警告，但在这种情况下，存储库在第一次启动时完全重新索引。 这可能是一个漫长的过程，尤其是对于大型实例而言。 在重新索引过程完成之前，存储库不可用。 使用`--skip-checkpoints`选项禁止显示警告。

您也可以在启动AEM之前使用[脱机重新索引](/help/sites-deploying/offline-reindexing.md)脱机重新索引存储库，以避免在第一次启动时完全重新索引。

有关Oak升级工具和高级用法的详细信息，请参阅[官方文档](https://jackrabbit.apache.org/oak/docs/migration.html)。
