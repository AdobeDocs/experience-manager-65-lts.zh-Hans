---
title: 常见问题解答（FAQ）
description: 有关 AEM 6.5 LTS 的常见问题解答。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 49%

---

# AEM 6.5 LTS 常见问题解答 (FAQ) {#faq}

本页旨在解答有关 AEM 6.5 LTS 的一些常见问题。

## Adobe 为何发布了 AEM 的 6.5 LTS？

Adobe 始终致力于确保所提供的应用程序的安全性和稳定性。AEM 6.5 长期支持为 AEM 6.5 的未来更新发展奠定了基础。特别是，AEM 6.5 LTS 包含对 Oracle Java 17 和 Java 21 的支持，并将成为实现 AEM 新功能和创新的 AEM 分支。

## 我是内部部署客户，如果我不升级到 AEM 6.5 LTS 会怎样？

AEM 6.5 LTS 包含重要的安全性和稳定性更新，包括对 Oracle Java 17 和 Java 21 的支持。Adobe 至少在未来 2 年内将继续支持 AEM 6.5，但建议企业组织现在开始计划升级到 6.5 LTS。

## 如果升级到AEM 6.5 LTS，我现有的自定义和集成是否会受到影响？

虽然 AEM 6.5 LTS 努力保持向后兼容性，但一些旧版功能和工件已被移除。
请务必查看[发行说明](/help/release-notes/release-notes.md#deprecated-and-removed-features)，并使用 [AEM 分析工具](/help/sites-deploying/aem-analyzer.md)评估您的自定义功能和集成受到的影响。

## 我应如何确保顺利过渡到 AEM 6.5 LTS？

为确保顺利过渡，建议您：

* 查看[发行说明](/help/release-notes/release-notes.md)，并进行完整的记录。
* 使用 [AEM 分析工具](/help/sites-deploying/aem-analyzer.md)评估升级的复杂性。
* 为升级过程计划并分配足够的时间和资源。
* 参加 Adobe 支持和启动会议，以获得指导和帮助。

## 什么是AEM 6.5 LTS Service Pack？

AEM 6.5 LTS Service Pack是一个累积更新，它包括自AEM 6.5 LTS首次发布以来对其所做的所有修复和改进。 建议应用最新的Service Pack，以确保您的AEM实例使用最新的功能和安全修补程序进行更新。

## 我当前使用的是AEM 6.5，能否在不升级到AEM 6.5 LTS GA版本的情况下直接升级到AEM 6.5 LTS Service Pack？

能，您可以直接从AEM 6.5升级到任何AEM 6.5 LTS Service Pack。 建议查看[发行说明](/help/release-notes/release-notes.md)和[升级到AEM 6.5 LTS](/help/sites-deploying/upgrade.md)部分。

## 我目前在AEM 6.5 LTS GA中，是否需要更改任何代码才能升级到AEM 6.5 LTS Service Pack？

不需要，您无需进行任何代码更改即可从AEM 6.5 LTS升级到AEM 6.5 LTS Service Pack。 但是，始终建议在将Service Pack应用于生产实例之前，查看[发行说明](/help/release-notes/release-notes.md)并在暂存环境中测试自定义项和集成。

## 我想从新的AEM 6.5 LTS设置着手，是否可以直接从AEM 6.5 LTS Service Pack开始？

是，您可以直接设置新的AEM 6.5 LTS Service Pack，而无需设置AEM 6.5 LTS GA内部版本。 建议查看[发行说明](/help/release-notes/release-notes.md)和[自定义独立安装](/help/sites-deploying/custom-standalone-install.md)部分以了解更多详细信息。
