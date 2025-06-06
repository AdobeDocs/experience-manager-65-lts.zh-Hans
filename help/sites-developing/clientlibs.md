---
title: 使用客户端库
description: AEM提供了客户端库文件夹，通过该文件夹，您可以在存储库中存储客户端代码，将其划分为不同类别，并定义何时以及如何向客户端提供每种类别的代码
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: cafc7120-114e-487a-8b81-9c695318731e
source-git-commit: a061c19dcb883b94ee61be21459c46e21eaf696a
workflow-type: tm+mt
source-wordcount: '2791'
ht-degree: 1%

---

# 使用客户端库{#using-client-side-libraries}

现代网站在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了&#x200B;**客户端库文件夹**，可让您将客户端代码存储在存储库中，将其按类别整理，并定义何时以及如何向客户端提供每种类别的代码。 然后，客户端库系统负责在最终网页中产生正确的链接，以加载正确的代码。

## AEM中客户端库的工作原理 {#how-client-side-libraries-work-in-aem}

在页面的HTML中包含客户端库（即，JS或CSS文件）的标准方法是，在该页面的JSP中包含`<script>`或`<link>`标记，并包含相关文件的路径。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

虽然此方法在AEM中有效，但当页面及其组成组件变得复杂时，它可能会导致问题。 在这种情况下，最终HTML输出中可能会包含同一JS库的多个副本。 为避免这种情况并允许对客户端库进行逻辑组织，AEM使用&#x200B;**客户端库文件夹**。

客户端库文件夹是`cq:ClientLibraryFolder`类型的存储库节点。 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html)中的定义为

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

