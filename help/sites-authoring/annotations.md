---
title: 编辑内容页面时的批注
description: 许多与内容直接相关的组件允许您添加注释。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 5e0e7d8e-4da2-4304-ac21-7500ca2ba9c6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 33%

---

# 编辑页面时的批注{#annotations-when-editing-a-page}

向网站页面添加内容时，通常会先进行讨论，然后再实际发布。 为此，您可以添加注释，其中许多与内容直接相关的组件（例如，与布局相反）可以让您添加注释。

批注在页面上放置彩色标记/便笺。 您（或其他用户）可以通过注释给其他作者/审阅人留下意见和/或问题。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

>[!NOTE]
>
>在经典UI中创建的注释显示在触屏UI中。 不过，草图是特定于UI的，并且仅在创建它们的UI中显示。

>[!CAUTION]
>
>删除资源（例如，段落）会删除附加到该资源的所有注释和草图，无论这些注释和草图处于整个页面的什么位置，均将如此。

>[!NOTE]
>
>根据您的要求，您还可以开发一个工作流，用于在添加、更新或删除注释时发送通知。

## 注释 {#annotations}

这是一种特殊的[模式](/help/sites-authoring/author-environment-tools.md#page-modes)，可用于创建和查看注释。

>[!NOTE]
>
>请不要忘记，[评论](/help/sites-authoring/basic-handling.md#timeline)也可用于在页面上提供反馈。

>[!NOTE]
>
>您可以对各种资源添加注释：
>
>* [为资产添加批注](/help/assets/manage-assets.md#annotating)
>* [为视频资源添加批注](/help/assets/managing-video-assets.md#annotate-video-assets)
>

### 对组件添加注释 {#annotating-a-component}

在“注释”模式下，您可以创建、编辑、移动或删除内容上的注释：

1. 在编辑页面时，您可以使用工具栏（右上方）中的图标进入注释模式：

   ![批注](do-not-localize/screen_shot_2018-03-22at110414.png)

   此时，您可以查看任何现有的注释。

   >[!NOTE]
   >
   >要退出注释模式，请单击顶部工具栏右侧的“注释”图标（x符号）。

1. 单击“添加注释”图标（工具栏左侧的加号）以开始添加注释。

   >[!NOTE]
   >
   >要停止添加注释（并返回查看），请单击顶部工具栏左侧的“取消”图标（白圆中的x符号）。

1. 单击所需的组件（可进行注释的组件将以蓝色边框突出显示）以添加注释，然后打开对话框：

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   在此处，可使用相应的字段和/或图标执行以下操作：

   * 输入注释文本。
   * 创建草图（线和形状）以突出显示组件的某个区域。


     创建草绘时，光标将变为十字线。 您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。

     ![草图](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 选择/更改颜色：

     ![选择/更改颜色](do-not-localize/chlimage_1-19.png)

   * 删除注释。

     ![删除注释](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 单击/点按注释对话框外部可关闭该对话框。 将显示截断的注释视图（第一个字）以及任何草图：

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 完成特定注释编辑之后，您可以：

   * 单击文本标记以打开注释。 打开后，即可查看全文、进行更改或删除注释。

      * 不能独立于注释删除草图。

   * 调整文本标记位置。
   * 单击草绘线以选取该草绘，并将其拖动到所需位置。
   * 移动或复制组件

      * 还将移动或复制任何相关的注释及其草图，并且它们相对于段落的位置将保持不变。

1. 要退出“注释”模式并返回以前使用的模式，请单击顶部工具栏右侧的“注释”图标（x符号）。

>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

### 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![批注指示器](assets/chlimage_1-242.png)
