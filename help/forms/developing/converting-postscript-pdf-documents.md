---
title: 将Postscript转换为PDF文档
description: 使用Distiller服务将PostScript®、Encapsulated PostScript (EPS)和PRN文件通过网络转换为紧凑、可靠且更安全的PDF文件。 Distiller服务使用Java API和Web服务API将大量打印文档转换为电子文档，如发票和报表。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 39d793ca-5909-428e-9f6e-08d587f828c0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# 将Postscript转换为PDF文档 {#converting-postscript-to-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 关于Distiller服务 {#about-the-distiller-service}

Distiller®服务通过网络将PostScript®、封装的PostScript (EPS)和PRN文件转换为紧凑、可靠且更安全的PDF文件。 Distiller服务通常用于将大量打印文档转换为电子文档，如发票和报表。 将文档转换为PDF还允许企业向客户发送文档的纸质版本和电子版本。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PostScript文档转换为PDF文档 {#converting-postscript-to-pdf-documents-inner}

本主题介绍如何使用Distiller服务API（Java和Web服务）以编程方式将PostScript (PS)、封装的PostScript (EPS)和PRN文件转换为PDF文档。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>要将PostScript文件转换为PDF文档，需要在托管AEM Forms的服务器上安装以下项之一： Acrobat 9或Microsoft Visual C++ 2005可再发行软件包。

### 步骤摘要 {#summary-of-steps}

要将任何受支持的类型转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Distiller服务客户端。
1. 检索要转换的文件。
1. 调用PDF创建操作。
1. 保存PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Distiller服务客户端**

您必须先创建Distiller服务客户端，然后才能以编程方式执行Distiller服务操作。 如果您使用的是Java API，请创建一个`DistillerServiceClient`对象。 如果您使用的是Web服务API，请创建一个`DistillerServiceService`对象。

**检索要转换的文件**

检索要转换的文件。 例如，要将PS文件转换为PDF文档，您必须检索PS文件。

**调用PDF创建操作**

创建服务客户端后，您可以调用PDF创建操作。 此操作将需要有关要转换的文档的信息，包括目标文档的路径。

**保存PDF文档**

您可以将PDF文档另存为PDF文件。

**另请参阅**

[使用Java API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服务API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API将PostScript文件转换为PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用PostScript服务API (Java)将Distiller文件转换为PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-distiller-client.jar。

1. 创建Distiller服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`DistillerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 检索要转换的文件。

   * 创建一个`java.io.FileInputStream`对象，该对象表示要使用其构造函数转换的文件，并传递一个指定文件位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 调用PDF创建操作。

   调用`DistillerServiceClient`对象的`createPDF`方法并传递以下值：

   * 表示要转换的PS、EPS或PRN文件的`com.adobe.idp.Document`对象
   * 包含要转换的文件名称的`java.lang.String`对象
   * 包含要使用的Adobe PDF设置名称的`java.lang.String`对象
   * 包含要使用的安全设置的名称的`java.lang.String`对象
   * 包含要在生成PDF文档时应用的设置的可选`com.adobe.idp.Document`对象
   * 包含要应用于PDF文档的元数据信息的可选`com.adobe.idp.Document`对象

   `createPDF`方法返回包含新PDF文档的`CreatePDFResult`对象以及可能生成的日志文件。 日志文件通常包含转换请求生成的错误或警告消息。

1. 保存PDF文档。

   要获取新创建的PDF文档，请执行以下步骤：

   * 调用`CreatePDFResult`对象的`getCreatedDocument`方法。 这将返回`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法来提取PDF文档。

   同样，要获取日志文档，请执行下列操作。

   * 调用`CreatePDFResult`对象的`getLogDocument`方法。 这将返回`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法来提取日志文档。

**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API将PostScript文件转换为PDF文档](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PostScript文件转换为PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用PostScript服务API（Web服务）将Distiller文件转换为PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Distiller服务客户端。

   * 使用默认构造函数创建`DistillerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DistillerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`DistillerServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的文件。

   * 使用构造函数创建`BLOB`对象。 此`BLOB`对象用于存储要转换为PDF文档的文件。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示文件位置以及用于打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 调用PDF创建操作。

   调用`DistillerServiceService`对象的`CreatePDF2`方法并传递以下必需值：

   * 表示要转换的PS文件的`BLOB`对象
   * 一个字符串，其中包含要转换的文件的路径名称
   * 包含要使用的Adobe PDF设置的字符串对象（例如，`Standard`）
   * 包含要使用的安全设置的字符串对象（例如，`No Securit`y）
   * 包含要在生成PDF文档时应用的设置的可选`BLOB`对象
   * 包含要应用于PDF文档的元数据信息的可选`BLOB`对象
   * 用于存储PDF文档的`BLOB`输出参数
   * 用于存储日志的`BLOB`输出参数

1. 保存PDF文档。

   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`CreatePDF2`方法（输出参数）返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
