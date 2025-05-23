---
title: 自定义任务的选项卡
description: 如何在LiveCycle AEM Forms Workspace中自定义任务的选项卡名称。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 88f5093c-f249-4e4b-900a-5897f47e513c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 自定义任务的选项卡 {#customizing-tabs-for-a-task}

您可以在`Start Process` Uber视图中自定义`Start Process`组件的选项卡名称，在`ToDo` Uber视图中自定义`Task Details`组件。

1. 按照[通用步骤自定义AEM Forms工作区](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 在`translation.json`文件中更改`tabname`的值。

   例如，将英语的`/apps/ws/locales/en-US/translation.json`更改为以下内容。

   * 对于在启动进程中启动的任务，请使用`"startprocess" : {}`块中的以下代码片段。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于待办事项中的任务，请使用`"todo" : {}`块中的以下代码片段。

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。
