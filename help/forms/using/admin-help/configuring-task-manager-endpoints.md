---
title: 配置任务管理器端点
description: 了解如何配置Task Manager端点以调用服务。 配置Task Manager端点需要不同的设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 57fd8b5d-6347-4b83-9489-e8ee59ee39a5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 配置任务管理器端点 {#configuring-task-manager-endpoints}

任务管理器端点使Workspace用户能够调用该服务。

**任务管理器终结点设置**

使用以下设置配置任务管理器端点。

**Name：** （必需）标识终结点。 该名称会显示在Workspace的卡片视图中。 不要包含&lt;字符，因为它将截断Workspace中显示的名称。 如果您输入URL作为端点的名称，请确保它符合RFC1738中指定的语法规则。

**描述：**&#x200B;终结点的描述。 不要包含&lt;字符，因为它将截断Workspace中显示的描述。

**任务说明：**&#x200B;启动此工作流的用户的说明。

**进程所有者：**&#x200B;负责进程的人员的姓名。

**用户可以转发任务：**&#x200B;允许用户转发初始任务。

**显示附件窗口：**&#x200B;允许用户查看附件窗口。

**允许添加附件：**&#x200B;允许用户添加附件和注释。

**最初锁定的任务：**&#x200B;锁定初始任务。

**为共享队列添加ACL：**&#x200B;初始任务是为共享队列用户创建的ACL。

**分类：**（必需）用户将在Workspace中看到表单的类别。 从列表中选择一个类别，或选择“新建类别”以添加类别。

**操作名称：** （必需）可分配给终结点的操作列表。
