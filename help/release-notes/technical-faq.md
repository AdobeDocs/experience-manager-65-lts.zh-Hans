---
title: 技术常见问题解答(FAQ)
description: 有关AEM 6.5 LTS的常见技术问题。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: ec722773ce3acff1d0de861523db8ff7df552c4b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# AEM 6.5 LTS技术常见问题解答 {#technical-faq}

本页旨在解答一些有关AEM 6.5 LTS的常见技术问题。

## 技术常见问题解答

### `/systemalive`端点在AEM 6.5 LTS中不再可用。

配置为提供`/systemalive`端点的Felix System Ready捆绑包已弃用，并被Apache Felix运行状况检查所取代。 AEM 6.5 LTS中不再包含此捆绑包。

新的运行状况检查端点在`/system/health`上可用，并使用Apache Felix运行状况检查实现。

有关Felix运行状况检查框架的详细文档，请参阅[felix文档](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy控制台支持

由于缺少Guava依赖项，AEM 6.5中使用的AEM Groovy控制台版本可能无法在AEM 6.5 LTS中使用。 新支持的AEM Groovy控制台版本是[19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8)。

### AEM 6.5 LTS是否支持用户同步？

是的，AEM 6.5 LTS支持用户同步。 AEM 6.5和6.5 LTS之间的用户同步功能没有变化。

### Maven Central上的Uber JAR似乎已损坏 — 出现什么问题？

验证您是否正在将Uber JAR与`apis`分类器一起使用。 请注意，Uber JAR的打包结构在AEM 6.5 LTS中已更改。 有关详细信息，请参阅[更新AEM Uber Jar版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

## 获取其他帮助

如果您遇到此处未涵盖的问题：
* 查看[发行说明](/help/release-notes/release-notes.md)中的已知问题。
* 如需帮助，请与 Adobe 支持部门联系。
