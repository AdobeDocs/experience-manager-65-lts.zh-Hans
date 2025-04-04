---
title: 在Windows Vista上配置SSL
description: 了解如何在Windows Vista上配置SSL。 使用并运行Java Keytool生成包含RSA密钥的SSL证书以进行身份验证。
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ee73f6a1-712c-461f-95e8-85f8c5694293
source-git-commit: d0f29cb177e98315cd50c2d7e96c3605eec14885
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 在Windows Vista上配置SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要具有RSA密钥的SSL证书以进行身份验证。 可以使用Java keytool创建证书。

>[!NOTE]
>
>Windows Vista不能使用DSA密钥。

您可以使用包含创建证书和密钥库所需的所有信息的单个命令来运行keytool。

**创建SSL证书**

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin并键入以下命令以创建证书和密钥库：

   `keytool -genkey -keyalg RSA -dname "CN=`*主机名* `, OU=`*组名* `, O=`*公司名* `,L=`*城市名* `, S=`*省/市* `, C=`*国家/地区代码* `" -alias`*&quot;LC证书&quot;* `-keypass` `key`*_* *密码* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 键入`changeit`作为密码。 此密码是Java安装的默认密码，系统管理员可能已更改此密码。
