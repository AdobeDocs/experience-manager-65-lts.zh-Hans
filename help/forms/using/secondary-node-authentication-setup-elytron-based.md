---
title: 辅助节点身份验证设置（基于Elytron）
description: JBoss EAP 8使用Elytron实现辅助节点与主域控制器的安全通信与注册。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# 辅助节点身份验证设置（基于Elytron）

## 使用Elytron配置辅助节点身份验证

JBoss EAP 8使用&#x200B;**Elytron**&#x200B;验证群集部署中&#x200B;**主节点和辅助节点**&#x200B;之间的通信。 此配置确保辅助节点与主域控制器之间的安全注册和通信。

根据环境和安全要求，有两种设置选项可用。

## 先决条件

* 必须在&#x200B;**主节点`secondary`**&#x200B;上创建名为&#x200B;**的**&#x200B;管理用户。
* 仅在辅助节点&#x200B;**上执行此配置**。
* 对群集中的&#x200B;**每个辅助节点**&#x200B;重复配置。
* 主节点和辅助节点上的&#x200B;**JBoss必须完全停止**。
* 所有凭据存储操作必须在&#x200B;**脱机模式**&#x200B;下执行。

要停止JBoss（如果它正在运行），请执行以下操作：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## 选择设置选项

* **选项1：使用默认凭据存储区快速安装**
建议用于较低环境和测试。

* **选项2：自定义凭据存储设置**
建议用于生产和安全环境。

## 选项1：使用默认凭据存储区进行快速设置

**最适合：**&#x200B;开发、测试和快速设置方案。

### 概述

* 已预配置默认凭据存储文件(`cs_secondary_hc.p12`)。
* 默认凭据存储密码已在`domain.conf`中设置。
* 只需添加身份验证密码别名。

### 配置步骤

#### 步骤1：验证默认凭据存储

确认默认凭据存储文件存在：

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

如果文件不存在，请使用&#x200B;**选项2**。

#### 步骤2：添加验证密码别名

从`<JBOSS_HOME>/bin`运行以下命令：

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> 密钥值必须与在主节点上创建`secondary`用户时使用的密码匹配。

#### 步骤3：验证domain.conf配置

验证以下条目是否存在（无需更改）：

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### 步骤4：启动节点

1. 启动&#x200B;**主节点**&#x200B;并等待它完全初始化。
2. 启动&#x200B;**辅助节点**。

### 验证

检查日志：

* **主节点**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **辅助节点**

  ```
  Connected to primary host controller
  ```

## 选项2：自定义凭据存储设置（生产）

**最适合：**&#x200B;要求增强安全性的生产环境。

### 配置步骤

#### 步骤1：删除默认凭据存储（如果存在）

如果默认凭据存储区存在，请将其重命名：

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### 步骤2：创建自定义凭据存储区

从`<JBOSS_HOME>/bin`：

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### 步骤3：添加验证密码别名

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### 步骤4：更新domain.conf

更新凭据存储区密码引用：

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### 步骤5：验证XML配置

确保`host-secondary.xml`包含配置的凭据存储区和身份验证客户端条目。
如果存在默认配置，则不需要进行更改。


#### 步骤6：启动节点

1. 启动&#x200B;**主节点**&#x200B;并等待完全启动。
2. 启动&#x200B;**辅助节点**。

### 验证

使用两个节点上的主机控制器日志确认注册成功。

## 摘要

* **选项1**&#x200B;使用预配置的凭据存储区提供快速安装。
* **选项2**&#x200B;使用自定义凭据存储密码提供更强的安全性。
* 只能在辅助节点上完成&#x200B;**的配置**。
* 主节点配置会在整个域中自动重用。

