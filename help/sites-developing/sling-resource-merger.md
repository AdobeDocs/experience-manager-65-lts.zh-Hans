---
title: 在AEM中使用Sling资源合并器
description: Sling资源合并器提供访问和合并资源的服务
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6fb6e522-fb81-4ba2-90b2-aad68f8bfa9e
source-git-commit: 9bc1cad84bb14b7513ede1fff2c1a37768dac442
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# 在AEM中使用Sling资源合并器{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling资源合并器提供访问和合并资源的服务。 它提供了以下两种情况的差异（差异）机制：

* 使用&#x200B;**[配置的搜索路径](/help/sites-developing/overlays.md)**&#x200B;进行的[资源叠加](/help/sites-developing/overlays.md#configuring-the-search-paths)。

* 使用资源类型层次结构（通过属性&#x200B;**）为启用了Touch的UI (**)覆盖`cq:dialog`组件对话框`sling:resourceSuperType`。

Sling资源合并器将叠加和覆盖资源（及其属性）与原始资源和属性相结合：

* 自定义定义的内容具有比原始定义更高的优先级。 即，它&#x200B;*覆盖*&#x200B;或&#x200B;*覆盖*。

* 根据需要，自定义项中定义的[属性](#properties)指示如何使用从原始内容合并的内容。

>[!CAUTION]
>
>Sling资源合并器和相关方法只能与[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html)一起使用。 此情况还意味着该覆盖仅适用于标准的触屏优化UI，尤其是以这种方式定义的覆盖仅适用于组件的触屏优化对话框。
>
>要叠加或覆盖其他区域（包括触控式组件或经典UI的其他部分），请从原始节点复制相应的节点和结构。 将副本放置在定义自定义的位置。

### AEM的目标 {#goals-for-aem}

在AEM中使用Sling资源合并器的目标如下：

* 确保未在`/libs`中进行自定义更改。
* 减少从`/libs`复制的结构。

  在使用Sling资源合并器时，不建议从`/libs`中复制整个结构。 原因是它会导致自定义项中包含过多信息（通常为`/apps`）。 在系统升级时，不必要地复制信息会增加出现问题的机会。

>[!NOTE]
>
>覆盖不依赖于搜索路径。 他们使用属性`sling:resourceSuperType`建立连接。
>
>但是，覆盖通常在`/apps`下定义，因为AEM中的最佳实践是在`/apps`下定义自定义项。 原因是您不能更改`/libs`下的任何内容。

>[!CAUTION]
>
>*不要*&#x200B;更改`/libs`路径中的任何内容。
>
>原因在于，下次升级实例时，`/libs`的内容会被覆盖。 并且，当您应用修补程序或功能包时，它可能会被覆盖。
>
>建议用于配置和其他更改的方法是：
>
>1. 在`/libs`下重新创建所需项（即`/apps`中存在的项）
>
>1. 在`/apps`中进行任何更改
>

### 属性 {#properties}

资源合并器提供以下属性：

* `sling:hideProperties` （`String`或`String[]`）

  指定要隐藏的属性或属性列表。

  通配符`*`会隐藏所有。

* `sling:hideResource` ( `Boolean`)

  它指示资源是否完全隐藏，包括其子级。

* `sling:hideChildren` （`String`或`String[]`）

  它包含要隐藏的子节点或子节点列表。 节点的属性将得到维护。

  通配符`*`会隐藏所有。

* `sling:orderBefore` ( `String`)

  它包含当前节点位于前面的同级节点的名称。

这些属性会影响叠加/覆盖（通常在`/libs`中）如何使用相应的/原始资源/属性（来自`/apps`）。

### 创建结构 {#creating-the-structure}

要创建覆盖或覆盖，您需要在目标（通常为`/apps`）下使用等效结构重新创建原始节点。 例如：

* 叠加

   * 站点控制台的导航条目（如边栏中所示）的定义定义定义位于：

     `/libs/cq/core/content/nav/sites/jcr:title`

   * 要叠加，请创建以下节点：

     `/apps/cq/core/content/nav/sites`

     然后根据需要更新属性`jcr:title`。

* 替代

   * 文本控制台的触屏启用对话框定义如下：

     `/libs/foundation/components/text/cq:dialog`

   * 要覆盖，请创建以下节点。 例如：

     `/apps/the-project/components/text/cq:dialog`

要创建任一结构，您只需重新创建骨架结构。 为了简化结构的重新创建，所有中间节点都可以是`nt:unstructured`类型（它们不必反映原始节点类型）。 例如，在`/libs`中。

因此，在上述覆盖示例中，需要以下节点：

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>在使用Sling资源合并器（即，处理标准的触屏UI时）时，不建议从`/libs`复制整个结构。 原因是这将导致过多信息保存在`/apps`中。 因此，它可能会导致系统升级时出现问题。

### 用例 {#use-cases}

通过标准功能，这些用例可让您执行以下操作：

* **添加属性**

  属性在`/libs`定义中不存在，但在`/apps`覆盖/覆盖中是必需的。

   1. 在`/apps`中创建对应的节点
   1. 在此节点上创建新属性»

* **重新定义属性（不是自动创建的属性）**

  属性在`/libs`中定义，但在`/apps`覆盖/覆盖中需要新值。

   1. 在`/apps`中创建对应的节点
   1. 在此节点上创建匹配属性（在`apps`下）

      * 该属性的优先级基于Sling资源解析程序配置。
      * 支持更改属性类型。

        如果您使用的属性类型与`/libs`中使用的属性类型不同，则会使用您定义的属性类型。

  >[!NOTE]
  >
  >支持更改属性类型。

* **重新定义自动创建的属性**

  默认情况下，自动创建的属性（如`jcr:primaryType`）不受覆盖/覆盖的约束，以确保当前位于`/libs`下的节点类型得到遵守。 要强制覆盖/覆盖，您必须在`/apps`中重新创建节点，明确隐藏属性并重新定义它：

   1. 在`/apps`下使用所需的`jcr:primaryType`创建对应的节点
   1. 在该节点上创建属性`sling:hideProperties`，其值设置为自动创建的属性的值；例如，`jcr:primaryType`

      此属性在`/apps`下定义，其优先级现在高于`/libs`下定义的属性

* **重新定义节点及其子节点**

  节点及其子节点在`/libs`中定义，但在`/apps`覆盖/覆盖中需要新配置。

   1. 合并以下各项的操作：

      1. 隐藏节点的子节点（保留节点的属性）
      1. 重新定义属性/属性

* **隐藏属性**

  属性在`/libs`中定义，但在`/apps`覆盖/覆盖中不是必需的。

   1. 在`/apps`中创建对应的节点
   1. 创建类型为`sling:hideProperties`或`String`的属性`String[]`。 用于指定要隐藏/忽略的属性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子节点**

  节点及其子节点在`/libs`中定义，但在`/apps`覆盖/覆盖中不是必需的。

   1. 在`/apps`下创建对应的节点
   1. 创建属性`sling:hideResource`

      * 类型： `Boolean`
      * 值： `true`

* **隐藏节点的子节点（同时保留节点的属性）**

  在`/libs`中定义了节点、其属性及其子节点。 `/apps`覆盖/覆盖中需要节点及其属性，但在`/apps`覆盖/覆盖中不需要部分或全部子节点。

   1. 在`/apps`下创建对应的节点
   1. 创建属性`sling:hideChildren`：

      * 类型： `String[]`
      * 值：要隐藏/忽略的子节点列表（如`/libs`中的定义）

      通配符&amp;amp；ast；可用于隐藏或忽略所有子节点。

* **重新排序节点**

  节点及其同级在`/libs`中定义。 要更改顺序，请在`/apps`覆盖或覆盖中重新创建节点。 通过引用`/libs`中的相应同级节点来定义其新位置。


   * 使用`sling:orderBefore`属性：

      1. 在`/apps`下创建对应的节点
      1. 创建属性`sling:orderBefore`：

         指定当前节点位于之前的节点（如`/libs`中所示）：

         * 类型： `String`
         * 值： `<before-SiblingName>`

### 从您的代码调用Sling资源合并器 {#invoking-the-sling-resource-merger-from-your-code}

Sling资源合并器包含两个自定义资源提供程序 — 一个用于叠加，另一个用于覆盖。 可以在代码中使用挂载点调用每个ID：

>[!NOTE]
>
>在访问资源时，建议使用适当的挂载点。
>
>此方法将调用Sling资源合并器并返回完全合并的资源。 它还减少了必须从`/libs`复制的结构数量。

* 叠加：

   * 用途：根据资源的搜索路径合并资源
   * 装入点： `/mnt/overlay`
   * 用法： `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆盖：

   * 用途：根据资源的超级类型合并资源
   * 装入点： `/mnt/overide`
   * 用法： `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用示例 {#example-of-usage}

下面介绍一些示例：

* 叠加：

   * [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆盖：

   * [配置页面属性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
