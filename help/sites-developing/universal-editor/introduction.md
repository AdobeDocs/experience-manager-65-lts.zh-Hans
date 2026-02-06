---
title: 通用编辑器
description: 了解通用编辑器的灵活性，以及它如何帮助您使用AEM 6.5 LTS增强Headless体验。
feature: Developing
role: Developer
exl-id: 495df631-5bdd-456b-b115-ec8561f33488
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 42%

---

# 关于通用编辑器 {#universal-editor}

了解通用编辑器的灵活性，以及它如何帮助您使用AEM 6.5 LTS增强Headless体验。

## 概述 {#overview}

通用编辑器是一个多功能可视化编辑器，是 Adobe Experience Manager Sites 的一部分。它允许作者对任何Headless体验进行“所见即所得”(WYSIWYG)编辑。

* 作者受益于通用编辑器的灵活性。 它支持对所有形式的AEM Headless内容进行相同一致的可视化编辑。
* 开发人员同样能够从通用编辑器的多样性中获益，因为它还支持对实施的真正解耦。它使开发人员几乎可以使用他们选择的任何框架或架构，而无需施加任何SDK或技术限制。

请参阅 [AEM as a Cloud Service 文档中有关通用编辑器的章节](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)，以了解更多详细信息。

## 架构 {#architecture}

通用编辑器是一项与 AEM 协同工作的服务，用于以 Headless 方式创作内容。

* 通用编辑器托管在`https://experience.adobe.com/#/aem/editor/canvas`，可以编辑AEM 6.5 LTS渲染的页面。
* 通用编辑器从AEM创作实例中通过Dispatcher读取AEM页面。
* 运行在与 Dispatcher 相同的主机上的通用编辑器服务会将更改写回 AEM 作者实例。

![使用通用编辑器的创作流程](assets/author-flow.png)

## 要求 {#requirements}

以下内容支持通用编辑器：

* AEM 6.5 LTS GA
   * 支持内部部署和Adobe Managed Services (AMS)托管。
* [AEM 6.5](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * 支持内部部署和AMS托管。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)（版本`2023.8.13099`或更高版本）

本文档重点介绍对通用编辑器的AEM 6.5 LTS支持。 要将通用编辑器与AEM 6.5 LTS结合使用，您需要满足以下条件：

* AEM 6.5 LTS GA
* 正确配置 Dispatcher

## 设置 {#setup}

要使用通用编辑器，请执行以下操作：

