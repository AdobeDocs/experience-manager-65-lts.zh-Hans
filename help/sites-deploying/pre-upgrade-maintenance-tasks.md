---
title: 升级前维护任务
description: 了解为AEM推荐的升级前任务。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 1dd5d370-d1d4-4d15-9663-35b941b9076b
source-git-commit: 8f7bbc3887601e10cf29e99ee54959a10c8a3f98
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---

# 升级前维护任务{#pre-upgrade-maintenance-tasks}

在开始升级之前，请务必遵循这些维护任务，以确保系统已准备就绪，并且可以在出现问题时回滚：

* [索引定义](#index-definitions)
* [确保有足够的磁盘空间](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全备份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [生成快速入门.properties文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和审核日志清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安装、配置和运行升级前任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [从/install目录中删除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷备用实例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [禁用自定义计划作业](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [执行脱机修订版清理](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [执行数据存储垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [根据需要升级数据库模式](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [旋转日志文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 索引定义 {#index-definitions}

确保已安装随最新AEM 6.5 Service Pack一起发布的所需索引定义。 (有关详细信息，请参阅[AEM 6.5 servicepack发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/release-notes/release-notes))。

## 确保有足够的磁盘空间 {#ensure-sufficient-disk-space}

执行升级时，请确保有足够的磁盘空间。

## 完全备份AEM {#fully-back-up-aem}

在开始升级之前，应完全备份AEM。 确保备份存储库、应用程序安装、数据存储和Mongo实例（如果适用）。 有关备份和还原AEM实例的详细信息，请参阅[备份和还原](/help/sites-administering/backup-and-restore.md)。

## 生成快速入门.properties文件 {#generate-quickstart-properties}

从jar文件启动AEM时，将在`crx-quickstart/conf`下生成`quickstart.properties`文件。 如果AEM以前仅使用启动脚本启动，则此文件不存在，且升级失败。 确保检查此文件是否存在，如果AEM不存在，请从jar文件重新启动它。

## 配置工作流和审核日志清除 {#configure-wf-audit-purging}

`WorkflowPurgeTask`和`com.day.cq.audit.impl.AuditLogMaintenanceTask`任务需要单独的OSGi配置，没有它们将无法工作。 如果它们在升级前任务执行期间失败，则缺少配置是最可能的原因。 因此，请确保为这些任务添加OSGi配置，或者如果不想运行它们，则从升级前优化任务列表中完全删除它们。 有关配置工作流清除任务的文档可在[管理工作流实例](/help/sites-administering/workflows-administering.md)中找到，有关审核日志维护任务配置的文档可在AEM 6[&#128279;](/help/sites-administering/operations-audit-log.md)中的审核日志维护中找到。


## 安装、配置和运行升级前任务 {#install-configure-run-pre-upgrade-tasks}

以前必须手动执行的升级前维护任务正在优化和自动化。 升级前维护优化功能允许以统一方式触发这些任务，并能够根据需要检查其结果。

### 使用方法 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI组件预配置了可以一次运行的所有升级前维护任务列表。 您可以按照以下步骤配置任务：

1. 通过浏览到&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;转到Web控制台

1. 搜索“**preupgradetasks**”，然后单击第一个匹配的组件。 组件的全名为`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必须运行的维护任务列表，如下所示：

   ![1487758925984](assets/1487758925984.png)

以下是对每个维护任务所针对的运行模式的描述。

| 任务 | 注释 |
|---|---|
| WorkflowpurgeTask | 必须在运行之前配置Adobe Granite工作流清除配置OSGi。 |
| GenerateBundlesListFileTask |   |
| RevisionCleanupTask |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | 在运行之前必须配置审计日志清除计划程序OSGi配置。 |

### 升级前运行状况检查的默认配置 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI组件预配置了调用`runAllPreUpgradeHealthChecks`方法时要执行的升级前运行状况检查标记的列表：

* **system** - granite维护运行状况检查使用的标记

* **升级前** — 自定义标记，可添加到所有可设置为在升级前运行的运行状况检查中

**MBean方法**

可以使用[JMX控制台](/help/sites-administering/jmx-console.md)访问受管Bean功能。

您可以通过以下方式访问MBean：

1. 转到&#x200B;*https://serveraddress:serverport/system/console/jmx*&#x200B;处的JMX控制台
1. 搜索&#x200B;**PreUpgradeTasks**&#x200B;并单击结果

1. 从&#x200B;**操作**&#x200B;部分中选择任意方法，然后在以下窗口中选择&#x200B;**调用**。

以下是`PreUpgradeTasksMBeanImpl`公开的所有可用方法的列表：

| 方法名称 | 类型 | 描述 |
|---|---|---|
| runAllPreUpgradeTasks() | 操作 | 运行列表中的所有升级前维护任务。 |
| runPreUpgradeTask(preUpgradeTaskName) | 操作 | 运行升级前维护任务，其名称作为参数给定。 |
| getPreUpgradeTaskLastRunTime(preUpgradeTaskName) | 操作 | 显示升级前维护任务的确切运行时间，其名称作为参数提供。 |
| getPreUpgradeTaskLastRunState(preUpgradeTaskName) | 操作 | 显示升级前维护任务的上次运行状态，其名称作为参数提供。 |
| runAllPreUpgradeHealthChecks(shutDownOnSuccess) | 操作 | 运行所有升级前运行状况检查，并将其状态保存在sling主路径中名为preUpgradeHCStatus.properties的文件中。 如果shutDownOnSuccess设置为true，AEM实例将关闭，但前提是所有升级前运行状况检查的状态均为“正常”。 属性文件用作任何未来升级的前提条件，如果升级前运行状况检查执行失败，升级过程将停止。 如果要忽略升级前运行状况检查的结果并仍启动升级，可以删除文件。 |
| detectUsageOfUnavailableAPI(aemVersion) | 操作 | 列出在升级到指定的AEM版本时不再满足的所有导入包。 目标AEM版本必须作为参数提供。 |

>[!NOTE]
>
>可以通过以下方式调用MBean方法：
>
>* JMX控制台
>* 连接到JMX的任何外部应用程序
>* cURL
>

## 从/install目录中删除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>仅在关闭AEM实例后，从crx-quickstart/install目录中删除包。 此步骤是开始就地升级过程之前的最后一个步骤。

删除通过本地文件系统上的`crx-quickstart/install`目录部署的所有Service Pack、功能包或修补程序。 这样做可防止在更新完成后，在新AEM版本之上意外安装旧修补程序和Service Pack。

## 停止任何冷备用实例 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷备用，请停止任何冷备用实例。 这样做可以确保在升级过程中出现问题，高效地重新上线。 成功完成升级后，必须从升级的主实例重建冷备用实例。

## 禁用自定义计划作业 {#disable-custom-scheduled-jobs}

禁用应用程序代码中包含的任何OSGi计划作业。

## 执行脱机修订版清理 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步骤仅对于TarMK安装是必需的

如果使用TarMK，则在升级之前应运行脱机修订版清理。 这样做可以使存储库迁移步骤和后续升级任务的执行速度更快，并且有助于确保在升级完成后可以成功执行在线修订版清理。 有关运行脱机修订清理的信息，请参阅[正在执行脱机修订清理](/help/sites-deploying/revision-cleanup.md#revision-cleanuprevision-cleanup)。

## 执行数据存储垃圾收集 {#execute-datastore-garbage-collection}

对CRX3实例运行修订清理后，您应该运行数据存储垃圾收藏集以删除数据存储中所有未引用的Blob。 有关说明，请参阅有关[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)的文档。

## 旋转日志文件 {#rotate-log-files}

Adobe建议在开始升级之前存档当前的日志文件。 这样，在升级期间和升级后，可以更轻松地监视和扫描日志文件，以识别并解决可能出现的任何问题。
