---
title: 常见问题解答（FAQ）
description: 有关 AEM 6.5 LTS 的常见问题解答。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: ht
source-wordcount: '513'
ht-degree: 100%

---

# AEM 6.5 LTS 常见问题解答（FAQ） {#faq}

本页旨在解答有关 AEM 6.5 LTS 的一些常见问题。

## Adobe 为何发布了 AEM 的 6.5 LTS？

Adobe 始终致力于确保所提供的应用程序的安全性和稳定性。AEM 6.5 长期支持为 AEM 6.5 的未来更新发展奠定了基础。特别是，AEM 6.5 LTS 包含对 Oracle Java 17 和 Java 21 的支持，并将成为实现 AEM 新功能和创新的 AEM 分支。

## 我是内部部署客户，如果我不升级到 AEM 6.5 LTS 会怎样？

AEM 6.5 LTS 包含重要的安全性和稳定性更新，包括对 Oracle Java 17 和 Java 21 的支持。Adobe 至少在未来 2 年内将继续支持 AEM 6.5，但建议企业组织现在开始计划升级到 6.5 LTS。

## 如果升级到 AEM 6.5 LTS，我现有的自定义功能和集成会受到影响吗？

虽然 AEM 6.5 LTS 努力保持向后兼容性，但一些旧版功能和工件已被移除。
请务必查看[发行说明](/help/release-notes/release-notes.md#deprecated-and-removed-features)，并使用 [AEM 分析工具](/help/sites-deploying/aem-analyzer.md)评估您的自定义功能和集成受到的影响。

## 我应如何确保顺利过渡到 AEM 6.5 LTS？

为确保顺利过渡，建议您：

* 查看[发行说明](/help/release-notes/release-notes.md)，并进行完整的记录。
* 使用 [AEM 分析工具](/help/sites-deploying/aem-analyzer.md)评估升级的复杂性。
* 为升级过程计划并分配足够的时间和资源。
* 参加 Adobe 支持和启动会议，以获得指导和帮助。

## 什么是 AEM 6.5 LTS 服务包？

AEM 6.5 LTS 服务包是累积更新，包含自 AEM 6.5 LTS 首次发布以来所做的所有修复和改进。建议应用最新的服务包，以确保您的 AEM 实例具有最新的功能和安全补丁。

## 我目前使用的是 AEM 6.5，可以直接升级到 AEM 6.5 LTS 服务包，而无需升级到 AEM 6.5 LTS GA 版本吗？

是的，您可以直接从 AEM 6.5 升级到任何 AEM 6.5 LTS 服务包。建议查看[发行说明](/help/release-notes/release-notes.md)和[升级到 AEM 6.5 LTS](/help/sites-deploying/upgrade.md) 部分。

## 我目前使用的是 AEM 6.5 LTS GA，是否需要进行任何代码更改才能升级到 AEM 6.5 LTS 服务包？

不用，您不需要进行任何代码更改即可从 AEM 6.5 LTS 升级到 AEM 6.5 LTS 服务包。不过，我们始终建议在将服务包应用到生产实例之前先查看[发行说明](/help/release-notes/release-notes.md)，并在暂存环境中测试您的自定义和集成。

## 我想重新开始使用新的 AEM 6.5 LTS 设置，可以直接从 AEM 6.5 LTS 服务包开始吗？

可以，您可以直接设置新的 AEM 6.5 LTS 服务包，而无需设置 AEM 6.5 LTS GA 版本。建议查看[发行说明](/help/release-notes/release-notes.md)和[自定义独立安装](/help/sites-deploying/custom-standalone-install.md)部分以了解更多详细信息。
