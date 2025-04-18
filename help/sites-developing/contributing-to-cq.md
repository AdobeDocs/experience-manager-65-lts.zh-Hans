---
title: 为AEM贡献内容
description: AEM的开发遵循大型开源项目中经常使用的成熟方法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 1197dc8e-7fbe-4f74-942b-3aa9fafc07ac
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2642'
ht-degree: 0%

---

# 为AEM贡献内容{#contributing-to-aem}

## 开发方法 {#development-methodology}

AEM的开发遵循大型开源项目中普遍采用的行之有效的方法体系。 AEM技术栈栈中的许多核心元素实际上是作为活动的开源项目来维护的，例如Sling和Jackrabbit，这些项目向Apache Software Foundation做出了贡献。 AEM中体现了这一精神的一个主要方面是，我们鼓励您使用可用的邮件列表和在线论坛与开发团队进行直接交互。

如果您正在为AEM的组件投稿，请像在投稿到开源项目时那样熟悉AEM，并像在打算为此类项目投稿时那样与现有核心团队沟通。

## 所需体验 {#required-experience}

超文本传输协议(HTTP)是我们所做一切的核心。 因此，在向AEM投稿之前，您应该对HTTP有深入的了解，最好是能够自行编写带线程池的多线程HTTP服务器的Java™实现。 您还应该了解HTTP/1.1保持活动状态行为，并且您应该深入了解与JavaScript的服务器/客户端交互，特别是AJAX表示的异步交互样式。

由于页面动态和交互式内容是WM体验的关键，因此您必须对文档对象模型及其用于响应事件的编程操作的潜力有相当深入的了解。 例如，您应该了解实时DOM操作以及在多个浏览器文档上拖放的行为（例如，使用iframe）。

在最高级别上，您应该充分了解：

