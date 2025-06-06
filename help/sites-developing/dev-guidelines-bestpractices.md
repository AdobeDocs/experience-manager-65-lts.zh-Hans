---
title: AEM 开发 - 准则和最佳实践
description: 在AEM上进行开发的准则和最佳实践
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7fd478a6-ddc6-4c7f-b09b-e4de6ec0e897
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# AEM 开发 - 准则和最佳实践{#aem-development-guidelines-and-best-practices}

## 使用模板和组件的准则 {#guidelines-for-using-templates-and-components}

Adobe Experience Manager (AEM)组件和模板构成了一个功能强大的工具包。 开发人员可以使用这些功能为网站业务用户、编辑和管理员提供使其网站适应不断变化的业务需求（内容敏捷性）的功能。 所有这些都可以在保持站点统一布局（品牌保护）的同时实现。

对于负责一个网站或一组网站（例如，在全球企业的一个分支办公室中）的人员来说，一个典型的挑战是在其网站上引入一种新的内容呈现方式。

假设需要向网站添加新闻列表页面，其中列出了从已发布的其他文章中提取的内容。 该页面应具有与网站其他部分相同的设计和结构。

应对这一挑战的建议方法是：

* 重用现有的模板，以便您可以创建一种类型的页面。 模板粗略定义了页面结构（导航元素、面板等），其设计进一步细化（CSS、图形）。
* 在新页面上使用段落系统(parsys/iparsys)。
* 定义对段落系统设计模式的访问权限，以便只有授权人员（通常是管理员）才能更改这些权限。
* 定义给定段落系统中允许的组件，以便编辑者随后能够将所需的组件放置在页面上。 在这种情况下，它可以是一个列表组件，该组件可以遍历页面的子树，并根据预定义的规则提取信息。
* 编辑者在他们负责的页面上添加和配置允许的组件，向企业提供所请求的功能（信息）。

这说明了这种方法如何使网站贡献用户和管理员能够快速响应业务需求，而无需开发团队的参与。 替代方法，如创建模板，通常是一项成本高昂的工作，需要变更管理流程和开发团队的参与。 这使得整个过程更长，成本更高。

因此，基于AEM的系统开发人员应使用：

* 用于统一性和品牌保护的段落系统设计模板和访问控制
* 段落系统，包括其配置选项，以实现灵活性。

以下适用于开发人员的常规规则在大多数常用项目中是合理的：

* 保持较低的模板数量 — 与网站上完全不同的页面结构数量一样低。
* 为自定义组件提供必要的灵活性和配置功能。
* 最大限度地利用AEM段落系统（parsys和iparsys组件）的强大功能和灵活性。

### 自定义组件和其他元素 {#customizing-components-and-other-elements}

在创建自己的组件或自定义现有组件时，重用现有定义通常最简单（也是最安全的）。 同样的原则也适用于AEM中的其他元素，例如错误处理程序。

这可以通过复制和覆盖现有定义来完成。 换句话说，将定义从`/libs`复制到`/apps/<your-project>`。 可以根据您的要求更新`/apps`中的新定义。

>[!NOTE]
>
>有关更多详细信息，请参阅[使用叠加图](/help/sites-developing/overlays.md)。

例如：

* [自定义组件](/help/sites-developing/components.md)

  这涉及覆盖组件定义：

   * 通过复制现有组件在`/apps/<website-name>/components/<MyComponent>`中创建组件文件夹：

      * 例如，要自定义文本组件复制，请执行以下操作：

         * 从 `/libs/foundation/components/text`
         * 至`/apps/myProject/components/text`

* [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  这种情况涉及覆盖servlet：

   * 在存储库中，复制一个或多个默认脚本：

      * 从 `/libs/sling/servlet/errorhandler/`
      * 至`/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**不要**&#x200B;更改`/libs`路径中的任何内容。
>
>原因是下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>对于配置和其他更改：
>
>1. 将`/libs`中的项目复制到`/apps`
>1. 在`/apps`中进行任何更改

## 何时使用JCR查询以及何时不使用它们 {#when-to-use-jcr-queries-and-when-not-to-use-them}

正确应用时，JCR查询是一个功能强大的工具。 它们适用于：

* 真正的最终用户查询，例如对内容进行全文搜索。
* 在整个存储库中必须找到结构化内容的情况。

  在这种情况下，请确保仅在需要时运行查询。 例如，在组件激活或缓存失效时（与工作流步骤、触发内容修改的事件处理程序和过滤器等相反）。

切勿将JCR查询用于纯渲染请求。 例如，JCR查询不适用于以下内容：

* 渲染导航
* 创建“前10个最新新闻项目”概述
* 显示内容项目计数

要呈现内容，请使用对内容树的导航访问权限，而不是执行JCR查询。

>[!NOTE]
>
>如果您使用[查询生成器](/help/sites-developing/querybuilder-api.md)，则使用JCR查询，因为查询生成器会在幕后生成JCR查询。
>

## 安全性注意事项 {#security-considerations}

>[!NOTE]
>
>参考[安全核对清单](/help/sites-administering/security-checklist.md)也是值得的。

### JCR（存储库）会话 {#jcr-repository-sessions}

使用用户会话，而不是管理会话。 这意味着您应该使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### 防止跨站点脚本(XSS) {#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)允许攻击者将代码注入其他用户查看的网页。 恶意Web用户可以利用此安全漏洞绕过访问控制。

AEM应用了在输出时筛选所有用户提供的内容的原则。 在开发和测试过程中，防御XSS都被列为最高优先事项。

此外，Web应用程序防火墙（如Apache的[mod_security](https://modsecurity.org)）可以对部署环境的安全提供可靠的集中控制，并保护用户免受以前未检测到的跨站点脚本攻击。

>[!CAUTION]
>
>随AEM提供的示例代码本身可能无法抵御此类攻击，通常依赖于Web应用程序防火墙进行的请求过滤。

XSS API备忘表包含您必须了解的信息，以便使用XSS API并使AEM应用程序更加安全。 您可以在此处下载它：

XSSAPI备忘单。

[获取文件](assets/xss_cheat_sheet_2016.pdf)

### 保护机密信息的通信 {#securing-communication-for-confidential-information}

对于任何Internet应用程序，在传输机密信息时，请确保

* 通过SSL保护流量
* 如果适用，则使用HTTP POST

这适用于系统机密的信息（如配置或管理访问权限）以及用户机密的信息（如个人详细信息）

## 不同的开发任务 {#distinct-development-tasks}

### 自定义错误页面 {#customizing-error-pages}

可以为AEM自定义错误页面。 建议这样做，以便实例不会显示内部服务器错误上的Sling跟踪。

有关完整详细信息，请参阅[自定义错误处理程序显示的错误页面](/help/sites-developing/customizing-errorhandler-pages.md)。

### 在Java™进程中打开文件 {#open-files-in-the-java-process}

由于AEM可以访问许多文件，因此建议为AEM明确配置Java™进程[&#128279;](/help/sites-deploying/configuring.md#open-files-in-the-java-process)的打开文件数。

为了最大限度地减少此问题，开发应确保在（有意义的）可能时正确关闭任何打开的文件。
