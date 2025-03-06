---
title: JBoss® Linux®环境中的AEM Forms JEE 6.5.15.0 Service Pack安装问题
description: AEM Forms JEE 6.5.15.0 Service Pack未在JBoss® Linux®环境中正确安装，任何修补程序更改都不会应用到应用程序服务器。 将'RUP_BOM.xml'文件添加到XML目录中。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
exl-id: ba3a5c1e-19db-49cf-ac64-513a6077f3e9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# JBoss®环境中的AEM Forms 6.5.15.0 JEE Service Pack安装问题 {#aem-forms-installation-issue-environment}

## 问题 {#issue}

未在JBoss® Linux®环境中正确安装AEM Forms JEE 6.5.15.0 Service Pack。 在`PatchInstallerProcessing[1-9*].log`文件中记录日志条目`[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`。 此条目表示AEM Forms JEE 6.5.15.0 Service Pack的安装不成功。

## 应用到 {#applies-to}

此解决方案适用于：
* JBoss® Linux®环境

>[!NOTE]
>
> 在执行[将RUP_BOM.xml文件添加到XML目录](#solution-solution)的步骤之前，请确保应用程序服务器上至少安装一次AEM Forms JEE 6.5.15.0 Service Pack。

## 解决方案 {#solution}

要修复安装问题，请将`RUP_BOM.xml`文件添加到AEM Forms JEE 6.5.15.0 Service Pack的XML目录中：
1. 导航到从中提取修补程序`AEMForms-6.5.0-0057_jboss_linux.tar.gz`的文件夹。
1. 导航到`/CDROM_Installers/Linux/Disk1/InstData`位置并找到`Resource1.zip`文件。
1. 将`Resource1.zip`文件复制到解压缩文件夹之外的其他位置，然后解压缩`Resource1.zip`文件。
1. 导航到`/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml`并复制`RUP_BOM.xml`文件。
1. 将RUP_BOM.xml文件粘贴到`[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`。
1. 重新安装[AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
