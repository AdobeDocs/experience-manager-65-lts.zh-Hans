---
title: 规划升级
description: 本文有助于在规划AEM升级时制定明确的目标、阶段和可交付成果。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 0%

---

# 规划升级 {#planning-your-upgrade}

## AEM升级概述 {#aem-upgrade-overview}

AEM通常用于高影响力的部署，这些部署可能会为数百万用户提供服务。 通常，实例上会部署自定义应用程序，这会增加复杂性。 任何升级此类部署的工作都需要有条不紊地处理。

本指南有助于在规划升级时制定明确的目标、阶段和交付项。 它侧重于整体升级执行和指南。 虽然提供了实际升级步骤的概述，但它会根据需要参考可用的技术资源。 它应当与本文件提及的可用技术资源一起使用。

AEM升级过程需要仔细处理规划、分析和执行阶段，并为每个阶段定义关键交付项。

>[!NOTE]
>
>最后6个Service Pack支持升级到AEM 6.5 LTS

务必确保您运行的是受支持的操作系统、Java™运行时、httpd和Dispatcher版本。 有关更多信息，请参阅TBD：链接AEM 6.5 LTS的技术要求。 您必须在升级计划中考虑升级这些组件，并且应在升级AEM之前进行升级。

<!-- Alexandru: drafting for now

## Upgrade Scope and Requirements {#upgrade-scope-requirements}

Below you will find a list of areas that are impacted in a typical AEM Upgrade project:

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>Impact</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Operating System</td>
   <td>Uncertain, but subtle effects</td>
   <td>At the time of the AEM upgrade, it may be time to upgrade the operating system as well and this might have some impact.</td>
  </tr>
  <tr>
   <td>Java&trade; Runtime</td>
   <td>Moderate Impact</td>
   <td>AEM 6.3 requires JRE 1.7.x (64 bit) or later. JRE 1.8 is the only version currently supported by Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Moderate Impact</td>
   <td>Online Revision Cleanup requires free<br /> disk space equal to 25% of the repository's size and 15% free heap space<br /> to complete successfully. You may need to upgrade your hardware to<br /> ensure sufficient resources for Online Revision Cleanup to fully<br /> run. Also, if upgrading from a version prior to AEM 6, there<br /> may be additional storage requirements.</td>
  </tr>
  <tr>
   <td>Content Repository (CRX or Oak)</td>
   <td>High Impact</td>
   <td>Starting from version 6.1, AEM does not support CRX2, so a migration to<br /> Oak (CRX3) is required if upgrading from an older version. AEM 6.3 has<br /> implemented a new Segment Node Store that also requires a migration. The<br /> crx2oak tool is used for this purpose.</td>
  </tr>
  <tr>
   <td>AEM Components/Content</td>
   <td>Moderate Impact</td>
   <td><code>/libs</code> and <code>/apps</code> are easily handled through the upgrade, but <code>/etc</code> usually requires some manual reapplication of customizations.</td>
  </tr>
  <tr>
   <td>AEM Services</td>
   <td>Low Impact</td>
   <td>Most AEM core services are tested for upgrade. This is an area of low impact.</td>
  </tr>
  <tr>
   <td>Custom Application Services</td>
   <td>Low to High Impact</td>
   <td>Depending on the application and customization, there may be<br /> dependencies on JVM, operating system versions, and some indexing related<br /> changes, as indexes are not generated automatically in Oak.</td>
  </tr>
  <tr>
   <td>Custom Application Content</td>
   <td>Low to High Impact</td>
   <td>Content that will not be handled through the upgrade can be backed up<br /> before the upgrade takes place and then moved back into the repository.<br /> Most content can be handled through the migration tool.</td>
  </tr>
 </tbody>
</table>

It is important to ensure that you are running a supported operating system, Java&trade; runtime, httpd, and Dispatcher version. For more information, see the [AEM 6.5 Technical Requirements page](/help/sites-deploying/technical-requirements.md). Upgrading these components must be accounted for in your project plan and should take place before upgrading AEM. -->

## 升级阶段 {#upgrade-phases}

规划和运行AEM升级需要完成大量工作。 为了明确在此过程中所做的各种工作，Adobe将规划和执行活动划分为单独的阶段。 在以下部分中，每个阶段都会生成一个交付项，通常在升级的将来阶段使用。

<!-- Alexandru:drafting for now

### Planning for Author Training {#planning-for-author-training}

With any new release, there are potential changes to the UI and user workflows that may be introduced. Also, new releases introduce new features that may be beneficial for the business to use. Adobe recommends reviewing the functional changes that have been introduced and organizing a plan to train your users on using them effectively.

![unu_cropped](assets/unu_cropped.png)

