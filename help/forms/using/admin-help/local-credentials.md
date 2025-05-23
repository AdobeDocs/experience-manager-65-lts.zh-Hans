---
title: 管理本地凭据
description: 了解如何使用信任存储区管理来管理本地凭据。 AEM forms支持标准PKCS12表单中的RSA和DSA凭据。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d297ab09-2b92-442a-8b19-ffee86e24bb9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 管理本地凭据 {#managing-local-credentials}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

本地凭据是在信任存储管理中托管的私钥凭据。 *本地凭据*&#x200B;标识用户的DES凭据的存储位置。 使用信任存储区管理，您可以使用例如现有的PFX文件导入和管理本地凭据，以便可以导入、编辑和删除本地凭据。

AEM forms支持采用标准PKCS12格式（.pfx和.p12文件）的最多4096位的RSA和DSA凭据。

您可以导入和导出任意数量的凭据。 如果要使用相同的别名替换过期的凭据，请删除该凭据，然后导入具有相同别名的新凭据。

有关Acrobat Reader DC扩展的信息和说明，请参阅[配置凭据以用于Acrobat Reader DC扩展](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 导入凭据 {#import-a-credential}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“本地凭据”。
1. 单击“导入”。 在“信任存储类型”下，选择以下选项之一：

   * **文档签名凭据：**&#x200B;用于在文档上颁发数字签名的凭据。
   * **Acrobat Reader DC扩展凭据：**&#x200B;特定于Acrobat Reader DC扩展的数字证书，允许在生成的PDF文档中激活Adobe Reader使用权限。
   * **默认值：**&#x200B;指示这是要与Acrobat Reader DC扩展一起使用的默认凭据。

   有关获取凭据的信息，请参阅[准备安装AEM表单](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf)。

1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC扩展和签名服务中凭据的显示名称。 此别名还用于使用AEM表单SDK以编程方式访问凭据。

   >[!NOTE]
   >
   >别名会自动转换为大写以便显示。 在进程中引用别名时，该别名不区分大小写。

1. 单击“浏览”以查找凭据，键入凭据的密码，然后单击“确定”。

   如果出现错误消息“由于文件格式不正确或密码不正确导致无法导入凭据”，请验证密码是否有效。

## 导出凭据 {#export-a-credential}

凭据将导出为PKCS#12格式的P12文件。

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“本地凭据”。
1. 单击要导出的凭据的别名，然后单击导出。
1. 在“密码”框中，键入密码。 此密码是新密码，用于加密导出的凭据。
1. 单击导出，按照说明导出凭据，然后单击确定。

## 编辑凭据的别名或信任存储类型 {#edit-a-credential-s-alias-or-trust-store-type}

导入凭据后，可以编辑其别名和信任存储类型。

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“本地凭据”。
1. 单击要编辑的凭据的别名。
1. 单击“更新凭据”。
1. 根据需要编辑别名及信任存储类型，然后单击“确定”。

## 删除凭据 {#delete-a-credential}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“本地凭据”。
1. 选中要删除的凭据对应的复选框。
1. 单击“删除”，然后单击“确定”。
