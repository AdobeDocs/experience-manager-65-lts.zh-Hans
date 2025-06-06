---
title: 导入和导出全局设置
description: 您可以导入和导出Workspace的搜索模板定义和全局设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f5b45667-87df-4069-8f08-2b6daf4bad1e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# 导入和导出全局设置 {#importing-and-exporting-global-settings}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以导入和导出Workspace的搜索模板定义和全局设置。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

例如，您可以通过导出一个环境中的搜索模板定义和全局设置并将它们导入另一个环境，来从开发环境移动到生产环境。

导出全局设置文件后，可以在XML或文本编辑器中修改设置。 但是，您可能只想编辑JChannelConnectionProperties、formViewOnly和specialRoutes设置。 有关详细信息，请参阅[Workspace全局设置](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果更改全局设置文件中的事件属性，则必须重新启动服务器。

## 导入搜索模板定义 {#import-a-search-template-definition}

1. 在管理控制台中，单击服务> Workspace >全局管理。
1. 在“导入搜索模板定义”框下，单击“选择文件”并选择搜索模板。 您只能导入最初从Workspace实例导出的搜索模板定义。
1. 单击“导入”。

## 导出搜索模板定义 {#export-a-search-template-definition}

1. 在“全局管理”页面的“导出搜索模板”定义下，单击“列出全部”。
1. 在搜索模板列表中，选择要导出的模板。

   >[!NOTE]
   >
   >您可以选择多个模板，但只导出最后选择的模板。

1. 单击导出，然后将文件保存在计算机上。

## 导入全局设置 {#import-global-settings}

1. 在“全局管理”页的“导入全局设置”下，单击“选择文件”并选择全局设置文件。 全局设置文件必须采用XML格式。
1. 单击“导入”。

## 导出全局设置 {#export-global-settings}

1. 在“全局管理”页面的“导出全局设置”下，单击“导出”。
1. 将文件保存在计算机上。

## Workspace全局设置 {#workspace-global-settings}

您可以修改全局设置文件；但是，您可能只想编辑JChannelConnectionProperties、formViewOnly和specialRoutes设置。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

Workspace全局设置文件包含以下设置：

### specialRoutes设置 {#specialroutes-settings}

*specialRoutes*&#x200B;设置在Workspace中指定特殊路由的属性，即批准和拒绝。 在某些情况下，这些路由的按钮会显示在Workspace的任务卡上，用户无需打开表单即可选择它们。 可以修改全局设置文件中的specialRoutes设置，以添加用于批准和拒绝的自定义名称或创建其他路由。

**client_specialRoutes_routes_approve_style：** Workspace主题中用于标识批准按钮图标的样式的名称。 样式必须包含启用图标和禁用图标的值。 要定义自定义按钮的样式，必须使用以下模板：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Workspace CSS文件嵌入在workspace-theme.swf文件中，该文件位于adobe-workspace-client.ear > adobe-workspace-client.war文件中。 要更改Workspace的外观，必须重新编译workspace-theme.swf文件。

**client_specialRoutes_routes_deny_names：** Workbench用户可以用来解释为“拒绝”的字符串类型。 这些字符串区分大小写。 例如，默认值为deny。 如果Workbench用户在进程中使用“拒绝”一词，则无法识别该词。 必须将“拒绝”一词添加到此设置中，才能自定义路由按钮并将样式应用于该按钮。

**client_specialRoutes_routes_deny_style：** Workspace主题文件中用于标识拒绝按钮图标的样式名称。 样式必须包含启用图标和禁用图标的值。 要定义自定义按钮的样式，必须使用以下模板：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names：** Workbench用户可以用来解释为“approve”的各种字符串。 这些字符串区分大小写。 例如，默认值为approve。 如果Workbench用户在流程中使用了“批准”一词，则无法识别该词。 必须将“批准”一词添加到此设置中，才能自定义路由按钮并将样式应用于该按钮。

**client_specialRoutes_names：**&#x200B;用于从资源文件中查找自定义字符串值的密钥。 此设置中的每个条目都需要包含名称和样式的值。

### JGgroup设置 {#jgroup-settings}

仅当您从Adobe LiveCycle ES 2.5或更早版本升级过时，才会显示这些设置。

**server_remoteevents_ClientTimeoutMilliseconds：** JGroup等待事件消息的最长时间。 此设置不应更改。

**server_remoteevents_ServerTimeoutMilliseconds：**&#x200B;在服务器上接收JGroup消息的超时。 此选项设置从服务器向客户端发送消息的延迟。

**server_remoteevents_JChannelConnectionProperties：** JGroup的连接属性，用于在RemoteEvent服务处理某个服务事件的服务器与Workspace的所有实例之间进行通信。

您可能需要更改多播IP地址(mcast_addr)、多播IP端口(mcast_port)和多播数据包TTL (ip_ttl)的UDP值。 默认情况下，多播IP地址和端口值是随机生成的，通常不需要更改这些值。 但是，如果贵公司对于多播IP地址的特定多播范围具有任何网络策略，则可能需要更改这些值。

>[!NOTE]
>
>TTL必须大于群集中的服务器之间的网络交换机数；但是，如果该值设置得过高，则可能导致多播数据包进入子网，并在子网中被丢弃。

不应更改此设置中的其余属性。

**server_remoteevents_JGroupName：**&#x200B;用于远程事件通信的JGroup的名称。 此值是随机生成的，以避免群集中的冲突。 此值不应更改。

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### formView设置 {#formview-settings}

**client_formView_openFormInFullScreen：**&#x200B;若要以全屏模式显示Workspace中的所有表单，请将此选项设置为true。 默认情况下，此选项设置为false，表单不会以全屏模式显示。 User服务包含一个选项，用于在全屏模式下打开与任务关联的文档。 这使您能够基于每个进程来控制显示。

**client_routes_formViewOnly：**&#x200B;设置为True时，路由不会显示在Workspace的卡片视图或列表视图中。 默认值为False，表示路由显示在卡片视图和列表视图中。

### 其他设置 {#other-settings}

**client_mimeTypes_openOutsideBrowser：**&#x200B;在Workspace浏览器实例外部打开的文档的MIME类型。 如果贵组织的流程需要额外的MIME类型，请在此处指定。 默认值为：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching：**&#x200B;缓存自定义任务用户界面。

**server_debugLevel：**&#x200B;不更改此设置。

**client_pollingInterval：**&#x200B;设置(JEE上的AEM表单已弃用) Flex Workspace上使用的轮询间隔（以秒为单位）以检测新任务和修改的任务。 默认值为3秒。 这在AEM Forms Workspace中不起作用。

**client_systemContext_name：**&#x200B;指定要在AEM Forms Workspace中任务附件的“添加者”字段（在“附件”选项卡中）中显示的自定义名称（例如“公民”）。

要定义自定义名称，请执行以下操作：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>对于Demo应用程序，默认显示名称为&#x200B;**公民**。 对于您创建的自定义应用程序，默认显示名称为&#x200B;**系统上下文帐户**。
>
>**client_idleTimeout：**&#x200B;当用户保持不活动状态特定时间后，AEM Forms Workspace会话将过期。 要启用该功能，请将一个条目添加到全局设置&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>中。 您可以指定值0来禁用空闲超时。 时间量以秒为单位指定。
