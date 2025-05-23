---
title: 页面创作快速指南
description: 有关创作页面内容关键操作的快速、高级指南
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 5a962fd3-33bb-44df-a48d-416a04f393eb
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 62%

---

# 页面创作快速指南{#quick-guide-to-authoring-pages}

这些步骤旨在作为（高级）快速指南，介绍AEM中创作页面内容的关键操作。

他们：

* 并非旨在提供全面的介绍。
* 提供详细文档的链接。

有关使用 AEM 进行创作的完整详细信息，请参阅：

* [作者的首要步骤](/help/sites-authoring/first-steps.md)
* [创作页面](/help/sites-authoring/page-authoring.md)

## 一些快速提示 {#a-few-quick-hints}

在概述具体内容之前，请查看下面列出的一些常规提示，请牢记这些提示。

### Sites 控制台 {#sites-console}

* **创建**

   * 此按钮在许多控制台中可用 — 显示的选项是上下文相关的，因此在不同的情况下可能有所变化。

* 对文件夹中的页面重新排序

   * 这可以在[列表视图](/help/sites-authoring/basic-handling.md#list-view)中完成。更改已应用并在其他视图中可见。

#### 页面创作 {#page-authoring}

* 导航链接

   * 当您处于&#x200B;***编辑***&#x200B;模式下时，**链接不可用于导航**。若要使用链接进行导航，您需要使用以下任一方式[预览页面](/help/sites-authoring/editing-content.md#previewing-pages)：

      * [预览模式](/help/sites-authoring/editing-content.md#preview-mode)
      * [以发布的形式查看](/help/sites-authoring/editing-content.md#view-as-published)

* 无法从页面编辑器启动/创建版本；现在，可以从站点控制台完成（通过对所选资源选择&#x200B;**创建**&#x200B;或[时间轴](/help/sites-authoring/basic-handling.md#timeline)）。

>[!NOTE]
>
>有几个键盘快捷键可以简化创作体验。
>
>* [编辑页面时的键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)
>

### 查找页面 {#finding-your-page}

查找页面时存在很多方面；您可以导航和/或搜索：

1. 打开&#x200B;**站点**&#x200B;控制台（使用[全局导航](/help/sites-authoring/basic-handling.md#global-navigation)中的&#x200B;**站点**&#x200B;选项） — 此操作将在您选择Adobe Experience Manager链接（左上方）时触发（下拉列表）。

1. 通过点按/单击相应的页面，在树中向下导航。 页面资源的显示方式取决于您使用的视图 — [卡片、列表或列](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)：

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. 使用[标头中的痕迹导航](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs)对树进行向上导航，这让您返回到选定的位置：

   ![qgtap-01](assets/qgtap-01.png)

1. 您还可以[搜索](/help/sites-authoring/search.md)页面。您可以从所显示的结果中选择页面。

   ![qgtap-03](assets/qgtap-03.png)

### 创建新页面 {#creating-a-new-page}

要[创建页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)：

1. [导航到要创建页面的位置](#finding-your-page)。
1. 使用&#x200B;**创建**&#x200B;图标，然后从列表中选择&#x200B;**页面**：

   ![qgtap-02](assets/qgtap-02.png)

1. 这将打开向导，逐步指导您收集[创建新页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)时所需的信息。按照屏幕上的说明操作。

### 选择页面以执行其他操作 {#selecting-your-page-for-further-action}

您可以选择一个页面，以对其执行操作。选择页面后，工具栏将自动更新，以显示与该资源相关的操作。

选择页面的方式取决于您在控制台中所使用的视图：

1. 列视图：

   * 单击所需资源的缩略图 — 缩略图上将覆盖一个勾号，表示已选择该页面。

1. 列表视图：

   * 单击所需资源的缩略图 — 缩略图上将覆盖一个勾号，表示已选择该页面。

1. 卡片视图：

   * 通过以下方式进入选择模式：[选择所需的资源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)：

      * 移动设备：选择并按住
      * 桌面： [快速操作](/help/sites-authoring/basic-handling.md#quick-actions) — 勾号图标：

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * 卡片上将覆盖一个勾号，表示已选择该页面。

   >[!NOTE]
   >
   >进入选择模式后，**Select**&#x200B;图标（勾号）将更改为&#x200B;**Deselect**&#x200B;图标（交叉号）。

### 快速操作（仅限卡片视图/桌面） {#quick-actions-card-view-desktop-only}

[快速操作](/help/sites-authoring/basic-handling.md#quick-actions)可用：

1. [导航](#finding-your-page)到要执行操作的页面。
1. 将鼠标指针悬停在表示所需资源的卡片上方；将显示快速操作：

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### 编辑页面内容 {#editing-your-page-content}

1. [导航](#finding-your-page)到要编辑的页面。
1. 使用“编辑”（铅笔）图标[打开要编辑的页面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)：

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   可以从以下位置访问该图标：

   * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
   * [选择页面](#selectiingyourpageforfurtheraction)后显示的工具栏。

1. 在打开编辑器时，您可以：

   * 通过以下方式[向页面中添加新组件](/help/sites-authoring/editing-content.md#inserting-a-component)：

      * 打开侧面板
      * 选择“组件”选项卡（[组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)）
      * 将所需的组件拖动到页面上。

     可以通过以下图标打开（或关闭）侧面板：

     ![打开侧面板](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [编辑页面中现有组件的内容](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)：

      * 通过单击打开组件工具栏。 使用&#x200B;**编辑**（铅笔）图标打开对话框。
      * 通过按住select键或双击来打开组件的就地编辑器。 此时会显示可用的操作（对于某些组件，该选择将受到限制）。
      * 要查看所有可用的操作，请使用以下图标进入全屏模式：

     ![全屏模式](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [配置现有组件的属性](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * 通过单击打开组件工具栏。 使用&#x200B;**配置**（扳手）图标打开对话框。

   * 通过以下任一方式[移动组件](/help/sites-authoring/editing-content.md#moving-a-component)：

      * 将所需组件拖动到新位置。
      * 通过单击打开组件工具栏。 必要时使用&#x200B;**剪切**&#x200B;和&#x200B;**粘贴**&#x200B;图标。

   * [复制（并粘贴）](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)组件：

      * 通过单击打开组件工具栏。 根据需要依次使用&#x200B;**复制**&#x200B;和&#x200B;**粘贴**&#x200B;图标。

   >[!NOTE]
   >
   >您可以将组件&#x200B;**粘贴**&#x200B;到同一页面或其他页面。如果在剪切/复制操作之前粘贴到已打开的其他页面，则表明该页面需要刷新。

   * [删除](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)组件：

      * 单击打开组件工具栏，然后使用&#x200B;**删除**&#x200B;图标。

   * 向页面[添加注释](/help/sites-authoring/annotations.md#annotations)：

      * 选择&#x200B;**注释**&#x200B;模式（对话气泡图标）。使用&#x200B;**添加注释**（加号）图标添加注释。使用右上方的 X 退出注释模式。

     ![批注](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [预览页面](/help/sites-authoring/editing-content.md#preview-mode)（用于查看页面在发布环境中的显示情况）

      * 从工具栏中选择&#x200B;**预览**。

   * 使用&#x200B;**编辑**&#x200B;下拉选择器返回编辑模式（或选择其他模式）。

   >[!NOTE]
   >
   >要使用内容中的链接进行导航，您必须使用[预览模式](/help/sites-authoring/editing-content.md#preview-mode)。

### 编辑页面属性 {#editing-the-page-properties}

[编辑页面属性](/help/sites-authoring/editing-page-properties.md)的方法（主要）有两种：

* 从&#x200B;**Sites**&#x200B;控制台中：

   1. [导航](#finding-your-page)到要发布的页面。
   1. 从以下任一位置选择&#x200B;**属性**&#x200B;图标：

      * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
      * [选择页面](#selectiingyourpageforfurtheraction)后显示的工具栏。

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. 页面属性会显示。您可以进行需要的更新，然后使用“保存”保留这些更改

* 在[编辑页面](#editing-your-page-content)时：

   1. 打开&#x200B;**页面信息**&#x200B;菜单。
   1. 选择&#x200B;**打开属性**&#x200B;以打开用于编辑属性的对话框。

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### 发布页面（或取消发布） {#publishing-your-page-or-unpublishing}

[发布页面](/help/sites-authoring/publishing-pages.md)（和取消发布）的方法主要有两种：

* 从&#x200B;**Sites**&#x200B;控制台中：

   1. [导航](#finding-your-page)到要发布的页面。
   1. 从以下任一位置选择&#x200B;**快速发布**&#x200B;图标：

      * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
      * [选择页面](#selectiingyourpageforfurtheraction)后显示的工具栏（还可以访问[稍后发布](/help/sites-authoring/publishing-pages.md#main-pars-title-12)）。

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* 在[编辑页面](#editing-your-page-content)时：

   1. 打开&#x200B;**页面信息**&#x200B;菜单。
   1. 选择&#x200B;**发布页面**。

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* 从控制台取消发布页面只能通过&#x200B;**管理发布**&#x200B;选项完成，该选项仅在工具栏上可用（不能通过快速操作）。

  **取消发布页面**&#x200B;选项仍可通过编辑器中的&#x200B;**页面信息**&#x200B;菜单使用。

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  请参阅[发布页面](/help/sites-authoring/publishing-pages.md#unpublishing-pages)以了解更多信息。

### 移动、复制并粘贴或删除页面 {#move-copy-and-paste-or-delete-your-page}

这些操作全部可以通过以下项触发：

1. [导航](#finding-your-page)到要移动、复制并粘贴或删除的页面。
1. 使用以下任一方式根据需要选择复制（然后粘贴）、移动或删除图标：

   * 所需资源的[快速操作（仅限卡片视图/桌面）](#quick-actions-card-view-desktop-only)。
   * [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。

   然后，取决于您的操作：

   * 复制：

      * 导航到新位置并粘贴。

   * 移动：

      * 此时将打开向导，收集移动页面所需的信息。 按照屏幕上的说明操作。

   * 删除：

      * 系统会要求您确认该操作。

   >[!NOTE]
   >
   >快速操作中并未提供“删除”操作。

### 锁定页面（然后解锁） {#locking-your-page-then-unlocking}

[锁定页面](/help/sites-authoring/editing-content.md#locking-a-page) ，可阻止其他作者在您处理页面时对其进行处理。可以找到“锁定”（和“解锁”）图标／按钮：

* [选择页面](#selecting-your-page-for-further-action)后显示的工具栏。
* 编辑页面时显示的[“页面信息”下拉菜单](#editing-the-page-properties)。
* 编辑页面（页面处于锁定状态）时显示的页面工具栏

例如，“锁定”图标如下所示：

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### 访问页面引用 {#accessing-page-references}

[在“引用”边栏中，可以快速访问对某个页面或某个页面的引用](/help/sites-authoring/author-environment-tools.md#references)。

1. 使用工具栏图标选择&#x200B;**引用**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   此时会显示引用类型列表：

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. 单击所需的引用类型以显示更多详细信息并（在适当时）采取进一步操作。

### 创建页面版本 {#creating-a-version-of-your-page}

要创建页面的[版本](/help/sites-authoring/working-with-page-versions.md)：

1. 要打开“时间线”边栏，请使用工具栏图标选择&#x200B;**[时间线](/help/sites-authoring/basic-handling.md#timeline)**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. 单击“时间轴”列右下方的向上箭头以显示其他按钮，包括&#x200B;**另存为版本**。

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. 选择&#x200B;**另存为版本**，然后再选择&#x200B;**创建**。

### 恢复/比较页面版本 {#restoring-comparing-a-version-of-your-page}

恢复和/或比较页面版本时所使用的机制基本相同：

1. 使用工具栏图标选择&#x200B;**[时间线](/help/sites-authoring/basic-handling.md#timeline)**（在[选择您的页面](#selecting-your-page-for-further-action)之前或之后）：

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   如果页面的某个版本已经保存，则会在“时间轴”中列出该版本。

1. 单击要还原的版本 — 这将显示其他操作按钮：

   * **恢复到此版本**

      * 该版本会恢复。

   * **显示差异**

      * 该页面会打开，并突出显示（两个版本之间的）差异。
