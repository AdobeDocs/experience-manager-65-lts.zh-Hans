---
title: Adobe Experience Manager Sites开发中的体验片段
description: 了解如何自定义Adobe Experience Manager的体验片段。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: bc621086-8128-4836-a580-dca99f61c439
source-git-commit: d894bb145d70fba819cc8452056e9e46112e69d9
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 0%

---

# 体验片段 {#experience-fragments}

## 基础知识 {#the-basics}

[体验片段](/help/sites-authoring/experience-fragments.md)是由一个或多个组件组成的组，这些组件包括可在页面中引用的内容和布局。

主体验片段或变体体验片段（或两者）使用以下内容：

* `sling:resourceType` ： `/libs/cq/experience-fragments/components/xfpage`

由于没有`/libs/cq/experience-fragments/components/xfpage/xfpage.html`，因此它将还原为以下内容：

* `sling:resourceSuperType` ： `wcm/foundation/components/page`

## 普通HTML演绎版 {#the-plain-html-rendition}

使用URL中的`.plain.`选择器，您可以访问纯HTML演绎版。

可以从浏览器中使用此功能。 但是，其主要目的是允许其他应用程序（例如，第三方Web应用程序、自定义移动实施）仅使用URL直接访问体验片段的内容。

纯HTML演绎版将协议、主机和上下文路径添加到路径中：

* 类型： `src`、`href`或`action`

* 或结尾为： `-src`或`-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>链接始终引用发布实例。 第三方使用它们，因此它们始终从发布实例而不是创作实例调用链接。
>
>有关详细信息，请参阅[外部化URL](/help/sites-developing/externalizer.md)。

![xf-14](assets/xf-14.png)

纯格式副本选择器使用转换器而不是其他脚本；[`Sling Rewriter`](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)用作转换器，并在以下位置进行配置：

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 配置HTML呈现版本生成 {#configuring-html-rendition-generation}

HTML演绎版是使用`Sling Rewriter`管道生成的。 管道定义于`/libs/experience-fragments/config/rewriter/experiencefragments`。 HTML Transformer支持以下选项：

* `allowedCssClasses`
   * 匹配应在最终演绎版中保留的CSS类的RegEx表达式。
   * 如果客户想要删除某些特定的CSS类，则此功能非常有用
* `allowedTags`
   * 最终演绎版中允许的HTML标记列表。
   * 默认情况下，系统允许不配置以下标记：html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、`noscript`、div、link和脚本。

建议您使用叠加来配置重写器。 查看[叠加图](/help/sites-developing/overlays.md)

## 社交变体 {#social-variations}

社交变体可发布在社交媒体（文本和图像）上。 在Adobe Experience Manager (AEM)中，这些社交变体可以包含组件；例如，文本组件、图像组件。

您可以从任何图像或文本资源类型中获取任何深度的社交帖子图像和文本。 资源可以来自构建基块或布局容器。

社交变体还允许构建基块，并在进行社交操作（在发布环境中）时将其考虑在内。

要将正确的文本和图像发布到社交媒体网络，如果您开发自己的自定义组件，则需要遵守一些惯例。

必须使用以下属性：

* 为了提取图像，

   * `fileReference`
   * `fileName`

* 要提取文本，

   * `text`

仅考虑使用此约定的组件。

## 体验片段的模板 {#templates-for-experience-fragments}

>[!CAUTION]
>
>体验片段仅支持&#x200B;***1&rbrace;***&#x200B;可编辑模板[。](/help/sites-developing/page-templates-editable.md)
>
>体验片段只能在基于可编辑模板的页面上使用。

为体验片段开发新模板时，您可以遵循[可编辑模板](/help/sites-developing/page-templates-editable.md)的标准实践。

要创建&#x200B;**创建体验片段**&#x200B;向导检测到的体验片段模板，必须遵循以下规则集之一：

1. 两者：

   1. 模板的资源类型（初始节点）必须继承自：
      `cq/experience-fragments/components/xfpage`

   1. 模板名称必须以下列内容开头：
      `experience-fragments`
允许用户在`/content/experience-fragments`中创建体验片段，因为该文件夹的`cq:allowedTemplates`属性包含名称以`experience-fragment`开头的所有模板。 客户可以更新此属性以包含他们自己的命名方案或模板位置。

1. 可以在体验片段控制台中配置[允许的模板](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder)。
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 体验片段的组件 {#components-for-experience-fragments}

[开发用于体验片段/体验片段的组件](/help/sites-developing/components.md)将遵循标准实践。

唯一额外的配置是确保模板上允许使用这些组件。 此功能是通过[内容策略](/help/sites-developing/page-templates-editable.md#content-policies)实现的。

## 体验片段链接重写器提供程序 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以创建体验片段。 体验片段：

* 由一组组件和一个布局组成，
* 可以独立于AEM页面而存在。

此类组的用例之一是将内容嵌入第三方接触点，例如Adobe Target。

### 默认链接重写 {#default-link-rewriting}

使用[导出到Target](/help/sites-administering/experience-fragments-target.md)功能，您可以：

* 创建体验片段，
* 向其中添加组件，
* 然后以HTML格式或JSON格式将其导出为Adobe Target选件。

可在AEM[的创作实例上](/help/sites-administering/experience-fragments-target.md#Prerequisites)启用此功能。 它需要有效的Adobe Target配置以及Link Externalizer配置。

链接外部化器用于确定在创建Target选件的HTML版本(随后将发送到Adobe Target)时所需的正确URL。 Adobe Target需要拥有Target HTML选件中所有链接的公共访问权限。 在使用体验片段和这些链接引用的任何资源之前，先发布它们。


默认情况下，构造Target HTML选件时，会向AEM中的自定义Sling选择器发送请求。 此选择器名为`.nocloudconfigs.html`。 顾名思义，它创建了体验片段的纯HTML渲染，但不包括云配置（这会是多余的信息）。

生成HTML页面后，`Sling Rewriter`管道对输出进行修改：

1. `html`、`head`和`body`元素已替换为`div`元素。 已删除`meta`、`noscript`和`title`元素（它们是原始`head`元素的子元素，在被`div`元素替换时不会考虑）。

   完成此过程是为了确保HTML Target选件可包含在Target活动中。

1. AEM会修改HTML中存在的任何内部链接，以便这些链接指向已发布的资源。

   要确定要修改的链接，AEM会对HTML元素的属性遵循以下模式：

   1. `src`属性
   1. `href`属性
   1. `*-src`属性（如data-src、custom-src等）
   1. `*-href`属性（如`data-href`、`custom-href`、`img-href`等）

   >[!NOTE]
   >
   >通常，HTML中的内部链接是相对链接，但在某些情况下，自定义组件会在HTML中提供完整的URL。 默认情况下，AEM会忽略这些功能齐全的URL且不进行任何修改。

   这些属性中的链接通过AEM链接外部化器`publishLink()`重新创建URL，就像在已发布的实例上一样，因此是公开可用的。

使用开箱即用的实施时，上述流程足以从体验片段生成Target选件，然后将其导出到Adobe Target。 但是，此流程中尚未考虑一些用例，包括：

* Sling映射仅在发布实例上可用。
* Dispatcher重定向。

对于这些用例，AEM提供了链接重写器提供程序界面。

### 链接重写器提供程序界面 {#link-rewriter-provider-interface}

对于[default](#default-link-rewriting)未涵盖的更复杂的情况，AEM提供链接重写器提供程序接口。 此工作流是`ConsumerType`接口，您可以在捆绑包中将其实施为服务。 它绕过AEM对HTML选件的内部链接执行的修改，这些修改是从Experience Fragment渲染的。 利用此界面，可自定义重写HTML内部链接的流程，以满足您的业务需求。

实施此接口作为服务的用例示例包括：

* Sling映射在发布实例上启用，但在创作实例上未启用。
* 使用Dispatcher或类似的技术在内部重定向URL。
* 资源有`sling:alias`机制。

>[!NOTE]
>
>此界面仅处理来自所生成Target选件的内部HTML链接。

链接重写器提供程序接口( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用链接重写器提供程序界面 {#how-to-use-the-link-rewriter-provider-interface}

要使用该接口，您首先需要创建一个包，其中包含用于实现链接重写器提供程序接口的新服务组件。

此服务用于插入Experience Fragment Export to Target重写以访问各种链接。

例如，`ComponentService`：

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

要使服务正常工作，现在需要在服务中实施三种方法：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您需要向系统指示当对特定体验片段变量调用“导出到Target”时，是否需要重写链接。 您可以使用以下方法执行此&#x200B;**实施**：


`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法接收导出到Target系统当前正在重写的体验片段变体作为参数。

