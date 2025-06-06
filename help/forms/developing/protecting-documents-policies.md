---
title: 使用策略保护文档
description: 使用Document Security服务将机密性设置动态应用于Adobe PDF文档，并保持对文档的控制。 Document Security服务还使用户能够控制收件人如何使用受策略保护的PDF文档。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 0664e8f8-fad4-40e6-871e-24bba642fb4f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# 使用策略保护文档 {#protecting-documents-with-policies}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于Document Security服务**

Document Security服务使用户能够动态地将机密性设置应用于Adobe PDF文档，并保持对文档的控制，无论这些文档的分布范围如何。

Document Security服务通过允许用户保持对收件人如何使用受策略保护的PDF文档的控制，防止信息超出用户可及的范围。 用户可以指定谁可以打开文档，限制他们使用文档的方式，并在文档分发后监视文档。 用户还可以动态控制对受策略保护文档的访问，甚至可以动态撤销对文档的访问。

Document Security服务还可以保护其他文件类型，如Microsoft Word文件（DOC文件）。 您可以使用Document Security客户端API处理这些文件类型。 支持以下版本：

* Microsoft Office 2003文件（DOC、XLS、PPT文件）
* Microsoft Office 2007文件（DOCX、XLSX、PPTX文件）
* PTC Pro/E文件

为清楚起见，以下两个部分讨论了如何使用Word文档：

