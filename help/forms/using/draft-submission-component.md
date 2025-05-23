---
title: 草稿和提交组件
description: 草稿和提交组件列出了处于草稿状态并已提交的表单。 您可以自定义组件的外观和样式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: 3d4ff4d1-aab6-47b9-9804-2a0f3438332d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 草稿和提交组件{#drafts-and-submissions-component}

草稿和提交组件列出了处于草稿状态的所有表单以及已提交的表单。 该组件具有用于草稿和已提交表单的单独部分（选项卡）。 用户只能查看其草稿和提交的表单。

## 配置组件 {#configuring-the-component}

草稿和提交组件包含两个选项卡：草稿和提交。

要使自适应表单的提交显示在提交选项卡中，请将&#x200B;**提交操作**&#x200B;设置为&#x200B;**[Forms Portal提交操作](../../forms/using/configuring-submit-actions.md)。 或者，**&#x200B;启用Forms Portal提交选项。 每当用户提交表单时，该表单即被添加到提交选项卡。

现成启用草稿功能。 当用户单击自适应表单上的&#x200B;**保存**&#x200B;时，该表单被添加到草稿选项卡。

执行以下步骤以添加和配置草稿和提交组件：

1. 将组件浏览器中Document Services类别下的&#x200B;**草稿和提交**&#x200B;组件拖放到您的页面。
1. 选择该组件，然后选择![settings_icon](assets/settings_icon.png)以打开该组件的“编辑”对话框。

   ![草稿和提交组件](assets/drafts-submissions-edit.png)

1. 在“编辑”对话框中，指定以下详细信息并选择&#x200B;**完成**&#x200B;以保存设置。

<table>
 <tbody>
  <tr>
   <th>选项卡</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>常规</td>
   <td>总结果</td>
   <td>指定要显示的最大结果数。 如果结果计数增加了“总结果”限制，则组件底部将显示<strong>更多</strong>链接。 单击<strong>更多</strong>显示所有表单。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>样式类型</td>
   <td>指定组件的样式。 您可以为列出表单指定<strong>无样式</strong>、<strong>默认样式</strong>或<strong>自定义样式</strong>。 对于自定义样式选项，您可以在<strong>自定义样式路径</strong>字段<strong>中指定自定义CSS文件的路径。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自定义样式路径</td>
   <td>如果在<strong>样式类型</strong>字段中选择<strong>自定义样式</strong>选项，请使用<strong>自定义样式路径</strong>字段指定自定义CSS文件的路径。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>显示选项</td>
   <td><p>指定要显示的选项卡。 您可以选择显示草稿表单、已提交的表单或同时显示两者。 </p> <p><strong>注意</strong>：<em>对于<strong>显示选项</strong>，如果您选择的选项不是<strong>Both</strong>，则不使用<strong>默认选项卡</strong>字段选项。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>默认选项卡</td>
   <td>指定在加载表单门户页面时显示的选项卡。 您可以选择<strong>草稿Forms选项卡</strong>和<strong>提交的Forms选项卡</strong>。</td>
  </tr>
  <tr>
   <td>草稿Forms选项卡配置</td>
   <td>自定义标题</td>
   <td>指定<strong>草稿Forms</strong>选项卡的标题。 默认值为<strong>草稿Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于草稿Forms列表的布局。</td>
  </tr>
  <tr>
   <td>已提交Forms选项卡配置</td>
   <td>自定义标题 </td>
   <td>指定<strong>已提交的Forms </strong>选项卡的标题。 默认值为<strong>提交的Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于已提交的Forms<strong> </strong>列表的布局。 </td>
  </tr>
 </tbody>
</table>

## 自定义存储 {#customizing-the-storage}

当您使用Forms Portal提交操作或启用自适应表单中的在表单门户中存储数据选项时，表单数据存储在AEM存储库中。 在生产环境中，建议不要将草稿或提交的表单数据存储在AEM存储库中。 相反，您必须将草稿和提交组件与企业数据库等安全存储集成以存储草稿和提交的表单数据。

通过Forms portal，您可以将数据存储在本地AEM存储库、远程AEM存储库中，或存储到数据库中。 AEM Forms允许您自定义存储草稿和提交的用户数据的实施。 您可以覆盖默认方法，以指定如何将草稿和提交数据存储到您选择的存储中。 例如，您可以将数据存储在组织中当前实施的数据存储中。

Forms portal提供开箱即用的服务(API)，用于在本地和远程AEM Forms发布实例的crx存储库上存储数据。 您可以使用自定义实施替换默认功能，如[为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md)文章中所述。 有关在自定义实施中将内容存储在安全位置所需方法的详细信息，请参阅[自定义草稿和提交数据服务](/help/forms/using/custom-draft-submission-data-services.md)和[草稿和提交组件的自定义存储](/help/forms/using/adding-custom-storage-provider-forms.md)。

AEM Forms文档提供了一个用于将草稿和提交组件与数据库[&#128279;](integrate-draft-submission-database.md)集成的示例。 您可以使用示例实施来开发自己的自定义实施。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出网页上的表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
