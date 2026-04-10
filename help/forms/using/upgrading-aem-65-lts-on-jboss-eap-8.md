---
title: 在JBoss EAP 8上升级AEM 6.5 LTS (Windows)
description: 本指南提供了使用JDK 21将现有Adobe Experience Manager (AEM) 6.5 LTS安装从Windows上的JBoss EAP 7.4升级到JBoss EAP 8的分步说明。
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 3%

---

# 在JBoss EAP 8上升级AEM 6.5 LTS (Windows)

## 概述

本指南提供了使用JDK 21将现有Adobe Experience Manager (AEM) 6.5 LTS安装从Windows上的JBoss EAP 7.4升级到JBoss EAP 8的分步说明。

**升级路径：** JBoss EAP 7.4 (JDK 11) → JBoss EAP 8 (JDK 21)

## 重要注意事项

>[!NOTE]
>
>这是一个关键的升级过程。 始终首先在非生产环境中执行此升级，并维护完整的备份。
>
> **先决条件：**&#x200B;在继续之前，必须完成系统备份和制定有文档记录的回滚计划。

## 升级前要求

### 系统要求

| 组件 | 要求 |
|-----------|-------------|
| 操作系统 | Windows Server 2016或更高版本（64位） |
| Source环境 | 带有AEM 6.5 LTS的JBoss EAP 7.4 |
| 目标环境 | JBoss EAP 8.x |
| Java开发工具包 | JDK 21（Oracle或OpenJDK） |
| AEM 版本 | AEM 6.5 Service Pack（最新推荐版本） |
| 磁盘空间 | 升级过程的最小可用空间为50 GB |

### 所需下载

在开始升级之前，请获取以下内容：

