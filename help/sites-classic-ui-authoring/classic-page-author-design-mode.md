---
title: 在设计模式下配置组件
description: 现成安装AEM实例后，即可在sidekick中立即找到一组组件。 除此之外，还可以使用各种其他组件。 您可以使用设计模式启用/禁用此类组件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 1334d04b-8e73-487c-aa87-531f00f1d5f2
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 在设计模式下配置组件{#configuring-components-in-design-mode}

现成安装AEM实例后，即可在sidekick中立即找到一组组件。

除此之外，还可以使用各种其他组件。 您可以使用设计模式[启用/禁用此类组件](#enabledisablecomponentsusingdesignmode)。 启用并位于您的页面后，您可以使用设计模式通过编辑属性参数来[配置组件设计的各个方面](#configuringcomponentsusingdesignmode)。

>[!NOTE]
>
>编辑这些组件时务必谨慎。 设计设置通常是整个网站设计不可分割的一部分，因此它们只应由具有适当权限（和体验）的人员更改，通常是管理员或开发人员。 有关详细信息，请参阅[开发组件](/help/sites-developing/components.md)。

这实际上涉及添加或删除页面段落系统中允许的组件。 段落系统(`parsys`)是包含所有其他段落组件的复合组件。 段落系统允许作者向页面添加不同类型的组件，因为它包含所有其他段落组件。 每个段落类型都表示为一个组件。

例如，产品页面的内容可能包含包含以下内容的段落系统：

* 产品的图像（采用图像或文本段落的形式）
* 产品描述（作为文本段落）
* 带有技术数据的表格（作为表格段落）
* 表单用户填写（作为表单开头、表单元素和表单结束段落）

>[!NOTE]
>
>有关`parsys`的详细信息，请参阅[开发组件](/help/sites-developing/components.md#paragraphsystem)和[使用模板和组件的准则](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)。

## 启用/禁用组件 {#enable-disable-components}

在设计模式下，Sidekick被最小化，您可以配置可用于创作的组件：

1. 要进入设计模式，请打开要编辑的页面，然后使用Sidekick图标：

   ![设计模式](do-not-localize/chlimage_1.png)

1. 在段落系统(**Design of par**)上单击&#x200B;**编辑**。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 此时将打开一个对话框，其中列出了Sidekick中显示的组件组及其包含的各个组件。

   根据需要选择添加或删除可在Sidekick中使用的组件。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 在设计模式下，Sidekick会最大限度地减少工作量。 通过单击箭头，您可以最大化Sidekick并返回到编辑模式：

   ![Sidekick已最小化](do-not-localize/sidekick-collapsed.png)

## 配置组件设计 {#configuring-the-design-of-a-component}

在设计模式下，您还可以配置各个组件的属性。 每个组件都有自己的参数，以下示例显示了&#x200B;**图像**&#x200B;组件：

1. 要进入设计模式，请打开要编辑的页面，然后使用Sidekick图标：

   ![设计模式 — Sidekick](do-not-localize/chlimage_1-1.png)

1. 您可以配置组件设计。

   例如，如果单击图像组件（**图像设计**）上的&#x200B;**编辑**，则可以配置特定于组件的参数：

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 单击&#x200B;**确定**&#x200B;以保存更改。

1. 在设计模式下，Sidekick会最大限度地减少工作量。 通过单击箭头，您可以最大化Sidekick并返回到编辑模式：

   ![Sidekick已最小化](do-not-localize/sidekick-collapsed-1.png)
