---
title: 编辑启动项
description: 为您的页面（或页面集）创建启动项后，您可以在页面的启动项副本中编辑内容。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
exl-id: 7b032487-a084-4403-a0d3-e5de62748769
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 75%

---

# 编辑启动项{#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

为某个页面（或一组页面）创建了启动项后，您可以在页面的启动项副本中编辑内容。

1. [从“引用”（ Sites 控制台）中访问启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)，即可显示可用操作。
1. 选择&#x200B;**转到页面**，即可打开要编辑的页面。

>[!NOTE]
>
>您不能在启动项中移动页面。尝试此操作将触发警告消息：
>
>* 警告：此页面是启动项的源。不允许移动此页面。

### 编辑基于 Live Copy 的启动页面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的启动项基于[Live Copy](/help/sites-administering/msm.md)，则您将会：

* 在编辑组件（内容和/或属性）时，请参阅锁定符号（小挂锁）。
* 在&#x200B;**页面属性**&#x200B;中查看&#x200B;**Live Copy**&#x200B;选项卡

Live Copy 用于将&#x200B;**&#x200B;源分支&#x200B;**&#x200B;中的内容同步到启动分支（以使启动项与源中所做的更改保持最新）。

您可以按照编辑标准 Live Copy 的方式进行更改；例如：

* 单击已关闭的挂锁将破坏此同步，并允许您对启动项中的内容进行新的更新。 解除锁定（打开挂锁）后，您的更改将不会被源分支中的相同位置所做的任何更改所覆盖。
* 特定页面的&#x200B;**暂停**（和&#x200B;**继续**）继承。

有关更多信息，请参阅[更改 Live Copy 内容](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)。

## 比较启动页面与其源页面 {#comparing-a-launch-page-to-its-source-page}

要跟踪您所做的更改，您可以在&#x200B;**引用**&#x200B;中查看启动项，并将启动页面与其源页面进行比较：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到启动项的源页面并将其选定](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)。
1. 打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板，然后选择&#x200B;**启动项**。
1. 选择您的特定启动项，然后选择&#x200B;**和源比较**：

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 此时将并列打开两个页面（启动页面和源页面）。

   有关使用此功能的完整信息，请参阅[页面差异](/help/sites-authoring/page-diff.md)。

## 更改使用的源页面 {#changing-the-source-pages-used}

您可以随时向启动项的源页面范围中添加页面或从中删除页面：

1. 从以下任一位置访问并选择启动项：

   * [“启动项”控制台](/help/sites-authoring/launches.md#the-launches-console)：

      * 选择&#x200B;**编辑**。

   * [“引用”（Sites 控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console)，可显示可用操作：

      * 选择&#x200B;**编辑启动项**。

   此时会显示源页面。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   >[!NOTE]
   >
   >要将页面添加到启动项，这些页面必须位于通用语言根目录下；即，在单个站点内。

## 编辑启动项配置 {#editing-a-launch-configuration}

您可以随时编辑启动项的属性：

1. 从以下任一位置访问并选择启动项：

   * [“启动项”控制台](/help/sites-authoring/launches.md#the-launches-console)：

      * 选择&#x200B;**属性**。

   * [“引用”（Sites 控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console)，可显示可用操作：

      * 选择&#x200B;**编辑属性**。

   详细信息会显示。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   有关启 [动日期和生产就绪字段的用途和交互的信息](/help/sites-authoring/launches.md#launches-the-order-of-events)**&#x200B;**&#x200B;**&#x200B;** ，请参阅启动项——事件的顺序。

## 发现页面的启动状态 {#discovering-the-launch-status-of-a-page}

从“引用”选项卡中选择特定启动项时，将会显示状态（请参阅[“引用”（Sites 控制台）中的启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)）。

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
