---
title: 管理表单元数据
description: 元数据允许更轻松地分类和组织资源，并帮助正在查找特定资源的用户。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 712590c6-2348-4c0d-93b9-686e6478ca03
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 2%

---

# 管理表单元数据{#manage-form-metadata}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/manage-form-metadata.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

## 概述  {#overview-nbsp}

元数据允许更轻松地分类和组织资源，并帮助正在查找特定资源的用户。

默认情况下，AEM Forms会为每个资源类型提供一组定义的元数据。 除了默认元数据之外，您还可以将自定义元数据添加到每个资源类型。 AEM Forms还为您提供了合适的方法，来为您的表单高效地创建、管理和交换所有这些元数据。

如果您是开发人员或站点所有者，则可以自定义AEM Forms的最终用户界面Forms Portal，以反映您在组织中使用的元数据。 有关Forms门户的更多信息，请参阅[在门户上发布表单简介](../../forms/using/introduction-publishing-forms.md)。

## AEM Forms中的元数据 {#metadata-in-aem-forms}

在AEM Forms中，与资源关联的元数据属性的列表取决于其类型。 此外，如果添加任何自定义元数据属性，则会将该属性添加到添加了自定义元数据的类型的所有资产中。

### 资源类型 {#asset-types}

AEM Forms支持以下资源类型：

* 表单模板（XFA表单）
* PDF forms
* 文档（平面PDF）
* 自适应表单
* 资源
* XFS

#### 广泛的元数据列表 {#extensive-list-of-metadata}

以下是AEM Forms中支持的元数据属性的广泛列表：

<table>
 <tbody> 
  <tr> 
   <td><strong>属性名称</strong></td> 
   <td><strong>资源类型</strong></td> 
   <td><strong>描述</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>标题</td> 
   <td>除资源以外的所有其他资源</td> 
   <td>表单的显示名称。<br /> </td> 
  </tr> 
  <tr> 
   <td>描述</td> 
   <td>除资源以外的所有其他资源</td> 
   <td>表单描述。 用户可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>类型</td> 
   <td>所有</td> 
   <td><p>指定资源类型的只读值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表单模板</li> 
     <li>PDF form、PDF form (Acroform)或PDF form （签名）</li> 
     <li>文档，文档（已签署）</li> 
     <li>自适应表单</li> 
     <li>资源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>已创建</td> 
   <td>所有</td> 
   <td>指定资源创建时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>所有</td> 
   <td>一个只读值，它指定上次修改资源的时间。</td> 
  </tr> 
  <tr> 
   <td>创作</td> 
   <td>除资源以外的所有其他资源</td> 
   <td><p>根据表单类型自动计算的只读值。</p> 
    <ul> 
     <li>PDF/Form template/Document — 从上传的二进制文件获取。</li> 
     <li>自适应表单 — 创建表单时登录用户。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>状态</td> 
   <td>除资源以外的所有其他资源</td> 
   <td><p> 只读值，定义表单的以下状态之一：</p> 
    <ul> 
     <li>无值：表示从未发布过表单。</li> 
     <li>已发布：发布表单时。</li> 
     <li>修改时间：表单发布一次后进行修改的时间。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次发布日期</td> 
   <td>除资源以外的所有其他资源</td> 
   <td>一个只读值，指定上次发布表单的时间。</td> 
  </tr> 
  <tr> 
   <td>发布开启/结束时间</td> 
   <td>除资源以外的所有其他资源</td> 
   <td><p>计划自动发布/取消发布表单的时间。 用户在编辑元数据时设置此值。</p> 
    <ul> 
     <li>发布开始时间和发布结束时间均应在当前日期之后。 </li> 
     <li>发布关闭时间应在发布开启时间之后。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表单模板</p> <p>PDF表单</p> </td> 
   <td><p>配置用户指定的URL以将表单数据提交到servlet。</p> <p>可以使用以下任一方法配置提交URL，并按优先级顺序列出：</p> 
    <ul> 
     <li>在AEM Forms Designer中创建XFA表单时，使用HTTP提交按钮直接在表单模板中指定提交URL。</li> 
     <li>在AEM Forms UI中，选择表单并在编辑元数据属性时指定提交URL。</li> 
     <li>在Forms Portal中，编辑Search &amp; Lister组件，然后在“表单链接”选项卡下指定提交URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML渲染配置文件</td> 
   <td>表单模板</td> 
   <td>以HTML格式呈现表单模板时使用的HTML呈现配置文件。</td> 
  </tr> 
  <tr> 
   <td>渲染格式</td> 
   <td><p>表单模板</p> <p>自适应表单</p> </td> 
   <td><p>此选项允许用户指定发布表单时的表单渲染格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li> 双向</li> 
    </ul> <p>此选项用于限制表单仅在Forms Portal上对最终用户可见。</p> </td> 
  </tr> 
  <tr> 
   <td>标记</td> 
   <td>除资源以外的所有其他资源</td> 
   <td>与表单关联的标签有助于快速轻松搜索。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>自适应表单</p> <p>表单模板</p> <p>资源</p> </td> 
   <td><p>与此表单相关的资产（其他表单或资源）列表。 这些资产可以分为以下两类：</p> 
    <ul> 
     <li>引用：当前表单引用的Assets。</li> 
     <li>引用者：引用当前资源的Assets。</li> 
    </ul> <p>这些资源显示为链接，通过单击这些链接可以直接访问其元数据。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表单模型(XDP/XSD)选择</td> 
   <td>自适应表单</td> 
   <td><p>指定创作自适应表单时使用的表单模型。 此属性可以具有以下值：</p> 
    <ul> 
     <li>表单模板：从存储库中的现有表单模板中选择表单模板。 此值可更新。</li> 
     <li>XML架构：已上传XSD文件。 此值可更新。</li> 
     <li>无</li> 
    </ul> 
    <div>
      表单模型一旦选定便可以更新，但不能删除。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 查看表单元数据 {#view-form-metadata}

Assets具有现有的属性值，可以在只读模式下查看这些值。 此元数据源自表单上传或表单创建时。

1. 导航到要查看元数据的资源的位置。

1. 使用以下方式之一打开属性页面：

   1. 单击“快速操作”中的查看属性![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)图标。

      >[!NOTE]
      >
      >快速操作是在鼠标悬停时显示在缩略图上的操作项。

   1. 选择表单，然后单击工具栏中显示的查看属性![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)图标。
   1. 在不处于选择模式时，通过单击表单缩略图导航到表单详细信息页面。 现在，单击右上角的![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)眼睛图标，然后单击其下方列表中的“属性”。

1. 打开的属性页显示的方案仅包含那些保存某些值的元数据属性。

   属性页面有一个包含两个操作图标的工具栏：

   * 编辑： ![aem6forms_edit](assets/aem6forms_edit.png)编辑元数据属性值
   * 视图： ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)导航到表单详细信息页面，该页面将在预览模式下打开表单。

   内容部分分为两部分：

   * 左侧面板包含表单的缩略图
   * 右侧面板包含以只读模式分布的元数据属性，这些属性分布在不同的选项卡中。

