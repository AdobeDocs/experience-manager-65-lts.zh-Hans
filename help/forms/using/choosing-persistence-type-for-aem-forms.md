---
title: 为AEM Forms安装选择持久性类型
description: 明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 8ddfc767-08a5-4045-86a7-97150e028a14
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# 为AEM Forms安装选择持久性类型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。

持久性是在物理存储上存储内容的方法。 它定义了数据的实际数据结构和存储机制。 MicroKernels在AEM Forms中充当持久性管理器。 AEM Forms支持TarMK、MongoMK和RDBMK类型的持久性（微内核）。 您可以根据AEM Forms实例的用途和部署类型（单服务器、场或群集），为AEM Forms选择持久性类型。

>[!NOTE]
>
>LiveCycle ES4 SP1使用TarPM持久性存储内容。

下表列出了所有支持的持久性类型以及各种参数，可帮助您选择环境的持久性类型：

<table>
 <tbody>
  <tr>
   <th><strong>安装类型/成本</strong></th>
   <th><strong>tarmk</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>独立设置</strong></th>
   <td>支持<br /> </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>群集设置</strong></th>
   <td>不支持</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>许可成本</strong></th>
   <td>包含在AEM中 </td>
   <td>需要单独的许可证</td>
   <td>需要单独的许可证</td>
  </tr>
 </tbody>
</table>

TarMK旨在提高性能，而MongoMK和RDBMK旨在实现可扩展性。 Adobe强烈建议将TarMK作为所有AEM Forms部署方案（对于Author和Publish实例）的默认持久性技术，但[选择Mongo或关系数据库微内核而非TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)部分中概述的使用情况除外。

有关受支持的微内核列表，请参阅OSGi技术要求上的[AEM Forms](/help/sites-deploying/technical-requirements.md) <!--or [AEM Forms on JEE supported platform combinations](/help/forms/using/aem-forms-jee-supported-platforms.md) articles-->。

## 在TarMK上选择Mongo或关系数据库微内核 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可扩展（集群）AEM Forms环境是由两个或多个水平配置的活动创作实例组成的集合。 如果支持所有并发创作活动的单个服务器不再可持续，您可以选择运行多个创作实例。

<!--Only MongoMK and RDBMK persistence type are supported for a scalable (clustered) AEM Forms on JEE environment.-->

服务器的数量或可扩展环境的大小因每次安装而异。 有关注意事项和示例的列表，请参阅[推荐的部署](/help/sites-deploying/recommended-deploys.md)和/或[AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)文章。 您还可以联系AEM Forms支持，以获取有关使用RDBMK和TarMK的AEM Forms容量规划的详细信息。
