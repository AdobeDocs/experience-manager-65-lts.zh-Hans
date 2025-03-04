---
title: 执行就地升级
description: 了解如何为AEM 6.5 LTS执行就地升级。
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: c3df47efd4b13dcd8061e5cdac32a75fbf36df4b
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 执行就地升级 {#performing-an-in-place-upgrade}

>[!NOTE]
>
>此页概述了AEM 6.5 LTS的就地升级过程。 如果您的安装已部署到应用程序服务器，请参阅[应用程序服务器安装的升级步骤](/help/sites-deploying/app-server-upgrade.md)。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)和[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合AEM 6.5 LTS ](/help/sites-deploying/technical-requirements.md)的[要求，并查看[升级计划注意事项](/help/sites-deploying/upgrade-planning.md)以及[Analyzer](/help/sites-deploying/pattern-detector.md)如何帮助您估计复杂性。

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 迁移先决条件 {#migration-prerequisites}

* **最低必需的Java版本：**&#x200B;确保您的系统上安装了Oracle Java™ 17。

## 准备AEM快速入门jar文件 {#prep-quickstart-file}

1. 下载新的AEM 6.5 LTS jar文件

1. [确定正确的升级启动命令](/help/sites-deploying/in-place-upgrade.md#determining-the-correct-upgrade-start-command-determining-the-correct-upgrade-start-command)

1. 如果实例正在运行，则停止该实例

1. 使用新的AEM 6.5 LTS jar替换`crx-quickstart`文件夹之外的旧文件夹

1. 备份`sling.properties`文件（通常存在于`crx-quickstart/conf/`中），然后将其删除

1. 通过运行以下命令来解压缩新的快速入门jar：

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. 解包命令将在`crx-quickstart/conf/`文件夹下生成新的`sling.properties`文件。 您现在可以将自定义更改应用到新生成的`sling.properties`文件。

<!-- Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## 执行升级 {#performing-the-upgrade}

**如果使用S3：**

1. 删除与S3连接器的早期版本关联的`crx-quickstart/install`下的所有jar。

1. 从[https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->下载1.60.2 S3连接器的最新版本

1. 提取S3连接器（版本1.60.2）并复制`crx-quickstart/install`下的以下文件夹的内容，如下所示：

   1. 复制`crx-quickstart/install/1`下的`com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1`
   1. 复制`crx-quickstart/install/15`下的`com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15`

现在，使用通过[确定正确的升级启动命令](#determining-the-correct-upgrade-start-command)部分下的信息确定的新命令启动AEM实例。

### 确定正确的升级启动命令 {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>Java 17中已删除对某些Java 8/11参数的支持，请参阅[Oracle Java™ 17文档](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html)和[AEM 6.5 LTS的Java&amp;trade参数注意事项](https://git.corp.adobe.com/AdobeDocs/experience-manager-65-lts.en/blob/main/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)。

要执行升级，请务必使用jar文件启动AEM以调出实例。

请注意，从启动脚本启动AEM将不会启动升级。 大多数客户都使用启动脚本启动AEM，并已自定义此启动脚本，以包括用于环境配置（如内存设置、安全证书等）的交换机。 因此，Adobe建议遵循以下过程来确定正确的升级命令：

1. 在运行的AEM实例上，从命令行执行以下命令：

   ```shell
   ps -ef | grep java
   ```

1. 查找AEM流程。 它类似于：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通过将现有jar的路径（本例中为`crx-quickstart/app/aem-quickstart*.jar`）替换为`crx-quickstart`文件夹的同级新AEM 6.5 LTS jar来修改命令。 以我们以前的命令为例，我们的命令是：

   ```shell
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar <AEM-6.5-LTS.jar> -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   这将确保所有适当的内存设置、自定义运行模式和其他环境参数都适用于升级。 升级完成后，可以从未来启动时的启动脚本启动实例。

## 部署已升级的代码库 {#deploy-upgraded-codebase}

就地升级过程完成后，应部署更新的代码库。 可以在[升级代码和自定义项页面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到将代码库更新为在AEM的目标版本中工作的步骤。

## 执行升级后检查和故障排除 {#perform-post-upgrade-check-troubleshooting}

请参阅[升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
