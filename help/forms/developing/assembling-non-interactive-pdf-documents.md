---
title: 汇编非交互式PDF文档
description: 使用非交互式PDF表单作为输入，使用Java API和Web服务API汇编非交互式PDF文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: fc5ea2a6-79b4-436e-b5bc-c4beaf3619ee
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# 汇编非交互式PDF文档 {#assembling-non-interactive-pdf-documents}

使用交互式PDF表单作为输入时，可以组合非交互式PDF文档。 即，假设您有一个表单，用户可以使用它向表单字段中输入数据。 您可以将该表单传递到Assembler服务，从而导致Assembler服务返回PDF文档，该文档阻止用户在其字段中输入数据。 本文档是非交互式PDF表单。 例如，下图显示了表示交互式表单的抵押应用程序。

为了进行此讨论，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文档中，请注意源属性被分配了值`inDoc`。 如果只有一个输入PDF文档传递到Assembler服务并返回了一个PDF文档，且您调用了`invokeOneDocument`操作，则将值`inDoc`分配给PDF源属性。 调用`invokeOneDocument`操作时，`inDoc`值是必须在DDX文档中指定的预定义键。

相反，在将两个或更多输入PDF文档传递到Assembler服务时，您可以调用`invokeDDX`操作。 在这种情况下，将输入PDF文档的文件名分配给`source`属性。

此DDX文档包含`NoXFA`元素，该元素指示Assembler服务返回非交互式PDF文档。

如果输入PDF文档基于Acrobat表单或静态XFA表单，则Assembler服务可以组合非交互式PDF文档，而无需将输出服务作为AEM表单安装的一部分。 但是，如果输入PDF文档是动态XFA表单，则输出服务必须是AEM表单安装的一部分。 在组装动态XFA表单时，如果Output服务不是AEM表单安装的一部分，则会引发异常。 请参阅[创建文档输出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务组合PDF文档。 本节不讨论相关概念，例如创建包含输入文档的收藏集对象，或者了解如何从返回的收藏集对象中提取结果。 (请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要汇编非交互式PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用交互式PDF文档。
1. 设置运行时选项。
1. 汇编PDF文档。
1. 保存非交互式PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为JAR文件，这些文件特定于部署AEM Forms的J2EE应用程序服务器。

**创建汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 此DDX文档必须包含`NoXFA`元素，该元素指示Assembler服务返回非交互式PDF文档。

**引用交互式PDF文档**

必须引用交互式PDF文档并将其传递给Assembler服务，才能取回非交互式PDF文档。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。

**汇编PDF文档**

创建Assembler服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用`invokeOneDocument`操作。 由于只有一个输入PDF文档被传递到Assembler服务并返回了一个文档，因此您可以使用`invokeOneDocument`操作，而不是`invokeDDX`操作。

**保存非交互式PDF文档**

如果只有一个PDF文档传递到Assembler服务，则Assembler服务返回单个文档，而不是集合对象。 也就是说，在调用`invokeOneDocument`操作时，将返回单个文档。 由于本节中引用的DDX文档包含有关创建非交互式PDF文档的说明，因此Assembler服务会返回一个非交互式PDF文档，该文档可以保存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API汇编非交互式PDF文档 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

使用Assembler服务API (Java)汇编非交互式PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`AssemblerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用其构造函数并传递指定DDX文件位置的字符串值，创建表示DDX文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 引用交互式PDF文档。

   * 使用对象的构造函数并传递交互式PDF文档的位置来创建一个`java.io.FileInputStream`对象。
   * 创建一个`com.adobe.idp.Document`对象并传递包含PDF文档的`java.io.FileInputStream`对象。 此`com.adobe.idp.Document`对象被传递到`invokeOneDocument`方法。

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。 请确保此DDX文档包含PDF源元素的值`inDoc`。
   * 包含交互式PDF文档的`com.adobe.idp.Document`对象。
   * 指定运行时选项（包括默认字体和作业日志级别）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象。

   `invokeOneDocument`方法返回包含非交互式PDF文档的`com.adobe.idp.Document`对象。

1. 保存非交互式PDF文档。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中。 确保使用`invokeOneDocument`方法返回的`Document`对象。

* “快速入门(SOAP模式)：使用Java API汇编非交互式PDF文档”

## 使用Web服务API汇编非交互式PDF文档 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

使用Assembler服务API（Web服务）汇编非交互式PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

   * 使用默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示DDX文档的文件位置以及用于打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 引用交互式PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示输入PDF文档的文件位置以及用于打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 表示交互式PDF文档的`BLOB`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeOneDocument`方法返回包含非交互式PDF文档的`BLOB`对象。

1. 保存非交互式PDF文档。

   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示非交互式PDF文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储`invokeOneDocument`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

* “快速入门(MTOM)：使用Web服务API汇编非交互式PDF文档”。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
