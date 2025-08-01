---
title: 管理证书和凭据的基础知识
description: 了解管理证书和凭据的基础知识。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 8aeacdb7-68a7-476f-a725-f9ad7406cc9c
source-git-commit: 02b9eb98d1fdf1b090166a6ae7c0a4379487d2e1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 管理证书和凭据的基础知识 {#basics-of-managing-certificates-and-credentials}

*凭据*&#x200B;包含签名或识别文档所需的私钥信息。 *证书*&#x200B;是您为信任配置的公钥信息。 AEM Forms将证书和凭据用于多种用途：

* Acrobat Reader DC扩展使用凭据在PDF文档中启用Adobe Reader使用权限。 （请参阅[配置凭据以用于Acrobat Reader DC扩展](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。）
* 您可以将Rights Management配置为仅显示凭据以便在Acrobat中使用，这些凭据来自可信发布者。 (请参阅[配置Rights Management显示设置](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)。)证书中必须存在公用名(CN)。
* 签名服务访问证书和凭据。 有关签名服务的详细信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_65)。

**正在生成对密钥**

AEM Forms使用信任存储区来存储和管理证书、凭据和证书吊销列表(CRL)。 此外，您可以使用独立的Hardware Security Module (HSM)设备存储私钥。

AEM forms不提供任何用于生成密钥对的选项。 但是，您可以使用Java keytool等工具生成它，并将其导入AEM Forms信任存储区。 有关Java keytool的详细信息，请参阅以下内容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

以下签名类型受支持，可以在AEM表单中导入：

* XML签名
* XMLTimeStampToken
* RFC 3161时间戳令牌
* PKCS#7
* PKCS#1
* DSA签名

**处理丢失或泄露的密钥**

如果您怀疑您的密钥已丢失或已被泄漏，请采取以下措施：

1. 通知证书颁发机构，以便他们将损坏的密钥添加到证书撤销列表以撤销该密钥。
1. 从证书颁发机构获取新密钥及其证书。
1. 使用新密钥再次签署使用泄露密钥签署的文档。
