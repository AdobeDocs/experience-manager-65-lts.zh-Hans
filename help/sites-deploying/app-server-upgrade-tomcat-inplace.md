---
title: 应用程序服务器安装的升级步骤(Tomcat)
description: 了解如何升级通过Tomcat部署的AEM实例。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤（Tomcat — 就地升级） {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>此页概述从AEM 6.5 LTS升级到Tomcat上的AEM 6.5 LTS Servicepack的升级过程（就地升级）。 要从AEM 6.5升级到6.5 LTS，[请参阅此处](/help/sites-deploying/app-server-upgrade-tomcat.md)。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合AEM 6.5 LTS Servicepack[的](/help/sites-deploying/technical-requirements.md)要求，并查看[升级计划注意事项](/help/sites-deploying/upgrade-planning.md)。


### 迁移先决条件 {#migration-prerequisites}

* **所需的最低Java版本**：确保已在Tomcat服务器上安装了Oracle® JRE 17/21。
* **Tomcat服务器**： AEM 6.5 LTS及其ServicePack支持的Tomcat服务器版本为&#x200B;**10.0.x**&#x200B;和&#x200B;**10.1.x**。

### 执行升级 {#performing-the-upgrade}

此过程中的所有示例都使用Tomcat作为Application Server，并暗示您已经部署了AEM 6.5 LTS的工作版本。 此过程用于记录从AEM版本&#x200B;**6.5** LTS到&#x200B;**6.5 LTS** Servicepack执行的升级。

1. 如果已部署AEM 6.5 LTS，请通过访问&#x200B;*`https://<serveraddress:port>/system/console/bundles`*&#x200B;检查捆绑包是否正常运行
1. 接下来，停止AEM 6.5 LTS。 可以通过Tomcat App Manager完成此操作，其地址为： *`https://<serveraddress:port>/manager/html`*
1. 在执行任何升级活动之前，请确保您已完成[预升级](#pre-upgrade-steps)活动，如备份AEM 6.5 LTS服务器
1. 停止AEM 6.5 LTS Tomcat服务器。 在大多数情况下，可以通过从终端运行`./catalina.sh`脚本来达到此目的：

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 删除不再需要的文件和文件夹。 需要专门移除的项目包括：

   * **cq-quickstart-65.war**&#x200B;文件和`cq-quickstart-65`文件夹中的`webapps`文件夹通常位于`<path-to-aem-server>/webapps`
   * `launchpad/startup`文件夹。 如果您位于服务器文件夹中，则可以通过在终端中运行以下命令来删除该文件夹：

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * `base.jar`文件。 您可以通过运行以下命令来实现这一点：

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt`文件：

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 通过运行以下命令删除`sling.options`文件：

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * 删除`sling.bootstrap.txt`文件：

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. 备份`sling.properties`文件（通常出现在`<path-to-aem-server>/bin/crx-quickstart/launchpad/`中）并将其删除
1. 将AEM 6.5 LTS Servicepack war文件复制到`<path-to-aem-server>/webapps`文件夹中
1. 通过运行以下命令启动AEM 6.5 LTS Tomcat服务器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 在AEM启动时监控错误日志，检查是否存在错误，以及AEM是否运行顺利
1. AEM 6.5 LTS启动后，通过访问&#x200B;*`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;检查捆绑包是否正常运行

## 执行升级后检查和故障排除 {#perform-post-upgrade-checks-and-troubleshooting}

有关详细信息，请参阅[升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
