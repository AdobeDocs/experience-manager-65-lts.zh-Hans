---
title: 导入和导出数据
description: 使用表单数据集成服务将数据导入PDF表单，并使用Java API和Web服务API从PDF表单导出数据。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 2e8b73eb-7070-4b7b-b14b-bfcca6175afb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 0%

---

# 导入和导出数据 {#importing-and-exporting-data}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 关于表单数据集成服务 {#about-the-form-data-integration-service}

表单数据集成服务可以将数据导入PDF表单并从PDF表单导出数据。 导入和导出操作支持两种类型的PDF forms：

* Acrobat表单(在Acrobat中创建)是包含表单字段的PDF文档。
* Adobe XML表单(在Designer中创建)是符合XML Adobe XML Forms架构(XFA)的PDF文档。

根据PDF表单的类型，表单数据可以以下列格式之一存在：

* XFDF文件，它是Acrobat表单数据格式的XML版本。
* XDP文件，它是一个包含表单字段定义的XML文件。 它还可能包含表单字段数据和嵌入的PDF文件。 Designer生成的XDP文件只能在其携带嵌入的base-64编码的PDF文档时使用。

您可以使用表单数据集成服务完成这些任务：

* 将数据导入PDF forms。 有关信息，请参阅[导入表单数据](importing-exporting-data.md#importing-form-data)。
* 从PDF forms导出数据。 有关信息，请参阅[导出表单数据](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 导入表单数据 {#importing-form-data}

您可以使用表单数据集成服务将表单数据导入交互式PDF forms中。 交互式PDF表单是一种PDF文档，其中包含一个或多个用于从用户那里收集信息或用于显示自定义信息的字段。 表单数据集成服务不支持表单计算、验证或脚本。

要将数据导入到Designer中创建的表单，必须引用有效的XDP XML数据源。 考虑以下抵押贷款申请表示例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

要将数据值导入此表单，您必须拥有与表单对应的有效XDP XML数据源。 无法使用任意XML数据源通过“表单数据集成”服务将数据导入表单。 任意XML数据源和XDP XML数据源的区别在于XDP数据源符合XML Forms架构(XFA)。 以下XML表示与示例抵押应用程序表单相对应的XDP XML数据源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将表单数据导入PDF表单，请执行以下步骤：

1. 包括项目文件。
1. 创建表单数据集成服务客户端。
1. 引用PDF表单。
1. 引用XML数据源。
1. 将数据导入PDF表单。
1. 将PDF表单另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建表单数据集成服务客户端**

您必须先创建数据集成服务客户端，然后才能以编程方式将数据导入PDF表单客户端API。 创建服务客户端时，您可以定义调用服务所需的连接设置。 有关信息，请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF表单**

要将数据导入PDF表单，您必须引用在Designer中创建的XML表单或在Acrobat中创建的Acrobat表单。

**引用XML数据源**

要导入表单数据，必须引用有效的数据源。 要将数据导入到Designer中创建的XFA XML表单中，您必须使用XDP XML数据源。 如果引用Acrobat表单，则必须使用XFDF数据源。 对于要将数据导入到的每个字段，必须指定值。 如果XML数据源中的元素与表单中的字段不对应，则该元素将被忽略。

**将数据导入PDF表单**

在引用PDF表单和有效的XML数据源后，您可以将数据导入PDF表单。

**将PDF表单另存为PDF文件**

将数据导入表单后，可将表单另存为PDF文件。 保存为PDF文件后，用户可以在Adobe Reader或Acrobat中打开表单，并使用导入的数据查看表单。

**另请参阅**

[使用Java API导入表单数据](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用Web服务API导入表单数据](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表单数据集成服务API快速入门](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[导出表单数据](importing-exporting-data.md#exporting-form-data)

### 使用Java API导入表单数据 {#import-form-data-using-the-java-api}

使用表单数据集成API (Java)导入表单数据：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-formdataintegration-client.jar。

1. 创建表单数据集成服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`FormDataIntegrationClient`对象并传递`ServiceClientFactory`对象。

1. 引用PDF表单。

   * 使用构造函数创建`java.io.FileInputStream`对象。 传递一个字符串值，该值用于指定PDF表单的位置。
   * 使用`com.adobe.idp.Document`构造函数创建存储PDF表单的`com.adobe.idp.Document`对象。 将包含PDF表单的`java.io.FileInputStream`对象传递给构造函数。

1. 引用XML数据源。

   * 使用对象的构造函数创建`java.io.FileInputStream`对象，并传递一个字符串值，该值指定包含要导入表单的数据的XML文件的位置。
   * 使用`com.adobe.idp.Document`构造函数创建用于存储表单数据的`com.adobe.idp.Document`对象。 将包含表单数据的`java.io.FileInputStream`对象传递给构造函数。

1. 将数据导入PDF表单。

   通过调用`FormDataIntegrationClient`对象的`importData`方法并传递以下值，将数据导入PDF表单：

   * 存储PDF表单的`com.adobe.idp.Document`对象。
   * 存储表单数据的`com.adobe.idp.Document`对象。

   `importData`方法返回一个用于存储包含XML数据源中数据的PDF表单的`com.adobe.idp.Document`对象。

1. 将PDF表单另存为PDF文件。

   * 创建`java.io.File`对象并确保文件扩展名为“。PDF”。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`importData`方法返回的`Document`对象）。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API导入表单数据](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API导入表单数据 {#import-form-data-using-the-web-service-api}

使用表单数据集成API（Web服务）导入表单数据：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建表单数据集成服务客户端。

   * 使用默认构造函数创建`FormDataIntegrationClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormDataIntegrationClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`FormDataIntegrationClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF表单。

   * 使用构造函数创建`BLOB`对象。 此`BLOB`对象用于存储PDF表单。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值指定PDF表单的位置和打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 引用XML数据源。

   * 使用构造函数创建`BLOB`对象。 此`BLOB`对象用于存储导入到表单中的数据。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值指定包含要导入的数据的XML文件的位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 将数据导入PDF表单。

   通过调用`FormDataIntegrationClient`对象的`importData`方法并传递以下值，将数据导入PDF表单：

   * 存储PDF表单的`BLOB`对象。
   * 存储表单数据的`BLOB`对象。

   `importData`方法返回一个用于存储包含XML数据源中数据的PDF表单的`BLOB`对象。

1. 将PDF表单另存为PDF文件。

   * 通过调用其构造函数并传递表示PDF文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`importData`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 导出表单数据 {#exporting-form-data}

您可以使用表单数据集成服务从交互式PDF表单中导出表单数据。 所导出数据的格式取决于表单类型。 如果表单类型是在Acrobat中创建的Acrobat表单，则导出的数据为XFDF。 如果表单类型是在Designer中创建的XML表单，则导出的数据是XDP。

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要从PDF表单导出表单数据，请执行以下步骤：

1. 包含项目文件
1. 创建表单数据集成服务客户端。
1. 引用PDF表单。
1. 从PDF表单导出数据。
1. 将导出的数据保存为XML文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建表单数据集成服务客户端**

您必须先创建数据集成服务客户端，然后才能以编程方式将数据导入PDF formClient API。 创建服务客户端时，您可以定义调用服务所需的连接设置。 有关信息，[正在设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF表单**

要从PDF表单导出数据，您必须引用在Designer或Acrobat中创建并包含表单数据的PDF表单。 如果尝试从空的PDF表单中导出数据，您将获得空的XML架构。

**从PDF表单导出数据**

在引用包含表单数据的PDF表单后，可以从该表单导出数据。 数据在基于表单的XML架构中导出。

**将表单数据另存为XML文件**

导出表单数据后，可以将数据保存为XML文件。 保存为XML文件后，您可以在XML查看器中打开XML文件以查看表单数据。

**另请参阅**

[使用Java API导出表单数据](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用Web服务API导出表单数据](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表单数据集成服务API快速入门](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[导入表单数据](importing-exporting-data.md#importing-form-data)

### 使用Java API导出表单数据 {#export-form-data-using-the-java-api}

使用表单数据集成API (Java)导出表单数据：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-formdataintegration-client.jar。

1. 创建表单数据集成服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`FormDataIntegrationClient`对象并传递`ServiceClientFactory`对象。

1. 引用PDF表单。

   * 使用对象的构造函数创建`java.io.FileInputStream`对象，并传递一个字符串值，该值指定包含要导出数据的PDF表单的位置。
   * 使用`com.adobe.idp.Document`构造函数创建存储PDF表单的`com.adobe.idp.Document`对象。 将包含PDF表单的`java.io.FileInputStream`对象传递给构造函数。

1. 从PDF表单导出数据。

   通过调用`FormDataIntegrationClient`对象的`exportData`方法导出表单数据，并传递存储PDF表单的`com.adobe.idp.Document`对象。 此方法返回将表单数据存储为XML架构的`com.adobe.idp.Document`对象。

1. 将PDF表单另存为PDF文件。

   * 创建`java.io.File`对象并确保文件扩展名为XML。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`exportData`方法返回的`Document`对象）。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API导出表单数据](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API导出表单数据 {#export-form-data-using-the-web-service-api}

使用表单数据集成API（Web服务）导出表单数据：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建表单数据集成服务客户端。

   * 使用默认构造函数创建`FormDataIntegrationClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormDataIntegrationClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`FormDataIntegrationClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF表单。

   * 使用构造函数创建`BLOB`对象。 此`BLOB`对象用于存储从中导出数据的PDF表单。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值指定PDF表单的位置和打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 从PDF表单导出数据。

   通过调用`FormDataIntegrationClient`对象的`exportData`方法将数据导入PDF表单，并传递存储PDF表单的`BLOB`对象。 此方法返回将表单数据存储为XML架构的`BLOB`对象。

1. 将PDF表单另存为PDF文件。

   * 通过调用其构造函数并传递表示XML文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`exportData`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入XML文件。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
