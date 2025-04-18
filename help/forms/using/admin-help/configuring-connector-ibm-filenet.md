---
title: 为IBM FileNet配置连接器
description: 了解如何配置IBM FileNet的连接器，以启用AEM Forms与IBM FileNet之间的通信。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORM
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 5cbb626c-fcd8-4936-acf8-95bac80d06b6
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# 为IBM FileNet配置连接器 {#configuring-connector-for-ibm-filenet}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

IBM FileNet连接器支持AEM Forms与IBM FileNet之间的通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“Connectors for ECM”。

>[!NOTE]
>
>在早期版本中，资产可以存储在ECM存储库中。 在此版本中，资产存储在AEM表单本地存储库中，并且存储库提供程序服务已被弃用。 当您升级到AEM表单时，会将资源从ECM存储库迁移到AEM表单存储库。 有关详细信息，请参阅适用于您的应用程序服务器的AEM表单升级指南。

## 配置与内容引擎的连接 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine提供了软件服务，用于管理FileNet内容存储库中的企业内容和客户定义的业务对象。

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 在“内容引擎URL”框中，输入完整的连接URL。 例如：

   如果正在将FileNet Content Engine 4.x与CEWS传输一起使用，请输入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果将FileNet Content Engine 4.x与EJB传输一起使用（只有WebLogic支持），请输入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在“凭据保护方案”列表中，选择以下保护级别之一：

   * **清除：**&#x200B;以无保护模式通过网络发送凭据
   * **对称：**&#x200B;通过网络发送加密的凭据

1. 在“加密文件位置”框中，输入加密文件的路径：

   * 如果选择Clear作为凭据保护方案，则会忽略此关键字及其值。
   * 如果选择Symmetric作为凭据保护方案，则输入的路径指向Forms Server上包含要使用的加密密钥的加密文件的位置。

1. 在默认对象存储框中，输入AEM Forms默认连接到的对象存储连接器。
1. 在“用户名”框中，输入具有您在上一步中指定的默认对象存储访问权限的用户的用户名。
1. 在“密码”框中，输入用户的密码，然后单击“保存”。

## 配置进程引擎设置 {#configure-the-process-engine-settings}

IBM FileNet的连接器包含IBM FileNet服务的Process Engine Connector ，用于与IBM FileNet Process Engine交互。 您可以配置此服务的设置。

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 要启用将Process Engine Connector用于IBM FileNet服务，请选择“使用Process Engine Connector服务”。
1. 在“Process Router/Connection Point（进程路由器/连接点）”框中，输入主机名或IP地址和端口号，然后输入进程路由器的名称。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在“用户名”框中，输入用于连接到进程引擎的用户名。
1. 在“密码”框中，输入用于连接进程引擎的密码，然后单击“保存”。

## 验证服务设置 {#validation-of-service-settings}

如果在配置与内容引擎的连接或流程引擎设置时输入了错误的用户名或密码，则根据服务当前是否正在运行，将获得以下结果：

* 如果IBM FileNet的存储库提供程序服务和IBM FileNet的Content Repository Connector服务都已停止，则在保存服务配置信息时，不会出现任何错误。 但是，下次启动服务时，将会引发异常，并且服务不会启动。
* 如果启动了IBM FileNet的存储库提供程序服务或IBM FileNet的Content Repository Connector ，则在保存服务配置信息时，该服务将立即尝试验证凭据信息。 在这种情况下，会发生错误并且不会保存配置信息。

## 更改存储库服务提供程序 {#change-the-repository-service-provider}

您可以配置要与FileNet一起使用的存储库服务提供程序。 存储库服务调用已委派给您配置的提供程序。

以下选项可供选择：

**当前存储库提供程序名称：**&#x200B;当前存储库服务提供程序的名称

**IBM FileNet存储库提供程序：**&#x200B;使FileNet存储库提供程序成为存储库的提供程序。 此选项已弃用。

**存储库提供程序：**&#x200B;使本地存储库提供程序成为存储库的提供程序

>[!NOTE]
>
>要选择除列出的系统信息库服务提供程序之外的其他系统信息库服务提供程序，请在应用程序和服务中配置RepositoryService。<!-- Fix broken link(See Managing Services) -->

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 在“存储库服务提供程序信息”区域中，选择替代存储库服务提供程序，然后单击“保存”。
