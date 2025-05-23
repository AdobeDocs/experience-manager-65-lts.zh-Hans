---
title: 为IBM&amp；reg；Content Manager配置连接器
description: 配置IBM&amp；reg； Content Manager的连接器，以启用AEM表单与IBM&amp；reg； Content Manager之间的通信。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 106f01a2-39fb-474b-8c58-5ab08666b918
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 为IBM® Content Manager配置连接器{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

适用于IBM® Content Manager的连接器支持在AEM Forms与IBM® Content Manager之间进行通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“Connectors for ECM”。

## 配置IBM®内容管理器连接 {#configure-the-ibm-content-manager-connection}

1. 在管理控制台中，单击服务>IBM连接器®内容管理器。
1. 在“数据存储名称”框中，输入要连接到的IBM® Content Manager数据存储的名称。 如果数据库是本地数据库，请输入数据库的名称。 如果数据库是远程数据库，请输入其别名。
1. 在“用户名”框中，输入将连接到IBM® Content Manager数据存储的用户的用户ID。
1. 在“密码”框中，输入用户的密码。
1. （可选）在“别名连接字符串”框中，输入其他连接参数。 通常，此框应为空。 有关更多信息，请参阅您的IBM®文档。
1. 单击“保存”。

## 验证服务设置 {#validation-of-service-settings}

如果输入的dataStore别名、用户名或密码不正确，则会获得以下结果，具体取决于IBM® Content Manager服务的Content Repository Connector是否正在运行：

* 如果服务已停止，则在保存服务配置信息时，不会出现任何错误。 但是，下次启动服务时，将会引发异常，并且服务不会启动。
* 如果服务已启动，则在保存服务配置信息时，服务会立即尝试验证凭据信息。 在这种情况下，会发生错误并且不会保存配置信息。