* [HTTP/1.1协议](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (首选[HTML5](https://html.spec.whatwg.org/))
* 级联样式表
* 可扩展标记语言(XML)
* 异步JavaScript和XML (AJAX)设计模式
* JavaScript对象表示法(JSON)
* 文档对象模型
* 有状态交互和无状态交互
* [统一资源标识符](https://www.ietf.org/rfc/rfc2396.txt)
* 浏览器Cookie
* 和其他现代Web开发概念

Adobe Experience Manager的技术栈栈基于[Apache Felix](https://felix.apache.org/documentation/index.html) OSGI容器和[Apache Sling](https://sling.apache.org/index.html) Web框架，并嵌入基于[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html)的Java™内容存储库([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html))。 请熟悉您打算投稿的区域中使用的这些单独项目以及任何其他开源组件（例如Apache Lucene）。

## 部落知识 {#tribal-knowledge}

某些概念和指导原则深深地植根于以前的日间文化中。 本节列出了一些您应该注意的“深入的DNA嵌入”问题。

### 一切都是内容 {#everything-is-content}

内容不仅包括Web应用程序保留的所有数据。 程序代码、库、脚本、模板、HTML、CSS、图像和各种构件、任何内容及一切都将保留在内容存储库中，并通过包管理器和包共享以包形式导入/导出。

### David模型 {#david-s-model}

在Java™内容存储库中建模内容的方式需要一种与软件行业中用于关系世界数据建模的常规做法完全不同的思维方式。 对于任何内容管理新手来说，JCR方式的基本读数为[David的模型：内容建模指南](https://wiki.apache.org/jackrabbit/DavidsModel)。

### RESTful {#restfulness}

REST方法深深地根植于我们的工作中。 这意味着，除其他外，避免有状态交互，并牢记URI是内容和服务的确定地址。

REST（Representational State Transfer，表示状态转移）是指万维网所基于的软件体系结构样式。 它描述了Web运行的关键要素，因此为如何设计基于Web的软件提供了一套原则。 因此，在设计要在Web上使用的API时，遵循这些“最佳实践”是明智的。

由于REST提供了我们所做许多工作的指导理念，因此您应该认为精通RESTful设计原则至关重要。 一个好的起点是[罗伊·菲尔丁的论文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)。

### Sling请求解析 {#sling-request-resolution}

要了解AEM的一个重要方面是，传入请求如何与内容和应用程序行为相关，内容在内容存储库中的结构方式，以及AEM在何处查找应用程序逻辑来处理请求。 了解Apache [Sling URL分解](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html)，以及它强制执行REST架构样式及其无状态、可缓存和分层系统约束的方式。

要了解Apache Sling的请求解析的关键方面是：请求如何主要映射到内容存储库中的特定资源，请求的其他属性以及这些内容对象的属性如何确定调用哪些应用程序代码来呈现内容，以及/apps中的代码如何覆盖/libs中的代码。

### 快速入门 {#quickstart}

没有第三步：要安装和运行，只需下载并双击快速入门JAR文件即可。 没有第三步。 任何其他可选功能只需要从包共享安装相应的包即可。

小型快速入门：将快速入门JAR文件的大小保持在最小值。 智能地优化使用库，并将可选功能移至包共享。

更快的启动时间：在进行可能影响启动时间的更改时，请确保该更改会缩短启动时间，而不是延长启动时间。

### 精益和平均 {#lean-and-mean}

我们喜欢轻巧、小巧、快速和优雅的代码和项目。 “足够好”还不够好。

代码重用：我们基于OSGi的产品架构和“一切都是内容”的理念意味着我们有异常好的机会重用代码和工件。 我们尽量利用这一事实，使功能保持精简而平滑。

松散耦合：我们偏好松散耦合的交互，而非紧密依赖和“不需要的亲密关系”。 松散耦合还支持更多的代码重用。

### 不要破坏演示 {#don-t-break-the-demo}

熟悉演示中最常在演示中显示的演示脚本和产品功能。 了解您所做的任何操作都不会中断“演示脚本”功能。 核心产品应始终为演示做好准备，即使在开发过程中也是如此。

### 可靠性设计 {#design-for-reliability}

我们致力于以失效软方式设计和代码功能，以便（例如）单个DOM元素的问题不会导致整个页面无法呈现。 换句话说，就是让那些本应是致命的，致命的东西。 让其他的一切都活下来。 让产品“原谅”

### 异常是新常态 {#abnormal-is-the-new-normal}

不要依赖关闭挂接，确保在启动时进行清理。 异常终止是正常终止。

`shutdown == kill -9 == power outage`

### 为弹性群集做好准备 {#be-ready-for-elastic-clustering}

始终为弹性聚类做好准备；始终假定存在聚类。 通常，遵守内容存储库中的所有内容意味着内置群集支持。

### 向后兼容性设计 {#design-for-backward-compatibility}

您所做的任何操作都不应破坏客户的旧代码。 只考虑`/libs`包含升级期间可以更新的产品代码。 存储库的`/apps`部分为项目代码，`/etc`部分包含必须保留的自定义配置。 通常，不覆盖`/apps`、`/content`和`/home`中的任何内容。 升级后，旧的项目代码、配置和内容应继续像升级前那样运行。

为向后兼容性而设计还可确保升级体验与初始安装的简单性相匹配。 只需停止AEM、替换快速入门JAR文件并再次启动AEM即可。 随着客户群的快速增长，升级效率是一项越来越显着的优势。

虽然在更新的、更好的功能取代了现有API时，现有API可以也应该标记为已弃用，但是在之前的5.x版本中发布的所有API都需要保持功能，因为它们可能在自定义应用程序代码中使用。 不应删除任何此类API。

在内容结构和用户体验的一般一致性方面，还应牢记向后兼容性。

## 核心概念 {#core-concepts}

**创作实例** — 通常，出于安全、管理和其他原因，生产站点会将AEM的实例分为创作实例和发布实例。 有关部署架构（包括创作/发布实例）的更多信息，请参阅有关AEM实例的文档。

**缓存、煎炸和烘烤** — 传统上，烘烤和煎炸的概念是不同的Web内容管理系统之间的重要区别。 在CMS行话中，“烘烤”是指在发布时将数据提交到静态文件的概念，而“烘烤”是指在请求时处理数据以最终呈现（即在即及时）的概念。

**群集和负载平衡** — 为了提高可用性并改善生产环境的性能，通常将多个创作和/或发布实例（合并到群集中）组合在一起，方法是将这些实例提供给不同的用户组使用，或在Dispatcher配置之后对其进行负载平衡。

也可以合并内容存储库的多个实例以创建&#x200B;*高可用性* JCR解决方案，然后该解决方案可与您的AEM解决方案集成，以最大程度地防止硬件和软件故障。 有关详细信息，请参阅[建议的部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter)。

**组件** — 在AEM中，组件是一种对象类型，通常可以通过从Sidekick中拖放组件来创建该对象的实例。 例如，AEM附带的现成组件包括文本、标题、Tag Cloud、轮播、图像和列表组件，所有这些组件在运行时都可以从Sidekick中使用。

**内容查找器** — 在创作模式下，“内容查找器”是页面左侧的一个特殊面板（框架），它根据您在顶部选择的选项卡显示图像、文档、Flash资源、页面、段落或存储库资源的列表，您可以将这些资源从“内容查找器”拖放到您正在处理的页面（右侧）中。

**数字资源** — 在AEM中，数字Assets是（通常）图像和富媒体文件。 有关更多信息，请参阅在DAM中使用Digital Assets 。

**Dispatcher** - Dispatcher既是缓存工具，又是负载平衡工具，它提供了某些安全保护措施。

**ExtJS小组件** - AEM中的大多数用户界面元素都使用ExtJS，它是使用JavaScript编写的第三方小组件库。 ExtJS具有高性能、可自定义的UI小组件以及设计良好且可扩展的组件模型。

**JCR，Java™内容存储库** - Java™内容存储库规范(JSR-283)提供了抽象数据模型和应用程序编程接口，用于实现结合了文件系统和对象数据库功能的大规模可扩展NoSQL数据存储库。 您无需详尽了解JSR-283，但应花时间熟悉JCR的基本功能及其支持的数据模型，因为JCR才可能实现AEM的“一切都是内容”理念。

实质上，JCR是一个由节点和属性组成的系统，其中节点可以从其他节点继承，并且所有内容都作为属性&#x200B;*值*&#x200B;存储。 请注意，除了普通继承之外，JCR还允许使用“mixin”节点的概念，从而启用多个继承的建模。

JCR具有多种预定义的节点类型和属性类型，但通常打字系统比较灵活，而且（事实上） JCR的优点之一就是它允许同等轻松地存储/管理结构化和非结构化内容。 也就是说，JCR可以适应高度结构化的数据，但它也可以适应任意的动态数据结构，而无需架构约束。

适用于JCR的Java™ API的JavaDoc可从[Apache Software Foundation - JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)获得。

在尝试读取JavaDoc或JCR规范本身之前，您可能需要查看由Adobe Experience Services实现的JCR的[此高级说明](/help/sites-developing/the-basics.md#java-content-repository)。

**多站点管理器(MSM)** - AEM的MSM功能可帮助客户处理多语言和跨国内容，使他们能够在集中式品牌推广与本地化内容之间取得平衡。

**OSGi** - OSGi是基于服务的运行时技术，为AEM中的模块化Java™开发提供了基础。 它是一个框架，不仅为代码资源（称为捆绑包）提供高度动态（且安全）的类加载和执行环境，而且可以完全控制捆绑包所公开的各种服务的可见性和生命周期。 服务注册表提供了捆绑包的协作模型，该模型将生命周期动态（和版本要求）考虑在内。 OSGi解决了许多应用程序服务器要解决的问题，但它是以一种轻量级、高度动态的方式解决的，这使得热部署服务（使新代码立即可用，而无需重新启动服务器）等成为可能。

**Parsys，段落系统** — 段落系统(parsys)是一个复合组件，它允许作者向页面添加不同类型的组件，并包含其他段落组件。 每个段落类型都表示为一个组件。 段落系统本身也是一个组件，它包含其他段落组件。

**微内核** — 存储库中的每个工作区都可以单独配置为通过特定的微内核（管理数据的读取和写入的类）存储其数据。 同样，也可以单独配置存储库范围的版本存储以使用特定的微内核。 有几种不同的微内核可用，能够以各种文件格式或关系数据库存储数据。 (例如，有MongoDB、DB2®或Oracle的持久性管理器) AEM的默认微内核是TarMK（请参阅下面的进一步说明）。

**发布实例** — 出于安全、管理和其他原因，生产站点通常会将AEM的实例划分为创作实例和发布实例。 有关部署架构（包括创作/发布实例）的更多信息，请参阅有关AEM实例的文档。

**快速入门** — 与许多其他程序不同，您使用单个“快速入门”自解压JAR文件来安装AEM。 第一次双击JAR文件时，将自动安装所需的一切。 快速入门JAR包括CRX存储库（包括管理设施）、虚拟存储库服务、索引和搜索服务、工作流服务、安全性和Web服务器，以及CQ Servlet引擎(CQSE)和所有AEM服务所需的所有文件。 没有要安装的其他文件：快速入门是独立的。

首次启动快速入门时，会在后台创建一个整个JCR兼容存储库，这可能需要几分钟的时间。 初次启动后，后续启动会更加迅速，因为存储库基础架构已经建立。

可以通过适当重命名快速入门文件来控制许多启动选项(例如活动端口号、相关AEM实例是否应为“发布”实例或“创作”实例；等等)。 要查看这方面的选项列表，请在命令行中使用“ — help”运行JAR：

```shell
java -jar <quickstartfilename>.jar -help
```

**复制代理** — 复制代理在AEM中占有核心地位，作为用于将内容从创作环境发布（激活）到发布环境的机制；从Dispatcher缓存中刷新内容；将用户生成的内容（例如表单输入）从发布环境返回到创作环境。

**基架** — 使用基架，您可以创建一个表单（基架），其中的字段反映您希望用于页面的结构，然后使用此表单轻松地基于此结构创建页面。

**分段** — 网站访客访问网站时具有不同的兴趣和目标。 了解访客的目标并满足他们的期望是在线营销取得成功的重要先决条件。 分段可通过分析和描述访客的详细信息来帮助实现此目标。

**Sidekick** - Sidekick是一个与面板类似的浮动窗口，显示在可编辑页面上，可以从其中拖动新组件并执行应用于该页面的操作。

**Site Catalyst** - SiteCatalyst为营销人员提供了一个跨多个营销渠道测量、分析和优化所有在线计划的集成数据的位置。 您可以使用Adobe SiteCatalyst分析来自AEM网站的数据。

**Tar存储(TarMK)** - TarMK是AEM中的默认持久性系统。 虽然AEM可以配置为使用其他持久性系统（例如MongoDB），但TarMK具有某些优势，即它针对典型JCR用例进行了性能优化（因此非常快速），使用行业标准数据格式，并且可以快速轻松地备份。

**Template** — 在AEM中，Template指定特定类型的页面。 它定义页面的结构（通常还会指定缩略图图像以及各种属性）。 例如，您可以为产品页面、站点地图和联系人信息使用单独的模板。

**工作流** - AEM工作流系统允许创建涉及页面或资产的自动化进程。
