---
title: 为JBoss Application Server配置SSL (AEM 6.5 LTS JEE)
description: 了解如何为JBoss应用程序服务器配置SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 86d6d0f7b6fe1c36349f29e45a3eee31b04e5e80
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---


# 为JBoss Application Server配置SSL (AEM 6.5 LTS JEE)

## 概述

要在运行在Java EE上的Adobe Experience Manager (AEM) 6.5 LTS的JBoss Application Server上配置SSL，必须启用安全HTTPS通信。 启用SSL将对客户端和服务器之间交换的数据进行加密，使其成为任何生产AEM Forms部署的关键安全要求。

该过程包括两个主要阶段：

- **获取SSL凭据** — 通过生成自签名证书或从证书颁发机构(CA)请求证书。
- **在JBoss上启用SSL** — 通过JBoss CLI命令使用Elytron子系统。

在本指南中，使用了以下占位符值：

- `[appserver root]` — 运行AEM Forms的JBoss应用程序服务器的主目录。
- `[type]` — 根据执行的安装类型而变化的文件夹名称。
- `[JAVA_HOME]` — JDK的安装目录。

## 第1部分：创建SSL凭据（自签名）

如果您没有来自CA的证书，则可以使用Java `keytool`实用程序生成自签名SSL凭据。 这适用于开发或测试环境。

### 步骤1 — 生成密钥库

在命令提示符中导航到`[JAVA_HOME]/bin`并运行以下命令，将值替换为适用于您的环境的值。 主机名必须是应用程序服务器的完全限定域名(FQDN)：

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

出现提示时，输入`keystore_password`。 请注意，密钥库的密码和密钥必须相同。

### 步骤2 — 将密钥库复制到配置目录

将生成的密钥库复制到适用于您的安装类型的相应配置文件夹中：

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### 步骤3 — 导出证书文件

使用以下命令之一从密钥库中导出证书：

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

出现提示时输入`keystore_password`。

### 第4步 — 复制并验证证书

将`AEMForms_cert.cer`复制到配置目录，然后验证其内容：

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### 步骤5 — 将证书导入Java Truststore

在导入之前，请确保`cacerts`文件是可写的：

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

然后导入证书：

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

提示输入密码时，键入`changeit` （默认Java Truststore密码 — 如果密码已更改，请与管理员核实）。 当询问&#x200B;**信任此证书时？ [no]**，类型`yes`。 您应该会看到一条确认消息：*&quot;证书已添加到密钥库。&quot;*

>[!NOTE]
>
> 如果您是通过SSL从Workbench连接到AEM Forms，则还必须在Workbench计算机上安装证书。

## 第2部分：使用Elytron子系统在JBoss上启用SSL

设置SSL凭据后，您现在可以通过JBoss CLI使用其Elytron安全子系统在JBoss上启用HTTPS。 在继续之前，请确保您的keystore文件位于相应的配置目录中。

>[!NOTE]
>
> 在Windows上，每个CLI命令都必须作为不带换行符的单行输入。 将`keystorename.keystore`替换为您的实际文件名，将`changeit`替换为您的密钥库/密钥密码。

### 步骤6a — 创建Elytron密钥库

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

如果您的密钥库使用该格式，请将`JKS`替换为`PKCS12`。

### 步骤6b — 创建Elytron密钥管理器

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

如果密钥库包含多个证书条目，请明确指定别名：

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### 步骤6c — 更新服务器SSL上下文

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### 步骤6d — 配置Undertow HTTPS侦听器

将SSL上下文连接到Undertow（JBoss Web服务器）以启用HTTPS侦听器：

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## 第3部分：重新启动应用程序服务器

完成Elytron配置后，重新启动JBoss以应用更改。

### 统包安装（Windows服务）

- 打开&#x200B;**控制面板>管理工具>服务**。
- 为Adobe Experience Manager表单&#x200B;**选择** JBoss。
- 选择&#x200B;**操作>停止**&#x200B;并等待服务停止。
- 选择&#x200B;**操作>开始**。

### 预配置或手动JBoss安装

在命令提示符下，导航到`[appserver root]/bin`：

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## 第4部分：向证书颁发机构请求凭据

对于生产环境，您应该使用由受信任的证书颁发机构(CA)颁发的证书。 此过程包括生成密钥对，创建证书签名请求(CSR)，然后导入CA签名证书。

### 生成密钥库并创建CSR

导航到`[JAVA_HOME]/bin`并生成密钥库：

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

然后生成CSR以提交到您的CA：

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

将`.csr`文件提交到您的CA。 收到返回的已签名证书后，请按照以下步骤操作。

### 导入CA签名证书

首先导入CA根证书：

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

如果浏览器尚未信任根证书，则也将其导入。 然后导入CA签名证书：

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> 导入的CA签名证书将替换任何现有的自签名公共证书（如果密钥库中存在）。

导入CA证书后，继续执行第2部分（Elytron配置）中的&#x200B;**步骤6a-6d**，重新启动服务器（第3部分），并验证SSL访问。

## 验证SSL访问

重新启动服务器后，通过通过HTTPS访问AEM Forms管理控制台来验证SSL是否正常工作。 JBoss的默认SSL端口为`8443`：

```
https://[host name]:8443/adminui
```

如果管理控制台通过HTTPS成功加载，则表示SSL已正确配置。 对到AEM Forms的所有后续SSL连接使用端口`8443`。
