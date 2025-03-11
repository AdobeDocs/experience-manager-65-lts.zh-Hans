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
source-git-commit: d716571f490fe4bf3b7e58ea2ca85bbe6703ec0d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# 应用程序服务器安装{#application-server-install}

>[!NOTE]
>
>`JAR`和`WAR`是Adobe Experience Manager (AEM)在中发布的文件类型。 这些格式正在进行质量保证，以满足Adobe承诺的支持级别。
>

本节将介绍如何通过应用程序服务器安装Adobe Experience Manager (AEM)。 请参阅[支持的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)部分，了解为各个应用程序服务器提供的特定支持级别。

以下应用程序服务器的安装步骤已说明：

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

有关安装Web应用程序、服务器配置以及如何启动和停止服务器的详细信息，请参阅相应的应用程序服务器文档。

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## 常规描述 {#general-description}

### 在应用程序服务器中安装AEM时的默认行为 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM提供单个war文件来进行部署。

如果部署，则默认情况下会发生以下情况：

* 运行模式为`author`
* 实例（存储库、Felix OSGI环境、捆绑包等）安装在`${user.dir}/crx-quickstart`中，其中`${user.dir}`是当前工作目录，指向crx-quickstart的路径称为`sling.home`

* 上下文根是war文件名，例如`aem-65-lts`

#### 配置 {#configuration}

您可以通过以下方式更改默认行为：

* 运行模式：在部署之前在AEM war文件的`WEB-INF/web.xml`文件中配置`sling.run.modes`参数

* sling.home：在部署之前在AEM war文件的`WEB-INF/web.xml`文件中配置`sling.home`参数

* 上下文根：重命名AEM war文件

#### 发布安装 {#publish-installation}

要部署发布实例，您需要将运行模式设置为发布：

* 从AEM war文件中解压缩WEB-INF/web.xml
* 将sling.run.modes参数更改为发布
* 将web.xml文件重新打包到AEM war文件中
* 部署AEM war文件

#### 安装检查 {#installation-check}

要检查是否已安装所有组件，您可以：

* 跟踪`error.log`文件以查看是否已安装所有内容
* 在`/system/console`中查找是否已安装所有包

#### 同一应用程序服务器上的两个实例 {#two-instances-on-the-same-application-server}

出于演示目的，可以将创作实例和发布实例安装在一个应用程序服务器中。 为此，请执行以下操作：

1. 更改发布实例的sling.home变量和sling.run.modes变量。
1. 从AEM war文件中解压缩WEB-INF/web.xml文件。
1. 将sling.home参数更改为其他路径（可以使用绝对路径和相对路径）。
1. 将sling.run.modes更改为发布实例的发布。
1. 重新打包web.xml文件。
1. 请重命名war文件，使其名称不同。 例如，一个重命名为aemauthor.war，另一个重命名为aempublish.war。
1. 使用更高的内存设置。 例如，默认的AEM实例使用`-Xmx3072m`
1. 部署两个Web应用程序。
1. 部署后，停止两个Web应用程序。
1. 在创作实例和发布实例中，均确保在sling.properties文件中，属性felix.service.urlhandlers=false设置为false（默认设置为true）。
1. 再次启动两个Web应用程序。

## 应用服务器的安装过程 {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

在部署之前，请阅读上面的[常规说明](#general-description)。

**服务器准备**

* 让基本身份验证标头通过：

   * 允许AEM对用户进行身份验证的一种方法是禁用WebSphere®服务器的全局管理安全性，要实现此目的：转到“安全”>“全局安全性”，然后取消选中“启用管理安全性”复选框，保存并重新启动服务器。

* 设置`"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上下文根= /安装AEM，请更改现有默认Web应用程序的上下文根。

**部署AEM Web应用程序**

* 下载AEM war文件
* 如果需要，在web.xml中进行配置（请参阅上面的“一般说明”）

   * 解压缩WEB-INF/web.xml文件
   * 将sling.run.modes参数更改为发布
   * 取消对sling.home初始参数的注释并根据需要设置此路径
   * 重新打包web.xml文件

* 部署AEM war文件

   * 选择上下文根目录（如果要设置Sling运行模式，则需要选择部署向导的详细步骤，然后在向导的步骤6中指定它）

* 启动AEM Web应用程序

#### Tomcat 11.0.x {#tomcat}

在部署之前，请阅读上面的[常规说明](#general-description)。

* **准备Tomcat服务器**

   * 增加VM内存设置：

      * 在`bin/catalina.bat`中(在UNIX®上为`catalina.sh`)添加以下设置：
      * `set "JAVA_OPTS= -Xmx2048m`

   * 在安装时，Tomcat不启用管理员或管理员访问权限。 因此，您必须手动编辑`tomcat-users.xml`以允许访问这些帐户：

      * 编辑`tomcat-users.xml`以包括管理员和经理的访问权限。 该配置应类似于以下示例：

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
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
      * 重命名tomcat webapps文件夹中的ROOT.war文件夹
      * 再次启动Web应用程序

   * 如果您使用管理器gui安装AEM Web应用程序，则需要增加已上传文件的最大大小，因为默认仅允许50 MB的上传大小。 对于打开管理器Web应用程序的Web.xml，

     `webapps/manager/WEB-INF/web.xml`

     并将max-file-size和max-request-size增加到至少500MB，请参阅以下`multipart-config`示例，了解此类`web.xml`文件。

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
   * 如果需要，在web.xml中进行配置（请参阅上面的“一般说明”）。

      * 解压缩WEB-INF/web.xml文件。
      * 将sling.run.modes参数更改为发布。
      * 取消对sling.home初始参数的注释，并根据需要设置此路径。
      * 重新打包web.xml文件。

   * 如果要将AEM war文件部署为根Web应用程序，请将其重命名为ROOT.war。 如果要将aemauthor重命名为上下文根，请将其重命名为aemauthor.war。
   * 将其复制到tomcat的webapps文件夹中。
   * 等待安装AEM。
