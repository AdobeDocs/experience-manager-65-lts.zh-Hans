---
title: 使用条形码表单
description: 使用Java API和Web服务API解码PDF表单或包含条形码的图像中的数据。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations, Barcoded Forms
hide: true
hidefromtoc: true
exl-id: 71dc8036-f9a3-4e00-bce1-3f162428053d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# 使用条形码表单 {#working-with-barcoded-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 关于条形码表单服务 {#about-the-barcoded-forms-service}

条形码表单服务可自动从填写和打印表单中捕获数据，并将捕获的信息集成到组织的核心IT系统中。

使用条形码表单服务，您可以将一维条形码和二维条形码添加到交互式PDF forms中。 然后，您可以将条形码表单发布到网站或通过电子邮件或CD分发这些表单。 当用户使用Adobe Reader、Acrobat Professional或Acrobat Standard填写条形码表单时，会自动更新条形码以编码用户提供的表单数据。 用户可以通过电子方式提交表单，或打印为纸面形式，并通过邮件、传真或手稿提交。 您以后可以提取用户提供的数据作为自动化工作流的一部分，在审批流程和业务系统之间传送数据。

有关条形码表单服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解码条形码表单数据 {#decoding-barcoded-form-data}

您可以使用条形码表单服务API来解码PDF表单或包含条形码的图像中的数据。 对表单数据进行解码是指提取条形码中的数据。 在从PDF表单（或图像）解码数据之前，用户必须用数据填充表单。

>[!NOTE]
>
>有关条形码表单服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要从PDF表单解码数据，请执行以下步骤：

1. 包括项目文件。
1. 创建条形码的formsClient API对象。
1. 获取包含条形码数据的PDF表单。
1. 从PDF表单中解码数据。
1. 将数据转换为XML数据源。
1. 处理解码的数据。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* xercesImpl.jar(位于&lt;安装目录>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果将AEM Forms部署在受支持的J2EE应用程序服务器（不是JBOSS）上，则必须将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建条形码表单客户端API对象**

您必须先创建条形码Forms服务客户端，然后才能以编程方式执行条形码表单服务操作。 如果您使用的是Java API，请创建一个`BarcodedFormsServiceClient`对象。 如果您使用条形码表单Web服务API，请创建一个`BarcodedFormsServiceService`对象。

**获取包含条形码数据的PDF表单**

获取包含已填充用户数据的条形码的PDF表单。

**从PDF表单解码数据**

在获取包含条形码的PDF表单（或图像）后，您可以解码数据。 条形码Forms服务支持以下类型的条形码：

* PDF417条形码。
* 数据矩阵条形码。
* 二维码条形码。
* 代码标签条形码。
* 128条码。
* 39条码。
* EAN-13条形码。
* EAN-8条形码。

在解码API中将字符集输入设置为十六进制意味着条形码的内容将编码为十六进制字符串。 例如，如果在表单中将UTF-8指定为字符编码，并在解码操作中指定十六进制，则条形码的内容将在解码输出的&lt; `xb:content`>元素中编码为十六进制字符串。 您可以通过在客户端应用程序中创建应用程序逻辑来转换此十六进制值以获取原始内容。

**将数据转换为XML数据源**

将表单数据解码后，可将其转换为XDP或XFDF数据。 例如，假设您要将数据导入到其他表单中。 要将数据导入XFA表单，则必须将数据转换为XDP数据。 有关信息，请参阅[导入表单数据](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**处理解码的数据**

您可以处理转换后的数据，以满足您的业务需求。 例如，在解码并转换数据后，可以将其保存到文件中，将其存储在企业数据库中，填充其他表单等。 本节讨论如何将转换的数据另存为XML文件。

>[!NOTE]
>
>当行分隔符和字段分隔符参数具有相同的值时，条形码表单服务无法解码条形码数据

**另请参阅**

[使用Java API解码条形码表单数据](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用Web服务API对条形码表单数据进行解码](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API解码条形码表单数据 {#decode-barcoded-form-data-using-the-java-api}

使用条形码表单API(Java)对表单数据进行解码：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建条形码表单客户端API对象

   使用对象的构造函数创建`BarcodedFormsServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 获取包含条形码数据的PDF表单

   * 创建一个`java.io.FileInputStream`对象，该对象表示包含条形码数据的PDF表单，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 从PDF表单解码数据

   通过调用`BarcodedFormsServiceClient`对象的`decode`方法并传递以下值来解码表单数据：

   * 包含PDF表单的`com.adobe.idp.Document`对象。
   * `java.lang.Boolean`对象，它指定是否解码PDF417条形码。
   * `java.lang.Boolean`对象，它指定是否解码数据矩阵条形码。
   * 指定是否解码QR码条形码的`java.lang.Boolean`对象。
   * `java.lang.Boolean`对象，它指定是否解码代码库条形码。
   * `java.lang.Boolean`对象，它指定是否对代码128条形码进行解码。
   * `java.lang.Boolean`对象，它指定是否对代码39条形码进行解码。
   * 指定是否解码EAN-13条形码的`java.lang.Boolean`对象。
   * 指定是否解码EAN-8条形码的`java.lang.Boolean`对象。
   * `com.adobe.livecycle.barcodedforms.CharSet`枚举值，它指定条形码中使用的字符集编码值。

   `decode`方法返回包含已解码表单数据的`org.w3c.dom.Document`对象。

1. 将数据转换为XML数据源

   通过调用`BarcodedFormsServiceClient`对象的`extractToXML`方法并传递以下值，将解码的数据转换为XDP或XFDF数据：

   * 包含已解码数据的`org.w3c.dom.Document`对象（确保您使用`decode`方法的返回值）。
   * 指定行分隔符的`com.adobe.livecycle.barcodedforms.Delimiter`枚举值。 建议您指定`Delimiter.Carriage_Return`。
   * 指定字段分隔符的`com.adobe.livecycle.barcodedforms.Delimiter`枚举值。 例如，指定`Delimiter.Tab`。
   * `com.adobe.livecycle.barcodedforms.XMLFormat`枚举值，它指定是将条形码数据转换为XDP还是XFDF XML数据。 例如，指定`XMLFormat.XDP`将数据转换为XDP数据。

   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   `extractToXML`方法返回一个`java.util.List`对象，其中每个元素都是一个`org.w3c.dom.Document`对象。 每个位于窗体上的条形码都有一个单独的元素。 也就是说，如果表单上有四个条形码，则返回的`java.util.List`对象中有四个元素。

1. 处理解码的数据

   * 循环访问`java.util.List`对象以获取列表中的每个`org.w3c.dom.Document`对象。
   * 对于列表中的每个元素，将`org.w3c.dom.Document`对象转换为`com.adobe.idp.Document`对象。 （使用Java API示例在解码条形码表单数据中显示了将`org.w3c.dom.Document`对象转换为`com.adobe.idp.Document`对象的应用程序逻辑）。
   * 通过调用`com.adobe.idp.Document`对象的`copyToFile`并传递表示XML文件的File对象，将XML数据保存为XML文件。

**另请参阅**

[快速入门(SOAP模式)：使用Java API解码条形码表单数据](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对条形码表单数据进行解码 {#decode-barcoded-form-data-using-the-web-service-api}

使用条形码表单API（Web服务）对表单数据进行解码：

1. 包含项目文件

   * 创建使用条形码表单服务WSDL的Microsoft .NET客户端程序集。 有关信息，请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * 引用Microsoft .NET客户端程序集。 有关信息，请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)中的“引用.NET客户端程序集”。

1. 创建条形码表单客户端API对象

   使用使用条形码表单服务WSDL的Microsoft .NET客户端程序集，通过调用其默认构造函数创建`BarcodedFormsServiceService`对象。

1. 获取包含条形码数据的PDF表单

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储包含条形码的PDF文档。
   * 通过调用其构造函数并传递表示PDF文档文件位置和文件打开模式的字符串值，创建`System.IO.FileStream`对象。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`binaryData`属性以填充`BLOB`对象。

1. 从PDF表单解码数据

   通过调用`BarcodedFormsServiceService`对象的`decode`方法并传递以下值来解码表单数据：

   * 包含PDF表单的`BLOB`对象。
   * `Boolean`对象，它指定是否解码PDF417条形码。
   * `Boolean`对象，它指定是否解码数据矩阵条形码。
   * 指定是否解码QR码条形码的`Boolean`对象。
   * `Boolean`对象，它指定是否解码代码库条形码。
   * `Boolean`对象，它指定是否对代码128条形码进行解码。
   * `Bolean`对象，它指定是否对代码39条形码进行解码。
   * 指定是否解码EAN-13条形码的`Boolean`对象。
   * 指定是否解码EAN-8条形码的`Boolean`对象。
   * `CharSet`枚举值，它指定条形码中使用的字符集编码值。

   `decode`方法返回包含已解码表单数据的字符串值。

1. 将数据转换为XML数据源

   通过调用`BarcodedFormsServiceService`对象的`extractToXML`方法并传递以下值，将解码的数据转换为XDP或XFDF数据：

   * 包含已解码数据的字符串值（请确保您使用`decode`方法的返回值）。
   * 指定行分隔符的`Delimiter`枚举值。 建议您指定`Delimiter.Carriage_Return`。
   * 指定字段分隔符的`Delimiter`枚举值。 例如，指定`Delimiter.Tab`。
   * `XMLFormat`枚举值，它指定是将条形码数据转换为XDP还是XFDF XML数据。 例如，指定`XMLFormat.XDP`将数据转换为XDP数据。

   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   `extractToXML`方法返回`Object`数组，其中每个元素都是`BLOB`实例。 每个位于窗体上的条形码都有一个单独的元素。 也就是说，如果表单上有四个条形码，则返回的`Object`数组中有四个元素。

1. 处理解码的数据

   * 通过调用其构造函数并传递表示受保护PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`encryptPDFUsingPassword`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`binaryData`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
