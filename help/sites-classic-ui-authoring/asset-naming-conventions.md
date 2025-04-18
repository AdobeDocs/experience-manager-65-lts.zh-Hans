---
title: 资产测试的命名约定
description: 存储库中的节点遵循Java内容存储库的命名约定。 但是，Adobe Experience Manager对资源节点的名称实施了进一步的约定。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 37de1a8b-b7db-469e-98a7-20ddb6218510
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 1%

---

# 资产测试的命名约定{#naming-conventions-for-assets-testing}

存储库中的节点遵循[Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository)的命名约定。 但是，Adobe Experience Manager对资源节点的名称实施了进一步的约定。

## 经典 UI {#classic-ui}

经典UI施加了更严格的限制：

* 当满足以下任一条件时验证显式节点名称的资源名称：

   * 提供了资产标题以转换为节点名称
   * 提供了显式节点名称

* 有效字符（从经典UI中创建资产时，只有这些字符实际有效）：

   * &#39;a&#39;到&#39;z&#39;
   * &#39;A&#39;到&#39;Z&#39;
   * &#39;0&#39;到&#39;9&#39;
   * _ （下划线）
   * `-` （短划线/减号）
