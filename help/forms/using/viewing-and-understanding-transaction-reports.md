---
title: 查看和了解事务处理报表
description: 使用交易报告就产品使用情况和重新平衡硬件和软件投资做出明智的决策。
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 761c9946-bf8e-468e-b8f5-36c958d68e90
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# 在OSGi上查看和了解AEM Forms的交易报表{#viewing-and-understanding-transaction-reports}

通过事务报表，您可以捕获和跟踪已提交的表单、已处理的文档和已渲染文档的数量。 跟踪这些交易背后的目标是针对产品使用情况做出明智的决策，并重新平衡硬件和软件投资。 有关详细信息，请参阅[AEM Forms交易报告概述](../../forms/using/transaction-reports-overview.md)。

## 设置事务报表  {#setting-up-transaction-reports}

交易报表功能作为AEM Forms附加组件包的一部分提供。 有关在所有创作实例和发布实例上安装附加组件包的信息，请参阅[安装和配置AEM表单](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安装AEM Forms附加组件包后，请执行以下操作：

* 在所有发布实例上启用反向复制
* 启用交易报表
* 提供查看交易报告的权限
* （可选）配置事务刷新周期和发件箱[&#128279;](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms事务报表不支持仅包含发布实例的拓扑。
>* 在使用事务报告之前，请确保为所有发布实例启用了反向复制。
>* 事务数据将从发布实例反向复制到仅相应的创作或处理实例。 创作或处理实例无法进一步将数据复制到另一个实例。
>

### 在所有发布实例上启用反向复制 {#enable-reverse-replication-on-all-the-publish-instances}

事务报表使用反向复制将事务计数从发布实例合并到创作实例。 在所有发布实例上设置反向复制。 有关设置反向复制的详细说明，请参阅[复制](/help/sites-deploying/replication.md)。

### 启用交易报表 {#enable-transaction-reports}

默认情况下，事务报表处于禁用状态。 您可以从AEM Web控制台启用报表。 要在AEM Forms环境中启用事务报表，请在所有创作实例和发布实例上执行以下步骤：

1. 以管理员身份登录到AEM实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms Transaction Reporting**&#x200B;服务。
1. 选择“记录事务处理”复选框。 单击&#x200B;**保存**。

   对所有创作实例和发布实例重复步骤1-3。

### 提供查看交易报告的权限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator组的成员才能查看事务报告。 要允许用户查看事务报告，请使用户成为fd-administrator组的成员。 有关使用户成为AEM组成员的说明，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### （可选）配置事务刷新时段和发件箱 {#optional-configure-transaction-flush-period-and-outboxes}

事务在存储到存储库中之前，会先缓存在内存中。 此过程可确保不会频繁写入存储库。 默认情况下，缓存周期（事务刷新周期）设置为60秒。 您可以更改默认时间段以适合您的环境。 执行以下步骤以更改默认高速缓存周期：

1. 以管理员身份登录到作者实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务存储库存储提供程序**&#x200B;服务。
1. 在&#x200B;**事务刷新周期**&#x200B;字段中指定秒数。 单击&#x200B;**保存**。

反向复制将事务数据复制到创作实例的默认发件箱。 您可以将交易数据放在自定义发件箱中。 执行以下步骤以指定自定义发件箱：

1. 以管理员身份登录到作者实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务存储库存储提供程序**&#x200B;服务。
1. 在&#x200B;**发件箱**&#x200B;字段中指定自定义发件箱的名称。 单击&#x200B;**保存**。将在所有创作实例上创建一个具有指定名称的发件箱。

## 查看事务处理报表 {#viewing-the-transaction-report}

您可以查看有关创作或发布实例的事务报表。 创作实例上的事务报表提供在配置的创作实例和发布实例上发生的所有事务的总和。 发布实例上的事务报表提供仅在基础发布实例上发生的事务计数。 执行以下步骤以查看报表：

1. 登录到`https://[hostname]:'port'`上的AEM Forms服务器。
1. 导航到&#x200B;**工具** > **Forms**>**查看交易报告**。

## 了解报告 {#understanding-the-report}

AEM Forms显示自配置日期以来的事务报表，如以下摘要报表中所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用&#x200B;**将日期重置为今天**&#x200B;选项重置事务记录。 如果将日期重置为今天，则所有先前的事务记录都将丢失。 在创作实例上重置日期时，此更改不会影响“发布”实例上的事务报表，反之亦然。
* 使用&#x200B;**仅显示发布实例的事务**&#x200B;查看仅在配置的发布实例或发布场上发生的所有事务。
* 使用类别：**Document Processed**、**Documents Rendered**&#x200B;和&#x200B;**Forms Submitted**&#x200B;查看相应的事务。 有关这些类别中记帐的交易类型，请参阅[可记帐交易报告API](../../forms/using/transaction-reports-billable-apis.md)。

## 查看交易记录日志 {#view-transaction-reporting-logs}

交易报告会将报告中显示的所有信息和一些附加信息放置在日志中。 日志中提供的信息对高级用户很有帮助。 例如，日志将事务划分为多个粒度类别，而报告中显示了三个整合的类别。 日志位于`/crx-repository/logs/`目录的`error.log`文件中。 即使未从AEM Web控制台启用事务报表，日志也将可用。

## 相关文章 {#related-articles}

* [适用于OSGi上的AEM Forms的交易报表概述](../../forms/using/transaction-reports-overview.md)
* [OSGi上AEM Forms的交易报告可计费API](../../forms/using/transaction-reports-billable-apis.md)
* [在OSGi上记录AEM Forms的自定义实施交易](/help/forms/using/record-transaction-custom-implementation.md)
