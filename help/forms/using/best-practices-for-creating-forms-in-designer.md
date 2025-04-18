---
title: 在Forms Designer中创建表单的最佳实践
description: 了解在Forms Designer中创建表单的最佳辅助功能实践
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0f9d0b66-d6e4-475a-8727-c1de1a1e1bb0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '11687'
ht-degree: 0%

---

# 在Forms Designer中创建表单的最佳实践

LiveCycle Designer使您能够构建丰富的表单内容并符合Section 508准则。 本指南包含创建无障碍表单的最佳实践的概述，以及使用LiveCycle Designer实施这些最佳实践的指南。 其中涵盖了以下最佳实践：

1. [保持表单简单且易于使用](#keep-simple)
1. [配置表单属性以生成辅助功能信息](#configure-form-properties)
1. [选择正确的控件](#choose-right-controls)
1. [为图像提供等效文本](#provide-text-equivalents)
1. [为表单控件提供适当的标签](#provide-proper-labels)
1. [确保阅读和制表符顺序正确](#ensure-reading-tab-order)
1. [确保表单控件可使用键盘](#ensure-keyboard-accessible)
1. [负责任地使用颜色](#use-color-responsibly)
1. [为表提供标题单元格](#provide-heading-cells)
1. [提供可导航的窗体结构](#provide-navigable-form)
1. [避免中断脚本](#avoid-disruptive-scripting)
1. [确保所有音频和视频内容都可访问](#ensure-audio-video-accessible)
1. [识别自然语言和语言的任何更改](#identify-natural-language)

## 保持表单简单且易于使用 {#keep-simple}

如果表单不易于使用，则无法访问表单。 您应该尝试设计简单实用的表单。 控件和字段的简单布局以及清晰、有意义的字幕和工具提示将使表单更易于所有用户使用。
设计整齐合理、指令清晰简单的表格将有助于所有用户尽可能轻松地填写表格。 导航功能（如选项卡顺序和键盘快捷键）应支持表单上对象的逻辑顺序。

### 避免移动、闪烁或闪烁内容

某些患有光敏性癫痫的人可能会因为运动频率大于2赫兹（1赫兹，等于每秒1赫兹）且小于55赫兹（每秒55赫兹）而引发癫痫发作。

低于2Hz的运动被认为足够慢，对患有光敏性癫痫的人来说是安全的。 高于55 Hz的频率被认为是无法感知的。

当在Web内容中使用任何移动时，开发人员应该了解这些参数。

其他用户可能有认知障碍，当表单中存在动画或闪烁的内容时，这些障碍会让用户难以集中注意力。

通常，应尽量避免在交互式表单中使用脚本插入的光学效果，如闪烁文本或动画。 这种影响降低了某些用户表单的可用性。

相关检查点
* 第508款§11934.21

   * (h)当显示动画时，信息应可按用户的选择以至少一个非动画演示模式显示。
   * (k)软件不得使用闪光或闪烁的文本、对象或闪光或闪烁频率大于2 Hz且小于55 Hz的其他元素。
* 第508款§11934.22
   * (j)页的设计应避免屏幕在大于2 Hz且小于55 Hz的频率下闪烁。
* WCAG 1.0
   * 7.1在用户代理允许用户控制闪烁之前，请避免导致屏幕闪烁。 (P1)
   * 7.2在用户代理允许用户控制闪烁之前，避免导致内容闪烁（即，定期更改演示方式，如打开和关闭）(P2)。
   * 7.3在用户代理允许用户冻结移动内容之前，请避免在页面中移动。
   * 14.1使用适用于站点内容的最清晰、最简单的语言。
* WCAG 2.0
   * 2.2.2暂停、停止、隐藏：对于移动、闪烁、滚动或自动更新的信息，以下全部为真：（A级）
   * 2.3.1闪光三次或低于阈值：网页不包含在任何一秒时段内闪光三次以上的任何内容，或者闪光低于常规闪光和红色闪光阈值。 （A级）
   * 2.3.2闪烁3次：网页不包含在任何一秒内闪烁3次以上的任何内容。 （AAA级）


## 配置表单属性以生成辅助功能信息 {#configure-form-properties}

要访问表单，辅助技术必须使其为[可感知](https://www.w3.org/TR/WCAG20/#perceivable)。 例如，大多数屏幕阅读器不会考虑表单的可视布局，而是考虑底层结构。

要使用LiveCycle Designer实施此基础结构，您必须创建包含辅助功能信息（有时也称为标记）的PDF表单，以便屏幕阅读器或其他辅助技术可以读取表单的文本和组件。 在包含辅助功能信息的表单中，每个元素都包含有关其自身结构的信息，以及有关其与其他元素之间的关系或依赖其他元素的信息。 只有在包含辅助功能信息的PDF文件中，屏幕阅读器才能准确地识别和描述文档内容。

要创建辅助功能表单，您必须配置表单属性，以便在将表单设计另存为PDF文件时，让LiveCycle Designer生成辅助功能信息：
1. 选择“文件”>“表单属性”。
1. 单击保存选项选项卡，在PDF区域中，确保选中为Acrobat生成辅助功能信息（标记） 。
1. 单击“确定”。

在LiveCycle Designer中，默认情况下会选中此选项。

>[!NOTE]
> 这些选项仅在将表单设计另存为PDF文件时适用。 它们不适用于使用LiveCycle Forms创建的PDF文件，这些文件的配置选项与LiveCycle Designer中的此选项无关。

**相关检查点**

* 第508款§1194.21
   * (d)辅助技术应提供有关用户界面元素的充分信息，包括元素的身份、操作和状态。 当图像表示项目群元素时，由图像传递的信息还必须以文本形式提供。
   * (l)使用电子表单时，该表单应让使用辅助技术的人员能够访问填写和提交表单所需的信息、字段要素和功能，包括所有指示和提示。
* 第508款§1194.22
   * (n)电子表格设计成在线填写时，表格应允许使用辅助技术的人获得填写和提交表格所需的信息、栏位要素和功能，包括所有指示和提示。


## 选择正确的控件 {#choose-right-controls}

设计表单时，请使用LiveCycle Designer对象库中可用的选项卡中的开发对象。 通过选择“窗口”>“对象库”或按Shift+F12可显示此面板（请参见图1）。

![对象库面板](/help/forms/using/assets/image-1.png)

图1： **对象库面板**

如果您使用其他对象，则辅助技术可能会忽略这些对象。 仅使用标准对象可省去为您自己创建的对象定义辅助功能属性的额外工作。 如果您创建并使用自己的自定义对象，请务必使用“辅助功能”调色板来设置辅助功能属性，例如“角色”、“工具提示”、“屏幕Reader优先级”和“自定义屏幕Reader文本”。 要显示“辅助功能”调色板，请选择“窗口”>“辅助功能”。

**相关检查点**
* 第508款§1194.21
   * (c)应提供当前焦点的明确定义的屏幕指示，该指示随着输入焦点的变化在交互式界面元素之间移动。 焦点应以编程方式公开，以便辅助型技术可以跟踪焦点并关注更改。
   * (d)辅助技术应提供有关用户界面元素的充分信息，包括元素的身份、操作和状态。 当图像表示项目群元素时，由图像传递的信息还必须以文本形式提供。
   * (l)使用电子表单时，该表单应让使用辅助技术的人员能够访问填写和提交表单所需的信息、字段要素和功能，包括所有指示和提示。
* 第508款§1194.22
   * (n)电子表格设计成在线填写时，表格应允许使用辅助技术的人获得填写和提交表格所需的信息、栏位要素和功能，包括所有指示和提示。

* WCAG 2.0
   * 3.2.4一致的标识：一组网页内具有相同功能的组件均采用一致的方式进行标识。 （AA级）。
   * 4.1.2名称、角色、值：对于所有用户界面组件（包括但不限于：表单元素、链接和脚本生成的组件），其名称和角色可以通过编程方式确定；可由用户设置的状态、属性和值可以通过编程方式设置；而且用户代理（包括辅助技术）可以收到这些项目的更改通知。 （A级）


## 为图像提供等效文本 {#provide-text-equivalents}

图像有助于提高某些类型的残障用户的理解。 但是，对于屏幕阅读器用户，如果您不提供替换文本，则图像将降低表单的可访问性。

如果选择使用图像，请为所有图像和图像字段对象提供文本描述。 确保文本描述了表单上的对象及其用途。 定义替换文本时，屏幕阅读器会在遇到图像时阅读此替换文本。 因此，包含信息的图像必须始终指定替换文本。

您可以使用辅助功能面板中的工具提示或自定义屏幕Reader文本属性，或通过文本字段、标题和对象名称提供文本描述，如在“绑定”选项卡的“名称”选项中所指定。 例如，图2显示了包含文本“获取Adobe Reader”的图像示例。 由于屏幕阅读器无法读取属于图像的文本，因此您应该在此对象的辅助功能面板的自定义屏幕Reader文本字段中包含替换文本。 在大多数情况下，替换文本应与图像中可见的文本相同（见图2）。

![使用辅助功能调色板指定图像的替换文本](/help/forms/using/assets/image-2.png)

图2： **使用辅助功能调色板指定图像的替换文本**

指定替换文本时，请考虑以下事项：
* 如果图像对象或扫描的图像包含表单的重要信息，请在“辅助功能”调色板中为图像创建描述对象及其用途的文本。 例如，公司徽标的文本可能包含“公司徽标”一词和公司名称。
* 如果图像对象包含语义颜色信息，则也请在描述中包含。 例如，对绿灯的描述可以是“传输成功”，对红灯的描述可以是“传输失败”。
* 如果使用复杂图形（如条形图），则以辅助功能的替代版本（如表格或更长的文本说明）提供信息。
* 请勿为仅用于修饰的静态图像创建文本描述。
* 请勿将扫描的数据用作背景信息。 当设计者扫描打印表单并使用Adobe LiveCycle Designer向表单添加新字段时，可能会发生这种情况。 屏幕阅读器无法检测到处于此状态的扫描数据。

当您在表单中包含纯粹的装饰性图形内容时，您想要确保屏幕阅读器不会朗读图像的存在。 对于大多数屏幕阅读器，可以通过在辅助功能面板中将“屏幕Reader文本”属性设置为“无”来实现此目的。 如果不这样做，某些屏幕阅读器可能会宣布图形的存在，而不指示图形代表的内容。 对于动态图像（如图像字段对象），请确保在更改图像时正确更新替换文本。 请勿为仅用于修饰的图像字段对象创建文本描述。 您可以使用FormCalc脚本语言动态地将文本描述分配给图像字段对象。 FormCalc是Adobe LiveCycle Designer的标准脚本语言。 例如，考虑一个表单，该表单在运行时数据的imagetext节点中具有名为ImageField1的图像字段和关联的文本。 您可以使用脚本在适当的事件（如`form:ready`）中传递此文本，如下所示：

`ImageField1.assist.toolTip = $record.imagetext.value`

相关检查点
* 第508款§1194.22
   * (a)应为每个非文本元素提供等效文本（例如，通过&quot;alt&quot;、&quot;longdesc&quot;或在元素内容中）。
* WCAG 1.0
   * 1.1为每个非文本元素提供等效文本（例如，通过“alt”、“longdesc”或在元素内容中）。 这包括：图像、文本的图形表示（包括符号）、图像映射区域、动画（例如动画GIF）、小程序和程序化对象、ASCII艺术、框架、脚本、用作列表项目符号的图像、分隔符、图形按钮、声音（无论是否经过用户交互播放）、独立音频文件、视频的音频轨道和视频(P1)。
* WCAG 2.0
   * 1.1.1非文本内容：呈现给用户的所有非文本内容都具有相同用途的替换文本，以下所列情况除外。 （A级）


## 为表单控件提供适当的标签{#provide-proper-labels}

表单控件的标签或标题标识了表单控件应表示的含义。 例如，文本“名字”会告诉用户必须在文本字段中输入其名字。 要使屏幕阅读器能够访问，标签必须以编程方式与表单控件关联，或者必须使用辅助功能面板为表单控件配置其他辅助功能信息；仅将文本对象放在控件旁边是不够的。 对于视力不佳或视力不佳的用户，标签必须正确放置到控件旁边。 这两种技术将在以下部分中讨论。

### 使用辅助功能调色板指定辅助功能标签文本

屏幕阅读器用户感知的标签不一定与可视字幕相同。 在某些情况下，您可能希望更详细地了解控件的用途。
对于表单中的每个字段对象，“辅助功能”调色板（见图3）可用于指定屏幕阅读器将朗读的内容以标识特定表单字段。

要使用“辅助功能”调色板，请执行以下步骤：

1. 选择“窗口”>“辅助功能”或按Shift+F6可显示“辅助功能”调色板。
1. 选择表单中的对象。 面板将显示对象的辅助功能属性。

![辅助功能调色板](/help/forms/using/assets/image-3.png)

图3： **辅助功能调色板**

将表单另存为PDF时，LiveCycle Designer会按顺序搜索表单中的“自定义文本”、“工具提示”、“标题”和“名称”属性，以查找屏幕阅读器要阅读的文本。 可以使用辅助功能面板中的“屏幕Reader优先顺序”选项覆盖此默认顺序：

1. 选择窗体设计上的对象。
1. 单击“辅助功能”调色板。
1. 选择除“无”之外的任何“屏幕Reader优先级”选项。

以下选项可供选择：

* **自定义文本**，您在辅助功能面板的自定义屏幕Reader文本字段中设置该文本。 此选项允许您指定您希望辅助技术（如屏幕阅读器）使用的任何文本。 大多数情况下，最好使用“题注”设置 — 只有在无法使用“题注”或“工具提示”时，才应考虑创建自定义屏幕Reader文本。
* **工具提示**，您在辅助功能面板的“工具提示”字段中设置。 对于大多数对象，当用户将指针悬停在对象上时，会在运行时显示工具提示。 仅当屏幕阅读器正在使用时，才会为某些只读对象（例如纸表单的条形码对象）显示工具提示。
* **Caption**，这将导致LiveCycle Designer将表单字段的关联（可视）标签用作屏幕阅读器文本。
* **名称**，您在“绑定”选项卡的“名称”字段中设置。 请注意，此名称不能包含任何空格。
* **无**，这将导致对象没有名称。 绝不建议对表单控件执行此操作。

使用辅助功能面板为表单控件设置标签时，请考虑以下事项：

* 如果您的表单控件的标题正确描述了控件，则屏幕阅读器可以访问该控件。 在这种情况下，请将“辅助功能”面板中的“自定义文本”和“工具提示”字段都留空，或者将“屏幕Reader优先顺序”更改为“标题”。
* 定位屏幕阅读器时，没有必要为同一表单控件指定不同的文本描述，因为只使用其中一个：屏幕Reader优先级顺序中的第一个非空字段。 例如，没有理由为屏幕阅读器同时指定自定义文本和工具提示文本。
* 默认情况下，如果在“工具提示”框或“自定义屏幕Reader”文本框中未指定任何内容，屏幕阅读器会读取描述。
* 请勿使用“辅助功能”调色板为任何不可见的字段或区域创建描述。
* 如果必须使用工具提示或自定义屏幕Reader文本选项创建描述，请始终包含表单上可见的描述，除非可见的描述没有意义，例如描述本身被缩写时。 这有助于屏幕阅读器用户就UI元素与其他用户进行有效通信。 如果同一UI元素的标题文本与工具提示或自定义屏幕Reader文本不同，则这些不同的用户组很难识别该元素。
* 对于表格单元格中的复选框和下拉列表控件，屏幕阅读器将朗读您为对象指定的任何标题、工具提示或自定义屏幕阅读器文本。 如果要在置于表中时将这些对象的替换文本使用列标题，则不要提供标题、工具提示或自定义屏幕阅读器文本。
* 如果控件需要其他说明，请确保这些说明也包含在替换文本中。 包含足够的口语信息以便用户了解需要输入的内容以及如何正确填写字段，但不要让用户过多的看到冗余信息。
* 请勿提供描述如何操作控件的不必要信息 — 让用户的辅助技术为用户处理此信息。 用户可以配置详细程度以适合其舒适度。

图4显示了一个文本字段的示例，该字段带有视觉标题，对于某些屏幕阅读器用户可能不清楚。 在此示例中，自定义屏幕Reader文本设置为“页数”，并且屏幕Reader优先顺序设置为自定义文本。 因此，屏幕阅读器将不会使用实际（可视的）描述文本（“页面数”）。 或者，也可以指定“刀尖”。

![当可见标签不充分时指定自定义屏幕Reader文本](/help/forms/using/assets/image-4.png)

图4：当可见标签不充分时，**指定自定义屏幕Reader文本**

### 标签单选按钮

当视力障碍用户进入单选按钮时，屏幕阅读器需要阅读以下两点：
* 单选按钮组用途的指示
* 每个单选按钮都有意义的标签
使用按钮标题使单选按钮可访问：
   1. 在层次结构面板中，选择排除组。
   1. 单击辅助功能调色板，然后在自定义屏幕Reader文本框中，键入要为组读取的文本。 例如，对于指示各种信用卡付款选项的排除组，请键入Select a method of payment。
   1. 如果每个单选按钮的字幕都提供了屏幕阅读器朗读时有意义的文本，则在“对象”面板中，选择“绑定”选项卡，然后取消选择“指定项目值”。

  若要使单选按钮可使用指定的项目值访问，请执行以下操作：
   1. 在层次结构面板中，选择排除组。
   1. 单击辅助功能调色板，然后在自定义屏幕Reader文本框中，键入要为组读取的文本。 例如，对于指示各种信用卡付款选项的排除组，请键入Select a method of payment。
   1. 在层次面板中，选择组中的第一个单选按钮。
   1. 在“对象”面板中，单击“字段”选项卡。 在“项目”区域中，双击该项目并为选定的单选按钮键入有意义的值。 例如，对于一组付款方法中的第一个按钮，您可以键入Cash。
   1. 对排除组中的每个单选按钮重复步骤3和4。

### 为自定义控件设置标签

强烈建议使用标准组件而不是自定义组件，因为它们将在默认情况下为辅助型技术提供正确的提示和信息。 但是，如果使用自定义控件，请考虑以下事项：
* 宣布复选框和单选按钮的状态。
* 在列表框和下拉列表中，宣布在列表中选定的默认项目。 确保用户知道使用向上箭头和向下箭头键在列表项中移动。 请注意，按Tab键或Enter或Return键将选择列表中的项目。 使用脚本，您可以设置对象的Change事件以宣布从列表中选择了哪个项目。
* 向用户宣布执行某项功能所需的任何特殊击键，例如，按空格键选择按钮或按向下箭头键从列表框中选择项目。

### 正确定位控件的标题

字幕的位置很重要，因为用户希望字幕位于控件旁边。 对于屏幕放大用户来说，这甚至更重要，因为如果距离太远，他们可能无法同时查看控件和题注。

创建对象时，LiveCycle Designer会自动按照对象类型指定放置标题。 例如，单选按钮的标题位于右侧。 此默认放置始终是辅助字幕的最佳位置。 如果必须更改题注文本的位置，请使用以下步骤：
1. 通过将焦点移动到对象来选择对象。
1. 在“布局”面板中，从面板底部的“题注”部分的“位置”选项中选择对象题注的位置。

图5中的示例显示了一个文本框，其上方有一个标题。 “布局”面板中的“位置”设置为“顶部”。 题注的默认位置位于文本框的左侧。

![使用布局调色板更改字幕位置](/help/forms/using/assets/image-5.png)

图5： **使用布局调色板更改字幕位置**

下表概述了常用控件的标签放置规则。

| 控件类型 | 投放规则 |
|--------------|-----------------|
| 文本输入（包括日期、时间和密码字段） | 将标题放在控件的左侧（默认）。 如果无法执行此操作，请将其放在紧靠其上方或下方。 标签应该放置在靠近控件的位置，以利于放大视图中的标签和控件一起显示。 |
| 复选框 | 将标题放在复选框的右侧（默认）。 对于表格单元格中的复选框控件，屏幕阅读器将朗读您为对象指定的任何标题、工具提示或自定义屏幕阅读器文本。 如果要将列标题用作表中复选框的替换文本，则不要提供标题、工具提示或自定义屏幕阅读器文本。 |
| 单选按钮群组 | 通过创建静态文本元素并将其放在组的左侧或上方，为单选按钮组创建可见标题。 对于每个单选按钮，将标签放在右侧（默认）。 |
| 下拉列表 | 将标题放在对象的左侧（默认）。 如果无法执行此操作，请将其放在紧靠其上方的位置。 对于表格单元格中的下拉列表控件，屏幕阅读器将朗读您为对象指定的任何标题、工具提示或自定义屏幕阅读器文本。 如果要使用列标题作为表中这些对象的替换文本，则不要提供标题、工具提示或自定义屏幕阅读器文本。 |
| 列表框 | 默认情况下，创建标题时，标题位于列表框上方。 |
| 按钮 | 题注会自动放置在按钮上，无需手动放置。 确保描述文本正确描述了按钮的用途。 |


### 动态填充工具提示或自定义屏幕Reader文本

您还可以使用数据源的值动态填充表单控件的替换文本，例如其工具提示。 例如，您可以为法语对象显示自定义工具提示。
您连接的架构可以为工具提示定义以下内容：


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


您指向的数据文件可以为工具提示定义以下内容：

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. 在“对象库”调色板中，单击“标准”类别并将对象拖到窗体设计上。 例如，插入文本字段对象。
1. （可选）在“对象”(Object)面板中，单击“字段”(Field)选项卡，然后在“题注”(Caption)框中键入对象的题注。 例如，键入Quanté。
1. 在“辅助功能”面板中，单击“工具提示”活动标签。
1. 选择数据连接。
1. 单击“绑定”框旁边的三角形，然后选择一个绑定。 例如，选择“工具提示”>“@dp_tt”。

绑定框中将显示以下字符串：$record.tooltip.dp_tt提示：可以在“项”框中键入此字符串，而不是选择它。
1. 单击“确定”。
1. 在预览PDF选项卡中查看表单。

### 提供链接文本

使用辅助技术的用户可能有不同的阅读链接文本的方法。 例如，屏幕阅读器用户通常使用链接列表（如图6中所示的列表）来快速扫描页面上的可用链接。

![JAWS链接列表对话框](/help/forms/using/assets/image-6.png)

图6： **JAWS链接列表对话框**

因此，链接必须是自我描述的；这就是其含义不应取决于其上下文（周围的文本）。 例如，单词“click here”可能形成短语“click here to download our application form”中的实际链接元素。 在阅读链接列表时，此类链接将难以理解，尤其是当存在多个包含相同文本的链接时。

在表单中使用链接时，请确保每个链接都正确描述了其用途，而不依赖于其在页面上的周围文本或位置。 例如，不要使用“单击此处”之类的短语作为链接文本，而应使用“下载申请表单”作为链接文本。

**相关检查点**

* 第508款§1194.21
   * (d)辅助技术应提供有关用户界面元素的充分信息，包括元素的身份、操作和状态。 当图像表示项目群元素时，由图像传递的信息还必须以文本形式提供。
   * (l)使用电子表单时，该表单应让使用辅助技术的人员能够访问填写和提交表单所需的信息、字段要素和功能，包括所有指示和提示。
* 第508款§1194.22
   * (n)电子表格设计成在线填写时，表格应允许使用辅助技术的人获得填写和提交表格所需的信息、栏位要素和功能，包括所有指示和提示。
* WCAG 1.0
   * 12.4将标签与其控件明确关联(P2)。
   * 13.1明确确定每个链接的目标(P2)。
* WCAG 2.0
   * 1.1.1非文本内容：呈现给用户的所有非文本内容都具有相同用途的替换文本，以下所列情况除外。 （A级）
   * 2.4.6标题和标签：标题和标签用于描述主题或目的。 （AA级）
   * 3.2.4一致的标识：一组网页内具有相同功能的组件均采用一致的方式进行标识。 （AA级）
   * 3.3.2标签或说明：内容需要用户输入时提供标签或说明。 （A级）
   * 4.1.2名称、角色、值：对于所有用户界面组件（包括但不限于：表单元素、链接和脚本生成的组件），其名称和角色可以通过编程方式确定；可由用户设置的状态、属性和值可以通过编程方式设置；而且用户代理（包括辅助技术）可以收到这些项目的更改通知。 （A级）


## 确保阅读和制表符顺序正确 {#ensure-reading-tab-order}

在设计面向视力障碍或其他残障用户的表单时，确保有意义的阅读顺序非常重要。 这些用户通常不使用鼠标在表单中导航，因此他们依赖键盘。 阅读顺序决定了屏幕阅读器用户在阅读表单时使用的顺序。 此外，Tab键顺序允许用户使用Tab或Shift+Tab键从一个交互式表单控件快速移动到下一个控件。 逻辑标签顺序可确保用户有权访问表单上的所有字段，并且能够以合理且高效的方式导航表单。

表单的阅读顺序包括所有静态对象（如文本和图像）和字段对象，但只有交互式表单控件是Tab键顺序的一部分。

>[!NOTE]
> 在许多情况下，标签顺序与阅读顺序密切相关。 为简单起见，在本指南中，术语“tab order”将取代“tab or reading order”。

### LiveCycle Designer Forms中的默认选项卡顺序

将表单另存为带标记的PDF时，会自动创建默认选项卡顺序。 最初，使用下列规则根据对象的本地位置确定表单中的制表符顺序：

* 从表单的左上角开始，所有对象都按从左到右、从上到下（局部顺序）的顺序排列。
* 您创建的任何子表单都被视为自包含单元，并且还会从左到右、从上到下导航。 如果两个子表单彼此相邻，且都包含对象，则读取顺序将在移动到下一个子表单之前浏览第一个子表单中的所有对象。

对于简单表单（即具有从左至右、从上至下的布局的表单），默认选项卡顺序通常是正确的。 要验证这一点，应在发布表单之前检查默认的Tab键顺序。 您可以通过以下任一方法使选项卡顺序可见：

* 选择“视图”>“显示标签顺序”。
* 在Tab Order调色板中单击Show Order。

所有对象都将显示在右上角的编号，指示对象在默认Tab键顺序中的位置。 此序列中的交互式对象构成了Tab键顺序。 图7显示了基本表单的阅读顺序可视化图表。

![典型订单的默认阅读顺序可视化图表](/help/forms/using/assets/image-7.png)

图7： **典型订单的默认阅读顺序可视化图表**

每个标签顺序编号均以彩色形式显示。 这些形状具有以下含义：
* 灰色圆(#1和#4)用于内容区域中的对象。
* 绿色圆(#6和#7)用于母版页对象。
* 淡紫色正方形(#2和#3)用于片段内的对象。

您可以选择仅显示交互式表单控件（它构成了选项卡顺序）或读取顺序中的所有对象（其中还包括静态对象，如文本和图像）。 要更改此首选项，请选择“工具”>“选项”>“标签顺序”，然后选择“仅显示字段的标签顺序”。

在复杂的表单中，可能很难看到Tab键如何从一个对象流向另一个对象。 您可以使用可视化辅助工具来帮助您查看表单上的Tab键浏览流程。 在打开可视化辅助的情况下，当您将指针悬停在对象上时，蓝色箭头会以Tab键顺序显示前两个对象和后两个对象的Tab键浏览流程（见图8）。

![可视化辅助工具突出显示选项卡顺序](/help/forms/using/assets/image-8.png)

图8： **视觉辅助突出显示Tab键顺序**

要启用可视辅助，请使用以下方法：
* 选择“工具”>“选项”>“Tab键顺序”，然后在“Tab键顺序”面板中选择“显示Tab键顺序的其他可视化帮助”。
* 在Tab Order调色板菜单中，选择“显示可视辅助”。

### 使用位置影响默认选项卡顺序

要影响默认制表符顺序，可以通过将对象移动到其他位置来更改对象的坐标。 例如，在图9中，“Product Name（产品名称）”字段出现在“Quantity（数量）”字段之前的标签顺序中。 要更改此订单，您可以移动“产品名称”字段，使其位于“数量”字段的下方或右侧。

![默认的Tab键顺序从左到右](/help/forms/using/assets/image-9.png)

图9： **默认制表符顺序从左到右**

通过执行以下操作之一，可以更改对象的位置：
* 使用鼠标拖动它
* 选择它，然后使用键盘箭头键移动它。

>[!NOTE]
> 通过选择“视图”>“对齐网格”来保持对象对齐很有用。

可以使用“布局”调色板更精确地更改对象的坐标（如图10所示）。 使用此调色板，您可以指定X和Y坐标以及对象的宽度和高度。

![使用坐标以使用布局调色板精确定位对象](/help/forms/using/assets/image-10.png)

图10： **使用坐标以使用布局调色板精确定位对象**

>[!NOTE]
> 当字幕和控件不合并时，表单控件字幕的位置与屏幕阅读器读取对象及其元素的顺序无关。 有关字幕的更多信息，请参阅本指南中的2.5部分“为表单控件提供适当的标签” 。

### 使用子表单影响默认选项卡顺序

如上所述，子表单允许您插入具有自己的选项卡顺序的对象组。 您可以通过执行以下操作之一来创建子表单：
* 选择“插入”>“标准”>“子表单”。
* 在“层次”调色板中选择对象，然后通过选择“插入”>“在子表单中换行”将其分组到子表单中。
* 选择实际表单中的对象，右键单击所选内容，然后选择“在子表单中换行”

当两个包含字段对象的子表单并排放置时，Tab键序列将在移到下一个子表单之前遍历第一个子表单中的字段。 图11说明了这一点，其中使用两个子表单创建基于列的默认选项卡顺序。

![使用子表单的默认选项卡顺序](/help/forms/using/assets/image-11.png)

图11： **使用子表单的默认制表符顺序**

子表单、单选按钮和内容区域，以及页面及其母版页上对象的垂直位置，都会影响选项卡的顺序。

### 使用“选项卡顺序”调色板创建自定义选项卡顺序

当您需要表单中的不同顺序时，您可以更改默认选项卡顺序，而无法在子表单中进行定位或分组来实现此更改。 要更改默认标签顺序，您可以使用“标签顺序”调色板创建自定义标签顺序。
Tab键顺序调色板（见图12）允许您检查和修改表单中的对象通过辅助技术读取和通过用户Tab键导航的顺序。

![Tab键顺序调色板](/help/forms/using/assets/image-12.png)

图12： **Tab键顺序调色板**

“Tab键顺序”调色板提供了表单上选项卡顺序的替代视图。 它将表单上的所有对象显示为编号列表，其中每个编号表示对象在Tab键流中的位置。
要打开“标签顺序”调色板，请选择“窗口”>“标签顺序”。


“Tab键顺序”调色板提供了以下可视标记：
* 灰色条标记表单的每个页面。 每个页面上的Tab键顺序均以数字1开头。
* 绿色圆圈内的字母M表示母版页对象(仅在查看“设计视图”(Design View)选项卡上的表单时可见)。
* 数字范围表示片段中的对象。
* 黄色背景表示当前选定的项目。
* 页面上第一个对象旁边的锁定图标表示无法在选项卡顺序中移动该对象（仅当在“母版页”选项卡上查看表单时才可见）。

当您选择“视图”>“显示标签顺序”时，列表会显示与表单本身显示的标签顺序编号相同的标签顺序编号。 通过在“选项卡顺序”调色板列表中上下移动对象，可以更改对象在选项卡顺序中的位置。 您可以移动单个对象或一组对象。 这可以通过以下方法之一实现：

* 将所选对象在列表中上下拖动，并将其放置在所需位置。 在放置对象之前，黑色控制滑块会标记您在列表中的当前位置。
* 在“Tab键顺序”调色板中，单击向上或向下箭头按钮，直到所选对象置于正确位置为止。 或者，按Ctrl +向上箭头键或Ctrl +向下箭头键。
* 在Tab Order调色板菜单中，选择“上移”或“下移”。
* 在“Tab键顺序调色板”列表中，单击所选对象（或将其选中并按F2）以使对象名称旁边列出的编号可编辑。 然后，键入数字以指示对象在Tab键顺序中的新位置，然后按Enter。
* 从“Tab键顺序”调色板菜单中选择“复制”，然后在列表中选择要在其上放置移动对象的对象，然后从菜单中选择“粘贴”。

当您将对象按顺序移动到新位置时，LiveCycle Designer会重新分配制表符顺序编号。 尽管位于主页上的对象的选项卡顺序显示在“设计视图”选项卡上，但您只能在“主页”选项卡上更改这些对象的顺序。 如果在表单中使用片段引用，则在查看表单的顺序时，将显示片段中的Tab顺序。 要更改片段内的选项卡顺序，必须打开片段源文件以进行编辑，进行更改并保存文件。 使用此片段的任何表单都受此更改的影响。

如果您决定不希望在表单上自定义标签顺序，则可以使用以下步骤快速返回到自动（默认）标签顺序（您将丢失对标签顺序所做的任何更改）：
1. 在Tab Order调色板上，选择Automatic。
1. 在出现的消息框中，单击“是”以确认删除自定义选项卡顺序。

**相关检查点**
* 第508款§1194.21
   * (a)当软件被设计为在具有键盘的系统上运行时，产品功能应该从键盘上执行，其中功能本身或执行功能的结果可以从文本上辨识。
* WCAG 1.0
   * 9.2确保任何具有自己界面的元素均能够以独立于设备的方式操作。
* WCAG 2.0
   * 1.3.2有意义的顺序：当内容的呈现顺序影响内容含义时，可以通过编程方式确定正确的阅读顺序。 （A级）
   * 2.1.1键盘：内容的所有功能均可通过键盘界面操作，且不需要任何击键时间限制，除非底层功能需要依赖于用户移动路径而非单纯依赖于端点的输入。 （A级）
   * 2.1.3键盘（无例外）：内容的所有功能均可通过键盘界面操作，无需为每次击键设置特定的时间安排。 （AAA级）
   * 2.4.3焦点顺序：如果网页可以按顺序导航，并且导航顺序会影响含义或操作，则可聚焦组件会按照保留含义和可操作性的顺序接收焦点。 （A级）


## 确保表单控件可使用键盘{#ensure-keyboard-accessible}

用户必须能够仅使用键盘或等效的替代输入设备完全填写表单。 行动不便或视力不佳的用户可能别无选择，只能使用键盘，而许多使用鼠标的用户只是更喜欢使用键盘输入。 通过允许使用各种输入方法，您不仅可以创建无障碍表单，还可以创建更适合所有用户偏好的表单。

在LiveCycle Designer中，确保控件可使用键盘的最简单方法是使用“对象库”面板中“常用”选项卡下列出的控件。 默认情况下，这些控件会同时响应鼠标和键盘输入。 有关更多信息，请参阅本指南中的2.3选择正确的控制项。

键盘辅助功能的另一个重要方面是确保每个交互式元素均属于表单的选项卡顺序。 这允许用户使用Tab和Shift+Tab键在表单中前后移动光标。 请确保设置包括所有字段和按钮的逻辑选项卡顺序。 有关更多信息，请参阅本指南的2.6部分。确保阅读和制表符顺序正确。

最后，确保脚本化行为也可在键盘上访问，并且不依赖于设备特定的事件也很重要。 例如，鼠标事件MouseEnter无法使用键盘执行。 此外，此类事件处理程序不得干扰键盘辅助功能。 例如，确保下拉列表或列表框中使用的更改事件不会触发意外操作。

**相关检查点**
* 第508款§1194.21
   * (a)当软件被设计为在具有键盘的系统上运行时，产品功能应该从键盘上执行，其中功能本身或执行功能的结果可以从文本上辨识。
* WCAG 1.0
   * 6.4对于脚本和小程序，请确保事件处理程序独立于输入设备(P2)。
   * 9.2确保任何具有自己接口的元件能够以独立于设备的方式操作(P2)。
   * 9.3对于脚本，请指定逻辑事件处理程序，而不是依赖于设备的事件处理程序(P2)。
* WCAG 2.0
   * 2.1.1键盘：内容的所有功能均可通过键盘界面操作，且不需要任何击键时间限制，除非底层功能需要依赖于用户移动路径而非单纯依赖于端点的输入。 （A级）
   * 2.1.2无键盘陷阱：如果可以使用键盘界面将键盘焦点移动到页面的某个组件，则焦点应可通过键盘界面从该组件上移开；如果除了通过未修改的箭头、Tab键或其他标准退出方法外，上述移开功能还需通过其他手段实现，则应告知用户将焦点移开的方法。 （A级）
   * 2.1.3键盘（无例外）：内容的所有功能均可通过键盘界面操作，无需为每次击键设置特定的时间安排。 （AAA级）


## 负责任地使用颜色{#use-color-responsibly}

为辅助功能设计表单涉及考虑有关使用颜色的一些其他准则。 设计人员使用颜色来通过突出显示各种表单组件来改善表单的外观。 但是，如果颜色使用不当，可能会使残障人士难以或无法阅读您格式的信息。

### 不要只使用颜色来传达信息

颜色可以强调和增强表单的某些部分，但您不应仅通过颜色来传递信息。

盲用户无法访问仅以颜色（具有语义意义的颜色）传递的任何信息。 这同样适用于色觉缺失的用户或使用不同配色方案的用户，例如具有白色文本的高对比度彩色屏幕或黑色背景中的前景。 您还必须记住，屏幕阅读器无法自动检测颜色信息。

例如，图13显示了带有红色标题（使用字体调色板指定）的表单字段，以指示该表单字段是必填字段。 在本例中，颜色是必填输入字段和可选输入字段之间差异的唯一表示符，这使得盲用户或具有特定类型色盲的用户无法区分它们。

![单独使用颜色传递信息](/help/forms/using/assets/image-13.png)

图13： **单独使用颜色传递信息**

要解决此问题，请在表单控件的替换文本中指明表单所需的状态（如2.5部分中所述，为表单控件提供适当的标签）。 例如，您可以将屏幕阅读器文本设置为“邮政编码（必需）”。 对于难以查看特定组合中的颜色的用户，除了指示该字段为必填的替换文本之外，建议在“对象”调色板中将文本字段类型设置为“用户输入 — 必需”。 或者，您也可以使用颜色以外的指示，如可视文本、文本样式和边框样式。 但是，对于屏幕阅读器用户，您仍必须使用“辅助功能”调色板传达所需的信息。

此外，在向表单用户提供描述或说明时，请记住，仅基于颜色的声明对于视觉障碍用户是不够的。 例如，不要使用诸如“单击绿色按钮以继续”之类的语句，而是使用文本描述进行操作，如“单击下一步按钮以继续”。

>[!NOTE]
> 这一最佳做法并不禁止使用颜色。 它禁止使用颜色作为传达重要信息的唯一手段。 如果这种信息仍然需要视觉指示，设计者可以使用星号或类似视觉指示器来标记必填字段。

### 提供足够的颜色对比度

许多视力障碍的用户依赖文本和背景之间的高对比度来阅读表单。 当背景色和前景色之间的对比度不足时，表单可能会变得难以阅读，如果不是无法阅读的话。 图14显示了对比度不足的表单示例。

![颜色对比度不足的表单](/help/forms/using/assets/image-14.png)

图14： **颜色对比度不足的表单**

强烈建议您使用默认字体和背景颜色：白色背景中的黑色。 如果必须更改这些默认颜色，请务必选择高对比度颜色的适当组合；在浅色背景颜色上使用深色前景色，反之亦然。 要确定，请使用工具（如WAT-C颜色对比度分析器）来验证对比度是否足够。

Adobe Reader和Adobe Acrobat允许用户指定为满足视觉需求是否必须替换颜色。 用户可以指定自己的对比度方案，也可以选择使用操作系统提供的方案。 此外，Adobe Reader和Adobe Acrobat拥有自己的高对比度方案，这些方案可能会启用。 要使这些选项成功，最好的方法始终使用缺省颜色。

在设计表单时，请经常使用颜色方案设置对其进行测试，这与许多视力障碍用户将用于完成表单的设置类似。 此实践可帮助您在设计过程的早期发现并更正问题。

建议使用颜色：
* 确保语义颜色不可见时不会丢失任何信息。
* 如果无法使用默认颜色，请确保颜色具有高对比度，如在浅（白）背景上为黑色。 视力缺佳的用户通常需要在文本及其背景之间保持高对比度才能阅读文本。
* 通过在Windows以及Adobe Reader或Adobe Acrobat中将屏幕切换为高对比度显示来测试表单的可读性。 Mac OSX仅为高对比度提供简单的灰度过滤器，因此这不足以进行测试。
* 不要仅根据颜色传达信息。 例如，不要只使用颜色来高亮显示重要的文本段。 此外，还可以使用其他突出显示方法和文本描述。
* 请勿使用太多颜色，因为这会使内容中的实际信息难以阅读。 在决定使用何种颜色时，应始终将信息的可读性作为首要任务。

**相关检查点**
* 第508款§1194.21
   * (i)不得以颜色编码作为传达信息、指示行动、提示回应或区分视觉要素的唯一手段。
* WCAG 1.0
   * 2.1确保以颜色传递的所有信息也无颜色可用，例如上下文或标记中的信息。
   * 2.2确保前景色和背景色组合在出现颜色缺陷的人查看时或在黑白屏幕上查看时提供足够的对比度。 [图像的优先级2，文本的优先级3] (P2)。
* WCAG 2.0
   * 1.4.1使用颜色：颜色不是传达信息、指示行为、提示响应或区分视觉元素的唯一视觉手段。 （A级）
   * 1.4.3对比度（最小）：文本的可视呈现和文本的图像的对比度至少为4.5:1，以下情况除外：（AA级）
   * 1.4.6对比度（增强）：文本的可视呈现和文本的图像的对比度至少为7:1，以下除外：（AAA级）


## 为表提供标题单元格{#provide-heading-cells}

表格是以辅助功能形式组织和展示内容的有效方式。 如果使用得当，表的行和列可为表单内容提供可预测且一致的结构。 例如，当屏幕阅读器用户导航到正文行单元格时，屏幕阅读器会指定单元格位置，然后读取单元格内容。 屏幕阅读器使用行与列标题或行与列编号的组合来指定单元格位置。 由于屏幕阅读器提供的信息可将用户定向到表格中的内容位置，因此其布局将直接影响表格的辅助功能。

在构建表时，可以为表元素指定以下角色。 这些角色允许屏幕阅读器使用特殊快捷方式浏览表结构，并向用户传达表单元格和相应的标题单元格之间的关系。
* 表
将表的角色分配给所选子表单。 当用户导航到此子表单时，大多数屏幕阅读器都将其识别为表格，并指示行和列的数量。
* 标题行
将标题行的角色分配给所选子表单或表行。 在讲正文行单元格的内容时，大多数屏幕阅读器首先识别标题行中相应单元格的内容。
* 正文行
将正文行的角色指定给选定的子表单或表行。 如果单元格包含子表单，则屏幕阅读器通常会朗读标题行中相应单元格的内容，然后朗读子表单中的字段。
* 页脚行
将页脚行的角色分配给所选子表单或表行。
* （无）
指定传送有关表或其内容的信息的行。 该行不被视为表的一部分；但是，屏幕阅读器将读取其内容。

正确使用表格时，表格是组织和提供表格信息的有效方式。 避免过于复杂的表，例如那些带有嵌套表和节的表。

### 使简单表格可访问

建议使用具有简单布局的表。 简单表以单个标题行开始，后跟主体行。

在为辅助功能设计简单表格时，请牢记以下准则：

* 表格的选项卡顺序是地理顺序，这与表单本身的选项卡顺序相同。 确保编排表格内容，使其在从左到右、从上到下读取时合理。
* 大多数屏幕阅读器将表中的第一行解释为标题行。 在读取正文行单元格的内容时，这些屏幕阅读器首先读取关联的标题行单元格的内容。 确保每个标题行单元格中的内容对列内容进行了有意义的描述。
* 避免单元格跨越两列或多列、嵌套表或表节。 某些屏幕阅读器无法正确解读这些功能，或者可能无法使用这些功能。 例如，如果正文行中的某个单元格跨越两列，则在读取行中的下一个单元格时，屏幕阅读器可能不会引用标题行中的正确单元格内容。

### 使复杂表格可访问

在设计具有辅助功能的表时，请尽量简化表布局，即表头行后跟正文行。 当然，某些内容可能需要更复杂的表布局。 例如，您可能需要使用单元格跨度或多个标题来有效地传达内容。

您可以使用表对象或组合子表单对象来创建复杂的表。 表对象允许您使用旨在帮助设计过程的功能，例如用于插入列和行以及调整列和行大小的选项。

使用“辅助功能”调色板，可以为子表单指定与表格相关的角色，以创建可访问的复杂表格。 根据您的设计经验和首选项，您可以选择通过组合子表单对象来创建复杂的表。 例如，您可以创建一个包含两行的子表单，然后将此子表单指定为表的标题，再为表主体行指定另一个子表单。

使用子表单对象而不是表格对象创建表格时，需要执行以下附加步骤：
* 在“子表单”选项卡上，将每个子表单的类型设置为“已定位”。
* 在“辅助功能”面板中，为构成表的每个子表单设置适当的子表单角色。 例如，将标题行的角色分配给用作表标题的子表单。
* 对于传达有关表或其内容的信息但不被视为表的一部分的行，将子表单角色指定为“无”。 屏幕阅读器将读取行内容。

屏幕阅读器支持的功能决定了复杂表格所读取的信息。 例如，假定一个表包含一个标题行和一个具有标题行的节。 当用户导航到表部分的正文行单元格时，屏幕阅读器通常会按顺序阅读以下内容：
* 表标题行中相应单元格中的内容
* 部分标题行中相应单元格中的内容
* 选定单元格中的内容
但是，某些屏幕阅读器可能不会从两个标题行中读取内容。

为表创建有意义的可见名称或标题。 您可以在Adobe LiveCycle Designer中创建表名称作为静态文本，并将其放在表的前面。 您可以在子表单中将表及其名称组合在一起。 当您想要组合布局中的关联对象时，子表单特别有用。

对于表格单元格中的控件，屏幕阅读器将朗读您为对象指定的任何标题、工具提示或自定义屏幕阅读器文本。 如果要将列标题用作表中控件的替换文本，则不要提供标题、工具提示或自定义屏幕阅读器文本。 但是，请注意，此策略并不总是像屏幕阅读器用户那样清晰，因为屏幕阅读器可能仅在用户未处于屏幕阅读器的表单交互模式时才会将列标题与控件关联。

**相关检查点**
* 第508款§1194.22
   * (g)数据表的行标题和列标题应予识别。
   * (h)对于具有两个或多个行或列标题逻辑级别的数据表，应使用标记将数据单元格与标题单元格相关联。
* WCAG 1.0
   * 5.1对于数据表，请标识行和列标题(P1)。
   * 5.2对于具有两个或多个行或列标题逻辑级别的数据表，请使用标记将数据单元格与标题单元格相关联(P1)
* WCAG 2.0
   * 1.3.1信息和关系：通过呈现传递的信息、结构和关系可以通过编程方式确定或文本提供。 （A级）


## 提供可导航的窗体结构{#provide-navigable-form}

当表单变得长而复杂时，其易用性将受到其结构方式的极大影响。 正如书被分为章节和章节时更容易理解一样，表格被分为标题和副标题时也更容易使用。 此分区对于屏幕阅读器用户特别有用，原因如下：
* 每个标题都会告诉屏幕阅读器用户在标题后面的部分中可以预期的内容。
* 屏幕阅读器提供了快捷方式，以便在表单中的不同标题之间快速来回跳转，还允许用户访问标题列表，该列表提供了文档结构的概览并允许快速导航。

提供使用户能够跳到表单的其他区域的机制可使表单更加方便。 您可以使用LiveCycle Designer中的辅助功能调色板向表单添加标题结构。

### 提供跳过机制

视力正常的用户可以按任意顺序扫描页面。 他们可以先查看页面右下角，然后向后扫描内容。 屏幕阅读器用户没有此选项，因为屏幕阅读器将开始阅读左上角的页面（如源代码中所示），并以线性顺序移动。 此外，视力正常的用户还可以扫描页面以查找感兴趣的链接，并使用鼠标激活这些链接。 屏幕阅读器用户必须按顺序浏览页面。

提供可导航表单结构的最简单和最有效的方法是在表单中使用结构标题和正确定义的列表。
您还可以提供允许用户跳至表单其他区域的机制，例如，通过在表单的顶部和底部添加导航按钮。 在表单的顶部，可以包括“打开数据文件”、“上一页”和“下一页”等按钮。 在表单底部，您可以包括保存数据、电子邮件数据、转到页顶和打印等按钮。

智能字段可能是使某些表单更容易填写的有效方法。 例如，旅行申请表单可能具有多行多列字段。 如果特定行为空，则按该行中最后一个项目上的Tab键可能会跳转到表单的下一部分，而不是继续通过将保留为空的多个字段执行Tab键。

### 使用辅助功能面板添加标题

您可以使用“辅助功能”调色板，根据对象的用途将角色分配给对象。 可以应用这些角色在不同级别创建标题。

![在辅助功能面板中指定标题角色](/help/forms/using/assets/image-15.png)
图15： **在辅助功能面板中指定标题角色**

按照以下步骤在您的表单中创建标题：

1. 使用静态文本标签标识表单中每个逻辑段的开头，
1. 对于每个标签，在“辅助功能”面板中选择一个标题选项作为“角色”。 不同的标题级别（1到6）允许您在表单中创建标题结构。 从级别1开始，然后使用级别2等用于嵌套子节。

大多数屏幕阅读器允许用户根据其级别在标题元素之间快速导航。 图16显示了使用标题划分为较小区段的表单。 在此示例中，使用以下标题结构：

* 标题级别1：产品请求
   * 标题层2：订单详细信息
      * 标题级别3：提交选项
* 标题级别2：其他信息
   * 标题级别3：个人详细信息
   * 标题级别3：地址

![使用标题构建表单](/help/forms/using/assets/image-16.png)

图16： **使用标题构造表单**

这些标题只是静态文本元素，它们被赋予特定的字体大小和具有适当级别的标题角色。

>[!NOTE]
> 只是将文本标签的可视外观更改为类似标题不会使屏幕阅读器将其识别为标题。 您必须应用标题角色。

始终确保标题级别的顺序符合逻辑。 例如，2级标题的子部分必须始终为3级标题；标记子部分时，绝不能跳过这些级别。 屏幕阅读器用户使用不同的级别来更好地了解表单的结构。 例如，遇到2级标题后，用户可使用快捷方式查找第3级标题并确定是否存在任何子部分。 如果跳过级别，用户将难以标识这些子部分。

### 标记列表

有时，将列表内容添加到表单可能也有用。 列表可用于将相关项目组合在一起，它们允许屏幕阅读器用户了解列表中的项目数并快速导航超过该列表。 正确标记列表可使屏幕阅读器用户更清楚地了解表单的结构。

在LiveCycle Designer中，您可以使用子表单创建列表，步骤如下：

1. 选择包含将标记为列表项内容的子表单。
1. 在“辅助功能”面板中，选择“列表”作为“角色”。
1. 在“列表”子表单中选择每个嵌套子表单，并将其“角色”设置为“列表项”。

>[!NOTE]
> 只能将列表项角色分配给指定列表角色的子表单中包含的子表单。 不能将表或表行定义为列表项或列表项；但是，列表项可以包含表。

**相关检查点**
* 第508款§11934.22
   * (o)应提供允许用户跳过重复导航链路的方法。
* WCAG 1.0
   * 3.5使用页眉元素来传达文档结构，并根据规范(P2)使用它们。
   * 3.6正确标记列表和列表项。 (P2)。
   * 12.3将大信息块划分成更易于管理的组，这些组在适当的情况下是自然的。 (P2)。
   * 13.3提供关于网站总体布局的信息（如网站地图或目录）。
   * 13.4以一致的方式使用导航机制(P2)。
* WCAG 2.0
   * 1.3.2有意义的顺序：当内容的呈现顺序影响内容含义时，可以通过编程方式确定正确的阅读顺序。 （A级）
   * 2.4.1绕过块：提供一种机制，绕过多个网页上重复出现的内容块。 （A级）
   * 2.4.5多种方式：除了通过进程或步骤生成网页之外，还有其他方法可用于在一组网页中查找网页。 （AA级）
   * 2.4.6标题和标签：标题和标签用于描述主题或目的。 （AA级）
   * 2.4.10章节标题：章节标题用于整理内容。 （AAA级）
   * 3.2.3一致的导航：在一组网页内的多个网页上重复使用的导航机制，这些网页每次均以相同的相对顺序重复出现，除非用户自发更改浏览顺序。 （AA级）


## 避免中断脚本{#avoid-disruptive-scripting}

在表单设计过程中，表单开发人员可以使用脚本提供更丰富的用户体验。 您可以将脚本添加到大多数表单字段和对象。 例如，可创建简单脚本以动态更新交互式表单上的值以响应用户输入。

在设计用于辅助功能的脚本时，请考虑以下一般准则：

* 保持表单内容免受视觉干扰。 例如，避免使用导致内容闪烁、闪烁或移动的功能。
* 确保弹出窗口仅作为用户启动的操作的结果出现。 同样，除非用户启动，否则不允许表单的当前焦点（用户的当前视图）发生更改或内容重新显示。 例如，如果用户正在填写表单下半部的字段，则除非用户选择导航到此位置，否则不允许焦点更改为表单的左上角。
* 残障用户可能需要更多时间来提供字段输入。 请勿为输入字段指定基于时间的响应。
* 请注意，如果客户端脚本更改客户端应用程序的焦点，则可能会干扰屏幕阅读器和键盘。 例如，当与下拉列表或列表框一起使用时，更改和mouseEnter事件可能会导致意外操作。 验证您的客户端脚本不会给屏幕阅读器用户和仅使用键盘的用户带来问题。
* 使用辅助技术的用户有时需要额外的时间来完成任务。 在定时例程即将过期的任何情况下，显示可访问消息以允许扩展。 通过JavaScript创建的警报框可通过辅助技术使用。 也可以部署带有消息的新窗口，该消息提醒用户即将超时。

**相关检查点**：
* 第508款§1194.22
   * (l)当页面使用脚本语言显示内容或创建界面元素时，脚本提供的信息应以辅助技术可读取的功能文本进行标识。
   * (p)当需要定时响应时，应提醒用户并给予足够的时间以指示需要更多时间。
* WCAG 1.0
   * 1.4对于任何基于时间的多媒体演示（例如电影或动画），将等效的替代形式（例如视觉轨迹的字幕或听觉描述）与演示(P1)同步。
   * 6.2确保在动态内容发生更改时更新动态内容的等效项。
   * 6.3确保在关闭或不支持脚本、小程序或其他编程对象时可以使用页面。 如果无法执行此操作，请在可访问的替代页面上提供等效信息。
   * 6.5确保动态内容可访问或提供替代演示文稿或页面(P2)。
   * 8.1使编程元素（如脚本和小程序）可直接访问或与辅助技术兼容[优先级1（如果功能重要且不会出现在其他位置）]，否则(P2)。
   * 9.3对于脚本，请指定逻辑事件处理程序，而不是依赖于设备的事件处理程序(P2)。
   * 10.1在用户代理允许用户关闭衍生窗口之前，不要出现弹出窗口或其他窗口，并且不要在未通知用户的情况下更改当前窗口。
* WCAG 2.0
   * 3.2.1聚焦：当任何组件收到焦点时，它不会发起对上下文的更改。 （A级）
   * 3.2.2输入：更改任何用户界面组件的设置不会自动导致上下文更改，除非在使用组件之前已告知用户该行为。 （A级）
   * 3.2.5请求时更改：上下文更改仅由用户请求启动，或者有机制可以关闭此类更改。 （AAA级）

## 确保所有音频和视频内容都可访问{#ensure-audio-video-accessible}

如果您的表单包含音频或视频内容（包括音频和视频剪辑），则必须确保此内容可供访问。 具体来说，请确保合并到表单中的视频剪辑包含适用于耳聋和听力缺佳用户的字幕（有时也称为字幕）以及适用于盲用户的视频描述。 对于未与视频内容同步的音频文件，只需简单的转录文件即可。
对于基于Flash的媒体，请参阅[链接](/help/forms/using/best-practices-for-creating-forms-in-designer.md)以了解有关提供字幕的信息。

**相关检查点**：
* 第508款§1194.22
   * (b)任何多媒体演示的同等替代方案应与演示同步。
* WCAG 1.0
   * 1.1为每个非文本元素提供等效文本（例如，通过“alt”、“longdesc”或在元素内容中）。 这包括：图像、文本的图形表示（包括符号）、图像映射区域、动画（例如动画GIF）、小程序和程序化对象、ASCII艺术、框架、脚本、用作列表项目符号的图像、分隔符、图形按钮、声音（无论是否经过用户交互播放）、独立音频文件、视频的音频轨道和视频(P1)。
   * 1.3在用户代理能够自动朗读视觉轨迹的等效文本之前，提供对多媒体演示的视觉轨迹的重要信息的听觉描述(P1)。
   * 1.4对于任何基于时间的多媒体演示（例如电影或动画），将等效的替代形式（例如视觉轨迹的字幕或听觉描述）与演示(P1)同步。
* WCAG 2.0
   * 1.2.1纯音频和纯视频（预先录制）：对于预先录制的纯音频和纯视频媒体，除非音频或视频是文本的替代媒体，并且明确进行了相应标记，否则不会出现以下情况：（A级）
   * 1.2.2字幕（预先录制）：为同步媒体中所有预先录制的音频内容提供了字幕，除非该媒体是文本的替代媒体，且明确进行了相应标记。 （A级）
   * 1.2.3音频描述或替代媒体（预先录制）：为同步媒体提供基于时间的媒体或预先录制的视频内容的音频描述的替代方法，除非该媒体是文本的替代媒体，且明确进行了相应标记。 （A级）
   * 1.2.4字幕（实时）：为同步媒体中的所有实时音频内容提供了字幕。 （AA级）
   * 1.2.5音频描述（预先录制）：为同步媒体中所有预先录制的视频内容提供了音频描述。 （AA级）
   * 1.2.6手语（预先录制）：为同步媒体中所有预先录制的音频内容提供手语口译。 （AAA级）
   * 1.2.7扩展音频描述（预先录制）：如果前景音频的暂停不足以让音频描述传达视频的感觉，则为同步媒体中的所有预先录制的视频内容提供扩展音频描述。 （AAA级）
   * 1.2.8替代媒体（预先录制）：为所有预先录制的同步媒体和所有预先录制的纯视频媒体提供了基于时间的替代媒体。 （AAA级）
   * 1.2.9纯音频（实时）：提供一种基于时间的媒体的替代方法，该媒体为纯音频实时内容提供等效信息。 （AAA级）

## 识别自然语言和语言的任何更改{#identify-natural-language}

表单内容将由使用特定于语言的语音合成器的辅助技术读取，因此正确识别表单的主要语言以确保表单以预期语言读取很重要。

如果表单中的文本（或替换文本）以多种语言呈现，则必须确定表单中用于切换一种语言的区域。

在LiveCycle Designer中，通过设置表单的Locale属性和顶级子表单的Locale属性来设置主语言。 要标识对主要语言的更改，请更改使用表单语言以外的语言的任何对象的Locale属性。

要设置表单的Locale属性：
1. 选择“文件”>“表单属性”，然后选择“默认”选项卡
2. 为“Form Locale（表单区域设置）”选择相应的语言（请参见图17）
3. 单击“确定”

![在“表单属性”对话框中更改表单区域设置](/help/forms/using/assets/image-17.png)

图17： **在表单属性对话框上更改表单区域设置**

要设置顶级子表单的Local属性或需要不同语言的对象，请执行以下操作：
1. 在设计视图中选择顶级子表单或对象
1. 通过选择“窗口”>“对象”来显示“对象”调色板
1. 在“对象”面板中，选择“字段”选项卡，然后在“区域设置”列表中，选择要用于对象的语言（请参见图18）。 将不同的区域设置选项应用于单个对象时，请记住，表格和子表单中的对象会自动接收与表格和子表单对象相同的区域设置设置。

![更改对象的区域设置](/help/forms/using/assets/image-18.png)

图18： **更改对象的区域设置**

**相关检查点**：
* WCAG 1.0
   * 4.1清楚地识别文档文本和任何文本等效项（如标题）的自然语言变化。
* WCAG 2.0
   * 3.1.1页面语言：每个网页的默认人类语言可以通过编程方式确定。 （A级）
   * 3.1.2局部语言：内容中每个段落或短语的人类语言可以通过编程方式确定，但适当的名称、技术术语、不定语言的单词，以及成为紧邻文本白话一部分的单词或短语除外。 （AA级）
