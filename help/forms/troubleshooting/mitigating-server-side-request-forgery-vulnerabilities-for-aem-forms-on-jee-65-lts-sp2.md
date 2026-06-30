---
title: 缓解JEE 6.5 LTS SP2上AEM Forms的服务器端请求伪造(SSRF)漏洞
description: 在JBoss上运行的JEE 6.5 LTS Service Pack 2部署中，针对AEM Forms上的服务器端请求伪造(SSRF)漏洞的缓解步骤。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1d825cd821609504c5e2cff7f7002bf3afe30434
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%

---

# 缓解JEE 6.5 LTS SP2上AEM Forms的服务器端请求伪造(SSRF)漏洞

## 快速参考 {#quick-reference}

| 影响级别 | 受影响的版本 | 建议的操作 |
| --- | --- | --- |
| 严重 | JEE 6.5 LTS Service Pack 2 (6.5 LTS SP2)上的AEM Forms | 手动安装[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| 未受影响 | OSGi、Workbench、Cloud Service上的AEM Forms | 无需执行任何操作 |

已解决的&#x200B;**漏洞：**

* 服务器端请求伪造(SSRF) (CWE-918)

## 概述 {#overview}

### 受影响的内容 {#whats-affected}

| 漏洞 | 影响 | 受影响的组件 |
| --- | --- | --- |
| 服务器端请求伪造(SSRF) (CWE-918) | 攻击者可能会诱使服务器向内部或外部资源发出意外请求 | JEE 6.5 LTS SP2上的AEM Forms |

### 未受影响的内容 {#whats-not-affected}

* Experience Manager Forms Workbench（所有版本）
* OSGi上的Experience Manager Forms（所有版本）
* Experience Manager Forms as a Cloud Service

## 分辨率选项 {#resolution-options}

### 开始之前 {#before-you-start}

在进行任何更改之前，请备份要替换的EAR文件：

* 在部署目录中找到`adobe-edcserver-jboss.ear`：

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* 将文件复制到部署目录之外的安全备份位置。
* 在继续进行任何更新之前，请确保备份完整且可访问。

如果您在更新过程中遇到任何问题，可使用此预防措施恢复原始状态。

### 在JEE 6.5 LTS SP2 (JBoss)上手动安装AEM Forms的修补程序

1. 从[Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)下载`adobe-edcserver-jboss.ear`。

1. 在部署目录中找到`adobe-edcserver-jboss.ear`，并将其替换为下载的文件：

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. 启动AEM Forms Configuration Manager以重新部署更新的EAR并应用修补程序。

1. 重新启动应用程序服务器，并从服务器日志确认部署成功。

## 引用 {#references}

* [Adobe Experience Manager Forms安全最佳实践](/help/forms/using/hardening-securing-aem-forms-environment.md)
