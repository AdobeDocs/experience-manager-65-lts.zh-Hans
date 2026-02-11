---
title: 在OSGi上升级到AEM 6.5 Forms LTS
description: 您可以从AEM 6.5.22.0 Forms直接升级到AEM 6.5 Forms LTS。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 6%

---

# 在OSGi上升级到AEM 6.5 Forms LTS {#upgrade-to-aem-forms-osgi}

要[从AEM 6.5升级到AEM 6.5 LTS](/help/sites-deploying/upgrade.md)，请升级到AEM 6.5.22.0 Forms或更高版本。 支持从AEM 6.5.22.0直接升级到AEM 6.5 Forms LTS。

如果您使用的是AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 Forms或AEM 6.5 Forms，则无法直接升级到AEM 6.5 Forms LTS。 有关详细升级路径，请参阅[升级路径](/help/forms/using/upgrade.md)文档。

升级到Service Pack AEM Forms 6.5.22.0后，请按照以下步骤升级到AEM 6.5 LTS Forms：

1. 安装AEM Forms附加组件包。 以下列出了这些步骤：

   1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
   1. 选择标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 筛选器]**&#x200B;部分中：
      1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
      1. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
   1. 选择适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后选择&#x200B;**[!UICONTROL 下载]**。
   1. 打开[包管理器](/help/sites-administering/package-manager.md)，然后单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
   1. 选择该包并点击&#x200B;**[!UICONTROL 安装]**。

      您还可以使用[AEM Forms发行版](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)文章中列出的直接链接下载包。

      安装包后，系统会提示您重新启动AEM实例。 **不立即停止服务器。**&#x200B;在停止AEM Forms服务器之前，请等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出现在&lt;crx-repository>/error.log文件中，并且日志稳定。 另请注意，一些软件包可以保持已安装状态。 您可以安全地忽略这些软件包的状态。


      **使用以下其他JVM命令行参数重新启动AEM实例**：
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      如果服务器是通过脚本或服务启动的，请相应地更新以包含上述内容，以便在后续重新启动后生效。

      >[!NOTE]
      >
      > 建议使用 “Ctrl + C” 命令重新启动 SDK。如果使用其他方式（例如停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。

