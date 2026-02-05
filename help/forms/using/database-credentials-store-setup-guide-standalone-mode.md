---
title: Database Credential Store安装指南（独立模式）
description: 在独立模式下，查找JBoss/Red Hat EAP上AEM Forms JEE的数据库凭据存储设置。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Database Credential Store安装指南（独立模式）

## 概述

本指南介绍在&#x200B;**独立模式**&#x200B;下JBoss/Red Hat EAP上适用于AEM Forms JEE的&#x200B;**数据库凭据存储区设置**。 执行手动安装时需要此项。


**本指南涵盖：**

- 正在创建数据库凭据存储(`cred-store.p12`)
- 安全添加数据库密码别名
- 配置JBoss以使用凭据存储区

**关键：**&#x200B;这些脚本仅在&#x200B;**脱机模式下运行**。 在运行这些脚本之前，必须停止JBoss。 脚本使用`embed-server`模式，这要求停止服务器。

**注意：**&#x200B;这&#x200B;**不是**&#x200B;完整的独立安装指南。 本文档假定：

- 已安装JBoss
- 独立配置文件（`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）已配置
- 数据库已设置并可访问

如果需要完整的独立安装说明，请参阅主安装指南。

## 先决条件

在运行这些脚本之前，请确保：

1. 必须停止&#x200B;**JBoss**
   - 这些脚本仅在&#x200B;**脱机模式下工作**
   - 脚本使用`embed-server`，这要求停止服务器
   - 如果JBoss正在运行，脚本将失败
   - 检查JBoss是否正在运行：
      - Windows：检查`java.exe`进程的任务管理器
      - Linux： `ps aux | grep jboss`或`ps aux | grep java`
   - 如果正在运行，则停止JBoss：
      - 在运行JBoss的终端中按`Ctrl+C`
      - 或者手动终止进程

2. **您已准备好数据库密码**

3. **您已决定凭据存储区的安全密码**

4. **您知道要使用哪个数据库配置文件：**
   - `lc_oracle.xml` (用于Oracle数据库)
   - `lc_mysql.xml` （对于MySQL数据库）
   - `lc_mssql.xml` (对于Microsoft SQL Server数据库)

## 设置步骤

### 步骤1：创建数据库凭据存储

使用提供的脚本创建数据库凭据存储区并添加所有必需的密码别名。

#### 在Windows上：

**脚本位置：** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**脚本将提示您输入：**
1. **JBOSS_HOME路径** （例如，`C:\Adobe\Adobe_Experience_Manager_Forms\jboss`）
2. **配置文件名** （如`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）
3. **凭据存储区密码** （这将保护密钥存储区文件 — 记住此密码）
4. **数据库密码** （您的实际数据库密码）

**脚本的作用：**

- 创建凭据存储区： `JBOSS_HOME\standalone\configuration\cred-store.p12`
- 临时修改配置文件以启用凭据存储创建
- 使用数据库密码添加以下别名：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 将配置文件恢复为其原始状态
- 验证是否已成功添加所有别名

#### 在Linux上：

**脚本位置：** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**脚本将提示您输入：**

1. **JBOSS_HOME路径** （例如，`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`）
2. **配置文件名** （如`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）
3. **凭据存储区密码** （这将保护密钥存储区文件 — 记住此密码）
4. **数据库密码** （您的实际数据库密码）

**脚本的作用：**

- 创建凭据存储区： `JBOSS_HOME/standalone/configuration/cred-store.p12`
- 临时修改配置文件以启用凭据存储创建
- 使用数据库密码添加以下别名：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 将配置文件恢复为其原始状态
- 验证是否已成功添加所有别名

**预期输出：**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### 步骤2：更新独立配置文件

运行脚本后，您需要配置JBoss以在启动时读取凭据存储区密码。

#### 在Windows上：

**文件位置：** `<JBOSS_HOME>\bin\standalone.conf.bat`

示例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

添加或更新以下行：

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

将`YourActualPassword123`替换为您在步骤1中使用的&#x200B;**凭据存储区密码**。

#### 在Linux上：

**文件位置：** `<JBOSS_HOME>/bin/standalone.conf`

示例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

添加或更新以下行：

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

将`YourActualPassword123`替换为您在步骤1中使用的&#x200B;**凭据存储区密码**。

### 步骤3：启动JBoss

完成凭据存储设置后，使用相应的配置文件启动JBoss。

**注意：**&#x200B;有关以独立模式启动JBoss的准确启动命令和过程，请参阅&#x200B;**主安装指南**。 启动命令可能会因您的特定配置和数据库类型（`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）而异。

## 验证

### 检查服务器日志

**日志位置：**

- Windows： `<JBOSS_HOME>\standalone\log\server.log`
- Linux： `<JBOSS_HOME>/standalone/log/server.log`

**查找成功的启动消息：**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**没有与**&#x200B;相关的错误

- 正在加载凭据存储
- 数据库连接
- 缺少别名

## 疑难解答

### 问题1：未找到凭据存储

**错误消息：**

```
ERROR Unable to load credential store
```

**解决方案：**

1. 验证凭据存储文件是否存在：
   - Windows： `dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux： `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. 如果缺少，请重新运行凭据存储创建脚本（步骤1）

### 问题2：凭据存储密码错误

**错误消息：**

```
ERROR Unable to load credential store - Invalid password
```

**解决方案：**
验证`standalone.conf.bat` / `standalone.conf` （步骤2）中的密码是否与创建凭据存储区时使用的密码匹配（步骤1）。

要修复的&#x200B;**：**
编辑`standalone.conf.bat` / `standalone.conf`并更新密码：

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### 问题3：数据库连接失败

**错误消息：**

```
ERROR Failed to obtain connection
```

**解决方案：**

1. 验证凭据存储区中使用的数据库密码是否正确
2. 检查数据源配置是否引用了正确的别名
3. 验证到数据库服务器的网络连接

**要重新创建凭据存储：**

1. 停止JBos
2. 删除现有的凭据存储：
   - Windows： `del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux： `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. 使用正确的数据库密码重新运行凭据存储创建脚本

### 问题4：脚本在执行期间失败

**错误消息：**

```
ERROR: jboss-cli.bat is not found
```

**解决方案：**
验证JBOSS_HOME路径是否正确，并指向JBoss安装目录。

**错误消息：**

```
ERROR: Configuration file not found
```

**解决方案：**

1. 验证配置文件名称是否正确
2. 检查文件是否存在于`JBOSS_HOME\standalone\configuration\`目录中
3. 确保您使用的是正确的特定于数据库的配置文件

## 快速参考

### 数据库凭据存储（独立模式）

**用途：**&#x200B;安全存储数据库密码

**脚本：**

- Windows： `create-elytron-cred-standalone.bat`
- Linux： `create-elytron-cred-standalone.sh`

**创建：**

- 文件： `standalone/configuration/cred-store.p12`
- 别名： `EncryptDBPassword`，`EncryptDBPassword_IDP_DS`，`EncryptDBPassword_EDC_DS`，`EncryptDBPassword_AEM_DS`

**配置：**

- 变量： `-DCS_PASS=password`
- 文件： `standalone.conf.bat` (Windows)或`standalone.conf` (Linux)

