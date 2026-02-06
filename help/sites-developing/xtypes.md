---
title: 使用xtype（经典UI）
description: 了解Adobe Experience Manager提供的所有xtype
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '3668'
ht-degree: 0%

---

# 使用xtype（经典UI）{#using-xtypes-classic-ui}

本页介绍Adobe Experience Manager (AEM)可用的所有xtype。

在ExtJS语言中，xtype是指定给类的符号名称。 您可以阅读ExtJS 2[概述中的“组件XTypes”段落，详细解释什么是xtype以及如何使用它。](https://docs.sencha.com/)

有关AEM中所有可用小组件的更多信息，请参阅[小组件API文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

要了解在AEM中使用了给定xtype的组件，您可以在CRXDE中使用以下`Xpath`查询。 只需将“checkbox”替换为您感兴趣的xtype：

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>本页介绍在经典UI中ExtJS xtype的使用。
>
>Adobe建议您使用基于[Coral UI](/help/sites-developing/touch-ui-concepts.md)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)的标准、新式、[触屏UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)。

## xtype {#xtypes}

以下列出了Adobe Experience Manager中可用的xtype：

* `annotation`

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Annotation`是一个特殊窗口。 它在主体中有一个表单，在页脚中有一个按钮组。 它通常用于编辑内容，但也只能显示信息。

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  以前称为`SimpleStore`。

  一个小型帮助程序类，用于更轻松地从Array数据创建[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 `ArrayStore`自动配置为[CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor`在DAM管理中使用。

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog`是一个对话框，在页面引用资产或标记时会弹出该对话框。

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig`提供了一个面板，用于查看Blueprint的活动副本和编辑此Blueprint属性（同步触发器和同步操作）。

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus提供了一个面板来查看和编辑Blueprint及其Live Copies关系。 通过[CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)版本完成浏览。

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  要使用宽度和高度调整为框大小的任何[组件](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基类。

  BoxComponent为调整大小和定位提供了自动的框模型调整，并在组件渲染模型中正常工作。

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BrowseDialog允许用户浏览存储库以选择路径。 它通常通过[BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)使用。

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已弃用：请改用[CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor`提供搜索引擎和网格以编辑搜索结果。

  `BulkEditor`必须插入到HTML表单中（导入功能所必需的）。 这完全适用于[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm提供了由HTML表单包围的[CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的独立版本。 “导入”按钮需要HTML表单。

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  简单按钮类

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一组按钮的容器。

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.chart包提供了使用基于Flash的图表将数据可视化的功能。 每个图表都直接绑定到CQ.Ext.data.Store，从而可自动更新图表。 若要更改图表的外观，请参阅[chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)配置选项。

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  单个复选框字段。 可用作传统复选框字段的直接替换。

* `checkboxgroup`

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)控件的分组容器。

* `clearcombo`

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ClearableComboBox是一个不可编辑的组合框，带有用于清除其值的触发器。

* `colorfield`

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorField允许用户直接或使用[CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)输入颜色十六进制值。

* `colorlist`

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorList允许用户从可编辑列表中选择颜色。

* `colormenu`

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含[CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)组件的菜单。

* `colorpalette`

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  用于选择颜色的简单调色板类。 面板可以呈现到任何容器中。

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  支持自动完成、远程加载、寻呼和许多其他功能的组合框控件。

  ComboBox的工作方式与传统HTML &lt;select>字段类似。 不同之处在于，要提交[valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，您必须指定[hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以创建隐藏的输入。

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  所有`Ext`组件的基类。 组件的所有子类都可以参与由`Ext`Container[类提供的创建、渲染和销毁的自动的](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)组件生命周期。 创建容器时，可以通过[项](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)配置选项将组件添加到容器中。

* `componentextractor`

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ComponentExtractor允许用户从网站/页面提取组件。

* `componentselector`

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可用组件的分组、有序选择。

* `componentstyles`

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `compositefield`

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基于面板的复杂表单字段的基类，包括一个表单字段或一组表单字段。

* `container`

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  任何可能包含其他组件的[CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基类。 容器处理包含项目的基本行为，即添加、插入和删除项目。

  最常用的Container类是[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder是一个特殊的双列[视区](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，它包含左侧的实际内容查找器和右侧的内容框架。

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab是一个专用面板，提供了在[CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的选项卡面板中使用的功能。 通常，它具有搜索表单（查询框）和用于显示搜索的数据视图。

* `cq.workflow.model.combo`

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelCombo是自定义的[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，它显示可用工作流模型的列表。

* `cq.workflow.model.selector`

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelSelector将WorkflowModelCombo与工作流的缩略图图像以及创建和编辑工作流模型的按钮组合在一起。

* `createsitewizard`

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateSiteWizard是创建(MSM)站点的分步向导。

* `createversiondialog`

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateVersionDialog是一个允许创建页面版本的对话框。

* `customcontentpanel`

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CustomContentPanel是用于[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的特殊面板：其内容是从对话框中其他字段以外的其他URL检索并提交的。

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  专用的SplitButton，它包含[CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)元素的菜单。 该按钮在每次单击时自动循环浏览每个菜单项，从而引发该按钮的[change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)事件(或调用该按钮的[changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)函数（如果提供）)。

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一种使用自定义布局模板和格式显示数据的机制。 DataView使用[CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)作为其内部模板机制，并绑定到[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以便在存储中的数据更改时，视图会自动更新以反映这些更改。

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供了一个包含[CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)下拉菜单和自动日期验证的日期输入字段。

* `datemenu`

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含[CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)组件的菜单。

* `datepicker`

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  弹出式日期选取器。 此类由[DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)类用于允许浏览和选择有效日期。

* `datetime`

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  日期时间允许用户通过组合[CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)来输入日期和时间。

* `dialog`

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  该对话框是一个特殊窗口。 它在主体中有一个表单，在页脚中有一个按钮组。 它通常用于编辑内容，但也只能显示信息。

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet是用于[对话框](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一个小型帮助程序类，用于创建配置了[CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以便更轻松地与[CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)服务器端[Provider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)交互。

* `displayfield`

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  未验证且未提交的仅用于显示的文本字段。

* `editbar`

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditBar允许用户使用栏上的按钮编辑内容。

  尽管此处未列出，但EditBar具有[CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的所有成员。

* `editor`

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一个基本编辑器字段，可根据需要处理显示/隐藏操作，并具有一些内置的大小和事件处理逻辑。

* `editorgrid`

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此类扩展[GridPanel类](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以在选定的[列](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)上提供单元格编辑。 可编辑列是通过在[列配置](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)中提供[编辑器](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)指定的。

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  编辑变换图像允许用户通过双击编辑内容，并通过上下文菜单提供更多的编辑操作。 当鼠标滑过内容时，可编辑区域以框架指示。

* `feedimporter`

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FeedImporter允许用户导入RSS或Atom信息源，并为每个信息源条目创建页面。

* `field`

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  表单字段的基类，提供默认事件处理、大小调整、值处理和其他功能。

* `fieldset`

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  用于分组[表单](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)中的项目的标准容器。

* `fileuploaddialogbutton`

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadDialogButton将创建一个按钮，该按钮将打开一个新的对话框，用于通过FileUploadField上载文件。 可以在编辑对话框内使用，上传必须在一个单独的表单中进行。

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField允许用户选择要上载的单个文件。

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialog是一个用于查找和替换页面及其子页面中的令牌的对话框。

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此类表示基于组件的网格控件的主界面，以表格形式的行和列表示数据。

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一种专门的存储实施，它提供按可用字段之一对记录进行分组。 与[CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)一起使用，以证明分组GridPanel的数据模型。

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialog是一个用于移动页面及其子页面的对话框，同时考虑重新激活之前激活的页面（“大幅”移动）。

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一个基本隐藏字段，用于存储必须在表单提交中传递的表单中的隐藏值。

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButton是一个小型帮助程序类，可轻松提供后退和前进按钮。 通常需要两个相关的实例：前进按钮实例是一个链接到后退按钮实例的简单按钮，用于处理历史记录。

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供了一个轻量级的HTML编辑器组件。 Safari不支持某些工具栏功能，因此系统在需要时会自动隐藏这些功能。 在相应的配置选项中注明。

  编辑器的工具栏按钮在[buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)属性中定义了工具提示。

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  显示iframe内容并允许iframe中表单的纯对话框。

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含iframe的面板。 它可让您轻松创建iframe、iframe加载事件和访问iframe的内容。

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField是一个文本字段，当焦点不在时显示为标签。

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一个小型帮助程序类，用于更轻松地从JSON数据创建[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 JsonStore自动配置了[CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本标签字段。

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialog是用于复制语言树的对话框。

* `linkchecker`

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LinkChecker是一种检查站点中外部链接的工具。

* `listview`

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.list.ListView是类似[网格的](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)视图的快速轻量实现。

* `livecopyproperties`

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LiveCopyProperties提供了一个用于查看和编辑Live Copy属性（关系继承、同步触发器和同步操作）的面板。

* `lvbooleancolumn`

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  呈现布尔数据字段的列定义类。 有关详细信息，请参阅[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)配置选项。

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此类封装要在[ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的初始化中使用的列配置数据。

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  根据默认区域设置或配置的[格式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)呈现传递日期的Column定义类。 有关详细信息，请参阅[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)配置选项。

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  根据[格式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)字符串呈现数值数据字段的列定义类。 有关详细信息，请参阅[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)配置选项。

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已弃用：请改用[内容查找器](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)来浏览媒体。**

  MediaBrowseDialog是用于浏览媒体库的对话框。

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  菜单对象。 可在其中添加菜单项的容器。 当您希望基于其他组件（例如[CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）的专用菜单时，菜单还可以用作基类。

  菜单可以包含[菜单项](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)或常规[组件](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  呈现到菜单中的所有项目的基类。 BaseItem提供默认渲染、激活状态管理和所有菜单组件共享的基本配置选项。

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它添加了一个菜单项，默认情况下该菜单项包含复选框，但也可以是单选按钮组的一部分。

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  所有需要菜单相关功能（如子菜单）且不是静态显示项目的菜单项的基类。 项通过添加特定于菜单的激活和点击处理，扩展了[CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基本功能。

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它向菜单添加一个分隔条，用于划分菜单项的逻辑组。 通常，在对add()的调用或项目配置中使用“ — ”添加它，而不是直接创建它。

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它向菜单添加一个静态文本字符串，用作标题或组分隔符。

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata`提供了一组字段来确定元数据字段所需的信息，例如在资产编辑器页面上。

  其中提供了以下字段：

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `MultiField`是用于编辑多值属性的表单字段的可编辑列表。

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Multivariate Testing组件可用于定义和编辑显示为交替横幅的一组图像。 按横幅收集点进率统计数据。

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox`允许用户订阅WCM操作和管理通知。

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  提供自动击键过滤和数字验证的数字文本字段。

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter`是一种用于导入Microsoft® Word文档并将其转换为AEM页面的工具。 此功能允许使用文字处理器离线编辑内容。

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw`可以包含自定义HTML代码（直接输入或从URL检索）。

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  随着记录数的增加，浏览器渲染这些记录所需的时间也会增加。 分页用于减少与客户端交换的数据量。

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `panel`是一个容器，具有特定的功能和结构组件，使其成为面向应用程序的用户界面的完美构建基块。

  基于继承的面板来自[CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  段落引用字段允许您浏览页面并选择其中一个段落。 它由触发器字段和关联的段落浏览对话框组成。

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password`类似于[CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，但其值保持私有，允许用户输入敏感数据。

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已弃用：请改用[CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField`是为路径完成路径设计的输入字段，以及用于打开[CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以浏览服务器存储库的按钮。 它还可以浏览页面段落以生成高级链接。

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可更新的进度条组件。 进度条支持两种不同的模式：手动和自动。

  在手动模式下，您负责显示、更新（通过[updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）并根据需要从您自己的代码中清除进度条。 此方法最适合您想要显示进度的情况。

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一种专用网格实现，旨在模拟开发IDE中通常看到的传统属性网格。 网格中的每一行都表示某个对象的属性，该数据在[CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s中存储为一组名称/值对。

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid`是用于显示和编辑对象属性的通用网格。

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip` — 可在标记中指定并由全局[CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)实例自动管理的工具提示的专用工具提示类。 有关其他用法的详细信息和示例，请参阅快速提示类标头。

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  单个`radio`字段。 与复选框相同，但为便于自动设置输入类型而提供。 当组中的每个单选按钮使用相同的名称时，浏览器会自动对单选按钮进行分组。


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)控件的分组容器。

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog`是一个用于在页面上显示引用的对话框。

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog`是一个用于还原树早期版本的对话框。

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialog是一个用于恢复页面的先前版本的对话框。

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText`提供了一个表单字段，用于编辑样式化文本信息（富文本）。

  `RichText`组件当前提供以下功能：

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RolloutPlan提供了一个用于监视页面转出进度的对话框。 [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)启动RolloutPlan。

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard`提供了一个用于转出页面的向导。 RolloutWizard启动[CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField`提供了一个搜索字段，该字段在可用于搜索存储库的下拉列表中提供结果。

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Selection`允许用户从多个选项中进行选择。 这些选项可以是配置的一部分，也可以从JSON响应加载。 所选内容可以呈现为下拉列表(select)或组合框(select plus free text entry)。

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick`是一个浮动辅助函数，可为用户提供用于编辑页面的常用工具。

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin`是一个提供WCM管理功能的控制台。

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter`允许用户导入完整的网站和创建初始项目。

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField`允许用户输入宽度和高度（例如，对于图像）。

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  支持垂直或水平方向、键盘调整、可配置的对齐、轴单击和动画的滑块。 它可以作为项目添加到任何容器中。 例如，用法： ...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  通过幻灯片放映组件，可以定义和编辑一组图像和图像标题。 用户可以观看幻灯片集。

  幻灯片放映组件基于[CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)组件。

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile是一种智能文件上载程序。

  如果安装了Flash插件（版本>= 9），则使用SWFupload库执行上载，这为处理上载提供了一种方便的方法。

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage是一种智能图像上传程序。 它提供用于处理上传图像的工具，例如，定义图像映射的工具和图像裁剪器。

  该组件设计为在单独的对话框选项卡中使用。

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  用于在布局中提供较大的空间。

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner`是数字、日期或时间值的触发器字段。 通过使用提供的上下触发器、滚轮或按键，可以增加和减小该值。

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `splitbutton`提供了一个内置下拉箭头，该箭头可以独立于按钮的默认点击事件单独触发事件。 通常，它用于显示一个下拉菜单，为主按钮操作提供其他选项，但任何自定义处理程序都可以提供`arrowclick`实现。

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static`可用于显示任意文本或HTML。

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics`将页面展示显示为图表。 利用小组件，可选择应显示统计数据的时间段。

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Store`类封装了[记录](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)对象的客户端缓存，这些对象为[GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)或[DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)等组件提供输入数据。

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField`根据用户的输入为其提供建议。

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher`为控制台中的标题栏提供了一个按钮组，以便在Web站点、数字Assets、工具、工作流和安全性之间切换。

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已弃用：请改用[CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TableEdit2`提供了用于创建表的构件。

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本选项卡容器。 TabPanels的使用方式与标准[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的使用方式完全一样，可用于布局目的，但对于包含子组件([`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html))也有特殊支持。

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

  是用于输入标记的表单构件。 它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  多行文本字段。 可用作传统`textarea`字段的直接替代项，另外还增加了对自动调整大小的支持。

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton`提供具有[CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)功能的文本链接。

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本文本字段。 可用作传统文本输入的直接替换，或用作更复杂的输入控件（如[CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）的基类。

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供了一个带有时间下拉菜单的时间输入字段，并自动进行时间验证。 用法示例： ...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype提示：这是[CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基类，它提供了所有基于提示的类所需的基本布局和定位。 此类可直接用于简单的静态定位刀尖。

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它向菜单添加一个分隔条，用于划分菜单项的逻辑组。 分隔符还可以带有标题。

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本`Toolbar`类。 尽管工具栏的[`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)为[`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，但工具栏元素（工具栏容器的子项）实际上可以是任何类型的组件。 工具栏元素可以通过其构造函数显式创建。

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  标准`tooltip`实现，用于在将鼠标悬停在目标元素上时提供其他信息。 @xtype工具提示。

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype`treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel`提供树状结构数据的树状结构UI表示形式。

  添加到[的](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)TreeNode`TreePanel`可以包含应用程序在其[属性](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)属性中使用的元数据。

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它为`TextFields`提供了一个方便的包装器，添加了可单击的触发器按钮（默认情况下看起来像组合框）。 触发器没有默认操作，因此您必须通过覆盖[onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)来分配一个函数以实施触发器点击处理程序。 您可以直接创建`TriggerField`，因为它将像组合框一样呈现。

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `UploadDialog`允许用户将文件上传到存储库创建新的UploadDialog。

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  工具栏项，以显示当前用户名并允许用户操作，如编辑用户属性和模拟。

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  表示可查看的应用程序区域（浏览器视区）的专用容器。

  `Viewport`将自身呈现到文档正文中，并自动调整自身大小以适合浏览器视区的大小并管理窗口大小调整。 只能创建一个视区。

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  专门用作应用程序窗口的面板。 Windows已浮动，[可调整大小](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，默认情况下为[可拖动](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 Windows可以[最大化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以填充视区，还原到其以前的大小，并且可以是[最小化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)天。

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  一个小型帮助程序类，用于更轻松地从XML数据创建[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 `XmlStore`自动配置有[CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

  `cqinclude` — 包含来自存储库中不同路径的小组件定义的伪xtype。 它最常用于页面对话框。 此xtype没有实际的JavaScript构件类。 `CQ.Util`类通过使用`formatData()`函数来处理它。
