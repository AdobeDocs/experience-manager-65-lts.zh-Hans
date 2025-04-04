---
title: 扩展资产编辑器
description: 了解如何使用自定义组件扩展Asset Editor的功能。
contentOwner: AG
role: User, Admin
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
exl-id: a74c52bc-f639-4fc2-90e5-bac24fbb9ade
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 12%

---

# 扩展资产编辑器 {#extending-asset-editor}

资产编辑器是一个页面，单击通过资产共享找到的资产时，将打开该页面，以便用户编辑资产的方面，如元数据、缩略图、标题和标记。

[创建和配置资产编辑器页面](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)中介绍了使用预定义编辑组件的编辑器配置。

除了使用预先存在的编辑器组件之外，[!DNL Adobe Experience Manager]开发人员还可以创建自己的组件。

## 创建资产编辑器模板 {#creating-an-asset-editor-template}

Geometrixx中包含以下示例页面：

* Geometrixx示例页面： `/content/geometrixx/en/press/asseteditor.html`
* 示例模板： `/apps/geometrixx/templates/asseteditor`
* 示例页面组件： `/apps/geometrixx/components/asseteditor`

### 配置Clientlib {#configuring-clientlib}

[!DNL Assets]组件使用WCM edit clientlib的扩展。 clientlibs通常加载到`init.jsp`中。

与默认的clientlib加载（在核心的`init.jsp`中）相比，[!DNL Assets]模板必须具有以下内容：

* 模板必须包含`cq.dam.edit` clientlib （而不是`cq.wcm.edit`）。

* clientlib 还必须包含在禁用的 WCM 模式中（例如，在&#x200B;**发布**&#x200B;时加载）才能渲染谓词、操作和镜头。

在大多数情况下，复制现有示例`init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`)应满足这些需求。

### 配置JS操作 {#configuring-js-actions}

某些[!DNL Assets]组件需要在`component.js`中定义的JS函数。 将此文件复制到组件目录并将其链接。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

该示例在`head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)中加载此JavaScript源。

### 其他样式表 {#additional-style-sheets}

某些[!DNL Assets]组件使用构件库。 要在内容上下文中正确呈现，必须加载其他样式表。 标记操作组件需要多个。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx样式表 {#geometrixx-style-sheet}

示例页面组件要求所有选择器以`static.css` (`/etc/designs/geometrixx/static.css`)的`.asseteditor`开头。 最佳实践：将所有`.asseteditor`选择器复制到样式表并根据需要调整规则。

### FormChooser：最终加载资源的调整 {#formchooser-adjustments-for-eventually-loaded-resources}

资产编辑器使用表单选择器，您可以通过简单地添加表单选择器和表单路径到资产的URL，在同一个表单页面上编辑资源（在本例中是资产）。

例如：

* 纯表单页面： [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 资产已加载到表单页面：[http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

`head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`)中的示例句柄执行以下操作：

* 它们可检测是否加载了资产或是否必须显示普通表单。
* 如果加载了资产，则会禁用WCM模式，因为Parsys只能在纯表单页面上编辑。
* 如果加载了资产，则他们会使用其标题，而不是表单页面上的标题。

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

在HTML部分中，使用前面的标题集（资源或页面标题）：

```html
<title><%= title %></title>
```

## 创建简单的表单字段组件 {#creating-a-simple-form-field-component}

此示例介绍如何构建一个组件，该组件显示并显示加载的资源的元数据。

1. 在项目目录中创建组件文件夹，例如`/apps/geometrixx/components/samplemeta`。
1. 使用以下代码片段添加`content.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 使用以下代码片段添加`samplemeta.jsp`：

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. 为了使组件可用，您需要能够对其进行编辑。要使组件可编辑，请在CRXDE Lite中添加主类型`cq:EditConfig`的节点`cq:editConfig`。 为了删除段落，请添加一个单值为`DELETE`的多值属性`cq:actions`。

1. 导航到浏览器，在示例页面（例如，`asseteditor.html`）上切换到设计模式并为段落系统启用新组件。

1. 在&#x200B;**编辑**&#x200B;模式中，新组件（例如，**示例元数据**）现在可在 Sidekick 中使用（位于&#x200B;**资产编辑器**&#x200B;组中）。插入组件。要能够存储元数据，必须将其添加到元数据表单中。

## 修改元数据选项 {#modifying-metadata-options}

您可以修改[元数据表单](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)中可用的命名空间。

当前可用的元数据在`/libs/dam/options/metadata`中定义：

* 此目录中的第一个级别包含命名空间。
* 每个命名空间中的项表示元数据，例如本地部件项中的结果。
* 元数据内容包含有关类型和多值选项的信息。

可以在`/apps/dam/options/metadata`中覆盖这些选项：

1. 将目录从`/libs`复制到`/apps`。

1. 删除、修改或添加项目。

>[!NOTE]
>
>如果添加新命名空间，则必须在存储库/CRX中注册它们。 否则，提交元数据表单将导致错误。
