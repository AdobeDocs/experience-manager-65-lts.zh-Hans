---
title: 如何以编程方式访问AEM JCR
description: 您可以通过编程方式修改位于AEM存储库(Adobe Experience Cloud的一部分)中的节点和属性
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
exl-id: 0b375003-183d-4007-b1a1-0c48607745d1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 如何以编程方式访问AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以通过编程方式修改位于Adobe CQ存储库(Adobe Experience Cloud的一部分)中的节点和属性。 要访问CQ存储库，请使用Java™内容存储库(JCR) API。 您可以使用Java™ JCR API创建、替换、更新和删除Adobe CQ存储库中的(CRUD)内容。 有关Java™ JCR API的详细信息，请参阅[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>此开发文章从外部Java™应用程序修改了Adobe CQ JCR。 相反，您可以使用JCR API从OSGi捆绑包中修改JCR。 有关详细信息，请参阅[将CQ数据保留在Java™内容存储库中](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)。

>[!NOTE]
>
>要使用JCR API，请将`jackrabbit-standalone-2.4.0.jar`文件添加到Java™应用程序的类路径中。 您可以从[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)上的Java™ JCR API网页获取此JAR文件。

>[!NOTE]
>
>要了解如何使用JCR查询API查询Adobe CQ JCR，请参阅[使用JCR API查询Adobe Experience Manager数据](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## 创建存储库实例 {#create-a-repository-instance}

虽然有不同的方法连接到存储库并建立连接，但此开发文章使用属于`org.apache.jackrabbit.commons.JcrUtils`类的静态方法。 方法的名称为`getRepository`。 此方法采用表示Adobe CQ服务器URL的字符串参数。 例如 `http://localhost:4503/crx/server`。

`getRepository`方法返回`Repository`实例，如以下代码示例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 创建会话实例 {#create-a-session-instance}

`Repository`实例表示CRX存储库。 您使用`Repository`实例与存储库建立会话。 要创建会话，请调用`Repository`实例的`login`方法并传递`javax.jcr.SimpleCredentials`对象。 `login`方法返回`javax.jcr.Session`实例。

您通过使用其构造函数并传递以下字符串值来创建`SimpleCredentials`对象：

* 用户名；
* 相应的密码

传递第二个参数时，调用字符串对象的`toCharArray`方法。 以下代码说明如何调用返回`javax.jcr.Sessioninstance`的`login`方法。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 创建节点实例 {#create-a-node-instance}

使用`Session`实例创建`javax.jcr.Node`实例。 `Node`实例允许您执行节点操作。 例如，您可以创建一个节点。 要创建表示根节点的节点，请调用`Session`实例的`getRootNode`方法，如下一行代码所示。

```java
//Create a Node
Node root = session.getRootNode();
```

创建`Node`实例后，您可以执行创建其他节点并向其添加值等任务。 例如，以下代码创建两个节点，并向第二个节点添加一个值。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 检索节点值 {#retrieve-node-values}

要检索节点及其值，请调用`Node`实例的`getNode`方法，并传递一个表示节点的完全限定路径的字符串值。 考虑在上一个代码示例中创建的节点结构。 要检索日期节点，请指定adobe/day，如以下代码所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ存储库中创建节点 {#create-nodes-in-the-adobe-cq-repository}

以下Java™代码示例表示一个连接到Adobe CQ、创建`Session`实例和添加新节点的Java™类。 为节点分配一个数据值，然后将节点的值及其路径写出到控制台。 完成会话后，请务必注销。

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

运行完整的代码示例并创建节点后，您可以在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中查看新节点，如下图所示。

![chlimage_1-68](assets/chlimage_1-68a.png)
