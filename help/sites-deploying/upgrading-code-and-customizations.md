---
title: 升级代码和自定义项
description: 了解有关在AEM中升级代码和自定义设置的更多信息。
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6b94caf1-97b7-4430-92f1-4f4d0415aef3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 升级代码和自定义项{#upgrading-code-and-customizations}

在计划升级时，必须调查并解决实施的以下方面。

* [升级代码库](#upgrade-code-base)
* [测试过程](#testing-procedure)

## 概述 {#overview}

1. **AEM Analyzer** — 按照升级计划中的说明运行AEM Analyzer，在[使用AEM Analyzer评估升级复杂性](/help/sites-deploying/aem-analyzer.md)页面中有详细介绍。 您会获得一个AEM Analyzer报告，该报告包含有关在AEM的Target版本中不可用的API/捆绑包之外，还必须解决的区域的更多详细信息。 AEM Analyzer报告会向您指示代码中的任何不兼容性。 如果不存在任何部署，则表明您的部署已经与6.5 LTS兼容。 您仍然可以选择为使用6.5 LTS功能而执行新开发，但并非只是为了保持兼容性。
1. **开发6.5 LTS的代码库** — 为Target版本的代码库创建专用分支或存储库。 使用升级前兼容性中的信息来规划要更新的代码区域。
1. **使用6.5 LTS Uber jar编译** — 更新代码库POM以指向6.5.2025 uber jar并编译针对它的代码。
1. **部署到6.5 LTS环境** - AEM 6.5 LTS的干净实例（创作+发布）应出现在开发/QA环境中。 应部署更新后的代码库和有代表性的内容示例（来自当前生产）。
1. **QA验证和错误修复** - QA应在6.5.2025的Author和Publish实例上验证应用程序。找到的任何错误都应修复并提交到6.5 LTS代码库。 根据需要重复Dev-Cycle，直到修复所有错误。

在继续升级之前，您应该有一个稳定的应用程序代码库，此代码库已针对AEM 6.5 LTS进行了全面测试。

## 升级代码库 {#upgrade-code-base}

### 在版本控制{#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}中为6.5 LTS代码创建专用分支

应使用某种形式的版本控制来管理实施AEM所需的所有代码和配置。 应创建版本控制中的专用分支，以管理目标版本AEM中的代码库所需的任何更改。 此分支管理针对AEM的目标版本迭代测试代码库以及后续错误修复。

### 更新AEM Uber Jar版本 {#update-the-aem-uber-jar-version}

AEM Uber jar将所有AEM API作为单个依赖项包含在您的Maven项目的`pom.xml`中。 最佳做法始终是将Uber Jar作为单个依赖项包含在内，而不是包含单个AEM API依赖项。 升级代码库时，将Uber Jar的版本更改为指向AEM的6.5 LTS版本。 更新任何已弃用的API或方法，以便与AEM的目标版本兼容。 针对新版本的Uber Jar重新编译代码库。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>AEM 6.5和AEM 6.5 LTS Uber Jar的打包方式略有不同。 请参阅以下部分：

适用于AEM 6.5的&#x200B;**Uber Jar**

1. `uber-jar-6.5.x.jar` — 包含AEM 6.5的所有公共API。
1. `uber-jar-6.5.x-apis-with-deprecations.jar` — 包括AEM 6.5中的公共API和已弃用的API。

适用于AEM 6.5 LTS的&#x200B;**Uber Jar**

对于AEM 6.5 LTS，再次存在两种类型的Uber Jar：

1. `uber-jar-6.6.x-apis.jar` — 包含AEM 6.5 LTS的所有公共API。
1. `uber-jar-6.6.x-deprecated-apis.jar` — 仅包含AEM 6.5 LTS中已弃用的API。

**主要区别： AEM 6.5与AEM 6.5 LTS Uber Jar**

* 在AEM 6.5中，如果同时需要公共的和已弃用的API，则可以在`pom.xml`文件中使用包含单个jar `uber-jar-6.5.x-apis-with-deprecations.jar`。
* 在AEM 6.5 LTS中，如果您同时需要公共API和已弃用的API，则必须包含两个单独的jar，即公共API的`uber-jar-6.6.x-apis.jar`和已弃用的API的`uber-jar-6.6.x-deprecated-apis.jar`。

已弃用的API Jar的&#x200B;**Maven坐标**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 开发人员备注 {#developer-notes}

* AEM 6.5 LTS不包括现成的Google guava库，可以根据需要安装所需的版本。
* Sling XSS包现在使用Java HTML清理器库，应使用`XSSAPI#filterHTML()`方法安全地呈现HTML内容，而不是将数据传递到其他API。

## 测试过程 {#testing-procedure}

应该为测试升级准备全面的测试计划。 测试已升级的代码库和应用程序必须先在较低的环境中完成。 发现的错误应以迭代方式修复，直到代码库稳定为止，只有到那时才应升级更高级别的环境。

### 测试升级过程 {#testing-upgrade-procedure}

此处概述的升级过程应在开发和QA环境中进行测试，如自定义运行手册中所述（请参阅[计划升级](/help/sites-deploying/upgrade-planning.md)）。 应重复升级过程，直到所有步骤都记录在升级运行手册中且升级过程顺利完成。

### 实施测试区域  {#implementation-test-areas-}

以下是任何AEM实施的重要方面，在升级环境并部署升级的代码库后，测试计划应涵盖这些方面。

<table>
 <tbody>
  <tr>
   <td><strong>功能测试区域</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>已发布的站点</td>
   <td>通过Dispatcher在发布层<br />上测试AEM实现和相关代码。 应包括页面更新和<br />缓存失效的条件。</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>在创作层上测试AEM实施和相关代码。 应包括页面、组件创作和对话框。</td>
  </tr>
  <tr>
   <td>与Experience Cloud解决方案集成</td>
   <td>验证与Analytics等产品的集成。</td>
  </tr>
  <tr>
   <td>与第三方系统的集成</td>
   <td>验证创作层和发布层上的任何第三方集成。</td>
  </tr>
  <tr>
   <td>身份验证、安全和权限</td>
   <td>任何身份验证机制（如LDAP/SAML）都应进行验证。应在创作层和发布层<br />上测试<br />权限和组。</td>
  </tr>
  <tr>
   <td>查询</td>
   <td>应测试自定义索引和查询以及查询性能。</td>
  </tr>
  <tr>
   <td>UI自定义</td>
   <td>创作环境中AEM UI的任何扩展或自定义设置。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>自定义和/或现成的工作流和功能。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td>加载测试应在模拟现实场景的创作层和发布层上执行。</td>
  </tr>
 </tbody>
</table>

### 记录测试计划和结果 {#document-test-plan-and-results}

应创建涵盖上述实施测试区域的测试计划。 通常，按作者和发布任务列表划分测试计划是合理之举。 此测试计划应在升级生产环境之前在开发、QA和暂存环境中执行。 测试结果和性能量度应在较低级别环境中捕获，以便在升级暂存环境和生产环境时进行比较。
