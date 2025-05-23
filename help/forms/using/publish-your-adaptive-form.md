---
title: 教程：发布自适应表单
description: 将自适应表单发布为AEM页面，将表单嵌入到AEM Sites页面，或将自适应表单嵌入到外部网页中
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: de5cc19f-f3dc-42d5-877d-c15bd00487d7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# 教程：发布自适应表单 {#tutorial-publish-your-adaptive-form}

![主页图像](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是[创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步骤。 建议按时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

在自适应表单准备就绪后，您可以发布表单以使其对最终用户可用。 最终用户可以在任何设备和互联网浏览器上打开已发布的表单。 发布自适应表单时，表单和相关内容将从AEM创作实例复制到AEM发布实例。 该表单通过发布实例提供给最终用户。

您可以通过以下方法发布自适应表单：

* [将自适应表单发布为AEM页面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [将自适应表单嵌入到AEM Sites页面中](#embed-the-adaptive-form-in-an-aem-sites-page)
* [将自适应表单嵌入到外部网页(托管在AEM外部的非AEM网页)中](../../forms/using/publish-your-adaptive-form.md)

## 开始之前 {#before-you-start}

* **[设置AEM Forms发布实例](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**：发布实例是以发布模式运行的AEM [!DNL Forms]的面向公众的实例。 在生产环境中，发布实例位于组织的防火墙之外。
* **[设置复制和反向复制](https://helpx.adobe.com/cn/experience-manager/6-3/help/sites-deploying/replication.html)**：复制操作将内容从创作实例复制到发布实例，并将用户输入（例如，表单输入）从发布实例返回到创作实例。

## 将自适应表单发布为AEM页面 {#publish-the-adaptive-form-as-an-aem-page}

将自适应表单发布为AEM页面时，整个网页只包含已发布的表单。 您可以使用自适应表单的URL将其从其他网页链接。 要将&#x200B;**shipping-address-add-update-form**&#x200B;自适应表单发布为AEM页面，请执行以下操作：

1. 登录到AEM [!DNL Forms]创作实例，然后在AEM [!DNL Forms] UI中找到shipping-address-add-update-form自适应表单。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 选择shipping-address-add-update-form自适应表单，然后选择&#x200B;**[!UICONTROL 发布]**。 此时将显示一个对话框，其中包含与自适应表单相关的资源。 选择&#x200B;**[!UICONTROL 发布]**。 自适应表单已发布，并且显示成功对话框。
1. 在发布实例上打开表单。 该表单可供最终用户填写和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 将自适应表单嵌入到AEM Sites页面中 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms]允许表单开发人员将自适应表单无缝嵌入到AEM [!DNL Sites]页面中。 嵌入的自适应表单功能齐全，用户无需离开页面即可填写并提交表单。它有助于用户停留在网页上其他元素的上下文中，同时与表单交互。

AEM [!DNL Forms]提供了一个组件AEM [!DNL Forms]容器，用于将自适应表单嵌入到AEM [!DNL Sites]页面。 默认情况下，该组件在AEM [!DNL Sites]容器中不可见。 执行以下步骤以启用AEM [!DNL Forms]容器组件并将自适应表单嵌入到AEM [!DNL Sites]页面中：

1. 在We.Retail网站中创建并打开页面以进行编辑。 例如，[https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 自适应表单已嵌入到[!DNL Sites]页面。

   您还可以在现有We.Retail [!DNL Site's]页面中嵌入自适应表单。 例如，“关于我们”页面[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 这样可节省创建页面的时间。 以下步骤使用新创建的页面。

   We.Retail网站随AEM一起提供。 如果未安装We.Retail网站，请参阅[We.Retail参考实施](https://helpx.adobe.com/cn/experience-manager/6-3/help/sites-developing/we-retail.html)安装网站。

1. 选择![属性](assets/properties.png)页面信息并在新创建的We.Retail网站页面中选择&#x200B;**[!UICONTROL 编辑模板]**&#x200B;选项。 将在浏览器的新选项卡中打开页面模板。
1. 在&#x200B;**[!UICONTROL 布局容器]**&#x200B;框中选择，然后选择![馈送管理](assets/feedmanagement.png)。 在&#x200B;**[!UICONTROL 允许的组件]**&#x200B;选项卡中，展开&#x200B;**[!UICONTROL 常规]**&#x200B;折叠面板，选择&#x200B;**[!UICONTROL AEM表单]**&#x200B;选项，然后选择![保存图标](assets/save_icon.svg)。 已为页面启用AEM [!DNL Forms]容器组件。

1. 打开浏览器选项卡，该选项卡包含在步骤1中打开的AEM [!DNL Sites]页面。 选择&#x200B;**[!UICONTROL 将组件拖动到此处]**&#x200B;框并选择&#x200B;**+。**&#x200B;在&#x200B;**[!UICONTROL 插入新组件]**&#x200B;框中，选择&#x200B;**[!UICONTROL AEM表单]**。 已将&#x200B;**[!UICONTROL AEM Forms Container]**&#x200B;组件添加到该页面。
1. 选择&#x200B;**[!UICONTROL AEM Forms container]**&#x200B;组件并选择![configure-icon](assets/configure-icon.svg)。 此时将显示一个包含AEM [!DNL Forms]容器属性的对话框。 在&#x200B;**[!UICONTROL 资产路径]**&#x200B;字段中，浏览并选择shipping-address-add-update-form自适应表单。 选择![保存图标](assets/save_icon.svg)。 自适应表单将嵌入到页面中。
1. 发布自适应表单和[!DNL Sites]页面。 以下是需要考虑的一些要点：

   * 如果您首次发布AEM [!DNL Sites]页面并且它包含嵌入表单，请发布[!DNL Sites]页面和嵌入表单。
   * 如果仅修改已发布站点页面中的嵌入表单，请发布原始表单，所做的更改将反映在已发布的站点页面中。 已发布的站点页面包含对表单的引用，无需重新发布页面。
   * 如果您修改[!DNL Sites]页面和嵌入的表单，请重新发布[!DNL Sites]页面和表单。

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   已将配送和帐单地址更改表单添加到AEM [!DNL Sites]页面。

## 将自适应表单嵌入到外部网页中 {#embed-the-adaptive-form-in-an-external-webpage}

通过在外部网页中插入几行AEM，您可以将自适应表单嵌入到外部网页(托管在AEM外部的非JavaScript网页)中。 JavaScript代码向AEM [!DNL Forms]服务器发送自适应表单和相关资源的HTTP请求，并将自适应表单添加到网页。 有关详细步骤，请参阅[将自适应表单嵌入到外部网页](/help/forms/using/embed-adaptive-form-external-web-page.md)。
