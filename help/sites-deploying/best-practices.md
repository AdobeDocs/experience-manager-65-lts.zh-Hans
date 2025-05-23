---
title: 部署最佳实践
description: 了解如何以尽可能高效和最有效的方式部署和维护Adobe Experience Manager (AEM)。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 4f830ee9-e0e3-48df-b67d-709258cb1991
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 5%

---

# 部署最佳实践{#deploying-best-practices}

部署最佳实践描述如何以尽可能高效和最有效的方式部署或维护Adobe Experience Manager (AEM)。 这一不断增加的主题列表包括AEM中的各个领域。

以下领域提供了有关部署和维护最佳实践和建议的文档：

* [Oak](#oak)
* [UI](#ui)
* [性能](#performance)

有关管理、开发或创作的最佳实践，请参阅以下内容之一：

* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [制定最佳实践](/help/sites-developing/best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)

下面的表格中介绍了特定文档并将其链接到该文档。

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md)是一个可扩展且性能优异的分层内容存储库，它是AEM的基础。

<table>
 <tbody>
  <tr>
   <td><p>可扩展性、性能和灾难恢复</p> </td>
   <td><a href="/help/sites-deploying/performance.md">性能和可扩展性</a></td>
   <td>提供一份白皮书，讨论技术灵活性、高性能和良好的灾难恢复功能</td>
  </tr>
  <tr>
   <td>建议的Oak部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建议的部署</a></td>
   <td>描述部署方案</td>
  </tr>
  <tr>
   <td>Mongo拓扑</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓扑最佳实践</a></td>
   <td>描述mongo拓扑 — 何时使用哪个拓扑。</td>
  </tr>
  <tr>
   <td>数据存储选项</td>
   <td><a href="/help/sites-deploying/data-store-config.md">配置节点和数据存储</a></td>
   <td>本文档介绍了有关存储二进制数据和内容节点的最佳实践。 包含有关使用Amazon S3数据存储的信息。</td>
  </tr>
  <tr>
   <td>在Oak中搜索</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查询和索引的最佳实践</a><br /> </td>
   <td>描述有关如何为内容编制索引的最佳实践。</td>
  </tr>
 </tbody>
</table>

## UI {#ui}

AEM当前在同一版本中有两个UI：经典用户界面和触屏优化用户界面。 因此，客户必须在项目实施期间决定使用哪种。 本文档旨在帮助查找正确的选择。

## 性能 {#performance}

此处列出了有关性能的最佳实践：

<table>
 <tbody>
  <tr>
   <td>Assurance质量最佳实践</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Assurance质量最佳实践</a></td>
   <td>对在<em>publish</em>环境中定义测试概念时涉及的问题的标准化概述。 这主要是QA工程师、项目经理和系统管理员的兴趣。</td>
  </tr>
  <tr>
   <td>将 Dispatcher 与 CDN 结合使用</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans#using-dispatcher-with-a-cdn">将 Dispatcher 与 CDN 结合使用</a></td>
   <td>内容交付网络(CDN)(如Akamai Edge Delivery或Amazon Cloud Front)从距离最终用户较近的位置交付内容。</td>
  </tr>
  <tr>
   <td>性能优化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">性能优化</a></td>
   <td>关键问题是网站响应访客请求所用的时间。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">性能测试的最佳实践</a></td>
   <td>描述在AEM部署上运行性能测试的最佳实践。<br /> </td>
  </tr>
 </tbody>
</table>
