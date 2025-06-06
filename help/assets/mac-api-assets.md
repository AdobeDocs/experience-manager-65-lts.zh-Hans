---
title: '[!DNL Assets] HTTP API。'
description: 在 [!DNL Adobe Experience Manager Assets]中使用HTTP API创建、读取、更新、删除和管理数字资源。
contentOwner: AG
role: Developer
feature: Assets HTTP API,Developer Tools
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 7bb4aec8-e6c0-416a-a318-d3120f9688c4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# [!DNL Assets] HTTP API {#assets-http-api}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

## 概述 {#overview}

[!DNL Assets] HTTP API允许对数字资源执行创建 — 读取 — 更新 — 删除(CRUD)操作，包括对元数据、演绎版和评论的操作，以及使用[!DNL Experience Manager]内容片段的结构化内容。 它在`/api/assets`中公开，并作为REST API实现。 它包括对内容片段[&#128279;](/help/assets/assets-api-content-fragments.md)的支持。

要访问API，请执行以下操作：

1. 在`https://[hostname]:[port]/api.json`处打开API服务文档。
1. 关注指向`https://[hostname]:[server]/api/assets.json`的[!DNL Assets]服务链接。

API响应是适用于某些MIME类型的JSON文件，是适用于所有MIME类型的响应代码。 JSON响应是可选的，可能不可用于（例如）PDF文件。 依靠响应代码进行进一步分析或执行操作。

在[!UICONTROL 结束时间]后，无法通过[!DNL Assets] Web界面和HTTP API使用资产及其演绎版。 如果[!UICONTROL 开启时间]是未来的时间，或者[!UICONTROL 结束时间]是过去的时间，则API会返回404错误消息。

>[!CAUTION]
>
>[HTTP API更新`jcr`命名空间中的元数据属性](#update-asset-metadata)。 但是，Experience Manager用户界面会更新`dc`命名空间中的元数据属性。

## 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊类型的资产。 它可用于访问结构化数据，如文本、数字、日期等。 由于`standard`资产（如图像或文档）存在若干差异，因此处理内容片段时适用一些其他规则。

有关详细信息，请参阅Experience Manager Assets HTTP API中的[内容片段支持](/help/assets/assets-api-content-fragments.md)。

## 数据模型 {#data-model}

[!DNL Assets] HTTP API公开两个主要元素：文件夹和资源（用于标准资源）。

此外，它会为描述内容片段中结构化内容的自定义数据模型显示更详细的元素。 有关详细信息，请参阅[内容片段数据模型](/help/assets/assets-api-content-fragments.md#content-fragments)。

### 文件夹 {#folders}

文件夹类似于传统文件系统中的目录。 它们是其他文件夹或断言的容器。 文件夹具有以下组件：

**实体**：文件夹的实体是其子元素，可以是文件夹和资源。

**属性**：

* `name`是文件夹的名称。 这与URL路径中没有扩展的最后一个区段相同。
* `title`是文件夹的可选标题，可以显示它而不是其名称。

>[!NOTE]
>
>文件夹或资产的某些属性映射到不同的前缀。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`前缀已替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

**链接**&#x200B;文件夹显示三个链接：

* `self`：链接到自身。
* `parent`：链接到父文件夹。
* `thumbnail`：（可选）链接到文件夹缩略图图像。

### 资源 {#assets}

在Experience Manager中，资产包含以下元素：

* 资源的属性和元数据。
* 多个演绎版，例如原始演绎版（最初上传的资源）、缩略图以及各种其他演绎版。 其他演绎版可以是大小不同、视频编码不同的图像，或者从PDF或[!DNL Adobe InDesign]文件中提取的页面。
* 可选注释。

有关内容片段中元素的信息，请参阅[Experience Manager Assets HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md#content-fragments)。

在[!DNL Experience Manager]中，文件夹具有以下组件：

* 实体：资产的子项是其演绎版。
* 属性。
* 链接。

[!DNL Assets] HTTP API包含以下功能：

* [检索文件夹列表](#retrieve-a-folder-listing)。
* [创建文件夹](#create-a-folder)。
* [创建资产](#create-an-asset)。
* [更新资产二进制文件](#update-asset-binary)。
* [更新资源元数据](#update-asset-metadata)。
* [创建资源演绎版](#create-an-asset-rendition)。
* [更新资源演绎版](#update-an-asset-rendition)。
* [创建资产评论](#create-an-asset-comment)。
* [复制文件夹或资产](#copy-a-folder-or-asset)。
* [移动文件夹或资源](#move-a-folder-or-asset)。
* [删除文件夹、资源或演绎版](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>为了便于阅读，以下示例省略了完整的cURL表示法。 事实上，表示法与[Resty](https://github.com/micha/resty)相关联，后者是`cURL`的脚本包装器。

**前提条件**

* 访问`https://[aem_server]:[port]/system/console/configMgr`。
* 导航到&#x200B;**[!UICONTROL Adobe Granite CSRF筛选器]**。
* 确保属性&#x200B;**[!UICONTROL 筛选器方法]**&#x200B;包括： `POST`、`PUT`、`DELETE`。

## 检索文件夹列表 {#retrieve-a-folder-listing}

检索现有文件夹及其子实体（子文件夹或资产）的Siren表示形式。

**请求**： `GET /api/assets/myFolder.json`

**响应代码**：响应代码为：

* 200 — 确定 — 成功。
* 404 - NOT FOUND — 文件夹不存在或无法访问。
* 500 — 内部服务器错误 — 如果出现其他错误。

**响应**：返回的实体的类是资产或文件夹。 包含的实体的属性是每个实体的完整属性集的子集。 要获取实体的完整表示形式，客户端应检索链接指向的URL的内容，该URL具有`self`的`rel`。

## 创建文件夹 {#create-a-folder}

在给定路径创建新`sling`： `OrderedFolder`。 如果提供了`*`而不是节点名称，则servlet将使用该参数名称作为节点名称。 已接受，因为请求数据是新文件夹的Siren表示形式或一组名称 — 值对，编码为`application/www-form-urlencoded`或`multipart`/`form`- `data`，可用于直接从HTML表单创建文件夹。 此外，可以将文件夹的属性指定为URL查询参数。

如果提供的路径的父节点不存在，则API调用会失败，并返回`500`响应代码。 如果文件夹已存在，调用将返回响应代码`409`。

**参数**： `name`是文件夹名称。

**请求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**响应代码**：响应代码为：

* 201 — 已创建 — 成功创建时。
* 409 — 冲突 — 如果文件夹已存在。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 创建资产 {#create-an-asset}

将提供的文件放在提供的路径中，以在DAM存储库中创建资产。 如果提供`*`而不是节点名称，则servlet使用参数名称或文件名作为节点名称。

**参数**：参数为资源名称的`name`和文件引用的`file`。

**请求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**响应代码**：响应代码为：

* 201 - CREATED — 如果已成功创建资产。
* 409 — 冲突 — 如果资产已存在。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 更新资产二进制文件 {#update-asset-binary}

更新资源的二进制文件（名为原始的演绎版）。 如果进行了配置，更新会触发默认资产处理工作流执行。

**请求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**响应代码**：响应代码为：

* 200 — 确定 — 如果已成功更新资产。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 更新资源元数据 {#update-asset-metadata}

更新资源元数据属性。 如果更新`dc:`命名空间中的任何属性，则API会更新`jcr`命名空间中的相同属性。 该API不会同步两个命名空间下的属性。

**请求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**响应代码**：响应代码为：

* 200 — 确定 — 如果已成功更新资产。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

### `dc`和`jcr`命名空间之间的同步元数据更新 {#sync-metadata-between-namespaces}

API方法更新`jcr`命名空间中的元数据属性。 使用用户界面进行的更新会更改`dc`命名空间中的元数据属性。 要同步`dc`和`jcr`命名空间之间的元数据值，您可以创建工作流并配置Experience Manager以在编辑资产时执行工作流。 使用ECMA脚本同步所需的元数据属性。 以下示例脚本在`dc:title`和`jcr:title`之间同步标题字符串。

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## 创建资源演绎版 {#create-an-asset-rendition}

为资源创建资源演绎版。 如果未提供请求参数名称，则使用文件名作为演绎版名称。

**参数**：格式副本的名称为`name`，文件引用为`file`。

**请求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**响应代码**：响应代码为：

* 201 - CREATED — 如果已成功创建呈现版本。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 更新资源演绎版 {#update-an-asset-rendition}

更新分别使用新的二进制数据替换资产演绎版。

**请求**： `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**响应代码**：响应代码为：

* 200 - OK — 如果已成功更新演绎版。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 在资产上添加评论 {#create-an-asset-comment}

创建新的资产注释。

**参数**：评论的消息正文的参数为`message`，JSON格式的注释数据的参数为`annotationData`。

**请求**： `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**响应代码**：响应代码为：

* 201 - CREATED — 如果评论已成功创建。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 复制文件夹或资源 {#copy-a-folder-or-asset}

将提供的路径中可用的文件夹或资产复制到新目标。

**请求标头**：参数为：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity`或`0`。 使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite` — 使用`F`防止覆盖现有目标上的资产。

**请求**： `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**响应代码**：响应代码为：

* 201 - CREATED — 文件夹/资产是否已复制到不存在的目标。
* 204 — 无内容 — 如果将文件夹/资产复制到现有目标。
* 412 - PRECONDITION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 移动文件夹或资源 {#move-a-folder-or-asset}

将给定路径下的文件夹或资源移动到新目标。

**请求标头**：参数为：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity`或`0`。 使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite` — 使用`T`强制删除现有资源，或使用`F`阻止覆盖现有资源。

**请求**： `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

请勿在URL中使用`/content/dam`。 移动资源和覆盖现有资源的示例命令为：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**响应代码**：响应代码为：

* 201 - CREATED — 文件夹/资产是否已复制到不存在的目标。
* 204 — 无内容 — 如果将文件夹/资产复制到现有目标。
* 412 - PRECONDITION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 删除文件夹、资源或演绎版 {#delete-a-folder-asset-or-rendition}

在提供的路径中删除资源(-tree)。

**请求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**响应代码**：响应代码为：

* 200 - OK — 已成功删除文件夹。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 提示和限制 {#tips-best-practices-limitations}

* [HTTP API更新`jcr`命名空间中的元数据属性](#update-asset-metadata)。 但是，Experience Manager用户界面会更新`dc`命名空间中的元数据属性。

* Assets HTTP API不返回完整的元数据。 命名空间是硬编码的，并且只返回这些命名空间。 有关完整的元数据，请参阅资源路径`/jcr_content/metadata.json`。
