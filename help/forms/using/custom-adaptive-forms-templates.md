---
title: 创建自定义自适应表单模板
description: 本文介绍了如何创建自定义自适应表单模板。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
exl-id: 20e958d7-5976-4ccd-99b6-0e3bdb424d2d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# 创建自定义自适应表单模板{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms引入了动态模板。 您可以使用AEM Sites模板编辑器[创建或编辑动态模板](../../forms/using/template-editor.md)。 下文中提到的模板是静态模板。 这些选项在默认安装中不可用。 [安装兼容包](../../forms/using/compatibility-package.md)以在您的环境中获取这些模板。

## 前提条件 {#prerequisites}

* 了解AEM [页面模板](/help/sites-authoring/templates.md)和[自适应表单创作](https://helpx.adobe.com/cn/aem-forms/6-1/introduction-forms-authoring.html)

* 了解AEM [客户端库](/help/sites-developing/clientlibs.md)

## 自适应表单模板 {#adaptive-form-template}

自适应表单模板是专用的AEM页面模板，具有某些用于创建自适应表单的属性和内容结构。 模板具有预配置的布局、样式和基本初始内容结构。

创建表单后，对原始模板内容结构所做的任何更改都不会反映在表单中。

## 默认自适应表单模板 {#default-adaptive-form-templates}

AEM QuickStart提供了以下自适应表单模板：

* 调查模板：允许您使用已配置多列的响应式布局创建单页自适应表单。 布局会根据您希望显示表单的各种屏幕的尺寸自动进行调整。
* 简单注册模板：允许您使用向导布局创建多步自适应表单。 在此布局中，您可以为每个步骤指定步骤完成表达式，该表达式将在向导继续下一步之前验证。
* 选项卡式注册模板：允许您使用左选项卡式布局创建多选项卡式自适应表单，在该表单中，您可以按任意顺序访问选项卡。
* 高级注册模板：允许您创建具有多个选项卡和向导的表单。 它使用左侧的选项卡布局，可让您按任意顺序访问选项卡。 它使用Adobe Document Cloud设计服务进行签名和验证。
* 空白模板：允许您创建没有任何页眉、页脚和初始内容的表单。 您可以添加文本框、按钮和图像等组件。 空白模板允许您创建可[嵌入到AEM网站页面](/help/forms/using/embed-adaptive-form-aem-sites.md)中的表单。

这些模板将`sling:resourceType`属性设置为相应的页面组件。 页面组件呈现包含自适应表单容器的CQ页面，进而呈现自适应表单。

下表枚举模板与页面组件之间的关联：

<table>
 <tbody>
  <tr>
   <td><p><strong>模板</strong></p> </td>
   <td><p><strong>页面组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用模板编辑器创建自适应表单模板 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用模板编辑器指定自适应表单的结构和初始内容。 例如，您希望所有表单作者在注册表单中都拥有几个文本框、导航按钮和提交按钮。 您可以创建一个模板，以供作者创建与其他注册表单一致的表单。 通过AEM模板编辑器，您可以：

* 在结构层中添加表单的页眉和页脚组件
* 提供表单的初始内容。
* 指定主题。
* 指定提交、重置和导航等操作。

有关详细信息，请参阅[模板编辑器](../../forms/using/template-editor.md)。

## 从CRXDE创建自适应表单模板 {#creating-an-adaptive-form-template-from-crxde}

您可以创建模板并使用它来创建自适应表单，而不是使用可用的模板。 自定义模板基于引用自适应表单容器和页面元素（如页眉和页脚）的各种页面组件。

您可以使用网站的基础页面组件创建这些组件。 或者，您可以扩展现成模板使用的自适应表单的页面组件。

执行以下步骤以创建自定义模板，如simpleEnrollmentTemplate。

1. 在创作实例上导航到CRXDE Lite 。

1. 在/apps目录下，为应用程序创建文件夹结构。 例如，如果应用程序名称为mycompany，请使用此名称创建一个文件夹。 通常，应用程序文件夹包含组件、配置、模板、src和安装目录。 在本例中，创建“组件”、“配置”和“模板”文件夹。

1. 导航到文件夹/libs/fd/af/templates。
1. 复制`simpleEnrollmentTemplate`节点。
1. 导航到文件夹/apps/mycompany/templates。 右键单击并选择&#x200B;**[!UICONTROL 粘贴]**。
1. 如有必要，请重命名复制的模板节点。 例如，将其重命名为注册模板。

1. 导航到位置/apps/mycompany/templates/enrollment-template。

1. 修改`jcr:content`节点的`jcr:title`和`jcr:description`属性，以区分模板和您复制的模板。

1. 修改模板的`jcr:content`节点包含`guideContainer`和`guideformtitle`组件。 `guideContainer`是保存自适应表单的容器。 `guideformtitle`组件显示应用程序名称、描述等。

   您可以包含自定义组件或`parsys`组件，而不是`guideformtitle`。 例如，移除`guideformtitle`，然后添加自定义组件或`parsys`组件节点。 请确保组件的`sling:resourceType`属性引用了该组件，并在页面`component.jsp`文件中定义了该组件。

1. 导航到位置/apps/mycompany/templates/enrollment-template/jcr：content。

1. 打开&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡，并将`cq:designPath`属性的值更改为/etc/designs/mycompany。

1. 现在为`cq:Page`类型创建一个/etc/designs/mycompany节点。

## 创建自适应表单页面组件 {#create-an-adaptive-form-page-component}

自定义模板的样式与默认模板相同，因为模板引用页面组件/libs/fd/af/components/page/base。 您可以在节点/apps/mycompany/templates/enrollment-template/jcr：content中找到作为属性`sling:resourceType`的组件引用。 由于基础是核心产品组件，因此请勿修改此组件。

1. 导航到节点/apps/mycompany/templates/enrollment-template/jcr：content并将属性`sling:resourceType`的值修改为/apps/mycompany/components/page/enrollmentpage
1. 将节点/libs/fd/af/components/page/base复制到文件夹/apps/mycompany/components/page。

1. 将复制的组件重命名为`enrollmentpage`。

1. **（仅当您已有contentpage时）**&#x200B;如果您的网站已有`contentpage`组件，请执行以下步骤(a-d)。 如果您的网站没有现有的`contentpage`组件，则可以保留`resourceSuperType`属性以指向现成的基本页。

   1. 对于`enrollmentpage`节点，将属性`sling:resourceSuperType`的值设置为mycompany/components/page/contentpage。 `contentpage`组件是站点的基本页面组件。 其他页面组件可以对其进行扩展。 删除`enrollmentpage`下的脚本文件，`head.jsp`、`content.jsp`和`library.jsp`除外。 `sling:resourceSuperType`组件（在本例中为`contentpage`）包含所有此类脚本。 标题（包括导航栏和页脚）继承自`contentpage`组件。

   1. 打开文件`head.jsp`。

      JSP文件包含行`<cq.include script="library.jsp"/>`。

      `library.jsp`文件包含`guide.theme.simpleEnrollment`客户端库，该库包含自适应表单的样式。

      页面组件`enrollmentpage`有一个独占的`head.jsp`文件，该文件覆盖`contentpage`组件的`head.jsp`文件。

   1. 将`contentpage`组件的`head.jsp`文件的所有脚本包含到`enrollmentpage`组件的`head.jsp`文件中。
   1. 在`content.jsp`脚本中，您可以添加其他页面内容或对页面渲染时包含的其他组件的引用。 例如，如果添加自定义组件`applicationformheader`，请确保在JSP文件中添加对该组件的以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同样，如果在模板节点结构中添加`parsys`组件，则还应包括自定义组件。

## 创建自适应表单客户端库 {#creating-an-adaptive-form-client-library}

新模板的`enrollmentpage`组件的`head.jsp`文件包含客户端库`guide.theme.simpleEnrollment`。 默认模板也使用此客户端库。 使用以下方法之一更改新模板中的样式：

* 定义自定义主题并将默认主题`guide.theme.simpleEnrollment`替换为自定义主题。
* 在/etc/designs/mycompany下定义新的客户端库。 在jsp页中的默认主题条目后包括客户端库。 在此客户端库中包含所有覆盖的样式和其他Java脚本文件。

>[!NOTE]
>
>主题是指用于呈现自适应表单的页面组件中包含的客户端库。 客户端库主要控制自适应表单的外观。
