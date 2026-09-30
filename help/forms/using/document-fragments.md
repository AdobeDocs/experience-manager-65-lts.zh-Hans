---
title: 文档片段
description: 通信管理中的文档片段（如文本、列表、条件和布局片段）允许您形成客户通信的静态、动态和可重复的组件。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 568a1513-1de9-4f68-be09-f47cd5b30847
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 5%
---
# 文档片段 {#document-fragments}

文档片段是通信的可重用部分/组件，您可以使用它们构成交互式通信/信件。 文档片段具有以下类型：

* **文本**：文本资产是由一个或多个文本段落组成的一段内容。 段落可以是静态的或动态的。

  * [交互式通信中的文本](/help/forms/using/texts-interactive-communications.md)

* **条件**：条件允许您根据提供的数据定义在创建通信时要包含的内容。 该条件用控制变量描述。 控制变量可以是数据字典元素或占位符。

  * [交互式通信中的条件](/help/forms/using/conditions-interactive-communications.md)

* **列表：**&#x200B;列表是一组文档片段，包括文本、列表、条件和图像。 列表元素的顺序可以固定或可编辑。 创建信件时，您可以使用部分或所有列表元素来复制可重用元素模式。
* **布局片段**：布局片段是可在一或多个字母中使用的布局。 布局片段用于创建可重复的模式，尤其是动态表。 布局可包含典型的表单字段，如“Address”和“Reference Number”。 它还包含表示目标区域的空子表单。 在Designer中创建布局(XDP)，然后将其上传到AEM Forms。
