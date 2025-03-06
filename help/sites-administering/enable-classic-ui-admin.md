---
title: Admin Console
description: 了解如何使用Adobe Experience Manager中提供的Admin Console。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 9cc6e4b6-7170-4c9a-a2c0-6ba4603cfd17
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Admin Console{#admin-consoles}

默认情况下，通过Admin Console切换到经典UI的功能被禁用。 因此，不再显示鼠标悬停在特定控制台图标上时看到的弹出图标，这些图标允许访问经典UI。

每个在`/libs/cq/core/content/nav`中具有经典UI版本的控制台都可以单独重新启用，以便在鼠标悬停在控制台图标上时再次弹出&#x200B;**经典UI**&#x200B;选项。

在此示例中，您将为站点控制台重新启用经典UI。

1. 使用CRXDE Lite查找与要为其重新启用Classic UI的Admin Console对应的节点。 它们位于以下位置：

   `/libs/cq/core/content/nav`

   例如

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 选择与要为其重新启用经典UI的控制台对应的节点。 对于此示例，您将为站点控制台重新启用经典UI。

   `/libs/cq/core/content/nav/sites`

1. 使用&#x200B;**覆盖节点**&#x200B;选项创建覆盖；例如：

   * **路径**： `/apps/cq/core/content/nav/sites`
   * **覆盖位置**： `/apps/`
   * **匹配节点类型**：活动（选中复选框）

1. 将以下布尔属性添加到覆盖的节点：

   `enableDesktopOnly = {Boolean}true`

1. **经典UI**&#x200B;选项再次作为Admin Console中的弹出框选项提供。

   ![经典UI弹出框选项](assets/syui-01-2019-02-27-15-16-55.png)

对要重新启用经典UI版本访问权限的每个控制台重复这些步骤。
