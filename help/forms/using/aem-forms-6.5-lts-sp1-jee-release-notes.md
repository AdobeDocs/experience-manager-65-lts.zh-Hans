---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1的发行说明'
description: 查找 [!DNL Adobe Experience Manager] 6.5 LTS SP1的发行信息、新增功能、安装操作说明和详细更改列表
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: c13c6c3d5511a5355570e999e378e4bdf0d7a88f
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 3%

---


# JEE上的Adobe Experience Manager (AEM) Forms 6.5 LTS SP1发行说明

## 版本信息

| **产品** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **版本号** | 6.5 LTS SP1 |
| **类型** | 长期支持服务包(JEE) |
| **版本类别** | 升级版本 |
| **下载URL** | 软件分发 |

## [!DNL Experience Manager] 6.5 LTS SP1中包含的内容 {#what-is-included-in-aem-65ltssp1}

JEE上的Adobe Experience Manager (AEM) Forms **6.5 LTS SP1**&#x200B;提供了多项新功能、客户请求的关键平台更新和常规错误修复，其中重点关注产品稳定性和长期支持。

## AEM Forms 6.5 LTS SP1中包含的内容

### &#x200B;1. Java支持更新

已引入对较新Java版本的支持：

* **Java™ 17**
* **Java™ 21**

### 2.应用程序服务器支持更新

#### JBoss EAP 8支持

* 添加了对&#x200B;**JBoss EAP 8**&#x200B;的支持。
* 已删除旧版&#x200B;**PicketBox**&#x200B;安全框架。
* **基于Elytron的凭据存储**&#x200B;现在支持安全凭据管理。

##### 配置：凭据存储（基于Elytron）

JBoss EAP 8上的AEM Forms使用Elytron管理安全凭据。 客户必须配置基于Elytron的凭据存储区，以确保服务器成功启动和安全数据库身份验证。

有关配置详细信息，请参阅安装和配置指南。

### 3.平台和兼容性更改

#### Servlet规范支持

* 支持&#x200B;**Servlet规范5+**
* 基于&#x200B;**Jakarta EE 9**&#x200B;合规性

#### 命名空间迁移要求

* Jakarta EE 9引入命名空间从`javax.*`更改为`jakarta.*`
* 必须将所有&#x200B;**自定义DSC**&#x200B;迁移到`jakarta.*`命名空间
* AEM Forms 6.5 LTS SP1仅支持&#x200B;**基于Jakarta EE 9+的应用程序服务器**

有关详细信息，请参阅&#x200B;**从javax迁移到jakarta命名空间**。

## 升级

有关详细的升级说明，请参阅JEE上的[AEM Forms 6.5 LTS SP1升级指南](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## 安装

有关安装步骤和先决条件，请参阅&#x200B;**AEM Forms 6.5 LTS SP1 (JEE)**&#x200B;安装指南。

## 支持的平台

有关支持的平台、操作系统、数据库和应用程序服务器的完整列表，请参见：

**支持的平台列表 — AEM Forms 6.5 LTS SP1 (JEE)**

## 已弃用和已移除的功能

* 已删除对CRX存储库持久性的&#x200B;**RDBMK**&#x200B;的支持。
* 对于群集环境，存储库持久性仅支持&#x200B;**MongoMK**。

## 从javax迁移到jakarta命名空间

### 从`javax`到`jakarta`命名空间的迁移

从&#x200B;**AEM Forms 6.5 LTS SP1**&#x200B;开始，仅支持实施&#x200B;**Jakarta Servlet API 5/6**&#x200B;的应用程序服务器。 使用&#x200B;**Jakarta EE 9及更高版本**&#x200B;时，所有API都从`javax.{}`命名空间转换为`jakarta.`。

因此，**所有自定义DSC都必须使用`jakarta`命名空间**。 使用`javax.{}` API构建的自定义组件&#x200B;**与支持的应用程序服务器不兼容**。

### 自定义DSC的迁移选项

您可以使用以下方法之一迁移现有的自定义DSC：

#### 选项1：Source代码迁移（推荐）

* 将所有导入语句从`javax.{}`更新为`jakarta.`
* 重新构建并重新编译自定义DSC项目
* 将更新的组件重新部署到应用程序服务器

**优势：**

* 确保与Jakarta EE 9+长期兼容
* 最适合积极维护的项目

#### 选项2：使用Eclipse转换器进行二进制迁移

* 使用&#x200B;**Eclipse转换器**&#x200B;工具将编译的二进制文件(`.jar`， `.war`)从`javax`转换为`jakarta`
* 无需更改源代码或重新编译
* 将转换后的二进制文件重新部署到应用程序服务器

>[!NOTE]
>
> 在&#x200B;**字节代码级别**&#x200B;执行二进制转换。

导入映射示例

以下是迁移期间所需的命名空间更改的常见示例：

之前(javax)    之后（雅加达）
javax.servlet。*    jakarta.servlet。*
javax.servlet.http。*    jakarta.servlet.http.*

### 导入映射示例

下表显示了从`javax`迁移到`jakarta`时所需的常见命名空间更改：

| 早于(`javax`) | 在(`jakarta`)之后 |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

在更新自定义DSC源代码或验证转换后的二进制文件时，使用这些映射作为引用。