## 添加/更新表单元数据值 {#add-update-form-metadata-values}

您可以编辑现有元数据属性的值或向现有元数据属性字段添加新值（例如，当元数据字段为空时）。

### 更新元数据属性值 {#update-metadata-property-values}

1. 按照上一节中提到的步骤打开属性页面，可以在其中查看所选表单的现有元数据。

1. 在工具栏中，单击编辑图标![aem6forms_edit](assets/aem6forms_edit.png)以将页面的模式从只读更改为读/写。

1. 打开的属性页面包含一个混合了可编辑输入字段和静态文本的架构。

1. 静态文本中显示的属性是无法编辑的属性。

1. 您可以导航到其他选项卡，以查找位于这些选项卡下方的元数据属性的输入字段。

   此页面有一个工具栏，其中包含两个与视图模式不同的操作图标：

   * 取消： ![aem6forms_close](assets/aem6forms_close.svg_w24.png)取消迄今为止对元数据属性值所做的任何更改
   * 完成： ![aem6forms_check](assets/aem6forms_check.png)保存迄今为止对元数据属性值所做的所有更改

   这两个操作都会将用户引导回包含更新值的属性页的只读模式。

### 更新表单缩略图 {#update-the-form-thumbnail}

属性页面中的左侧面板显示表单的缩略图。 默认情况下，显示的缩略图是创建表单（自适应表单）时或上传表单时生成的缩略图。

对于所有表单类型，您可以选择通过单击&#x200B;**[!UICONTROL 上传图像]**&#x200B;并从本地目录浏览图像文件来上传图像。 所选图像将用作缩略图，而不是默认图像。

