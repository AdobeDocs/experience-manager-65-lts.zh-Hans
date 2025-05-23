---
title: 云服务配置
description: 您可以扩展现有实例以创建您自己的配置
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6b9b8d8c-8cd5-4c21-9b75-acd74d00354a
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# 云服务配置{#cloud-service-configurations}

配置旨在提供存储服务配置的逻辑和结构。

您可以扩展现有实例以创建自己的配置。

## 概念 {#concepts}

开发配置时采用的原则基于以下概念：

* 服务/适配器用于检索配置。
* 配置（例如属性/段落）继承自父项。
* 按路径从Analytics节点引用。
* 易于扩展。
* 能够灵活地满足更复杂的配置，如[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 支持依赖项(例如，[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)插件需要[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)配置)。

## 结构 {#structure}

配置的基本路径为：

`/etc/cloudservices`。

对于每种类型的配置，都提供了模板和组件。 这使得在定制后具有可以满足大多数需求的配置模板成为可能。

要为新服务提供配置，请执行以下操作：

* 创建服务页面

  `/etc/cloudservices`

* 在此项下：

   * 配置模板
   * 配置组件

模板和组件必须从基础模板继承`sling:resourceSuperType`：

`cq/cloudserviceconfigs/templates/configpage`

或基本组件

`cq/cloudserviceconfigs/components/configpage`

服务提供商还应提供服务页面：

`/etc/cloudservices/<service-name>`

### 模板 {#template}

您的模板扩展了基本模板：

`cq/cloudserviceconfigs/templates/configpage`

并定义指向自定义组件的`resourceType`。

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 组件 {#components}

您的组件应该扩展基本组件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

设置模板和组件后，您可以通过在下添加子页面来添加配置：

`/etc/cloudservices/<service-name>`

### 内容模型 {#content-model}

内容模型作为`cq:Page`存储在以下位置：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

这些配置存储在子节点`jcr:content`下。

* 在对话框中定义的固定属性应直接存储在`jcr:node`上。
* 动态元素（使用`parsys`或`iparsys`）使用子节点存储组件数据。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

有关API的参考文档，请参阅[com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### AEM集成 {#aem-integration}

可用服务列在&#x200B;**Cloud Service属性**&#x200B;对话框（继承自`foundation/components/page`或`wcm/mobile/components/page`的任何页面）的&#x200B;**页面**&#x200B;选项卡中。

该选项卡还提供：

* 指向可启用服务的位置的链接
* 从路径字段选择配置（服务的子节点）

#### 密码加密 {#password-encryption}

存储服务的用户凭据时，应对所有密码进行加密。

您可以通过添加隐藏表单字段来实现此目的。 此字段的属性名称中应包含批注`@Encrypted`；即，对于`password`字段，名称将写为：

`password@Encrypted`

然后，`EncryptionPostProcessor`将自动加密该属性（使用`CryptoSupport`服务）。

>[!NOTE]
>
>这类似于标准` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)`注释。

>[!NOTE]
>
>默认情况下，`EcryptionPostProcessor`只加密向`/etc/cloudservices`发出的`POST`请求。

#### 服务页jcr：content节点的其他属性 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>componentreference</td>
   <td>要自动包含在页面中的组件的引用路径。<br />这用于附加功能和JS包含项。<br />这包括包含<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br />的页面上的组件（通常在<code>body</code>标记之前）。<br />在Adobe Analytics和Adobe Target中，我们使用此功能来包含附加功能，例如，用于跟踪访问者行为的JavaScript调用。</td>
  </tr>
  <tr>
   <td>说明</td>
   <td>服务的简短描述。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>服务的扩展描述。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>在列表中使用的服务排名。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>用于在页面属性对话框中显示配置的过滤器。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>服务网站的URL。</td>
  </tr>
  <tr>
   <td>serviceURL标签</td>
   <td>服务URL标签。</td>
  </tr>
  <tr>
   <td>thumbnailpath</td>
   <td>服务的缩略图路径。</td>
  </tr>
  <tr>
   <td>可见</td>
   <td>在页面属性对话框中可见；默认情况下可见（可选）</td>
  </tr>
 </tbody>
</table>

### 用例 {#use-cases}

默认提供以下服务：

* [跟踪器代码片段](/help/sites-administering/external-providers.md)(Google、WebTrends等)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另请参阅[创建自定义Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md)。