New features in AEM 6.5 can be found in [the AEM section of adobe.com](/help/release-notes/release-notes.md). Make sure to note any changes to UIs or product features that are commonly used in your organization. As you look through the new features, also take note of any that can be of value to your organization. After looking through what has changed in AEM 6.5, develop a training plan for your authors. This could involve using freely available resources like the help feature videos or formal training offered through [Adobe Digital Learning Services](https://learning.adobe.com/). -->

### 创建测试计划 {#creating-a-test-plan}

每个客户的AEM实施都是独一无二的，并且已经过自定义以满足其业务要求。 因此，必须确定已对系统所做的所有自定义设置，以便将其包含在测试计划中。 此测试计划将支持Adobe在已升级的实例上执行的QA过程。

需要复制确切的生产环境，并且应在升级后对其执行测试，以确保所有应用程序和自定义代码仍按需运行。 回退所有自定义设置并运行性能、负载和安全测试。 在组织测试计划时，除了开箱即用的UI和日常操作中使用的工作流之外，还要确保涵盖针对系统所做的所有自定义设置。 这些集成包括自定义OSGI服务和Servlet、与Adobe Experience Cloud的集成、通过AEM连接器与第三方的集成、自定义第三方集成、自定义组件和模板、AEM中的自定义UI叠加以及自定义工作流。 此外，仍应测试自定义查询，以确保其索引在升级后继续有效工作。

### 评估升级复杂性 {#assessing-upgrade-complexity}

由于Adobe客户在其AEM环境中应用的自定义设置的数量和性质多种多样，因此请务必提前一些时间来确定在您的升级中应需要的总体工作级别。 Analyzer for AEM可以帮助您评估升级的复杂性。

适用于AEM 6.5 LTS的AEM Analyzer应该可以相当准确地估计在大多数情况下升级过程中会出现的情况。 但是，对于具有不兼容更改的更复杂的自定义和部署，您可以根据[执行就地升级](/help/sites-deploying/in-place-upgrade.md)中的说明将开发实例升级到AEM 6.5 LTS。 完成后，在此环境中执行一些高级烟雾测试。 本练习的目标不是详尽地完成测试案例清单并生成正式的缺陷清单，而是粗略地估计升级代码以实现6.5 LTS兼容性所需的工作量。 在与AEM分析器和上一节中确定的体系结构更改相结合时，可以为项目管理团队提供粗略的估计，以规划升级。

### 构建升级和回滚Runbook {#building-the-upgrade-and-rollback-runbook}

虽然Adobe已记录升级AEM实例的流程，但每个客户的网络布局、部署架构和自定义都需要对此方法进行微调和定制。 因此，Adobe建议您查看提供的所有文档，并将其用于告知特定于升级的Runbook，其中概述了将在环境中执行的特定升级和回滚过程。

<!--Alexandru:drafting for now

![runbook-diagram](assets/runbook-diagram.png) -->

Adobe在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚过程，以及在执行[就地升级](/help/sites-deploying/in-place-upgrade.md)中应用升级的分步说明。 您应该查看这些说明并与您的系统体系结构、定制和停机时间容差一起考虑，以确定在升级期间将执行的适当的切换和回滚过程。 在起草您的自定义Runbook时，应包括对架构或服务器大小所做的任何更改。

### 制定升级计划 {#developing-an-upgrade-plan}

先前练习的输出可用于构建升级计划，该计划涵盖测试或开发工作、培训和实际升级执行的预期时间线。

<!--Alexandru: drafting for now

![develop-project-plan](assets/develop-project-plan.png) -->

全面的项目计划应包括：

* 最终确定开发和测试计划
* 升级开发和QA环境
* 更新AEM 6.5 LTS的自定义代码库
* QA测试和修复周期
* 升级暂存环境
* 集成、性能和负载测试
* 环境认证
* 上线

### 执行开发和QA {#performing-development-and-qa}

Adobe已提供[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)以与AEM 6.5 LTS兼容的过程。 在运行此迭代过程时，应根据需要对Runbook进行更改。

<!--Alexandru: drafting for now

![patru_cropped](assets/patru_cropped.png) -->

开发和测试过程通常是迭代过程。 在发现需要调整升级过程的问题后，请确保将它们添加到您的自定义升级Runbook中。 在反复测试和修复之后，代码库应该经过完全验证并准备好部署到暂存环境。

### 最终测试 {#final-testing}

Adobe建议在代码库获得贵组织的QA团队认证后进行最后一轮测试。 此轮测试将涉及在暂存环境中验证您的Runbook，然后进行多轮用户验收、性能和安全性测试。

<!--Alexandru: drafting for now

![cinci_cropped](assets/cinci_cropped.png) -->

此步骤至关重要，因为这是您唯一一次能够针对类似生产的环境验证Runbook中的步骤。 升级环境后，请务必留出一些时间让最终用户登录，并完成他们在日常活动中使用系统时执行的活动。 在上线之前发现并纠正这些区域的问题，有助于防止代价高昂的生产中断。

### 执行升级 {#performing-the-upgrade}

一旦从所有利益相关者那里收到最终签发，就应该按照定义的Runbook过程执行。 Adobe在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚步骤，并在执行[就地升级](/help/sites-deploying/in-place-upgrade.md)中提供了安装步骤作为参考点。

![执行升级](assets/perform-upgrade.png)

Adobe在升级说明中为环境验证提供了一些步骤。 这些功能包括基本检查，如扫描升级日志和验证所有OSGi捆绑包是否已正确启动，但Adobe建议同时根据您的业务流程使用您自己的测试用例进行验证。 Adobe还建议检查AEM在线修订清理及相关例程的时间表，以确保在公司保持安静的时间段执行这些操作。 这些例程对于AEM的长期性能至关重要。