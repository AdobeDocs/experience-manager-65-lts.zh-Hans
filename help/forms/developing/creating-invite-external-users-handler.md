---
title: 创建“邀请外部用户”处理程序
description: 了解如何创建邀请外部用户处理程序。 它允许Rights Management服务邀请外部用户成为Rights Management用户。
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 5e1f1f3c-a2f3-4bf1-ba96-a02f8b16c180
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# 创建“邀请外部用户”处理程序 {#create-invite-external-users-handler}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以为Rights Management服务创建邀请外部用户处理程序。 通过“邀请外部用户”处理程序，Rights Management服务可以邀请外部用户成为Rights Management用户。 当用户成为Rights Management用户后，该用户能够执行任务，例如打开受策略保护的PDF文档。 将邀请外部用户处理程序部署到AEM Forms后，您可以使用管理控制台与其交互。

>[!NOTE]
>
>邀请外部用户处理程序是AEM Forms组件。 在创建邀请外部用户处理程序之前，建议您熟悉如何创建组件。

**步骤摘要**

要开发邀请外部用户处理程序，必须执行以下步骤：

1. 设置开发环境。
1. 定义邀请外部用户处理程序实施。
1. 定义组件XML文件。
1. 部署邀请外部用户处理程序。
1. 测试邀请外部用户处理程序。

## 设置开发环境 {#setting-up-development-environment}

要设置开发环境，必须创建一个Java项目，如Eclipse项目。 支持的Eclipse版本是`3.2.1`或更高版本。

Rights Management SPI要求在项目的类路径中设置`edc-server-spi.jar`文件。 如果不引用此JAR文件，则无法在Java项目中使用Rights Management SPI。 此JAR文件与AEM Forms SDK一起安装在`[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`文件夹中。

除了将`edc-server-spi.jar`文件添加到项目的类路径外，还必须添加使用Rights Management服务API所需的JAR文件。 在邀请外部用户处理程序中使用Rights Management服务API时需要这些文件。

## 定义邀请外部用户处理程序实施 {#define-invite-external-users-handler}

要开发邀请外部用户处理程序，必须创建实现`com.adobe.edc.server.spi.ersp.InvitedUserProvider`接口的Java类。 此类包含一个名为`invitedUser`的方法，当使用可通过管理控制台访问的&#x200B;**添加受邀用户**&#x200B;页面提交电子邮件地址时，Rights Management服务将调用该方法。

`invitedUser`方法接受`java.util.List`实例，该实例包含从&#x200B;**添加受邀用户**&#x200B;页面提交的字符串类型电子邮件地址。 `invitedUser`方法返回`InvitedUserProviderResult`对象的数组，这通常是电子邮件地址到用户对象的映射（不返回null）。

>[!NOTE]
>
>除了演示如何创建“邀请外部用户”处理程序之外，本节还使用AEM Forms API。

邀请外部用户处理程序的实现包含名为`createLocalPrincipalAccount`的用户定义方法。 此方法接受将电子邮件地址指定为参数值的字符串值。 `createLocalPrincipalAccount`方法假定名为`EDC_EXTERNAL_REGISTERED`的本地域预先存在。 您可以将此域名配置为所需的任何名称；但是，对于生产应用程序，您可能希望与企业域集成。

`createUsers`方法遍历每个电子邮件地址并创建相应的用户对象（`EDC_EXTERNAL_REGISTERED`域中的本地用户）。 最后，调用`doEmails`方法。 在示例中，此方法被有意保留为存根。 在生产实施中，它将包含应用程序逻辑，用于向新创建的用户发送邀请电子邮件。 在示例中保留它以演示实际应用程序的应用程序逻辑流程。

### 定义邀请外部用户处理程序实施 {#user-handler-implementation}

以下邀请外部用户处理程序实施接受从“添加受邀用户”页面提交的电子邮件地址，可通过管理控制台访问该页面。

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>此Java类保存为名为InviteExternalUsersSample.java的JAVA文件。

