---
title: 排查复制问题
description: 本文介绍了如何解决复制问题。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 015def31-c7de-42b3-8218-1284afcb6921
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 排查复制问题{#troubleshooting-replication}

本页提供有关如何解决复制问题的信息。

## 问题 {#problem}

由于某种原因，复制（非反向复制）失败。

## 解决方法 {#resolution}

复制失败的原因有很多。 本文解释了分析这些问题时可能需要采用的方法。

**单击“激活”按钮时是否触发复制？ 如果NOT，则执行以下操作：**

1. 前往/crx/de/index.jsp并以管理员身份登录。
1. 查看节点/bin/replicate或/bin/replicate.json是否存在。 如果该节点存在，则将其删除并保存。

**复制是否在复制代理队列中排队？**

请转到/etc/replication/agents.author.html检查此项，然后单击要检查的复制代理。

**如果一个代理队列或几个代理队列卡住：**

1. 队列是否显示&#x200B;**已阻止**&#x200B;状态？ 如果是这样，发布实例是否未运行或无响应？ 检查发布实例以查看它哪里有问题。 即，检查日志，并查看是否存在OutOfMemory错误或某些其他问题。 如果只是速度较慢，则进行线程转储并分析它们。
1. 队列状态是否显示&#x200B;**队列处于活动状态 — # pending**？ 基本上，复制作业可能会卡在等待发布实例或Dispatcher响应的套接字读取中。 这可能意味着发布实例或Dispatcher处于高负载下或卡在锁中。 在本例中，从作者处进行线程转储并发布。

   * 在线程转储分析器中打开来自作者的线程转储，检查它是否显示复制代理的sling事件作业卡在socketRead中。
   * 在线程转储分析器中从发布中打开线程转储，分析可能导致发布实例不响应的原因。 您应该会看到其名称中带有POST /bin/receive的线程，该线程是从作者接收复制的线程。

**如果所有代理队列卡住**

1. 可能由于存储库损坏或某些其他问题，无法在/var/replication/data下序列化特定内容。 查看logs/error.log以了解相关错误。 要清除错误的复制项目，请执行以下操作：

   1. 前往https://&lt;host>：&lt;port>/crx/de并以管理员用户身份登录。
   1. 单击顶部菜单中的“工具”。
   1. 单击放大镜按钮。
   1. 选择“XPath”作为“类型”。
   1. 在“查询”框中，输入此查询/jcr：root/var/eventing/jobs//element(&#42;，slingevent：Job) order by @slingevent：created
   1. 单击“搜索”。
   1. 在结果中，排名最前的项目是最新的Sling事件作业。 单击每个，然后查找与队列顶部显示的内容匹配的停滞复制。

**创建复制.log**

有时，将所有复制日志记录设置为在DEBUG级别添加到单独的日志文件中会很有帮助。 要执行此操作：

1. 前往https://host:port/system/console/configMgr并以管理员身份登录。
1. 查找Apache Sling日志记录器配置，并通过单击工厂配置右侧的&#x200B;**+**&#x200B;按钮创建实例。 这将创建新的日志记录器。
1. 设置配置，如下所示：

   * 日志级别： DEBUG
   * 日志文件：logs/replication.log
   * 记录器：com.day.cq.replication

1. 如果您怀疑该问题与任何方式的Sling事件/作业相关，则还可以将此Java™包添加到类别：org.apache.sling.event下

## 暂停复制代理队列  {#pausing-replication-agent-queue}

有时，暂停复制队列以减小创作系统上的负载而不禁用它可能是合适的。 目前，只有通过暂时配置无效端口的黑客攻击才能实现此目的。 从5.4开始，您可能会在复制代理队列中看到暂停按钮，该按钮有一些限制

1. 状态不会持续存在，这意味着如果重新启动服务器或复制捆绑包被回收，它将恢复到运行状态。
1. 暂停空闲的时间较短（在没有其他线程进行复制的活动后为OOB 1小时），不会持续较长时间。 因为Sling中有一个避免空闲线程的功能。 基本检查作业队列线程是否已经长时间未使用，如果是，它会启动清理周期。 由于清理周期，它会停止线程，因此暂停的设置丢失。 由于作业是持久性的，因此它会启动一个新线程来处理没有暂停配置详细信息的队列。 由于此队列变为运行状态。

## 用户激活时不会复制页面权限 {#page-permissions-are-not-replicated-on-user-activation}

不会复制页面权限，因为它们存储在授予访问权限的节点下，而不是用户中。

通常，页面权限不应从创作复制到发布，默认情况下也不应复制。 这是因为在这两个环境中，访问权限应该不同。 因此，Adobe建议您在发布时配置ACL，与创作分开。

## 将命名空间信息从创作复制到发布时阻止复制队列 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

有时，在尝试将命名空间信息从创作实例复制到发布实例时，复制队列会被阻止。 发生此情况是因为复制用户没有`jcr:namespaceManagement`权限。 要避免出现此问题，请确保：

* 发布实例上也存在复制用户（在[传输](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)选项卡>用户下配置）。
* 用户在安装内容的路径上拥有读写权限。
* 用户在存储库级别具有`jcr:namespaceManagement`权限。 您可以按如下方式授予权限：

1. 以管理员身份登录到CRX/DE ( `https://localhost:4502/crx/de/index.jsp`)。
1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 选择&#x200B;**存储库**。
1. 单击&#x200B;**添加条目**（加号图标）。
1. 输入用户的名称。
1. 从权限列表中选择`jcr:namespaceManagement`。
1. 单击&#x200B;**确定**。
