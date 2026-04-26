---
title: 管理流程
description: “进程列表”页显示用户已启动或自动启动的进程。 了解有关管理流程的更多信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6459abd5-6341-4c28-a747-bde9a91e3a88
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# 管理流程 {#managing-processes}

“进程列表”页显示用户已启动或自动启动的进程。

1. 在管理控制台中，单击服务> Forms工作流> Forms工作流。 “进程列表”显示以下信息：

   **进程名称 — 版本：**&#x200B;在Workbench中定义的进程名称。

   **应用程序：**&#x200B;进程所属的应用程序，如Workbench中所定义。

   **状态：**&#x200B;活动表示进程是为进程版本激活的进程。 “不活动”表示该进程是一个旧版本，它仍具有进程实例。

   **创建日期：**&#x200B;部署进程的日期和时间。

1. 单击进程名称可在“进程实例”页上查看其进程实例。

## 使用流程实例 {#working-with-process-instances}

如果从“进程列表”页访问“进程实例”页，则会列出所选进程的所有进程实例。 如果在执行搜索后访问“进程实例”页，则只列出找到的进程实例。

对于每个流程实例，该列表显示了以下信息：

**进程ID：**&#x200B;实例化进程（即用户或自动步骤启动进程时）时，表单工作流分配的标识符。 您可以使用此标识符来跟踪流程实例的整个生命周期。

**进程名称 — 版本：**&#x200B;在Workbench中定义的进程名称。

**状态：**&#x200B;指示进程实例是正常运行、状态更改还是已停止。 （请参阅关于流程实例状态。）

**创建日期：**&#x200B;创建进程实例的日期和时间。

**更新日期：**&#x200B;上次更改进程实例状态的日期和时间。

您可以在“流程实例”页上执行以下任务：

* 选择进程实例可查看有关它的详细信息，如它的操作和子进程。 选择流程实例后，将显示“流程实例详细资料”页。
* 暂停、取消暂停或终止进程实例。
* 搜索流程实例。 要开始搜索，请单击“搜索”。

### 关于流程实例状态 {#about-process-instance-statuses}

流程实例（包括子流程）可以具有以下状态：

**完成：**&#x200B;进程实例中的所有分支和操作都已完成。 “完成”是流程实例的最终状态。

**正在完成：**&#x200B;进程实例的状态将更改为“完成”。

**INITIATED：**&#x200B;进程实例已创建，但尚未运行。 INITIATED是流程实例的第一个状态。

**正在运行：**&#x200B;进程实例运行正常。 可能正在进行自动步骤，或者流程实例可能正在接收用户输入或等待用户交互。

**已挂起：**&#x200B;进程实例已由管理员或进程中的某个步骤挂起。 在状态更改之前，不会执行任何进一步的操作。

**正在挂起：**&#x200B;状态将更改为“已挂起”。 如果某个操作被设计为忽略挂起请求并且尚未完成，则该操作必须在进程实例挂起之前完成。

**已终止：**&#x200B;管理员已终止进程实例。

**正在终止：**&#x200B;状态将更改为TERMINATED。 如果某个操作被设计为忽略终止请求且尚未完成，则该操作必须在终止进程实例之前完成。

**取消暂停：**&#x200B;暂停后，状态将更改为“正在运行”。

>[!NOTE]
>
>当请求更改进程实例的状态（例如挂起或终止）时，该请求将进入forms workflow命令队列。 根据队列的大小和整体处理速度，显示的状态在重新加载页面一次或更多次之前可能不会更改。

### 暂停或取消暂停进程实例 {#suspend-or-unsuspend-process-instances}

如果您需要排除问题，或者您知道流程实例在后续步骤中会因某些外部条件而遇到问题，则可以临时挂起流程实例。

可以挂起状态为“正在运行”的进程实例。

After you suspend a process instance, its status changes to SUSPENDING, then SUSPENDED, and the process pauses at its current operation. The process instance remains in this status until the status is changed to UNSUSPENDED.

Only process instances that have a status of SUSPENDED can be changed to UNSUSPENDED.

When you unsuspend a process instance, its status changes to RUNNING, and it continues with the operation where it had been suspended.

When you suspend a process instance that has invoked other processes (child processes) using their invoke operation, the child processes are also suspended.

1. 在管理控制台中，单击服务> Forms工作流> Forms工作流。
1. On the Process Instance page, select the process and click Suspend or Unsuspend.

### Terminate a process instances {#terminate-a-process-instances}

