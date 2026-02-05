---
title: 创建通信解决方案与您的自定义门户集成
description: 了解如何将创建通信UI与您的自定义门户集成
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
source-git-commit: 16f57ae1663f035d1dc39005d37426c7a0d8dc16
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 4%

---

# 将`Create Correspondence`解决方案与您的自定义门户集成{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概述 {#overview}

本文详细介绍如何将`Create Correspondence`解决方案与您的环境集成。

## 基于URL的调用 {#url-based-invocation}

从自定义门户调用`Create Correspondence`应用程序的一种方法是使用以下请求参数准备URL：

* 书信模板的标识符（使用cmLetterId参数）。

* 从所需数据源获取的XML数据的URL（使用cmDataUrl参数）。

例如，自定义门户会将URL准备为\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，这可能是来自门户上链接的href。

>[!NOTE]
>
>以这种方式调用并不安全，因为必需的参数是作为GET请求传递的，方法是在URL中公开相同的（可见）。

>[!NOTE]
>
>在调用`Create Correspondence`应用程序之前，保存并上传数据以在给定dataURL调用`Create Correspondence` UI。 此流程可以从自定义门户本身完成，也可以通过其他后端流程完成。

## 基于数据的内联调用 {#inline-data-based-invocation}

调用`Create Correspondence`应用程序的另一种更安全的方法是转到位于https://&#39;[server]：[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html的URL。 发送参数和数据时运行此URL以作为POST请求调用`Create Correspondence`应用程序，并对最终用户隐藏它们。 此工作流还意味着您现在可以传递`Create Correspondence`应用程序内联的XML数据（作为同一请求的一部分，使用`cmData`参数）。 此工作流在之前的方法中不可能或理想。

### 用于指定书信的参数 {#parameters-for-specifying-letter}

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| cmLetterInstanceId | 字符串 | 书信实例的标识符。 |
| cmLetterId | 字符串 | 书信模板的名称。 |

表中的参数顺序指定用于加载信件的参数的首选项。

### 用于指定XML数据源的参数 {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>使用基本协议（如cq、ftp、http或file）的源文件中的XML数据。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字符串</td> 
   <td>使用信件实例中可用的xml数据。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布尔值</td> 
   <td>重用数据字典中附加的测试数据。</td> 
  </tr>
 </tbody>
</table>

表中的参数顺序指定用于加载XML数据的参数的首选项。

### 其他参数 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布尔值</td> 
   <td>若为True，则以预览模式打开书信<br /> </td> 
  </tr>
  <tr>
   <td>随机</td> 
   <td>时间戳</td> 
   <td>解决浏览器缓存问题。</td> 
  </tr>
 </tbody>
</table>

如果您对`cmDataURL`使用http或cq协议，则`http/cq`的URL必须可匿名访问。