在上例中，您想要重写：

* `src`中存在链接

* 仅`href`属性

* 对于特定体验片段：
  `/content/experience-fragment/master`

导出到Target系统忽略通过它的任何其他体验片段，并且此服务不会影响它们。

#### rewriteLink {#rewritelink}

对于受重写过程影响的体验片段变体，它会继续让服务处理链接重写。 每次在内部HTML中遇到链接时，都会调用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作为输入，方法接收参数：

* `link`
正在处理的链接的`String`表示形式。 通常是创作实例中指向资源的相对URL。

* `tag`
正在处理的HTML元素的名称。

* `attribute`
确切的属性名称。

例如，如果Export to Target系统正在处理此元素，您可以将`CSSInclude`定义为：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

使用以下参数完成对`rewriteLink()`方法的调用：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

在创建服务时，您可以根据给定的输入进行决策，然后相应地重写链接。

例如，您要删除URL的`/etc.clientlibs`部分并添加适当的外部域。 为了简单起见，请考虑您有权访问服务的资源解析程序，如`rewriteLinkExample2`中所示：

>[!NOTE]
>
>有关如何通过服务用户获取资源解析程序的详细信息，请参阅[AEM中的服务用户](/help/sites-administering/security-service-users.md)。

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法返回`null`，则Export to Target系统将保持链接不变，即指向资源的相对链接。

#### 优先级 — getPriority {#priorities-getpriority}

您可能需要多项服务才能支持不同类型的体验片段。 您还可以使用通用服务来外部化和映射所有体验片段。 在这些情况下，可能会发生与使用哪个服务有关的冲突，因此AEM提供了为其他服务定义&#x200B;**优先级**&#x200B;的可能性。 使用下列方法指定优先级：

* `getPriority()`

此方法允许使用多个服务，其中`shouldRewrite()`方法为同一体验片段返回true。 从其`getPriority()`方法返回最高数字的服务是处理体验片段变体的服务。

例如，您可以有一个`GenericLinkRewriterProvider`处理所有体验片段的基本映射，并且当`shouldRewrite()`方法返回所有体验片段变量的`true`时。 对于多个特定的体验片段，您可能需要特殊的处理，因此在这种情况下，您可以提供`SpecificLinkRewriterProvider`，对于该，`shouldRewrite()`方法仅在某些体验片段变量中返回true。 为确保选择`SpecificLinkRewriterProvider`来处理这些体验片段变量，它必须在其`getPriority()`方法中返回大于`GenericLinkRewriterProvider.`的数字
