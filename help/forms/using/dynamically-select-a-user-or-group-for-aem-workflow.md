---
title: 动态选择用户或组以执行以AEM Forms为中心的工作流步骤
description: 了解如何在运行时为AEM Forms工作流选择用户或组。
content-type: troubleshooting
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services
exl-id: b3b3567f-df0a-4a24-849c-dcc0b745de63
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# 动态选择用户或组以执行以AEM Forms为中心的工作流步骤 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

了解如何在运行时为AEM Forms工作流选择用户或组。

在大型组织中，需要动态地为流程选择用户。 例如，根据代理与客户的接近程度选择现场代理为客户提供服务。 在这种情况下，将动态选择代理。

在OSGi[&#128279;](/help/forms/using/aem-forms-workflow.md)上分配任务和以Forms为中心的工作流的Adobe Sign步骤，提供了用于动态选择用户的选项。 您可以使用ECMAScript或OSGi捆绑包为“分配任务”步骤动态选择被分配人，或为“签名文档”步骤选择签名者。

## 使用ECMAScript动态选择用户或组 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一种脚本语言。 它用于客户端脚本和服务器应用程序。 执行以下步骤，使用ECMAScript动态选择用户或组：

1. 打开CRXDE Lite。 URL是`https://'[server]:[port]'/crx/de/index.jsp`
1. 在以下路径创建扩展名为.ecma的文件。 如果路径（节点结构）不存在，请创建路径：

   * （分配任务步骤的路径） `/apps/fd/dashboard/scripts/participantChooser`
   * （签名步骤的路径） `/apps/fd/workflow/scripts/adobesign`

1. 将具有动态选择用户的逻辑的ECMAScript添加到.ecma文件中。 单击&#x200B;**[!UICONTROL 全部保存]**。

   有关示例脚本，请参阅[用于动态选择用户或组的示例ECMAScript](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group)。

1. 添加脚本的显示名称。 此名称显示在工作流步骤中。 要指定名称，请执行以下操作：

   1. 展开脚本节点，右键单击&#x200B;**[!UICONTROL jcr：content]**&#x200B;节点，然后单击&#x200B;**[!UICONTROL Mixins]**。
   1. 在“编辑Mixin”对话框中添加属性`mix:title`，然后单击&#x200B;**确定**。
   1. 将以下属性添加到脚本的jcr：content节点：

      | 名称 | 类型 | 价值 |
      |--- |--- |--- |
      | jcr:title | 字符串 | 指定脚本的名称。 例如，选择最近的字段代理。 此名称显示在分配任务和签名文档步骤中。 |

   1. 单击&#x200B;**全部保存**。 该脚本将在AEM Workflow的组件中可供选择。

      ![脚本](assets/script.png)

### 用于动态选择用户或组的示例ECMAScript {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

以下示例ECMAScript为“分配任务”步骤动态选择被分配人。 在此脚本中，根据有效负载的路径选择用户。 使用此脚本之前，请确保脚本中提到的所有用户都存在于AEM中。 如果脚本中提到的用户在AEM中不存在，则相关流程可能会失败。

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

以下示例ECMAScript为Adobe Sign步骤动态选择代理人。 在使用以下脚本之前，请确保脚本中提到的用户信息（电子邮件地址和电话号码）正确无误。 如果脚本中提到的用户信息不正确，则相关进程可能会失败。

>[!NOTE]
>
>在使用ECMAScript for Adobe Sign时，脚本必须位于/apps/fd/workflow/scripts/adobesign/的crx-repository中，并且应该具有一个名为getAdobeSignRecipients的函数以返回用户列表。

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## 使用Java界面动态选择用户或组 {#use-java-interface-to-dynamically-choose-a-user-or-group}

您可以使用[RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面动态选择用户或组以执行Adobe Sign和分配任务步骤。 您可以创建一个使用了[RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java接口的OSGi捆绑包，并将其部署到AEM Forms服务器。 这使该选项可以在AEM工作流的分配任务和Adobe Sign组件中进行选择。

您需要[AEM Forms客户端SDK](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans) jar和[granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/)文件来编译下面列出的代码示例。 将这些jar文件作为外部依赖项添加到OSGi捆绑包项目中。 您可以使用任何Java IDE创建OSGi捆绑包。 以下过程提供了使用Eclipse创建OSGi捆绑包的步骤：

1. 打开Eclipse IDE。 导航到&#x200B;**[!UICONTROL 文件]**> **[!UICONTROL 新建项目]**。
1. 在选择向导屏幕上，选择&#x200B;**[!UICONTROL Maven项目]**，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 在新的Maven项目中，保留默认值，然后单击&#x200B;**[!UICONTROL 下一步]**。 选择原型并单击&#x200B;**[!UICONTROL 下一步]**。 例如，maven-archetype-quickstart。 为项目指定&#x200B;**[!UICONTROL 组ID]**、**[!UICONTROL 项目ID]**、**[!UICONTROL 版本]**&#x200B;和&#x200B;**[!UICONTROL 包]**，然后单击&#x200B;**[!UICONTROL 完成]**。 将创建项目。
1. 打开pom.xml文件进行编辑，并将文件的所有内容替换为以下内容：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. 添加使用[RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java接口为“分配”任务步骤动态选择用户或组的源代码。 有关示例代码，请参阅[使用Java接口动态选择用户或组的示例](#-sample-scripts-for)。
1. 打开命令提示符并导航到包含OSGi捆绑包项目的目录。 使用以下命令创建OSGi捆绑包：

   `mvn clean install`

1. 将捆绑包上传到AEM Forms服务器。 您可以使用AEM包管理器将包导入到AEM Forms服务器。

导入捆绑包后，中提供了用于选择用于动态选择用户或组的Java界面的选项，以执行Adobe Sign和分配任务步骤。

### 用于动态选择用户或组的示例Java代码 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

以下代码示例为Adobe Sign步骤动态选择被分配人。 您可以在OSGi捆绑包中使用代码。 在使用下列代码之前，请确保代码中提到的用户信息（电子邮件地址和电话号码）正确无误。 如果代码中提到的用户信息不正确，则相关流程可能会失败。

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```
