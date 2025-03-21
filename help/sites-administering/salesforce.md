---
title: 与Salesforce集成
description: 了解如何将Adobe Experience Manager (AEM)与Salesforce集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 68003650-76d7-40b3-860b-70454c13211e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---

# 与Salesforce集成 {#integrating-with-salesforce}

将Salesforce与Adobe Experience Manager (AEM)集成提供了商机管理功能，并使用Salesforce提供的现成功能。 您可以配置AEM将潜在客户发布到Salesforce，并创建直接从Salesforce访问数据的组件。

AEM与Salesforce之间的双向可扩展集成使您能够：

* 组织可充分利用和修改数据以提升客户体验。
* 从营销活动到销售活动的参与。
* 自动从Salesforce数据存储区传输和接收数据的组织。

本文档将介绍以下内容：

* 如何配置Salesforce云服务(配置AEM以与Salesforce集成)。
* 如何在Client Context和Personalization中使用Salesforce潜在客户/联系人信息。
* 如何使用Salesforce工作流模型将AEM用户作为潜在客户发布到Salesforce。
* 如何创建一个显示Salesforce中数据的组件。

## 配置AEM以与Salesforce集成 {#configuring-aem-to-integrate-with-salesforce}

要配置AEM以便与Salesforce集成，首先需要在Salesforce中配置远程访问应用程序。 然后，将Salesforce云服务配置为指向此远程访问应用程序。

>[!NOTE]
>
>您可以在Salesforce中创建免费的开发人员帐户。

要配置AEM以与Salesforce集成，请执行以下操作：

>[!CAUTION]
>
>在继续此过程之前，请安装[Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip)集成包。 有关如何使用包的更多详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md#package-share)页面。

1. 在AEM中，导航到&#x200B;**云服务**。 在第三方服务中，单击&#x200B;**Salesforce**&#x200B;中的&#x200B;**立即配置**。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 创建配置，例如&#x200B;**开发人员**。

   >[!NOTE]
   >
   >新配置将重定向到新页面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**。 该值与在Salesforce中创建远程访问应用程序时必须在回调URL中指定的值完全相同。 这些值必须匹配。

