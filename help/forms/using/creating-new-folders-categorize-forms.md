---
title: 创建新文件夹以对表单进行分类
description: 使用文件夹组织您的表单模板、PDF、资源和自适应表单。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: cc84c92b-d1a3-4314-a079-7dcbf013712a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 创建新文件夹以对表单进行分类 {#create-new-folders-to-categorize-forms}

您可以使用文件夹更好地组织资源。 由于AEM Forms支持多种类型的资源（表单模板、PDF、文档、资源和自适应表单以及各种元数据），因此您可以使用文件夹根据所需的标准对表单进行分类。

AEM Forms允许您更改文件夹的标题。 标题与存储库中存储文件夹的节点名称不同。 相反，标题将保留为文件夹的元数据。 如果更改文件夹的标题，则该文件夹中存在的任何资源的路径都不会受到影响。

## 创建文件夹 {#create-a-folder}

您可以通过以下方式之一在AEM Forms中创建文件夹：

* 上传包含所需文件夹结构中的资源的ZIP文件(请参阅[在AEM Forms中获取XDP和PDF文档](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 创建空文件夹

1. 登录到`https://<server>:<port>/aem/forms.html`上的AEM Forms用户界面。
1. 导航到要创建文件夹的位置。
1. 单击工具栏中的![aem6forms_add](assets/aem6forms_add.png)图标，然后选择&#x200B;**[!UICONTROL 创建文件夹]**。

1. 输入以下详细信息：

   * **标题：**&#x200B;文件夹的显示名称
   * **名称：** *（必需）*&#x200B;要将文件夹存储在存储库中的节点名称

   >[!NOTE]
   >
   >默认情况下，“名称”字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择使用建议的名称继续操作或进一步编辑它。

1. 单击&#x200B;**[!UICONTROL 提交].**

   具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

   如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以将鼠标悬停在名称字段旁边显示的错误![aem6forms_error_alert](assets/aem6forms_error_alert.png)图标上，以查看错误消息。

### 编辑文件夹标题 {#edit-the-folder-title-br}

1. 选择要编辑其标题的文件夹。
1. 单击工具栏中的编辑![aem6forms_edit](assets/aem6forms_edit.png)图标。
1. 输入新标题。 该文本字段已预填充为文件夹标题的当前值。 您可以将其更改为新值。
1. 单击&#x200B;**[!UICONTROL 提交].**
