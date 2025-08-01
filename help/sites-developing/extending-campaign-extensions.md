---
title: 自定义Adobe Campaign扩展
description: 您可以在Adobe Campaign中从AEM或从AEM到Adobe Campaign调用自定义代码。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7cdce721-ca00-43ac-a543-85bfad382821
index: false
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 自定义Adobe Campaign扩展 {#creating-custom-extensions}

通常，在实施项目时，您在AEM和Adobe Campaign中都拥有自定义代码。 使用现有API，您可以在Adobe Campaign中从AEM或从AEM到Adobe Campaign调用自定义代码。 本文档介绍如何执行此操作。

## 先决条件 {#prerequisites}

您必须安装以下软件：

* Adobe Experience Manager
* Adobe Campaign 6.1

有关详细信息，请参阅[将AEM与Adobe Campaign 6.1集成](/help/sites-administering/campaignonpremise.md)。

## 示例1：AEM到Adobe Campaign {#example-aem-to-adobe-campaign}

AEM与Campaign之间的标准集成基于JSON和JSSP (JavaScript Server Page)。 这些JSSP文件可在Campaign控制台中找到，且全部以&#x200B;**aec** (Adobe Experience Cloud)开头。

![chlimage_1-15](assets/chlimage_1-15a.png)

在此示例中，创建了新的自定义JSSP文件，并从AEM端调用该文件以检索结果。 例如，它可用于从Adobe Campaign中检索数据，或将数据保存到Adobe Campaign中。

1. 在Adobe Campaign中，要创建JSSP文件，请单击&#x200B;**新建**&#x200B;图标。

   ![左上角附近带有星号的页面所指示的“新建”图标。](do-not-localize/chlimage_1-4a.png)

1. 输入此JSSP文件的名称。 在此示例中，使用了&#x200B;**cus:custom.jssp**（这意味着它位于&#x200B;**cus**&#x200B;命名空间中）。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 将以下代码置于jssp-file中：

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 保存您所做的工作。 其余的工作在AEM中进行。
1. 在AEM端创建一个简单的servlet，以便调用此JSSP。 在此示例中，您可以假设以下情况：

   * 在AEM和Campaign之间可以使用连接
   * 已在&#x200B;**/content/geometrixx-outdoors**&#x200B;上配置Campaign云服务

   此示例中最重要的对象是&#x200B;**GenericCampaignConnector**，它允许您在Adobe Campaign端调用（获取和发布）jssp文件。

   以下是一个小的代码片段：

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 在此示例中，必须将凭据传递到调用。 您可以通过getCredentials()方法获取它们，其中您传入的页面配置了Campaign云服务。

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

完整的代码如下所示：

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## 示例2：Adobe Campaign到AEM {#example-adobe-campaign-to-aem}

AEM提供了开箱即用的API，用于检索可在站点管理员资源管理器视图中任何位置使用的对象。

![chlimage_1-17](assets/chlimage_1-17a.png)

对于资源管理器中的每个节点，都有一个API链接到该节点。 例如，对于节点：

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommended](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API是：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommended.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL **.1.json**&#x200B;的末尾可以替换为&#x200B;**.2.json**、**.3.json**（根据您感兴趣的子级别数）。 若要获取所有关键字，可以使用&#x200B;**infinity**：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

为使用API，AEM默认使用基本身份验证。

名为&#x200B;**amcIntegration.js**&#x200B;的JS库在6.1.1（内部版本8624及更高版本）中可用，该库在其他多个库中实现该逻辑。

### AEM API调用 {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
