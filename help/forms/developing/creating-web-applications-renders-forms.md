---
title: 创建呈现Forms的Web应用程序
description: 创建基于Web的应用程序，该应用程序使用Java Servlet调用Forms服务和渲染表单。 Java Servlet用作返回表单的Forms服务与客户端Web浏览器之间的链接。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Workbench, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 071781e8-990d-4d01-b46e-be1c57bdbe3a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 创建可渲染Forms的Web应用程序 {#creating-web-applications-thatrenders-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 创建可渲染Forms的Web应用程序 {#creating-web-applications-that-renders-forms}

您可以创建基于Web的应用程序，该应用程序使用Java Servlet调用Forms服务和渲染表单。 使用Java™ Servlet的优点是，可以将进程的返回值写入客户端Web浏览器。 也就是说，Java servlet可用作返回表单的Forms服务与客户端Web浏览器之间的链接。

>[!NOTE]
>
>本节介绍如何创建基于Web的应用程序，该应用程序使用Java servlet调用Forms服务并基于片段呈现表单。 (请参阅[根据片段渲染Forms](/help/forms/developing/rendering-forms-based-fragments.md)。)

使用Java Servlet，您可以将表单写入客户端Web浏览器，以便客户查看表单并在表单中输入数据。 使用数据填充表单后，Web用户单击表单上的提交按钮以将信息发送回Java Servlet，从中可检索和处理数据。 例如，可以将数据发送到另一个进程。

本节讨论如何创建基于Web的应用程序，以便用户选择基于美国的表单数据或基于加拿大的表单数据，如下图所示。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

呈现的表单是基于片段的表单。 也就是说，如果用户选择美国数据，则返回的表单会使用基于美国数据的片段。 例如，表单页脚包含美国地址，如下图所示。

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

同样，如果用户选择加拿大数据，则返回的表单包含加拿大地址，如下图所示。

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>有关基于片段创建表单设计的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

**示例文件**

本节使用位于以下位置的示例文件：

&lt;*Forms Designer安装目录*>/Samples/Forms/采购订单/表单片段

其中&lt;*install directory*>是安装路径。 出于客户端应用程序的目的，已从此安装位置复制了采购订单Dynamic.xdp文件，并将其部署到名为&#x200B;*Applications/FormsApplication*&#x200B;的Forms应用程序。 采购订单Dynamic.xdp文件放置在名为FormsFolder的文件夹中。 同样，片段放置在名为Fragments的文件夹中，如下图所示。

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

要访问采购订单Dynamic.xdp表单设计，请将`Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp`指定为表单名称（传递给`renderPDFForm`方法的第一个参数），并将`repository:///`指定为内容根URI值。

Web应用程序使用的XML数据文件已从Data文件夹移至`C:\Adobe`(属于承载AEM Forms的J2EE应用程序服务器的文件系统)。 文件名是采购订单&#x200B;*Canada.xml*&#x200B;和采购订单&#x200B;*US.xml*。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

### 步骤摘要 {#summary-of-steps}

要创建基于Web的应用程序，以基于片段呈现表单，请执行以下步骤：

1. 创建Web项目。
1. 创建表示Java servlet的Java应用程序逻辑。
1. 为Web应用程序创建网页。
1. 将Web应用程序打包到WAR文件中。
1. 将WAR文件部署到J2EE应用程序服务器。
1. 测试您的Web应用程序。

>[!NOTE]
>
>其中某些步骤取决于部署AEM Forms的J2EE应用程序。 例如，用于部署WAR文件的方法取决于您使用的J2EE应用程序服务器。 本节假定AEM Forms部署在JBoss®上。

### 创建Web项目 {#creating-a-web-project}

创建包含可调用Forms服务的Java servlet的Web应用程序的第一步是创建一个Web项目。 本文档所基于的Java IDE是Eclipse 3.3。使用Eclipse IDE创建一个Web项目，并将所需的JAR文件添加到您的项目中。 最后，将名为&#x200B;*index.html*&#x200B;的HTML页面和Java Servlet添加到您的项目中。

以下列表指定了必须添加到Web项目中的JAR文件：

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

有关这些JAR文件的位置，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Web项目：**

1. 启动Eclipse并单击&#x200B;**文件** > **新建项目**。
1. 在&#x200B;**新建项目**&#x200B;对话框中，选择&#x200B;**Web** > **动态Web项目**。
1. 键入`FragmentsWebApplication`作为项目名称，然后单击&#x200B;**完成**。

**要将所需的JAR文件添加到项目：**

1. 在“项目资源管理器”窗口中，右键单击`FragmentsWebApplication`项目并选择&#x200B;**属性**。
1. 单击&#x200B;**Java生成路径**，然后单击&#x200B;**库**&#x200B;选项卡。
1. 单击&#x200B;**添加外部JAR**&#x200B;按钮并浏览要包含的JAR文件。

**要向项目添加Java servlet，请执行以下操作：**

1. 在“项目资源管理器”窗口中，右键单击`FragmentsWebApplication`项目并选择&#x200B;**新建** > **其他**。
1. 展开&#x200B;**Web**&#x200B;文件夹，选择&#x200B;**Servlet**，然后单击&#x200B;**下一步**。
1. 在“创建Servlet”对话框中，键入`RenderFormFragment`作为Servlet的名称，然后单击&#x200B;**完成**。

**要将HTML页面添加到您的项目，请执行以下操作：**

1. 在“项目资源管理器”窗口中，右键单击`FragmentsWebApplication`项目并选择&#x200B;**新建** > **其他**。
1. 展开&#x200B;**Web**&#x200B;文件夹，选择&#x200B;**HTML**，然后单击&#x200B;**下一步**。
1. 在“新建HTML”对话框中，键入`index.html`作为文件名，然后单击&#x200B;**完成**。

>[!NOTE]
>
>有关创建调用`RenderFormFragment` Java Servlet的HTML页面的信息，请参阅[创建网页](/help/forms/developing/rendering-forms.md#creating-the-web-page)。

### 为servlet创建Java应用程序逻辑 {#creating-java-application-logic-for-the-servlet}

您可以创建Java应用程序逻辑，以从Java Servlet中调用Forms服务。 以下代码显示`RenderFormFragment` Java Servlet的语法：

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

通常，您不会将客户端代码放置在Java servlet的`doGet`或`doPost`方法中。 更好的编程做法是将此代码放在单独的类中，从`doPost`方法（或`doGet`方法）中实例化该类，并调用适当的方法。 但是，为了代码简洁，本节中的代码示例尽量少，代码示例放在`doPost`方法中。

要使用Forms服务API呈现基于片段的表单，请执行以下任务：

1. 在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。 有关这些文件的位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 检索从HTML表单提交的单选按钮的值，并指定使用美国数据还是加拿大数据。 如果提交了American，请创建一个`com.adobe.idp.Document`，将数据存储在&#x200B;*采购订单US.xml*&#x200B;中。 同样，如果为Canadian，则创建一个`com.adobe.idp.Document`以将数据存储在&#x200B;*Purchase Order Canada.xml*&#x200B;文件中。
1. 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。
1. 使用构造函数创建存储URI值的`URLSpec`对象。
1. 调用`URLSpec`对象的`setApplicationWebRoot`方法，并传递表示应用程序的Web根的字符串值。
1. 调用`URLSpec`对象的`setContentRootURI`方法，并传递一个指定内容根URI值的字符串值。 确保表单设计和片段位于内容根URI中。 否则，Forms服务会引发异常。 要引用AEM Forms存储库，请指定`repository://`。
1. 调用`URLSpec`对象的`setTargetURL`方法，并传递一个字符串值，该值指定将表单数据发布到的目标URL值。 如果您在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到哪个URL来执行计算。
1. 调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。
   * 包含要与表单（在步骤2中创建）合并的数据的`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 有关详细信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 一个`URLSpec`对象，它包含Forms服务基于片段呈现表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。

   `renderPDFForm`方法返回的`FormsResult`对象包含必须写入客户端Web浏览器的表单数据流。

1. 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
1. 通过调用其`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
1. 通过调用其`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
1. 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
1. 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
1. 通过调用`InputStream`对象的`read`方法并将该字节数组作为参数传递，创建字节数组以表单数据流填充该字节数组。
1. 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

以下代码示例表示调用Forms服务并基于片段呈现表单的Java servlet。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### 创建网页 {#creating-the-web-page}

index.html网页提供Java servlet的入口点并调用Forms服务。 此网页是基本的HTML表单，包含两个单选按钮和一个提交按钮。 单选按钮的名称为单选按钮。 当用户单击提交按钮时，表单数据将发布到`RenderFormFragment` Java Servlet。

Java Servlet通过使用以下Java代码捕获从HTML页面发布的数据：

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

以下HTML代码位于在设置开发环境期间创建的index.html文件中。 （请参阅[创建Web项目](/help/forms/developing/rendering-forms.md#creating-a-web-project)。）

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### 打包Web应用程序 {#packaging-the-web-application}

要部署调用Forms服务的Java servlet，请将您的Web应用程序打包到WAR文件。 确保组件的业务逻辑所依赖的外部JAR文件（如adobe-livecycle-client.jar和adobe-forms-client.jar）也包含在WAR文件中。

**要将Web应用程序打包到WAR文件：**

1. 在&#x200B;**项目资源管理器**&#x200B;窗口中，右键单击`FragmentsWebApplication`项目并选择&#x200B;**导出** > **WAR文件**。
1. 在&#x200B;**Web模块**&#x200B;文本框中，键入`FragmentsWebApplication`作为Java项目的名称。
1. 在&#x200B;**目标**&#x200B;文本框中，为&#x200B;**文件名键入`FragmentsWebApplication.war`**，指定WAR文件的位置，然后单击“完成”。

### 将WAR文件部署到J2EE应用程序服务器 {#deploying-the-war-file-to-the-j2ee-application-server}

您可以将WAR文件部署到部署AEM Forms的J2EE应用程序服务器。 部署WAR文件后，您可以使用Web浏览器访问HTML网页。

**要将WAR文件部署到J2EE应用程序服务器：**

* 将WAR文件从导出路径复制到`[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`。

### 测试Web应用程序 {#testing-your-web-application}

部署Web应用程序后，可以使用Web浏览器对其进行测试。 假定您使用的计算机与托管AEM Forms的计算机相同，则可以指定以下URL：

* http://localhost:8080/FragmentsWebApplication/index.html

  选择一个单选按钮，然后单击“提交”按钮。 Web浏览器中将显示基于片段的表单。 如果出现问题，请参阅J2EE应用程序服务器的日志文件。
