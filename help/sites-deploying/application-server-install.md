---
title: 应用程序服务器安装
description: 了解如何将Adobe Experience Manager与应用程序服务器一起安装。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: 2a33cb4b8aa1dcfd989cf61465492d563f9cd99a
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 1%

---

# 应用程序服务器安装{#application-server-install}

>[!NOTE]
>
>`JAR`和`WAR`是Adobe Experience Manager (AEM)在中发布的文件类型。 这些格式正在进行质量保证，以满足Adobe承诺的支持级别。
>

本节将介绍如何通过应用程序服务器安装Adobe Experience Manager (AEM)。 请参阅[支持的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)部分，了解为各个应用程序服务器提供的特定支持级别。

以下应用程序服务器的安装步骤已说明：

* [WebSphere](#websphere)
* [Tomcat 10.0.x/10.1.x](#tomcat)

有关安装Web应用程序、服务器配置以及如何启动和停止服务器的详细信息，请参阅相应的应用程序服务器文档。

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## 常规描述 {#general-description}

### 在应用程序服务器中安装AEM时的默认行为 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM提供单个war文件来进行部署。

如果部署，则默认情况下会发生以下情况：

* 运行模式为`author`
* 中安装的实例（存储库、Felix OSGI环境、捆绑包等）是`${user.dir}/crx-quickstart`，其中`${user.dir}`是当前工作目录。 crx-quickstart的此路径名为`sling.home`

* 上下文根目录是war文件名。 例如 `aem-65-lts`。

#### 配置 {#configuration}

您可以通过以下方式更改默认行为：

* 运行模式：在部署之前在AEM war文件的`sling.run.modes`文件中配置`WEB-INF/web.xml`参数

* sling.home：在部署之前在AEM war文件的`sling.home`文件中配置`WEB-INF/web.xml`参数

* 上下文根：重命名AEM war文件

#### 发布安装 {#publish-installation}

要部署发布实例，您需要将运行模式设置为发布：

* 从AEM war文件中解压缩`WEB-INF/web.xml`
* 将`sling.run.modes`参数更改为发布
* 将`web.xml`文件重新打包到AEM war文件中
* 部署AEM war文件

#### 安装检查 {#installation-check}

要检查是否已安装所有软件，您可以：

* 跟踪`error.log`文件以查看是否已安装所有内容
* 在`/system/console`中查找是否已安装所有包

#### 同一应用程序服务器上的两个实例 {#two-instances-on-the-same-application-server}

出于演示目的，可以将创作实例和发布实例同时安装在一个应用程序服务器中。 要实现这一点，您需要：

1. 更改发布实例的`sling.home`变量和`sling.run.modes`变量
1. 从AEM war文件中解压缩`WEB-INF/web.xml`文件
1. 将`sling.home`参数更改为其他路径（可以使用绝对路径和相对路径）
1. 将发布实例的`sling.run.modes`更改为`publish`
1. 重新打包`web.xml`文件
1. 请重命名war文件，使其名称不同。 例如，将一个重命名为`aemauthor.war`，另一个重命名为`aempublish.war`
1. 使用更高的内存设置。 例如，默认的AEM实例使用`-Xmx3072m`
1. 部署两个Web应用程序
1. 部署后，停止两个Web应用程序
1. 在创作实例和发布实例中，确保在`sling.properties`文件中属性`felix.service.urlhandlers`设置为`false`。 （默认设置是`true`）。
1. 再次启动两个Web应用程序。

## 应用服务器的安装过程 {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

在部署之前，请阅读上面的[一般说明](#general-description)。

**服务器准备**

* 让基本身份验证标头通过：

   * 允许AEM对用户进行身份验证的一种方法是禁用WebSphere®服务器的全局管理安全。 为此，请转到&#x200B;**安全>全局安全**&#x200B;并取消选中&#x200B;**启用管理安全复选框**，保存并重新启动服务器。

* 设置 `"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上下文根= /安装AEM，请更改现有默认Web应用程序的上下文根。

**部署AEM Web应用程序**

* 下载AEM war文件
* 如有需要，在`web.xml`文件中进行配置。 有关详细信息，请参阅上面的[一般说明](#general-description)。

   * 解压缩`WEB-INF/web.xml`文件
   * 将`sling.run.modes`参数更改为`publish`
   * 取消注释初始`sling.home`参数，并根据需要设置此路径
   * 重新打包`web.xml`文件。

* 部署AEM war文件

   * 选择上下文根。 如果要设置sling运行模式，您需要选择部署向导的详细步骤，然后在向导的步骤6中指定该步骤。

* 启动AEM Web应用程序

#### Tomcat 10.0.x/10.1.x {#tomcat}

在部署之前，请阅读上面的[常规说明](#general-description)。

* **准备Tomcat服务器**

   * 增加VM内存设置：

      * 在`bin/catalina.bat`中(在UNIX®上为`catalina.sh`)添加以下设置：

        ```
        set "JAVA_OPTS= -Xmx2048m`
        ```

   * 在安装时，Tomcat不启用管理员或管理员访问权限。 因此，您必须手动编辑`tomcat-users.xml`以允许访问这些帐户：

      * 编辑`tomcat-users.xml`以包括管理员和经理的访问权限。 该配置应类似于以下示例：

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
          <role rolename="manager"/>
          <role rolename="tomcat"/>
          <role rolename="admin"/>
          <role rolename="role1"/>
          <role rolename="manager-gui"/>
          <user username="both" password="tomcat" roles="tomcat,role1"/>
          <user username="tomcat" password="tomcat" roles="tomcat"/>
          <user username="admin" password="admin" roles="admin,manager-gui"/>
          <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * 如果要使用上下文根“/”部署AEM，则必须更改现有ROOT Web应用程序的上下文根：

      * 停止并取消部署ROOT Web应用程序
      * 重命名Tomcat webapps文件夹中的`ROOT.war`文件夹
      * 再次启动Web应用程序

   * 如果您使用管理器gui安装AEM Web应用程序，则需要增加已上传文件的最大大小，因为默认仅允许50 MB的上传大小。 要实现打开管理器Web应用程序的`web.xml`：

     `webapps/manager/WEB-INF/web.xml`

     并将`max-file-size`和`max-request-size`增加到至少500MB。 在下面的`multipart-config`示例文件中查看以下`web.xml`：

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **部署AEM Web应用程序**

   * 下载AEM war文件。
   * 如有需要，在`web.xml`文件中进行配置。

      * 解压缩`WEB-INF/web.xml`文件
      * 将`sling.run.modes`参数更改为`publish`
      * 取消注释初始`sling.home`参数，并根据需要设置此路径
      * 重新打包`web.xml`文件。

   * 如果要将AEM war文件部署为根Web应用程序，请将其重命名为`ROOT.war`。 如果要将`aemauthor.war`作为上下文根目录，请将其重命名为`aemauthor`。
   * 将其复制到Tomcat的Webapps文件夹中
   * 等待安装AEM。