对于自适应表单，还提供了附加功能，允许用户生成缩略图作为当前自适应表单预览的快照。 由于AEM Forms还支持创作自适应表单，因此每次更改自适应表单时，自适应表单的预览都可能会发生更改。 此功能可生成缩略图，从而帮助您根据当前预览状态为自适应表单获取新的缩略图。 单击&#x200B;**[!UICONTROL 生成预览]**&#x200B;以执行此操作。

>[!NOTE]
>
>* 在缩略图中使用正方形图像。 当您使用非正方形图像并在列表视图中查看缩略图时，缩略图显示为已裁剪。
>* 上传或生成新图像后，缩略图将替换为此图像，并且无法重置为上一个图像。
>

## 添加自定义元数据 {#add-custom-metadata}

除了开箱即用的元数据之外，AEM Forms还支持新的自定义元数据。

提供了一个工具（元数据架构编辑器）来定义元数据布局的架构；即表单的&#x200B;**[!UICONTROL 属性]**&#x200B;页面中显示的布局。 通过元数据架构编辑器，可为资源添加或修改自定义架构。

AEM Forms在此工具中公开受支持表单类型的元数据架构。 通过这种方式，您可以访问这些架构，并使用元数据架构编辑器中提供的功能来添加自定义属性。

### 导航到元数据架构编辑器 {#navigate-the-metadata-schema-editor}

1. 导航到&#x200B;**[!UICONTROL 工具> Assets >元数据架构]**。

1. 从列出的架构表单中单击&#x200B;**[!UICONTROL 表单]**。

1. 在打开的列表中，单击要为其添加自定义元数据的资源类型。

   >[!NOTE]
   >
   >这些架构包含现成提供的元数据属性，不得更改/编辑（选中复选框并单击工具栏中的编辑）以避免功能问题。

1. 单击的任何资产类型都会打开一个包含`extendedmetadata`选项的列表。 编辑此架构。

1. 选中`extendedmetadata`旁边的复选框，然后单击工具栏中显示的编辑![aem6forms_edit](assets/aem6forms_edit.png)图标。

1. AEM Forms会打开所选资源类型的元数据架构编辑器/表单生成器（在本例中为“自适应表单”）。

   自适应表单类型的![元数据架构编辑器](assets/metadata-schema-editor-for-adaptive-form-type.png)

   元数据编辑器

   1. 左侧面板包含放置字段的选项卡部分，右侧面板显示所有可用的UI组件以及从左侧面板中选择的字段的属性。

   1. 锁定的部分不可编辑，并包含开箱即用提供的所有元数据属性的字段。

   1. 单击+符号可添加其他选项卡。

   1. 您可以添加所需类型的自定义字段，方法是将&#x200B;**[!UICONTROL 构建表单]**&#x200B;分区中的字段组件拖到架构页面上。
   1. 单击该字段后，可在&#x200B;**[!UICONTROL 设置]**&#x200B;部分下提供该字段的规范。

### 在架构编辑器中添加自定义元数据属性 {#add-custom-metadata-property-in-schema-editor}

1. 导航到要添加自定义属性的选项卡（现有或新）。

1. 将所需类型的组件从&#x200B;**[!UICONTROL 构建表单]**&#x200B;区域拖到左侧面板并放置在方便的位置。

   >[!NOTE]
   >
   >不能移动锁定的部分，但可以将组件放在任何空格中。

1. 单击刚刚拖动的组件。 在右侧面板中打开的设置选项卡中，填写以下字段的信息：

   1. 指定字段标签，该标签用作位于架构中的字段上方的显示名称（例如：Department）
   1. 在映射到属性字段下，您可以看到预填充的值&#x200B;**。/jcr：content/metadata/default“**”。 将“**default**”更改为所需的属性名称，该属性名称用于存储crx存储库中的属性(例如：“”。/jcr：content/metadata/department&#39;)

      >[!NOTE]
      >
      >请勿更改前缀&#39;。/jcr：content/metadata/&#39; ，它定义存储属性的路径。
      >
      >此外，属性名称必须是唯一的，以避免在存储库中的同一位置写入两个或更多属性的值。 因此，建议您更改“default”值。

   1. 根据需要填写其他设置。 例如：如果要使字段成为必填字段，请选择必填选项。
   1. 要删除您添加的字段，请选择该字段，然后单击删除![delete-1](assets/delete-1.png)图标。

1. 如有必要，请按照步骤1 - 3添加其他资产。
1. 完成所有更改后，单击&#x200B;**完成**。

   您已成功添加自定义元数据属性。

AEM Forms中的所有自适应表单现在都包含此额外的元数据属性。 您可以从属性页面对其进行编辑。