If an operation of a process instance has stalled or encountered some other error condition, or if you need to force a process instance to stop running, you can terminate the process instance.

You can terminate process instances that have any status.

When you terminate a process instance, its status changes to TERMINATING, then TERMINATED, and the process stops at its current operation. No further operations are run, and all associated operations and tasks are terminated.

1. 在管理控制台中，单击服务> Forms工作流> Forms工作流。
1. On the Process Instance page, select the process and click Terminate.

## Working with process instance details {#working-with-process-instance-details}

The Process Instance Detail page shows the history of a process instance.

The Summary area shows basic information about the process instance.

On the Operations tab, each operation for the process instance is shown in order of completion from first to last with the following information:

**Operation Name:** The name of the operation, as defined in Workbench.

**Status:** Indicates whether the operation is running normally or has stopped. （请参阅关于流程实例状态。）

**Branch Name:** The name of the branch, as defined in Workbench.

**Start Date:** The date and time the operation started.

**Completed Date:** The date and time the operation completed.

A subprocess is a process instance that is started by another process and runs independently of that other process. 仅当子流程在Workbench中作为流程的一部分进行设计时，才会显示它们。 在“子流程”选项卡上，每个子流程均显示以下信息：

**进程ID：**&#x200B;此正整数，在实例化进程（即，当用户或自动步骤启动进程时）时形成Workflow分配。 您可以使用此标识符跟踪流程实例的生命周期。

**进程名称 — 版本：**&#x200B;在Designer中定义的进程名称。

**状态：**&#x200B;指示进程实例是正常运行、正在更改状态还是已停止。 （请参阅关于流程实例状态。）

**创建日期：**&#x200B;子进程的创建日期和时间。

**更新日期：**&#x200B;上次更改子进程的状态的日期和时间。

您可以在“流程实例详细信息”页面上执行以下任务：

* 选择一个操作以查看其详细信息。 选择操作后，将显示“操作详细信息”页。
* 选择一个子进程以查看其详细信息。 选择子进程后，将显示“进程实例详细资料”页。
* 终止或重试操作或子进程，具体取决于它们的状态。

### 关于操作状态 {#about-operation-statuses}

操作（流程中的步骤）可以具有以下状态：

**完成：**&#x200B;操作已完成。

**正在运行：**&#x200B;操作运行正常。 它可能正在接收用户输入或等待用户交互，或者可能正在进行自动步骤。

**已停止：**&#x200B;处理操作时出现问题。 在“停止的操作”页面中检查错误或异常。

**已终止：**&#x200B;管理员已终止操作。

### 终止操作或子进程 {#terminate-operations-or-subprocesses}

如果操作或子进程停止或遇到其他错误情况，或者需要强制操作或子进程停止运行，则可以终止操作。

You can terminate an operation that is RUNNING.

When you terminate an operation, its status changes to TERMINATED. The operation does not complete and the process instance stops running.

You can terminate a subprocess that has any status.

When you terminate a subprocess, its status changes to TERMINATING, then TERMINATED, and the process instance stops at its current operations. No further operations are run in the subprocess, although the parent process instance continues to run.

You cannot terminate processes that have gateway elements in the process diagram. If you attempt to terminate these types of processes, the operations within the gateway elements are not affected. To terminate operations that are within a gateway element, you must terminate the operations directly.

1. On the Process Instance Details page, click the Operations tab or the Subprocesses tab.
1. Select the operation or subprocess and click Terminate.

### Retry an operation {#retry-an-operation}

You can retry operation that has a status of STALLED.

When you retry an operation, Forms workflow is sent a request to restart the operation. If the request is successful, the status changes to RUNNING. If the operation cannot be restarted, it remains STALLED, and you may need to terminate it.

1. On the Process Instance Details page, click the Operations tab.
1. Select the operation and click Retry.

## Working with operations {#working-with-operations}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

The Operation Details page shows a summary of one operation in a process and its current user assignments.

1. 在管理控制台中，单击服务> Forms工作流> Forms工作流。
1. Click a process name to display its process instances. Click a process instance to display the Process Instance Details page, then select an operation to display the Operation Detail page.

   For each task, the list shows the following information:

   **进程名称 — 版本：**&#x200B;在Workbench中定义的进程名称。

   **应用程序：**&#x200B;进程所属的应用程序，如Workbench中所定义。

   **状态：**&#x200B;活动表示进程是为进程版本激活的进程。 “不活动”表示该进程是一个旧版本，它仍具有进程实例。

   **创建日期：**&#x200B;部署进程的日期和时间。
