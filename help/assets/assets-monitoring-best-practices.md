---
title: 监控 [!DNL Assets] 部署的最佳实践
description: 部署 [!DNL Adobe Experience Manager] 部署后监视其环境和性能的最佳实践。
contentOwner: AG
role: Admin, Architect
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
exl-id: d2cb447c-69d6-4659-a29e-02af22b543fd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---

# 监控[!DNL Adobe Experience Manager Assets]部署的最佳实践 {#assets-monitoring-best-practices}

从[!DNL Experience Manager Assets]的角度来看，监控应包括观察和报告以下流程和技术：

* 系统CPU
* 系统内存使用
* 系统磁盘IO和IO等待时间
* 系统网络IO
* 栈利用和异步进程（如工作流）的JMX MBean
* OSGi控制台运行状况检查

通常，[!DNL Experience Manager Assets]可以通过两种方式进行监控：实时监控和长期监控。

## 实时监控 {#live-monitoring}

您应在开发的性能测试阶段或高负载情况下执行实时监控，以了解环境的性能特征。 通常，应使用一套工具执行实时监控。 以下是一些建议：

* [Visual VM](https://visualvm.github.io/)： Visual VM允许您查看详细的Java VM信息，包括CPU使用情况、Java内存使用情况。 此外，它还允许您取样并评估在部署中运行的代码。
* [Top](https://man7.org/linux/man-pages/man1/top.1.html)： Top是一个Linux命令，它打开了一个仪表板，显示使用情况统计数据，包括CPU、内存和IO使用情况。 它提供了实例上所发生情况的高级概述。
* [Htop](https://hisham.hm/htop/)： Htop是交互式进程查看器。 除了Top可以提供的内容之外，它还提供了详细的CPU和内存使用率。 可以在大多数Linux系统上使用`yum install htop`或`apt-get install htop`安装Htop。

* Iotop： Iotop是磁盘IO使用情况的详细仪表板。 它显示一些条形和仪表，这些条形和仪表描述了使用磁盘IO的进程及其使用的数量。 可以在大多数Linux系统上使用`yum install iotop`或`apt-get install iotop`安装Iotop。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)： Iftop显示有关以太网/网络使用的详细信息。 Iftop显示使用以太网的实体上每个通信通道的统计信息及其使用的带宽量。 可以在大多数Linux系统上使用`yum install iftop`或`apt-get install iftop`安装Iftop。

* Java Flight Recorder (JFR)：Oracle中的一种商业工具，您可以在非生产环境中自由使用。 有关更多详细信息，请参阅[如何使用Java飞行记录器诊断CQ运行时问题](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)。
* [!DNL Experience Manager] `error.log`文件：您可以调查[!DNL Experience Manager] `error.log`文件以了解系统中记录的错误的详细信息。 使用命令`tail -F quickstart/logs/error.log`识别要调查的错误。
* [工作流控制台](/help/sites-administering/workflows.md)：利用工作流控制台监视滞后或卡住的工作流。

通常，您会同时使用这些工具来全面了解[!DNL Experience Manager]部署的性能。

>[!NOTE]
>
>这些工具是标准工具，Adobe不直接支持它们。 它们不需要额外的许可证。

![chlimage_1-33](assets/chlimage_1-143.png)

*图：使用Visual VM工具进行实时监控。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 长期监测 {#long-term-monitoring}

对[!DNL Experience Manager]部署的长期监控涉及对实时监控的相同部分进行更长时间的监控。 它还包括定义特定于您环境的警报。

### 日志聚合和报告 {#log-aggregation-and-reporting}

有多种工具可用于聚合日志，例如Splunk(TM)和Elastic Search、Logstash和Kabana (ELK)。 要评估[!DNL Experience Manager]部署的正常运行时间，请务必了解特定于系统的日志事件并根据这些事件创建警报。 了解您的开发和运营实践可以帮助您更好地了解如何调整日志聚合过程以生成严重警报。

### 环境监测 {#environment-monitoring}

环境监控包括监控以下内容：

* 网络吞吐量
* 磁盘IO
* 内存
* CPU利用
* JMX MBean
* 外部网站

您需要外部工具(如NewRelic(TM)和AppDynamics(TM))来监视每个项目。 使用这些工具，您可以定义特定于您的系统的警报，例如，高系统利用率、工作流备份、运行状况检查失败或对您网站的未经身份验证的访问。 Adobe不推荐使用任何优于其他工具的工具。 找到适合您的工具，并使用该工具监控讨论的项目。

#### 内部应用程序监控 {#internal-application-monitoring}

内部应用程序监控包括监控构成[!DNL Experience Manager]栈栈的应用程序组件（包括JVM、内容存储库），以及通过基于平台构建的自定义应用程序代码进行监控。 通常，它通过JMX Mbeans执行，可由许多流行的监控解决方案直接监控，如SolarWinds (TM)、HP OpenView (TM)、Hyperic (TM)、Zabbix (TM)等。 对于不支持直接连接到JMX的系统，您可以编写Shell脚本来提取JMX数据，并以这些系统本身能够理解的格式将其公开给这些系统。

默认情况下不启用对JMX Mbean的远程访问。 有关通过JMX进行监视的详细信息，请参阅[使用JMX技术进行监视和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)。

在许多情况下，需要基线来有效地监视统计信息。 要创建基线，请在正常工作条件下观察系统预定时间段，然后识别正常度量。

**JVM监视**

与任何基于Java的应用程序栈栈一样，[!DNL Experience Manager]依赖于通过基础Java虚拟机提供给它的资源。 您可以通过JVM公开的Platform MXBean监控许多这些资源的状态。 有关MXBean的详细信息，请参阅[使用Platform MBean服务器和Platform MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)。

以下是您可以为JVM监视的一些基线参数：

内存

* `MBean: lava.lang:type=Memory`
* URL： `/system/console/jmx/java.lang:type=Memory`
* 实例：所有服务器
* 警报阈值：当栈或非栈内存利用率超过相应最大内存的75%时。
* 警报定义：可能是系统内存不足，或者代码中存在内存泄漏。 分析线程转储以得出定义。

>[!NOTE]
>
>此Bean提供的信息以字节表示。

Threads

* MBean： `java.lang:type=Threading`
* URL： `/system/console/jmx/java.lang:type=Threading`
* 实例：所有服务器
* 警报阈值：当线程数大于基线的150%时。
* 警报定义：要么是一个活动的失控进程，要么是低效的操作占用了大量资源。 分析线程转储以得出定义。

**监视器[!DNL Experience Manager]**

[!DNL Experience Manager]还通过JMX公开一组统计数据和操作。 这些功能有助于评估系统运行状况，并在潜在问题影响用户之前发现它们。 有关详细信息，请参阅[!DNL Experience Manager] JMX MBean上的[文档](/help/sites-administering/jmx-console.md)。

以下是您可以为[!DNL Experience Manager]监视的一些基线参数：

复制代理

* MBean： `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL： `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 实例：一个创作实例和所有发布实例（用于刷新代理）
* 警报阈值：当`QueueBlocked`的值为`true`或`QueueNumEntries`的值大于基线的150%时。

* 警报定义：系统中存在阻塞的队列，指示复制目标已关闭或无法访问。 通常，网络或基础架构问题会导致过多条目排入队列，从而对系统性能产生负面影响。

>[!NOTE]
>
>对于MBean和URL参数，请将`<AGENT_NAME>`替换为您要监视的复制代理的名称。

会话计数器

* MBean： `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL： */system/console/jmx/org.apache.jackrabbit.oak：id=7，name=&quot;OakRepository Statistics&quot;，type*=&quot;RepositoryStats&quot;
* 实例：所有服务器
* 警报阈值：当打开的会话超过基线50%以上时。
* 警报定义：会话可以通过一段代码打开，但永远不会关闭。 随着时间的推移，这种情况可能会慢慢出现，并最终导致系统中内存泄漏。 虽然会话的数量应在系统中波动，但不应持续增加。

运行状况检查

[操作仪表板](/help/sites-administering/operations-dashboard.md#health-reports)中可用的运行状况检查具有用于监视的相应JMX MBean。 但是，您可以编写自定义运行状况检查来公开其他系统统计信息。

以下是一些现成的运行状况检查，这些检查对监控很有帮助：

* 系统检查
   * MBean： `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性以了解有关问题原因的更多信息。

* 复制队列

   * MBean： `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性，了解有关导致问题的队列的更多信息。

* 响应性能

   * MBean： `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 实例：所有服务器
   * 警报持续时间：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性，了解有关导致问题的队列的更多信息。

* 查询性能

   * MBean： `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：一个或多个查询在系统中运行缓慢。 检查日志属性，了解有关导致问题的查询的更多信息。

* 活动包

   * MBean： `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：系统上存在非活动或未解析的OSGi捆绑包。 检查日志属性，以了解有关导致问题的捆绑包的更多信息。

* 日志错误

   * MBean： `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL： `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：日志文件中有错误。 检查日志属性以了解有关问题原因的更多信息。

## 常见问题和解决方法  {#common-issues-and-resolutions}

在监视过程中，如果您遇到问题，可以执行以下一些故障排除任务，以解决[!DNL Experience Manager]部署的常见问题：

* 如果使用TarMK，请经常运行Tar压缩。 有关详细信息，请参阅[维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
* 检查`OutOfMemoryError`日志。 有关详细信息，请参阅[分析内存问题](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=zh-Hans)。

* 检查日志中是否存在对未索引查询、树遍历或索引遍历的任何引用。 这些指示未索引的查询或索引不足的查询。 有关优化查询和索引性能的最佳实践，请参阅[有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。
* 使用工作流控制台验证您的工作流是否按预期执行。 如果可能，将多个工作流合并到单个工作流中。
* 重新访问实时监控，并查找任何特定资源的其他瓶颈或高占用率。
* 调查来自客户端网络的出口点和指向[!DNL Experience Manager]部署网络（包括Dispatcher）的入口点。 这些往往是瓶颈领域。 有关详细信息，请参阅[Assets网络注意事项](/help/assets/assets-network-considerations.md)。
* 扩大[!DNL Experience Manager]服务器的大小。 您的[!DNL Experience Manager]部署可能大小不足。 Adobe客户支持可以帮助您确定您的服务器是否规模过小。
* 在出现错误时检查`access.log`和`error.log`文件中的条目。 查找可能指示自定义代码异常的模式。 将它们添加到您监视的事件列表中。
