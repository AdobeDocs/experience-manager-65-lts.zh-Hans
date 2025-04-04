---
title: 按值呈现Forms
description: 使用Forms API (Java)通过Java API和Web服务API按值呈现表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 8ad8cf67-3e90-4790-a063-099134b377a3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# 按值呈现Forms {#rendering-forms-by-value}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

通常，在Designer中创建的表单设计会通过引用Forms服务进行传递。 窗体设计可以很大，因此，通过引用传递它们会更有效，从而不必按值封送窗体设计字节。 Forms服务还可以缓存表单设计，以便在缓存表单设计时，它不必持续读取表单设计。

如果表单设计包含UUID属性，则将其缓存。 UUID值对于所有表单设计都是唯一的，可用于唯一标识表单。 按值呈现表单时，仅当表单重复使用时才应缓存表单。 但是，如果表单未重复使用并且必须是唯一的，您可以避免使用使用AEM Forms API设置的缓存选项来缓存表单。

Forms服务还可以解决表单设计中链接内容的位置。 例如，从表单设计内引用的链接图像是相对URL。 始终假定链接的内容与表单设计位置相关。 因此，解决链接内容的问题是通过将相对路径应用于绝对表单设计位置来确定其位置。

您可以按值传递表单设计，而不是按参考传递表单设计。 在动态创建表单设计时，即客户端应用程序在运行时生成用于创建表单设计的XML时，按值传递表单设计是非常有效的。 在这种情况下，表单设计不会存储在物理存储库中，因为它存储在内存中。 在运行时动态创建表单设计并按值传递时，可以缓存表单并提高Forms服务的性能。

**按值传递表单的限制**

当表单设计按值传递时，以下限制适用：

* 表单设计中不能包含相对链接的内容。 所有图像和片段必须嵌入到表单设计内或绝对引用。
* 渲染表单后无法执行服务器端计算。 如果将表单提交回Forms服务，则会提取并返回数据，而无需任何服务器端计算。
* 由于HTML只能在运行时使用链接的图像，因此无法生成具有嵌入图像的HTML。 这是因为Forms服务通过从引用的表单设计检索图像来支持使用HTML嵌入图像。 由于按值传递的表单设计没有引用位置，因此在显示HTML页面时无法提取嵌入的图像。 因此，图像引用必须是绝对路径，才能在HTML中渲染。

>[!NOTE]
>
>虽然您可以按值呈现不同类型的表单(例如，包含使用权限的HTML表单或表单)，但本节将讨论如何呈现交互式PDF forms。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要按值呈现表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 参考窗体设计。
1. 按值呈现表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建数据集成服务客户端，然后才能以编程方式将数据导入PDF表单客户端API。 创建服务客户端时，您可以定义调用服务所需的连接设置。

**参考表单设计**

在按值呈现表单时，您必须创建包含要呈现的表单设计的`com.adobe.idp.Document`对象。 您可以引用现有的XDP文件，也可以在运行时动态创建表单设计，并用该数据填充`com.adobe.idp.Document`。

>[!NOTE]
>
>此部分和相应的快速入门引用了现有XDP文件。

**按值呈现表单**

要按值渲染表单，请将包含表单设计的`com.adobe.idp.Document`实例传递到渲染方法的`inDataDoc`参数（可以是`FormsServiceClient`对象的任何渲染方法，如`renderPDFForm`、`(Deprecated) renderHTMLForm`等）。 此参数值通常为合并到表单的数据保留。 同样，将空字符串值传递给`formQuery`参数。 通常，此参数需要一个指定窗体设计名称的字符串值。

>[!NOTE]
>
>如果要在表单中显示数据，则必须在`xfa:datasets`元素中指定该数据。 有关XFA架构的信息，请转到[https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)。

**将表单数据流写入客户端Web浏览器**

当Forms服务按值呈现表单时，它会返回您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，该表单对用户可见。

**另请参阅**

[使用Java API按值呈现表单](#render-a-form-by-value-using-the-java-api)

[使用Web服务API按值呈现表单](#render-a-form-by-value-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API按值呈现表单 {#render-a-form-by-value-using-the-java-api}

使用Forms API (Java)按值呈现表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。

1. 参考表单设计

   * 创建一个`java.io.FileInputStream`对象，该对象表示要呈现的表单设计，方法是使用其构造函数并传递一个指定XDP文件位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 按值呈现表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个用于指定表单设计名称的字符串值。）
   * 包含表单设计的`com.adobe.idp.Document`对象。 通常，此参数值会保留给与表单合并的数据。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是一个可选参数，如果您不想指定运行时选项，则可以指定`null`。
   * 包含Forms服务所需URI值的`URLSpec`对象。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。

   `renderPDFForm`方法返回的`FormsResult`对象包含可以写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用其`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 创建字节数组并分配`InputStream`对象的大小。 调用`InputStream`对象的`available`方法以获取`InputStream`对象的大小。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，使用表单数据流填充字节数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[按值呈现Forms](/help/forms/developing/rendering-forms.md)

[快速入门(SOAP模式)：使用Java API按值渲染](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API按值呈现表单 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API（Web服务）按值呈现表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 参考表单设计

   * 使用构造函数创建`java.io.FileInputStream`对象。 传递一个指定XDP文件位置的字符串值。
   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已使用密码加密的PDF文档。
   * 创建用于存储`java.io.FileInputStream`对象的内容的字节数组。 您可以通过使用其`available`方法获取`java.io.FileInputStream`对象的大小来确定字节数组的大小。
   * 通过调用`java.io.FileInputStream`对象的`read`方法并传递字节数组，使用流数据填充字节数组。
   * 通过调用其`setBinaryData`方法并传递字节数组来填充`BLOB`对象。

1. 按值呈现表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个用于指定表单设计名称的字符串值。）
   * 包含表单设计的`BLOB`对象。 通常，此参数值会保留给与表单合并的数据。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是一个可选参数，如果您不想指定运行时选项，则可以指定`null`。
   * 包含Forms服务所需URI值的`URLSpec`对象。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。
   * 方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 用于存储渲染的PDF表单。
   * 方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数在表单中存储页数。）
   * 方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数存储区域设置值。）
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用其`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`BLOB`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[按值呈现Forms](#rendering-forms-by-value)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