1. **JBoss EAP 8.0分发**\
   下载自：[https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **JDK 21安装程序**\
   下载Oracle JDK 21或OpenJDK 21 for Windows（64位）

3. **AEM 6.5 LTS WAR文件**\
   从AEM Software Distribution获取最新的Adobe 6.5 Service Pack WAR

## 步骤1：创建完整备份

>[!IMPORTANT]
>
> 请在继续之前执行全面的备份。

### 备份核对清单

- [ ]现有JBoss EAP 7.4安装目录的完整备份
- [ ]文件夹的`crx-repository`备份
- [ ]文件夹的`crx-quickstart`备份
- [ ]导出所有自定义配置
- [ ]数据库备份（如果使用外部数据库）
- [ ]记录当前系统状态和配置

### 创建备份

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**建议：**&#x200B;将备份存储在单独的驱动器或网络位置。

## 步骤2：安装JBoss EAP 8

### 提取JBoss EAP 8

1. 将JBoss EAP 8 ZIP分发解压缩到目标安装目录：

   ```
   C:\jboss-eap-8.0
   ```

2. 请将此目录路径记为`<JBOSS_HOME>`，以便在本指南中使用。

### 复制目录结构

确保新的JBoss EAP 8安装与以前的JBoss EAP 7.4安装具有相同的自定义目录结构，特别是：

- 自定义部署目录
- 外部配置文件夹
- 日志文件位置
- 任何自定义模块或库

## 步骤3：迁移存储库数据

### 复制CRX存储库

1. 导航到现有的JBoss EAP 7.4安装：

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. 将整个`crx-repository`文件夹复制到新的JBoss EAP 8安装：

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**重要信息：**&#x200B;此文件夹包含您的内容存储库，必须完全传输。

### 验证存储库副本

复制后，验证存储库的大小和结构与源是否匹配：

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## 步骤4：停止AEM实例

在进行任何更改之前，请确保已完全停止AEM。

### 通过Windows服务停止

1. 打开&#x200B;**服务** （运行： `services.msc`）
2. 找到您的AEM/JBoss服务
3. 右键单击并选择&#x200B;**停止**
4. 等待服务完全停止

### 通过命令行停止

如果AEM是手动启动的：

1. 转到JBoss控制台窗口
2. 按`Ctrl+C`
3. 等待正常关机完成

### 验证关机

确保Java进程不再运行：

```cmd
tasklist | findstr java
```

## 步骤5：清理旧版AEM文件

从`crx-quickstart`目录中删除过时的文件以确保进行干净升级。

>[!CAUTION]
>
> 仅删除下面列出的特定文件和文件夹。 请勿删除任何其他配置文件、自定义代码或存储库数据。

### 5.1删除Launchpad启动文件夹

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**操作：**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**用途：**&#x200B;此文件夹包含将在升级期间重新生成的旧OSGi包。

### 5.2删除基本JAR文件

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**操作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**用途：**&#x200B;此JAR将被新WAR文件中的版本替换。

### 5.3删除Bootstrap命令文件

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**操作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**用途：**&#x200B;将为新环境重新生成Bootstrap命令。

### 5.4删除sling.options文件

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**操作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5删除sling_bootstrap.txt文件

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**操作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6备份和删除sling.properties文件

此文件包含特定于环境的配置，可能需要稍后合并。

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**操作：**

1. **创建备份：**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **删除原始文件：**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**用途：**&#x200B;将生成新的`sling.properties`。 检查您的备份，以便在升级后恢复任何自定义配置。

## 步骤6：安装和配置JDK 21

### 安装JDK 21

1. 运行Windows版JDK 21安装程序
2. 安装到标准位置（例如，`C:\Program Files\Java\jdk-21`）
3. 完成安装向导

### 配置环境变量

#### 设置JAVA_HOME

1. 打开&#x200B;**系统属性** → **高级** → **环境变量**
2. 在&#x200B;**系统变量**&#x200B;下，单击&#x200B;**新建**
3. 已设置：
   - 变量名称： `JAVA_HOME`
   - 变量值： `C:\Program Files\Java\jdk-21`
4. 单击&#x200B;**确定**

#### 更新路径变量

1. 在&#x200B;**系统变量**&#x200B;中，选择`Path`并单击&#x200B;**编辑**
2. 添加新条目：

   ```
   %JAVA_HOME%\bin
   ```

3. 将此条目移至列表顶部以确保JDK 21优先
4. 在所有对话框中单击&#x200B;**确定**

### 验证Java安装

1. 打开&#x200B;**新**&#x200B;命令提示符（以加载更新的环境变量）
2. 验证Java版本：

   ```cmd
   java -version
   ```

   预期输出：

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. 验证JAVA_HOME：

   ```cmd
   echo %JAVA_HOME%
   ```

## 步骤7：配置JVM设置

在部署AEM之前，请配置适当的JVM内存设置以供生产使用。

### 编辑standalone.conf.bat

1. 导航至：

   ```
   <JBOSS_HOME>\bin
   ```

2. 在文本编辑器中打开`standalone.conf.bat`（以管理员身份）

3. 找到或添加`JAVA_OPTS`配置：

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. 保存并关闭文件

**建议的设置：**

| 参数 | 建议值 | 描述 |
|-----------|-------------------|-------------|
| `-Xms` | 40.96亿 — 8.192亿 | 初始栈大小 |
| `-Xmx` | 40.96亿 — 8.192亿 | 最大栈大小 |
| `-XX:MaxMetaspaceSize` | 7.68亿 — 1.024亿 | 元空间限制 |

**注意：**&#x200B;根据服务器的可用内存和工作负载要求调整值。

## 步骤8：部署AEM 6.5 LTS WAR

### 准备WAR文件

确保按照部署指南正确配置您的AEM WAR文件：

- `jboss-deployment-structure.xml`存在
- `web.xml`包含多部分配置设置
- 如果进行了任何修改，WAR将重新打包

### 部署到JBoss

1. 将AEM 6.5 LTS WAR文件复制到部署目录：

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**重要信息：**&#x200B;请确保WAR文件名与所需的URL上下文路径相匹配。

## 步骤9：使用AEM启动JBoss EAP 8

### 启动服务器

1. 以&#x200B;**管理员**&#x200B;的身份打开&#x200B;**命令提示符**

2. 导航到JBoss bin目录：

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. 启动JBoss EAP 8：

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### 监视初始启动

观看控制台输出：

1. **WAR部署：**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **AEM初始化消息：**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **存储库升级（如果适用）：**

   ```
   Performing repository migration...
   ```

**预计启动时间：** 5-15分钟，具体取决于存储库大小和系统资源。

## 步骤10：验证升级是否成功

### 查看AEM启动

监视JBoss控制台以查看最终启动消息：

```
**** AEM started successfully ****
```

### 访问AEM界面

1. 打开Web浏览器
2. 导航至：

   ```
   http://localhost:8080/cq-quickstart
   ```

3. 使用管理员凭据登录：
   - 用户名： `admin`
   - 密码： `admin`（或您的自定义密码）

### 验证系统信息

1. 导航到&#x200B;**工具** → **操作** → **Web控制台**

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. 单击&#x200B;**系统信息**

3. 验证：

   - **JVM版本：**&#x200B;应显示Java 21
   - **JBoss版本：**&#x200B;应显示EAP 8.x
   - **AEM版本：**&#x200B;应显示6.5.xx

### 检查系统运行状况

导航到&#x200B;**工具** → **操作** → **诊断**&#x200B;以运行运行状况检查：

- 捆绑包状态：所有捆绑包都应处于“活动”状态
- 资源分辨率：应显示正常状态
- 查询性能：检查是否存在任何性能下降

## 升级后任务

### 恢复自定义配置

1. 查看已备份的`sling.properties`文件
2. 将任何自定义运行模式或配置还原到新文件：

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. 如果配置已更改，请重新启动AEM

### 更新复制代理

1. 导航到作者上的&#x200B;**工具** → **部署** → **复制** → **代理**
2. 查看和测试所有复制代理
3. 更新对旧服务器路径的任何硬编码引用

### 测试关键功能

- [ ]内容创作和发布
- [ ]资源上传和处理
- [ ]工作流执行
- [ ]用户身份验证
- [ ]集成端点
- [ ]自定义组件和模板

### 性能优化

1. 查看和清除任何临时缓存
2. 在初始使用期间监视系统性能
3. 如果需要，根据实际使用模式调整JVM设置

## 疑难解答

### 常见问题

| 问题 | 可能的原因 | 解决方案 |
|-------|---------------|----------|
| AEM无法启动 | Java版本不正确 | 验证`JAVA_HOME`指向JDK 21 |
| 存储库损坏错误 | 存储库复制不完整 | 从备份中恢复并重新复制存储库 |
| 内存不足错误 | 栈内存不足 | 在`-Xmx`中增加`standalone.conf.bat` |
| 处于“已安装”状态的包 | 缺少依赖项 | 在Web控制台中检查捆绑包依赖关系 |
| 端口8080已在使用中 | 使用端口的其他服务 | 停止冲突的服务或更改JBoss端口 |

### 日志文件位置

- **JBoss服务器日志：**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **AEM错误日志：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **AEM访问日志：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### 回滚过程

如果升级失败且无法解析：

1. 停止JBoss EAP 8
2. 恢复JBoss EAP 7.4的完整备份
3. 还原`crx-repository`文件夹
4. 验证`JAVA_HOME`是否指向JDK 11（如果回滚）
5. 启动上一个环境

## 最佳做法

### 生产部署之前

- [ ]在开发环境中测试完整的升级过程
- [ 在暂存环境中使用类似生产的数据进行]测试
- [ ]记录所有自定义配置和集成
- [ ]创建详细的回滚计划
- [ ]计划在维护时段升级
- [ ]通知所有利益相关者计划内停机时间

### 成功升级后

- [ ]监控系统日志48-72小时
- [ ]执行负载测试以确定性能问题
- [ ]更新系统文档
- [ ]培训团队了解任何JBoss EAP 8差异
- [ ]存档所有升级文档和备份

## 相关文档

- [JBoss EAP 8迁移指南](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Adobe Experience Manager 6.5升级指南](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html?lang=zh-Hans)
- [AEM正在安装Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=zh-Hans)

## 文档信息

| 字段 | 值 |
|-------|-------|
| 文档版本 | 1.0 |
| 上次更新时间 | 2026年2月 |
| AEM 版本 | 6.5 LTS |
| Source平台 | JBoss EAP 7.4 / JDK 11 |
| Target平台 | JBoss EAP 8.x / JDK 21 |
| 操作系统 | Windows Server |

**法律声明：** Adobe、Adobe Experience Manager和AEM是Adobe Inc.的注册商标。JBoss和Red Hat是Red Hat， Inc.的注册商标。
