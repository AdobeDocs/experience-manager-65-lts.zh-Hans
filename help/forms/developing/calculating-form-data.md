---
title: 计算表单数据
description: 使用Forms服务计算用户在表单中输入的值并显示结果。 Forms服务使用Java API和Web服务API计算值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 071a6ccb-8204-4cbc-a39b-143da52c16f7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# 计算表单数据 {#calculating-form-data}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

Forms服务可以计算用户在表单中输入的值并显示结果。 要计算表单数据，必须执行两项任务。 首先，创建用于计算表单数据的表单设计脚本。 窗体设计支持三种类型的脚本。 一种脚本类型在客户端运行，另一种脚本类型在服务器上运行，第三种脚本类型同时在服务器和客户端运行。 本主题中讨论的脚本类型在服务器上运行。 HTML、PDF和表单指南（已弃用）转换支持服务器端计算。

在表单设计过程中，您可以使用计算和脚本提供更丰富的用户体验。 可将计算和脚本添加到大多数表单字段和对象。 创建表单设计脚本，以对用户输入交互式表单的数据执行计算操作。

用户在表单中输入值，然后单击“计算”按钮以查看结果。 以下流程描述了允许用户计算数据的示例应用程序：

* 用户访问名为StartLoan.html的HTML页面，该页面用作Web应用程序的起始页面。 此页调用名为`GetLoanForm`的Java Servlet。
* `GetLoanForm` servlet渲染贷款表单。 此表单包含脚本、交互式字段、计算按钮和提交按钮。
* 用户在表单的字段中输入值并单击计算按钮。 该表单将发送到执行脚本的`CalculateData` Java Servlet。 该表单将发送回用户，并在表单中显示计算结果。
* 用户继续输入和计算值，直到显示满意的结果。 满意后，用户单击“提交”按钮处理表单。 该表单将发送到另一个名为`ProcessForm`的Java Servlet，负责检索提交的数据。 (请参阅[处理提交的Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)


下图显示了应用程序的逻辑流。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

下表描述了此图中的步骤。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>从HTML起始页调用<code>GetLoanForm</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服务客户端API向客户端Web浏览器呈现贷款表单。 渲染包含配置为在服务器上运行的脚本的表单与渲染不包含脚本的表单之间的区别在于，您必须指定用于执行脚本的目标位置。 如果未指定目标位置，则不会执行配置为在服务器上运行的脚本。 例如，请考虑本节中介绍的应用程序。 <code>CalculateData</code> Java Servlet是执行脚本的目标位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户将数据输入到交互式字段中，然后单击“计算”按钮。 该表单将发送到<code>CalculateData</code> Java Servlet，并在其中执行脚本。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表单将呈现回Web浏览器，并在表单中显示计算结果。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>当值满意时，用户单击“提交”按钮。 该表单被发送到另一个名为<code>ProcessForm</code>的Java Servlet。</p></td>
  </tr>
 </tbody>
</table>

通常，作为PDF内容提交的表单包含客户端上执行的脚本。 但是，也可以执行服务器端计算。 提交按钮不能用于计算脚本。 在此情况下，不会执行计算，因为Forms服务认为交互已完成。

为了说明表单设计脚本的使用，本节将检查一个简单的交互式表单，该表单包含配置为在服务器上运行的脚本。 下图显示了一个表单设计，该设计包含一个脚本，该脚本添加用户在前两个字段中输入的值并在第三个字段中显示结果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.**&#x200B;名为NumericField1 **B.**&#x200B;名为NumericField2 **C.**&#x200B;名为NumericField3的字段

此窗体设计中的脚本语法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此窗体设计中，“计算”按钮是一个命令按钮，脚本位于该按钮的`Click`事件中。 当用户在前两个字段（NumericField1和NumericField2）中输入值并单击“计算”按钮时，表单将发送到Forms服务，并在其中执行脚本。 Forms服务将表单呈现回客户端设备，并在NumericField3字段中显示计算结果。

>[!NOTE]
>
>有关创建表单设计脚本的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要计算表单数据，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 检索包含计算脚本的表单。
1. 将表单数据流写回客户端Web浏览器

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。 如果您使用的是Java API，请创建一个`FormsServiceClient`对象。 如果您使用的是Forms Web服务API，请创建一个`FormsServiceService`对象。

**检索包含计算脚本的表单**

您可以使用Forms服务客户端API创建应用程序逻辑，该逻辑处理包含配置为在服务器上运行的脚本的表单。 该过程与处理提交的表单类似。 (请参阅[处理提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)

验证与已提交表单关联的处理状态为`1` `(Calculate)`，这意味着Forms服务正在对表单数据执行计算操作，并且必须将结果写回用户。 在这种情况下，将自动执行配置为在服务器上运行的脚本。

**将表单数据流写回客户端Web浏览器**

验证与提交的表单关联的处理状态为`1`后，必须将结果写回客户端Web浏览器。 显示表单时，计算值将显示在相应的字段中。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[使用Java API计算表单数据](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[使用Web服务API计算表单数据](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[正在设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)
[创建呈现Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API计算表单数据 {#calculate-form-data-using-the-java-api}

使用Forms API (Java)计算表单数据：

1. 包含项目文件

   将客户端JAR文件（如adobe-forms-client.jar）包含在Java项目的类路径中。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。

1. 检索包含计算脚本的表单

   * 要检索包含计算脚本的表单数据，请使用其构造函数创建`com.adobe.idp.Document`对象，并从构造函数中调用`javax.servlet.http.HttpServletResponse`对象的`getInputStream`方法。
   * 调用`FormsServiceClient`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`com.adobe.idp.Document`对象。
      * 一个字符串值，它指定包含所有相关HTTP标头的环境变量。 通过为`CONTENT_TYPE`环境变量指定一个或多个值来指定要处理的内容类型。 例如，要处理XML和PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 指定`HTTP_USER_AGENT`标头值的字符串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存储运行时选项的`RenderOptionsSpec`对象。

     `processFormSubmission`方法返回包含表单提交结果的`FormsResult`对象。

   * 通过调用`FormsResult`对象的`getAction`方法，验证与已提交表单关联的处理状态为`1`。 如果此方法返回值`1`，则执行计算，并且数据可以写回客户端Web浏览器。

1. 将表单数据流写回客户端Web浏览器

   * 创建用于将表单数据流发送到客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建字节数组并使用表单数据流填充该数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**


[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[正在设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API计算表单数据 {#calculate-form-data-using-the-web-service-api}

使用Forms API（Web服务）计算表单数据：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 检索包含计算脚本的表单

   * 要检索发布到Java Servlet的表单数据，请使用其构造函数创建`BLOB`对象。
   * 使用`javax.servlet.http.HttpServletResponse`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 使用对象的构造函数创建`java.io.ByteArrayOutputStream`对象并传递`java.io.InputStream`对象的长度。
   * 将`java.io.InputStream`对象的内容复制到`java.io.ByteArrayOutputStream`对象中。
   * 通过调用`java.io.ByteArrayOutputStream`对象的`toByteArray`方法创建字节数组。
   * 通过调用其`setBinaryData`方法并将字节数组作为参数传递来填充`BLOB`对象。
   * 使用构造函数创建`RenderOptionsSpec`对象。 通过调用`RenderOptionsSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来设置区域设置值。
   * 调用`FormsServiceClient`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`BLOB`对象。
      * 一个字符串值，它指定包含所有相关HTTP标头的环境变量。 例如，您可以指定以下字符串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 指定`HTTP_USER_AGENT`标头值的字符串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存储运行时选项的`RenderOptionsSpec`对象。 有关更多信息， 。
      * 方法填充的空`BLOBHolder`对象。
      * 方法填充的空`javax.xml.rpc.holders.StringHolder`对象。
      * 方法填充的空`BLOBHolder`对象。
      * 方法填充的空`BLOBHolder`对象。
      * 方法填充的空`javax.xml.rpc.holders.ShortHolder`对象。
      * 方法填充的空`MyArrayOf_xsd_anyTypeHolder`对象。 此参数用于存储与表单一起提交的文件附件。
      * 用提交表单的方法填充的空`FormsResultHolder`对象。

     `processFormSubmission`方法使用表单提交结果填充`FormsResultHolder`参数。 `processFormSubmission`方法返回包含表单提交结果的`FormsResult`对象。

   * 通过调用`FormsResult`对象的`getAction`方法，验证与已提交表单关联的处理状态为`1`。 如果此方法返回值`1`，则执行计算，并且数据可以写回客户端Web浏览器。

1. 将表单数据流写回客户端Web浏览器

   * 创建用于将表单数据流发送到客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 创建字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**
[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
