---
title: 处理任务
description: 任务是指要对内容完成的工作项，可在项目中使用任务来确定当前任务的完成程度
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 852aaf6e-acf3-4224-bf4c-c0913110abd4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 41%

---

# 处理任务 {#working-with-tasks}

任务表示与内容相关要执行的工作项目。 当有任务分配给您时，它会显示在您的 Workflow 收件箱中。任务项可以通过值&#x200B;**Type**&#x200B;列与工作流项进行区分。

任务也用在项目中，以确定项目的完整性级别。

## 跟踪项目进度 {#tracking-project-progress}

您可以通过查看项目内由&#x200B;**任务**&#x200B;拼贴表示的活动/已完成任务来跟踪项目进度。项目进度可由以下两项决定：

* **任务拼贴：**&#x200B;项目详细信息页面上的“任务拼贴”中描述了项目的整体进度。

* **任务列表：**&#x200B;单击任务拼贴时，将显示任务列表。 此列表包含与项目相关的所有任务的详细信息。

这两个选项都列出了工作流任务和直接在任务拼贴中创建的任务。

### “任务”拼贴 {#task-tile}

如果项目具有任何相关任务，则任务拼贴将显示在项目内。 任务拼贴显示项目的当前状态。 “任务”拼贴基于工作流内的现有任务，它不包括将来随着工作流的继续执行而生成的任何任务。以下信息会显示在“任务”拼贴中：

* 已完成任务的百分比
* 活动任务的百分比
* 过期任务的百分比

![任务拼贴](assets/project-tile-tasks.png)

### 查看或修改项目中的任务 {#viewing-or-modifying-the-tasks-in-a-project}

除了跟踪进度外，您还可能想要查看有关项目的更多信息或对其进行修改。

#### 任务列表 {#task-list}

单击任务拼贴右下方的省略号按钮，可显示您的收件箱，该收件箱已根据与项目相关的任务进行了过滤。 任务详细信息会与元数据一起显示，例如到期日期、被分派人、优先级和状态。

![项目任务收件箱](assets/project-tasks.png)

#### 任务详细信息 {#task-details}

有关特定任务的详细信息，请在收件箱中单击该任务以将其选定，然后单击工具栏中的&#x200B;**打开**。

![任务详细信息](assets/project-task-detail.png)

您可以通过不同的选项卡查看、编辑或向任务添加详细信息。

* **任务** — 一般任务信息
* **项目信息** — 与任务关联的项目摘要
* **工作流信息** — 与任务关联的工作流的摘要（如果适用）
* **备注** — 任务本身的一般备注

### 添加任务 {#adding-tasks}

您可以将新任务添加到项目中。然后，这些任务会出现在“任务”拼贴中，并出现在“通知”收件箱中，以便您了解未完成的任务。

要添加任务，请执行以下操作：

1. 在项目中，找到&#x200B;**任务**&#x200B;拼贴
1. 单击图块右上角的向下V形标记并选择&#x200B;**创建任务**。
1. 在&#x200B;**添加任务**&#x200B;窗口中，提供任务详细信息，如优先级、被分派人和到期日期。

   ![添加任务](assets/project-add-task.png)

1. 单击&#x200B;**“提交”。**

## 在收件箱中处理任务 {#working-with-tasks-in-the-inbox}

您可以直接从收件箱访问项目任务，而不是从项目本身访问项目任务。 收件箱会为您提供跨项目的任务概览，以便您了解整个工作流。

在收件箱中，您可以打开任务并设置任务状态。 如果任务被分配到您所属的用户组，则它们也会显示在您的收件箱中。在这种情况下，组内的任何成员都可以执行工作并完成任务。

![收件箱](assets/project-inbox.png)

要完成任务，请选择该任务并单击工具栏中的&#x200B;**完成**。 向该任务中添加信息，然后单击&#x200B;**完成**。有关更多信息，请参阅[您的收件箱](/help/sites-authoring/inbox.md)。
