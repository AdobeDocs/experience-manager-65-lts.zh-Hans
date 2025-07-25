---
title: 交互式通信中的文本
description: 创建和编辑要在交互式通信中使用的文本文档片段 — 文本是用于构建交互式通信的四种文档片段类型之一。 其他三个是条件、列表和布局片段。
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: ca18b9f4-9d06-4b15-81dd-68a6821e2e3e
source-git-commit: 6db207b08535c063e41b333054561036481e8db9
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 1%

---

# 交互式通信中的文本{#texts-in-interactive-communications}

## 概述 {#overview}

文本文档片段由文本的一个或多个段落组成。 段落可以是静态的或动态的。 动态段落可能包含表单数据模型属性和变量。 您还可以应用规则并在文本文档片段中重复。 例如，称呼中的客户名称可以是表单数据模型(FDM)属性，其值在运行时可用。 通过更改这些值，可以使用同一交互式通信为使用代理UI的不同客户准备交互式通信。

交互式通信中的文本文档片段支持以下类型的动态数据：

* **数据模型对象**：数据属性使用后端数据源。
* **基于规则的内容**：文本中根据规则显示或隐藏的部分内容。 规则也可以基于表单数据模型的属性和变量。
* **变量**：在文本文档片段中，变量未绑定到后端数据源。 在准备交互式通信以将其提交到后处理时，代理会填充/选择变量中的值或将变量绑定到数据源。
* **重复**：您的交互式通信中可能有动态信息，如信用卡对帐单中的交易，其发生次数会随着每次生成的交互式通信而不断变化。 使用重复，可以格式化并构建此类动态信息。 有关详细信息，请参阅[内联条件和重复](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/cm-inline-condition.html)。

## 创建文本 {#createtext}

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文本]**。
1. 指定以下信息：

   * **[!UICONTROL 标题]**： （可选）输入文本文档片段的标题。 标题不需要是唯一的，并且可以包含特殊字符和非英语字符。 文本通过其标题（如果可用）进行引用，例如在缩略图和属性中。
   * **[!UICONTROL 名称]**：文件夹中文本的唯一名称。 文件夹中不能存在任何状态下具有相同名称的两个文档片段（文本、条件或列表）。 在“名称”字段中，只能输入英语字符、数字和连字符。 根据“标题”字段自动填充“名称”字段。 在“标题”字段中输入的特殊字符、空格、数字和非英语字符将在“名称”字段中替换为连字符。 虽然“标题”字段中的值会自动复制到“名称”，但您可以编辑该值。

   * **[!UICONTROL 描述]**：键入文本描述。
   * **[!UICONTROL 表单数据模型]**： （可选）选择“表单数据模型”单选按钮以基于表单数据模型创建文本。 选择“表单数据模型”单选按钮时，会显示&#x200B;**[!UICONTROL 表单数据模型]**&#x200B;字段。 浏览并选择表单数据模型。 在为交互式通信创建文本和条件时，请确保您使用要在交互式通信中使用的数据模型。 有关表单数据模型的详细信息，请参阅[数据集成](/help/forms/using/data-integration.md)。

   * **[!UICONTROL 标记]**：若要创建自定义标记，请在文本字段中输入值，然后按Enter键（可选）。 保存此文本时，将创建新添加的标记。

1. 选择&#x200B;**[!UICONTROL 下一步]**。

   此时将显示“创建文本”页。 如果您已选择创建基于表单数据模型的文本，则表单数据模型属性会显示在左窗格中。

