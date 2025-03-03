---
title: 应用程序服务器安装的升级步骤(Tomcat)
description: 了解如何升级通过Tomcat部署的AEM实例。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8798c608ea168d753be2a08b25a0d0d344b0fef6
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤(Tomcat) {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>此页概述针对Tomcat的AEM 6.5 LTS战争的升级过程。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)和[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合AEM 6.5 LTS的要求。 了解Analyzer如何帮助您估计升级的复杂性，并查看制定升级计划（有关详细信息，请参阅[计划升级](/help/sites-deploying/upgrade-planning.md)）。

### 迁移先决条件 {#migration-prerequisites}

* **所需的最低Java版本**：确保已在Tomcat服务器上安装了IBM Sumeru JRE 17。
* **Tomcat服务器**： 6.5 LTS所需的Tomcat服务器的版本是&#x200B;**11.0.x**。

### 执行升级 {#performing-the-upgrade}

此过程中的所有示例都使用Tomcat作为应用程序服务器，并暗示您已部署AEM的工作版本。 此过程旨在记录从AEM版本&#x200B;**6.5**&#x200B;到&#x200B;**6.5 LTS**&#x200B;执行的升级。

1. 如果已部署AEM 6.5，请通过访问&#x200B;*`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;检查捆绑包是否正常运行
1. 接下来，停止AEM 6.5。可以通过Tomcat App Manager完成此操作，其地址为： *`https://<serveraddress:port>/manager/html`*
1. 在执行任何升级活动之前，请确保您已完成[预升级](#pre-upgrade-steps)活动，如备份AEM 6.5服务器
1. 安装Java 17，并通过运行以下命令确保其正确安装：

   ```
   java –version
   ```

1. 设置与AEM 6.5 LTS兼容的Tomcat服务器
1. 查看AEM服务器的启动参数，并确保根据系统要求更新参数。 有关详细信息，请参阅[自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
1. 使用Java 17在Tomcat服务器上部署新下载的6.5 LTS战争，并通过运行以下命令启动AEM 6.5 LTS Tomcat服务器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 在AEM启动并运行后，通过访问*`https://<serveraddress:port>/cq/system/console/bundles*`确保所有捆绑包都处于运行状态
1. 现在停止AEM 6.5 LTS Tomcat服务器。 在大多数情况下，可以通过从终端运行`./catalina.sh`脚本来达到此目的：

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 现在，使用本教程将您的内容从AEM 6.5迁移到AEM 6.5 LTS：[使用Oak升级将AEM 6.5内容迁移到AEM 6.5 LTS](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. 迁移内容后，在`sling.properties`文件中应用所需的任何自定义更改
1. 通过运行以下命令启动AEM 6.5 LTS Tomcat服务器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 在AEM启动时监控错误日志，检查是否存在错误，以及AEM是否运行顺利
1. AEM 6.5 LTS启动后，通过访问&#x200B;*`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;检查捆绑包是否正常运行

## 部署已升级的代码库 {#deploy-upgraded-codebase}

就地升级过程完成后，应部署更新的代码库。 您可以在[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)页面中找到将代码库更新为在AEM的目标版本中工作的步骤。

## 执行升级后检查和故障排除 {#perform-post-upgrade-checks-and-troubleshooting}

有关详细信息，请参阅[升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。