1. 执行安装后活动。

   * **运行迁移实用程序**

     迁移实用程序使自适应表单和以前版本的通信管理资产与AEM 6.5表单兼容。 您可以从AEM Software Distribution下载该实用程序。 有关配置和使用迁移实用程序的逐步信息，请参阅[迁移实用程序](../../forms/using/migration-utility.md)。

     如果您使用[示例将草稿和提交组件](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)与数据库集成并从以前的版本升级，请在执行升级后运行以下SQL查询：

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置Adobe Sign**

     如果您在早期版本的AEM Forms中配置了Adobe Sign，则从AEM Cloud Service重新配置Adobe Sign。 有关详细信息，请参阅[将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支持jQuery**

     在AEM 6.5 Forms中，jQuery的版本更新为3.2.1，jQuery UI的版本更新为1.12.1。AEM表单在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用的是任何其他jQuery版本，则在执行升级时不会显示任何问题。 但是，当您升级到AEM 6.5 Forms时：

      * 确保您的自定义组件（如果有）与支持的jQuery版本兼容。
      * 从自定义组件中删除不支持的API。 请参阅[升级指南](https://jquery.com/upgrade-guide/3.0/)以获取已删除的API列表。 例如，删除了对load()、.unload()和.error() API的支持。 使用.on()方法替换前面提到的API。 例如，将$(&quot;img&quot;)。load(fn)更改为$(&quot;img&quot;)。on(&quot;load&quot;， fn)。

   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置分析和报表**

     在AEM 6.4 Forms中，源的流量变量和印象的成功事件不可用。 因此，当您从AEM 6.2 Forms或之前的版本升级时，AEM Forms会停止向Adobe Analytics服务器发送数据，并且自适应表单的Analytics报表将不可用。 此外，AEM 6.4 Forms还为Form Analytics版本引入了流量变量，并为字段逗留时间引入了成功事件。 因此，请为您的AEM Forms环境重新配置分析和报表。 有关详细步骤，请参阅[配置分析和报表](../../forms/using/configure-analytics-forms-documents.md)。

1. 验证服务器是否升级成功，所有数据是否也迁移成功，服务器是否能够正常运行。

   * **验证捆绑的状态：**&#x200B;确保所有捆绑都处于活动状态。
   * **验证复制和反向复制：**&#x200B;发布、填写并提交一些迁移的表单。 同时验证提交的数据。
   * **验证对管理员和开发人员用户界面的访问权限：**&#x200B;从管理员帐户登录AEM实例，并验证您有权访问以下URL：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >在AEM 6.4 Forms中，crx-repository的结构发生了更改。 如果从6.3 Forms升级到AEM 6.5 Forms，请使用更改后的路径来重新创建自定义。 有关已更改路径的完整列表，请参阅[AEM中的Forms存储库重组](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)。


## 在JBoss EAP 8上部署AEM (Windows)

### 概述

本指南分步说明了如何使用JDK 21在Windows环境中将Adobe Experience Manager (AEM)作为独立的OSGi WAR文件部署在JBoss Enterprise Application Platform (EAP) 8上。

### 系统要求

在开始部署过程之前，请确保您的环境满足以下要求：

| 组件 | 要求 |
|-----------|-------------|
| 操作系统 | Windows Server 2016或更高版本（64位） |
| Java开发工具包 | JDK 21(Oracle或OpenJDK) |
| 应用程序服务器 | JBoss EAP 8.x |
| AEM Distribution | AEM WAR文件(从Adobe获取) |

>[!NOTE]
>
> 验证`JAVA_HOME`环境变量是否指向JDK 21安装目录。

### 步骤1：安装JBoss EAP 8

#### 下载JBoss EAP

1. 导航到Red Hat开发人员门户：\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. 下载适用于Windows的JBoss EAP 8 ZIP分发。

#### 提取JBoss EAP

1. 将下载的ZIP文件解压到首选安装目录。

2. 请将此目录路径记为`<JBOSS_HOME>`，以便在本指南中使用。

   **示例：**\
   ```C:\jboss-eap-8.0```

### 步骤2：准备AEM WAR文件

#### 获取AEM WAR

从AEM Software Distribution或您的Adobe代表处获取Adobe WAR文件。

#### 重命名WAR文件

重命名WAR文件以反映所需的URL上下文路径：

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> WAR文件名决定了应用程序的URL上下文。 例如，`cq-quickstart.war`将在`/cq-quickstart`处访问。


### 步骤3：配置AEM WAR

所有配置修改都必须在&#x200B;**之前完成**，然后才能部署到JBoss。

#### 创建工作目录

1. 创建临时工作目录：

   ```
   C:\aem\war-config
   ```

2. 将 `cq-quickstart.war` 复制到此目录中。

#### 提取WAR内容

1. 打开&#x200B;**命令提示符**&#x200B;并导航到工作目录：

   ```cmd
   cd C:\aem\war-config
   ```

2. 提取WAR文件：

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   这将创建一个包含`WEB-INF`和其他应用程序文件的目录结构。

### 步骤4：配置JBoss部署描述符

#### 创建部署结构文件

1. 导航到解压缩的WAR中的`WEB-INF`目录：

   ```cmd
   cd WEB-INF
   ```

2. 创建名为`jboss-deployment-structure.xml`的新文件。

3. 添加以下XML内容：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. 保存并关闭该文件。

**用途：**&#x200B;此配置提供对AEM所需的JDK内部模块的访问权限。

### 步骤5：配置多部分上载设置

>[!NOTE]
>
> 步骤5仅适用于&#x200B;**AEM Forms**。 如果您仅设置&#x200B;**AEM**，则可以跳过此步骤。


#### 修改web.xml

1. 在文本编辑器中打开`WEB-INF\web.xml`。

2. 找到包含运行模式配置的`<servlet>`部分：

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. 将结束`</servlet>`标记和前一行替换为：

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. 保存并关闭`web.xml`。

**用途：**&#x200B;这些设置为AEM Forms和数字资产管理启用大文件上传（最大1 GB）。

### 步骤6：重新打包WAR文件

完成所有配置更改后，重新打包WAR文件。

1. 导航回包含提取内容的工作目录：

   ```cmd
   cd C:\aem\war-config
   ```

2. 创建新的WAR文件：

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> 完成所有配置后，仅执行一次此步骤。

### 步骤7：部署和启动AEM

#### 将WAR部署到JBoss

1. 将重新打包的`cq-quickstart.war`复制到JBoss部署目录：

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **示例：**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### 配置JVM设置（可选，但推荐）

在启动JBoss之前，请配置JVM内存设置：

1. 在文本编辑器中打开`<JBOSS_HOME>\bin\standalone.conf.bat`。

1. 修改或添加以下行以设置栈内存：

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> 根据服务器容量和AEM要求调整内存值。

1. 保存并关闭该文件。

#### 启动JBoss EAP

1. 以&#x200B;**管理员**&#x200B;的身份打开&#x200B;**命令提示符**。

1. 导航到JBoss bin目录：

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **示例：**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. 启动JBoss服务器：

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **参数：**
   * `-b 0.0.0.0` — 将服务器绑定到所有网络接口
   * `-bmanagement 0.0.0.0` — 将管理接口绑定到所有网络接口

#### 监控部署

查看控制台输出中的部署消息。 成功部署由以下指示：

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### 步骤8：访问AEM

部署完成且AEM完全启动后：

**AEM作者URL：**
```http://<server-ip>:8080/cq-quickstart```

**默认凭据：**

* 用户名： `admin`
* 密码： `admin`

**重要信息：**&#x200B;在首次登录后立即更改默认密码。

### 疑难解答

#### 常见问题

| 问题 | 解决办法 |
|-------|----------|
| 部署失败，出现ClassNotFoundException | 验证`jboss-deployment-structure.xml`是否正确配置 |
| 启动期间出现OutOfMemoryError | 在`standalone.conf.bat`中增加栈内存 |
| AEM不会在部署后启动 | 检查`<JBOSS_HOME>\standalone\log\server.log`中的JBoss日志 |
| 无法在浏览器中访问AEM | 验证防火墙设置是否允许端口8080 |

#### 日志文件

* **JBoss服务器日志：** `<JBOSS_HOME>\standalone\log\server.log`
* **AEM错误日志：**&#x200B;在启动后可通过AEM Web控制台使用\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### 其他配置

#### 配置运行模式

要更改AEM运行模式（创作/发布），请在重新打包WAR之前修改`sling.run.modes`中的`WEB-INF\web.xml`参数：

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### 生产推荐

对于生产环境：

* 在JBoss中配置SSL/TLS证书
* 设置AEM复制代理
* 配置Dispatcher以实现负载平衡
* 启用自动备份
* 实施监控和警报

### 相关文档

* [JBoss EAP 8文档](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Adobe Experience Manager文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
* [AEM安装和部署指南](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

### 文档信息

| 字段 | 值 |
|-------|-------|
| 上次更新时间 | 2026年2月 |
| AEM 版本 | 6.5+ (LTS) |
| JBoss版本 | EAP 8.x |
| JDK版本 | 21 |
| 平台 | Windows |


