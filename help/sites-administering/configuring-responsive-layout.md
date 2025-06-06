---
title: 配置布局容器和布局模式
description: 了解如何配置布局容器和布局模式。
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 413f15c9-5b51-4d8d-8cf0-3e98608b9d9e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 4%

---

# 配置布局容器和布局模式{#configuring-layout-container-and-layout-mode}

了解如何配置布局容器和布局模式。

>[!TIP]
>
>本文档为站点管理员和开发人员提供了响应式设计概述，介绍了如何在AEM中实现功能。
>
>对于内容作者，内容页面的响应式布局文档[中提供了如何在内容页面上使用响应式设计功能的详细信息。](/help/sites-authoring/responsive-layout.md)

## 概述 {#overview}

[响应式布局](/help/sites-authoring/responsive-layout.md)是一种用于实现[响应式网页设计](https://en.wikipedia.org/wiki/Responsive_web_design)的机制。 这允许用户创建网页，这些网页的布局和尺寸取决于用户使用的设备。

AEM 使用一组机制为页面实现响应式布局：

* [**布局容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;组件

  此组件提供了一个网格段落系统，允许您在响应式网格中添加和放置组件。 它可以用作页面的默认Parsys，和/或在组件浏览器中提供给作者。

   * 默认&#x200B;**布局容器**&#x200B;组件定义于：

     /libs/wcm/foundation/components/responsivegrid

   * 您可以定义布局容器：

      * 作为用户可以添加到页面中的组件。
      * 作为页面的默认parsys。
      * 两者。

        您可以将布局容器作为页面的标准，同时允许用户在此中添加更多布局容器；例如，实现列控件。

* **[布局模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
将布局容器放置到页面上后，即可使用&#x200B;**布局**&#x200B;模式在响应式网格内放置内容。

* [**模拟器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
这让您创建和编辑响应式网站，通过以交互的方式调整组件大小，根据设备/窗口大小重新排列布局。然后，用户可以使用模拟器查看内容的呈现方式。

通过这些响应式网格机制，您可以：

* 使用断点（指示设备分组）根据设备布局定义不同的内容行为。
* 根据设备组隐藏组件（定义将隐藏组件的断点）。
* 使用水平对齐网格功能（将组件放入网格中，根据需要调整大小，定义它们何时应该折叠/重排成并排或上下对齐）。
* 实现列控件。

>[!TIP]
>
>Adobe提供了[GitHub文档](https://adobe-marketing-cloud.github.io/aem-responsivegrid/)的响应式布局，前端开发人员可以参考该文档，以便在AEM之外使用AEM网格，例如，在为将来的AEM站点创建静态HTML模型时。

>[!NOTE]
>
>在开箱即用的安装中，已为[We.Retail参考网站](/help/sites-developing/we-retail.md)配置了响应式布局。 [为其他页面激活布局容器组件](#enable-the-layout-container-component-for-page)。

>[!CAUTION]
>
>尽管&#x200B;**布局容器**&#x200B;组件在经典UI中可用，但其完整功能仅在触屏UI中可用。

## 激活网站的布局模式 {#activate-layout-mode-for-your-site}

这些过程用于在您的网站上启用&#x200B;**布局**&#x200B;模式。

### 配置断点 {#configure-the-breakpoints}

[断点](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)：

* 在响应式设计中使用。
* 可以定义：

   * 在页面模板上，设置会从中复制到使用该模板创建的任何页面。
   * 在页面节点上，任何子页面都会从中继承设置。

* 定义标题和宽度：

   * 标题描述了通用设备分组，并根据需要提供了方向；例如，手机、平板电脑、表格横向。
   * 宽度定义该通用设备分组的最大宽度（以像素为单位）。 例如，如果断点电话的宽度为768，则表示它是用于电话设备的最大布局宽度。

* 使用模拟器时，在页面编辑器顶部显示为标记。
* 继承自父节点层次结构，可以随意覆盖。
* 有一个默认（开箱即用）断点，它覆盖上一个&#x200B;*配置的*&#x200B;断点之上的所有内容。

它们可以使用CRXDE Lite或XML进行定义。

>[!NOTE]
>
>如果您正在设置新项目：
>
>* 向模板添加断点。
>
>如果要迁移现有项目（包含现有内容），您必须：
>
>* 向模板添加断点
>* 将相同的断点添加到现有页面
>
>  由于继承正在运行，您可以将其限制为内容的根页面。

#### 使用CRXDE Lite配置断点 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或等效功能），导航到：

   * 您的模板定义。
   * 页面的`jcr:content`节点。

1. 在`jcr:content`下创建节点：

   * 名称：`cq:responsive`
   * 类型：`nt:unstructured`

1. 在此下创建节点：

   * 名称：`breakpoints`
   * 类型：`nt:unstructured`

1. 在断点节点下，可以创建任意数量的断点。 每个定义都是一个具有以下属性的节点：

   * 名称：`<descriptive name>`
   * 类型：`nt:unstructured`
   * 标题： `String` * `<descriptive title seen in Emulator>`*
   * 宽度： `Decimal` * `<value of breakpoint>`*

#### 使用XML配置断点 {#configuring-breakpoints-using-xml}

断点位于`.context.html`的`<jcr:content>`部分中，位于相应的模板（或内容）文件夹下。

示例定义：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 添加响应信息提供程序 {#add-a-responsive-information-provider}

>[!NOTE]
>
>仅当页面组件不是基于基础页面组件时，才需要此操作。

将以下`cq:infoProviders`节点结构复制到父页面组件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 为页面启用组件调整大小 {#enable-component-resizing-for-the-page}

需要这些过程，以便您可以在&#x200B;**布局**&#x200B;模式下调整组件大小。

### 将布局容器设置为主Parsys {#set-layout-container-as-main-parsys}

要将页面的main parsys设置为布局容器，请将parsys定义为：

`wcm/foundation/components/responsivegrid`

在：

* 页面组件
* 页面模板（供将来使用）

以下两个示例说明了定义：

* **HTL：**

  ```html
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```html
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 包含响应式CSS {#include-the-responsive-css}

#### 使用LESS的断点的CSS {#css-for-breakpoints-using-less}

AEM使用LESS生成必要的CSS部分，这些项目需要包含在您的项目中。

您还必须创建一个[客户端库](https://experienceleague.adobe.com/docs/?lang=zh-Hans)以提供额外的配置和函数调用。 以下LESS提取是您必须添加到项目的最小值示例：

```css
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

可在以下位置找到基本网格定义：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 样式设置注意事项 {#styling-considerations}

保持在响应容器中的组件(连同它们各自的HTML DOM元素)根据响应栅格大小而调整大小。 因此，在这些情况下，建议避免（或更新）固定宽度（包含）DOM元素的定义。

例如：

* 之前：

   * `width=100px`

* 之后：

   * `max-width=100px`

#### 调整大小和自适应图像合规性 {#resizing-and-adaptive-image-compliance}

网格中组件的任何大小调整都将相应地触发以下监听器：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

要正确调整响应式网格中包含的自适应图像的大小并更新其内容，您需要将设置为`REFRESH_PAGE`的`afterEdit`侦听器添加到每个包含组件的`EditConfig`文件中。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

该自适应图像机制可通过控制为窗口的当前大小选择正确图像的脚本来提供。 它在DOM准备就绪或收到专用事件时激活。 当前必须刷新页面才能正确反映用户操作的结果。

>[!CAUTION]
>
>自定义样式表客户端库必须作为标头的一部分加载，它们才能在创作和发布中正常工作。

## 为页面启用布局容器组件 {#enable-the-layout-container-component-for-page}

这些任务允许作者将&#x200B;**布局容器**&#x200B;组件的实例拖动到页面上。

### 启用布局容器组件以进行页面编辑 {#enable-the-layout-container-component-for-page-editing}

要允许作者向内容页面添加更多响应式网格，您需要为页面启用布局容器组件。 您可以使用以下任一方式执行此操作：

* **创作环境**

  使用[设计模式](/help/sites-authoring/default-components-designmode.md)激活页面的&#x200B;**层容器**&#x200B;组件。

* **组件定义**

  定义组件时，请使用`allowedComponent`或静态包含。

### 配置布局容器的网格 {#configure-the-grid-of-the-layout-container}

您可以配置可用于布局容器每个特定实例的列数：

1. **创作环境**

   您可以配置可用于布局容器每个特定实例的列数。

   为此，请使用[设计模式](/help/sites-authoring/default-components-designmode.md)，然后打开所需容器的“设计”对话框。 您可以在此指定有多少列可用于定位和大小调整。 默认值为12。

1. **XML**

   响应式网格的定义指定于：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定义以下参数：

   * 可用列数：

      * `columns="{String}8"`

   * 可添加到当前组件的组件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

## 嵌套响应式网格 {#nested-responsive-grids}

在某些情况下，您可能会发现有必要嵌套响应式网格来支持项目的需求。 但是，请记住，Adobe推荐的最佳做法是保持结构尽可能平坦。

当您无法避免使用嵌套的响应式网格时，请确保：

* 所有容器（容器、选项卡、折叠等）都具有属性`layout = responsiveGrid`。
* 不要在容器层次结构中混合使用属性`layout = simple`。

这包括页面模板中的所有结构化容器。

内部容器的列号不得大于外部容器的列号。 下面的示例满足此条件。 对于默认（桌面）屏幕，外部容器的列号为8，而内部容器的列号为4。

>[!BEGINTABS]

>[!TAB 示例节点结构]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB 示例生成的HTML]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
