---
title: 应用程序服务器安装的升级步骤(WLP)
description: 了解如何升级通过Webspehere Liberty部署的AEM实例。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 2a5d9026-49bc-4766-bcbe-38d834c14f72
source-git-commit: 82af7ee5b3665dcc33b47e05c8580e9981728888
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤(WLP) {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>此页概述了WLP (WebSphere® Liberty)上AEM 6.5 LTS的升级过程。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)和[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合AEM 6.5 LTS[&#128279;](/help/sites-deploying/technical-requirements.md)的要求。

查看[计划升级](/help/sites-deploying/upgrade-planning.md)以及[AEM Analyzer](/help/sites-deploying/aem-analyzer.md)如何帮助您估算升级AEM的复杂性。

### 迁移先决条件 {#migration-prerequisites}

* **最低必需的Java版本**：确保已在WLP服务器上安装了IBM® Sumeru JRE 17。

### 执行升级 {#performing-the-upgrade}

1. 在执行任何升级活动之前，请确保您已完成[预升级](#pre-upgrade-steps)步骤，如备份AEM 6.5服务器
1. 根据您的要求，选择以下升级路径之一：
   1. **就地升级**：如果当前WLP服务器支持Servlet 6，则可以执行就地升级并继续执行步骤3。
   1. **Sidegrade**：如果您喜欢全新设置或WLP服务器不支持Servlet 6，请使用AEM 6.5 LTS设置新的WLP实例，并按照[AEM 6.5到AEM 6.5 LTS的内容迁移使用Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)指南中的说明迁移内容，然后跳到[部署升级后的代码库](#deploy-upgraded-codebase)部分

1. 停止AEM实例。 通常可以通过以下命令来完成：

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 删除不再需要的文件和文件夹。 需要专门移除的项目包括：

   * `dropins`文件夹中的&#x200B;**cq-quickstart-65.war**&#x200B;和`expanded`文件夹通常分别位于`<path-to-aem-server>/dropins/cq-quickstart-65.war`和`<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`
   * `launchpad/startup`文件夹。 如果您位于服务器文件夹中，则可以通过在终端中运行以下命令来删除该文件夹：

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar`文件。 您可以通过运行以下命令来实现这一点：

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
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
1. 安装Java 17，并通过运行以下各项确保正确安装了该版本：

   ```shell
   java -version
   ```

1. 查看AEM服务器的启动参数，并确保根据您的要求更新参数。 有关详细信息，请参阅[Java 17注意事项](/help/sites-deploying/custom-standalone-install.md#java-considerations)。
1. 下载新的6.5 LTS WAR并将其复制到以下位置的放置文件夹： `/<path-to-aem-server>/dropins/`
1. 启动AEM实例：通常可以通过以下命令完成：

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. 如果您在`sling.properties`中有自定义更改，请按照以下说明操作：

   1. 通过运行`<path-to-wlp-directory>/bin/server stop server_name`停止AEM实例
   1. 将您的自定义`sling.properties`更改应用到新生成的`sling.properties`文件（通过引用在步骤5中创建的备份文件）
   1. 启动AEM实例。 通常可以通过运行`<path-to-wlp-directory>/bin/server start server_name`来完成

## 部署已升级的代码库 {#deploy-upgraded-codebase}

升级过程完成后，应部署更新的代码库。 可以在[升级代码和自定义项页面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到将代码库更新为在AEM的目标版本中工作的步骤。

## 执行升级后检查和故障排除 {#perform-post-upgrade-checks-and-troubleshooting}

请参阅[升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
