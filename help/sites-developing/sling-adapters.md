---
title: 使用 Sling 适配器
description: Sling提供了一个适配器模式，用于方便地翻译实现自适应界面的对象。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7eae83bd-7982-4051-821f-b43f65c5af2b
source-git-commit: cf22b13e0f7c8e66b598f85aab81b022480e60bc
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 2%

---

# 使用Sling适配器{#using-sling-adapters}

[Sling](https://sling.apache.org)提供[适配器模式](https://sling.apache.org/documentation/the-sling-engine/adapters.html)以方便翻译实现[可适应](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)接口的对象。 此接口提供了一个通用[adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)方法，它将对象转换为作为参数传递的类类型。

例如，要将Resource对象转换为对应的Node对象，您只需执行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 用例 {#use-cases}

有以下用例：

* 获取特定于实施的对象。

  例如，通用[`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html)接口的基于JCR的实现提供了对基础JCR [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)的访问。

* 快捷方式创建需要传递内部上下文对象的对象。

  例如，基于JCR的[`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)保留对请求的[`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html)的引用，而基于此请求会话工作的许多对象（如[`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)或[`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/security/UserManager.html)）都需要该引用。

* 服务的快捷方式。

  极少数情况 — `sling.getService()`也非常简单。

### 空返回值 {#null-return-value}

`adaptTo()`返回null。

原因多种多样，包括：

* 实施不支持目标类型。
* 处理此情况的适配器工厂未处于活动状态（例如，由于缺少服务引用）
* 内部条件失败。
* 服务不可用。

正确处理空值情况很重要。 对于jsp渲染，如果导致jsp失败导致内容为空，则最好是让jsp失败。

### 缓存 {#caching}

为了提高性能，实施可以缓存从`obj.adaptTo()`调用返回的对象。 如果`obj`是相同的，则返回的对象是相同的。

对所有基于`AdapterFactory`的案例执行此缓存。

但是，没有一般规则 — 对象可以是新实例或现有实例。 这意味着您无法依赖这两种行为。 因此，对象可在此方案中重用，这一点很重要，尤其是在`AdapterFactory`内。

### 工作原理 {#how-it-works}

有多种方法可以实现`Adaptable.adaptTo()`：

* 对象本身；实现方法本身并映射到某些对象。
* 通过[`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可以映射任意对象。

  对象仍必须实现`Adaptable`接口，并且必须扩展[`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/adapter/SlingAdaptable.html)（它将`adaptTo`调用传递到中央适配器管理器）。

  挂接到现有类（如`adaptTo`）的`Resource`机制。

* 两者的组合。

对于第一种情况，Java™文档可以说明哪些`adaptTo-targets`是可能的。 但是，对于特定的子类（如基于JCR的资源），通常不可能执行此操作。 在后一种情况下，`AdapterFactory`的实现通常是捆绑包的私有类的一部分，因此未在客户端API中公开或列在Java™文档中。 从理论上讲，可以从`AdapterFactory`OSGi[服务运行时访问所有](/help/sites-deploying/configuring-osgi.md)实现并查看其“可适应的”（源和目标）配置，但不能将它们相互映射。 最后，它取决于内部逻辑，必须记录该逻辑。 因此，请参考。

## 引用 {#reference}

### Sling {#sling}

[**资源**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html)已适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>如果它是基于JCR节点的资源或引用节点的JCR属性</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Property.html">属性</a></td>
   <td>如果它是基于JCR属性的资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html">项目</a></td>
   <td>如果它是基于JCR的资源（节点或属性）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">地图</a></td>
   <td>如果是基于JCR节点的资源（或其他支持值的资源映射），则返回属性的映射。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">值映射</a></td>
   <td>如果是基于JCR节点的资源或其他支持值的资源映射，它会返回便于使用的属性映射。 也可以使用<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code>（处理null大小写等）实现它（更简单）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，允许在查找属性时考虑资源的层次结构。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，允许您修改该节点上的属性。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">输入流</a></td>
   <td>当文件资源基于JCR节点（<code>nt:file</code>或<code>nt:resource</code>）、包资源或文件系统资源时，它会返回文件资源的二进制内容。 它会返回二进制JCR属性资源的数据。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>它会返回资源的URL。 它会返回基于JCR节点的资源的存储库URL、捆绑资源的JAR捆绑URL或文件系统资源的文件URL。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">文件</a></td>
   <td>如果它是文件系统资源</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此资源是脚本（例如jsp文件），且脚本引擎已注册到sling。</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>如果此资源是脚本（例如jsp文件），且脚本引擎已向sling注册，或者它是servlet资源。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">日历</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">值[]</a></td>
   <td>如果是基于JCR属性的资源，则返回值（该值适合）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>如果它是基于JCR节点的资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html">页面</a></td>
   <td>如果它是基于JCR节点的资源，并且该节点是<code>cq:Page</code>（或<code>cq:PseudoPage</code>）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html">组件</a></td>
   <td>如果它是<code>cq:Component</code>节点资源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Design.html">设计</a></td>
   <td>如果它是设计节点(<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html">模板</a></td>
   <td>如果它是<code>cq:Template</code>节点资源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>如果它是<code>cq:Template</code>节点资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/Asset.html">资源</a></td>
   <td>如果它是<code>dam:Asset</code>节点资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/Rendition.html">演绎版</a></td>
   <td>如果它是<code>dam:Asset</code>节目（<code>nt:file</code>的节目文件夹下的<code>dam:Asset</code>）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/tagging/Tag.html">标记</a></td>
   <td>如果它是<code>cq:Tag</code>节点资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/security/UserManager.html">用户管理器</a></td>
   <td>基于JCR会话（如果是基于JCR的资源），并且用户有权访问UserManager。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a></td>
   <td>“可授权”是“用户”和“组”的公共基本界面。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a></td>
   <td>用户是一种特殊的可授权用户，可以进行身份验证和模拟。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/SimpleSearch.html">简单搜索</a></td>
   <td>在资源下搜索(如果它是基于JCR的资源，则使用setSearchIn())。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流状态</a></td>
   <td>给定页面/工作流有效负荷节点的工作流状态。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html">复制状态</a></td>
   <td>给定资源或其<code>jcr:content</code>子节点的复制状态（首先选中）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/connector/ConnectorResource.html">连接器资源</a></td>
   <td>如果它是基于JCR节点的资源，则它会针对某些类型返回经过调整的连接器资源。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">配置</a></td>
   <td>如果它是<code>cq:ContentSyncConfig</code>节点资源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果它在<code>cq:ContentSyncConfig</code>节点资源下</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceResolver.html)适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html">会话</a></td>
   <td>请求的JCR会话（如果是基于JCR的资源解析程序，则为默认）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">组件管理器</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>基于JCR会话（如果是基于JCR的资源解析程序）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/tagging/TagManager.html">标记管理器</a></td>
   <td>基于JCR会话（如果是基于JCR的资源解析程序）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">用户管理器</a></td>
   <td>UserManager提供对作为用户和组的可授权对象的访问和维护。 UserManager绑定到特定会话。
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a> </td>
   <td>当前用户。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a><br /> </td>
   <td>当前用户。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html">Querybuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/Externalizer.html">外部化器</a></td>
   <td>用于外部化绝对URL，即使没有请求对象也是如此。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)适应：

还没有目标，但实施了Adaptable，并且可以在自定义AdapterFactory中用作源。

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果是Sling重写器响应</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[页面](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html)**&#x200B;适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>页面的资源。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已标记的资源是当前资源。 就是你看到的那个物体。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>页面的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>页面资源可适应的一切。</td>
  </tr>
 </tbody>
</table>

**[组件](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html)**&#x200B;适应：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | 组件的资源。 |
| --- | --- |
| [标记资源](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html) | 已标记的资源是当前资源。 就是你看到的那个物体。 |
| [节点](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | 组件的节点。 |
| ... | 组件资源可以适应的一切。 |

**模板[2&rbrace;](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html)适应：**

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>模板的资源。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已标记的资源是当前资源。 就是你看到的那个物体。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>此模板的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>模板资源可以适应的一切。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授权**、&lbrace;User&#x200B;**和&#x200B;**&#x200B;组**&#x200B;适应：

| [节点](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用户/组主节点。 |
| --- | --- |
| [ReplicationStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html) | 它会返回用户/组主节点的复制状态。 |

#### DAM {#dam}

**资源**&#x200B;已适应：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | 资源的资源。 |
| --- | --- |
| [节点](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | 资源的节点。 |
| ... | 资产资源可以适应的一切。 |

#### 标记 {#tagging}

**标记**&#x200B;适应：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | 标记的资源。 |
| --- | --- |
| [节点](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | 标记的节点。 |
| ... | 标记资源可以适应的一切。 |

#### 其他 {#other}

此外，Sling / JCR / OCM还为自定义OCM （` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`对象内容映射[）对象提供了](https://jackrabbit.apache.org/jcr/object-content-mapping.html)。
