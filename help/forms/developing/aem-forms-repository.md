---
title: 使用AEM Forms存储库
description: 管理AEM Forms存储库，以使用Java API和Web服务API创建文件夹、写入、列出、读取、更新和搜索资源。 此外，了解如何创建资源关系、锁定和删除资源。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 4a911fe6-2939-4c8c-b486-7575c759857d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '9036'
ht-degree: 0%

---

# 使用AEM Forms存储库 {#working-with-aem-forms-repository}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于存储库服务**

存储库服务为AEM Forms提供资源存储和管理服务。 当开发人员创建&#x200B;*AEM Forms*&#x200B;应用程序时，他们可以在存储库中部署资源，而不是在文件系统中部署资源。 资源可以包括任何类型的宣传资料，包括XML表单、PDF forms(包括Acrobat表单)、表单片段、图像、配置文件、策略、SWF文件、DDX文件、XML架构、WSDL文件和测试数据。

例如，考虑以下名为&#x200B;*Applications/FormsApplication*&#x200B;的Forms应用程序：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

请注意，FormsFolder中有一个名为Loan.xdp的文件。 要访问此窗体设计，请指定完整路径（包括版本）： `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

AEM Forms存储库中资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示了一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用Web浏览器浏览AEM Forms存储库。 要浏览存储库，请在Web浏览器`https://[server name]:[server port]/repository`中输入以下URL。 您可以使用Web浏览器验证与使用AEM Forms存储库部分关联的快速入门结果。 例如，如果将内容添加到AEM Forms存储库，则可以在Web浏览器中查看该内容。 (请参阅[快速入门(SOAP模式)：使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)。)

存储库API提供了几种可用于存储和检索存储库信息的操作。 例如，在处理应用程序时需要资源时，您可以获取资源列表或检索存储在存储库中的特定资源。

>[!NOTE]
>
>存储库API无法用于与Content Services交互（已弃用）。 要与内容服务交互（已弃用），请使用文档管理API。

使用存储库服务API，您可以完成以下任务：

