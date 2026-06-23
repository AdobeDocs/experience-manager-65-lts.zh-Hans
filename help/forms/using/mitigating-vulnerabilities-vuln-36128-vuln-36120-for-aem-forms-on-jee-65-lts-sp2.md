---
title: 缓解JEE 6.5 LTS SP2上AEM Forms的VULN-36128和VULN-36120漏洞
description: 在JBoss上运行的JEE 6.5 LTS Service Pack 2部署中，适用于AEM Forms上的VULN-36128和VULN-36120的缓解步骤。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1b876f20cbc3a00a02a4449f0d353fb858695235
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---

# 缓解JEE 6.5 LTS SP2上AEM Forms的VULN-36128和VULN-36120漏洞

## 快速参考 {#quick-reference}

| 影响级别 | 受影响的版本 | 建议的操作 |
| --- | --- | --- |
| 严重 | JEE 6.5 LTS Service Pack 2 (6.5 LTS SP2)上的AEM Forms | 手动安装[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| 未受影响 | OSGi、Workbench、Cloud Service上的AEM Forms | 无需执行任何操作 |

已解决的&#x200B;**漏洞：**

* **VULN-36128**：远程代码执行漏洞允许未经授权的远程攻击者执行任意代码。
* **VULN-36120**：输入验证漏洞不正确，可能会允许对敏感信息进行未经授权的访问。

## 缓解步骤 {#mitigation-steps}

### 开始之前 {#before-you-start}

在进行任何更改之前，请备份要替换的EAR文件：

* 在部署目录中找到`adobe-edcserver-jboss.ear`：

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* 将文件复制到部署目录之外的安全备份位置。
* 在继续进行任何更新之前，请确保备份完整且可访问。

如果您在更新过程中遇到任何问题，可使用此预防措施恢复原始状态。

### 在JEE 6.5 LTS SP2 (JBoss)上手动安装AEM Forms的修补程序 {#manual-hotfix-installation-aem-forms-jee-65-lts-sp2-jboss}

1. 从[Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)下载`adobe-edcserver-jboss.ear`。

1. 在部署目录中找到`adobe-edcserver-jboss.ear`，并将其替换为下载的文件：

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. 启动AEM Forms Configuration Manager以重新部署更新的EAR并完全应用该修补程序。

1. 重新启动应用程序服务器，并从服务器日志确认部署成功。

## 引用 {#references}

* [Adobe Experience Manager Forms安全最佳实践](/help/forms/using/hardening-securing-aem-forms-environment.md)
