---
title: AEM Forms简介
description: 使用此 AEM 6.5 LTS 指南创建、管理、发布和更新数字表单。查找有关安装、升级和配置数字表单的帮助，并了解如何创作自适应表单。
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: e9549ac9-0ada-4661-969a-709f0ed3b133
source-git-commit: d9f6415aabcbc55af23824d9e0ab33c418f6761f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM Forms简介{#introduction-to-aem-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

有关AEM Forms中最新功能和增强功能的信息，请参阅[AEM Forms中的新增功能](../../forms/using/whats-new.md)。

## 关于AEM Forms {#about-aem-forms}

Adobe Experience Manager (AEM)提供了一个易于使用的解决方案，用于创建、管理、发布和更新复杂的数字表单，同时与后端流程、业务规则和数据集成。

AEM Forms将表单创作、管理和发布与通信管理功能、文档安全和集成分析结合使用，以创建引人入胜的端到端体验。 AEM Forms旨在跨Web和移动渠道工作，它可以高效地集成到您的业务流程中，在提高效率的同时减少纸面流程和错误。

在大型企业中，通常只创建表单一次，之后通过将它复制到内容管理系统中来进行重用。保持表单的大型数据库处于最新状态并使它们成为可发现的表单是一项巨大的挑战。 AEM提供了一个可自定义的Forms门户，确保客户能够跨Web和移动渠道查找和访问所需的表单。

AEM Forms提供了表单管理工具，不仅允许您管理自适应表单，还可管理XFA表单、PDF forms和相关资源。 有关详细信息，请参阅[管理表单简介](../../forms/using/introduction-managing-forms.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](/help/sites-deploying/deploy.md)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

![AEM表单功能](do-not-localize/4th-draft-updated.gif)

### 主要功能 {#key-capabilities}

总之，AEM Forms提供了强大的表单管理功能（如以下功能），可减少手动流程并提高客户满意度。

* 用于设计和部署动态表单(包括PDF、HTML5和自适应表单)的集中式Forms Portal
* 易于使用的图形用户界面，可让企业用户轻松导入、管理、预览和发布表单
* 响应式表单目录，具有使用关键字、标记和元数据的强大搜索功能
* 动态检测用户的设备和位置，以在Web和移动渠道中正确呈现表单
* 与Adobe Analytics集成以有效衡量表单使用量度
* 与Adobe Document Cloud eSign服务集成，或用涂鸦方式以电子方式签署包含机密信息的文档
* 自动化表单发布功能，以及通过多个渠道提供及时、个性化且一致的通信的能力

## AEM表单类型 {#aem-form-types}

AEM Forms允许您扩展新表单和现有表单，以创建：

* 像素完美、分页的HTML和PDF forms，外观几乎类似于纸张，或者
* 自动呈现用户设备和浏览器的自适应表单。

**PDF forms**

PDF forms可以离线填写、本地保存以及在下次在线时发送表单数据。 您可以使用2D条形码来捕获表单数据，并使用数字签名来验证用户的真实性。

**HTML表单**

可以在移动设备和桌面浏览器中查看基于HTML5浏览器的表单。 您可以使用Scribble或eSign服务以电子方式对HTML表单进行签名。

**自适应表单**

自适应表单可以根据需要添加或删除字段或部分，动态地适应用户响应。 通过AEM，可重用Adobe XML表单模板创建自适应表单。

### 支持的功能 {#supported-features}

所有表单类型都支持以下功能：

* 动态布局
* 表单字段验证
* 上下文相关帮助
* 脚本和XML数据处理
* 辅助功能设计和检查
* 能够在服务器端保存表单
* 支持文件附件
* 与用于数据捕获的HTML Workspace集成

## 离线数据收集 {#offline-data-collection}

在提交表单数据后，Adobe Experience Manager会将表单数据与现有系统、业务规则以及所需人员连接起来。

AEM Forms提供了Forms Workspace，它是一种移动应用程序，可将您的数字业务流程扩展到移动设备。 使用Forms Workspace，您可以收集并记录数据，即使离线也是如此。 Forms Workspace使用移动设备的功能，允许您捕获照片、视频并收集数据（如时间戳和其他信息）。 下次连接到网络时，可以同步收集的数据。

离线捕获数据并在下次联机时对其进行同步对现场人员尤其有用。 它提高了生产效率，减少了错误。

**使用Forms Workspace进行离线数据收集的优势**

* 易于使用的HTML Workspace应用程序用于任务分配和跟踪
* 拖放工作流设计环境
* 企业内容管理连接器(ECM)
* 开放式标准支持，包括用于连接表单数据与企业系统的XML和SOAP
* 现成的HTML报告可监控积压、工作队列和关键绩效指标(KPI)
* 可自定义的仪表板，用于实时insight进入业务运营
* 用于连接第三方报告工具的API

![第三份草稿](do-not-localize/3rd-draft.gif)

## 个性化通信 {#personalized-communication}

高效自助服务数字体验的一个重要组成部分是，及时传达用户可以在任意位置通过任意设备访问的个性化信息。个性化和及时的通信可以提高转化率和用户满意度。

借助AEM Forms，企业用户可通过自定义文档模板、合并来自后端流程的信息以及包含交互式组件来创建引人注目的个性化用户体验。 直观的用户界面帮助非技术用户开发业务规则，该业务规则决定何时基于查询生成通信，或启动用户生成的响应。

个性化的文档（如收据、欢迎套件和报表）可以轻松地跨多个渠道交付。 组织可以将流量引入个性化的 Web 门户，从而让受众注册或购买额外的服务。

**主要功能**

* 通信创作环境，支持模板、内容块、业务规则等
* 文档转换和组装
* 支持通过多个渠道（包括Web、电子邮件和纸张）按需或批量文档交付
* 具有更改历史记录的审核跟踪
* 支持数字签名以验证内容完整性和签名者的身份
* AEM Forms的Document Security附加产品，包括加密、使用策略、跟踪和审核

![布局二](do-not-localize/layout-02.png)

简化的个性化通信工作流
