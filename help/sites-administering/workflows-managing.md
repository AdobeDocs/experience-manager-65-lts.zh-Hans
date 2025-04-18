---
title: 管理对工作流的访问权限
description: 了解如何根据用户帐户配置访问控制列表，以允许（或禁用）启动和参与工作流。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 084c59b1-1e72-475e-8ec9-2cbc6e695876
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# 管理对工作流的访问权限{#managing-access-to-workflows}

根据用户帐户配置ACL以允许（或禁用）启动和参与工作流。

## 工作流所需的用户权限 {#required-user-permissions-for-workflows}

在下列情况下，可以对工作流执行操作：

* 您使用的是`admin`帐户
* 该帐户已分配给默认组`workflow-users`：

   * 此组拥有用户执行工作流操作所需的所有权限。
   * 当帐户处于此组中时，它仅有权访问已启动的工作流。

* 该帐户已分配给默认组`workflow-administrators`：

   * 此组拥有特权用户监视和管理工作流所需的所有权限。
   * 当帐户在此组中时，它可以访问所有工作流。

>[!NOTE]
>
>这些是最低要求。 您的帐户还必须为已分配参与者或已分配组的成员，才能执行特定步骤。

## 配置对工作流的访问权限 {#configuring-access-to-workflows}

工作流模型继承了用于控制用户如何与工作流交互的默认访问控制列表(ACL)。 要自定义工作流的用户访问权限，请在存储库中为包含工作流模型节点的文件夹修改访问控制列表(ACL)：

* [将特定工作流模型的ACL应用于/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中创建子文件夹并将ACL应用于该子文件夹](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有关使用CRXDE Lite配置ACL的信息，请参阅[访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 将特定工作流模型的ACL应用于/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型存储在`/var/workflow/models`中，则您可以在文件夹上分配一个特定的ACL（仅与该工作流相关）：

1. 在Web浏览器中打开CRXDE Lite(例如，[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，为工作流模型文件夹选择节点：

   `/var/workflow/models`

1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 在&#x200B;**本地访问控制策略** （**访问控制列表**）表中，单击加号图标以&#x200B;**添加条目**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，添加具有以下属性的ACE：

   * **主体**： `content-authors`
   * **类型**：`Deny`
   * **权限**： `jcr:read`
   * **rep：glob**：对特定工作流的引用

   ![wf-108](assets/wf-108.png)

   **访问控制列表**&#x200B;表现在包含`prototype-wfm-01`工作流模型上`content-authors`的限制。

   ![wf-109](assets/wf-109.png)

1. 单击&#x200B;**全部保存**。

   `prototype-wfm-01`工作流不再适用于`content-authors`组成员。

### 在/var/workflow/models中创建子文件夹并将ACL应用于该子文件夹 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您的[开发团队可以在子文件夹](/help/sites-developing/workflows-models.md#creating-a-new-workflow)中创建工作流

`/var/workflow/models`

类似于存储在下的DAM工作流

`/var/workflow/models/dam/`

然后，您可以将ACL添加到文件夹本身。

1. 在Web浏览器中打开CRXDE Lite(例如，[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，为工作流模型文件夹中的单个文件夹选择节点；例如：

   `/var/workflow/models/prototypes`

1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 在&#x200B;**适用的访问控制策略**&#x200B;表中，单击加号图标以&#x200B;**添加**&#x200B;条目。
1. 在&#x200B;**本地访问控制策略** （**访问控制列表**）表中，单击加号图标以&#x200B;**添加条目**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，添加具有以下属性的ACE：

   * **主体**： `content-authors`
   * **类型**：`Deny`
   * **权限**： `jcr:read`

   >[!NOTE]
   >
   >与[将特定工作流模型的ACL应用于/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)一样，您可以包含rep：glob以限制对特定工作流的访问。

   ![wf-110](assets/wf-110.png)

   **访问控制列表**&#x200B;表现在包含`prototypes`文件夹上`content-authors`的限制。

   ![wf-111](assets/wf-111.png)

1. 单击&#x200B;**全部保存**。

   `prototypes`文件夹中的模型对`content-authors`组的成员不再可用。
