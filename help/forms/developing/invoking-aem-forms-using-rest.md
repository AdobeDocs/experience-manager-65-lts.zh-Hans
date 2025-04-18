---
title: 使用REST请求调用AEM Forms
description: 使用REST请求调用在Workbench中创建的流程。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 11a7278e-efaa-402c-8add-5280bf5a156a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 0%

---

# 使用REST请求调用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

可以配置在Workbench中创建的进程，以便您可以通过代表性状态传输(REST)请求来调用它们。 从HTML页面发送REST请求。 即，您可以使用REST请求直接从网页调用Forms进程。 例如，您可以打开网页的新实例。 然后，您可以调用Forms进程，并加载渲染的PDF文档，其中包含HTTP POST请求中发送的数据。

存在两种类型的HTML客户端。 第一个HTML客户端是使用JavaScript编写的AJAX客户端。 第二个客户端是包含提交按钮的HTML表单。 基于HTML的客户端应用程序不是唯一可能的REST客户端。 任何支持HTTP请求的客户端应用程序都可以使用REST调用调用来调用服务。 例如，您可以使用PDF表单中的REST调用来调用服务。 (请参阅[从Acrobat调用MyApplication/EncryptDocument进程](#rest-invocation-examples)。)

在使用REST请求时，建议您不要直接调用Forms服务。 而是调用在Workbench中创建的流程。 在创建用于REST调用的进程时，请使用程序化起点。 在这种情况下，将自动添加REST端点。 有关在Workbench中创建进程的信息，请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

使用REST调用服务时，系统会提示您输入AEM表单用户名和密码。 但是，如果不想指定用户名和密码，则可以禁用服务安全性。

要使用REST调用Forms服务（流程在激活时变为服务），请配置REST端点。 （请参阅[管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)中的“管理端点”。）

配置REST端点后，您可以使用HTTP GET方法或POST方法调用Forms服务。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必需`ServiceName`值是要调用的Forms服务的名称。 可选的`OperationName`值是服务操作的名称。 如果未指定此值，则此名称默认为`invoke`，即启动进程的操作名称。 可选的`ServiceVersion`值是以X.Y格式编码的版本。 如果未指定此值，则使用最新版本。 `enctype`值也可以是`application/x-www-form-urlencoded`。

## 支持的数据类型 {#supported-data-types}

使用REST请求调用AEM Forms服务时，支持以下数据类型：

* Java原始数据类型，例如字符串和整数
* `com.adobe.idp.Document`数据类型
* XML数据类型，如`org.w3c.Document`和`org.w3c.Element`
* 集合对象，如`java.util.List`和`java.util.Map`

  通常接受将这些数据类型作为Workbench中创建进程的输入值。

  如果使用HTTP POST方法调用Froms服务，则参数将传递到HTTP请求正文中。 如果AEM Forms服务的签名具有字符串输入参数，则请求正文可以包含输入参数的文本值。 如果服务的签名定义了多个字符串参数，则请求可以遵循HTTP的`application/x-www-form-urlencoded`表示法，并将参数的名称用作表单的字段名称。

  如果Forms服务返回字符串参数，则结果以文本形式表示输出参数。 如果服务返回多个字符串参数，则结果为XML文档，它按以下格式对输出参数进行编码：
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >`output-paramater1`值表示输出参数名称。

  如果Forms服务需要`com.adobe.idp.Document`参数，则只能使用HTTP POST方法调用该服务。 如果服务需要一个`com.adobe.idp.Document`参数，则HTTP请求正文将成为输入Document对象的内容。

  如果AEM Forms服务需要多个输入参数，则HTTP请求正文必须是由RFC 1867定义的多部分MIME消息。 （RFC 1867是Web浏览器用于将文件上传到网站的标准。） 每个输入参数必须作为多部分消息的单独部分发送，并以`multipart/form-data`格式编码。 每个部件的名称必须与参数的名称匹配。

  列表和映射也用作在Workbench中创建的AEM Forms进程的输入值。 因此，您可以在使用REST请求时使用这些数据类型。 不支持Java数组，因为它们未用作AEM Forms进程的输入值。

  如果输入参数是列表，则REST客户端可以通过多次指定该参数（针对列表中的每个项目指定一次）来发送该参数。 例如，如果A是文档列表，则输入必须是由多个名为A的部分组成的多部分消息。在这种情况下，每个名为A的部件都会成为输入列表中的项。 如果B是字符串列表，则输入可以是包含多个名为B的字段的`application/x-www-form-urlencoded`消息。在这种情况下，每个名为B的表单字段都会成为输入列表中的项。

  如果输入参数是映射并且是仅服务输入参数，则输入消息的每个部分/字段都成为映射中的键/值记录。 每个部分/字段的名称将成为记录的键。 每个部分/字段的内容将成为记录的值。

  如果输入映射不是仅服务输入参数，则属于该映射的每个键/值记录可以使用名为的参数发送，该参数是参数名称和记录键的串联。 例如，名为`attributes`的输入映射可以随以下键/值对的列表一起发送：

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  这将转换为包含三个记录的映射： `Color=red`、`Shape=box`和`Width=5`。

  列表和映射类型的输出参数会成为生成XML消息的一部分。 输出列表在XML中表示为一系列XML元素，列表中每个项目都有一个元素。 每个元素都被赋予与输出列表参数相同的名称。 每个XML元素的值是以下两个值之一：

* 列表中项目的文本表示形式（如果列表包含字符串类型）
* 指向文档内容的URL（如果列表包含`com.adobe.idp.Document`对象）

  以下示例是一个服务返回的XML消息，该服务具有名为&#x200B;*list*的单个输出参数，该参数是一个整数列表。
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`在生成的XML消息中，输出映射参数表示为一系列的XML元素，其中映射中的每个记录都有一个元素。 每个元素的名称与映射记录的键相同。 每个元素的值是映射记录值的文本表示形式（如果映射包含具有字符串值的记录）或指向文档内容的URL（如果映射包含具有`com.adobe.idp.Document`值的记录）。 以下是由具有名为`map`的单个输出参数的服务返回的XML消息的示例。 此参数值是一个映射，包含将字母与`com.adobe.idp.Document`对象关联的记录。
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 异步调用 {#asynchronous-invocations}

某些AEM Forms服务（例如以人为中心的长期流程）需要很长时间才能完成。 这些服务可以以非阻塞方式异步调用。 （请参阅[调用以人为中心的长期进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

通过在调用URL中将`services`替换为`async_invoke`，可以异步调用AEM Forms服务，如以下示例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL返回负责此调用的作业的标识符值（采用“文本/普通”格式）。

通过使用被替换为`async_status`的`services`的调用URL，可以检索异步调用的状态。 URL必须包含一个`job_id`参数，该参数指定与此调用关联的作业的标识符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL会根据作业管理器的规范（例如，2表示正在运行，3表示已完成，4表示失败，等等）返回一个整数值（以“文本/纯”格式），用于编码作业状态。

如果作业已完成，则URL将返回与同步调用服务相同的结果。

作业完成并检索到结果后，可以使用具有`services`的调用URL将作业处理为`async_dispose`。 URL还应包含指定作业的标识符值的`job_id`参数。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作业处置成功，则此URL将返回空消息。

## 错误报告 {#error-reporting}

如果由于服务器上抛出异常而无法完成同步或异步调用请求，则该异常将作为HTTP响应消息的一部分报告。 如果调用URL（或者如果异步调用，则为`async_result` URL）没有.xml后缀，则REST提供程序返回HTTP代码`500 Internal Server Error`，后跟异常消息。

如果调用URL（或者如果存在异步调用，则为`async_result` URL）确实具有.xml后缀，则REST提供程序返回HTTP代码`200 OK`，后跟一个描述异常的XML文档，格式如下。

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

`DSCError`元素是可选的，仅当异常是`com.adobe.idp.dsc.DSCException`的实例时才会出现。

## 安全性和身份验证 {#security-and-authentication}

为了向REST调用提供安全传输，AEM Forms管理员可以在托管AEM Forms的J2EE应用程序服务器中启用HTTPS协议。 此配置特定于J2EE应用程序服务器；它不是Forms Server配置的一部分。

>[!NOTE]
>
>作为希望通过REST端点公开流程的Workbench开发人员，请记住XSS漏洞问题。 XSS漏洞可用于窃取或操纵Cookie、修改内容的呈现方式，以及危害机密信息。 如果XSS漏洞是一个问题，建议您使用其他输入和输出数据验证规则来扩展进程逻辑。

## 支持REST调用的AEM Forms服务 {#aem-forms-services-that-support-rest-invocation}

虽然建议您使用Workbench而不是直接服务来调用创建的流程，但有些一些AEM Forms服务确实支持REST调用。 建议直接调用进程而不是服务的原因是，这样可以更高效地调用进程。 请考虑以下方案。 假定您要从REST客户端创建策略。 即，您希望REST客户端定义策略名称、离线租赁期等值。

要创建策略，您必须定义复杂的数据类型，如`PolicyEntry`对象。 `PolicyEntry`对象定义与策略关联的属性，例如权限。 （请参阅[创建策略](/help/forms/developing/protecting-documents-policies.md#creating-policies)。）

不要发送REST请求来创建策略（这将包括定义复杂的数据类型，如`PolicyEntry`对象），而应创建使用Workbench创建策略的进程。 定义进程以接受原始输入变量，如定义进程名称的字符串值或定义离线租赁期的整数。

这样，您就不必创建包含操作所需的复杂数据类型的REST调用请求。 该进程定义了复杂的数据类型，您从REST客户端执行的所有操作是调用该进程并传递原始数据类型。 有关使用REST调用进程的信息，请参阅[使用REST调用MyApplication/EncryptDocument进程](#rest-invocation-examples)。

以下列表列出了支持直接REST调用的AEM Forms服务。

* Distiller服务
* Rights Management服务
* 生成PDF服务
* 生成3dPDF服务
* FormDataIntegration

## REST调用示例 {#rest-invocation-examples}

提供了以下REST调用示例：

* 将布尔值传递给AEM Forms进程
* 将日期值传递到AEM Forms进程
* 将文档传递到AEM Forms进程
* 将文档和文本值传递到AEM Forms进程
* 将枚举值传递到AEM Forms进程
* 使用REST调用MyApplication/EncryptDocument进程
* 从Acrobat调用MyApplication/EncryptDocument进程

  每个示例都演示了向AEM Forms流程传递各种数据类型

**将布尔值传递给进程**

以下HTML示例将两个`Boolean`值传递到名为`RestTest2`的AEM Forms进程。 调用方法的名称为`invoke`，版本为1.0。请注意，使用的是HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**将日期值传递给进程**

以下HTML示例将日期值传递到名为`SOAPEchoService`的AEM Forms进程。 调用方法的名称为`echoCalendar`。 请注意，使用的是HTML `Post`方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**将文档传递到进程**

以下HTML示例调用名为`MyApplication/EncryptDocument`的AEM Forms进程，该进程需要PDF文档。 有关此进程的信息，请参阅[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**将文档和文本值传递给进程**

以下HTML示例调用名为`RestTest3`的AEM Forms进程，该进程需要文档和两个文本值。 请注意，使用的是HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**将枚举值传递给进程**

以下HTML示例调用名为`SOAPEchoService`的AEM Forms进程，该进程需要枚举值。 请注意，使用的是HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**使用REST调用MyApplication/EncryptDocument进程**

您可以使用REST调用名为&#x200B;*MyApplication/EncryptDocument*&#x200B;的AEM Forms短期进程。

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请使用workbench创建名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于`SetValue`操作。 此进程的输入参数是名为`inDoc`的`document`进程变量。
1. 使用密码加密PDF文档。 此操作基于`PasswordEncryptPDF`操作。 密码加密的PDF文档在名为`outDoc`的过程变量中返回。

   使用REST请求调用此进程时，Web浏览器中会显示加密的PDF文档。 在查看PDF文档之前，请指定密码（除非禁用了安全保护）。 以下HTML代码表示对`MyApplication/EncryptDocument`进程的REST调用请求。

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**从Acrobat调用MyApplication/EncryptDocument进程** {#invoke-process-acrobat}

您可以使用REST请求从Acrobat调用Forms进程。 例如，您可以调用&#x200B;*MyApplication/EncryptDocument*&#x200B;进程。 要从Acrobat调用Forms进程，请在Designer中的XDP文件上放置提交按钮。 (请参阅[Designer帮助](https://www.adobe.com/go/learn_aemforms_designer_63)。)

在按钮的&#x200B;*提交到URL*&#x200B;字段中指定用于调用进程的URL，如下图所示。

用于调用进程的完整URL为https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果流程需要PDF文档作为输入值，请确保以PDF的形式提交表单，如上图所示。 此外，要成功调用进程，该进程必须返回PDF文档。 否则，Acroabt无法处理返回值并出现错误。 不必指定输入进程变量的名称。 例如，*MyApplication/EncryptDocument*&#x200B;进程有一个名为`inDoc`的输入变量。 只要将表单作为PDF提交，您就不必指定inDoc。

您还可以将表单数据作为XML提交到Forms进程。要提交XML数据，请确保`Submit As`下拉列表指定XML。 由于进程的返回值必须是PDF文档，因此PDF文档会显示在Acrobat中。
