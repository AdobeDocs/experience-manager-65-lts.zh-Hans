---
title: 将任务或表单另存为草稿
description: 在AEM Forms应用程序中保存任务或表单草稿副本的步骤
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 25dba5c5-0f27-457a-935b-c451e0bf5241
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 将任务或表单另存为草稿 {#saving-a-task-or-form-as-a-draft}

另存为草稿选项保存任务或表单的快照以及在相关表单中填写的数据。 您也可以从模板创建草稿。 草稿将保存在移动设备中，并与Adobe Experience Manager Forms服务器同步，以供日后检索。

您可以[更新表单](/help/forms/using/working-with-form.md)，[用照片和涂鸦笔记为表单](/help/forms/using/add-attachments.md)添加批注。 在继续更新表单时，建议将其另存为草稿。 对于您决定稍后提交已填写表单的情况，将其另存为草稿会很有帮助。

要为表单门户上保存的表单启用另存为草稿功能，请参阅[将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md)。
要配置自适应表单的提交，请参阅[草稿和提交组件](/help/forms/using/draft-submission-component.md)。 (对于与AEM Forms JEE服务器同步的表单无效。)

要创建草稿，请打开窗体并选择&#x200B;**另存为草稿** ![另存为草稿](assets/save-as-draft.png)。 提供草稿的名称，然后选择&#x200B;**保存**。 草稿将保存在“草稿”文件夹中，并与服务器同步。 如果应用程序处于离线状态，则该文件夹会保存在Outbox文件夹中。

如果之后更新相应的表单，更改会立即反映出来。 将AEM Forms应用程序与AEM Forms服务器同步时，草稿会上传到AEM Forms服务器。 此外，草稿会从“发件箱”移至“任务”或“草稿”文件夹。 其旁边将显示一个编辑图标。

当您继续处理多个任务和起点并保存它们时，草稿将被保存。 每次将应用程序与AEM Forms服务器同步时，草稿都会保存到服务器上。 它确保您随时可以根据上次保存的日期和时间恢复草稿。 例如，如果您重新安装应用程序或更改移动设备，则可以从服务器下载草稿。

## 删除草稿 {#delete-a-draft}

草稿文件夹列出了所有草稿。 您可以使用“删除草稿”选项从移动设备和服务器中永久删除草稿。

删除从任务创建的草稿的选项不可用。 删除从任务创建的草稿时，该任务将被放弃。

您可以在脱机模式和联机模式下放弃草稿。 在脱机模式下放弃草稿时，仅当与服务器的连接恢复时，才会从服务器中删除草稿。

执行以下步骤可删除草稿：

1. 在AEM Forms应用程序中，导航到&#x200B;**Forms。**
1. 从“搜索”旁边的下拉列表中选择&#x200B;**草稿**。
1. 带有编辑图标![edit-draft-app](assets/edit-draft-app.png)的表单表示草稿。 选择拔模旁边的水平省略号。
1. 在您选择水平省略号时显示的选项中，选择&#x200B;**删除草稿**。
