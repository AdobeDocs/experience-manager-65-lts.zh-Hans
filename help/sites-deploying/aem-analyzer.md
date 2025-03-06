---
title: 使用AEM Analyzer评估升级复杂性
description: 了解如何使用AEM Analyzer评估升级的复杂性。
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 87c30912-c89a-42f1-b37b-ec439e7318c7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 15%

---

# 使用AEM Analyzer评估升级复杂性 {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## 概述 {#overview}

AEM 6.5 LTS分析器通过指明需要更新的区域来评估您当前的AEM实施，以提供到6.5 LTS的无缝升级体验。

该工具会生成一个报告来标识潜在重构的区域。

## AEM 6.5 LTS分析器报告 {#aem-65lts-analyzer-report}

AEM 6.5 LTS Analyzer报告用于深入了解一般升级准备情况。 该报告包含为了确保成功升级到AEM 6.5 LTS而必须解决的各类问题的发现结果。

AEM 6.5 LTS Analyzer报告包括以下类别：

* 必须重构的应用程序功能
* 必须移至受支持位置的存储库项目
* 配置问题
* 已被新功能删除或AEM 6.5 LTS当前不支持的AEM 6.5功能
* 删除Java和Guava API用法

通过AEM 6.5 LTS分析器报告中的链接，可访问这些类别以及与这些类别相关的可能影响和解决方案的更多信息。

## 可用性 {#analyzer-availability}

可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)以zip文件的形式下载AEM Analyzer。 您可以在源AEM实例上通过[包管理器](/help/sites-administering/package-manager.md)安装包。

## 使用AEM Analyzer的重要注意事项 {#important-considerations-for-using-aem-analyzer}

请阅读以下章节，以了解运行AEM Analyzer时的重要注意事项：

* 分析器报告是使用AEM [模式检测器](/help/sites-deploying/pattern-detector.md)的输出生成的。 Analyzer使用的模式检测器的版本包含在AEM Analyzer安装包中
* AEM Analyzer只能由&#x200B;**管理员**&#x200B;用户或&#x200B;**管理员**&#x200B;组中的用户运行
* 版本6.5及更高版本的AEM实例支持Analyzer。

>[!NOTE]
>
>为避免对业务关键型实例产生影响，建议您在自定义、配置、内容和用户应用程序方面尽可能接近生产环境的暂存环境中运行AEM Analyzer。 或者，也可以在克隆的生产“创作”环境中运行。