1. 登录到您的Salesforce帐户(或者，如果您没有帐户，请在[https://developer.salesforce.com](https://developer.salesforce.com)处创建一个帐户。)
1. 在Salesforce中，导航到&#x200B;**创建** > **应用程序**&#x200B;以访问&#x200B;**连接的应用程序**(在以前版本的Salesforce中，工作流是&#x200B;**部署** > **远程访问**)。
1. 单击&#x200B;**新建**，以便您可以将AEM与Salesforce连接。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 输入&#x200B;**连接的应用程序名称**、**API名称**&#x200B;和&#x200B;**联系电子邮件**。 选中&#x200B;**启用OAuth设置**&#x200B;复选框，然后输入&#x200B;**回调URL**&#x200B;并添加OAuth作用域（例如，完全访问）。 回调URL类似于： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   更改服务器名称/端口号和页面名称以匹配您的配置。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 单击&#x200B;**保存**&#x200B;以保存Salesforce配置。 Salesforce创建了&#x200B;**使用者密钥**&#x200B;和&#x200B;**使用者密钥**，您需要这两个密钥来配置AEM。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >等待几分钟（最多15分钟）以激活Salesforce中的远程访问应用程序。

1. 在AEM中，导航到&#x200B;**云服务**，然后导航到您之前创建的Salesforce配置（例如，**开发人员**）。 单击&#x200B;**编辑**，然后从salesforce.com输入客户密钥和客户密钥。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登录 Url | 这是Salesforce授权端点。 其值是预填充的，适用于大多数情况。 |
   |---|---|
   | 客户密钥 | 输入从salesforce.com中的“远程访问应用程序注册”页获得的值 |
   | 客户密码 | 输入从salesforce.com中的“远程访问应用程序注册”页获得的值 |

1. 单击&#x200B;**连接到Salesforce**&#x200B;以进行连接。 Salesforce要求您允许配置连接到Salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，将打开一个确认对话框，告知您已成功连接。

1. 导航到网站的根页面，然后单击&#x200B;**页面属性**。 然后选择&#x200B;**云服务**&#x200B;并添加&#x200B;**Salesforce**&#x200B;并选择正确的配置（例如，**开发人员**）。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   现在，您可以使用工作流模型将潜在客户发布到Salesforce，并创建从Salesforce访问数据的组件。

## 将AEM用户导出为Salesforce潜在客户 {#exporting-aem-users-as-salesforce-leads}

如果要将AEM用户导出为Salesforce潜在客户，请配置工作流以将潜在客户发布到Salesforce。

要将AEM用户导出为Salesforce潜在客户，请执行以下操作：

1. 通过右键单击工作流&#x200B;**Salesforce.com导出**&#x200B;并单击&#x200B;**开始**，导航到`http://localhost:4502/workflow`处的Salesforce工作流。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 选择要作为此工作流的&#x200B;**有效负荷**&#x200B;创建潜在客户的AEM用户（主页>用户）。 请确保选择用户的配置文件节点，因为它包含映射到Salesforce潜在客户的&#x200B;**FirstName**&#x200B;和&#x200B;**LastName**&#x200B;字段的&#x200B;**givenName**&#x200B;和&#x200B;**familyName**&#x200B;等信息。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >在开始此工作流之前，AEM中的潜在客户节点在发布到Salesforce之前必须填写某些必填字段。 这些是&#x200B;**givenName**、**familyName**、**company**&#x200B;和&#x200B;**电子邮件**。 要查看AEM用户与Salesforce潜在客户之间的映射的完整列表，请参阅[AEM用户与Salesforce潜在客户之间的映射配置。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 单击&#x200B;**确定**。 用户信息将导出到salesforce.com。 您可以在salesforce.com中进行验证。

   >[!NOTE]
   >
   >错误日志显示是否导入了商机。 有关详细信息，请查看错误日志。

### 配置Salesforce.com导出工作流 {#configuring-the-salesforce-com-export-workflow}

如有必要，请配置Salesforce.com导出工作流以使其与正确的Salesforce.com配置匹配，或进行其他更改。

要配置Salesforce.com导出工作流，请执行以下操作：

1. 导航到`http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 打开Salesforce.com导出步骤，选择&#x200B;**参数**&#x200B;选项卡，选择正确的配置并单击&#x200B;**确定**。 此外，如果您希望工作流重新创建在Salesforce中删除的潜在客户，请选中该复选框。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 单击&#x200B;**保存**&#x200B;以保存更改。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM用户与Salesforce潜在客户之间的映射配置 {#mapping-configuration-between-aem-user-and-salesforce-lead}

要查看或编辑AEM用户与Salesforce潜在客户之间的当前映射配置，请打开配置管理器： `https://<hostname>:<port>/system/console/configMgr`并搜索&#x200B;**Salesforce潜在客户映射配置**。

1. 通过单击&#x200B;**Web控制台**&#x200B;或直接转到`https://<hostname>:<port>/system/console/configMgr.`打开配置管理器
1. 搜索&#x200B;**Salesforce潜在客户映射配置**。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 根据需要更改映射。 默认映射遵循模式&#x200B;**aemUserAttribute=sfLeadAttribute**。 单击&#x200B;**保存**&#x200B;以保存更改。

## 配置Salesforce客户端上下文存储 {#configuring-salesforce-client-context-store}

Salesforce客户端上下文存储显示有关当前登录用户的附加信息，而不显示AEM中已提供的信息。 它会根据用户与Salesforce的连接，从Salesforce中提取此附加信息。

为此，请配置以下内容：

1. 通过AEM Connect组件将Salesforce用户与Salesforce ID关联。
1. 将Salesforce配置文件数据添加到客户端上下文页面，以便您可以配置要查看的属性。
1. （可选）构建一个使用Salesforce客户端上下文存储中的数据的区段。

### 将AEM用户与Salesforce ID关联 {#linking-an-aem-user-with-a-salesforce-id}

用Salesforce ID映射AEM用户，以便在客户端上下文中加载它。 在真实情景中，您将基于已知用户数据与验证进行关联。 出于演示目的，在此过程中使用&#x200B;**Salesforce Connect**&#x200B;组件。

1. 导航到AEM中的网站，登录，然后从Sidekick中拖放&#x200B;**Salesforce Connect**&#x200B;组件。

   >[!NOTE]
   >
   >如果&#x200B;**Salesforce Connect**&#x200B;组件不可用，请转到&#x200B;**设计**&#x200B;视图并将其选中以使其在&#x200B;**编辑**&#x200B;视图中可用。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   将组件拖动到页面时，该组件显示&#x200B;**链接到Salesforce=关**。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此组件仅用于演示目的。 对于真实情景，将有另一个流程将用户与潜在客户关联起来/匹配。

1. 在页面上拖动组件后，请打开该组件以对其进行配置。 选择配置、联系人类型以及Salesforce潜在客户或联系人，然后单击&#x200B;**确定**。

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM将用户与Salesforce联系人或商机关联。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 将Salesforce数据添加到客户端上下文 {#adding-salesforce-data-to-client-context}

您可以在Client Context中从Salesforce加载用户数据以用于个性化：

1. 通过导航到要扩展的客户端上下文，例如`http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 将&#x200B;**Salesforce配置文件数据**&#x200B;组件拖动到客户端上下文。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 双击组件以将其打开。 选择&#x200B;**添加项**&#x200B;并从下拉列表中选择属性。 添加所需数量的属性，然后选择&#x200B;**确定**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 现在，您会在客户端上下文中显示Salesforce中特定于Salesforce的属性。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用Salesforce客户端上下文存储中的数据构建区段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以生成一个使用Salesforce客户端上下文存储中的数据的区段。 要执行此操作：

1. 通过转到&#x200B;**工具** > **分段**&#x200B;或转到[http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)，导航到AEM中的分段。
1. 创建或更新区段以包含来自Salesforce的数据。 有关详细信息，请参阅[分段](/help/sites-administering/campaign-segmentation.md)。

## 搜索潜在客户 {#searching-leads}

AEM附带了一个示例搜索组件，该组件根据给定的条件在Salesforce中搜索潜在客户。 此组件向您展示如何使用Salesforce REST API搜索Salesforce对象。 要触发对salesforce.com的调用，请将页面与Salesforce配置链接到一起。

>[!NOTE]
>
>这是一个示例组件，向您展示了如何使用Salesforce REST API查询Salesforce对象。 以为例，根据您的需求创建更复杂的组件。

要使用此组件，请执行以下操作：

1. 导航到要使用此配置的页面。 打开页面属性并选择&#x200B;**云服务。**&#x200B;单击&#x200B;**添加服务**&#x200B;并选择&#x200B;**Salesforce**&#x200B;和相应的配置，然后单击&#x200B;**确定**。

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 将Salesforce搜索组件拖动到页面（前提是它已启用）。 要启用该功能，请转到“设计”模式并将其添加到相应的区域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 打开搜索组件并指定搜索参数，然后单击&#x200B;**确定。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM显示搜索组件中指定的符合指定条件的潜在客户。

   ![chlimage_1-87](assets/chlimage_1-87.png)
