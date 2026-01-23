---
title: 数据库凭据存储设置（基于Elytron）
description: JBoss EAP 8支持Elytron凭据存储，以便在AEM Forms中进行安全的数据库密码管理，进而进行域模式设置。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: d397e6a51ad2a52da5ccb0a690e1acd3fafcee3c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# 数据库凭据存储设置（基于Elytron）

## 使用Elytron配置数据库凭据存储

JBoss EAP 8使用&#x200B;**Elytron凭据存储区**&#x200B;安全地管理AEM Forms部署的数据库密码。 Adobe提供了&#x200B;**自动脚本**，以简化域模式下基于Elytron的凭据存储区的创建和配置。

在启动JBoss域控制器&#x200B;**之前，必须完成此设置**。

### 先决条件

* 在运行凭据存储创建脚本之前，必须完全停止&#x200B;**JBoss服务器**。
* 只能在&#x200B;**脱机模式下创建凭据存储**。

要停止JBoss（如果它正在运行），请执行以下操作：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### 下载脚本

根据您的操作系统下载相应的脚本：

| 脚本名称 | 操作系统 |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux / UNIX |

对于Linux，使脚本可执行：

```
chmod +x create-elytron-cred-domain.sh
```

### 配置步骤

#### 步骤1：下载并放置脚本

下载相应的脚本，并将其放在以下目录中：

```
<JBOSS_HOME>/bin
```

#### 步骤2：运行脚本

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux / UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### 步骤3：提供所需信息

在执行过程中，脚本会提示您输入以下内容：

1. **JBOSS_HOME路径**
输入JBoss安装目录的完整路径。

2. **数据库配置文件名称**
根据您的数据库输入以下内容之一：

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **凭据存储区密码**
输入强密码以保护凭据存储。

   > 此密码在输入过程中处于隐藏状态，必须在后续步骤中记住此密码。

4. **数据库密码**
输入实际的数据库连接密码。

#### 步骤4：脚本执行和验证

该脚本会自动执行以下操作：

* 在中创建`cred-store.p12`：

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* 创建以下凭据别名：

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* 验证是否成功添加了所有别名

成功执行可确认凭据存储创建和别名验证。

#### 步骤5：配置JVM选项

更新JBoss域启动配置以提供凭据存储区密码。

* **Linux**
编辑：

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  添加：

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
编辑：

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  添加：

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

将`YourCredStorePassword`替换为创建凭据存储时输入的密码。

域配置文件使用`${CS_PASS}`变量引用此值。


#### 步骤6：验证域配置

打开数据库域配置文件：

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

验证数据源是否引用Elytron凭据存储区：

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

每个数据源都使用特定的别名：

* **IDP_DS：** `EncryptDBPassword_IDP_DS`
* **EDC_DS：** `EncryptDBPassword_EDC_DS`
* **AEM_DS：** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS：** `EncryptDBPassword`

所有别名都引用存储在凭据存储中的相同数据库密码。

>[!NOTE]
>
>* 仅在主节点上配置凭据存储。
>* 辅助节点会自动使用与主节点同步的域配置。