* [将策略应用到Word文档](protecting-documents-policies.md#applying-policies-to-word-documents)
* [从Word文档中删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服务完成以下任务：

* 创建策略。 有关信息，请参阅[创建策略](protecting-documents-policies.md#creating-policies)。
* 修改策略。 有关信息，请参阅[修改策略](protecting-documents-policies.md#modifying-policies)。
* 删除策略。 有关信息，请参阅[删除策略](protecting-documents-policies.md#deleting-policies)。
* 将策略应用到PDF文档。 有关信息，请参阅[将策略应用到PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 从PDF文档中删除策略。 有关信息，请参阅[从PDF文档中删除策略](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* 检查受策略保护的文档。 有关信息，请参阅[检查受策略保护的PDF文档](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤销对PDF文档的访问权限。 有关信息，请参阅[撤销对文档的访问权限](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢复对已撤消文档的访问。 有关信息，请参阅[恢复对已撤消文档的访问](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 创建水印。 有关信息，请参阅[创建水印](protecting-documents-policies.md#creating-watermarks)。
* 搜索事件。 有关信息，请参阅[搜索事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建策略 {#creating-policies}

您可以使用Document Security Java API或Web服务API以编程方式创建策略。 *策略*&#x200B;是包含文档安全设置、授权用户和使用权限的信息集合。 您可以使用适用于不同情况和用户的安全设置创建和保存任意数量的策略。

通过策略，您可以执行以下任务：

* 指定可以打开文档的个人。 收件人可以属于组织，也可以是组织的外部成员。
* 指定收件人可以如何使用文档。 您可以限制对其他Acrobat和Adobe Reader功能的访问。 这些功能包括打印和复制文本、添加签名以及向文档添加注释的功能。
* 随时更改访问和安全设置，即使在分发受策略保护的文档之后也是如此。
* 在分发文档后监视文档的使用。 您可以查看文档的使用方式以及谁在使用它。 例如，您可以查找某人何时打开了文档。

### 使用Web服务创建策略 {#creating-a-policy-using-web-services}

使用Web服务API创建策略时，请引用描述策略的现有可移植文档权限语言(PDRL) XML文件。 策略权限和主体在PDRL文档中定义。 以下XML文档是一个PDRL文档示例。

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建策略，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 设置策略的属性。
1. 创建策略条目。
1. 注册策略。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-rightsmanagement-client.jar
* namespace.jar(如果AEM Forms部署在JBoss上)
* jaxb-api.jar(如果AEM Forms部署在JBoss上)
* jaxb-impl.jar(如果AEM Forms部署在JBoss上)
* jaxb-libs.jar(如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar(如果AEM Forms部署在JBoss上)
* relaxngDatatype.jar(如果AEM Forms部署在JBoss上)
* xsdlib.jar(如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(如果未在JBoss上部署AEM Forms，请使用其他JAR文件)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Document Security客户端API对象**

在以编程方式执行Document Security服务操作之前，请先创建Document Security服务客户端对象。

**设置策略的属性**

要创建策略，请设置策略属性。 必需的属性是策略名称。 每个策略集的策略名称必须是唯一的。 策略集只是策略的集合。 如果策略属于不同的策略集，则可能存在两个同名策略。 但是，单个策略集中的两个策略不能具有相同的策略名称。

要设置的另一个有用属性是有效期。 有效期是指受策略保护的文档可供授权收件人访问的时间段。 如果不设置此属性，则策略始终有效。

可以将有效期设置为以下选项之一：

* 从文档发布之时起文档可访问的一组天数
* 结束日期后，无法访问文档
* 文档可访问的特定日期范围
* 始终有效

您可以仅指定开始日期，这样策略就会在开始日期之后生效。 如果只指定结束日期，则该策略在结束日期之前有效。 但是，如果未定义开始日期和结束日期，则会引发异常。

在设置属于策略的属性时，您还可以设置加密设置。 将策略应用到文档时，这些加密设置将生效。 可以指定以下加密值：

* **AES256**：表示使用256位密钥的AES加密算法。
* **AES128**：表示使用128位密钥的AES加密算法。
* **NoEncryption：**&#x200B;表示不加密。

指定`NoEncryption`选项时，不能将`PlaintextMetadata`选项设置为`false`。 如果尝试这样做，则会引发异常。

>[!NOTE]
>
>有关您可以设置的其他属性的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`接口描述。

**创建策略条目**

策略条目将承担者（组和用户）和权限附加到策略。 策略必须至少有一个策略条目。 例如，假设您执行以下任务：

* 创建并注册一个策略条目，该策略条目允许组仅查看联机文档，并禁止收件人复制文档。
* 将策略条目附加到策略。
* 使用Acrobat使用策略保护文档。

这些操作会导致收件人仅能够在线查看文档，而无法复制文档。 除非从文档中删除安全性，否则文档将保持安全。

**注册策略**

必须先注册新策略，然后才能使用它。 注册策略后，可以使用它来保护文档。

### 使用Java API创建策略 {#create-a-policy-using-the-java-api}

使用Document Security API (Java)创建策略：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 设置策略的属性。

   * 通过调用`InfomodelObjectFactory`对象的静态`createPolicy`方法创建`Policy`对象。 此方法返回`Policy`对象。
   * 通过调用`Policy`对象的`setName`方法并传递指定策略名称的字符串值来设置策略的name特性。
   * 通过调用`Policy`对象的`setDescription`方法并传递指定策略说明的字符串值来设置策略的说明。
   * 通过调用`Policy`对象的`setPolicySetName`方法并传递指定策略集名称的字符串值，指定新策略所属的策略集。 （您可以为此参数值指定`null`，这将导致策略被添加到&#x200B;*我的策略*&#x200B;策略集。）
   * 通过调用`InfomodelObjectFactory`对象的静态`createValidityPeriod`方法创建策略的有效期。 此方法返回`ValidityPeriod`对象。
   * 通过调用`ValidityPeriod`对象的`setRelativeExpirationDays`方法并传递指定天数的整数值，设置受策略保护文档可访问的天数。
   * 通过调用`Policy`对象的`setValidityPeriod`方法并传递`ValidityPeriod`对象来设置策略的有效期。

1. 创建策略条目。

   * 通过调用`InfomodelObjectFactory`对象的静态`createPolicyEntry`方法创建策略条目。 此方法返回`PolicyEntry`对象。
   * 通过调用`InfomodelObjectFactory`对象的静态`createPermission`方法指定策略的权限。 传递属于表示权限的`Permission`接口的静态数据成员。 此方法返回`Permission`对象。 例如，要添加允许用户从受策略保护的PDF文档复制数据的权限，请传递`Permission.COPY`。 （对要添加的每个权限重复此步骤）。
   * 通过调用`PolicyEntry`对象的`addPermission`方法并传递`Permission`对象，向策略条目添加权限。 （对创建的每个`Permission`对象重复此步骤）。
   * 通过调用`InfomodelObjectFactory`对象的静态`createSpecialPrincipal`方法创建策略主体。 传递属于表示主体的`InfomodelObjectFactory`对象的数据成员。 此方法返回`Principal`对象。 例如，若要将文档的发布者添加为主体，请传递`InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 通过调用`PolicyEntry`对象的`setPrincipal`方法并传递`Principal`对象，将主体添加到策略条目。
   * 通过调用`Policy`对象的`addPolicyEntry`方法并传递`PolicyEntry`对象，将策略条目添加到策略中。

1. 注册策略。

   * 通过调用`DocumentSecurityClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`registerPolicy`方法并传递以下值来注册策略：

      * 表示要注册的策略的`Policy`对象。

   * 一个字符串值，表示策略所属的策略集。

   如果在连接设置中使用AEM表单管理员帐户创建`DocumentSecurityClient`对象，则在调用`registerPolicy`方法时指定策略集名称。 如果您为策略集传递了`null`值，则会在管理员&#x200B;*我的策略*&#x200B;策略集中创建该策略。

   如果在连接设置中使用Document Security用户，则可以调用仅接受策略的重载`registerPolicy`方法。 也就是说，您无需指定策略集名称。 但是，该策略已添加到名为&#x200B;*我的策略*&#x200B;的策略集。 如果不想将新策略添加到此策略集，请在调用`registerPolicy`方法时指定策略集名称。

   >[!NOTE]
   >
   >创建策略时，引用现有策略集。 如果指定的策略集不存在，则会引发异常。

有关使用Document Security服务的代码示例，请参阅以下内容：

* “快速入门(SOAP模式)：使用Java API创建策略”

### 使用Web服务API创建策略 {#create-a-policy-using-the-web-service-api}

使用Document Security API（Web服务）创建策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 设置策略的属性。

   * 使用构造函数创建`PolicySpec`对象。
   * 通过为`PolicySpec`对象的`name`数据成员分配字符串值来设置策略的名称。
   * 通过为`PolicySpec`对象的`description`数据成员分配字符串值来设置策略的描述。
   * 通过为`PolicySpec`对象的`policySetName`数据成员分配字符串值，指定策略所属的策略集。 指定现有策略集名称。 （您可以为此参数值指定`null`，这将导致策略被添加到&#x200B;*我的策略*。）
   * 通过为`PolicySpec`对象的`offlineLeasePeriod`数据成员分配整数值，设置策略的脱机租赁期。
   * 使用表示PDRL XML数据的字符串值设置`PolicySpec`对象的`policyXml`数据成员。 要执行此任务，请使用它的构造函数创建一个.NET `StreamReader`对象。 将表示策略的PDRL XML文件的位置传递给`StreamReader`构造函数。 接下来，调用`StreamReader`对象的`ReadLine`方法，并将返回值分配给字符串变量。 循环访问`StreamReader`对象，直到`ReadLine`方法返回null。 将字符串变量分配给`PolicySpec`对象的`policyXml`数据成员。

1. 创建策略条目。

   使用Document Security Web服务API创建策略时，不必创建策略条目。 策略条目在PDRL文档中定义。

1. 注册策略。

   通过调用`DocumentSecurityServiceClient`对象的`registerPolicy`方法并传递以下值来注册策略：

   * 表示要注册的策略的`PolicySpec`对象。
   * 一个字符串值，表示策略所属的策略集。 您可以指定一个`null`值，该值会导致将策略添加到&#x200B;*MyPolices*&#x200B;策略集。

   如果在连接设置中使用AEM表单管理员帐户创建`DocumentSecurityClient`对象，请在调用`registerPolicy`方法时指定策略集名称。

   如果在连接设置中使用Document SecurityDocument Security用户，则可以调用仅接受策略的重载`registerPolicy`方法。 也就是说，您无需指定策略集名称。 但是，该策略已添加到名为&#x200B;*我的策略*&#x200B;的策略集。 如果不想将新策略添加到此策略集，请在调用`registerPolicy`方法时指定策略集名称。

   >[!NOTE]
   >
   >在创建策略并指定策略集时，请确保指定现有的策略集。 如果指定的策略集不存在，则会引发异常。

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API创建策略”
* “快速入门(SwaRef)：使用Web服务API创建策略”

## 修改策略 {#modifying-policies}

您可以使用Document Security Java API或Web服务API修改现有策略。 要更改现有策略，您需要检索并修改现有策略，然后在服务器上更新策略。 例如，假设您检索现有策略并延长其有效期。 在更改生效之前，必须更新策略。

当业务需求发生变化且策略不再反映这些需求时，您可以修改策略。 您可以简单地更新现有策略，而不是创建策略。

要使用Web服务（例如，使用通过JAX-WS创建的Java代理类）修改策略属性，必须确保在Document Security服务中注册该策略。 然后，您可以使用`PolicySpec.getPolicyXml`方法引用现有策略，并使用适用的方法修改策略属性。 例如，您可以通过调用`PolicySpec.setOfflineLeasePeriod`方法来修改离线租赁期。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要修改现有策略，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索现有策略。
1. 更改策略属性。
1. 更新策略。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。 如果您使用的是Java API，请创建一个`RightsManagementClient`对象。 如果您使用的是Document Security Web服务API，请创建`RightsManagementServiceService`对象。

**检索现有策略**

检索现有策略以对其进行修改。 要检索策略，请指定策略名称和策略所属的策略集。 如果为策略集名称指定了`null`值，则从&#x200B;*我的策略*&#x200B;策略集中检索该策略。

**设置策略的属性**

要修改策略，请修改策略属性的值。 唯一不能更改的策略属性是name属性。 例如，要更改策略的脱机租赁期，您可以修改策略的脱机租赁期属性的值。

使用Web服务修改策略的脱机租赁期时，`PolicySpec`界面上的`offlineLeasePeriod`字段被忽略。 要更新脱机租赁期，请修改PDRL XML文档中的`OfflineLeasePeriod`元素。 然后使用`PolicySpec`接口的`policyXML`数据成员引用更新的PDRL XML文档。

>[!NOTE]
>
>有关您可以设置的其他属性的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`接口描述。

**更新策略**

在对策略所做的更改生效之前，您必须使用Document Security服务更新策略。 对保护文档的策略的更改在下次与Document Security服务同步时更新。

### 使用Java API修改现有策略 {#modify-existing-policies-using-the-java-api}

使用Document Security API (Java)修改现有策略：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 检索现有策略。

   * 通过调用`RightsManagementClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`getPolicy`方法并传递以下值，创建表示要更新的策略的`Policy`对象

      * 一个字符串值，表示策略所属的策略集名称。 您可以指定导致使用`MyPolicies`策略集的`null`。
      * 表示策略名称的字符串值。

1. 设置策略的属性。

   更改策略的属性以满足您的业务要求。 例如，要更改策略的脱机租赁期，请调用`Policy`对象的`setOfflineLeasePeriod`方法。

1. 更新策略。

   通过调用`PolicyManager`对象的`updatePolicy`方法更新策略。 传递表示要更新的策略的`Policy`对象。

**代码示例**

有关使用Document Security服务的代码示例，请参阅快速入门(SOAP模式)：使用Java API修改策略部分。

### 使用Web服务API修改现有策略 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API（Web服务）修改现有策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索现有策略。

   通过调用`RightsManagementServiceClient`对象的`getPolicy`方法并传递以下值，创建表示要修改的策略的`PolicySpec`对象：

   * 一个字符串值，它指定策略所属的策略集名称。 您可以指定导致使用`MyPolicies`策略集的`null`。
   * 一个字符串值，它指定策略的名称。

1. 设置策略的属性。

   更改策略的属性以满足您的业务要求。

1. 更新策略。

   通过调用`RightsManagementServiceClient`对象的`updatePolicyFromSDK`方法并传递表示要更新的策略的`PolicySpec`对象来更新策略。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API修改策略”
* “快速入门(SwaRef)：使用Web服务API修改策略”

## 删除策略 {#deleting-policies}

您可以使用Document Security Java API或Web服务API删除现有策略。 删除策略后，无法再用它来保护文档。 但是，使用该策略的现有受策略保护的文档仍受保护。 您可以在较新的策略可用时删除策略。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要删除现有策略，请执行以下步骤：

1. 包含项目文件
1. 创建Document Security客户端API对象。
1. 删除策略。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。 如果您使用的是Java API，请创建一个`RightsManagementClient`对象。 如果您使用的是Document Security Web服务API，请创建`RightsManagementServiceService`对象。

**删除策略**

要删除策略，请指定要删除的策略以及该策略所属的策略集。 其设置用于调用AEM Forms的用户必须具有删除该策略的权限；否则会发生异常。 同样，如果尝试删除不存在的策略，则会发生异常。

### 使用Java API删除策略 {#delete-policies-using-the-java-api}

使用Document Security API (Java)删除策略：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 删除策略。

   * 通过调用`RightsManagementClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`deletePolicy`方法并传递以下值来删除策略：

      * 一个字符串值，它指定策略所属的策略集名称。 您可以指定导致使用`MyPolicies`策略集的`null`。
      * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API删除策略”

### 使用Web服务API删除策略 {#delete-policies-using-the-web-service-api}

使用Document Security API（Web服务）删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 删除策略。

   通过调用`RightsManagementServiceClient`对象的`deletePolicy`方法并传递以下值来删除策略：

   * 一个字符串值，它指定策略所属的策略集名称。 您可以指定导致使用`MyPolicies`策略集的`null`。
   * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API删除策略”
* “快速入门(SwaRef)：使用Web服务API删除策略”

## 将策略应用到PDF文档 {#applying-policies-to-pdf-documents}

您可以将策略应用到PDF文档以保护文档。 通过将策略应用于PDF文档，您可以限制对文档的访问。 如果文档已受策略保护，则无法将策略应用到该文档。

在文档打开时，您还可以限制对Acrobat和Adobe Reader功能的访问，包括打印和复制文本、进行更改以及向文档添加签名和注释的功能。 此外，当您不再希望用户访问受策略保护的PDF文档时，也可以撤销该文档。

您可以在分发受策略保护的文档后监视其使用情况。 也就是说，您可以看到文档的使用方式以及谁在使用它。 例如，您可以查找何时有人打开了文档。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要将策略应用到PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索应用了策略的PDF文档。
1. 将现有策略应用到PDF文档。
1. 保存受策略保护的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

在以编程方式执行Document Security服务操作之前，请先创建Document Security服务客户端对象。 如果您使用的是Java API，请创建一个`DocumentSecurityClient`对象。 如果您使用的是Document Security Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索PDF文档**

您可以检索PDF文档以应用策略。 将策略应用到PDF文档后，使用文档时会限制用户。 例如，如果策略不允许在脱机时打开文档，则用户必须联机才能打开文档。

**将现有策略应用到PDF文档**

要将策略应用到PDF文档，请引用现有策略并指定该策略属于哪个策略集。 设置连接属性的用户必须具有对指定策略的访问权限。 如果不存在，则会发生异常。

**保存PDF文档**

在Document Security服务将策略应用于PDF文档后，您可以将受策略保护的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问权限](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API将策略应用到PDF文档 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API (Java)将策略应用到PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 检索PDF文档。

   * 使用构造函数创建表示PDF文档的`java.io.FileInputStream`对象。 传递一个指定PDF文档位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 将现有策略应用到PDF文档。

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`protectDocument`方法并传递以下值，将策略应用到PDF文档：

      * 包含应用了策略的PDF文档的`com.adobe.idp.Document`对象。
      * 指定文档名称的字符串值。
      * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定导致使用`MyPolicies`策略集的`null`值。
      * 指定策略名称的字符串值。
      * 一个字符串值，表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，并且可以为null（如果此参数为null，则下一个参数值必须为null）。
      * 一个字符串值，表示作为文档发布者的用户管理员用户的规范名称的名称。 此参数值是可选的，可以为`null` （如果此参数为null，则以前的参数值必须为`null`）。
      * 表示用于选择MS Office模板的区域设置的`com.adobe.livecycle.rightsmanagement.Locale`。 此参数值是可选的，不用于PDF文档。 要保护PDF文档的安全，请指定`null`。

     `protectDocument`方法返回包含受策略保护的PDF文档的`RMSecureDocumentResult`对象。

1. 保存PDF文档。

   * 调用`RMSecureDocumentResult`对象的`getProtectedDoc`方法以获取受策略保护的PDF文档。 此方法返回`com.adobe.idp.Document`对象。
   * 创建`java.io.File`对象并确保文件扩展名为PDF。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`getProtectedDoc`方法返回的`Document`对象）。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门（EJB模式）：使用Java API将策略应用到PDF文档”
* “快速入门(SOAP模式)：使用Java API将策略应用到PDF文档”

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将策略应用到PDF文档 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API（Web服务）将策略应用到PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储应用了策略的PDF文档。
   * 通过调用其构造函数并传递表示PDF文档文件位置和文件打开模式的字符串值，创建`System.IO.FileStream`对象。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 将现有策略应用到PDF文档。

   通过调用`RightsManagementServiceClient`对象的`protectDocument`方法并传递以下值，将策略应用到PDF文档：

   * 包含应用了策略的PDF文档的`BLOB`对象。
   * 指定文档名称的字符串值。
   * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定导致使用`MyPolicies`策略集的`null`值。
   * 指定策略名称的字符串值。
   * 一个字符串值，表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，并且可以为null（如果此参数为null，则下一个参数值必须为`null`）。
   * 一个字符串值，表示作为文档发布者的用户管理员用户的规范名称的名称。 此参数值是可选的，可以为null（如果此参数为null，则上一个参数值必须为`null`）。
   * 指定区域设置值的`RMLocale`值（例如，`RMLocale.en`）。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数（例如，`application/pdf`）。

   `protectDocument`方法返回包含受策略保护的PDF文档的`BLOB`对象。

1. 保存PDF文档。

   * 通过调用其构造函数并传递代表受策略保护的PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`protectDocument`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API将策略应用到PDF文档”
* “快速入门(SwaRef)：使用Web服务API将策略应用到PDF文档”

## 从PDF文档中删除策略 {#removing-policies-from-pdf-documents}

您可以从受策略保护的文档中删除策略以从文档中删除安全性。 即，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要从受策略保护的PDF文档中删除策略，请执行以下步骤：

1. 包含项目文件
1. 创建Document Security客户端API对象。
1. 检索受策略保护的PDF文档。
1. 从PDF文档中删除策略。
1. 保存不安全的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

在以编程方式执行Document Security服务操作之前，请先创建Document Security服务客户端对象。

**检索受策略保护的PDF文档**

您可以检索受策略保护的PDF文档以删除策略。 如果尝试从不受策略保护的PDF文档中删除策略，则会导致异常。

**从PDF文档中删除策略**

如果您在连接设置中指定了管理员，则可以从受策略保护的PDF文档中删除策略。 如果没有，则用于保护文档的策略必须包含`SWITCH_POLICY`权限，才能从PDF文档中删除策略。 此外，在AEM Forms连接设置中指定的用户还必须具有该权限。 否则，将引发异常。

**保存不安全的PDF文档**

Document Security服务从PDF文档中删除策略后，您可以将不安全的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用到PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API从PDF文档中删除策略 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API (Java)从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 检索受策略保护的PDF文档。

   * 使用受策略保护的PDF文档的构造函数并传递指定PDF文档位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 从PDF文档中删除策略。

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`removeSecurity`方法并传递包含受策略保护的PDF文档的`com.adobe.idp.Document`对象，从PDF文档中删除策略。 此方法返回包含不安全的PDF文档的`com.adobe.idp.Document`对象。

1. 保存不安全的PDF文档。

   * 创建`java.io.File`对象并确保文件扩展名为PDF。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`removeSecurity`方法返回的`Document`对象）。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API从PDF文档中删除策略”

### 使用Web服务API删除策略 {#remove-a-policy-using-the-web-service-api}

使用Document Security API（Web服务）从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索受策略保护的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储受策略保护的PDF文档，策略将从该文档中删除。
   * 通过调用其构造函数并传递表示PDF文档文件位置和文件打开模式的字符串值，创建`System.IO.FileStream`对象。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 从PDF文档中删除策略。

   通过调用`DocumentSecurityServiceClient`对象的`removePolicySecurity`方法并传递包含受策略保护的PDF文档的`BLOB`对象，从PDF文档中删除策略。 此方法返回包含不安全的PDF文档的`BLOB`对象。

1. 保存不安全的PDF文档。

   * 通过调用其构造函数并传递表示不安全PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`removePolicySecurity`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API从PDF文档中删除策略”
* “快速入门(SwaRef)：使用Web服务API从PDF文档中删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤销对文档的访问权限 {#revoking-access-to-documents}

您可以撤销对受策略保护的PDF文档的访问权限，从而导致用户无法访问该文档的所有副本。 当用户尝试打开吊销的PDF文档时，他们被重定向到指定的URL，在那里可以查看修订的文档。 必须以编程方式指定用户重定向到的URL。 当您撤销对文档的访问权限时，更改将在用户下次通过联机打开受策略保护的文档与Document Security服务同步时生效。

撤销文档访问权限的功能提供了附加安全性。 例如，假定文档有较新版本可用，并且您不再希望任何人查看过时的版本。 在此情况下，对旧文档的访问可以撤销，除非恢复访问，否则任何人都无法查看该文档。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要撤销受策略保护的文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索受策略保护的PDF文档。
1. 撤销受策略保护的文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。

**检索受策略保护的PDF文档**

检索受策略保护的PDF文档以撤销它。 您无法撤销已撤销或不是受策略保护文档的文档。

如果您知道受策略保护文档的许可证标识符值，则无需检索受策略保护的PDF文档。 但是，在大多数情况下，必须检索PDF文档以获取许可证标识符值。

**撤销受策略保护的文档**

要撤销受策略保护的文档，请指定受策略保护文档的许可证标识符。 此外，您可以指定用户尝试打开撤消文档时可以查看的文档URL。 也就是说，假定已过期的文档被撤销。 当用户尝试打开撤消的文档时，他们将看到更新的文档而不是撤消的文档。

>[!NOTE]
>
>如果尝试撤销已撤销的文档，则会引发异常。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用到PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢复对已撤消文档的访问](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤销对文档的访问 {#revoke-access-to-documents-using-the-java-api}

通过使用Document Security API (Java)撤销对受策略保护的PDF文档的访问权限：

1. 包含项目文件

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 检索受策略保护的PDF文档

   * 使用受策略保护的PDF文档的构造函数并传递指定PDF文档位置的字符串值，创建表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 撤销受策略保护的文档

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`getLicenseId`方法，检索受策略保护文档的许可证标识符值。 传递表示受策略保护文档的`com.adobe.idp.Document`对象。 此方法返回代表许可证标识符值的字符串值。
   * 通过调用`DocumentSecurityClient`对象的`getLicenseManager`方法创建`LicenseManager`对象。
   * 通过调用`LicenseManager`对象的`revokeLicense`方法并传递以下值来撤销受策略保护的文档：

      * 指定受策略保护文档的许可证标识符值的字符串值（指定`DocumentManager`对象的`getLicenseId`方法的返回值）。
      * `License`接口的静态数据成员，它指定撤销文档的原因。 例如，您可以指定`License.DOCUMENT_REVISED`。
      * 一个`java.net.URL`值，它指定修订文档的位置。 如果您不想将用户重定向到其他URL，则可以传递`null`。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API撤销文档”

### 使用Web服务API撤销对文档的访问 {#revoke-access-to-documents-using-the-web-service-api}

通过使用Document Security API（Web服务）撤销对受策略保护的PDF文档的访问权限：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索受策略保护的PDF文档

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已撤销的受策略保护的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示要撤销的受策略保护的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 撤销受策略保护的文档

   * 通过调用`DocumentSecurityServiceClient`对象的`getLicenseID`方法并传递表示受策略保护文档的`BLOB`对象，检索受策略保护文档的许可证标识符值。 此方法返回代表许可证标识符的字符串值。
   * 通过调用`DocumentSecurityServiceClient`对象的`revokeLicense`方法并传递以下值来撤销受策略保护的文档：

      * 指定受策略保护文档的许可证标识符值的字符串值（指定`DocumentSecurityServiceService`对象的`getLicenseId`方法的返回值）。
      * `Reason`枚举的静态数据成员，它指定撤销文档的原因。 例如，您可以指定`Reason.DOCUMENT_REVISED`。
      * 一个`string`值，它指定修订文档所在的URL位置。 如果您不想将用户重定向到其他URL，则可以传递`null`。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API撤销文档”
* “快速入门(SwaRef)：使用Web服务API撤销文档”

**另请参阅**

[从Word文档中删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢复对已撤消文档的访问 {#reinstating-access-to-revoked-documents}

您可以恢复对已吊销的PDF文档的访问，从而使用户能够访问已吊销文档的所有副本。 当用户打开已撤销的恢复文档时，用户能够查看文档。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要恢复对已撤销PDF文档的访问，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索已吊销PDF文档的许可证标识符。
1. 恢复对已吊销的PDF文档的访问权限。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。 如果您使用的是Java API，请创建一个`DocumentSecurityClient`对象。 如果您使用的是Document Security Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索已吊销的PDF文档的许可证标识符**

检索已吊销PDF文档的许可证标识符以恢复已吊销PDF文档。 获取许可证标识符值后，您可以恢复已撤消的文档。 如果尝试恢复未撤消的文档，则会导致异常。

**恢复对已撤销的PDF文档的访问**

要恢复对已吊销的PDF文档的访问，必须指定已吊销文档的许可证标识符。 如果尝试恢复对未撤消的PDF文档的访问，则会导致出现异常。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用到PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤销对文档的访问权限](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢复对已撤销文档的访问 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用Document Security API (Java)恢复对已撤销文档的访问：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 检索已吊销PDF文档的许可证标识符。

   * 创建一个`java.io.FileInputStream`对象，该对象通过使用其构造函数并传递一个指定PDF文档位置的字符串值，来表示已撤销的PDF文档。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。
   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`getLicenseId`方法并传递表示已撤销文档的`com.adobe.idp.Document`对象，检索已撤销文档的许可证标识符值。 此方法返回代表许可证标识符的字符串值。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过调用`DocumentSecurityClient`对象的`getLicenseManager`方法创建`LicenseManager`对象。
   * 通过调用`LicenseManager`对象的`unrevokeLicense`方法并传递已吊销文档的许可证标识符值，恢复对已吊销的PDF文档的访问。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Web服务API恢复对已吊销文档的访问”

### 使用Web服务API恢复对已撤消文档的访问 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用Document Security API（Web服务）恢复对已撤销文档的访问：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索已吊销PDF文档的许可证标识符。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已撤销的PDF文档，恢复了对该文档的访问权限。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示已吊销PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过调用`DocumentSecurityServiceClient`对象的`getLicenseID`方法并传递表示已撤销文档的`BLOB`对象，检索已撤销文档的许可证标识符值。 此方法返回代表许可证标识符的字符串值。
   * 通过调用`DocumentSecurityServiceClient`对象的`unrevokeLicense`方法并传递指定已吊销PDF文档的许可证标识符值的字符串值（传递`DocumentSecurityServiceClient`对象的`getLicenseId`方法的返回值），恢复对已吊销PDF文档的访问。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API恢复对已吊销文档的访问”
* “快速入门(SwaRef)：使用Web服务API恢复对已吊销文档的访问”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检查受策略保护的PDF文档 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API（Java和Web服务）检查受策略保护的PDF文档。 检查受策略保护的PDF文档会返回有关受策略保护的PDF文档的信息。 例如，您可以确定用于保护文档的策略以及保护文档的日期。

如果您的LiveCycle版本是8.x或早期版本，则无法执行此任务。 AEM Forms中添加了对检查受策略保护文档的支持。 如果尝试使用LiveCycle 8.x（或更早版本）检查受策略保护的文档，则会引发异常。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要检查受策略保护的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索要检查的受策略保护的文档。
1. 获取有关受策略保护文档的信息。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

在以编程方式执行Document Security服务操作之前，请先创建Document Security服务客户端对象。 如果您使用的是Java API，请创建一个`RightsManagementClient`对象。 如果您使用的是Document Security Web服务API，请创建`RightsManagementServiceService`对象。

**检索受策略保护的文档以检查**

要检查受策略保护的文档，请检索它。 如果尝试检查未使用策略保护或撤消的文档，则会引发异常。

**检查文档**

检索受策略保护的文档后，可以检查该文档。

**获取有关受策略保护文档的信息**

检查受策略保护的PDF文档后，您可以获取有关该文档的信息。 例如，您可以确定用于保护文档的策略。

如果您使用属于我的策略的策略保护文档，然后调用`RMInspectResult.getPolicysetName`或`RMInspectResult.getPolicysetId`，则返回null。

如果使用策略集（我的策略除外）中包含的策略对文档进行保护，则`RMInspectResult.getPolicysetName`和`RMInspectResult.getPolicysetId`将返回有效的字符串。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检查受策略保护的PDF文档 {#inspect-policy-protected-pdf-documents-using-the-java-api}

使用Document Security Service API (Java)检查受策略保护的PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。 有关这些文件的位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 检索要检查的受策略保护的文档。

   * 使用受策略保护的PDF文档的构造函数创建一个`java.io.FileInputStream`对象。 传递一个指定PDF文档位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 检查文档。

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`LicenseManager`对象的`inspectDocument`方法来检查受策略保护的文档。 传递包含受策略保护的PDF文档的`com.adobe.idp.Document`对象。 此方法返回包含有关受策略保护文档的信息的`RMInspectResult`对象。

1. 获取有关受策略保护文档的信息。

   要获取有关受策略保护文档的信息，请调用属于`RMInspectResult`对象的相应方法。 例如，要检索策略名称，请调用`RMInspectResult`对象的`getPolicyName`方法。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API检查受策略保护的PDF文档”

### 使用Web服务API检查受策略保护的PDF文档 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

使用Document Security服务API（Web服务）检查受策略保护的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索要检查的受策略保护的文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储要检查的PDF文档。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值表示PDF文档的文件位置以及用于在中打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和流长度以读取。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 检查文档。

   通过调用`RightsManagementServiceClient`对象的`inspectDocument`方法来检查受策略保护的文档。 传递包含受策略保护的PDF文档的`BLOB`对象。 此方法返回包含有关受策略保护文档的信息的`RMInspectResult`对象。

1. 获取有关受策略保护文档的信息。

   要获取有关受策略保护文档的信息，请获取属于`RMInspectResult`对象的相应字段的值。 例如，要检索策略名称，请获取`RMInspectResult`对象的`policyName`字段的值。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API检查受策略保护的PDF文档”
* “快速入门(SwaRef)：使用Web服务API检查受策略保护的PDF文档”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建水印 {#creating-watermarks}

水印通过唯一地标识文档并控制版权侵权，帮助确保文档的安全。 例如，您可以创建并放置一个水印，在文档的所有页面上显示“机密”。 创建水印后，您可以将其包含在策略中。 即，您可以使用新建的水印设置策略的水印属性。 将包含水印的策略应用于文档后，水印将显示在受策略保护的文档中。

>[!NOTE]
>
>只有具有Document Security管理权限的用户才能创建水印。 即，在定义创建Document Security服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要创建水印，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 设置水印属性。
1. 向Document Security服务注册水印。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。 如果您使用的是Java API，请创建一个`RightsManagementClient`对象。 如果您使用的是Document Security Web服务API，请创建`RightsManagementServiceService`对象。

**设置水印属性**

要创建水印，必须设置水印属性。 必须始终定义名称属性。 除了名称属性之外，还必须至少设置以下属性之一：

* 自定义文本
* 包含日期
* UserIdInclude
* UserNameInclude

下表列出了使用Web服务创建水印时所需的键值对。

<table>
 <thead>
  <tr>
   <th><p>键名</p></th>
   <th><p>描述</p></th>
   <th><p>价值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>指定打开文档的用户名是否为水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定打开文档的用户标识是否为水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定当前日期是否为水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值为true，则必须使用<code>WaterBackCmd:SRCTEXT</code>指定自定义文本的值。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定水印的不透明度。 如果未指定，则默认值为0.5。</p></td>
   <td><p>介于0.0-1.0之间的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定水印的旋转。 缺省值为0度。</p></td>
   <td><p>介于0和359之间的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>如果指定此值，则<code>WaterBackCmd:IS_SIZE_ENABLED</code>必须存在并且值必须为true。 如果未指定此属性，则默认行为适合页面。</p></td>
   <td><p>大于0.0且小于或等于1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定水印的水平对齐方式。 默认值为center。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定水印的垂直对齐方式。 默认值为center。</p></td>
   <td><p>顶部、中心或底部</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否为背景。 默认值为false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自定义比例，则为True。 如果此值为true，则还必须指定SCALE。 如果此值为false，则默认值为适合页面。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定水印的自定义文本。 如果此值存在，则<code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code>也必须存在并设置为true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有水印都必须定义以下属性之一：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他属性都是可选的。

**注册水印**

新的水印必须先在Document Security服务中注册，然后才能使用。 注册水印后，您可以在策略中使用该水印。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用到PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API创建水印 {#create-watermarks-using-the-java-api}

使用Document Security API (Java)创建水印：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，如`adobe-rightsmanagement-client.jar`。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 设置水印属性

   * 通过调用`InfomodelObjectFactory`对象的静态`createWatermark`方法创建`Watermark`对象。 此方法返回`Watermark`对象。
   * 通过调用`Watermark`对象的`setName`方法并传递指定策略名称的字符串值来设置水印的名称属性。
   * 通过调用`Watermark`对象的`setBackground`方法并传递`true`来设置水印的背景属性。 通过设置此属性，水印将显示在文档的背景中。
   * 通过调用`Watermark`对象的`setCustomText`方法并传递表示水印文本的字符串值来设置水印的自定义文本属性。
   * 通过调用`Watermark`对象的`setOpacity`方法并传递指定不透明度级别的整数值来设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

1. 注册水印。

   * 通过调用`RightsManagementClient`对象的`getWatermarkManager`方法创建`WatermarkManager`对象。 此方法返回`WatermarkManager`对象。
   * 通过调用`WatermarkManager`对象的`registerWatermark`方法并传递表示水印的`Watermark`对象来注册水印。 此方法返回代表水印标识值的字符串值。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API创建水印”

### 使用Web服务API创建水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API（Web服务）创建水印：

1. 创建Document Security客户端API对象。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 设置水印属性。

   * 通过调用`WatermarkSpec`构造函数创建`WatermarkSpec`对象。
   * 通过为`WatermarkSpec`对象的`name`数据成员分配字符串值来设置水印的名称。
   * 通过为`WatermarkSpec`对象的`id`数据成员分配字符串值来设置水印的`id`属性。
   * 对于要设置的每个水印属性，请创建一个单独的`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`数据成员（例如，`WaterBackCmd:OPACITY)`）分配值来设置键值。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`数据成员（例如，`.25`）分配值来设置值。
   * 创建`MyArrayOf_xsd_anyType`对象。 对于每个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象，调用`MyArrayOf_xsd_anyType`对象的`Add`方法。 传递`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将`MyArrayOf_xsd_anyType`对象分配给`WatermarkSpec`对象的`values`数据成员。

1. 注册水印。

   通过调用`RightsManagementServiceClient`对象的`registerWatermark`方法并传递表示水印的`WatermarkSpec`对象来注册水印。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API创建水印”
* “快速入门(SwaRef)：使用Web服务API创建水印”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改水印 {#modifying-watermarks}

您可以使用Document Security Java API或Web服务API修改现有水印。 要更改现有水印，可以检索它，修改其属性，然后在服务器上更新它。 例如，假设您检索水印并修改其不透明度属性。 在更改生效之前，必须更新水印。

当您修改水印时，此更改将影响对其应用了水印的未来文档。 也就是说，包含水印的现有PDF文档不受影响。

>[!NOTE]
>
>只有具有Document Security管理权限的用户才能修改水印。 即，在定义创建Document Security服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-9}

要修改水印，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索要修改的水印。
1. 设置水印属性。
1. 更新水印。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。 如果您使用的是Java API，请创建一个`DocumentSecurityClient`对象。 如果您使用的是Document Security Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索要修改的水印**

要修改水印，必须检索现有水印。 可以通过指定水印名称或指定其标识符值来检索水印。

**设置水印属性**

要修改现有水印，请更改一个或多个水印属性的值。 使用Web服务以编程方式更新水印时，必须设置最初设置的所有属性，即使值未发生更改也是如此。 例如，假定设置了以下水印属性： `WaterBackCmd:IS_USERID_ENABLED`、`WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、`WaterBackCmd:OPACITY`和`WaterBackCmd:SRCTEXT`。 尽管您要修改的唯一属性是`WaterBackCmd:OPACITY`，但您必须设置其他值。

>[!NOTE]
>
>使用Java API修改水印时，无需指定所有属性。 设置要修改的水印属性。

>[!NOTE]
>
>有关水印属性名称的信息，请参阅[创建水印](protecting-documents-policies.md#creating-watermarks)。

**更新水印**

修改水印的属性后，必须更新水印。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[创建水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改水印 {#modify-watermarks-using-the-java-api}

使用Document Security API (Java)修改水印：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 检索要修改的水印。

   通过调用`DocumentSecurityClient`对象的`getWatermarkManager`方法创建`WatermarkManager`对象，并传递指定水印名称的字符串值。 此方法返回表示要修改的水印的`Watermark`对象。

1. 设置水印属性。

   通过调用`Watermark`对象的`setOpacity`方法并传递指定不透明度级别的整数值来设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此示例仅修改不透明度属性。

1. 更新水印。

   * 通过调用`WatermarkManager`对象的`updateWatermark`方法更新水印，并传递其属性被修改的`Watermark`对象。

**代码示例**

有关使用Document Security服务的代码示例，请参阅快速入门(SOAP模式)：使用Java API修改水印部分。

### 使用Web服务API修改水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API（Web服务）修改水印：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索要修改的水印。

   通过调用`DocumentSecurityServiceClient`对象的`getWatermarkByName`方法检索要修改的水印。 传递一个指定水印名称的字符串值。 此方法返回表示要修改的水印的`WatermarkSpec`对象。

1. 设置水印属性。

   * 对于要更新的每个水印属性，请创建一个单独的`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`数据成员（例如，`WaterBackCmd:OPACITY)`）分配值来设置键值。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`数据成员（例如，`.50`）分配值来设置值。
   * 创建`MyArrayOf_xsd_anyType`对象。 对于每个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象，调用`MyArrayOf_xsd_anyType`对象的`Add`方法。 传递`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将`MyArrayOf_xsd_anyType`对象分配给`WatermarkSpec`对象的`values`数据成员。

1. 更新水印。

   通过调用`DocumentSecurityServiceClient`对象的`updateWatermark`方法并传递表示要修改的水印的`WatermarkSpec`对象来更新水印。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API修改水印”

## 搜索事件 {#searching-for-events}

Rights Management服务会在发生特定操作时对其进行跟踪，例如将策略应用到文档、打开受策略保护的文档以及撤销对文档的访问权限。 必须对Rights Management服务启用事件审核，否则不会跟踪事件。

事件分为以下类别之一：

* 管理员事件是与管理员相关的操作，例如创建管理员帐户。
* 文档事件是与文档相关的操作，例如关闭受策略保护的文档。
* 策略事件是与策略相关的操作，例如创建策略。
* 服务事件是与Rights Management服务相关的操作，例如与用户目录同步。

您可以使用Rights Management Java API或Web服务API搜索指定的事件。 通过搜索事件，您可以执行任务，例如创建特定事件的日志文件。

>[!NOTE]
>
>有关Rights Management服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-10}

要搜索Rights Management事件，请执行以下步骤：

1. 包括项目文件。
1. 创建Rights Management客户端API对象。
1. 指定要搜索的事件。
1. 搜索事件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Rights Management客户端API对象**

您必须先创建Rights Management服务客户端对象，然后才能以编程方式执行Rights Management服务操作。 如果您使用的是Java API，请创建一个`DocumentSecurityClient`对象。 如果您使用的是Rights Management Web服务API，请创建一个`DocumentSecurityServiceService`对象。

**指定要搜索的事件**

指定要搜索的事件。 例如，您可以搜索策略创建事件，该事件将在创建新策略时发生。

**搜索事件**

指定要搜索的事件后，可以使用Rights Management Java API或Rights Management Web服务API来搜索事件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜索事件 {#search-for-events-using-the-java-api}

使用Rights Management API (Java)搜索事件：

1. 包含项目文件

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Rights Management客户端API对象

   使用对象的构造函数创建`DocumentSecurityClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要搜索的事件

   * 通过调用`DocumentSecurityClient`对象的`getEventManager`方法创建`EventManager`对象。 此方法返回`EventManager`对象。
   * 通过调用其构造函数创建`EventSearchFilter`对象。
   * 通过调用`EventSearchFilter`对象的`setEventCode`方法并传递属于表示要搜索的事件的`EventManager`类的静态数据成员，指定要搜索的事件。 例如，要搜索策略创建事件，请传递`EventManager.POLICY_CREATE_EVENT`。

   >[!NOTE]
   >
   >您可以通过调用`EventSearchFilter`对象方法来定义其他搜索条件。 例如，调用`setUserName`方法以指定与事件关联的用户。

1. 搜索事件

   通过调用`EventManager`对象的`searchForEvents`方法并传递定义事件搜索条件的`EventSearchFilter`对象来搜索事件。 此方法返回`Event`对象的数组。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP)：使用Java API搜索事件”

### 使用Web服务API搜索事件 {#search-for-events-using-the-web-service-api}

使用Rights Management API（Web服务）搜索事件：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Rights Management客户端API对象

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 指定要搜索的事件

   * 使用构造函数创建`EventSpec`对象。
   * 通过设置`EventSpec`对象的`firstTime.date`数据成员的`DataTime`实例（表示事件发生时日期范围的开始）来指定事件发生期间的开始。
   * 将值`true`分配给`EventSpec`对象的`firstTime.dateSpecified`数据成员。
   * 通过设置`EventSpec`对象的`lastTime.date`数据成员的`DataTime`实例来指定事件发生期间的结束，该实例表示事件发生时日期范围的结束。
   * 将值`true`分配给`EventSpec`对象的`lastTime.dateSpecified`数据成员。
   * 通过为`EventSpec`对象的`eventCode`数据成员分配字符串值来设置要搜索的事件。 下表列出了可以分配给此属性的数值：

   <table>
    <thead>
    <tr>
    <th><p>事件类型</p></th>
    <th><p>价值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. 搜索事件

   通过调用`DocumentSecurityServiceClient`对象的`searchForEvents`方法并传递表示要搜索的事件和最大结果数的`EventSpec`对象来搜索该事件。 此方法返回`MyArrayOf_xsd_anyType`集合，其中每个元素都是`AuditSpec`实例。 使用`AuditSpec`实例，您可以获取有关事件的信息，如发生时间。 `AuditSpec`实例包含指定此信息的`timestamp`数据成员。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API搜索事件”
* “快速入门(SwaRef)：使用Web服务API搜索事件”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将策略应用到Word文档 {#applying-policies-to-word-documents}

除了PDF文档之外，权限管理服务还支持其他文档格式，例如Microsoft Word文档（DOC文件）和其他Microsoft Office文件格式。 例如，您可以将策略应用到Word文档以对其进行保护。 通过将策略应用于Word文档，可以限制对该文档的访问。 如果文档已受策略保护，则无法将策略应用到该文档。

您可以在分发受策略保护的Word文档后监视其使用情况。 也就是说，您可以看到文档的使用方式以及谁在使用它。 例如，您可以查找何时有人打开了文档。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-11}

要将策略应用到Word文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security客户端API对象。
1. 检索应用了策略的Word文档。
1. 将现有策略应用到Word文档。
1. 保存受策略保护的Word文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

您必须先创建Document Security服务客户端对象，然后才能以编程方式执行Document Security服务操作。

**检索Word文档**

检索Word文档以应用策略。 将策略应用到Word文档后，用户使用文档时受到限制。 例如，如果策略不允许在脱机时打开文档，则用户必须联机才能打开文档。

**将现有策略应用到Word文档**

要将策略应用到Word文档，必须引用现有策略并指定该策略属于哪个策略集。 设置连接属性的用户必须具有对指定策略的访问权限。 如果不存在，则会发生异常。

**保存Word文档**

在Document Security服务将策略应用于Word文档后，您可以将受策略保护的Word文档另存为DOC文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问权限](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API将策略应用到Word文档 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API (Java)将策略应用到Word文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentSecurityClient`对象并传递`ServiceClientFactory`对象。

1. 检索Word文档。

   * 通过使用其构造函数并传递指定Word文档位置的字符串值，创建表示Word文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 将现有策略应用到Word文档。

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`protectDocument`方法并传递以下值，将策略应用到Word文档：

      * 包含应用了策略的Word文档的`com.adobe.idp.Document`对象。
      * 指定文档名称的字符串值。
      * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定导致使用`MyPolicies`策略集的`null`值。
      * 指定策略名称的字符串值。
      * 一个字符串值，表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，并且可以为null（如果此参数为null，则下一个参数值必须为null）。
      * 一个字符串值，表示作为文档发布者的用户管理员用户的规范名称的名称。 此参数值是可选的，可以为`null` （如果此参数为`null`，则以前的参数值必须为`null`）。
      * 表示用于选择MS Office模板的区域设置的`com.adobe.livecycle.rightsmanagement.Locale`。 此参数值是可选的，您可以指定`null`。

     `protectDocument`方法返回包含受策略保护的Word文档的`RMSecureDocumentResult`对象。

1. 保存Word文档。

   * 调用`RMSecureDocumentResult`对象的`getProtectedDoc`方法以获取受策略保护的Word文档。 此方法返回`com.adobe.idp.Document`对象。
   * 创建`java.io.File`对象并确保文件扩展名为DOC。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`getProtectedDoc`方法返回的`Document`对象）。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API将策略应用到Word文档”

### 使用Web服务API将策略应用到Word文档 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API（Web服务）将策略应用到Word文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象。

   * 使用默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索Word文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储应用了策略的Word文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 将现有策略应用到Word文档。

   通过调用`DocumentSecurityServiceClient`对象的`protectDocument`方法并传递以下值，将策略应用到Word文档：

   * 包含应用了策略的Word文档的`BLOB`对象。
   * 指定文档名称的字符串值。
   * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定导致使用`MyPolicies`策略集的`null`值。
   * 指定策略名称的字符串值。
   * 一个字符串值，表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，并且可以为null（如果此参数为null，则下一个参数值必须为`null`）。
   * 一个字符串值，表示作为文档发布者的用户管理员用户的规范名称的名称。 此参数值是可选的，可以为null（如果此参数为null，则上一个参数值必须为`null`）。
   * 指定区域设置值的`RMLocale`值（例如，`RMLocale.en`）。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数（例如，`application/doc`）。

   `protectDocument`方法返回包含受策略保护的Word文档的`BLOB`对象。

1. 保存Word文档。

   * 通过调用其构造函数并传递代表受策略保护的Word文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`protectDocument`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入Word文件。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API将策略应用到Word文档”

## 从Word文档中删除策略 {#removing-policies-from-word-documents}

您可以从受策略保护的Word文档中删除策略，以从文档中删除安全性。 即，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的Word文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关Document Security服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-12}

要从受策略保护的Word文档中删除策略，请执行以下步骤：

1. 包含项目文件
1. 创建Document Security客户端API对象。
1. 检索受策略保护的Word文档
1. 从Word文档中删除策略。
1. 保存不安全的Word文档

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Document Security客户端API对象**

在以编程方式执行Document Security服务操作之前，请先创建Document Security服务客户端对象。

**检索受策略保护的Word文档**

检索受策略保护的Word文档以删除策略。 如果尝试从不受策略保护的Word文档中删除策略，则会导致异常。

**从Word文档中删除策略**

如果连接设置中指定了管理员，则可以从受策略保护的Word文档中删除策略。 如果没有，则用于保护文档的策略必须包含`SWITCH_POLICY`权限，才能从Word文档中删除策略。 此外，在AEM Forms连接设置中指定的用户还必须具有该权限。 否则，将引发异常。

**保存不安全的Word文档**

Document Security服务从Word文档中删除策略后，您可以将不安全的Word文档另存为DOC文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用到Word文档](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API从Word文档中删除策略 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API (Java)从受策略保护的Word文档中删除策略：

1. 包含项目文件

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-rightsmanagement-client.jar。

1. 创建Document Security客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`RightsManagementClient`对象并传递`ServiceClientFactory`对象。

1. 检索受策略保护的Word文档

   * 使用受策略保护的Word文档的构造函数并传递指定Word文档位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 从Word文档中删除策略

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`removeSecurity`方法并传递包含受策略保护的Word文档的`com.adobe.idp.Document`对象，从Word文档中删除策略。 此方法返回包含不安全的Word文档的`com.adobe.idp.Document`对象。

1. 保存不安全的Word文档

   * 创建`java.io.File`对象并确保文件扩展名为DOC。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`removeSecurity`方法返回的`Document`对象）。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP模式)：使用Java API从Word文档中删除策略”

### 使用Web服务API从Word文档中删除策略 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API（Web服务）从受策略保护的Word文档中删除策略：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Document Security客户端API对象

   * 使用默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索受策略保护的Word文档

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储受策略保护的Word文档，策略将从该文档中删除。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 从Word文档中删除策略

   通过调用`RightsManagementServiceClient`对象的`removePolicySecurity`方法并传递包含受策略保护的Word文档的`BLOB`对象，从Word文档中删除策略。 此方法返回包含不安全的Word文档的`BLOB`对象。

1. 保存不安全的Word文档

   * 通过调用其构造函数并传递表示不安全Word文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`removePolicySecurity`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。

**代码示例**

有关使用Document Security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM)：使用Web服务API从Word文档中删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