## 为授权处理程序定义组件XML文件 {#define-component-xml-authorization-handler}

查找组件XML文件以部署Invite外部用户处理程序组件。 每个组件都存在一个组件XML文件，该文件提供了有关该组件的元数据。

以下`component.xml`文件用于邀请外部用户处理程序。 请注意，服务名称为`InviteExternalUsersSample`，此服务公开的操作名为`invitedUser`。 输入参数是`java.util.List`实例，输出值是`com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`实例的数组。

### 定义邀请外部用户处理程序的组件XML文件 {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## 正在打包邀请外部用户处理程序 {#packaging-invite-external-users-handler}

要将邀请外部用户处理程序部署到AEM Forms，必须将Java项目打包到JAR文件中。 确保JAR文件中也包含邀请外部用户处理程序的业务逻辑所依赖的外部JAR文件，例如`edc-server-spi.jar`和`adobe-rightsmanagement-client.jar`文件。 另外，组件XML文件必须存在。 `component.xml`文件和外部JAR文件必须位于JAR文件的根目录下。

>[!NOTE]
>
>在下图中，显示了`BootstrapImpl`类。 本节不讨论如何创建`BootstrapImpl`类。

下图显示了打包到邀请外部用户处理程序的JAR文件中的Java项目内容。

![邀请用户](assets/ci_ci_InviteUsers.png)

A.组件所需的外部JAR文件B. JAVA文件

将邀请外部用户处理程序打包到JAR文件中。 在上图中，请注意列出了.JAVA文件。 打包到JAR文件后，还必须指定相应的.CLASS文件。 如果没有.CLASS文件，授权处理程序将无法工作。

>[!NOTE]
>
>将外部授权处理程序打包到JAR文件后，可以将组件部署到AEM Forms。 在给定时间只能部署一个邀请外部用户处理程序。

>[!NOTE]
>
>您还可以以编程方式部署组件。

## 测试邀请外部用户处理程序 {#testing-invite-external-users-handler}

要测试邀请外部用户处理程序，可以使用管理控制台添加要邀请的外部用户。

要使用管理控制台添加要邀请的外部用户，请执行以下操作：

1. 使用Workbench部署邀请外部用户处理程序的JAR文件。
1. 重新启动应用程序服务器。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。

1. 登录到管理控制台。
1. 单击&#x200B;**[!UICONTROL 服务]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 配置]** >已邀请的&#x200B;**[!UICONTROL 用户注册]**。
1. 通过选中&#x200B;**[!UICONTROL 启用受邀用户注册]**&#x200B;框启用受邀用户注册。 在&#x200B;**[!UICONTROL 使用内置注册系统]**&#x200B;下，单击&#x200B;**[!UICONTROL 否]**。 保存您的设置。
1. 在管理控制台主页中，单击&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 用户管理]** > **[!UICONTROL 域管理]**。
1. 单击&#x200B;**[!UICONTROL 新建本地域]**。 在以下页面中，创建一个名称和标识符值为`EDC_EXTERNAL_REGISTERED`的域。 保存更改。
1. 在管理控制台主页中，单击&#x200B;**[!UICONTROL 服务]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 受邀用户和本地用户]**。 此时会显示&#x200B;**[!UICONTROL 添加受邀用户]**&#x200B;页面。
1. 输入电子邮件地址（由于当前的邀请外部用户处理程序实际上并不发送电子邮件，因此电子邮件地址不一定有效）。 单击&#x200B;**[!UICONTROL 确定]**。 用户受邀加入系统。
1. 在管理控制台主页上，单击&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 用户管理]** > **[!UICONTROL 用户和组]**。
1. 在&#x200B;**[!UICONTROL 查找]**&#x200B;字段中，输入您指定的电子邮件地址。 单击&#x200B;**[!UICONTROL 查找]**。 您邀请的用户显示为本地`EDC_EXTERNAL_REGISTERED`域中的用户。

>[!NOTE]
>
>如果停止或卸载该组件，则邀请外部用户处理程序将失败。
