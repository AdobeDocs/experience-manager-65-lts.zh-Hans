---
title: 提升启动项
description: 您需要提升启动页面以将内容移回源（生产）中，然后才能进行发布。提升启动页面时，源页面的相应页面将被提升页面的内容替换。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 1167735d-a13a-438e-bef8-205e27f59f4e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 56%

---

# 提升启动项{#promoting-launches}

您需要提升启动页面以将内容移回源（生产）中，然后才能进行发布。提升启动页面时，源页面的对应页面会被替换为提升页面的内容。提升启动页面时可以做出以下选择：

* 是只提升当前页面还是提升整个启动项。
* 是否提升当前页面的子页面。
* 是提升整个启动项还是只提升已更改的页面。

## 提升启动页面 {#promoting-launch-pages}

要提升页面，请在编辑要提升的启动页面时执行以下步骤：

1. 在Sidekick的&#x200B;**页面**&#x200B;选项卡中，单击&#x200B;**提升启动项**。
1. 指定要提升的页面：

   * （默认）要仅提升当前页面，请选择&#x200B;**将页面更改提升到生产版本**。
   * 若要同时提升当前页面的子页面，请选择&#x200B;**包含子页面**。
   * 若要提升启动项中的所有页面，请选择&#x200B;**将完整启动项提升至生产版本**。

1. 要将生产页面添加到工作流包，请选择&#x200B;**添加到工作流包**，然后选择工作流包。
1. 单击&#x200B;**提升**。

## 使用 AEM 工作流处理提升的页面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型批处理提升的启动页面：

1. 创建工作流包。
1. 当作者提升启动页面时，他们会将其存储在工作流包中。
1. 将包作为有效负荷，以启动工作流模型。

要在提升页面时自动启动工作流，请[为包节点配置工作流启动器](/help/sites-administering/workflows-starting.md#workflows-launchers)。

例如，您可以在作者提升启动页面时自动生成页面激活请求。配置工作流启动器，以在包节点被修改时启动请求激活工作流。

![chlimage_1-136](assets/chlimage_1-136.png)
