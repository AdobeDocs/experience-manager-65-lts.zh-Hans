---
title: 工作流参与率
description: 工作流通常包括需要人员对页面或资源执行活动的步骤。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
exl-id: 2680e967-ec04-4ae6-b379-f1f0e7c6606b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 73%

---

# 参与工作流{#participating-in-workflows}

工作流通常包括需要人员对页面或资源执行活动的步骤。工作流会选择要执行活动的用户或组，并将工作项分配给该用户或组。用户收到通知后，便可以执行相应的操作：

* [查看通知](#notifications-of-available-workflow-actions)
* [完成参与者步骤](#completing-a-participant-step)
* [委派参与者步骤](#delegating-a-participant-step)
* [对参与者步骤执行回退](#performing-step-back-on-a-participant-step)
* [打开工作流项目查看详细信息（并执行操作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [查看工作流有效负载（多个资源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流操作的通知 {#notifications-of-available-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 您的[通知](/help/sites-authoring/inbox.md)指示器（工具栏）将递增：

  ![通知指示器](do-not-localize/wf-57.png)

* 该工作项将在您的通知[收件箱](/help/sites-authoring/inbox.md)中列出：

  ![wf-58](assets/wf-58.png)

* 当您使用页面编辑器时，状态栏将显示：

   * 应用于页面的工作流的名称；例如，“请求激活”。
   * 当前用户可在工作流的当前步骤中使用的任何操作；例如“完成”、“委派”、“查看详细信息”。
   * 页面需执行的工作流数量。您可以：

      * 使用向左/向右箭头浏览各种工作流的状态信息。
      * 单击实际编号以打开所有适用工作流的下拉列表，然后选择要显示在状态栏中的工作流。

  ![wf-59](assets/wf-59.png)

  >[!NOTE]
  >
  >状态栏只对拥有工作流权限的用户可见；例如，`workflow-users` 组的成员。
  >
  >
  >如果当前用户直接参与工作流的当前步骤，则会显示相应的操作。

* 当打开资源的&#x200B;**时间轴**&#x200B;时，会显示工作流步骤。单击警报横幅时，也会显示可用的操作：

  ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 完成参与者步骤 {#completing-a-participant-step}

您可以完成一个工作项，从而使工作流进入到下一步。

在此操作中，您可以指示：

* **下一步**：要执行的下一个步骤；您可以从提供的列表中进行选择
* **评论**：如有必要

您可以通过以下任一方式完成参与者步骤：

* [收件箱](#completing-a-participant-step-inbox)
* [页面编辑器](#completing-a-participant-step-page-editor)
* [时间线](#completing-a-participant-step-timeline)
* [打开工作流项以查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 完成参与者步骤 - 收件箱 {#completing-a-participant-step-inbox}

请按照以下过程完成工作项：

1. 打开 **[AEM 收件箱](/help/sites-authoring/inbox.md)**。
1. 选择要对其执行操作的工作流项目（单击缩略图）。
1. 从工具栏中选择&#x200B;**完成**。
1. 将打开&#x200B;**完成工作项**&#x200B;对话框。 从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**注释**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 完成参与者步骤 - 页面编辑器 {#completing-a-participant-step-page-editor}

请按照以下过程完成工作项：

1. 打开[要编辑的页面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 从顶部的状态栏中选择&#x200B;**完成**。
1. 将打开&#x200B;**完成工作项**&#x200B;对话框。 从下拉选择器中选择&#x200B;**下一步**，并根据需要添加&#x200B;**注释**。
1. 单击&#x200B;**确定**&#x200B;以完成该步骤（或者单击&#x200B;**取消**&#x200B;以中止该操作）。

#### 完成参与者步骤 - 时间线 {#completing-a-participant-step-timeline}

您也可以使用时间线来完成并推进步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）：

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. 单击警报横幅可显示可用的操作。 选择&#x200B;**前进**：

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. 根据工作流，您可以选择下一步：

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 选择&#x200B;**前进**&#x200B;以确认操作。

### 委派参与者步骤 {#delegating-a-participant-step}

如果某个步骤已分配给您，但由于某种原因您无法采取操作，则您可以将该步骤委派给其他用户或组。

可向其进行委派的用户取决于工作项分配到的对象：

* 如果将工作项分配给某个组，则可以向该组的成员进行委派。
* 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
* 如果将工作项分配给单个用户，则不能委派工作项。

在此操作中，您可以指示：

* **用户**：您要向其进行委派的用户；您可以从提供的列表中进行选择
* **评论**：如有必要

您可以通过以下任一方式委派参与者步骤：

* [收件箱](#delegating-a-participant-step-inbox)
* [页面编辑器](#delegating-a-participant-step-page-editor)
* [时间线](#delegating-a-participant-step-timeline)
* [打开工作流项以查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 委派参与者步骤 - 收件箱 {#delegating-a-participant-step-inbox}

请按照以下过程委派工作项：

1. 打开 **[AEM 收件箱](/help/sites-authoring/inbox.md)**。
1. 选择要对其执行操作的工作流项目（单击缩略图）。
1. 从工具栏中选择&#x200B;**委派**。
1. 此时将打开对话框。 从下拉选择器中指定&#x200B;**用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派参与者步骤 - 页面编辑器 {#delegating-a-participant-step-page-editor}

请按照以下过程委派工作项：

1. 打开[要编辑的页面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 从顶部的状态栏中选择&#x200B;**委派**。
1. 此时将打开对话框。 从下拉选择器中指定&#x200B;**用户**（也可以是组），并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 委派参与者步骤 - 时间线 {#delegating-a-participant-step-timeline}

您也可以使用时间线来委派和/或分配步骤：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 单击警报横幅可显示可用的操作。 选择&#x200B;**更改被分派人**：

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 指定新的被分派人：

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 选择&#x200B;**分配**，确认操作。

### 对参与者步骤执行回退 {#performing-step-back-on-a-participant-step}

如果您发现需要重复一个步骤或一系列步骤，您可以执行回退。这使您能够选择在工作流中先前发生的步骤以进行重新处理。 工作流会返回到您指定的步骤，然后从此处继续执行。

在此操作中，您可以指示：

* **上一步**：要返回到的步骤；您可以从提供的列表中进行选择
* **评论**：如有必要

您可以通过以下任一方式对参与者步骤执行后退：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [页面编辑器](#performing-step-back-on-a-participant-step-page-editor)
* [时间线](#performing-step-back-on-a-participant-step-timeline)
* [打开工作流项以查看详细信息](#opening-a-workflow-item-to-view-details-and-take-actions)时。

#### 对参与者步骤执行回退 - 收件箱 {#performing-step-back-on-a-participant-step-inbox}

请按照以下过程执行回退：

1. 打开 **[AEM 收件箱](/help/sites-authoring/inbox.md)**。
1. 选择要对其执行操作的工作流项目（单击缩略图）。
1. 选择&#x200B;**回退**，打开对话框。

1. 指定&#x200B;**上一步**&#x200B;并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 对参与者步骤执行回退 - 页面编辑器 {#performing-step-back-on-a-participant-step-page-editor}

请按照以下过程执行回退：

1. 打开[要编辑的页面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 从顶部的状态栏中选择&#x200B;**回退**。
1. 指定&#x200B;**上一步**&#x200B;并根据需要添加&#x200B;**评论**。
1. 单击&#x200B;**确定**&#x200B;完成该步骤（或者单击&#x200B;**取消**&#x200B;中止该操作）。

#### 对参与者步骤执行回退 - 时间线 {#performing-step-back-on-a-participant-step-timeline}

您也可以使用时间线来回滚（回退）到上一步：

1. 选择所需的页面，然后打开&#x200B;**时间线**（或者先打开&#x200B;**时间线**，然后再选择页面）。
1. 单击警报横幅可显示可用的操作。 选择&#x200B;**回滚**：

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. 指定工作流应返回到的步骤：

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 选择&#x200B;**回滚**，确认操作。

### 打开工作流项目以查看详细信息（并执行操作） {#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作项的详细信息并执行相应的操作。

工作流详细信息会以选项卡的形式显示，并且工具栏中会提供相应的操作：

* **工作项**&#x200B;选项卡：

  ![wf-72](assets/wf-72.png)

* **工作流信息**&#x200B;选项卡：

  ![wf-73](assets/wf-73.png)

  如果已为模型配置了[工作流暂存](/help/sites-developing/workflows.md#workflow-stages)，则可以根据以下内容查看进度：

  ![wf-107](assets/wf-107.png)

* **评论**&#x200B;选项卡：

  ![wf-75](assets/wf-75.png)

您可以通过以下任一方式打开工作项详细信息：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [页面编辑器](#performing-step-back-on-a-participant-step-page-editor)

#### 打开工作流详细信息 - 收件箱 {#opening-workflow-details-inbox}

要打开工作流项目并查看其详细信息，请执行以下操作：

1. 打开 **[AEM 收件箱](/help/sites-authoring/inbox.md)**。
1. 选择要对其执行操作的工作流项目（单击缩略图）。
1. 选择&#x200B;**打开**，打开信息选项卡。

1. 如有必要，请选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定** （或&#x200B;**取消**）进行确认。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

#### 打开工作流详细信息 - 页面编辑器 {#opening-workflow-details-page-editor}

要打开工作流项目并查看其详细信息，请执行以下操作：

1. 打开[要编辑的页面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 从状态栏中选择&#x200B;**查看详细信息**&#x200B;以打开信息选项卡。

1. 如有必要，请选择相应的操作，提供任何详细信息，然后单击&#x200B;**确定** （或&#x200B;**取消**）进行确认。
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;以退出。

### 查看工作流有效负荷（多个资源） {#viewing-the-workflow-payload-multiple-resources}

您可以查看与工作流实例关联的有效负荷的详细信息。最初会显示资源包，之后您可以深入查看各个页面。

要查看工作流实例的有效负荷和资源，请执行以下操作：

1. 打开 **[AEM 收件箱](/help/sites-authoring/inbox.md)**。
1. 选择要对其执行操作的工作流项目（单击缩略图）。
1. 从工具栏中选择&#x200B;**查看有效负载**&#x200B;以打开对话框。

   由于工作流包只是存储库中路径的指针集合，因此您可以在此处添加/删除/修改条目以调整工作流包所引用的内容。使用&#x200B;**资源定义**&#x200B;组件可添加新条目。

   ![wf-78](assets/wf-78.png)

1. 可以使用这些链接打开各个页面。
