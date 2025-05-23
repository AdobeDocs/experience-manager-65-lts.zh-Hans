---
title: 在页面中嵌入链接组件
description: 您可以使用链接组件从任何页面链接自适应文档或自适应表单。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: a6ae1633-63a8-4364-b298-bc569459a136
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 在页面中嵌入链接组件{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

链接组件是Document Services类别的成员。 确保Document Services类别在AEM组件浏览器中可见。 如果未列出该类别，请按照[启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)中列出的步骤操作。

## 链接组件 {#link-component}

利用链接组件，表单门户作者可在页面上的任何位置创建指向自适应表单的链接。 链接组件在组件浏览器的“文档服务”部分中提供。

执行以下步骤以将链接组件添加到页面：

1. 将&#x200B;**Link**&#x200B;组件拖动到页面上。 选择该组件并选择![cmppr](assets/cmppr.png)。 这将打开编辑链接组件对话框。

   ![edit-link-component](assets/edit-link-component.png)

1. 在&#x200B;**显示**&#x200B;选项卡中，指定以下内容：

   * **链接标题**：链接的链接文本或标题。
   * **链接工具提示**：链接的工具提示。
   * **布局模板**：链接组件布局的模板。

1. 打开&#x200B;**资源信息**&#x200B;选项卡并指定资源的类型。 资产可以是&#x200B;**表单**。 根据所选资产类型，将显示以下选项：

   * **资源路径**：存储资源的存储库路径。

   * **渲染类型**：渲染格式 — PDF、HTML或Auto。 自动渲染类型会检测用户环境，并相应地将表单渲染为HTML或PDF。 例如，如果从移动设备访问表单，则自动渲染类型将在HTML中渲染表单。
   * **将URL：** URL提交到提交表单数据的Servlet。
   * **HTML配置文件**：用于将表单渲染为HTML的配置文件。
   * **PDF配置文件**：用于将表单渲染为PDF文档的配置文件。

1. 打开&#x200B;**高级**&#x200B;选项卡。 可用键值对格式指定其他参数。 单击链接时，这些附加参数将与表单一起传递。

   选择&#x200B;**完成**&#x200B;以保存配置。

## 使用链接组件的最佳实践 {#best-practices-for-using-link-component-br}

* 如果在“表单路径”中指定的路径指向文档，且该文档具有PDF作为其允许的渲染格式，请确保选择PDF作为渲染类型。
* 可以在多个位置指定表单的提交URL，其优先顺序如下：

   1. 表单中嵌入的提交URL（在提交按钮中）具有最高优先级。
   1. Forms Manager中提到的提交URL具有中优先级。
   1. Forms Portal中提到的提交URL的优先级最低。