1. 键入文本并使用以下选项在文本中设置格式、条件化并插入表单数据模型属性和变量：

   * [表单数据模型](#formdatamodel)
   * [变量](#variables)
   * [规则编辑器](#rules)
   * [格式化选项](#formatting)

      * [从其他应用程序复制粘贴带格式的文本](#paste)

      * [突出显示文本的各个部分](#highlight)

   * [重复](/help/forms/using/cm-inline-condition.md)
   * [特殊字符](#special)
   * [搜索和替换文本](#searching)
   * [键盘快捷键](/help/forms/using/keyboard-shortcuts.md)

   >[!NOTE]
   >
   >您可以在文本编辑器中使用@符号添加表单数据模型元素、数据字典元素和变量。 在文本编辑器中输入以@开头的字符串时，将搜索所有数据模型元素、数据字典元素和变量，并显示包含所搜索字符串的元素或变量。 您可以在搜索结果中导航并选择元素或变量。 如果没有匹配结果，则显示&#x200B;*未找到匹配结果*&#x200B;消息。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   随即会创建文本。 现在，您可以在创建交互式通信时继续使用文本作为构建块。

## 编辑文本 {#edittext}

您可以使用以下步骤编辑现有文本文档片段。 您还可以选择在交互式通信编辑器中编辑文本文档片段。

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 导航到文本文档片段并将其选定。
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 进行所需的更改。 有关文本中选项的详细信息，请参阅[创建文本](#createtext)。
1. 选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 关闭]**。

## 使用表单数据模型属性个性化文本文档片段 {#formdatamodel}

您可以通过插入表单数据模型属性来个性化文本文档片段。 通过在文本中插入表单数据模型属性，您可以在预览交互式通信时从关联的数据源获取并填充特定于收件人的数据。 有关表单数据模型的详细信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

如果在创建文本时指定了表单数据模型，则表单数据模型中的属性会显示在文本编辑器的左窗格中。 对于文本文档片段和包含该片段的交互式通信，指定的表单数据模型应该相同。

![insertfdmelementtext](assets/insertfdmelementtext.png)

* 要将表单数据模型属性插入文本，请将光标放在要插入该属性的位置，然后通过点按左窗格中选择&#x200B;**[A]**&#x200B;属性，并选择&#x200B;**[!UICONTROL [B]添加选定项]**。 也可以双击属性将其插入到&#x200B;**[C]**&#x200B;光标位置。 表单数据模型属性以棕色背景颜色突出显示。

或者，可以使用文本编辑器中的@符号搜索和添加表单数据模型属性。 将光标放在要插入属性的位置。 键入@，后跟搜索字符串。 对文档片段中可用的所有表单数据模型属性和变量执行搜索操作。 将检索包含搜索字符串的属性或变量，并将其显示为下拉列表。 浏览搜索结果，然后单击要在光标位置插入的属性。 按Esc隐藏搜索结果。

* 要允许代理在[使用代理UI准备和发送交互式通信](/help/forms/using/prepare-send-interactive-communication.md)时在代理UI中编辑表单数据模型属性的值，请选择该属性的&#x200B;**[D]**&#x200B;锁定图标并确保它处于解锁状态。 属性的默认状态为锁定，代理无法在代理UI中编辑属性。

您还可以使用表单数据模型属性来构建用于显示或隐藏部分内容的规则。 有关详细信息，请参阅[在文本中创建规则](#rules)。

## 在文本文档片段中创建和使用变量 {#variables}

变量是可在创建交互式通信时绑定的占位符。 变量可以绑定到表单数据模型属性或文本片段。 还可以保留变量以供代理填充。

在以下情况下，您可以使用变量而不是表单数据模型属性：

* 文本文档片段用于多个交互式通信中，其中不同的交互式通信需要不同的绑定。
* 文本文档片段在创建时没有表单数据模型。 您可以在创建交互式通信时插入变量，然后将其绑定到表单数据模型属性。
* 您需要从文本文档片段中绑定和检索文本。 只有那些可以绑定到变量的文本文档片段不应具有中没有变量的变量。

创建或编辑文本文档片段时，您可以创建和插入变量。 您创建的变量将显示在代理UI的数据选项卡中。 代理在[使用代理UI](/help/forms/using/prepare-send-interactive-communication.md)准备和发送交互式通信时指定变量的值。

### 创建变量 {#createvariables}

1. 在左窗格中，选择&#x200B;**[!UICONTROL 变量]**。

   此时将显示“变量”窗格。

   ![变量窗格](assets/variablespane.png)

1. 选择&#x200B;**[!UICONTROL 创建]**。

   此时将显示“创建变量”窗格。

1. 输入以下信息并选择&#x200B;**[!UICONTROL 创建]**：

   * **[!UICONTROL 名称]** ：变量的名称。
   * **[!UICONTROL 描述]** ：可以选择输入有关变量的描述。
   * **[!UICONTROL 类型]** ：选择变量的类型：字符串、数字、布尔值或日期。
   * **[!UICONTROL 仅允许特定值]** ：对于String和Number变量，您可以确保代理从代理UI中占位符的特定值集中进行选择。 要指定值集，请选择此选项，然后指定&#x200B;**[!UICONTROL 值]**&#x200B;字段中允许使用逗号分隔的值。

1. 选择&#x200B;**[!UICONTROL 创建]**。

   随即会创建变量并将其列在“变量”窗格中。

1. 若要在文本中插入变量，请将光标放在适当的位置，选择变量，然后选择&#x200B;**[!UICONTROL 添加选定项]**。

   ![变量已插入](assets/variableinserted.png)

   变量以浅蓝色背景颜色突出显示，而表单数据模型属性以棕色背景颜色突出显示。

   或者，也可以在文本编辑器中使用@符号搜索和添加变量。 将光标置于要插入变量的位置。 键入@，后跟搜索字符串。 对文档片段中可用的所有表单数据模型属性和变量执行搜索操作。 将检索包含搜索字符串的属性和变量，并将其显示为下拉列表。 浏览搜索结果，然后单击要在光标位置插入的变量。 按Esc隐藏搜索结果。

1. 选择&#x200B;**[!UICONTROL 保存]**。

## 在文本中创建规则 {#rules}

在文本中使用规则编辑器，您可以创建规则以根据&#x200B;**预设条件**&#x200B;显示或隐藏文本字符串或内容段。 这些条件可以基于以下基础构建：

* 字符串
* 数字
* 数学表达式
* 日期
* 关联的表单数据模型的属性
* 您在文本中可能创建的任何变量

### 在文本中创建规则 {#create-rules-in-text}

1. 创建或编辑文本时，选择要使用规则条件化的文本字符串、段落或内容。

   ![selectcontentapplyrule](assets/selectcontentapplyrule.png)

1. 选择&#x200B;**[!UICONTROL 创建规则]**。

   此时将显示“创建规则”对话框。 除了字符串、数字、数学表达式和日期之外，规则编辑器中还提供以下内容来创建规则语句：

   * 关联的表单数据模型的属性
   * 您可能已创建的任何变量

   选择要评估的适当选项。

   ![ruleeditor](assets/ruleeditor.png) ![ruleeditorfdm](assets/ruleeditorfdm.png)

   >[!NOTE]
   >
   >不支持使用收藏集属性创建规则来条件化和显示文本。

1. 选择相应的运算符以计算规则，例如“等于”、“包含”和“开头为”。

   ![ruleeditorfdm-1](assets/ruleeditorfdm-1.png)

1. 插入求值表达式、值、数据模型属性或变量。

   ![根据FDM](assets/ruleeditorfdm-1-1.png)的源数据，如果收件人的位置是美国，则显示所选文本的规则

   根据FDM源数据在收件人位置为US时显示所选文本的规则

   * 创建或编辑规则时，您还可以选择![icon_resize](assets/icon_resize.png) （调整大小）以展开“创建规则”/“编辑规则”对话框。 展开的完整窗口对话框允许您拖放表单数据模型属性和变量来构建规则。 再次选择调整大小以返回创建规则对话框。
   * 您还可以在规则中创建多个条件。
   * 您还可以创建重叠规则，在该规则中，将规则应用于已应用规则的内容的一部分。

1. 选择&#x200B;**[!UICONTROL 完成]**。

   应用规则。 应用规则的文本或内容以绿色突出显示。 将鼠标悬停在高亮显示的左侧手柄上时，将显示应用的规则。

   ![appliedruletext](assets/appliedruletext.png)

   单击所应用规则的左侧手柄时，您将获得编辑或删除规则的选项。

## 设置文本格式 {#formatting}

创建或编辑文本时，工具栏会根据您选择的编辑类型而发生更改：“段落”、“对齐”或“列表”：

![选择工具栏类型](do-not-localize/toolbarselection.png)

选择工具栏类型：“段落”、“对齐方式”或“列表”

![字体编辑工具栏](do-not-localize/paragraphtoolbar.png)

字体编辑工具栏

![对齐工具栏](assets/alignmenttoolbar.png)

对齐工具栏

![列表工具栏](do-not-localize/listingtoolbar.png)

列表工具栏

### 突出显示/强调文本部分 {#highlight}

要高亮显示\强调可编辑文档片段中的文本部分，请选择该文本，然后选择“高亮显示颜色”。

![textbackgroundcolorapplied-1](assets/textbackgroundcolorapplied-1.png)

您可以直接选择基本颜色调色板中存在的基本颜色`**[A]**`，或者在使用滑块&#x200B;**选择相应的颜色阴影后选择**&#x200B;选择`**[B]**`。

或者，您也可以转到“高级”选项卡选择适当的色相、亮度和饱和度`**[C]**`以创建精确的颜色，然后选择“选择`**[D]**`”以应用颜色突出显示文本。

![textbackgroundcolor-2](assets/textbackgroundcolor-2.png)

### 粘贴格式化文本 {#paste}

要重用存在于其他应用程序(例如Microsoft®Word或HTML页面)中的文本的一个或多个段落，请复制该文本并将其粘贴到文本编辑器中。 复制的文本的格式将保留在文本编辑器中。

您可以在可编辑的文本文档片段中复制并粘贴文本的一个或多个段落。 例如，您可能拥有Microsoft® Word文档，其中包含可接受的居住证明项目符号列表，如下所示：

![pastetextmsword-2](assets/pastetextmsword-2.png)

您可以直接将文本从Microsoft® Word文档复制并粘贴到可编辑的文本文档片段中。 项目符号列表、字体和文本颜色等格式将保留在文本文档片段中。

![pastetexteditablemodule-1](assets/pastetexteditablemodule-1.png)

## 在文本中插入特殊字符 {#special}

如有必要，请在文档片段中插入特殊字符。 例如，可以使用“特殊字符”面板插入：

* 货币符号，如€、@和£
* 数学符号，例如∑、√、∂和^
* 标点符号，如&quot;和&quot;

![specialcharacters-2](assets/specialcharacters-2.png)

文本编辑器内置支持210个特殊字符。 管理员可以[通过自定义](/help/forms/using/custom-special-characters.md)添加对更多/自定义特殊字符的支持。

## 搜索和替换文本 {#searching}

使用包含大量文本的文本文档片段时，您需要搜索特定的文本字符串。 您可能还需要将特定文本字符串替换为替换字符串。

查找和替换功能允许您搜索（和替换）文本文档片段中的任何文本字符串。 该功能还包括强大的正则表达式搜索。

1. 打开文本文档片段以进行[编辑](#edittext)。
1. 选择&#x200B;**[!UICONTROL 查找和替换]**。

1. 在&#x200B;**[!UICONTROL 查找]**&#x200B;文本框中输入要搜索的文本并在&#x200B;**[!UICONTROL 替换]**&#x200B;文本框中输入新文本（替换文本），然后选择&#x200B;**[!UICONTROL 替换]**。

1. 如果找到搜索到的文本，该文本将被替换文本替换。

   * 如果找到搜索文本的其他实例，则该实例会在文本文档片段中突出显示。 如果再次选择&#x200B;**[!UICONTROL 替换]**，则高亮显示的实例将被替换，如果找到第三个实例，光标将向前移动。
   * 如果找不到其他实例，“查找和替换”对话框将显示消息：模块已到达末尾。

   您还可以选择全部替换以一次性替换所有匹配项。

   “查找和替换”还包括功能强大的正则表达式搜索。 要在搜索中使用正则表达式，请选择&#x200B;**[!UICONTROL 正则表达式]**，然后选择&#x200B;**[!UICONTROL 查找]**&#x200B;或&#x200B;**[!UICONTROL 替换]**。
