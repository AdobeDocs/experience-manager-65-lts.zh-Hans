---
title: 延迟内容迁移
description: 了解Adobe Experience Manager 6.4中的延迟内容迁移。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: 78c5486c-ed84-4ec8-b0b0-42d4e8611098
source-git-commit: 09d2e75729060135f9eff1fc9f0126b0f940310b
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# 延迟内容迁移 {#lazy-content-migration}

为了向后兼容，从Adobe Experience Manager (AEM) 6.3开始的&#x200B;**/etc**&#x200B;和&#x200B;**/content**&#x200B;中的内容和配置在升级后不会立即接触或转换。 这样做是为了确保客户应用程序对这些结构的依赖关系保持不变。 即使开箱即用的AEM 6.5中的内容将在其他位置托管，与这些内容结构相关的功能仍然相同。

虽然并非所有这些位置都可以自动转换，但有一些延迟的`CodeUpgradeTasks`也称为延迟内容迁移。 这允许客户通过重新启动具有以下系统属性的实例来触发这些自动转换：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

这会导致在迁移期间运行`CodeUpgradeTasks`。

虽然目标是高效执行，但此升级过程是同步的，因此会随着必须处理的内容量的不同而出现停机。 Adobe建议在生产系统之前评估暂存环境中的运行时间，以计划相应的维护时段。

由于这通常还需要调整应用程序，因此，此活动应该与相应的应用程序部署一起执行。

以下是6.5中引入的`CodeUpgradeTasks`的完整列表：

| **名称** | **相关** **适用于**&#x200B;之前的AEM版本 | **迁移** **类型** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即时 | 检测从`VersionStorage`中删除的所有`LiveRelationShips`并将排除属性添加到父级 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即时 | 通过默认设置重新构建cloudservices以提供安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 删除从&#x200B;**/content**&#x200B;到&#x200B;**/conf**&#x200B;的基于属性的链接（替换为OSGi机制），并生成相应的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即时 | 由于merge_preserve处理，默认的安全拒绝规则将覆盖给定的权限，因此需要在升级时重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即时 | 使用Html5SmartFile小组件检测组件，在内容中搜索组件的使用情况并重新构建持久性，有效地将二进制文件下移一级，而不是将其存储在组件级别。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即时 | 将旧样式项目从&#x200B;**/etc/projects**&#x200B;移至&#x200B;**/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即时 | 将容器层引入层级（区域）并调整引用。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即时 | 设置目标组件的固定位置名称。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即时 | 6.2结构、实例、通知之前的复杂工作流模型转换，然后从&#x200B;**/var/backup**&#x200B;的备份位置合并回来 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 将资源、自定义元数据架构和处理配置文件从&#x200B;**/apps**&#x200B;移动到&#x200B;**/conf**，并将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即时 | 将资源和自定义搜索Facet从&#x200B;**/apps**&#x200B;移动到&#x200B;**/conf**，并将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即时 | 更新InboxItems以排序收件箱项目（调整元数据以实现高效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即时 | 通过将&#x200B;**/conf**&#x200B;的相对路径替换为&#x200B;**/apps**&#x200B;来调整文件夹上的metadataSchema属性 |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即时 | 调整导航结构 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即时 | 将监视仪表板的自定义配置从&#x200B;**/libs**&#x200B;和&#x200B;**/apps**&#x200B;移出 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即时 | 转换Assets中的processingProfile属性（在6.1之前使用）以匹配6.3及更高版本结构。 还将配置文件的相对路径调整为&#x200B;**/conf**，而不是&#x200B;**/apps**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即时 | 升级任务，用于在发生升级时删除过时的CRXDE Lite和Web控制台菜单项。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延迟 | 移动SRP云配置、社区标语配置、清理&#x200B;**/etc/social**&#x200B;和&#x200B;**/etc/enablement**（运行延迟迁移时，必须调整任何引用和数据 — 任何应用程序部分都应不再依赖于此结构）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延迟 | 清理&#x200B;**/etc/cloudsettings** （包含ContextHub配置）。 首次访问时自动迁移配置。 如果启动延迟内容迁移的同时升级&#x200B;**/etc/cloudsettings**&#x200B;中的此内容，则必须在升级之前通过包保留并重新安装，以便隐式转换生效，并且在完成之后后续卸载包。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延迟 | 将旧版标题结构调整为用户配置文件节点中的标题。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延迟 | 将商务内容从&#x200B;**/etc/commerce**&#x200B;迁移到&#x200B;**/var/commerce**。 在迁移期间，将移动内容并更新对已移动内容的引用，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延迟 | 将旧目录设置和Dynamic Media云服务设置从&#x200B;**/etc**&#x200B;迁移到&#x200B;**/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延迟 | 清理&#x200B;**/etc/clientlibs**&#x200B;下的旧版clientlibs |
