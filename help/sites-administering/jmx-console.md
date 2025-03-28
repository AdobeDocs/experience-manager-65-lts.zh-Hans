---
title: 使用JMX控制台监控服务器资源
description: 了解如何使用JMX控制台监控服务器资源。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Operations
role: Admin
exl-id: c5907a0b-031f-4e3a-8a5c-5daf31eb71fc
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '4830'
ht-degree: 0%

---

# 使用JMX控制台监控服务器资源{#monitoring-server-resources-using-the-jmx-console}

通过JMX控制台，您可以监视和管理CRX服务器上的服务。 后面的部分总结了通过JMX框架公开的属性和操作。

有关如何使用控制台控件的信息，请参阅[使用JMX控制台](#using-the-jmx-console)。 有关JMX的背景信息，请参阅Oracle网站上的[Java Management Extensions (JMX)技术](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html)页。

有关创建MBean以使用JMX控制台管理服务的信息，请参阅[将服务与JMX控制台集成](/help/sites-developing/jmx-integration.md)。

## 工作流维护 {#workflow-maintenance}

用于管理正在运行、已完成、过时和失败的工作流实例的操作。

* 域： com.adobe.granite.workflow
* 类型：维护

>[!NOTE]
>
>有关其他工作流管理工具和可能的工作流实例状态的说明，请参阅[工作流控制台](/help/sites-administering/workflows-administering.md)。

### 运营 {#operations}

**listRunningWorkflowsPerModel**&#x200B;列出每个工作流模型正在运行的工作流实例数。

* 参数：无
* 返回的值：包含Count和ModelId列的表格式数据。

**listCompletedWorkflowsPerModel**&#x200B;列出每个工作流模型的已完成工作流实例数。

* 参数：无
* 返回的值：包含Count和ModelId列的表格式数据。

**returnWorkflowQueueInfo**&#x200B;列出有关已处理的工作流项和已排队等待处理的工作流项的信息。

* 参数：无
* 返回值：包含以下列的表格式数据：

   * Jobs
   * 队列名称
   * 活动作业
   * 平均处理时间
   * 平均等待时间
   * 取消的作业
   * 失败的作业
   * 已完成的作业
   * 已处理的作业
   * 排队的作业

**returnWorkflowJobTopicInfo**&#x200B;按主题列出工作流作业的处理信息。

* 参数：无
* 返回值：包含以下列的表格式数据：

   * 主题名称
   * 平均处理时间
   * 平均等待时间
   * 取消的作业
   * 失败的作业
   * 已完成的作业
   * 已处理的作业

**returnFailedWorkflowCount**&#x200B;显示失败的工作流实例数。 您可以指定工作流模型来查询或检索所有工作流模型的信息。

* 参数：

   * model：要查询的模型的ID。 要查看所有工作流模型的失败工作流实例计数，请不要指定任何值。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：失败的工作流实例数。

**returnFailedWorkflowCountPerModel**&#x200B;显示每个工作流模型失败的工作流实例数。

* 参数：无。
* 返回的值：包含“计数”和“模型ID”列的表格数据。

**terminateFailedInstances**&#x200B;终止失败的工作流实例。 您可以终止所有失败的实例，或仅终止特定模型的失败实例。 或者，您可以在实例终止后重新启动实例。 也可以测试操作以查看结果，而无需实际执行该操作。

* 参数：

   * 重新启动实例： （可选）指定值`true`以在实例终止后重新启动实例。 默认值`false`导致无法重新启动已终止的工作流实例。
   * 试运行： （可选）指定值`true`以查看操作的结果，而不实际执行操作。 默认值`false`导致执行该操作。
   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的失败实例。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：有关已终止实例的表格式数据，包含以下列：

   * 发起者
   * 实例ID
   * 模型ID
   * 有效负荷
   * 开始注释
   * 工作流标题

**retryFailedWorkItems**&#x200B;尝试执行工作项步骤失败。 您可以针对特定工作流模型重试所有失败的工作项或仅重试失败的工作项。 您可以选择测试工序以查看结果，而无需实际执行该工序。

* 参数：

   * 试运行： （可选）指定值`true`以查看操作的结果，而不实际执行操作。 默认值`false`导致执行该操作。
   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的失败工作项。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：有关重试的失败工作项的表格式数据，包括以下列：

   * 发起者
   * 实例ID
   * 模型ID
   * 有效负荷
   * 开始注释
   * 工作流标题

**PurgeActive**&#x200B;删除特定时期的活动工作流实例。 您可以清除所有模型的活动实例，或仅清除特定模型的实例。 您可以选择测试工序以查看结果，而无需实际执行该工序。

* 参数：

   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流启动以来的天数：要清除的工作流实例的时限（以天为单位）。
   * 试运行： （可选）指定值`true`以查看操作的结果，而不实际执行操作。 默认值`false`导致执行该操作。

* 返回值：有关已清除的活动工作流实例的表格数据，包括以下列：

   * 发起者
   * 实例ID
   * 模型ID
   * 有效负荷
   * 开始注释
   * 工作流标题

**countStaleWorkflows**&#x200B;返回过期的工作流实例数。 您可以检索所有工作流模型或特定模型的过时实例数。

* 参数：

   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：过期的工作流实例数。

**restartStaleWorkflows**&#x200B;重新启动过时的工作流实例。 您可以重新启动所有过时实例，或仅重新启动特定模型的过时实例。 也可以测试操作以查看结果，而无需实际执行该操作。

* 参数：

   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的过时实例。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 试运行： （可选）指定值`true`以查看操作的结果，而不实际执行操作。 默认值`false`导致执行该操作。

* 返回的值：已重新启动的工作流实例的列表。

**fetchModelList**&#x200B;列出所有工作流模型。

* 参数：无
* 返回值：标识工作流模型（包括ModelId和ModelName列）的表格数据。

**countRunningWorkflows**&#x200B;返回正在运行的工作流实例数。 您可以检索所有工作流模型或特定模型的运行实例数。

* 参数：

   * 模型： （可选）返回其运行实例数的模型的ID。 指定无模型可返回所有工作流模型的运行实例数。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：正在运行的工作流实例的数量。

**countCompletedWorkflows**&#x200B;返回已完成的工作流实例数。 您可以检索所有工作流模型或特定模型的已完成实例数。

* 参数：

   * 模型： （可选）返回已完成实例数的模型的ID。 指定无模型可返回所有工作流模型的已完成实例数。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：已完成的工作流实例的数量。

**purgeCompleted**&#x200B;从存储库中删除已完成的特定时期工作流的记录。 当您大量使用工作流时，请定期使用此操作以最大限度地减小存储库的大小。 您可以清除所有模型的已完成实例，或仅清除特定模型的实例。 您可以选择测试工序以查看结果，而无需实际执行该工序。

* 参数：

   * 模型： （可选）要应用操作的模型的ID。 不指定任何模型以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流完成以来的天数：工作流实例处于已完成状态的天数。
   * 试运行： （可选）指定值`true`以查看操作的结果，而不实际执行操作。 默认值`false`导致执行该操作。

* 返回值：有关已清除的已完成工作流实例的表格数据，包括以下列：

   * 发起者
   * 实例ID
   * 模型ID
   * 有效负荷
   * 开始注释
   * 工作流标题

## 存储库 {#repository}

有关CRX存储库的信息

* 域： com.adobe.granite
* 类型：存储库

### 属性 {#attributes}

**名称** JCR存储库实施的名称。 只读。

**版本**&#x200B;存储库实施版本。 只读。

**HomeDir**&#x200B;存储库所在的目录。 默认位置为&lt;QuickStart_Jar_Location>/crx-quickstart/repository。 只读。

**CustomerName**&#x200B;软件许可证颁发给的客户的名称。 只读。

**LicenseKey**&#x200B;此存储库安装的唯一许可证密钥。 只读。

**可用磁盘空间**&#x200B;此存储库实例可用的磁盘空间（以MB为单位）。 只读。

**MaximumNumberOfOpenFiles**&#x200B;一次可以打开的文件数。 只读。

**SessionTracker** crx.debug.sessions系统变量的值。 true表示调试会话。 false表示正常会话。 读/写。

**描述符**&#x200B;表示存储库属性的键值对集。 所有属性均为只读。

<table>
 <tbody>
  <tr>
   <th>键</th>
   <th>价值</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>指示节点和节点的属性是否可以具有相同的名称。 true表示支持相同名称，false表示不支持相同名称。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>指示不可引用节点标识符的稳定性。 可以使用以下值：
    <ul>
     <li>identifier.stability.infinition.duration：标识符不会更改。</li>
     <li>identifier.stability.method.duration：在方法调用之间可以更改标识符。</li>
     <li>identifier.stability.save.duration：标识符在保存/刷新周期内不会更改。</li>
     <li>identifier.stability.session.duration：标识符在会话期间不会更改。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支持JCR 1.0 XPath查询语言。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>在system.id文件中找到的系统标识符。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>指示是否支持JCR 1.0 XPath查询语言。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>存储库实施的版本。</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>指示节点的主节点类型是否可以更改。 true表示可以更改主节点类型，false表示不支持更改。</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>指示是否支持节点类型管理。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>指示是否可以覆盖节点类型的继承属性或子节点定义。 true表示支持覆盖，false表示无覆盖。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支持对存储库更改进行异步观察。 支持异步观察使应用程序能够在每次更改发生时接收和响应有关这些更改的通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr：score伪属性在包含jcrfn：contains（在XPath中）或CONTAINS（在SQL中）函数以执行全文搜索的XPath和SQL查询中可用。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示存储库支持简单版本控制。 通过简单的版本控制，存储库可维护节点的连续一系列版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示存储库支持使用API创建和删除工作区。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示存储库支持添加和删除现有节点的mixin节点类型。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示存储库允许节点定义将主项目作为子项包含。 主项目可以使用API访问，而无需知道项目名称。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED均为true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示存储库使用API提供写访问权限。 false表示只读访问。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示您可以更改现有节点正在使用的节点定义。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>存储库实施的JCR规范的版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示应用程序可以对存储库执行日志观察。 通过日志观察，可以获得特定时间段内的一组更改通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>存储库支持的查询语言。 无值表示不支持查询。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true表示存储库支持将节点导出为XML代码。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true表示存储库支持注册具有多个二进制属性的节点类型。 false表示节点类型支持单个二进制属性。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true表示存储库支持访问控制，用于设置和确定节点访问的用户权限。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示存储库支持配置和基线。</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true表示存储库支持创建可共享节点。</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>存储库集群的标识符。</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true表示存储库支持存储的查询。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示存储库支持全文搜索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>指示对节点类型继承的存储库支持的级别。 可以使用以下值：</p> <p>node.type.management.inheritance.minimal：主节点类型的注册仅限于仅将nt：base作为超类型的节点。 mixin节点类型的注册仅限于没有超类型的节点。</p> <p>node.type.management.inheritance.single：主节点类型的注册仅限于具有一个超类型的节点。 Mixin节点类型的注册仅限于最多具有一个超类型的节点。</p> <p><br /> node.type.management.inheritance.multiple：可以使用一个或多个超类型注册主节点类型。 Mixin节点类型可以使用零个或多个超类型进行注册。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true表示此群集节点是群集的首选主节点。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true表示存储库支持事务。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>存储库供应商的URL。</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true表示存储库支持节点属性的值约束。</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>javax.jcr.PropertyType常量的数组，这些常量表示注册的节点类型可以指定的属性类型。 零长度数组指示注册的节点类型不能指定属性定义。 属性类型包括STRING、URI、BOOLEAN、LONG、DOUBLE、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE和UNDEFINED（如果支持）</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true表示存储库支持保留子节点的顺序。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>存储库供应商的名称。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>查询中连接的支持级别。 可以使用以下值：</p>
    <ul>
     <li>query.joins.none：不支持连接。 查询可以使用一个选择器。</li>
     <li>query.joins.inner：支持内部连接。</li>
     <li>query.joins.inner.outer：支持内连接和外连接。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true表示存储库支持XPath 1.0查询语言。</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true表示存储库支持将XML代码作为内容导入。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示存储库支持同名的同级节点（具有相同父项的节点）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示存储库支持带有剩余定义的名称属性。 如果受支持，项目定义的名称属性可以是星号(“*”)。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示存储库支持在创建节点时自动创建节点的子项（节点或属性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此存储库节点是群集的主节点。</td>
  </tr>
  <tr>
   <td>级别1.受支持</td>
   <td>true表示option.xml.export.support为true，而query.languages的长度不为零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示存储库支持未归档的内容。 未归档的节点不属于存储库层次结构。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>存储库实施的JCR规范的名称。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true表示存储库支持完全版本控制。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>存储库的名称。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示存储库支持节点锁定。 锁定使用户可以暂时阻止其他用户进行更改。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示存储库支持活动。 活动是在工作区中执行的一组更改，这些更改被合并到另一个工作区中。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示存储库支持可以具有零个或多个值的节点属性。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示存储库支持使用外部保留管理应用程序将保留策略应用于内容，并支持保留和释放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示存储库支持生命周期管理。</td>
  </tr>
 </tbody>
</table>

**工作区名称**&#x200B;存储库中工作区的名称。 只读。

**DataStoreGarbageCollectionDelay**&#x200B;扫描每10个节点后垃圾收集休眠的时间（以毫秒为单位）。 读/写。

**BackupDelay**&#x200B;备份过程在备份的每个步骤之间休眠的时间（以毫秒为单位）。 读/写。

**BackupInProgress** true值表示正在执行备份进程。 只读。

**BackupProgress**&#x200B;对于当前备份，已备份的所有文件的百分比。 只读。

**CurrentBackupTarget**&#x200B;对于当前备份，为存储备份文件的ZIP文件。 当备份未进行时，不会显示任何值。 只读。

**BackupWasSuccessful**&#x200B;值为true表示当前备份期间没有发生错误，或者没有正在进行备份。 false表示当前备份期间出错。 只读。

**BackupResult**&#x200B;当前备份的状态。 可以使用以下值：

* 正在进行备份：当前正在执行备份。
* 已取消备份：已取消备份。
* 备份已完成，但出现错误：备份过程中出现错误。 错误消息提供有关原因的信息。
* 备份已完成：备份成功。
* 目前未执行任何备份：没有正在进行的备份。

只读。

**TarOptimizationRunningSince**&#x200B;当前TAR文件优化进程开始的时间。 只读。

**TarOptimizationDelay** TAR优化进程在每个步骤之间休眠的时间（以毫秒为单位）。 读/写。

**ClusterProperties**&#x200B;表示群集属性和值的一组键值对。 表中的每一行代表一个群集属性。 只读。

**ClusterNodes**&#x200B;存储库群集的成员。

**ClusterId**&#x200B;此存储库群集的标识符。 只读。

**ClusterMasterId**&#x200B;此存储库群集的主节点的标识符。 只读。

**ClusterNodeId**&#x200B;存储库群集的此节点的标识符。 只读。

### 运营 {#operations-1}

**createWorkspace**&#x200B;在此存储库中创建工作区。

* 参数：

   * name：表示新工作区名称的字符串值。

* 返回值：无

**runDataStoreGarbageCollection**&#x200B;对存储库节点执行垃圾收集。

* 参数：

   * 删除：一个布尔值，指示是否删除未使用的存储库项目。 值为true会导致删除未使用的节点和属性。 如果值为false，则会扫描所有节点，但不会删除任何节点。

* 返回值：无

**stopDataStoreGarbageCollection**&#x200B;停止正在运行的数据存储垃圾收集。

* 参数：无
* 返回值：当前状态的字符串表示形式

**startBackup**&#x200B;在ZIP文件中备份存储库数据。

* 参数：

   * `target`：（可选）一个`String`值，表示要将存储库数据存档到的ZIP文件或目录的名称。 要使用ZIP文件，请包含ZIP文件扩展名。 要使用目录，请不要包含文件扩展名。

     要执行增量备份，请指定以前用于备份的目录。

     您可以指定绝对路径或相对路径。 相对路径相对于crx-quickstart目录的父级路径。

     未指定值时，将使用默认值`backup-currentdate.zip`，其中`currentdate`的格式为`yyyyMMdd-HHmm`。

* 返回值：无

**cancelBackup**&#x200B;停止当前的备份进程，并删除该进程为存档数据而创建的临时存档。

* 参数：无
* 返回值：无

**blockRepositoryWrites**&#x200B;阻止对存储库数据的更改。 所有资料库备份侦听程序都会收到有关该块的通知。

* 参数：无
* 返回值：无

**unblockRepositoryWrites**&#x200B;从存储库中删除块。 所有资料库备份侦听程序都会收到块删除的通知。

* 参数：无
* 返回值：无

**startTarOptimization**&#x200B;使用tarOptimizationDelay的默认值启动TAR文件优化过程。

* 参数：无
* 返回值：无

**stopTarOptimization**&#x200B;停止TAR文件优化。

* 参数：无
* 返回值：无

**tarIndexMerge**&#x200B;合并所有TAR集的顶级索引文件。 顶级索引文件是具有不同主版本的文件。 例如，以下文件将合并到文件index_3_1.tar中： index_1_1.tar 、 index_2_0.tar 、 index_3_0.tar。 已合并的文件将被删除（在前面的示例中，删除了index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 参数：

   * `background`：一个布尔值，指示是否在后台运行操作，以便在执行期间可以使用Web控制台。 值为true会在后台运行该操作。

* 返回值：无

**becomeClusterMaster**&#x200B;将此存储库节点设置为群集的主节点。 如果尚未为主节点，则此命令将停止当前主实例的侦听器，并在当前节点上启动主侦听器。 然后，将此节点设置为主节点并重新启动，从而导致群集中的所有其他节点（即由主节点控制的节点）连接到此实例。

* 参数：无
* 返回值：无

**joinCluster**&#x200B;将此存储库作为群集主节点添加到群集。 提供用户名和密码以进行身份验证。 连接使用基本身份验证。 安全凭据在发送到服务器之前进行base-64编码。

* 参数：

   * `master`：一个字符串值，表示运行主存储库节点的计算机的IP地址或计算机名。
   * `username`：用于对群集进行身份验证的名称。
   * `password`：用于身份验证的密码。

* 返回值：无

**traversalCheck**&#x200B;从特定节点开始遍历子树并可以选择修复其中的不一致。 有关持久性管理器的文档将对此进行详细介绍。

**consistencyCheck**&#x200B;检查并（可选）修复数据存储中的一致性。 数据存储上的文档将对此进行详细介绍。

## 存储库统计数据（时间序列） {#repository-statistics-timeseries}

`org.apache.jackrabbit.api.stats.RepositoryStatistics`定义的每种统计类型的TimeSeries字段的值。

* 域： `com.adobe.granite`
* 类型：`TimeSeries`
* 名称： `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum类中的以下值之一：

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * 查询计数
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 属性 {#attributes-1}

为报告的每种统计类型提供了以下属性：

* ValuePerSecond：过去一分钟内的每秒测量值。 只读。
* ValuePerMinute：过去一小时内每分钟测量的值。 只读。
* ValuePerHour：上周每小时的测量值。 只读。
* ValuePerWeek：过去三年中每周测量到的值。 只读。

## 存储库查询统计信息 {#repository-query-stats}

有关存储库查询的统计信息。

* 域： com.adobe.granite
* 类型：QueryStat

### 属性 {#attributes-2}

**SlowQueries**&#x200B;有关完成时间最长的存储库查询的信息。 只读。

**SlowQueriesQueueSize**&#x200B;要包含在SlowQueries列表中的最大查询数。 读写。

**PopularQueries**&#x200B;有关发生次数最多的存储库查询的信息。 只读。

**PopularQueriesQueueSize** PopularQueries列表中的最大查询数。 读写。

### 运营 {#operations-2}

**clearSlowQueriesQueue**&#x200B;从SlowQueries列表中删除所有查询。

* 参数：无
* 返回值：无

**clearPopularQueriesQueue**&#x200B;从PopularQueries列表中删除所有查询。

* 参数：无
* 返回值：无

## 复制代理 {#replication-agents}

监视每个复制代理的服务。 创建复制代理时，服务会自动显示在JMX控制台中。

* **域：** com.adobe.granite.replication
* **类型：**&#x200B;代理
* **名称：**&#x200B;没有值
* **属性：** {id=&quot;*名称*&quot;}，其中&#x200B;*名称*&#x200B;是代理Name属性的值。

### 属性 {#attributes-3}

**Id**&#x200B;表示复制代理配置的标识符的字符串值。 多个代理可以使用相同的配置。 只读。

**有效**&#x200B;指示代理配置是否正确的布尔值：

* `true`：配置有效。
* `false` ：配置包含错误。

只读。

**已启用**&#x200B;指示代理是否已启用的布尔值：

* `true`：已启用。
* `false`：已禁用。

**QueueBlocked**&#x200B;布尔值，指示队列是否存在且被阻止：

* `true`：已阻止。 正在等待自动重试。
* `false`：未阻止或不存在。

只读。

**QueuePaused**&#x200B;指示作业队列是否暂停的布尔值：

* `true`：已暂停（已暂停）
* `false`：未暂停或不存在。

读写。

**QueueNumEntries**&#x200B;表示代理队列中的作业数的int值。 只读。

**QueueStatusTime**&#x200B;日期值，指示获取显示的状态值时服务器上的时间。 该值对应于加载页面的时间。 只读。

**QueueNextRetryTime**&#x200B;对于被阻止的队列，使用日期值指示下次自动重试的时间。 如果没有显示时间，则不会阻止队列。 只读。

**QueueProcessingSince**&#x200B;日期值，指示当前作业的处理开始时间。 如果未显示时间，则队列将被阻塞或闲置。 只读。

**QueueLastProcessTime**&#x200B;指示上一个作业何时完成的日期值。 只读。

### 运营 {#operations-3}

**queueForceRetry**&#x200B;对于被阻止的队列，向队列发出重试命令。

* 参数：无
* 返回值：无

**queueClear**&#x200B;从队列中删除所有作业。

* 参数：无
* 返回值：无

## Sling引擎 {#sling-engine}

提供有关HTTP请求的统计信息，以便您可以监视SlingRequestProcessor服务的性能。

* 域： org.apache.sling
* 类型：引擎
* 属性：{service=RequestProcessor}

### 属性 {#attributes-4}

**RequestsCount**&#x200B;自上次重置统计信息以来发生的请求数。

**MinRequestDurationMsec**&#x200B;自上次重置统计信息以来处理请求所需的最短时间（以毫秒为单位）。

**MaxRequestDuratioMsec**&#x200B;自上次重置统计信息以来，处理请求所需的最长时间（以毫秒为单位）。

**StandardDeviationDurationMsec**&#x200B;处理请求所需时间的标准偏差。 使用自上次重置统计信息以来的所有请求计算标准偏差。

**MeanRequestDurationMsec**&#x200B;处理请求所需的平均时间。 使用自上次重置统计信息以来的所有请求计算平均值

### 运营 {#operations-4}

**resetStatistics**&#x200B;将所有统计信息设置为零。 当您需要分析特定时间范围内的请求处理性能时，请重置统计信息。

* 参数：无
* 返回值：无

**id**&#x200B;包ID的字符串表示形式。

**已安装**&#x200B;指示是否已安装包的布尔值：

* `true`：已安装。
* `false`：未安装。

**installedBy**&#x200B;上次安装包的用户的ID。

**installedDate**&#x200B;上次安装包的日期。

**size**&#x200B;保存包大小（字节）的长值。


## 快速入门启动器 {#quickstart-launcher}

有关启动过程和快速入门启动器的信息。

* 域： com.adobe.granite.quickstart
* 类型：启动器

### 运营 {#operations-5}

**log**

在QuickStart窗口中显示消息。

参数：

* p1：表示要显示的消息的`String`值。
* 返回值：无

**startupFinished**

调用服务器启动器的startupFinished方法。 方法会尝试在Web浏览器中打开欢迎页面。

* 参数：无
* 返回值：无

**startupProgress**

设置服务器启动进程的完成值。 QuickStart窗口中的进度条表示完成值。

* 参数：
   * p1：一个浮点值，以小数形式表示启动过程完成的程度。 该值应介于0和1之间。 例如，0.3表示已完成30%。
* 返回值：无。

## 第三方服务 {#third-party-services}

一些第三方服务器资源安装了向JMX控制台公开属性和操作的MBean。 下表列出了第三方资源并提供指向更多信息的链接。

<table>
 <tbody>
  <tr>
   <th>域</th>
   <th>类型</th>
   <th>MBean类</th>
  </tr>
  <tr>
   <td>JMI实现</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotspotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>类加载</li>
     <li>编译</li>
     <li>垃圾收集器</li>
     <li>内存</li>
     <li>内存管理器</li>
     <li>内存池</li>
     <li>操作系统</li>
     <li>运行时间</li>
     <li>线程</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a>包</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>框架</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a>包</td>
  </tr>
 </tbody>
</table>

## 使用JMX控制台 {#using-the-jmx-console}

JMX控制台显示有关服务器上运行的多个服务的信息：

* 属性：服务属性，如配置或运行时数据。 属性可以是只读或读写。
* 操作：可以对服务调用的命令。

与OSGi服务一起部署的MBean向控制台公开服务属性和操作。 MBean确定公开的属性和操作，以及属性是只读属性还是读写属性。

JMX控制台的主页包括一个服务表。 表中的每一行表示一个由MBean公开的服务。

1. 打开Web控制台，然后单击JMX选项卡。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 单击服务的单元格值可查看服务的属性和操作。
3. 要更改属性值，请单击该值，在显示的对话框中指定该值，然后单击保存。
4. 要调用服务操作，请单击操作名称，在显示的对话框中指定参数值，然后单击调用。

## 使用外部JMX应用程序进行监控 {#using-external-jmx-applications-for-monitoring}

CRX允许外部应用程序通过[Java管理扩展(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)与托管Bean (MBean)交互。 使用通用控制台（如[JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html)或特定于域的监视应用程序），可以获取和设置CRX配置和属性，以及监视性能和资源使用情况。

### 使用JConsole连接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole连接到CRX，请执行以下步骤：

1. 打开终端窗口。
1. 输入以下命令：

   `jconsole`

将启动JConsole并显示JConsole窗口。

### 连接到本地CRX进程 {#connecting-to-a-local-crx-process}

JConsole将显示本地Java虚拟机进程的列表。 该列表将包含两个快速入门流程。 从本地进程（通常是PID较高的进程）列表中选择快速入门“CHILD”进程。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 连接到远程CRX进程 {#connecting-to-a-remote-crx-process}

要连接到远程CRX进程，必须启用承载远程CRX进程的JVM以接受远程JMX连接。

要启用远程JMX连接，在启动JVM时必须设置以下系统属性：

`com.sun.management.jmxremote.port=portNum`

在上述属性中，`portNum`是您要启用JMX RMI连接的端口号。 请确保指定一个未使用的端口号。 除了发布RMI连接器以进行本地访问外，设置此属性还会在专用只读注册表中使用已知名称“jmxrmi”在指定端口发布其他RMI连接器。

默认情况下，启用JMX代理进行远程监视时，它使用基于密码文件的密码验证，启动Java VM时需要使用以下系统属性指定该密码文件：

`com.sun.management.jmxremote.password.file=pwFilePath`

有关设置密码文件的详细说明，请参阅[相关的JMX文档](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html)。

示例：

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX提供的MBean {#using-the-mbeans-provided-by-crx}

在连接到快速入门流程后，JConsole为CRX所运行的JVM提供了一系列常规监视工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

要访问CRX的内部监控和配置选项，请转到MBeans选项卡，然后从左侧的分层内容树中，选择您感兴趣的属性或操作部分。 例如，com.adobe.granite/Repository/Operations部分。

在该部分中，在左窗格中选择所需的属性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
