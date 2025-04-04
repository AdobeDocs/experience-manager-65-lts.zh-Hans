---
title: 配置SSL的概述
description: 了解如何通过配置SSL增强通信的安全性。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2e81b9b9-321d-4423-9748-6385956b1d90
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 配置SSL的概述 {#overview-of-configuring-ssl}

您可以创建安全套接字层(SSL)凭据并在应用程序服务器上配置SSL，以增强与应用程序服务器通信的安全性。

作为安全产品，Rights Management需要配置SSL。 配置SSL证书时，请确保仅使用RSA密钥。 不支持包含DSA密钥的SSL证书。

提供的信息适用于交钥匙安装、自动安装和手动安装。 它提供了一个配置SSL的方法示例。 您也可以使用更适合您的网络或组织的其他方法。

>[!NOTE]
>
>建议您先完成AEM表单模块的安装、配置和部署，并确保产品在应用程序服务器中配置SSL之前正常运行。

>[!NOTE]
>
>创建SSL安全证书和凭据时，请使用与运行应用程序服务器相同的用户帐户权限。 如果使用其他用户权限运行应用程序服务器，则当ContentRootURI指向https时，表单可能无法正确呈现为PDForm呈现形式。

如果您具有启用了SSL的LDAP服务器，请配置“用户管理”以与它配合使用。 （请参阅[为启用SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。）
