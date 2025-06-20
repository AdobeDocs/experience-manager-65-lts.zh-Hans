---
title: 自定义控制台
description: AEM提供了多种机制，让您能够自定义创作实例的控制台
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 2a94ea8d-2919-4f30-be31-ce559493805d
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 22%

---

# 自定义控制台 {#customizing-the-consoles}

>[!CAUTION]
>
>本文档介绍如何在启用触屏的现代UI中自定义控制台，并且不适用于经典UI。

AEM提供了各种机制，使您能够自定义创作实例的控制台（和[页面创作功能](/help/sites-developing/customizing-page-authoring-touch.md)）。

* Clientlibs
Clientlibs允许您扩展默认实施以实现新功能，同时重用标准函数、对象和方法。 自定义时，您可以在`/apps.`下创建自己的clientlib。例如，它可以保存自定义组件所需的代码。

* 叠加
叠加基于节点定义，允许您用自己的自定义功能（在`/apps`中）叠加标准功能（在`/libs`中）。 创建叠加时，不需要原始内容的1:1副本，因为sling资源合并器允许继承。

可以通过多种方式使用这些变量来扩展AEM控制台。 下面包含少量选件（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 正在使用和创建[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和创建[叠加图](/help/sites-developing/overlays.md)。
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html)
>


>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>建议用于配置和其他更改的方法是：
>
>1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
>
>1. 在`/apps`中进行任何更改
>

例如，可以覆盖`/libs`结构中的以下位置：

* 控制台（任何基于Granite UI页面的控制台）；例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>有关更多提示和工具，请参阅知识库文章[AEM TouchUI问题疑难解答](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-16935)。

## 自定义控制台的默认视图 {#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、信息卡、列表）：

1. 可通过从下覆盖所需条目来重新排序视图：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一个条目将是默认条目。

   可用的节点与可用的视图选项相关：

   * `column`
   * `card`
   * `list`

1. 例如，在列表的覆盖中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定义下列属性：

   * **名称**：`sling:orderBefore`
   * **类型**：`String`
   * **值**：`column`

### 将新操作添加到工具栏 {#add-new-action-to-the-toolbar}

1. 您可以构建自己的组件，并为自定义操作包含相应的客户端库。 例如，在以下位置执行&#x200B;**提升至Twitter**&#x200B;操作：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然后可以将其连接到控制台上的工具栏项：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在选择模式下：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 将工具栏操作限制为特定组 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自定义呈现条件来叠加标准操作，并施加在呈现它之前必须满足的特定条件。

   例如，创建一个组件以根据组控制渲染条件：

   `/apps/myapp/components/renderconditions/group`

1. 要将这些方法应用于站点控制台上的创建站点操作，请执行以下操作：

   `/libs/wcm/core/content/sites`

   创建叠加：

   `/apps/wcm/core/content/sites`

1. 然后，为操作添加rendercondition：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此节点上的属性，您可以定义`groups`允许执行特定操作；例如，`administrators`

### 在列表视图中自定义列 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已针对文本字段的列进行优化；对于其他数据类型，可以在`/apps`中叠加`cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

要自定义列表视图中的列：

1. 叠加可用列的列表。

   * 在节点上：

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * 添加新列 — 或删除现有列。

   有关详细信息，请参阅[使用叠加（和Sling资源合并器）](/help/sites-developing/overlays.md)。

1. 可选：

   * 如果要插入其他数据，您需要使用编写[PageInforProvider](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)

     `pageInfoProviderType`属性。

   例如，请参阅下面的附加类/捆绑包（来自GitHub）。

1. 现在，您可以在列表视图的列配置器中选择该列。

### 筛选资源 {#filtering-resources}

使用控制台时，常见的用例是用户必须从资源（例如，页面、组件、资源等）中进行选择的情况。 这可以采用列表形式，例如，作者必须从中选择一个项目。

为了使列表保持合理的大小并且与用例相关，可以通过自定义谓词的形式实施筛选条件。有关详细信息，请参阅[自定义页面创作 — 筛选资源](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)。