默认情况下，`cq:ClientLibraryFolder`节点可以放置在存储库的`/apps`、`/libs`和`/etc`子树中的任意位置(这些默认值和其他设置可通过[系统控制台](https://localhost:4502/system/console/configMgr)的&#x200B;**Adobe Granite HTML库管理器**&#x200B;面板进行控制)。

每个`cq:ClientLibraryFolder`都填充了一组JS和/或CSS文件以及几个支持文件（见下文）。 `cq:ClientLibraryFolder`的属性配置如下：

* `categories`：标识此`cq:ClientLibraryFolder`内的JS和/或CSS文件集所属的类别。 `categories`属性是多值属性，它允许库文件夹成为多个类别的一部分（请参阅下面的内容，了解其用处）。

* `dependencies`：这是此库文件夹所依赖的其他客户端库类别的列表。 例如，在给定两个`cq:ClientLibraryFolder`节点`F`和`G`的情况下，如果`F`中的某个文件需要`G`中的另一个文件才能正常工作，则`G`的`categories`中至少有一个应属于`F`的`dependencies`中。

* `embed`：用于嵌入来自其他库的代码。 如果节点F嵌入节点G和H，则生成的HTML将是来自节点G和H的内容集。
* `allowProxy`：如果客户端库位于`/apps`下，则此属性允许通过代理servlet访问它。 请参阅下面的[查找客户端库文件夹并使用代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

## 引用客户端库 {#referencing-client-side-libraries}

由于HTL是开发AEM站点的首选技术，因此应使用HTL在AEM中包含客户端库。 但是，也可以使用JSP执行此操作。

### 使用HTL {#using-htl}

在HTL中，通过AEM提供的帮助程序模板来加载客户端库，该模板可通过[`data-sly-use`](https://helpx.adobe.com/cn/experience-manager/htl/using/block-statements.html#use)访问。 此文件中有三个可用的模板，可以通过[`data-sly-call`](https://helpx.adobe.com/cn/experience-manager/htl/using/block-statements.html#template-call)来调用它们：

* **css** — 仅加载引用的客户端库的CSS文件。
* **js** — 仅加载引用的客户端库的JavaScript文件。
* **all** — 加载引用的客户端库的所有文件(CSS和JavaScript)。

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

有关详细信息和使用示例，请参阅文档[HTML模板语言快速入门](https://helpx.adobe.com/cn/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

将`ui:includeClientLib`标记添加到您的JSP代码中，以便在生成的HTML页面中添加指向客户端库的链接。 要引用库，请使用`ui:includeClientLib`节点的`categories`属性的值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，`/etc/clientlibs/foundation/jquery`节点的类型为`cq:ClientLibraryFolder`，类别属性的值为`cq.jquery`。 JSP文件中的以下代码引用了库：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML页包含以下代码：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有关完整信息（包括用于筛选JS、CSS或主题库的属性），请参阅[ui：includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`以前常用于包含客户端库，但自AEM 5.6以来已弃用。应改用[`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib)，如上所述。

## 创建客户端库文件夹 {#creating-client-library-folders}

创建一个`cq:ClientLibraryFolder`节点以定义JavaScript和层叠样式表库并将它们提供给HTML页面。 使用节点的`categories`属性标识它所属的库类别。

该节点包含一个或多个在运行时合并到单个JS和/或CSS文件中的源文件。 生成的文件的名称是具有`.js`或`.css`文件扩展名的节点名称。 例如，名为`cq.jquery`的库节点会生成名为`cq.jquery.js`或`cq.jquery.css`的文件。

客户端库文件夹包含以下项目：

* 要合并的JS和/或CSS源文件。
* 支持CSS样式的资源，如图像文件。

  **注意：**&#x200B;您可以使用子文件夹来组织源文件。
* 一个`js.txt`文件和/或一个`css.txt`文件，用于标识要合并到生成的JS和/或CSS文件中的源文件。

![clientlibarch](assets/clientlibarch.png)

有关特定于小组件的客户端库要求的信息，请参阅[使用和扩展小组件](/help/sites-developing/widgets.md)。

Web客户端必须具有访问`cq:ClientLibraryFolder`节点的权限。 您还可以从存储库的安全区域公开库（请参阅下面的嵌入其他库的代码）。

### 覆盖/lib中的库 {#overriding-libraries-in-lib}

位于`/apps`下方的客户端库文件夹优先于`/libs`中类似的同名文件夹。 例如，`/apps/cq/ui/widgets`优先于`/libs/cq/ui/widgets`。 当这些库属于同一类别时，将使用`/apps`以下的库。

### 查找客户端库文件夹并使用代理客户端库Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客户端库文件夹位于存储库中的`/etc/clientlibs`下方。 这仍受支持，但建议客户端库现在位于`/apps`下。 这是为了在其他脚本附近找到客户端库，这些脚本通常位于`/apps`和`/libs`下方。

>[!NOTE]
>
>客户端库文件夹下的静态资源必须位于名为&#x200B;*resources*&#x200B;的文件夹中。 如果文件夹&#x200B;*资源*&#x200B;下没有静态资源（如图像），则无法在发布实例上引用该资源。 示例如下： https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>为了更好地将代码与内容和配置隔离，建议在`/apps`下找到客户端库，并使用`allowProxy`属性通过`/etc.clientlibs`公开它们。

为了能够访问`/apps`下的客户端库，使用了代理servlet。 仍在客户端库文件夹上强制执行ACL，但如果`allowProxy`属性设置为`true`，则servlet允许通过`/etc.clientlibs/`读取内容。

如果静态资源位于客户端库文件夹下的资源下，则只能通过代理访问。

例如：

* 您在`/apps/myprojects/clientlibs/foo`中有一个clientlib
* 您在`/apps/myprojects/clientlibs/foo/resources/icon.png`中有一个静态图像

然后，将`foo`上的`allowProxy`属性设置为true。

* 然后，您可以请求`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然后，您可以通过`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`引用图像

>[!CAUTION]
>
>在使用代理的客户端库时，AEM Dispatcher配置可能需要更新，以确保允许使用扩展客户端库的URI。

>[!CAUTION]
>
>Adobe建议查找`/apps`下的客户端库，并使用代理servlet使其可用。 但是，请记住，最佳做法仍然要求公共站点从不包含直接通过`/apps`或`/libs`路径提供的任何内容。

### 创建客户端库文件夹 {#create-a-client-library-folder}

1. 在Web浏览器([https://localhost:4502/crx/de](https://localhost:4502/crx/de))中打开CRXDE Lite。
1. 选择要在其中找到客户端库文件夹的文件夹，然后单击&#x200B;**创建>创建节点**。
1. 输入库文件的名称，然后在类型列表中选择`cq:ClientLibraryFolder`。 单击&#x200B;**确定**，然后单击&#x200B;**全部保存**。
1. 要指定库所属的类别，请选择`cq:ClientLibraryFolder`节点，添加以下属性，然后单击&#x200B;**全部保存**：

   * 名称：类别
   * 类型：字符串
   * 值：类别名称
   * 多：选择

1. 以任何方式将源文件添加到库文件夹中。 例如，使用WebDav客户端复制文件，或创建文件并手动创作内容。

   **注意：**&#x200B;如果需要，您可以在子文件夹中组织源文件。

1. 选择客户端库文件夹，然后单击&#x200B;**创建>创建文件**。
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”：

   * **`js.txt`：**&#x200B;使用此文件名生成JavaScript文件。
   * **`css.txt`：**&#x200B;使用此文件名生成层叠样式表。

1. 打开文件并键入以下文本以标识源文件路径的根：

   `#base=*[root]*`

   将* `[root]`*替换为包含源文件的文件夹相对于TXT文件的路径。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：

   `#base=.`

   以下代码将根设置为`cq:ClientLibraryFolder`节点下名为mobile的文件夹：

   `#base=mobile`

1. 在`#base=[root]`下面的行中，键入源文件相对于根的路径。 将每个文件名放在单独的一行中。
1. 单击&#x200B;**全部保存**。

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，将其他库标识为依赖项。 在JSP中，引用客户端库文件夹的`ui:includeClientLib`标记会导致HTML代码包含指向生成的库文件和依赖项的链接。

依赖项必须是另一个`cq:ClientLibraryFolder`。 要识别依赖关系，请使用以下属性向您的`cq:ClientLibraryFolder`节点添加属性：

* **名称：**&#x200B;依赖项
* **类型：**&#x200B;字符串[]
* **值：**&#x200B;当前库文件夹所依赖的cq：ClientLibraryFolder节点的categories属性值。

例如，/ `etc/clientlibs/myclientlibs/publicmain`依赖于`cq.jquery`库。 引用主客户端库的JSP将生成包含以下代码的HTML：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 嵌入来自其他库的代码 {#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到另一个客户端库中。 在运行时，生成的嵌入库的JS和CSS文件包含嵌入库的代码。

嵌入代码可用于提供对存储在存储库安全区域中的库的访问权限。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最佳做法是将应用程序文件夹中所有与应用程序相关的文件保留在`/apps`以下。 拒绝网站访客访问`/apps`文件夹也是最佳实践。 为满足这两个最佳实践，请在`/apps`下创建一个客户端库文件夹，并使其可通过[查找客户端库文件夹和使用代理客户端库Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)中所述的代理servlet访问。

使用类别属性可标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性将属性添加到嵌入`cq:ClientLibraryFolder`节点：

* **名称：**&#x200B;已嵌入
* **类型：**&#x200B;字符串[]
* **值：**&#x200B;要嵌入的`cq:ClientLibraryFolder`节点的categories属性值。

#### 使用嵌入以最大限度地减少请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现发布实例为典型页面生成的最终HTML包含相对大量的`<script>`元素，特别是当您的网站正在使用客户端上下文信息进行分析或定位时。 例如，在非优化项目中，您可能会在HTML中找到以下页面的`<script>`元素系列：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在这种情况下，有必要将所有所需的客户端库代码合并到单个文件中，以便减少页面加载上的来回请求数量。 为此，您可以使用`cq:ClientLibraryFolder`节点的嵌入属性，将所需的库`embed`到特定于应用程序的客户端库中。

AEM中包含以下客户端库类别。 您应该仅嵌入运行特定站点所需的那些项目。 但是，**您应该保持此处列出的顺序**：

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源路径。 例如，可公开访问的库`/etc/client/libraries/myclientlibs/publicmain`嵌入了`/apps/myapp/clientlib`客户端库：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

`main.css`文件包含以下样式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain`节点生成的CSS文件包含以下样式（使用原始图像的URL）：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 将库用于特定移动组 {#using-a-library-for-specific-mobile-groups}

使用客户端库文件夹的`channels`属性来标识使用该库的移动组。 当针对不同的设备功能设计相同类别的库时，`channels`属性非常有用。

要将客户端库文件夹与设备组关联，请将具有以下属性的属性添加到您的`cq:ClientLibraryFolder`节点：

* **名称：**&#x200B;个频道
* **类型：**&#x200B;字符串[]
* **值：**&#x200B;移动组的名称。 要从组中排除库文件夹，请在名称前面添加感叹号(“！”)。

例如，下表列出了`cq.widgets`类别中每个客户端库文件夹的`channels`属性的值：

| 客户端库文件夹 | 渠道属性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 使用预处理器 {#using-preprocessors}

AEM允许可插拔的预处理器，并随附对CSS和JavaScript的[YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)和JavaScript的[Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/)的支持，并将YUI设置为AEM的默认预处理器。

可插拔预处理器允许灵活使用，包括：

* 定义可以处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩减，也可用于非缩小的情况
* 客户端库可以定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩器。 有关已知问题的列表，请参阅[YUI压缩器GitHub文档](https://github.com/yui/yuicompressor/issues)。 针对特定客户端库切换到GCC压缩程序可能会解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>不要将缩小的库放入客户端库中。 而是应提供Raw库，如果需要缩减，请使用预处理器的选项。

### 用途 {#usage}

您可以选择为每个客户端库或系统范围配置预处理器配置。

* 在clientlibrary节点上添加多值属性`cssProcessor`和`jsProcessor`

* 或通过&#x200B;**系统库管理器** OSGi配置定义HTML默认配置

clientlib节点上的预处理器配置优先于OSGI配置。

### 格式和示例 {#format-and-examples}

#### 格式化 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### 用于CSS缩小和GCC用于JS的YUI压缩器 {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 使用Typescript进行预处理，然后使用GCC进行缩小和模糊处理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC选项 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有关GCC选项的更多详细信息，请参阅[GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 设置系统默认缩小器 {#set-system-default-minifier}

在AEM中，YUI被设置为默认缩小器。 要将其更改为GCC，请执行以下步骤。

1. 转到[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)上的Apache Felix配置管理器
1. 查找并编辑&#x200B;**Adobe Granite HTML库管理器**。
1. 启用&#x200B;**最小化**&#x200B;选项（如果尚未启用）。
1. 将&#x200B;**JS处理器默认配置**&#x200B;的值设置为`min:gcc`。

   如果用分号分隔，例如`min:gcc;obfuscate=true`，则可以传递选项。

1. 单击&#x200B;**保存**&#x200B;即可保存更改。

## 调试工具 {#debugging-tools}

AEM提供了几种用于调试和测试客户端库文件夹的工具。

### 请参阅嵌入的文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库产生预期的结果，您可以查看运行时嵌入的文件的名称。 要查看文件名，请将`debugClientLibs=true`参数附加到网页的URL。 生成的库包含`@import`语句，而不是嵌入的代码。

在上一个[嵌入来自其他库的代码](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)部分的示例中，`/etc/client/libraries/myclientlibs/publicmain`客户端库文件夹嵌入了`/apps/myapp/clientlib`客户端库文件夹。 将参数附加到网页会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开`publicmain.css`文件将显示以下代码：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL：

   `?debugClientLibs=true`
1. 加载页面时，查看页面源。
1. 单击提供为链接元素的href链接，以打开文件并查看源代码。

### 发现客户端库 {#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`组件生成系统上所有客户端库文件夹的信息页面。 `/libs/granite/ui/content/dumplibs`节点将组件作为资源类型。 要打开该页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

该信息包括库路径和类型（CSS或JS）以及库属性的值（如类别和依赖项）。 页面上的后续表将显示每个类别和渠道中的库。

### 查看生成的输出 {#see-generated-output}

`dumplibs`组件包括一个测试选择器，该选择器显示为`ui:includeClientLib`标记生成的源代码。 该页面包含用于不同js、css和主题属性组合的代码。

1. 使用以下方法之一打开“测试输出”页：

   * 从`dumplibs.html`页面，单击&#x200B;**单击此处进行输出测试**&#x200B;文本中的链接。

   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）：

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   默认页面显示没有categories属性值的标记的输出。

1. 要查看类别的输出，请键入客户端库的`categories`属性的值，然后单击&#x200B;**提交查询**。

## 配置用于开发和生产的库处理 {#configuring-library-handling-for-development-and-production}

HTML Library Manager服务在运行时处理`cq:ClientLibraryFolder`标记并生成库。 环境、开发或生产的类型决定了应如何配置服务：

* 提高安全性：禁用调试
* 提高性能：删除空白并压缩库。
* 提高可读性：包含空格而不压缩。

有关配置服务的信息，请参阅[AEM HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
