---
title: 应用程序服务器安装的升级步骤(WLP)
description: 了解如何升级通过Webspehere Liberty部署的AEM实例。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 6a62741ee0ce22a6fb80cf8c68c6eeafacd2e873
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤(WLP) {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>此页概述了AEM 6.5 LTS war on WLP (WebSphere Liberty)的升级过程。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)和[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合AEM 6.5 LTS的要求。 了解Analyzer如何帮助您估计升级的复杂性，并查看制定升级计划（有关详细信息，请参阅[计划升级](/help/sites-deploying/upgrade-planning.md)）。

### 迁移先决条件 {#migration-prerequisites}

* **最低必需的Java版本**：确保已在WLP服务器上安装了IBM Sumeru JRE 17。

### 执行升级 {#performing-the-upgrade}

1. 在开始任何升级活动之前，对实例执行备份。
1. 根据所使用的WLP服务器版本，确定是否需要就地升级或升级。 如果您当前的WLP服务器支持Servlet 6，则可以执行就地升级并继续此文档。 否则，您需要执行副档操作。 对于次要版本，请按照“使用Oak进行内容迁移 — 升级”文档中的说明进行操作 — 待添加的[待定链接]
1. 停止AEM实例。 通常可以通过以下命令来完成：

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 删除不再需要的文件和文件夹。 需要专门移除的项目包括：

   * `dropins`文件夹中的`cq-quickstart-65.war`和扩展的文件夹通常分别位于`<path-to-aem-server>/dropins/cq-quickstart-65.war`和`<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`
   * `launchpad/startup`文件夹。 如果您位于服务器文件夹中，则可以通过在终端中运行以下命令来删除该文件夹：

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar`文件。 您可以通过运行以下命令来实现这一点：

     ```shell
     find crx-quickstart/launchpad -type f -name 
     "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt`文件：

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 通过运行以下命令删除`sling.options`文件：

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * 删除`sling.bootstrap.txt`文件：

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. 备份`sling.properties`文件（通常出现在`crx-quickstart/conf/`中）并将其删除
1. 在`server.xml`文件中将servlet的版本更改为&#x200B;**6.0**
1. 查看AEM服务器的启动参数，并确保根据您的系统要求更新这些参数。 有关详细信息，请参阅[自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
1. 安装Java 17，并通过运行以下各项确保正确安装了该版本：

   ```shell
   java -version
   ```

1. 从Software Distribution下载新的WAR 6.5 LTS，并将其复制到位于`/<path-to-aem-server>/dropins/`的放置文件夹
1. 启动AEM实例：通常可以通过以下命令完成：

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. 如果您在`sling.properties`中有自定义更改，请按照以下说明操作：

   1. 通过运行`<path-to-wlp-directory>/bin/server stop server_name`停止AEM实例
   1. 将您的自定义`sling.properties`更改应用到新生成的`sling.properties`文件（通过引用在步骤6中创建的备份文件）
   1. 启动AEM实例。 通常可以通过运行`<path-to-wlp-directory>/bin/server start server_name`来完成

## 部署已升级的代码库 {#deploy-upgraded-codebase}

就地升级过程完成后，应部署更新的代码库。 您可以在[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)页面中找到将代码库更新为在AEM的目标版本中工作的步骤。

## 执行升级后检查和故障排除 {#perform-post-upgrade-checks-and-troubleshooting}

有关详细信息，请参阅[升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。