---
title: 升级后检查和故障排除
description: 了解如何对升级后可能显示的问题进行故障排除。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8b3d8d0f-10f7-4736-881d-8f1f21c69182
source-git-commit: a037dc7cbb13abfeb8a7289baded50d3d788cbf6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# 升级后检查和故障排除{#post-upgrade-checks-and-troubleshooting}

## 升级后检查 {#post-upgrade-checks}

在[就地升级](/help/sites-deploying/in-place-upgrade.md)后，应执行以下活动以完成升级。 我们假定AEM已使用AEM 6.5 LTS jar启动，并且已部署升级的代码库。

* [验证日志以确认升级成功](#verify-logs-for-upgrade-success)

* [验证OSGi包](#verify-osgi-bundles)

* [验证Oak版本](#verify-oak-version)

* [页面初始验证](#initial-validation-of-pages)

* [验证计划的维护配置](#verify-scheduled-maintenance-configurations)

* [启用复制代理](#enable-replication-agents)

* [启用自定义计划作业](#enable-custom-scheduled-jobs)

* [执行测试计划](#execute-test-plan)


### 验证升级成功的日志 {#verify-logs-for-upgrade-success}

**upgrade.log**

过去，检查实例的升级后状态需要仔细检查各种日志文件、存储库部分和启动板。 生成升级后报告有助于在升级启动前检测有缺陷的升级。

此功能的主要目的在于减少手动解释或跨越多个端点复杂解析逻辑的需要，这些逻辑是确保升级成功所必需的。 该解决方案旨在为外部自动化系统提供明确的信息以在更新的成功或识别失败时做出反应。

更具体地说，它确保：

* 升级框架检测到的升级故障集中存储在一个升级报告中。
* 升级报告包含有关必要手动干预的指标。

为了适应这种情况，已在`upgrade.log`文件中更改生成日志的方式。

**error.log**

在使用Target版本jar启动AEM期间和之后，应该仔细查看error.log。 应审查任何警告或错误。 通常，最好在日志的开头查找问题。 日志中稍后发生的错误实际上可能是文件早期调出的根本原因的副作用。 如果出现重复错误和警告，请参阅下面的[分析升级问题](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)。

### 验证OSGi包 {#verify-osgi-bundles}

导航到OSGi控制台`/system/console/bundles`，并查看是否有任何捆绑包未启动。 如果有任何捆绑包处于已安装状态，请查阅`error.log`以确定根问题。

### 验证Oak版本 {#verify-oak-version}

升级后，您应该会看到Oak版本已更新为&#x200B;**1.68.x**。 要验证Oak版本，请导航到OSGi控制台，并查看与Oak捆绑包关联的版本：Oak Core、Oak Commons、Oak Segment Tar。

### 页面初始验证 {#initial-validation-of-pages}

对AEM中的多个页面执行初始验证。 如果升级创作环境，请打开起始页和欢迎页( `/aem/start.html`， `/libs/cq/core/content/welcome.html`)。 在创作和发布环境中，打开几个应用程序页面并进行冒烟测试，以使其正确呈现。 如果发生任何问题，请查阅`error.log`以进行故障排除。

### 验证计划的维护配置 {#verify-scheduled-maintenance-configurations}

#### 启用数据存储垃圾收集 {#enable-data-store-garbage-collection}

如果使用文件数据存储，请确保已启用数据存储垃圾收集任务并将其添加到每周维护列表。 说明概述在[修订清理](/help/sites-administering/data-store-garbage-collection.md)下。

>[!NOTE]
>
>对于S3自定义数据存储安装或使用共享数据存储时，不建议这样做。

#### 启用联机修订清理 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK区段格式，请确保已启用“修订版清理”任务并将其添加到“每日维护”列表中。 说明概述在[修订清理](/help/sites-deploying/revision-cleanup.md)下。

### 启用复制代理 {#enable-replication-agents}

完全升级并验证发布环境后，在创作环境中启用复制代理。 验证代理是否能够连接到各自的发布实例。 有关事件顺序的更多详细信息，请参阅[升级过程](/help/sites-deploying/upgrade-procedure.md)。

### 启用自定义计划作业 {#enable-custom-scheduled-jobs}

此时可以启用任何作为代码库一部分的计划作业。

### 执行测试计划 {#execute-test-plan}

执行[升级&#x200B;**测试过程**&#x200B;部分](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure)下的代码和自定义项中定义的详细测试计划。

## 分析升级问题 {#analyzing-issues-with-the-upgrade}

本节包含升级到AEM 6.5 LTS的过程中可能会遇到的一些问题场景。

### 包和捆绑包无法更新  {#packages-and-bundles-fail-to-update}

如果在升级期间无法安装包，则也不会更新包中包含的包。 此类问题是由数据存储配置错误导致的。 它们还将在error.log中显示为&#x200B;**ERROR**&#x200B;和&#x200B;**WARN**&#x200B;消息。 由于大多数情况下，默认登录可能无法工作，因此您可以直接使用CRXDE检查并查找配置问题。

### 升级未运行 {#the-upgrade-did-not-run}

在开始准备步骤之前，请确保先运行&#x200B;**源**&#x200B;实例，方法是使用`java -jar aem-quickstart.jar`命令执行该实例。 这是确保正确生成quickstart.properties文件所必需的。 如果缺少该参数，升级将无法工作。 或者，您可以通过查看源实例安装文件夹中的`crx-quickstart/conf`来检查文件是否存在。 此外，在启动AEM以开始升级时，必须使用`java -jar <aem-quickstart-6.5-LTS.jar>`命令执行该升级。 从启动脚本启动时，在升级模式下不会启动AEM。

### 某些AEM捆绑包未切换到活动状态 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果存在未启动的包，请检查是否存在任何未满足的依赖项。

如果出现此问题，但此问题基于失败的软件包安装，从而导致捆绑包无法升级，则系统将认为它们与新版本不兼容。 有关如何解决此问题的更多信息，请参阅上面的&#x200B;**无法更新的包和包**。

此外，还建议将新的AEM 6.5 LTS实例的捆绑包列表与升级后的实例进行比较，以检测未升级的捆绑包。 这将提供在`error.log`中搜索内容的更近范围。

### 自定义捆绑包未切换到活动状态 {#custom-bundles-not-switching-to-the-active-state}

如果您的自定义捆绑包未切换到活动状态，则很可能是因为存在未导入已更改API的代码。 这通常会导致依赖关系得不到满足。

另外，最好检查是否有必要执行导致问题的更改，如果没有，则恢复。 此外，在严格的语义版本控制后，检查资源包导出的版本增加是否超过需要。

### 正在分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多数情况下，需要查阅日志来查找错误原因。 但是，在升级时，由于旧捆绑包可能无法正确升级，因此还需要监视依赖项问题。

最好的方法是删除error.log ，方法是删除所有可能与您遇到的问题无关的消息。 您可以使用以下代码通过grep等工具执行此操作：

```shell
grep -v UnrelatedErrorString
```

某些错误消息可能不会立即说明问题。 在这种情况下，查看发生错误的上下文也有助于了解错误是在何处创建的。 您可以使用以下内容分隔错误：

* 用于在错误之前添加行的`grep -B`；

或

* `grep -A`在之后添加行。

在少数情况下，还可以找到错误WARN消息，因为可能存在导致此状态的有效案例，并且应用程序并不总是能够确定这是否是实际错误。 请务必查阅这些信息。

### 联系 Adobe 支持 {#contacting-adobe-support}

如果您已经查看了此页面上的建议但仍遇到问题，请与Adobe支持部门联系。 要向处理您的案例的支持工程师提供尽可能多的信息，请确保您包含升级中的`error.log`和`upgrade.log`文件。
