---
title: 'Foundation 组件 '
description: 了解Adobe Experience Manager 6.5中的基础组件。
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: c507bef7-4ddc-4e8c-9947-71cb2ecbbf0a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '6846'
ht-degree: 4%

---

# Foundation 组件  {#foundation-components}

>[!CAUTION]
>
>AEM 6.5弃用了大多数基础组件。Adobe建议在AEM项目中使用更新颖、可扩展的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。 这些组件是[We.Retail示例内容](/help/sites-developing/we-retail.md)的一部分，也可以[单独安装并由管理员用于开发](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=zh-Hans)。
>
>您可以使用[AEM Modernize Tools Suite](https://opensource.adobe.com/aem-modernize-tools/)重构基于基础组件的站点以使用核心组件。

基础组件设计为可在创作标准网页的内容时使用。 它们构成了AEM标准安装中现成可用的组件子集。

有些可通过组件浏览器立即使用。 还可以使用[设计模式](/help/sites-authoring/default-components-designmode.md)（如果页面基于静态模板）或[编辑模板](/help/sites-authoring/templates.md)（如果页面基于可编辑模板）来使用其他各种模式。

基础组件的使用受支持，但它们大部分已被弃用，并被提供了更多可扩展性和灵活性的核心组件取代。

>[!NOTE]
>
>此部分仅讨论在标准 AEM 安装中现成可用的组件。
>
>根据您的实例，您可能已针对您的要求明确开发了自定义组件。 这些自定义组件甚至可能具有与此处讨论的某些组件相同的名称。

[编辑页面](/help/sites-authoring/editing-content.md)时，可以在页面编辑器侧面板上的&#x200B;**组件**&#x200B;选项卡中使用组件。

您可以选择一个组件，并将其拖动到页面上的所需位置。然后，可以使用下列方法编辑该组件：

* [配置属性](/help/sites-authoring/editing-page-properties.md)
* [编辑内容](/help/sites-authoring/editing-content.md)

* [编辑内容 – 全屏模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

组件根据称为组件组的各种类别进行排序，包括：

* [常规](#general)：包含基本组件，包括文本、图像、表格和图表。
* [列](#columns)：包含组织内容布局所需的组件。
* [表单](#formgroup)：包含创建表单所需的所有组件。

## 常规 {#general}

常规组件是用于创建内容的基本组件。

### 帐户项 {#account-item}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)。

您可以定义带有标题和描述的链接。

![chlimage_1-88](assets/chlimage_1-88.png)

### 自适应图像 {#adaptive-image}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[图像核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=zh-Hans)。

自适应图像基础组件生成大小适合打开网页的窗口的图像。 要使用该组件，需从文件系统或DAM提供图像资源。 当打开网页时，Web浏览器下载已调整大小的图像的副本，以使其适合当前窗口。

以下特性可确定窗口的大小：

* 设备屏幕：移动设备通常显示网页，以便它们在整个屏幕中扩展。
* Web浏览器窗口大小：便携式计算机和台式计算机的用户可以调整Web浏览器窗口的大小。

例如，当网页在手机上打开时，组件生成小图像，当在平板电脑上打开时，组件生成中等大小的图像。 在笔记本电脑上，组件会在页面在最大化的Web浏览器中打开时创建并传递大图像。 当Web浏览器调整大小以适合屏幕的一部分时，组件通过交付较小的图像来适应并刷新视图。

#### 支持的图像格式 {#supported-image-formats}

您可以将以下文件扩展名的图像文件与自适应图像组件结合使用：

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>AEM不支持使用动画GIF文件进行自适应格式副本。

#### 图像大小和质量 {#images-sizes-and-quality}

下表列出了为给定视区宽度生成的图像宽度。 计算所生成图像的高度以保持不变的长宽比，并且图像边缘内不会出现空格。 可使用裁剪来避免留空格。

如果图像是JPEG图像，则视区大小也会影响JPEG质量。 可以使用以下JPEG特性：

* 低(0.42)
* Medium (0.82)
* 高(1.00)

| **视区宽度范围（像素）** | **图像宽度（像素）** | **JPEG品质** | **目标设备类型** |
|---|---|---|---|
| 宽度&lt;= 319 | 320 | 低 |  |
| 宽度= 320 | 320 | 中 | 手机（纵向） |
| 320 &lt;宽度&lt; 481 | 480 | 中 | 移动电话（横向） |
| 480 &lt;宽度&lt; 769 | 476 | 高 | 平板电脑（纵向） |
| 768 &lt;宽度&lt; 1025 | 620 | 高 | 平板电脑（横向） |
| 宽度&lt;= 1025 | 完整（原始大小） | 高 | 桌面 |

#### 属性 {#properties}

通过对话框，您可以编辑自适应图像组件实例的属性，其中许多属性与它所基于的图像组件相同。 这些属性位于两个选项卡中：

* **图像**

   * **图像**
从内容查找器中拖动图像，或单击以打开可在其中加载图像的浏览窗口。 加载图像后，您可以裁切、旋转或删除图像。 要放大和缩小图像，请使用图像下方的滑动条（在“确定”和“取消”按钮上方）

   * **裁切**
剪切图像的部分。 拖动边框以裁切图像。

   * **旋转**
反复单击“旋转”，直到根据需要旋转图像为止。

   * **清除**
删除当前图像。

* **高级**

   * **标题**
自适应图像组件不使用此属性。

   * **替换文本**
用于图像的替换文本。

   * **链接到**
自适应图像组件不使用此属性。

   * **描述**
自适应图像组件不使用此属性。

### 轮盘 {#carousel}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[轮盘核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=zh-Hans)。

利用轮盘组件，可显示与各个页面关联的图像：

* 一次一个
* 短时间
* 按照您指定的顺序
* 具有您指定的时间延迟

可单击的控件还允许用户根据需要实时循环显示页面。 选择当前可见的页面图像会将您转到该页面。 换句话说，轮播充当导航控件。

#### 属性 {#properties-1}

这些属性位于两个选项卡中：

* **轮播**
您可以在此处指定轮播的运行方式：

   * 播放速度
显示下一张幻灯片之前的时间（以毫秒为单位）。
   * 过渡时间
两张幻灯片之间的过渡时间（毫秒）。
   * 控件样式
下拉菜单中提供了各种选项；例如“上一个/下一个按钮”、“右上切换”。

* **列表**

  在此，您可以指定在轮播中包含页面的方式：

   * **生成列表使用**
可通过多种方法来构建页面列表 — 子页面、固定列表、搜索或高级搜索（均如下所述）。
无论您选择哪种方法，您包含在列表中的页面都应当已经有一个与页面关联的图像。 轮播中显示的就是此图像。 如果给定页面的页面属性下没有图像，则应在开始之前将图像与页面关联。 否则，轮播会显示一个主要为空白的页面。 请参阅[编辑页面属性](/help/sites-authoring/editing-page-properties.md)。
根据您选择的项目，将显示一个新面板：

      * 子页面的&#x200B;**选项**

         * **父页面**
手动或使用选择器指定路径。 留空将使用当前页面作为父页面。

      * 固定列表的&#x200B;**选项**

         * **页**
选择页面列表。 使用`+`添加更多条目，使用“向上”/“向下”按钮调整顺序。

      * **搜索选项**

         * **开始于**
手动或使用选择器输入起始路径。

         * **搜索查询**
您可以输入纯文本搜索查询。

      * 高级搜索的&#x200B;**选项**

         * **Querybuilder谓词表示法**
您可以使用Querybuilder谓词表示法输入搜索查询。 例如，您可以输入“fulltext=Marketing”，以使其内容中包含“Marketing”的所有页面都显示在轮播中。
有关查询表达式和更多示例的完整讨论，请参阅[QueryBuilder API](/help/sites-developing/querybuilder-api.md)。

   * **排序依据**
从下拉菜单中选择`jcr:title`、`jcr:created`、`cq:lastModified`或`cq:template`。

   * **限制**
可选。 要在轮播中使用的项目的最大数量。

>[!NOTE]
>
>您可以为Adobe Experience Manager创建一个自定义轮播组件，该组件在AEM DAM中显示数字资源。 请参阅[为Adobe Experience Manager创建自定义轮播组件](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)。

### 图表 {#chart}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

图表组件允许您添加条形图、折线图或饼图。 AEM会根据您提供的数据创建一个图表。 提供数据的方法是直接在“数据”选项卡中键入内容，或者复制并粘贴电子表格。

* **数据**

   * **图表数据**
使用CSV格式输入图表数据；逗号分隔值格式使用逗号(“，”)作为字段分隔符。

* **高级**

   * **图表类型**
从饼图、折线图和条形图中选择。

   * **替换文本**
显示替换文本而不是图表。

   * **宽度**
图表的宽度（像素）。

   * **高度**
图表的高度（像素）。

下面显示了一个图表数据示例，其后是生成的条形图：

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
>
>您可以创建一个自定义AEM图表控件，以在AEM JCR中显示数据。 有关信息，请参阅[在图表中显示Adobe Experience Manager数据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)。

### 内容片段 {#content-fragment}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)。

[内容片段](/help/sites-authoring/content-fragments.md)已创建并管理为独立于页面的资产。 您随后可以在创作内容页面时使用这些片段及其变体。

### 设计导入程序 {#design-importer}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

利用此组件，可上传包含设计包的zip文件。

### 下载 {#download}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

下载组件在选定网页上创建一个链接，用于下载特定文件。 您可以从内容查找器拖动资产或上传文件。

* **下载**

   * **描述**
与下载链接一起显示的简短描述。

   * **文件**
可在生成的网页上下载的文件。 从内容查找器中拖动资产或选择区域，以便您可以上传可供下载的文件。

以下示例显示了Geometrixx中的下载组件：

![dc_download_use](assets/dc_download_use.png)

### 外部 {#external}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

外部应用程序集成组件(**External**)允许您使用iframe将外部应用程序嵌入到AEM页面。

* **外部**

   * **目标应用程序**
指定要集成的Web应用程序的URL；例如：

     ```
     https://en.wikipedia.org/wiki/Main_Page
     ```

   * **传递参数**
选中方框，以便在需要时向应用程序传递参数。

   * **宽度和高度
**定义iframe的大小

外部应用程序已集成到AEM页面的段落系统中；例如，使用`https://en.wikipedia.org/wiki/Main_Page`的Target应用程序时：

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>根据您的使用情形，其他选项可用于集成外部应用程序，例如[集成Portlet](/help/sites-administering/aem-as-portal.md)。

### 闪光灯 {#flash}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

Flash组件允许您加载Flash影片。 您可以将Flash资源从内容查找器拖到组件上，也可以使用对话框：

* **闪存**

   * **Flash电影**

     Flash影片文件。 从内容查找器中拖动资产，或单击以打开浏览窗口。

   * **大小**

     存放影片的显示区域的尺寸（以像素为单位）。

* **备用图像**

  要显示的替代图像

* **高级**

   * **上下文菜单**

     指示应显示还是隐藏上下文菜单。

   * **窗口模式**

     窗口的显示方式，例如，不透明、透明或作为不同的（实心）窗口。

   * **背景颜色**

     从提供的颜色图表中选择的背景颜色。

   * **最低版本**

     运行电影所需的最低版本的Adobe Flash Player。 默认值为9.0.0。

   * **属性**

     需要任何其它属性。

### 图像 {#image}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[图像核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=zh-Hans)。

图像组件根据指定的参数显示图像和随附文本。

您可以上传图像，然后对其进行编辑和处理（例如，裁切、旋转、添加链接/标题/文本）。

您可以从[Assets浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)将图像直接拖放到组件或其[配置对话框](/help/sites-authoring/editing-content.md#component-edit-dialog)上。 您还可以从“配置”对话框上传图像；此对话框还控制图像的所有定义和操作：

![chlimage_1-91](assets/chlimage_1-91.png)

上传图像后（而不是之前），您可以根据需要使用[就地编辑](/help/sites-authoring/editing-content.md#edit-content)裁切/旋转图像：

![就地编辑工具栏](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>就地编辑器在编辑时使用图像的原始大小和纵横比。 您还可以指定高度和宽度属性。 在保存编辑更改时，将应用属性中定义的任何大小和纵横比限制。
>
>根据您的实例，页面[&#128279;](/help/sites-developing/designer.md)的设计也可能施加最小和最大限制。 这些限制是在项目实施期间制定的。

全屏编辑模式中提供了多个其他选项；例如，映射和缩放：

![全屏编辑模式 — 映射和缩放](do-not-localize/chlimage_1-16.png)

>[!NOTE]
>
>无法使用Internet Explorer监视上载进度。
>
>Internet Explorer用户必须上传图像并单击&#x200B;**确定**，然后重新打开图像以在预览中查看上传的文件，并能够执行修改（即裁切）。
>
>有关AEM使用的HTML5功能的更多信息，请参阅[认证平台](/help/release-notes/release-notes.md#certifiedplatforms)部分。

加载图像时，可以配置以下内容：

* **映射**

  要映射图像，请选择映射。 您可以指定创建图像映射的方式（矩形、多边形等）以及区域应指向的位置。

* **裁切**

  要剪下图像的一部分，请选择裁切。 使用鼠标裁切图像。

* **旋转**

  要旋转图像，请选择旋转。 重复使用，直到图像以您想要的方式旋转。

* **清除**

  删除当前图像。

* **标题**

  图像的标题。

* **替换文本**

  创建无障碍内容时使用的替换文本。

* **链接到**

  创建指向网站内资产或其他页面的链接。

* **描述**

  图像的描述。

* **大小**

  设置图像的高度和宽度。

>[!NOTE]
>
>某些选项仅在全屏编辑器中可用。

最终图像（具有&#x200B;**标题**&#x200B;和&#x200B;**描述**）可以显示为：

![chlimage_1-92](assets/chlimage_1-92.png)

### 布局容器 {#layout-container}

此组件提供了一个网格段落系统，允许您在[响应式网格](/help/sites-authoring/responsive-layout.md)中添加和放置组件。 您可以根据目标设备的宽度（包括各种手机、平板电脑和桌面）定义不同的内容布局。

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
>
>此组件已使用[HTML模板语言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hans)实施。

### 列表 {#list}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[列表核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=zh-Hans)。

利用列表组件，可配置用于显示列表的搜索条件：

* **列表**

   * **生成列表使用**

     在此，您可以指定列表检索其内容的位置。 有多种方法：

   * 根据您选择的项目，将显示一个新面板：

      * 子页面的&#x200B;**选项**

         * **的**&#x200B;子项（父页面）

           手动或使用选择器指定路径。 留空将使用当前页面作为父页面。

      * 固定列表的&#x200B;**选项**

         * **页**

           选择页面列表。 使用+添加更多条目，使用上/下按钮调整顺序。

      * **搜索选项**

         * 开始

           手动或使用选择器输入起始路径。

         * 搜索查询

           您可以输入纯文本搜索查询。

      * 高级搜索的&#x200B;**选项**

         * **Querybuilder谓词表示法**

           您可以使用Querybuilder谓词表示法输入搜索查询。 例如，您可以输入“fulltext=Marketing”，以使其内容中包含“Marketing”的所有页面都显示在轮播中。

           有关查询表达式和更多示例的完整讨论，请参阅[QueryBuilder API](/help/sites-developing/querybuilder-api.md)。

      * **标记**

        指定&#x200B;**父页面**、**标记/关键字**&#x200B;以及所需的匹配条件。

   * **显示为**

     您希望如何列出这些项目；包括链接、Teaser和新闻。

   * **排序依据**

     是否对列表进行排序，如果是，则为排序使用的标准。 您可以输入条件，也可以从提供的下拉列表中选择一个条件。

   * **限制**

     指定要在列表中显示的项目的最大数量。

   * **启用信息源**

     指示是否应为列表激活RSS馈送。

   * **在**&#x200B;后分页

     在此处，您可以指定要一次显示的列表项数量。 具有比指定更多项目的列表使用分页将列表分为多个部分。

以下示例显示了&#x200B;**List**&#x200B;组件显示子页面列表的方式（设计受网站设计的自定义CSS定义控制）。

![dc_list_use](assets/dc_list_use.png)

### 登录 {#login}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

提供用户名和密码字段。

![chlimage_1-94](assets/chlimage_1-94.png)

您可以配置：

* 登录

   * 区域标签

     输入字段的导入文本。

   * 用户名标签

     用于标记用户名字段的文本。

   * 密码标签

     用于标记密码字段的文本。

   * “登录”按钮标签

     登录按钮的文本。

   * 重定向到

     您可以在网站上指定用户登录后应打开的页面。

* 已登录

   * “继续”按钮标签

     用于指示用户已登录的文本。

### 订单状态 {#order-status}

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

* **标题**

   * **标题**

     指定要显示的标题文本。

   * **链接**

     指定应显示订单状态的页面（产品）。

   * **类型/大小**

     从提供的选择中选择。

![chlimage_1-95](assets/chlimage_1-95.png)

### 引用 {#reference}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hans)。

通过&#x200B;**引用**&#x200B;组件，您可以引用AEM网站其他页面（在当前实例中）的文本。 然后，引用的段落的内容会像在当前页面上一样显示。 当源段落发生更改（可能需要页面刷新）时，内容会更新。

* **段落引用**

   * **引用**

     指定要引用的页面和段落的路径（包括内容）。

要指定段落的路径，必须在（页面的）路径后添加以下内容：

`.../jcr:content/par/<paragraph-ID>`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

除了引用特定段落之外，还可以修改路径以指定整个段落系统。 您可以通过以下方式为路径添加后缀来执行此引用：

`/jcr:content/par`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

配置后，内容将与源页面上完全一致。 只有在打开组件进行编辑时，才会看到它是引用：

![chlimage_1-96](assets/chlimage_1-96.png)

### 搜索 {#searching}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[快速搜索核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/quick-search.html?lang=zh-Hans)。

搜索组件可为页面添加搜索功能。

您可以配置：

* 搜索

   * **节点类型**

     如果将搜索限制到特定节点类型，请在此处列出它们；例如，`cq:Page`。

   * **在**&#x200B;中搜索的路径

     指定要搜索的分支的根页面。

   * **搜索按钮文本**

     实际搜索按钮上显示的名称。

   * **统计文本**

     搜索结果上方显示的文本。

   * **没有结果文本**

     如果没有结果，将显示此处输入的文本。

   * **拼写检查文本**

     如果某人输入了类似的词语，则此文本会在该词语之前显示。
例如，如果您键入`Geometrixxe`，则系统显示“您的意思是？ Geometrixx”。

   * **类似的页面文本**

     在类似页面的结果旁边显示的文本。 要查看具有相似内容的页面，请单击此链接。

   * **相关搜索文本**

     旁边显示的文本将搜索相关术语和主题。

   * **搜索趋势文本**

     用户输入的搜索词上方的标题。

   * **结果页标签**

     此列表底部显示的文本，带有指向其他结果页面的链接。

   * **上一个标签**

     在指向以前的搜索页面的链接上显示的名称。

   * **下一个标签**

     在指向后续搜索页面的链接上显示的名称。

以下示例显示了从标准安装的根目录中搜索单词&#x200B;*`geometrixx`*&#x200B;之后的搜索组件。 它还说明了结果的分页：

![dc_search_use](assets/dc_search_use.png)

以下示例显示了一个拼写错误且不可用的搜索词：

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Sitemap {#sitemap}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[导航](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/navigation.html?lang=zh-Hans)、[语言导航](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/language-navigation.html?lang=zh-Hans)和[痕迹导航核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/breadcrumb.html?lang=zh-Hans)。

自动列出站点地图，该列表（默认设置）列出当前网站中的所有页面（作为活动链接）。 例如，提取显示：

![dc_sitemap_use](assets/dc_sitemap_use.png)

如有必要，您可以配置以下内容：

* **站点地图**

   * **根路径**

     列表开始位置的路径。

### 幻灯片放映 {#slideshow}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[轮盘核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=zh-Hans)。

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

通过此组件，您可以加载一系列要在页面上显示为幻灯片放映的图像。 您可以添加或删除图像并为每个图像分配标题。 在“高级”下，还可以指定显示区域的大小。

您可以配置：

* **张幻灯片**

   * **新幻灯片**

     您可以使用&#x200B;**添加**（和&#x200B;**删除**）按钮指定幻灯片选择。

   * **标题**

     根据需要指定标题。 标题覆盖在相应的幻灯片上。

* **高级**

   * **大小**

     以像素为单位指定宽度和高度。

幻灯片放映组件随后会按顺序重复显示每个幻灯片，并停留一小段时间，然后再淡入下一张幻灯片：

![dc_slideshow_use](assets/dc_slideshow_use.png)

### 表 {#table}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=zh-Hans)。

>[!NOTE]
>
>**Table** Foundation组件基于[富文本编辑器](/help/sites-authoring/rich-text-editor.md)，它与&#x200B;**[Text](#text)** Foundation组件一样。

**Table**&#x200B;组件已预配置为允许您构建、填充和格式化表。 使用该对话框，您可以通过以下任一方式配置表并创建内容：

* 从头开始
* 从外部编辑器（如Excel、OpenOffice和Notepad）复制和粘贴电子表格或表。

您可以使用内联编辑器对内容进行基本更改：

![dc_table](assets/dc_table.png)

在全屏模式下，您可以配置表布局：

![chlimage_1-97](assets/chlimage_1-97.png)

以下屏幕截图显示了表组件的示例；设计由特定于站点的CSS决定：

![dc_table_use](assets/dc_table_use.png)

### 标记云 {#tag-cloud}

标记云以图形方式显示应用于网站内内容的标记选择：

![dc_tagclouduse](assets/dc_tagclouduse.png)

配置标记云组件时，您可以指定：

* **要显示的标记**

  从中收集要显示的标记的位置。 从页面、具有所有子项或所有标记的页面中进行选择。

* **页面**

  选择要引用的页面。

* **标记上无链接**

  显示的标记是否应作为链接。

有关应用标记的详细信息，请访问[使用标记](/help/sites-authoring/tags.md)。

### 文本 {#text}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=zh-Hans)。

>[!NOTE]
>
>**Text** Foundation组件基于[富文本编辑器](/help/sites-authoring/rich-text-editor.md)，与&#x200B;**Table** Foundation组件一样。

文本组件允许您使用WYSIWYG编辑器输入文本块，该编辑器具有[富文本编辑器](/help/sites-authoring/rich-text-editor.md)提供的功能。 通过一系列图标可以设置文本的格式，包括字体特征、对齐方式、链接、列表和缩进。

![chlimage_1-98](assets/chlimage_1-98.png)

打开&#x200B;**配置**&#x200B;对话框时，您还可以设置：

* **分隔条**
* **文本样式**

格式化文本将显示在页面上。 实际设计取决于站点CSS：

![dc_text_use](assets/dc_text_use.png)

有关文本组件和富文本编辑器提供的功能的更多详细信息，请参阅[富文本编辑器](/help/sites-authoring/rich-text-editor.md)页。

#### 就地编辑 {#inplace-editing}

除了基于对话框的富文本编辑模式之外，AEM还提供[就地编辑](/help/sites-authoring/editing-content.md)，该模式允许直接编辑显示在页面布局中的文本。

### 文本与图像 {#text-image}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[图像](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=zh-Hans)和[文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=zh-Hans)。

文本和图像组件添加文本块和图像。 您还可以单独添加和编辑文本和图像。 有关详细信息，请参阅[Text](#text)和[Image](#image)组件。

![chlimage_1-99](assets/chlimage_1-99.png)

您可以配置：

* **组件样式** （**样式**）

  在此，您可以向左或向右对齐图像。 默认值是&#x200B;**左对齐**，图像在左对齐。

* **图像属性** （**高级图像属性**）

  用于指定以下内容：

   * **图像资源**

     上传所需的图像。

   * **标题**

     块的标题，由mouseover显示。

   * **替换文本**

     图像无法显示时要显示的替换文本。 如果留空，则使用标题。

   * **链接到**

     指定目标路径。

   * **描述**

     图像的描述。

   * **大小**

     设置图像的高度和宽度。

以下示例显示了一个文本图像组件，该组件以左对齐方式显示图像：

![dc_textimage_use](assets/dc_textimage_use.png)

### 标题 {#title}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[标题核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=zh-Hans)。

标题组件可以：

* 通过将“标题”字段留空来显示当前页面的名称。
* 显示您在“标题”字段中指定的文本。

您可以配置：

* **标题**

  如果要使用页面标题以外的名称，请在此处输入该名称。

* **链接**

  如果标题要作为链接运行，则为URI。

* **类型/大小**

  从下拉列表中选择小或大。 “小”作为图像生成。 “大”作为文本生成。

以下示例显示正在显示的&#x200B;**标题**&#x200B;组件；设计由特定于站点的CSS决定。

![dc_title_use](assets/dc_title_use.png)

### 视频 {#video}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件嵌入组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html?lang=zh-Hans)。

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

通过&#x200B;**Video**&#x200B;组件，可在页面上放置预定义的、现成的视频元素。

另请参阅[配置视频配置文件](/help/sites-administering/config-video.md#configuringvideoprofiles)以用于HTML5元素。

将组件的实例放置在页面上后，可以配置以下内容：

* 视频

   * **视频资产**

     上传或放置您的视频资产。

   * **大小**

     视频的本机大小（宽度x高度，以像素为单位）将显示在“大小”（见上文）旁边的框中。 如果要覆盖视频的本机尺寸，请在此处手动输入宽度和高度尺寸。 选择&#x200B;**确定**&#x200B;将关闭对话框。

>[!NOTE]
>
>支持的格式包括：
>
>* `.mp4`
>* `Ogg`
>* `FLV` （Flash视频）

## 列 {#columns}

列是一种在AEM中控制内容布局的机制。 在标准安装中，提供了用于创建两列或三列的组件。

以下示例显示了正在使用的两列组件。 可以将占位符用于新组件：

![dc_columncontroluse](assets/dc_columncontroluse.png)

### 2 列 {#columns-1}

列控件组件，默认使用两个相等的列。

### 3 列 {#columns-2}

列控件组件，默认为三个相等的列。

### 列控件 {#column-control}

列控件组件允许用户选择要如何将网页主面板中的内容拆分为多个列。 用户可以选择所需的列数（从预定义列表中），然后在每个列中创建、删除或移动内容。

* **列控件**

   * **列布局**

     选择要呈现的列数。 创建后，每个列都有自己的链接，用于在添加内容时拖动组件或资产。

## 表单 {#form}

>[!CAUTION]
>
>已弃用基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

表单组件用于创建表单，以供访客提交输入。 Forms和表单组件可用于收集包括用户反馈（例如客户满意度调查表）和用户信息（例如用户注册）的信息。

>[!NOTE]
>
>有关AEM Forms的信息，请参阅[AEM Forms帮助](/help/forms/using/introduction-aem-forms.md)。

Forms由几个不同的组件组成：

* **表单**

  表单组件定义页面上新表单的开始和结束。 然后，可以将其他组件置于这些元素（例如表格和下载）之间。

* **表单字段和元素**

  表单字段和元素可以包括文本框、单选按钮和图像。 用户通常会在表单字段中完成一项操作，例如键入文本。 有关更多信息，请参阅各个表单元素。

* **配置文件组件**

  配置文件组件与用于社交协作和其他需要访客个性化的区域的访客配置文件相关。

下面显示了一个示例表单。 它由&#x200B;**Form**&#x200B;组件（开始和结束）组成，其中两个&#x200B;**Form** **Text**&#x200B;字段用于输入，**General** **Text**&#x200B;字段用于潜在客户文本，以及&#x200B;**Submit**&#x200B;按钮。

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>有关开发和自定义表单的信息，请参阅[开发Forms页面](/help/sites-developing/developing-forms.md)。 此功能包括添加操作、约束、预加载字段以及使用脚本来调用服务到操作等。

### （许多）表单组件的通用设置 {#settings-common-to-many-form-components}

虽然每个表单组件的用途各不相同，但许多表单组件由类似的选项和参数组成。

配置任何表单组件时，对话框中提供以下选项卡：

* **标题和文本**

  在此，必须指定基本信息，例如表单的标题和任何随附文本。 在适当时，它还允许您定义其他关键信息，例如字段是否可多选，以及是否可供选择的项。

* **初始值**

  用于指定默认值。

* **约束**

  您可以在此指定是否需要某个字段并对该字段设置约束（例如，必须为数字）。

* **样式**

  指示字段的大小和样式。

>[!NOTE]
>
>您看到的字段因各个组件而存在显着差异。

这些选项卡为您提供了必要的参数。 这些选项卡可以取决于单个组件类型，但可包括以下内容：

* **标题和文本**

   * **元素名称**

     表单元素的名称。 它指示数据存储到存储库中的什么位置。
此字段为必填项，应当仅包含以下字符：

      * 字母数字字符
      * `_ . / : -`

   * **标题**

     与字段一起显示的标题。 如果留空，将显示默认标题。

   * **描述**

     允许您根据需要为用户提供其他信息。 在表单上，它以比标题小的字体显示在字段下方。

   * **显示/隐藏**

     确定字段何时可见。

* **初始值**

   * **默认值**

     打开表单时显示在字段中的值。 也就是说，在用户输入任何内容之前。

* **约束**

   * **必需**

     约束取决于表单组件类型，但提供一个或多个单击框以指示该字段是必填的或该字段的某些部分是必填的。

   * **必需消息**

     用于通知用户此字段为必填的消息。 必填字段还标有星号。

   * **约束**

     可供选择的约束取决于表单元件类型。

   * **约束消息**

     通知用户所需内容的消息。

* **样式**

   * **大小**

     在行和列中。

   * **宽度**

     按像素。

   * **CSS**

### 表单（组件） {#form-component}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单容器核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=zh-Hans)。

表单组件使用&#x200B;**表单开始**&#x200B;和&#x200B;**表单结束**&#x200B;元素定义表单的开始和结束。 开始位置和结束位置始终成对，以确保正确定义表单。

![dc_form-1](assets/dc_form-1.png)

在表单的开头和结尾之间，您可以添加表单组件，以定义用户的实际输入字段。

>[!NOTE]
>
>基础组件表单组件仅支持使用其他基础组件表单组件（按钮、文本、隐藏等）。 不支持在基础组件表单中使用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)表单组件（反之）。

#### 表单的开头 {#start-of-form}

此组件定义页面上新表单的开始。 您可以配置：

* **表单**

   * **感谢页面**

     要引用以感谢访客提供其输入的页面。 如果留空，表单会在提交后重新显示。

   * **启动工作流**

     确定在提交表单后触发的工作流。

* **高级**

   * **操作类型**

     表单需要操作。 操作定义根据用户提交的数据触发执行的操作(类似于HTML中的action= )。 某些客户需要相应的&#x200B;**操作配置**。
标准AEM安装中包含一系列操作类型：

      * **帐户请求**
      * **创建内容**
      * **创建潜在客户**
      * **创建和更新帐户**
      * **电子邮件服务：创建订阅者并添加到列表**
      * **电子邮件服务：发送自动回复者电子邮件**
      * **电子邮件服务：从列表中取消订阅用户**
      * **编辑社区**
      * **编辑资源**
      * **编辑工作流控制的资源**
      * **邮件**
      * **已下订单详细信息**
      * **配置文件更新**
      * **重置密码**
      * **设置密码**
      * **存储内容**

        默认操作类型。

      * **存储上传的内容**
      * **提交订单**
      * **取消订阅者**
      * **更新订单**

   * **表单标识符**

     表单标识符唯一标识表单。 如果单个页面上有多个表单，请使用表单标识符；请确保它们具有不同的标识符。

   * **加载路径**

     用于将预定义值加载到表单字段中的节点属性的路径。

     一个可选字段，它指定存储库中节点的路径。 当此节点具有匹配字段名称的属性时，表单上的相应字段将预加载这些属性的值。 如果不存在匹配项，则字段包含默认值。

     使用&#x200B;**加载路径**，您可以预加载包含必填字段中的值的表单。 请参阅[预加载表单值](/help/sites-developing/developing-forms.md#preloading-form-values)。

   * **客户端验证**

     指示此表单是否需要客户端验证（服务器验证&#x200B;*始终*&#x200B;发生）。 可以使用&#x200B;**Forms Captcha**&#x200B;组件进行客户端验证。

   * **验证资源类型**

     如果要验证整个表单（而不是单个字段），请定义表单验证资源类型。 如果要验证完整的表单，还应包括以下内容之一：

      * 用于客户端验证的脚本：

        `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * 用于服务器端验证的脚本：

        `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`

   * **操作配置**

     **操作配置**&#x200B;中可用的选项取决于所选的&#x200B;**操作类型**：

      * **帐户请求**

         * **创建帐户页**

           创建帐户时使用的页面。

      * **创建内容**

         * 内容路径

           表单转储的任何内容的内容路径。 输入以斜杠`/`结尾的路径。 斜杠表示对于每个表单端口，将在给定位置创建一个新节点；例如：

           `/forms/feedback/`

         * **类型**

           选择所需的类型。

         * **表单**

           指定表单。

         * **渲染方式**

           从列表中选择所需的选项。

         * **资源类型**

           如果设置，它作为`sling:resourceType`添加到每个评论

         * **查看选择器**

      * **创建潜在客户**

         * **潜在客户已添加到此列表**

           指定所需的潜在客户列表。

      * **创建和更新帐户**

         * **初始组**

           要为其分配新用户的组。

         * **主页**

           成功登录后显示的页面。

         * **路径**

           创建和存储新帐户的路径（相对）。

         * **查看数据……**

           选择此按钮可在批量编辑器中访问有关表单结果的信息。 从此处，您可以将信息导出到`.tsv`（制表符分隔）文件（例如用于Excel电子表格中）。

      * **邮件**

         * **来自**

           输入电子邮件应来自的电子邮件地址。

         * **Mailto**

           输入表单发送到的一个或多个电子邮件地址。

         * **抄送**

           输入一个或多个抄送电子邮件地址。

         * **密件抄送**

           输入一个或多个密送电子邮件地址。

         * **主题**

           输入电子邮件的主题。

      * **重置密码**

         * **更改密码页**

           更改密码时使用的页面。

      * **存储内容**

         * **内容路径**

           表单转储的任何内容的内容路径。 输入以斜杠`/`结尾的路径。 斜杠表示对于每个表单端口，将在给定位置创建一个新节点；例如：
           `/forms/feedback/`

         * **查看数据……**

           单击此按钮可在批量编辑器中访问有关表单结果的信息。 从此处，您可以将信息导出到.tsv（制表符分隔）文件（例如，用于Excel电子表格）。

      * **存储上传的内容**

        具有与&#x200B;**存储内容**&#x200B;相同的选项。

      * **取消订阅者**

         * **潜在客户已从此列表中删除**

           指定所需的潜在客户列表。

#### 表单结尾 {#end-of-form}

标记表单的结尾。 您可以配置以下内容：

* **表单结束**

   * **显示提交按钮**

     指示是否应显示提交按钮。

   * **提交名称**

     标识符（如果您在表单中使用多个提交按钮）。

   * **提交标题**

     按钮上显示的名称，如“提交”或“发送”。

   * **显示重置按钮**

     选中该复选框可使“重置”按钮可见。

   * **重置标题**

     “重置”按钮上显示的名称。

   * **描述**

     按钮下方显示的信息。

### 帐户名称 {#account-name}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html?lang=zh-Hans)。

允许用户输入帐户名称：

![dc_form_accountname](assets/dc_form_accountname.png)

### 地址 {#address}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html?lang=zh-Hans)。

允许您添加具有以下格式的国际地址字段：

![dc_form_addressfield](assets/dc_form_addressfield.png)

该组件配置为立即使用，但您可以根据需要更改配置。 例如，可以为地址的单个元素添加约束。 将字段留空表示使用默认设置。

### 验证码 {#captcha}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

>[!CAUTION]
>
>如果没有广泛的项目级自定义，则预计此组件将不再能够开箱即用。

Captcha组件要求用户键入屏幕上显示的字母数字字符串。 字符串会随着每次刷新而更改。

![dc_form_captcha](assets/dc_form_captcha.png)

您可以为此组件配置各种参数，包括验证码字符串无效时要显示的消息。

### 复选框组 {#checkbox-group}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单选项核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html?lang=zh-Hans)。

通过复选框，您可以构建一个或多个复选框的列表，同时可以选择多个复选框。

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

您可以指定各种参数，包括标题、描述和元素名称。 使用+和 — 按钮，您可以添加或删除项目，然后使用向上箭头和向下箭头放置它们。

>[!NOTE]
>
>使用&#x200B;**项加载路径**，您可以使用值预加载复选框组列表。
>
>请参阅[预加载具有多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 信用卡详细信息 {#credit-card-details}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

允许您提供输入信用卡详细信息所需的字段。 您可以对其进行配置，以指定接受的卡类型以及所需的信息（例如安全代码）。

![chlimage_1-100](assets/chlimage_1-100.png)

### 下拉列表 {#dropdown-list}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单选项核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html?lang=zh-Hans)。

下拉列表可以配置为为您提供一系列值供您选择：

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

您可以指定要显示在列表中的标题和项目。 使用+和 — 按钮，您可以添加或删除列表项，然后使用“向上”和“向下”按钮放置它们。 您可以指定是否允许用户从列表中选择多个项目，以及用户首次打开列表时应自动选择的任何项目（初始值）。

>[!NOTE]
>
>使用&#x200B;**项加载路径**，您可以使用值预加载下拉列表。
>
>请参阅[预加载具有多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 文件上传 {#file-upload}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

文件上传组件为用户提供了一种选择和上传文件的机制。

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>您可以创建自定义上传组件以将文件上传到Sling Servlet。 有关信息，请参阅[将文件上传到Adobe Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-cloud-service-create-asset-servlet-for-uploading-small-files/td-p/404276)。

### 隐藏字段 {#hidden-field}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单隐藏核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-hidden.html?lang=zh-Hans)。

允许您创建隐藏字段。 这些隐藏字段可用于各种目的。 例如，在提交表单后必须执行操作，或者在后处理中需要隐藏数据时。

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>您还可以自定义表单，以根据表单中其他字段的值显示或隐藏特定表单组件。 仅在特定条件下需要表单字段时，更改该字段的可见性很有用。
>
>请参阅[显示和隐藏表单组件](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components)。

### 图像按钮 {#image-button}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单按钮核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html?lang=zh-Hans)。

图像按钮允许您创建具有自己的图像和文本的按钮：

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### 图像上传 {#image-upload}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

图像上传组件为用户提供了一种选择和上传图像文件的机制。

![dc_form_imageupload](assets/dc_form_imageupload.png)

### 链接字段 {#link-field}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

链接字段允许用户指定URL：

![dc_form_link](assets/dc_form_link.png)

最常用于日历事件表单，其中用于事件的URL/链接字段。

### 密码字段 {#password-field}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

允许用户输入密码：

![dc_form_password](assets/dc_form_password.png)

### 密码重置 {#password-reset}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

此组件为用户提供以下两个字段：

* 密码的输入
* 反复输入密码以检查输入是否正确。

在默认设置下，该组件显示如下：

![dc_password_reset](assets/dc_password_reset.png)

### 单选按钮组 {#radio-group}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单选项核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html?lang=zh-Hans)。

单选按钮组为您提供一个或多个单选复选框的列表，在任何特定时间只能选择其中一个复选框。

您可以指定元素名称以及标题和描述。 使用+和 — 按钮，您可以添加或删除项目，使用向上和向下箭头放置项目，并在必要时指定默认值：

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>使用&#x200B;**项加载路径**，您可以使用值预加载单选按钮组。
>
>请参阅[预加载具有多个值的表单字段](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values)。

### 提交按钮 {#submit-button}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单按钮核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html?lang=zh-Hans)。

利用此组件，可创建包含默认文本的提交按钮：

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

或者使用您自己的文本：

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### 标记字段 {#tags-field}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

此字段允许您选择标记：

![dc_form_tags_use](assets/dc_form_tags_use.png)

您可以使用专用选项卡指定各种参数，包括可以使用的命名空间：

* **标记字段**

   * **允许的命名空间**

      * **Geometrixx Outdoors**
      * **工作流**
      * **论坛**
      * **Stock摄影**
      * **Geometrixx Media**
      * **标准标记**
      * **营销**
      * **资源属性**
      * **宽度（以像素为单位）**
      * **弹出窗口大小**

### 文本字段 {#text-field}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单文本核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html?lang=zh-Hans)。

可以将标准文本字段配置为所需的大小，并在消息中拥有您自己的潜在客户：

![dc_form_text](assets/dc_form_text.png)

### 工作流提交按钮 {#workflow-submit-button-s}

>[!CAUTION]
>
>已弃用此基础组件。 Adobe建议改用[表单按钮核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html?lang=zh-Hans)。

允许您创建在工作流中使用的提交按钮。

![chlimage_1-101](assets/chlimage_1-101.png)
