---
title: 配置自适应表单缓存
description: 自适应表单缓存专为自适应表单和文档设计。 它会缓存自适应表单和自适应文档，以减少在客户端渲染自适应表单或文档所需的时间。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: a6793fdf-7ee8-4a54-91d8-635eb79ca702
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# 配置自适应表单缓存 {#configure-adaptive-forms-cache}

高速缓存是一种缩短数据访问时间、减少延迟并提高输入/输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于减少在客户端渲染自适应表单所需的时间。 它专为自适应表单而设计。

## 在创作实例和发布实例中配置自适应表单缓存 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 转到`https://[server]:[port]/system/console/configMgr`上的AEM Web控制台配置管理器。
1. 单击&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**&#x200B;以编辑其配置值。
1. 在[!UICONTROL 编辑配置值]对话框中，指定AEM [!DNL Forms]服务器实例可在&#x200B;**[!UICONTROL 自适应Forms数量]**&#x200B;字段中缓存的最大表单数或文档数。 默认值为 100。

   >[!NOTE]
   >
   >要禁用缓存，请将“自适应Forms数量”字段中的值设置为&#x200B;**0**。 禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

   自适应表单HTML缓存的![配置对话框](assets/cache-configuration-edit.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

您的环境配置为使用缓存自适应表单和相关资源。


## （可选）在Dispatcher配置自适应表单缓存 {#configure-the-cache}

您还可以在Dispatcher配置自适应表单缓存，以获得额外的性能提升。

### 前提条件 {#pre-requisites}

* 启用[在客户端](prepopulate-adaptive-form-fields.md#prefill-at-client)合并或预填充数据选项。 它有助于合并预填充表单的每个实例的唯一数据。

### 在Dispatcher上缓存自适应表单的注意事项 {#considerations}

* 使用自适应表单缓存时，请使用AEM [!DNL Dispatcher]来缓存自适应表单的客户端库(CSS和JavaScript)。
* 在开发自定义组件时，在用于开发的服务器上，将禁用自适应表单缓存。
* 不缓存不带扩展名的URL。 例如，缓存了模式为`/content/forms/[folder-structure]/[form-name].html`的URL，缓存时忽略模式为`/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`的URL。 因此，请使用带有扩展名的URL来获得缓存的好处。
* 本地化自适应表单的注意事项：
   * 使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`而不是`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`请求自适应表单的本地化版本
   * [禁止对格式为`http://host:port/content/forms/af/<adaptivefName>.html`的URL使用浏览器区域设置](supporting-new-language-localization.md#how-localization-of-adaptive-form-works)。
   * 当您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，并且在配置管理器中禁用了&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，会提供自适应表单的非本地化版本。 非本地化语言是开发自适应表单时使用的语言。 不会考虑为您的浏览器配置的区域设置（浏览器区域设置），并且会提供自适应表单的非本地化版本。
   * 当您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`并在配置管理器中启用&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，会提供自适应表单的本地化版本（如果可用）。 本地化的自适应表单的语言基于为您的浏览器配置的区域设置（浏览器区域设置）。 它可能会导致[仅缓存自适应表单]的第一个实例。 若要防止实例上发生此问题，请参阅[疑难解答](#only-first-insatnce-of-adptive-forms-is-cached)。

### 在Dispatcher中启用缓存

要在Dispatcher上启用和配置缓存自适应表单，请执行以下步骤：

1. 为环境的每个发布实例打开以下URL，并[为环境的发布实例启用刷新代理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hans#invalidating-dispatcher-cache-from-a-publishing-instance)：
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [将以下内容添加到您的dispatcher.any文件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#automatically-invalidating-cached-files)：

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   添加以上内容时：

   * 自适应表单会保留在缓存中，直到未发布表单的更新版本为止。

   * 发布自适应表单中引用的资源的较新版本时，受影响的自适应表单会自动失效。 引用的资源自动失效有一些例外。 有关异常的解决方法，请参阅[疑难解答](#troubleshooting)部分。
1. [添加以下规则dispatcher.any或自定义规则文件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#specifying-the-documents-to-cache)。 它不包括不支持缓存的URL。 例如，交互式通信。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Do not cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Do not cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Do not cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [将以下参数添加到忽略URL参数列表](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#ignoring-url-parameters)：

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM环境配置为缓存自适应表单。 它会缓存所有类型的自适应表单。 如果在传递缓存的页面之前需要检查页面的用户访问权限，请参阅[缓存受保护内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-hans)。

## 疑难解答 {#troubleshooting}

### 某些包含图像或视频的自适应表单不会从Dispatcher缓存中自动失效 {#videos-or-images-not-auto-invalidated}

#### 问题 {#issue1}

当您通过资产浏览器选择图像或视频并将其添加到自适应表单并在Assets编辑器中编辑这些图像和视频时，包含此类图像的自适应表单不会自动从Dispatcher缓存中失效。

#### 解决方案 {#Solution1}

发布图像和视频后，明确取消发布并发布引用这些资产的自适应表单。

### 仅缓存自适应表单的第一个实例 {#only-first-instance-of-adaptive-forms-is-cached}

#### 问题 {#issue3}

当自适应表单URL没有任何本地化信息，并且在配置管理器中启用了&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，将提供自适应表单的本地化版本。 仅缓存自适应表单的第一个实例并将其交付给每个后续用户。

#### 解决方案 {#Solution3}

通过执行以下步骤来解决问题：

1. 打开conf.d/httpd-dispatcher.conf或配置为在运行时加载的任何其他配置文件。

1. 将以下代码添加到文件中并进行保存。 它是一个示例代码，可对其进行修改以适合您的环境。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
