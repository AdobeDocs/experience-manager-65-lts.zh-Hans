---
title: 使用SubmittedXML数据创建PDF文档
description: 使用Forms服务检索用户在交互式表单中输入的表单数据。 将表单数据传递到另一个AEM Forms服务操作，然后使用该数据创建PDF文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 66736a58-b2ef-404e-b94c-9bc407828359
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# 使用提交的XML数据创建PDF文档 {#creating-pdf-documents-with-submittedxml-data}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 使用提交的XML数据创建PDF文档 {#creating-pdf-documents-with-submitted-xml-data}

使用户能够填写交互式表单的基于Web的应用程序要求将数据提交回服务器。 使用Forms服务，您可以检索用户输入到交互式表单中的表单数据。 然后，您可以将表单数据传递到另一个AEM Forms服务操作，并使用这些数据创建PDF文档。

>[!NOTE]
>
>在阅读本内容之前，建议您充分了解如何处理已提交的表单。 处理提交的Forms中介绍了一些概念，例如表单设计和提交的XML数据之间的关系。

请考虑以下涉及三个AEM Forms服务的工作流：

* 用户从基于Web的应用程序将XML数据提交到Forms服务。
* Forms服务用于处理提交的表单并提取表单字段。 可以处理表单数据。 例如，可以将数据提交到企业数据库。
* 表单数据会发送到输出服务以创建非交互式PDF文档。
* 非交互式PDF文档存储在内容服务中（已弃用）。

下图提供了此工作流的可视表示形式。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

用户从客户端Web浏览器提交表单后，非交互式PDF文档存储在内容服务中（已弃用）。 下图显示了一个存储在Content Services中的PDF文档（已弃用）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步骤摘要 {#summary-of-steps}

要创建包含提交的XML数据的非交互式PDF文档，并将其存储在内容服务（已弃用）的PDF文档中，请执行以下任务：

1. 包括项目文件。
1. 创建Forms、输出和文档管理对象。
1. 使用Forms服务检索表单数据。
1. 使用输出服务创建非交互式PDF文档。
1. 使用文档管理服务将PDF表单存储在内容服务中（已弃用）。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms、输出和文档管理对象**

在以编程方式执行Forms服务API操作之前，请先创建Forms客户端API对象。 同样，由于此工作流调用输出和文档管理服务，因此请创建输出客户端API对象和文档管理客户端API对象。

**使用Forms服务检索表单数据**

检索提交到Forms服务的表单数据。 您可以处理提交的数据以满足您的业务要求。 例如，可以将表单数据存储到企业数据库中。 但是，要创建非交互式PDF文档，表单数据将传递到Output服务。

**使用输出服务创建非交互式PDF文档。**

使用Output服务创建基于表单设计和XML表单数据的非交互式PDF文档。 在工作流中，将从Forms服务中检索表单数据。

**使用文档管理服务将PDF表单存储在Content Services中（已弃用）**

使用文档管理服务API在内容服务中存储PDF文档（已弃用）。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API创建包含提交的XML数据的PDF文档 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、输出和文档管理API (Java)创建包含提交的XML数据的PDF文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 创建Forms、输出和文档管理对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。
   * 使用构造函数创建`OutputClient`对象并传递`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentManagementServiceClientImpl`对象并传递`ServiceClientFactory`对象。

1. 使用Forms服务检索表单数据

   * 调用`FormsServiceClient`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`com.adobe.idp.Document`对象。
      * 一个字符串值，它指定环境变量，包括所有相关的HTTP标头。 通过为`CONTENT_TYPE`环境变量指定一个或多个值来指定要处理的内容类型。 例如，要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`。
      * 指定`HTTP_USER_AGENT`标头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存储运行时选项的`RenderOptionsSpec`对象。

     `processFormSubmission`方法返回包含表单提交结果的`FormsResult`对象。

   * 确定Forms服务是否通过调用`FormsResult`对象的`getAction`方法已完成表单数据的处理。 如果此方法返回值`0`，则数据已准备好进行处理。
   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象以检索表单数据。 （此对象包含可以发送到Output服务的表单数据。）
   * 通过调用`java.io.DataInputStream`构造函数并传递`com.adobe.idp.Document`对象来创建`java.io.InputStream`对象。
   * 通过调用静态`org.w3c.dom.DocumentBuilderFactory`对象的`newInstance`方法创建一个`org.w3c.dom.DocumentBuilderFactory`对象。
   * 通过调用`org.w3c.dom.DocumentBuilderFactory`对象的`newDocumentBuilder`方法创建`org.w3c.dom.DocumentBuilder`对象。
   * 通过调用`org.w3c.dom.DocumentBuilder`对象的`parse`方法并传递`java.io.InputStream`对象来创建`org.w3c.dom.Document`对象。
   * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建接受两个参数的自定义方法：`org.w3c.dom.Document`对象以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此过程之后的代码示例中，此自定义方法称为`getNodeText`。 给出了该方法的正文。

1. 使用输出服务创建非交互式PDF文档。

   通过调用`OutputClient`对象的`generatePDFOutput`方法并传递以下值来创建PDF文档：

   * `TransformationFormat`枚举值。 要生成PDF文档，请指定`TransformationFormat.PDF`。
   * 一个字符串值，它指定窗体设计的名称。 确保表单设计与从Forms服务检索到的表单数据兼容。
   * 一个字符串值，它指定表单设计所在的内容根。
   * 包含PDF运行时选项的`PDFOutputOptionsSpec`对象。
   * 包含渲染运行时选项的`RenderOptionsSpec`对象。
   * 包含要与表单设计合并的数据的XML数据源的`com.adobe.idp.Document`对象。 确保`FormsResult`对象的`getOutputContent`方法返回了此对象。
   * `generatePDFOutput`方法返回包含该操作结果的`OutputResult`对象。
   * 通过调用`OutputResult`对象的`getGeneratedDoc`方法检索非交互式PDF文档。 此方法返回表示非交互式PDF文档的`com.adobe.idp.Document`实例。

1. 使用文档管理服务将PDF表单存储在内容服务中（已弃用）

   通过调用`DocumentManagementServiceClientImpl`对象的`storeContent`方法并传递以下值来添加内容：

   * 一个字符串值，它指定添加内容的存储。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定添加内容的空间的完全限定路径（例如，`/Company Home/Test Directory`）。 此值是必需参数。
   * 表示新内容的节点名称（例如，`MortgageForm.pdf`）。 此值是必需参数。
   * 指定节点类型的字符串值。 要添加新内容，如PDF文件，请指定`{https://www.alfresco.org/model/content/1.0}content`。 此值是必需参数。
   * 表示内容的`com.adobe.idp.Document`对象。 此值是必需参数。
   * 指定编码值的字符串值（例如，`UTF-8`）。 此值是必需参数。
   * `UpdateVersionType`枚举值，指定如何处理版本信息（例如，`UpdateVersionType.INCREMENT_MAJOR_VERSION`以递增内容版本）。 )此值是必需参数。
   * 指定与内容相关方面的`java.util.List`实例。 此值是可选参数，您可以指定`null`。
   * 存储内容属性的`java.util.Map`对象。

   `storeContent`方法返回描述内容的`CRCResult`对象。 使用`CRCResult`对象，您可以获取内容的唯一标识符值等。 要执行此任务，请调用`CRCResult`对象的`getNodeUuid`方法。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