1. [在AEM创作实例上配置服务。](#configure-aem)
1. [设置本地通用编辑器服务。](#set-up-ue)
1. [调整您的Dispatcher以允许Universal Editor服务。](#update-dispatcher)

完成设置后，您即可[对应用程序进行接入配置，以使用通用编辑器。](#instrumentation)

### 配置服务 {#configure-aem}

Universal Editor依赖于许多必须配置的服务。

#### 为 `login-token` cookie 设置 SameSite 属性。 {#samesite-attribute}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Adobe Granite 令牌身份验证处理程序**，并点击&#x200B;**更改配置值**。
1. 在对话框中，**将 login-token cookie 的 SameSite 属性**（`token.samesite.cookie.attr`）值修改为 `Partitioned`。
1. 单击&#x200B;**保存**。

#### 移除 `SAMEORIGIN` 标头中的 X-Frame 选项。 {#sameorigin}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Apache Sling Main Servlet**，并点击&#x200B;**编辑配置值**。
1. 如果存在，请从`X-Frame-Options=SAMEORIGIN` 附加响应标头&#x200B;**属性（**）中删除 `sling.additional.response.headers` 值。
1. 单击&#x200B;**保存**。

#### 配置Adobe Granite查询参数身份验证处理程序 {#query-parameter}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Adobe Granite 查询参数身份验证处理程序**，并点击&#x200B;**编辑配置值**。
1. 在&#x200B;**路径**&#x200B;字段（`path`）中，添加 `/` 以启用。
   * 如果该字段为空，则会禁用此身份验证处理程序。
1. 单击&#x200B;**保存**。

#### 定义在通用编辑器中打开的内容路径或`sling:resourceTypes` {#paths}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到&#x200B;**通用编辑器 URL 服务**，然后点击&#x200B;**编辑配置值**。
1. 定义应为哪些内容路径或 `sling:resourceTypes` 打开通用编辑器。
   * 在&#x200B;**通用编辑器打开映射**&#x200B;字段中，提供通用编辑器为其打开的路径。
   * 在应由通用编辑器&#x200B;**字段打开的:resourceTypesSling**&#x200B;中，输入通用编辑器直接打开的资源的列表。
1. 单击&#x200B;**保存**。
1. 检查您的[外部化器配置](/help/sites-developing/externalizer.md)，并确保至少按照以下示例设置了本地、作者和发布环境：

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成这些配置步骤后，AEM将按以下顺序打开页面的通用编辑器：

1. AEM检查`Universal Editor Opening Mapping`下的映射，如果内容位于该处定义的任何路径下，则为其打开通用编辑器。

1. 对于`Universal Editor Opening Mapping`中定义的路径之外的内容，AEM检查内容`resourceType`是否与&#x200B;**Sling:resourceTypes中的条目匹配，该条目应由通用编辑器**&#x200B;打开。 如果匹配，AEM将在`${author}${path}.html`处的通用编辑器中打开该内容。
1. 否则，AEM将打开页面编辑器。

在 `Universal Editor Opening Mapping` 中，可使用以下变量来定义映射：

* `path`：要打开的资源的内容路径
* `localhost`： `localhost`的Externalizer项没有架构，例如`localhost:4502`
* `author`：没有架构的作者的Externalizer条目，例如`localhost:4502`
* `publish`：用于无架构发布的外部化器条目，例如`localhost:4503`
* `preview`：用于预览的外部化器项，不带架构，例如`localhost:4504`
* `env`：`prod`、`stage`、`dev` 基于已定义的 Sling 运行模式
* `token`：`QueryTokenAuthenticationHandler` 需要查询令牌

映射示例：

* 打开 AEM 作者上 `/content/foo` 下的所有页面：
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 打开`https://localhost:4502/content/foo/x.html?login-token=<token>`的结果
* 打开远程 NextJS 服务器上 `/content/bar` 下的所有页面，提供所有变量的信息
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 打开`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`的结果

### 设置通用编辑器服务 {#set-up-ue}

在更新并配置好 AEM 后，您可以为本地开发和测试搭建本地通用编辑器服务。

1. 安装 Node.js 版本 >=20。
1. 从[Software Distribution](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud/software-distribution/home)下载并解压缩最新的通用编辑器服务
1. 通过环境变量或`.env`文件配置通用编辑器服务。
   * [有关详细信息，请参阅 AEM as a Cloud Service 通用编辑器文档。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 请注意，如果需要重写内部 IP，可能需要使用 `UES_MAPPING` 选项。
1. 运行 `universal-editor-service.cjs`

### 更新 Dispatcher {#update-dispatcher}

如果配置了AEM并且运行了本地Universal Editor服务，则需要在Dispatcher中允许新服务[的反向代理。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/dispatcher)

1. 调整创作实例的vhost文件以包含反向代理。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >默认端口为 8080。如果在[您的 `.env` 文件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)中通过 `UES_PORT` 参数更改了端口值，则必须在此处相应调整。

1. 重新启动 Apache。

## 检测您的应用程序 {#instrumentation}

在更新 AEM 并运行本地通用编辑器服务后，您可以开始使用通用编辑器编辑 Headless 内容。

但是，必须检测应用程序以利用通用编辑器。 其中涉及包括元标记，以指示编辑器如何以及在何处保留内容。 有关此接入配置的详细信息，请参阅 [AEM as a Cloud Service 的通用编辑器文档。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

请注意，如果遵循AEM as a Cloud Service通用编辑器的相关文档，则在将其与AEM 6.5 LTS结合使用时将会应用以下更改。

* 元标记中的协议必须为 `aem65`，而不是 `aem`。

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 必须通过元标记来声明通用编辑器服务的端点。

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 在组件定义的 `plugins` 部分中，必须使用 `aem65` 而不是 `aem`。

>[!TIP]
>
>有关通用编辑器的全面开发人员指南，请参阅AEM as a Cloud Service文档中的[面向AEM开发人员的通用编辑器概述](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)。 请注意本节中描述的AEM 6.5 LTS更改。

## AEM 6.5 LTS与AEM as a Cloud Service之间的差异 {#differences}

AEM 6.5 LTS中的通用编辑器与AEM as a Cloud Service中的通用编辑器工作方式大致相同，包括UI和大部分设置。 但是，您应该注意一些差异。

* 6.5 LTS中的通用编辑器仅支持Headless用例。
* 对于6.5 LTS，通用编辑器的设置略有不同（[，如当前文档中的](#setup)所述）。
* 6.5 LTS中的通用编辑器使用与AEM as a Cloud Service不同的资产选取器和内容片段选取器。