* 生成AEM Analyzer报告内容可能需要相当长的时间，从几分钟到几小时不等。 所需的时间在很大程度上取决于AEM存储库内容的大小和性质、AEM版本以及其他因素
* 由于生成报告内容可能需要花费大量时间，因此报告内容将由后台进程生成并保存在缓存中。 查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 查看AEM Analyzer报表 {#viewing-the-aem-analyzer-report}

要查看AEM Analyzer报表，请执行以下步骤：

1. 选择Adobe Experience Manager并导航到&#x200B;**工具 — 操作 — 6.5 LTS现代化器**

   ![查看分析器报告1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. 单击&#x200B;**AEM 6.5 LTS分析器**&#x200B;以将其打开

   ![查看分析器报告2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. 单击&#x200B;**生成报告**&#x200B;以执行AEM Analyzer

   ![查看分析器报告3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. 在AEM Analyzer生成报告时，您可以在屏幕上查看该工具执行的进度。 它按照完成百分比显示进度。 它还会显示分析的项目数和发现结果数

   ![查看分析器报告4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. 生成6.5 LTS分析器报告后，它将以表格形式显示调查结果的摘要和数量，按调查结果类型和重要性级别进行整理。 要获取有关特定发现结果的更多详细信息，您可以单击与表中发现结果类型对应的数字

   ![查看分析器报告5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. 您可以通过单击&#x200B;**导出到CSV**，选择下载逗号分隔值(CSV)格式的报表。 您可以通过单击&#x200B;**刷新报告**，强制Analyzer清除其缓存并重新生成报告。 如果缓存过期，则必须重新生成报告。

## 解释AEM Analyzer报告 {#interpreting-the-aem-analyzer-report}

在AEM实例中运行6.5 LTS分析器工具时，报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：

   * **报告时间**：生成并首次提供报告内容的时间
   * **过期时间**：报告内容缓存过期的时间
   * **生成时间段**：生成报告的时间量
   * **发现结果计数**：报告中包含的发现结果总数

* **系统概述**：有关运行分析器的AEM系统的信息
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

  ![分析器报告摘要](/help/sites-deploying/assets/analyzer-report-summary.png)

  每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

>[!NOTE]
>
>要了解有关每个发现结果类别的更多信息，请参阅[模式检测器类别](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso)。

为了了解重要性级别，请遵循下表：

| 重要性 | 描述 |
|---|---|
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |

## 解释AEM 6.5 LTS分析器CSV报告 {#interpreting-the-aem-65lts-analyzer-report}

当您从AEM实例单击&#x200B;**CSV**&#x200B;选项时，将从内容缓存生成CSV格式的Analyzer报告，并将该报告返回到您的浏览器。 根据您的浏览器设置，此报表将自动下载为默认名称为`report.csv`的文件。

如果缓存已过期，则在生成并下载CSV文件之前会重新生成报表。

CSV 格式的报告包括从模式检测器输出生成的信息，这些信息按类别类型、子类型和重要性级别进行排序和组织。其格式适合在 Microsoft Excel 等应用程序中查看和编辑。它旨在以可重复的格式提供所有发现结果信息，在比较不同时间的报告以衡量进度时，这些信息很有用。

CSV 格式的报告包含以下列：

* **代码**：类别代码
* **类型**：类别名称
* **子类型**：类别子类型
* **重要性**：重要性级别
* **标识符**：发现结果的主要标识符
* **消息**：为发现结果提供的消息
* **上下文**：发现结果数据的 JSON 字符串

单个发现结果的列中的值“`\N`”表示未提供任何数据。

## HTTP接口 {#http-interface}

6.5 LTS分析器提供了一个HTTP接口，可用作AEM中用户界面的替代方法。 该接口同时支持`HEAD`和`GET`命令。 它可用于生成Analyzer报告，并以三种格式之一返回报告：JSON、CSV和制表符分隔值(TSV)。

以下URL可用于HTTP访问，其中`<host>`是安装Analyzer的服务器的主机名以及端口（如果需要）：

* `http://<host>/apps/aem66-analyzer/analysis/report.json`（对于 JSON 格式）
* `http://<host>/apps/aem66-analyzer/analysis/report.csv`（对于 CSV 格式）
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv`（对于 TSV 格式）

### 执行HTTP请求 {#executing-an-http-request}

执行HTTP请求的一种简单方法是，在您已经以管理员身份登录AEM的同一浏览器中打开一个选项卡。 您可以在该浏览器选项卡中输入 URL，并让浏览器显示或下载结果。

您还可以使用命令行工具，如`curl`或`wget`以及任何HTTP客户端应用程序。 如果不将浏览器选项卡用于经过身份验证的会话，则必须在注释中提供管理用户名和密码。

以下是如何实现此操作的示例：

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## 调整缓存生命周期 {#adjusting-the-cache-lifetime}

默认的AEM 6.5 LTS Analyzer缓存生命周期为24小时。 在AEM实例和HTTP界面中都有用于刷新报告和重新生成缓存的选项，此默认值可能适用于AEM 6.5 LTS Analyzer的大多数使用情况。 如果AEM实例的报告生成时间特别长，则可能需要调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为`maxCacheAge`属性存储在以下存储库节点上：

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

## 使用内容转换器 {#using-content-transformer}

### 可用性 {#content-transformer-availability}

Content Transformer与AEM 6.5 LTS Analyzer捆绑在一起，可以从软件分发门户以zip文件的形式下载。

### 使用内容转换器的重要注意事项 {#important-considerations-for-using-content-transformer}

请参阅以下部分，了解使用内容转换器(CT)的重要注意事项：

* 要使用Content Transformer，您必须首先在AEM环境中运行AEM Analyzer
* 虽然您可以在生产环境中运行内容转换器，但建议您在克隆的生产环境中运行内容转换器。 更重要的是，您需要确保AEM Analyzer和CT在同一环境中运行
* 您需要是要运行内容转换器的环境的管理员
* 默认情况下，在进行转换之前，可能会更改源内容的删除操作将在`/etc/packages/modernizer-content-transformation`下创建源路径的备份包。 虽然“删除操作”对话框有禁用/启用备份包创建的选项，但强烈建议始终选择启用包创建
* 内容转换器中的每个页面都配置为最多列出50个查找结果。 因此，一次最多可以转换50个发现。 此操作是为了在UI中提供及时响应。

### 打开内容转换器 {#opening-the-content-transformer}

1. 以管理员身份登录到源AEM实例，然后转到起始页：*https://host:port/aem/start.htm*
1. 导航到&#x200B;**工具 — 操作 — 6.5 LTS现代化器**

   ![打开内容转换器1](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. 单击&#x200B;**Content Transformer for 6.5 LTS Analyzer报告**&#x200B;卡

   ![正在打开内容转换器2](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. 如果未生成Analyzer报告，则&#x200B;**转换内容**&#x200B;页面将显示&#x200B;**无报告**。 如果删除了所有与内容相关的发现，则还会显示同一&#x200B;**无报告**&#x200B;消息

   ![打开内容转换器3](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. 下方是一个示例，说明AEM Analyzer报表创建成功且发现与内容相关问题的情况下内容转换器概述页面的外观。

AEM Analyzer报告的剩余到期时间显示在侧边栏中。 建议使用最新的AEM Analyzer报告运行内容转换器，以避免遗漏任何与内容相关的发现

![打开内容转换器4](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. 您可以根据模式代码、子类型、重要性和Source来过滤问题

   ![打开内容转换器5](/help/sites-deploying/assets/opening-content-transformer-5.png)

### 删除路径 {#removing-paths}

1. 您可以选择所有问题或特定问题，然后选择&#x200B;**删除**&#x200B;以解决这些问题

   ![正在删除路径1](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >默认情况下，在转换之前，删除操作会在`/etc/packages/modernizer-content-transformation`下创建源路径的备份包。 虽然“删除操作”对话框有禁用/启用备份包创建的选项，但强烈建议始终选择启用包创建。

   ![正在删除路径2](/help/sites-deploying/assets/removing-paths-2.png)

1. 下面显示了为路径删除操作创建的备份包的示例。 您可以单击&#x200B;**安装**&#x200B;以恢复源路径

   ![正在删除路径3](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >请勿删除`/etc/packages/modernizer-content-transformation`，因为这是备份包所在的位置。 只有在您确定不再需要这些包时，才能删除此位置以减小存储库大小。

1. （可选）您可以打包选定的内容查找结果以供将来使用。 为此，请选择要包括的调查结果，然后单击左上方的&#x200B;**包**。 输入包名称，选择包路径，然后单击&#x200B;**包**&#x200B;按钮以完成该过程。

   ![正在删除路径3](/help/sites-deploying/assets/removing-paths-4.png)

### 已知问题 {#known-issues}

* 有时，删除操作可能会显示通知：*&quot;某些路径未成功删除，请检查日志并重试。“*”。 但是，如果实际删除了路径，则可以安全地忽略此消息
* 同样，包操作可能会失败，并出现以下错误： *&quot;执行所需操作时出现错误，请检查日志并重试。“*”。 这可能是由于会话过期导致的。 在这种情况下，重试操作应该可以解决此问题。
