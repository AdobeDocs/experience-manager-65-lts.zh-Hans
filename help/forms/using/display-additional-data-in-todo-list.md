---
title: 在待办事项列表中显示附加数据
description: 如何自定义LiveCycle AEM Forms工作区待办事项列表的显示，以显示默认列表以外的更多信息。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 988e986f-8e0b-48a2-a529-9c0f931131b9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 在待办事项列表中显示附加数据{#displaying-additional-data-in-todo-list}

默认情况下，AEM Forms工作区的待办事项列表会显示任务显示名称和描述。 但是，您可以添加其他信息，如创建日期、截止日期等。 您还可以添加图标和更改显示样式。

![查看HTML Workspace的“待办事项”选项卡，其中显示了默认配置](assets/html-todo-list.png)

本文详细介绍了添加要为ToDo列表中的每个任务显示的信息所需的步骤。

## 可添加的内容 {#what-can-be-added}

您可以添加服务器发送的`task.json`中可用的信息。 信息可以纯文本形式添加，也可以使用样式设置信息的格式。

有关JSON对象描述的详细信息，请参阅[此](/help/forms/using/html-workspace-json-object-description.md)文章。

## 显示任务信息 {#displaying-information-on-a-task}

1. 按照[通用步骤自定义AEM Forms工作区](../../forms/using/generic-steps-html-workspace-customization.md)。
1. 要显示任务的附加信息，必须在`translation.json`的任务块中添加相应的键值对。

   例如，将`/apps/ws/locales/en-US/translation.json`更改为英语：

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。

1. 例如，在任务块中添加信息：

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 为新属性定义CSS {#defining-css-for-the-new-property}

1. 可以将样式应用于添加到任务的信息（属性）。 为此，您需要为添加到`/apps/ws/css/newStyle.css`的新属性添加样式信息。

   例如，添加：

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## 在HTML模板中添加条目 {#adding-entry-in-the-html-template}

最后，您需要在开发包中为要添加到任务的每个属性包含一个条目。 要创建工作区代码，请参阅构建AEM Forms工作区代码。

1. 复制`task.html`：

   * 发件人： `/libs/ws/js/runtime/templates/`
   * 收件人：`/apps/ws/js/runtime/templates/`

1. 将新信息添加到`/apps/ws/js/runtime/templates/task.html`。

   例如，在`div class="taskProperties"`下添加：

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
