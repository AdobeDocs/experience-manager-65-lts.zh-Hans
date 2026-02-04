---
title: 搜索流程实例
description: 使用“进程搜索”页可以输入用于查找进程实例的搜索标准。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e358ee51-c23f-4737-9dcf-3193ed541bbb
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# 搜索流程实例{#searching-for-process-instances}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

使用“进程搜索”页可以输入用于查找进程实例的搜索标准。 您可以从Forms Workflow页面访问“进程搜索”页面。 或者，您可以单击“流程实例”页面上的&#x200B;**搜索**。

您可以输入执行常规搜索的基本标准、执行详细搜索的特定属性或执行组合搜索的基本标准和特定属性的组合。

## 执行常规搜索 {#perform-a-general-search}

如果您知道流程实例的流程ID，则对流程进行常规搜索最为合适。 或者，如果您正在查找一组相关的进程实例，或者只有几个进程实例在运行。

输入执行常规搜索的基本条件。 如果输入多个条件，则使用隐含的AND条件执行搜索。

1. 在管理控制台中，单击服务> Forms Workflow >进程搜索。
1. 在“进程搜索”页的“常规搜索”下，提供以下条件：

   * **进程ID：**&#x200B;标识每个唯一进程实例的正整数。
   * **进程状态：**&#x200B;从列表中选择状态。
   * **应用程序：**&#x200B;从列表中选择应用程序。 仅显示已部署的应用程序。
   * **进程名称 — 版本：**&#x200B;从菜单中选择进程名称。 只显示已部署的进程。

1. 单击&#x200B;**搜索**。 此时将显示“流程实例”页，其中列出了找到的实例。

## 对进程执行详细搜索 {#perform-a-detailed-search-for-a-process}

您可以输入特定属性以执行详细搜索。 如果您有许多进程实例在运行，并且需要按特定条件缩小可能的查找范围，则详细搜索是最合适的。

1. 在管理控制台中，单击服务> Forms Workflow >进程搜索。
1. 在“进程搜索”页的“详细搜索”下，指定您的第一个标准集：

   * 在“属性”列表中，选择一个属性。
   * 在“筛选器”列表中，选择一个运算符。
   * 在“值”框中，键入适合所选属性的值。

1. 要添加另一行，请选择“更多筛选器”。 将显示另一组“属性”、“筛选器”和“值”列表，以及“条件”列表。
1. 在条件下，选择AND或OR。 根据需要重复步骤1 - 3，以进一步缩小搜索范围。
1. 要添加或删除行，请单击“更多筛选器”或“更少筛选器”。 一到四行即可。
1. 单击&#x200B;**搜索**。 此时将显示“流程实例”页，其中列出了找到的实例。

另请参阅[关于进程实例状态](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)。

## 对进程执行组合搜索 {#perform-a-combined-search-for-a-process}

要创建同时使用常规和详细标准的搜索，请在“进程搜索”页的两个区域中输入值。 系统在这两个区域之间应用隐含的`AND`。

如果搜索范围太窄，则找不到实例。
