---
title: 内容架构
description: 关于内容架构的提示（提示 — 一切都是内容）
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: eb47f730-ac26-47a0-9bd7-3b7e94c79ecd
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 内容架构{#content-architecture}

## 遵循David的模型 {#follow-david-s-model}

大卫·纽舍勒在多年前写了《大卫模型》，但其思想在今天仍然成立。 David模型的主要原则如下：

* 先有数据，后有结构。 也许吧。
* 推动内容层次结构；不要让这种情况发生。
* 工作区用于`clone()`、`merge()`和`update()`。
* 注意同名同胞。
* 引用内容可视为有害。
* 文件就是文件。
* 身份识别是邪恶的。

David模型可在Jackrabbit维基百科上找到，网址为[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 一切都是内容 {#everything-is-content}

所有内容都应存储在存储库中，而不是依赖单独的第三方数据源，例如数据库。 这种方法适用于创作内容、二进制数据（如图像、代码和配置）。 它允许我们使用一组API来管理所有内容并通过复制管理此内容的提升。 您还可以获得备份、日志记录等的单一来源。

### 使用“内容模型优先”设计原则 {#use-the-content-model-first-design-principle}

构建新功能时，始终首先设计JCR内容结构，然后考虑使用默认Sling Servlet阅读和编写内容。 通过这种方法，您可以确保实施与开箱即用的访问控制机制很好地配合使用，并避免生成不必要的CRUD样式的Servlet。

### 是RESTful {#be-restful}

根据resourceTypes而不是路径定义servlet。 这种方法使我们能够使用JCR访问控制，遵守REST原则，并使用在请求中提供给我们的资源和资源解析器。 此方法允许您更改在服务器端渲染URL的脚本，而无需更改任何客户端URL。 它还隐藏客户端的服务器端实施详细信息，以提高安全性。

### 避免定义新节点类型 {#avoid-defining-new-node-types}

节点类型在基础架构层的较低级别工作。 使用分配给`sling:resourceType`、`nt:unstructured`、`oak:Unstructured`或`sling:Folder`节点类型的`cq:Page`满足大多数要求。 节点类型等同于存储库中的架构，并且将来更改节点类型可能会很昂贵。

### 遵守JCR中的命名约定 {#adhere-to-naming-conventions-in-the-jcr}

遵守命名惯例可为代码库增加一致性，从而降低缺陷的发生率，并提高开发人员在系统中工作的速度。 Adobe在开发AEM时使用了以下约定：

* 节点名称

   * 全部为小写。
   * 使用连字符进行分词。

* 属性名称

   * 驼峰式大小写，以小写字母开头。

* 组件(JSP/HTML)

   * 全部为小写。
   * 使用连字符进行分词。
