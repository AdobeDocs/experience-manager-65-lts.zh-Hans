---
title: 开发工具
description: 要开发JCR、Apache Sling或Adobe Experience Manager应用程序，可以使用多个工具集。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 46db0690-03e9-4b31-aa44-200f224f3707
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---

# 开发工具{#development-tools}

要开发JCR、Apache Sling或Adobe Experience Manager (AEM)应用程序，可以使用以下工具集：

* 由[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)和WebDAV组成的集。 CRXDE Lite已嵌入到CRX/AEM中，使您能够在该浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在日志记录和与SVN集成时创建和编辑文件(如.jsp和.java)、文件夹、模板、组件、对话框、节点、属性和捆绑包。

  在以下情况下，建议您使用CRXDE Lite：无法直接访问CRX/AEM服务器；通过扩展或修改现成组件和Java™捆绑包来开发应用程序；不需要专用调试器、代码完成和语法高亮显示。

* 一组包含以下内容：
   * 集成开发环境。 例如，[Eclipse](/help/sites-developing/howto-projects-eclipse.md)或[IntelliJ](/help/sites-developing/ht-intellij.md)。
   * 构建工具。 例如，[Apache Maven](/help/sites-developing/ht-projects-maven.md)。
   * FileVault ，由Adobe开发，用于将存储库映射到文件系统（版本控制系统）。 例如，Subversion。
   * 错误跟踪器系统。 例如，Jira。
   * 一种中央依赖性管理系统。 例如，Apache Archiva。
   * 以及构建自动化系统。 例如，Apache Continuum。

  通过此设置，您可以将应用程序（内容、代码、配置）完全集成到任何开发环境和流程中。 不同元素之间的链接是通过FileVault表示存储库的文件系统，因为前面提到的所有开发工具都可以处理文件。

## 集成开发环境的扩展 {#extensions-for-integrated-development-environments}

Adobe发布了以下扩展：

* [AEM Eclipse扩展](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets扩展](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM附带了其他有助于开发的工具：

* [对话框编辑器](/help/sites-developing/dialog-editor.md)
* [使用 Translator 管理词典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse开发AEM项目](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA开发AEM项目](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理服务器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 现代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo 工具](/help/sites-developing/aem-repo-tool.md)

有助于创建新项目的工具：

* [AEM项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM Lazybone模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>以下教程可能对启动新的AEM项目有帮助：
>[AEM Sites快速入门第1部分 — 项目设置](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
