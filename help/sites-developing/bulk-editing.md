---
title: 配置页面以批量编辑页面属性
description: 批量编辑页面属性允许您同时编辑多个页面的属性
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Developer
exl-id: 7ba0a378-0b52-40bd-8dab-32490594558e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 24%

---

# 配置页面以批量编辑页面属性 {#configuring-your-page-for-bulk-editing-of-page-properties}

[批量编辑页面属性](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages)功能让您一次编辑多个页面的属性。

由于可能存在不同的值，默认情况下不会启用页面属性以进行批量编辑。 必须明确允许（启用）。 在定义可用于批量编辑的页面属性时，您需要考虑某些事项，例如：

* 某些字段通常是唯一的；例如，页面标题。 确定在应用一个值时启用此类字段进行批量编辑是否有意义。
* 某些字段可能具有多个值 — 这在呈现时需要有意义的表示形式。

  例如，显示“准备发布”的复选框。 在批量编辑之前，这可能会有多个值（例如，就绪、正在审核、正在进行）。

>[!CAUTION]
>
>页面属性的批量编辑：
>
>* 在经典UI中不可用。
>* 不适用于 Live Copy 中的页面。
>* 仅适用于具有相同资源类型的页面。
>

>[!NOTE]
>
>批量编辑也可用于Assets。 其操作大体相同，只有少数几点差别。有关完整信息，请参阅[编辑多个Assets的属性](/help/assets/metadata.md)。 您可以使用[架构编辑器](/help/assets/metadata-schemas.md)自定义Assets的批量元数据编辑器中的字段。

## 启用字段 {#enabling-a-field}

>[!NOTE]
>
>某些字段可能具有多个值 — 这在呈现时需要有意义的表示形式。 因此，您应该只启用以下字段类型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

已在页面组件中启用字段（在模板中为&#x200B;*而非*）：

1. 使用CRXDE Lite（或等效方法）打开页面组件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此示例假设核心组件已安装在实例上，如果实例运行的是We.Retail示例内容，就是这种情况。 有关详细信息，请参阅[核心组件文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)。

1. 导航至`cq:dialog` 定义中的必填字段。
1. 在字段节点上定义以下属性：

   * **名称**：`allowBulkEdit`
   * **类型**：`Boolean`
   * **值**：`true`

   例如，对于标准页面[基础组件](/help/sites-authoring/default-components-foundation.md)：

   `/libs/foundation/components/page`

   将在以下日期定义属性：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您&#x200B;***必须***&#x200B;不更改`/libs`路径中的任何内容。
   >
   >这是因为下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
   >
   >建议用于配置和其他更改的方法是：
   >
   >    1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
   >    1. 在`/apps`中进行任何更改

1. 选择&#x200B;**保存全部**，以保留您的更新。
