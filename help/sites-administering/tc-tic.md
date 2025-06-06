---
title: 配置翻译集成框架
description: 了解如何在Adobe Experience Manager中配置翻译集成框架。
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b89e2899-35b9-4105-bfa5-ca21dc6f4e14
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 44%

---

# 配置翻译集成框架{#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成，以编排AEM内容的翻译。

* 连接到您的翻译服务提供商。
* 创建翻译集成框架配置。
* 将云配置与您的页面关联。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

## 连接到翻译服务提供商 {#connecting-to-a-translation-service-provider}

创建用于将AEM连接到您的翻译服务提供商的云配置。

默认情况下，AEM包括[连接到Microsoft® Translator](/help/sites-administering/tc-msconf.md)的功能。 您可在[此处](https://exchange.adobe.com/apps/browse/ec?page=1&amp;partnerLevel=All&amp;product=AEM&amp;q=experience+manager+translation&amp;sort=RELEVANCE)找到具有AEM连接器且是Adobe Exchange合作伙伴计划成员的其他翻译技术供应商。

安装连接器软件包后，即可为连接器创建云配置。一般需要提供凭据，以便向翻译服务进行身份验证。有关为 Microsoft Translator 连接器添加云配置的信息，请参阅[与 Microsoft Translator 集成](/help/sites-administering/tc-msconf.md)。

如果需要，可为同一连接器创建多个云配置。 例如，为您在同一供应商的每个帐户或项目都创建一个配置。

配置连接后，即可创建使用它的翻译集成框架配置。

## 创建翻译集成配置 {#creating-a-translation-integration-configuration}

创建翻译集成框架配置以指定如何翻译您的内容。该配置包括以下信息：

* 要使用的翻译服务提供商。
* 要执行人工翻译还是机器翻译。
* 是否翻译与页面或资产关联的其他内容，如标记。

创建框架配置后，请将云配置与要根据该配置翻译的页面关联。开始翻译过程后，将根据关联的框架配置执行翻译工作流。

当网站的不同部分有不同的翻译要求时，请相应地创建多个框架配置。例如，多语言网站包括英语、西班牙语和日语版本。 站点所有者使用两个不同的翻译服务提供商生成西班牙语和日语译文。因此，配置了两个框架配置。每个配置使用一个不同的翻译服务提供商。

配置翻译集成框架后，可[将它与使用它的页面关联](/help/sites-administering/tc-prep.md)。

**注意：**&#x200B;有关AEM中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

只有一个框架配置可控制如何翻译页面内容和资产。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站点配置属性 {#sites-configuration-properties}

站点属性控制如何执行页面内容的翻译。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架为网站内容执行的翻译方法：</p>
    <ul>
     <li>机器翻译：翻译提供商使用机器翻译实时执行翻译。</li>
     <li>人工翻译：将内容发送到翻译提供商，以供译员进行翻译。 </li>
     <li>不翻译：不发送内容以供翻译。 这是为了跳过某些不翻译但可用最新内容更新的内容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供商。 安装提供商的相应连接器后，列表中即会显示该提供商。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（仅限机器翻译）用于描述所翻译内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译组件字符串</td>
   <td>选择以翻译与页面关联的组件的组件字符串。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与页面关联的标记。</td>
  </tr>
  <tr>
   <td>翻译页面资源</td>
   <td><p>选择如何翻译从文件系统添加到组件或从Assets引用的资源：</p>
    <ul>
     <li>不翻译：不翻译页面资产。</li>
     <li>使用站点翻译工作流：根据在站点选项卡上配置的属性处理Assets。</li>
     <li>使用Assets翻译工作流：根据Assets选项卡上的属性配置处理Assets。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业和划定其范围。</td>
  </tr>
 </tbody>
</table>

### 资源配置属性 {#assets-configuration-properties}

资源属性控制如何配置资源。有关翻译资源的更多信息，请参阅[创建资源的语言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架为资源执行的翻译类型：</p>
    <ul>
     <li>机器翻译：翻译提供商使用机器翻译立即执行翻译。</li>
     <li>人工翻译：自动将内容发送到翻译提供商，以供人工翻译。 </li>
     <li>不翻译：不发送Assets以供翻译。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供商。 安装提供商的相应连接器后，列表中即会显示该提供商。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（仅限机器翻译）用于描述所翻译内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译资源</td>
   <td>选择以在翻译项目中包含资产。 </td>
  </tr>
  <tr>
   <td>翻译元数据</td>
   <td>选择以翻译资源元数据。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与资源关联的标记。</td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业或划定其范围。</td>
  </tr>
 </tbody>
</table>

1. 单击侧栏中的工具>操作>云>云服务。
1. 在翻译集成区域，是否已创建任何配置决定了将显示哪个链接：

   * 如果尚未创建任何配置，请单击“立即配置”。
   * 如果配置已经存在，请单击“显示配置”，然后单击“可用配置”旁边显示的+链接。

1. 键入配置的名称，然后单击“创建”。
1. 在站点和Assets选项卡上配置属性，然后单击确定。

## 配置页面以供翻译 {#configuring-pages-for-translation}

要配置如何将您的源页面翻译为其他语言，请将这些页面与以下云配置关联：

* 用于将 AEM 连接到您的翻译服务提供商的云配置。
* 用于配置翻译细节的翻译集成框架。

翻译集成框架云配置标识要用于连接到服务提供商的云配置。 将源页面与框架云配置关联时，该页面必须与该框架云配置使用的服务提供商云配置关联。

将页面与云配置关联时，该页面的后代页面继承这种关联。例如，如果将/content/geometrixx/en/products页面与翻译集成框架关联，则根据该框架翻译产品页面及其下的所有页面。

必要时，可在后代页面上取代该关联。例如，网站的内容主要与服装有关。 但某个分支的页面介绍公司情况。站点的根页面与指定使用“服装”类别进行机器翻译的翻译集成框架关联。 描述公司情况的分支使用框架，该框架使用“常规”类别执行机器翻译。

### 将页面与翻译提供商关联 {#associating-a-page-with-a-translation-provider}

将页面与您用于翻译该页面和后代页面的翻译提供商关联。

1. 在站点控制台中，选择要配置的页面，然后单击查看属性。
1. 单击编辑，然后单击云服务选项卡。
1. 单击添加配置>翻译集成。
1. 选择要使用的翻译提供商，然后单击完成。

### 将页面与翻译集成框架关联 {#associating-pages-with-a-translation-integration-framework}

将页面与定义您要如何为该页面和后代页面执行翻译的翻译集成框架关联。

1. 在站点控制台中，选择要配置的页面，然后单击查看属性。
1. 单击编辑，然后单击云服务选项卡。
1. 单击添加配置>翻译集成。
1. 选择要使用的翻译集成框架，然后单击完成。