* 创建文件夹。 请参阅[创建文件夹](aem-forms-repository.md#creating-folders)。
* 编写资源及其属性。 请参阅[正在写入资源](aem-forms-repository.md#writing-resources)。
* 列出给定收藏集中的资源或其他相关资源。 请参阅[列出资源](aem-forms-repository.md#listing-resources)。
* 读取资源及其属性。 请参阅[正在读取资源](aem-forms-repository.md#reading-resources)。
* 更新资源及其属性。 请参阅[更新资源](aem-forms-repository.md#updating-resources)。
* 搜索资源，包括其历史记录、相关资源和属性。 请参阅[搜索资源](aem-forms-repository.md#searching-for-resources)。
* 指定资源之间的关系。 请参阅[创建资源关系](aem-forms-repository.md#creating-resource-relationships)。
* 管理资源访问控制，包括锁定和解锁资源，以及读写访问控制列表(ACL)。 请参阅[锁定资源](aem-forms-repository.md#locking-resources)。
* 删除资源及其属性。 请参阅[删除资源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用存储库API，您无法通过使用ECM存储库来管理资源访问控制、搜索资源或指定资源关系。

>[!NOTE]
>
>将加密的PDF写入存储库时，无法使用自动关系提取功能。 否则，可以将加密的PDF存储在存储库中并在以后进行检索。 从PDF中检索它后，检索器可以选择将它解密。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建文件夹 {#creating-folders}

文件夹（资源集合）用于将对象（文件或资源）存储在组织的分组中。 文件夹可以包含资源和其他文件夹，也称为子文件夹。 资源一次只能存储在一个文件夹中。

文件从文件夹继承访问控制列表(ACL)，子文件夹从其父文件夹继承ACL。 因此，在创建子文件夹之前，父文件夹必须存在。 IDE仅允许您逐个文件夹进行交互，而不是逐个文件进行交互。 您不能对文件夹进行版本控制，也不需要这样做；文件夹本身并不包含数据。 它只是包含数据的资源的容器。 默认的ACL是系统级别的权限，这意味着用户必须具有系统级别的权限（读取、写入、遍历、管理ACL），直到有人授予他们对特定文件夹的权限为止。 ACL只能在IDE中工作。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建文件夹，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 创建文件夹。
1. 将文件夹写入存储库。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式创建资源集合。 这是通过创建服务客户端来实现的。

**创建文件夹**

调用存储库服务方法以创建资源集合，并使用标识信息（包括其UUID、文件夹名称和描述）填充资源集合。

**将文件夹写入存储库**

调用存储库服务方法以写入资源集合，指定目标文件夹的URI。

**另请参阅**

[使用Java API创建文件夹](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服务API创建文件夹](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API创建文件夹 {#create-folders-using-the-java-api}

使用存储库服务API (Java)创建文件夹：

1. 包含项目文件

   在Java项目的类路径中包含项目文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 创建文件夹

   要创建资源集合，必须首先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`repositoryInfomodelFactoryBean`对象的`newResourceCollection`方法，并传入以下参数：

   * 要分配给资源的`com.adobe.repository.infomodel.Id` UUID标识符。
   * 要分配给资源的`com.adobe.repository.infomodel.Lid` UUID标识符。
   * 包含资源集合名称的`java.lang.String`。 例如 `FormsFolder`。

   该方法返回表示新文件夹的`com.adobe.repository.infomodel.bean.ResourceCollection`对象。

   使用`setDescription`方法设置文件夹的描述，并传入以下参数：

   * 描述资源集合的`String`。 在此示例中，`"test Folder"`被使用`.`

1. 将文件夹写入存储库

   调用`ResourceRepositoryClient`对象的`writeResource`方法并传入文件夹的URI和`ResourceCollection`对象。 例如，文件夹的URI可以是以下值`/Applications/FormsApplication/1.0/`。

   该方法返回新创建的`com.adobe.repository.infomodel.bean.Resource`对象的实例。 例如，您可以通过调用`com.adobe.repository.infomodel.bean.Resource`对象的`getId`方法检索新资源的标识符值。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[快速入门(SOAP模式)：使用Java API创建文件夹](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建文件夹 {#create-folders-using-the-web-service-api}

使用存储库服务API（Web服务）创建文件夹：

1. 包含项目文件

   * 使用base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 创建文件夹

   使用`ResourceCollection`类的默认构造函数创建文件夹，并传入以下参数：

   * `Id`对象，通过调用`Id`类的默认构造函数创建并分配给`Resource`对象的`id`字段。
   * `Lid`对象，通过调用`Lid`类的默认构造函数创建并分配给`Resource`对象的`lid`字段。
   * 一个字符串，其中包含分配给`Resource`对象的`name`字段的资源集合名称。 此示例中使用的名称为`"testfolder"`。
   * 一个字符串，其中包含分配给`Resource`对象的`description`字段的资源集合描述。 此示例中使用的描述是`"test folder"`。

1. 将文件夹写入存储库

   调用`RepositoryServiceService`对象的`writeResource`方法并传入以下参数：

   * 要创建文件夹的路径。
   * 表示文件夹的`ResourceCollection`对象。
   * 为其他两个参数传递`null`。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 写入资源 {#writing-resources}

您可以在存储库中的给定位置创建资源。 自然文件大小受数据库限制和会话超时的影响。 对于默认配置，文件限制为25 MB。 要提高或降低最大文件大小，必须更改数据库配置。

写入资源相当于将数据存储在存储库中。 将资源写入存储库后，存储库生态系统中的所有客户端都可以访问该资源。 将资源（如XML架构、XDP文件和XSD文件）写入存储库时，会根据MIME类型解析内容。 如果支持MIME类型，则解析器确定是否存在与其他内容的隐含关系。 例如，如果层叠样式表(CSS)具有引用公共CSS的相对URL，则您还应将公共CSS提交到存储库中。 这两个资源之间的关系作为待定关系存储30天的不可调整周期。 在30天期限内将公共CSS提交到存储库时，即会形成关系。

创建资源时，访问控制列表(ACL)继承自父文件夹。 在创建初始资源或文件夹之前，根文件夹具有系统级别的权限，此时资源或文件夹将获得默认ACL权限。

您可以使用存储库服务Java API或Web服务API以编程方式编写资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要编写资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 读取资源。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**为资源指定目标文件夹的URI**

创建包含要读取的资源URI的字符串。 语法包含正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**创建资源**

调用存储库服务方法以创建资源，并使用标识信息（包括资源的UUID、资源名称和说明）填充资源。

**指定资源内容**

调用存储库服务方法以创建资源内容，并将该内容存储在资源中。

**将资源写入目标文件夹**

调用存储库服务方法来写入资源，指定目标文件夹的URI。

**另请参阅**

[使用Java API编写资源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服务API编写资源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API编写资源 {#write-resources-using-the-java-api}

使用存储库服务API (Java)编写资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 URI存储为`java.lang.String`对象。

1. 创建资源

   要创建资源，必须首先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`RepositoryInfomodelFactoryBean`对象的`newResource`方法，这将创建一个`com.adobe.repository.infomodel.bean.Resource`对象。 在此示例中，提供了以下参数：

   * 通过调用`Id`类的默认构造函数创建的`com.adobe.repository.infomodel.Id`对象。
   * 通过调用`Lid`类的默认构造函数创建的`com.adobe.repository.infomodel.Lid`对象。
   * 包含资源文件名的`java.lang.String`。

   要指定资源的描述，请调用`Resource`对象的`setDescription`方法，并传递包含描述的字符串。 在此示例中，描述为`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`RepositoryInfomodelFactoryBean`对象的`newResourceContent`方法，该方法返回`com.adobe.repository.infomodel.bean.ResourceContent`对象。 将内容添加到`ResourceContent`对象。 在本例中，可通过执行以下任务来实现这一点：

   * 正在调用`ResourceContent`对象的`setDataDocument`方法并传入`com.adobe.idp.Document`对象
   * 正在调用`ResourceContent`对象的`setSize`方法并传入`Document`对象的大小（以字节为单位）

   通过调用`Resource`对象的`setContent`方法并在`ResourceContent`对象中传递来将内容添加到资源。 有关详细信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 将资源写入目标文件夹

   调用`ResourceRepositoryClient`对象的`writeResource`方法并传入文件夹的URI和`Resource`对象。

**另请参阅**

[写入资源](aem-forms-repository.md#writing-resources)

[快速入门(SOAP模式)：使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API编写资源 {#write-resources-using-the-web-service-api}

使用存储库服务API（Web服务）编写资源：

1. 包含项目文件

   * 使用base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 使用与Microsoft .NET Framework兼容的语言时（例如，C#），请将URI存储在`System.String`对象中。

1. 创建资源

   要创建资源，请调用`Resource`类的默认构造函数。 在此示例中，以下信息存储在`Resource`对象中：

   * `com.adobe.repository.infomodel.Id`对象，通过调用`Id`类的默认构造函数创建并分配给`Resource`对象的`id`字段。
   * `com.adobe.repository.infomodel.Lid`对象，通过调用`Lid`类的默认构造函数创建并分配给`Resource`对象的`lid`字段。
   * 一个字符串，其中包含分配给`Resource`对象的`name`字段的资源文件名。 此示例中使用的名称为`"testResource"`。
   * 一个字符串，其中包含分配给`Resource`对象的`description`字段的资源描述。 此示例中使用的描述是`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`ResourceContent`类的默认构造函数。 然后将内容添加到`ResourceContent`对象。 在本例中，可通过执行以下任务来实现这一点：

   * 正在将包含文档的`BLOB`对象分配给`ResourceContent`对象的`dataDocument`字段。
   * 正在将`BLOB`对象的大小以字节为单位，分配给`ResourceContent`对象的`size`字段。

   通过将`ResourceContent`对象分配到`Resource`对象的`content`字段，将内容添加到资源。

1. 将资源写入目标文件夹

   调用`RepositoryServiceService`对象的`writeResource`方法并传入文件夹的URI和`Resource`对象。 为其他两个参数传递`null`。

**另请参阅**

[写入资源](aem-forms-repository.md#writing-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出资源 {#listing-resources}

您可以通过列出资源来发现资源。 对存储库执行查询，以查找与给定资源集合相关的所有资源。

整理资源后，您可以检查通过查看结构的特定分支创建的结构，就像在操作系统中一样。

列出资源按关系运行：资源是文件夹的成员。 成员资格由“成员”类型的关系表示。 在给定文件夹中列出资源时，将查询与关系“member of”的给定文件夹相关的资源。 关系是方向性的：关系的成员具有作为目标成员的源。 源是资源；目标是父文件夹。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要列出资源，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 指定文件夹路径。
1. 检索资源列表。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式创建资源集合。 这是通过创建服务客户端来实现的。

**指定文件夹路径**

创建一个字符串，其中包含包含资源的文件夹的路径。 语法包含正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**检索资源列表**

调用存储库服务方法以检索资源列表，指定目标文件夹的路径。

**另请参阅**

[使用Java API列出资源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用Web服务API列出资源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出资源 {#list-resources-using-the-java-api}

使用存储库服务API (Java)列出资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定文件夹路径

   指定要查询的资源集合的URI。 在这种情况下，其URI为`"/testFolder"`。 URI存储为`java.lang.String`对象。

1. 检索资源列表

   调用`ResourceRepositoryClient`对象的`listMembers`方法并传入文件夹的URI。

   此方法返回一个`java.util.List`对象（共`com.adobe.repository.infomodel.bean.Resource`个），这些对象是类型为`Relation.TYPE_MEMBER_OF`的`com.adobe.repository.infomodel.bean.Relation`的源，并且以资源集合URI作为目标。 您可以通过此`List`进行迭代以检索每个资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[正在列出资源](aem-forms-repository.md#listing-resources)。

[快速入门(SOAP模式)：使用Java API列出资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API列出资源 {#list-resources-using-the-web-service-api}

使用存储库服务API（Web服务）列出资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定文件夹路径

   指定包含要查询的文件夹URI的字符串。 在这种情况下，其URI为`"/testFolder"`。 使用与Microsoft .NET Framework兼容的语言时（例如，C#），请将URI存储在`System.String`对象中。

1. 检索资源列表

   调用`RepositoryServiceService`对象的`listMembers`方法，并将文件夹的URI作为第一个参数传递。 为其他两个参数传递`null`。

   该方法返回可转换为`Resource`对象的对象数组。 您可以循环遍历对象数组以检索每个相关资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[正在列出资源](aem-forms-repository.md#listing-resources)。

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 正在读取资源 {#reading-resources}

您可以从存储库中的给定位置检索资源以读取其内容和元数据。 工作流由初始化表单作为前端。 该流程具有读取表单所需的所有权限。 系统检索数据表单并从存储库中读取内容。 存储库授予对内容和元数据的访问权限（甚至能够知道资源存在）。

存储库具有以下四种权限类型：

* **遍历**：允许您列出资源；即读取资源元数据，但不读取资源内容
* **读取**：允许您读取资源内容
* **写入**：允许您写入资源内容
* **管理访问控制列表(ACL)**：允许您处理资源上的ACL

用户只有在拥有运行进程的权限时，才能运行进程。 IDE用户需要遍历和读取权限才能与存储库同步。 ACL仅在设计时应用，因为运行时发生在系统上下文中。

您可以使用存储库服务Java API或Web服务API以编程方式读取资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要读取资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 读取资源。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**指定要读取的资源的URI**

创建包含要读取的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**读取资源**

调用存储库服务方法以读取资源，指定URI。

**另请参阅**

[使用Java API读取资源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服务API读取资源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API读取资源 {#read-resources-using-the-java-api}

使用存储库服务API (Java)读取资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要读取的资源的URI

   指定一个字符串值，该值表示要检索的资源的URI。 例如，假定名为&#x200B;*testResource*&#x200B;的资源位于名为&#x200B;*testFolder*&#x200B;的文件夹中，请指定`/testFolder/testResource`。

1. 读取资源

   调用`ResourceRepositoryClient`对象的`readResource`方法，并将资源的URI作为参数传递。 此方法返回表示资源的`Resource`实例。

**另请参阅**

[正在读取资源](aem-forms-repository.md#reading-resources)

[快速入门(SOAP模式)：使用Java API读取资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API读取资源 {#reading-resources-using-the-web-service-api}

使用存储库服务API（Web服务）读取资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。）
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。）

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要读取的资源的URI

   指定包含要检索的资源URI的字符串。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework兼容的语言时（例如，C#），请将URI存储在`System.String`对象中。

1. 读取资源

   调用`RepositoryServiceService`对象的`readResource`方法，并将资源的URI作为第一个参数传递。 为其他两个参数传递`null`。

**另请参阅**

[正在读取资源](aem-forms-repository.md#reading-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新资源 {#updating-resources}

您可以检索和更新存储库中的资源内容。 更新资源时，对这些资源的访问控制在版本之间保持不变。 执行更新时，您可以选择递增主版本。 如果不选择递增主版本，则会自动更新次版本。

更新资源时，会根据指定的资源属性创建新版本。 更新资源时，需要指定两个重要参数：目标URI和包含所有已更新元数据的资源实例。 请务必注意，如果不更改给定属性（例如，名称），则在您传入的实例中仍需要该属性。 解析内容时创建的关系将添加到特定版本，除非另外指定，否则不会转发这些关系。

例如，如果更新XDP文件并且它包含对其他资源的引用，则也会记录这些附加引用。 假设form.xdp版本1.0具有两个外部引用：徽标和样式表，随后您更新了form.xdp，使其现在具有三个引用：徽标、样式表和架构文件。 在更新过程中，存储库会将第三个关系（添加到架构文件）添加到其挂起关系表中。 一旦架构文件出现在存储库中，关系就会自动形成。 但是，如果form.xdp 2.0版不再使用徽标，则form.xdp 2.0版将与徽标无关。

所有更新操作都是原子操作和事务性操作。 例如，如果两个用户读取同一资源，并且都决定将1.0版本更新为2.0版本，则其中一个用户将成功，而其中一个用户将失败，存储库的完整性将得到维护，并且两个用户都将收到一条消息，确认存储库是成功还是失败。 如果事务未提交，则在出现数据库故障时将会回滚，并且会超时或回滚，具体取决于应用程序服务器。

您可以使用存储库服务Java API或Web服务API以编程方式更新资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要更新资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 检索要更新的资源。
1. 更新资源。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**检索要更新的资源**

读取资源。 有关详细信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

**更新资源**

在资源中设置新信息并调用存储库服务方法来更新资源，指定URI、更新的资源以及应如何更新版本信息。

**另请参阅**

[使用Java API更新资源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服务API更新资源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新资源 {#update-resources-using-the-java-api}

使用存储库服务API (Java)更新资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 检索要更新的资源

   指定要检索和读取资源的资源URI。 在此示例中，资源的URI是`"/testFolder/testResource"`。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新描述，请调用`Resource`对象的`setDescription`方法，并将新的描述字符串作为参数传递。

   然后调用`ServiceClientFactory`对象的`updateResource`方法，并传入以下参数：

   * 包含资源URI的`java.lang.String`对象。
   * 包含已更新资源信息的`Resource`对象。
   * 一个`boolean`值，指示是更新主要版本还是次要版本。 在此示例中，传入值`true`以指示主版本将递增。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[快速入门(SOAP模式)：使用Java API更新资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API更新资源 {#update-resources-using-the-web-service-api}

使用存储库API（Web服务）更新资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 检索要更新的资源

   指定要检索的资源的URI并读取该资源。 在此示例中，资源的URI是`"/testFolder/testResource"`。 有关详细信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新描述，请为`Resource`对象的`description`字段分配一个新值。

1. 调用`RepositoryServiceService`对象的`updateResource`方法，并传入以下参数：

   * 包含资源URI的`System.String`对象。
   * 包含已更新资源信息的`Resource`对象。
   * 一个`boolean`值，指示是更新主要版本还是次要版本。 在此示例中，传入值`true`以指示主版本将递增。
   * 对其余两个参数传递`null`。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索资源 {#searching-for-resources}

您可以构建用于搜索存储库中资源（包括历史记录、相关资源和属性）的查询。

您可以检索相关资源以确定表单及其片段之间的依赖关系。 例如，如果您有一个表单，则可以确定它使用的片段或外部资源。 如果您有图像，您还可以找到使用该图像的表单。 您还可以使用基于属性的筛选来搜索相关资源。 例如，您可以搜索使用具有指定名称的图像的所有表单，或查找由具有指定名称的表单使用的任何图像。 您还可以使用资源属性进行搜索。 例如，您可以执行查询以查找其名称以给定字符串开头的所有表单或资源，该字符串可能包含“%”和“_”通配符。 请记住，基于属性的搜索不是基于关系；此类搜索基于您对给定资源具有特定知识的假设。

**查询语句**

*查询*&#x200B;包含一个或多个用条件逻辑联接的语句。 *语句*&#x200B;由左操作数、运算符和右操作数组成。 此外，您还可以指定用于搜索结果的排序顺序。 *排序顺序*&#x200B;包含与SQL `ORDER BY`子句等同的信息，该排序顺序由元素组成，这些元素包含搜索所基于的属性，以及指示要使用升序还是降序的值。

您可以使用存储库服务Java API以编程方式搜索资源。 此时，无法使用Web服务API来搜索资源。

**排序行为**

调用`ResourceRepositoryClient`对象的`searchProperties`方法并指定排序顺序时，未遵循排序顺序。 例如，假设您创建了一个具有三个自定义属性的资源，其中属性名称为`name`、`secondName`和`asecondName`。 接下来，在属性名称上创建排序顺序元素，并将`ascending`值设置为`true`。

然后调用`ResourceRepositoryClient`对象的`searchProperties`方法并按排序顺序传递。 搜索将返回正确的资源，并具有三个属性。 但是，属性不按属性名称排序。 它们按添加顺序返回： `name`、`secondName`和`asecondName`。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要搜索资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定搜索的目标文件夹。
1. 指定搜索中使用的属性。
1. 创建搜索中使用的查询。
1. 为搜索结果创建排序顺序。
1. 搜索资源。
1. 从搜索结果中检索资源。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**指定搜索的目标文件夹**

创建一个字符串，其中包含进行搜索的基本路径。 语法包含正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**指定搜索中使用的属性**

您可以根据资源中包含的属性进行搜索。 指定要执行搜索的属性的值。

**创建搜索中使用的查询**

使用语句和条件构造查询。 每个语句将指定搜索所基于的属性、要使用的条件以及要在搜索中使用的属性值。

**为搜索结果创建排序顺序**

排序顺序由元素组成，每个元素包含搜索中使用的属性之一，以及指示使用升序还是降序的值。

**搜索资源**

使用文件夹、查询和排序顺序搜索资源。 此外，指示搜索的深度以及要返回的结果数量的上限。

**从搜索结果中检索资源**

对返回的资源列表进行迭代，并提取信息以供进一步处理。

**另请参阅**

[使用Java API搜索资源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜索资源 {#search-for-resources-using-the-java-api}

使用存储库服务API (Java)搜索资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定搜索的目标文件夹

   指定要从中执行搜索的基本路径的URI。 在此示例中，资源的URI是`/testFolder`。

1. 指定搜索中使用的属性

   指定要执行搜索的属性的值。 属性存在于`com.adobe.repository.infomodel.bean.Resource`对象中。 在此示例中，将对name属性执行搜索；因此，使用了包含`Resource`对象名称的`java.lang.String`，在本例中为`testResource`。

1. 创建搜索中使用的查询

   要创建查询，请通过调用`Query`类的默认构造函数创建一个`com.adobe.repository.query.Query`对象，并将语句添加到查询中。

   要创建语句，请调用`com.adobe.repository.query.Query.Statement`类的构造函数，并传入以下参数：

   * 包含资源属性常量的左操作数。 在此示例中，由于资源的名称用作搜索的基础，因此使用静态值`Resource.ATTRIBUTE_NAME`。
   * 包含搜索属性时使用的条件的运算符。 运算符必须是`Query.Statement`类中的静态常量之一。 在此示例中，使用了静态值`Query.Statement.OPERATOR_BEGINS_WITH`。
   * 包含进行搜索的属性值的右操作数。 在此示例中，使用了name属性（包含值`"testResource"`的`String`）。

   通过调用`Query.Statement`对象的`setNamespace`方法并传递`com.adobe.repository.infomodel.bean.ResourceProperty`类中包含的某个静态值来指定左操作数的命名空间。 在此示例中，使用 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   通过调用`Query`对象的`addStatement`方法并传入`Query.Statement`对象，将每个语句添加到查询中。

1. 为搜索结果创建排序顺序

   要指定搜索结果中使用的排序顺序，请通过调用`SortOrder`类的默认构造函数创建`com.adobe.repository.query.sort.SortOrder`对象，并将元素添加到排序顺序中。

   要为排序顺序创建元素，请为`com.adobe.repository.query.sort.SortOrder.Element`类调用一个构造函数。 在此示例中，由于资源的名称用作搜索的基础，因此静态值`Resource.ATTRIBUTE_NAME`用作第一个参数，而升序（`true`的`boolean`值）指定为第二个参数。

   通过调用`SortOrder`对象的`addSortElement`方法并传入`SortOrder.Element`对象，将每个元素添加到排序顺序中。

1. 搜索资源

   要基于属性属性搜索`resources`，请调用`ResourceRepositoryClient`对象的`searchProperties`方法，并传入以下参数：

   * 包含从中执行搜索的基本路径的`String`。 在这种情况下，使用`"/testFolder"`。
   * 搜索中使用的查询。
   * 搜索的深度。 在这种情况下，`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`用于指示要使用基本路径及其所有文件夹。
   * 一个`int`值，表示从中选择未分页结果集的第一行。 在此示例中，指定了`0`。
   * `int`值，表示返回的最大结果数。 在此示例中，指定了`10`。
   * 搜索中使用的排序顺序。

   该方法按指定的排序顺序返回`java.util.List`个对象（共`Resource`个）。

1. 从搜索结果中检索资源

   要检索搜索结果中包含的资源，请对`List`进行迭代，并将每个对象转换为`Resource`以提取其信息。 在此示例中，将显示每个资源的名称。

**另请参阅**

[搜索资源](aem-forms-repository.md#searching-for-resources)

[快速入门(SOAP模式)：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 创建资源关系 {#creating-resource-relationships}

您可以指定存储库中资源之间的关系。 有三种关系：

* **依赖关系**：资源依赖其他资源的关系，这意味着存储库中需要所有相关资源。
* **成员资格（文件系统）**：资源位于给定文件夹中的关系。
* **自定义**：资源之间指定的关系。 例如，如果一个资源已被弃用，而另一个资源被引入存储库，则您可以指定自己的替换关系。

您可以创建自己的自定义关系。 例如，如果您将HTML文件存储在存储库中并且该文件使用图像，则可以指定自定义关系以将HTML文件与图像相关联（因为通常只有XML文件使用存储库定义的依赖关系与图像相关联）。 另一个自定义关系示例是，如果您想使用循环图结构而不是树结构构建存储库的不同视图。 您可以定义循环图以及查看器来遍历这些关系。 最后，您可以指明一个资源将替换另一个资源，即使这两个资源完全不同。 在这种情况下，您可以在保留范围之外定义关系类型，并在这两个资源之间创建关系。 您的应用程序将是唯一能够检测并处理这种关系的客户，并且可用于对该关系进行搜索。

您可以使用存储库服务Java API或Web服务API以编程方式指定资源之间的关系。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要指定两个资源之间的关系，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要关联的资源的URI。
1. 创建关系。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**指定要关联的资源的URI**

创建包含要关联的资源的URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**创建关系**

调用Repository服务方法来创建和指定关系的类型。

**另请参阅**

[使用Java API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服务API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API创建关系资源 {#create-relationship-resources-using-the-java-api}

使用存储库服务Java API创建关系资源，执行以下任务：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并且位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 URI存储为`java.lang.String`对象。 在本例中，首先向存储库写入资源，然后检索其URI。 有关写入资源的详细信息，请参阅[写入资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`ResourceRepositoryClient`对象的`createRelationship`方法并传入以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型，它是`com.adobe.repository.infomodel.bean.Relation`类中的静态常量之一。 在此示例中，通过指定值`Relation.TYPE_DEPENDANT_OF`来建立依赖关系。
   * 一个`boolean`值，指示目标资源是否自动更新为新head资源的基于`com.adobe.repository.infomodel.Id`的标识符。 在此示例中，由于依赖关系，指定了值`true`。

   您还可以通过调用`ResourceRepositoryClient`对象的`getRelated`方法并传入以下参数来检索给定资源的相关资源列表：

   * 要检索相关资源的资源的URI。 在此示例中，指定了源资源(`"/testFolder/testResource1"`)。
   * 一个`boolean`值，指示指定的资源是否为关系中的源资源。 在此示例中，指定值`true`，因为情况如此。
   * 关系类型，它是`Relation`类中的静态常量之一。 在此示例中，使用先前使用的相同值指定了依赖关系： `Relation.TYPE_DEPENDANT_OF`。

   `getRelated`方法返回`Resource`个对象的`java.util.List`，通过它您可以迭代检索每个相关资源，并在执行此操作时将包含在`List`中的对象转换为`Resource`。 在此示例中，`testResource2`应位于返回的资源的列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[快速入门(SOAP模式)：使用Java API创建资源之间的关系](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建关系资源 {#create-relationship-resources-using-the-web-service-api}

使用存储库API（Web服务）创建关系资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并且位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 使用与Microsoft .NET Framework兼容的语言（例如，C#）时，URI将存储为`System.String`对象。 在本例中，首先向存储库写入资源，然后检索其URI。 有关写入资源的详细信息，请参阅[写入资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`RepositoryServiceService`对象的`createRelationship`方法并传入以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型。 在此示例中，通过指定值`3`来建立依赖关系。
   * 指示是否指定了关系类型的`boolean`值。 在此示例中，指定了值`true`。
   * 一个`boolean`值，指示目标资源是否自动更新为新head资源的基于`Id`的标识符。 在此示例中，由于依赖关系，指定了值`true`。
   * 指示是否指定了目标标头的`boolean`值。 在此示例中，指定了值`true`。
   * 为最后一个参数传递`null`。

   您还可以通过调用`RepositoryServiceService`对象的`getRelated`方法并传入以下参数来检索给定资源的相关资源列表：

   * 要检索相关资源的资源的URI。 在此示例中，指定了源资源(`"/testFolder/testResource1"`)。
   * 一个`boolean`值，指示指定的资源是否为关系中的源资源。 在此示例中，指定值`true`，因为情况如此。
   * 指示是否指定了源资源的`boolean`值。 在此示例中，提供了值`true`。
   * 包含关系类型的整数数组。 在此示例中，使用与之前使用的值相同的数组来指定依赖关系： `3`。
   * 对其余两个参数传递`null`。

   `getRelated`方法返回一个对象数组，这些对象可以转换为`Resource`个对象，您可以通过这些对象进行迭代以检索每个相关资源。 在此示例中，`testResource2`应位于返回的资源的列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 锁定资源 {#locking-resources}

您可以锁定资源或资源集，以供特定用户独占使用，或在多个用户之间共享使用。 共享锁表示资源会发生一些情况，但不会阻止其他任何人对该资源执行操作。 共享锁定应被视为一种信令机制。 独占锁意味着锁定资源的用户将要更改资源，并且该锁可确保在用户不再需要访问资源并已释放该锁之前，其他人都无法执行此操作。 如果存储库管理员解锁资源，则该资源上的所有独占和共享锁定将被自动删除。 此类操作适用于用户不再可用并且未解锁资源的情况。

锁定资源后，当您在Workbench中查看“资源”选项卡时，会出现一个锁定图标，如下图所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存储库服务Java API或Web服务API以编程方式控制对资源的访问。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要锁定和解锁资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要锁定的资源的URI。
1. 锁定资源。
1. 检索资源的锁定。
1. 解锁资源

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**指定要锁定的资源的URI**

创建包含要锁定的资源的URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**锁定资源**

调用存储库服务方法以锁定资源，指定URI、锁定类型和锁定深度。

**检索资源的锁定**

调用Repository服务方法以检索资源的锁，指定URI。

**解锁资源**

调用存储库服务方法以解锁资源，指定URI。

**另请参阅**

[使用Java API锁定资源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服务API锁定资源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API锁定资源 {#lock-resources-using-the-java-api}

使用存储库服务API (Java)锁定资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要锁定的资源的URI

   指定要锁定的资源的URI。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResource"`。 URI存储为`java.lang.String`对象。

1. 锁定资源

   调用`ResourceRepositoryClient`对象的`lockResource`方法并传入以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以便独占使用，因此锁定范围指定为`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 锁定深度。 在本例中，由于锁定将仅应用于特定资源而不应用于其任何成员或子级，因此锁定深度指定为`Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >需要四个参数的`lockResource`方法的重载版本引发异常。 请确保使用需要三个参数的`lockResource`方法，如本演练中所示。

1. 检索资源的锁定

   调用`ResourceRepositoryClient`对象的`getLocks`方法，并将资源的URI作为参数传递。 该方法会返回一个Lock对象列表，您可以通过该列表进行迭代。 在此示例中，通过分别调用每个锁定对象的`getOwnerUserId`、`getDepth`和`getType`方法，为每个对象打印锁定所有者、深度和范围。

1. 解锁资源

   调用`ResourceRepositoryClient`对象的`unlockResource`方法，并将资源的URI作为参数传递。 有关详细信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[快速入门(SOAP模式)：使用Java API锁定资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API锁定资源 {#lock-resources-using-the-web-service-api}

使用存储库服务API（Web服务）锁定资源：

1. 包含项目文件

   * 使用Base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要锁定的资源的URI

   指定包含要锁定的资源的URI的字符串。 在这种情况下，由于名为`testResource`的资源位于文件夹`testFolder`中，其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework兼容的语言时（例如，C#），请将URI存储在`System.String`对象中。

1. 锁定资源

   调用`RepositoryServiceService`对象的`lockResource`方法并传入以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以便独占使用，因此锁定范围指定为`11`。
   * 锁定深度。 在本例中，由于锁定将仅应用于特定资源而不应用于其任何成员或子级，因此锁定深度指定为`2`。
   * `int`值，指示锁定到期前的秒数。 在此示例中，使用`1000`的值。
   * 为最后一个参数传递`null`。

1. 检索资源的锁定

   调用`RepositoryServiceService`对象的`getLocks`方法并传递资源的URI作为第一个参数，传递第二个参数的`null`。 此方法返回一个包含`Lock`对象的`object`数组，您可以通过该数组对其进行迭代。 在此示例中，通过分别访问每个`Lock`对象的`ownerUserId`、`depth`和`type`字段，为每个对象打印锁定所有者、深度和范围。

1. 解锁资源

   调用`RepositoryServiceService`对象的`unlockResource`方法并传递资源的URI作为第一个参数，传递第二个参数的`null`。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 删除资源 {#deleting-resources}

您可以使用存储库服务Java API(SOAP)以编程方式从存储库中的给定位置删除资源。

删除资源时，删除通常是永久性的，但在某些情况下，ECM存储库可能会根据其历史记录机制存储资源的版本。 因此，在删除资源时，请务必确保不再需要该资源。 删除资源的常见原因包括需要增加数据库中的可用空间。 您可以删除某个版本的资源，但如果要这样做，您必须指定资源标识符，而不是其逻辑标识符(LID)或路径。 如果删除文件夹，则该文件夹中的所有内容（包括子文件夹和资源）都会自动删除。

不会删除相关资源。 例如，如果您有一个使用logo.gif文件的表单，并且您删除了logo.gif，则关系将存储在待处理关系表中。 作为替代方法，对于版本弃用，请将最新版本的对象状态设置为已弃用。

在ECM系统中，删除操作不是事务安全的。 例如，如果您尝试删除100个资源，但第50个资源的操作失败，则将删除前49个实例，但其余实例将不会被删除。 否则，默认行为是回滚（无承诺）。

>[!NOTE]
>
>在将`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`方法与ECM存储库( EMC Documentum Content Server和IBM FileNet P8 Content Manager )结合使用时，如果删除指定资源之一失败，则事务将不会回滚，这意味着无法删除已删除的文件。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要删除资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要删除的资源的URI。
1. 删除资源。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

必须先建立连接并提供凭据，然后才能以编程方式读取资源。 这是通过创建服务客户端来实现的。

**指定要删除的资源的URI**

创建包含要删除的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。 如果要删除的资源是文件夹，则删除操作将递归。

**删除资源**

调用Repository服务方法以删除资源，指定URI。

**另请参阅**

[使用Java API删除资源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服务API删除资源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速启动](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)删除资源 {#delete-resources-using-the-java-api-soap}

使用存储库API (Java)删除资源：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对象的构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为testResourceToBeDeleted的资源位于名为testFolder的文件夹中，其URI为`/testFolder/testResourceToBeDeleted`。 URI存储为`java.lang.String`对象。 在本例中，首先将资源写入存储库，并检索其URI。 有关写入资源的详细信息，请参阅[写入资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`ResourceRepositoryClient`对象的`deleteResource`方法，并将资源的URI作为参数传递。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[快速入门(SOAP模式)：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除资源 {#delete-resources-using-the-web-service-api}

使用存储库API（Web服务）删除资源：

1. 包含项目文件

   * 使用Base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为`testResourceToBeDeleted`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResourceToBeDeleted"`。 在本例中，首先将资源写入存储库，并检索其URI。 有关写入资源的详细信息，请参阅[写入资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`RepositoryServiceService`对象的`deleteResources`方法，并传递包含资源URI的`System.String`数组作为第一个参数。 为第二个参数传递`null`。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
