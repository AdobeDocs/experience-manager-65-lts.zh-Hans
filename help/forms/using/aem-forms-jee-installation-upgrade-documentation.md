---
title: 适用于AEM Forms on JEE的安装和升级工作流
description: JEE (JBoss)上的AEM Forms 6.5 LTS的安装和升级工作流，以及相关PDF及其用途的整合列表。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# 适用于AEM Forms on JEE的安装和升级工作流 {#aem-forms-jee-installation-upgrade-documentation}

## 应用到 {#applies-to}

该文档适用于&#x200B;**AEM 6.5 LTS Forms**。

使用以下工作流和表格为您的方案选择正确的指南。 某些文档以PDF形式发布；随着时间推移，可能会添加其他文档。

## 安装和升级工作流 {#installation-upgrade-workflow}

1. 查看JEE上的AEM Forms的[支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)，并确保您的系统满足所需的软件/硬件组合。
2. 决定您是执行&#x200B;**全新安装**&#x200B;还是&#x200B;**升级**。
3. 对于您选择的路径，请按照下面所述的顺序操作（某些情况需要多个指南）。

## 预安装和预升级步骤 {#start-here}

| 指南 | 描述 |
| --- | --- |
| JEE上的AEM Forms的[支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md) | 列出AEM Forms on JEE支持的软件和硬件组合。 使用此选项可在开始安装或升级之前验证先决条件。 |
| [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md) | 介绍推荐的体系结构和部署拓扑，以便您可以选择与您的环境匹配的方法（例如，单服务器与群集）。 |
| [为AEM Forms安装选择持久性类型](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | 帮助您在开始之前为安装拓扑选择适当的持久性类型。 |

## 如何在JBoss上的JEE上安装Adobe Experience Manager Forms (AEM Forms)？ {#installing-aem-forms-jee-jboss}

### 全包式 {#install-jee-jboss-turnkey}

| 指南 | 描述 |
| --- | --- |
| [使用JBoss Turnkey (PDF)在JEE上安装和部署AEM Forms 6.5 LTS](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | 用于在JBoss上进行&#x200B;**全新统包安装**。 本文档提供了有关使用JBoss全包分发在JEE上安装和部署AEM Forms的说明。 |

### 单个服务器（非全包式） {#install-jee-jboss-single-server}

| 指南 | 描述 |
| --- | --- |
| [准备安装AEM Forms （单服务器） (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | 在&#x200B;**之前**&#x200B;使用&#x200B;**全新单服务器（非全包安装）安装**。 本文档列出了在单服务器拓扑中在JEE上安装AEM Forms的先决条件和环境准备步骤。 |
| [在JEE for JBoss (PDF)上安装和部署AEM Forms ](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | 用于在JBoss （**非密钥**）上在JEE上逐步安装和部署&#x200B;**AEM Forms的**。 对于单服务器安装，请在&#x200B;**完成**&#x200B;准备安装AEM Forms （单服务器）*后*&#x200B;遵循本指南。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## 如何在JEE on JBoss上升级Adobe Experience Manager Forms (AEM Forms)？ {#upgrading-aem-forms-jee-jboss}

### 全包式 {#upgrade-jee-jboss-turnkey}

| 指南 | 描述 |
| --- | --- |
| [在JEE上升级到AEM Forms 6.5 LTS for JBoss Turnkey (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | 用于&#x200B;**全包升级**。 本文档提供了有关在JEE JBoss全包安装中升级现有AEM Forms的说明。 |

### 单个服务器 {#upgrade-jee-jboss-single-server}

| 指南 | 描述 |
| --- | --- |
| [准备升级AEM Forms (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | 在&#x200B;**之前使用**&#x200B;进行&#x200B;**单服务器升级**。 介绍在升级到AEM 6.5 LTS Forms之前如何准备环境。 它适用于以单服务器安装模式在JEE上运行AEM Forms的环境。 |
| [在JEE上升级到AEM Forms for JBoss (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | 在&#x200B;**单服务器**&#x200B;安装模式下，用于JBoss上的&#x200B;**逐步升级过程**。 在&#x200B;**完成**&#x200B;准备升级AEM Forms *后，请遵循本指南*。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

