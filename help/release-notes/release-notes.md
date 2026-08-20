---
title: Adobe Experience Manager 6.5 LTS SP3的最新发行说明
description: 查找Adobe Experience Manager 6.5 LTS Service Pack 3的最新发行信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: d4d05cf9f295e6c3740ebf1e3559b5d117898342
workflow-type: tm+mt
source-wordcount: '6752'
ht-degree: 26%

---


# Adobe Experience Manager 6.5 LTS SP3的最新发行说明 {#release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 3 (SP3) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2026年8月20日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.3.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

<!-- **Mandatory Hotfix** – To avoid SNFE (SegmentNotFoundException) issues with offline compaction when installing SP2, install the hotfix described in [Known issues – Repository corruption during online compaction](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146). -->

## [!DNL Adobe Experience Manager] 6.5 LTS SP3中包含的内容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP3包括新增功能、客户请求的关键增强功能和错误修复。 自2025年3月6.5 LTS首次推出以来，它提高了整个平台的性能、安全性和本地化程度。 在 6.5 LTS 上[安装此服务包](#install-update)。

### 已修复问题概述 {#fixed-issues-overview}

[!DNL Adobe Experience Manager] 6.5 LTS， SP3解决了跨[!DNL Sites]和[!DNL Experience Manager Foundation]的问题。 这些修复提高了可访问性、创作可靠性、Headless内容交付、多站点管理和平台稳定性。 后面的部分列出了每个修复及其参考编号。

大多数更改适用于[!DNL Sites]：

* 最大组的辅助功能改进。 这些更新加强了页面编辑器、Assets侧边栏、筛选器和相关创作界面中的键盘导航、屏幕阅读器反馈、焦点管理、语义标记、文本对比度和触屏目标大小调整。
* [!DNL Content Fragments]中的修复跨越片段编辑器、模型编辑器、REST API和GraphQL API。 更新可更正本地化、字段验证、编辑行为和响应处理。
* MSM Live Copies修复允许作者从Blueprint页面可靠地转出更改并保留现有转出配置。
* Adobe Managed Services上提供跨渠道支持，包括所需的捆绑包、系统用户和配置。
* 其他修复针对管理员和经典界面、核心组件、组件控制台、Campaign集成、体验片段和启动项。

其余更改将应用于[!DNL Experience Manager Foundation]：

* 本地化更新跨运行状况报表、操作控制台和多个创作界面翻译以前仅含英文的文本。
* 稳定性修复可恢复运行状况监控端点，在间歇性配置错误后保持邮件服务运行，并更正工作流变量和工作流包编辑。
* 此版本还添加了AEM上下文服务支持，并解决了安全性、翻译和用户界面问题。

有关完整列表，请参阅[6.5 LTS Service Pack 3](#fixed-issues)中的已修复问题。


<!-- ## Key features and enhancements -->



<!-- UPDATE THE EACH RELEASE -->

## 修复了6.5 LTS Service Pack 3中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP3}

* AEM 6.5 LTS Service Pack 3包括Crossswalk包、内容包、系统用户、服务用户映射、功能切换和所需的OSGi配置。 全新安装会自动提供交叉通路先决条件，并且只需要特定于客户的运行时配置。 (SITES-41596)
* AEM 6.5 LTS，Service Pack 3更新`cq-wcm-core`以支持Adobe Managed Services上的交叉通行。 此更新添加了模板创建和通用编辑器访问权限，同时删除了过时的自定义代码和功能切换。 (SITES-37657)


#### 辅助功能 {#sites-accessibility-65-lts-sp3}

* 页面编辑器画布现在支持仅键盘组件管理。 作者可以使用“插入组件”、“剪切”、“粘贴”和“删除”来添加、重新排序和删除组件。 (SITES-25359)关键
* 现在，键盘用户无需使用拖放手势，即可在站点列表视图中重新排序表行。 键盘控件允许用户选择行，将其移动到其他位置，然后完成放置。 (SITES-24946)关键

* 自定义属性编辑器现在支持键盘交互及其格式控件。 作者可以在工具栏选项之间移动焦点、选择文本样式以及仅使用键盘设置属性值格式。 (SITES-40333)主要

* 现在，当可用的交互需要拖放时，键盘焦点会跳过侧面板组件列表。 此更改可防止键盘用户输入无法使用的组件选择工作流。 (SITES-40752)
* 现在，关闭叠加操作会将焦点恢复到其触发控制。 键盘和屏幕阅读器用户不再返回叠加图或失去其在界面中的位置。 (SITES-40819)
* 键盘导航不再将焦点移动到隐藏的页面内容。 此更改将保持可预测的焦点顺序，并防止导航中断。 (SITES-41430)
* “锁定”按钮现在可根据屏幕阅读器的标题提供精确的反馈。 用户会听到清晰的操作标签，而不是冗长的描述。 (SITES-41431)
* 现在，有一个视觉指示器标识“更改文件或文件夹”列表框中的选定选项。 该指示器可帮助用户了解痕迹导航路径并识别当前文件夹。 (SITES-25532)
* 屏幕阅读器现在会朗读一次升序或降序排序方向。 描述性标签清晰地标识按钮操作，并删除重复的反馈。 (SITES-25534)
* AEM Sites现在跨常见的创作工作流提供更广泛的无障碍支持。 更新可改善键盘交互、界面标签、焦点管理和辅助技术反馈。 (SITES-38239)
* 现在，工具栏项目在获得键盘焦点时会显示可见标签。 键盘用户可以在激活每个控件之前对其进行识别。 (SITES-40751)
* 键盘和屏幕阅读器用户现在可以离开收件箱菜单，而无需将其保持打开状态。 菜单会自动关闭，并保留清晰的导航路径。 (SITES-25518)
* 颜色样本现在显示具有足够对比度的选定状态图标。 更清晰的指示器可帮助用户识别不同背景颜色的活动色板。 (SITES-25523)
* 现在，编辑布局工具栏向辅助技术准确报告当前设备。 设备按钮不再建议用户打开和关闭每个按钮。 (SITES-25524)
* 搜索模式现在显示&#x200B;**排序依据**&#x200B;标签，并具有足够的文本对比度。 更新的样式提高了视力缺佳用户的可读性。 (SITES-25531)
* 站点列表视图排序按钮现在满足最低对比度要求。 用户可以在表格背景中更轻松地识别每种排序控件及其状态。 (SITES-25372)
* 当“筛选器”字段获得键盘焦点时，不再重新加载侧边栏Assets列表。 用户可以输入字段，而不会出现意外的内容移动或屏幕阅读器重复加载公告。 (SITES-25377)
* 内容片段侧边栏选项卡现在提供了一致的可访问标签。 NVDA声明选项卡名称，而不是声明选定的子导航项目。 (SITES-25509)
* 现在，当键盘或屏幕阅读器焦点移出帮助菜单时，该菜单将关闭。 用户可以继续导航标题控件或页面内容，而无需保持菜单打开。 (SITES-25517)
* 现在，在人口统计工具栏字段中输入的文本满足最低对比度要求。 用户可以在文本字段的背景中更清楚地阅读配置文件值。 (SITES-25318)
* “页面信息”菜单现在会显示具有足够文本对比度的聚焦选项。 更清晰的样式可帮助用户在整个菜单中跟踪键盘焦点。 (SITES-25321)
* Teaser、Image和Carousel对话框中的复选框现在向屏幕阅读器显示其相关说明。 当键盘焦点出现在每个复选框上时，用户会听到支持描述。 (SITES-25364)
* 文本编辑器控件现在将其当前状态传达给辅助技术。 屏幕阅读器标识活动段落格式和选定的超链接目标选项。 (SITES-25367)
* 屏幕阅读器现在可清楚地朗读&#x200B;**旋转设备**&#x200B;按钮和当前设备方向。 激活控件会报告新的方向，而不使用描述相反操作的标签。 (SITES-25292)
* 键盘导航现在会跳过折叠的人口统计工具栏中隐藏的控件。 用户可以在“布局预览”中移动，而不会遇到不可用的工具栏选项。 (SITES-25304)
* 在布局预览过程中，“人口统计”工具栏中的文本标签现在满足最低对比度要求。 用户可以在工具栏后台更清楚地阅读标签，例如推荐。 (SITES-25307)
* 人口统计工具栏现在显示具有足够对比度的按钮焦点指示器。 用户可以在键盘导航期间识别活动的Commerce、角色或设备控件。 (SITES-25308)
* 编辑布局工具栏为设备选择器使用分组的焦点指示器。 大纲包括相关的&#x200B;**选择设备**&#x200B;和&#x200B;**旋转设备**&#x200B;控件作为预期工具栏行为的一部分。 (SITES-25283)
* 当用户选择其他设备时，“编辑布局”工具栏不再截断&#x200B;**iPhone 8 Plus**&#x200B;标签。 在所有按钮状态中，完整设备名称都保持可见。 (SITES-25284)
* 编辑布局标尺现在为屏幕阅读器提供测量上下文。 用户会听到描述性标签和测量格式，而不是无法解释的一系列数字。 (SITES-25287)
* 当桌面视图处于活动状态时，“编辑布局”工具栏现在会突出显示&#x200B;**桌面**&#x200B;按钮。 视觉指示器使当前设备选择清晰。 (SITES-25290)
* 现在，键盘焦点在所有可用颜色的色板按钮上保持可见。 添加间距可防止焦点指示器混合到选定样本中。 (SITES-25253)
* 屏幕阅读器现在可以正确识别时间扭曲日期字段。 字段不再提供误导性反馈，这表示它将打开一个对话框。 (SITES-25263)
* 现在，注释按钮标签在其默认和悬停状态下满足最低对比度要求。 用户可以在按钮背景中清楚地阅读标签。 (SITES-25267)
* 屏幕阅读器现在在“注释”对话框中宣布了有意义的控件标签。 每个按钮都传达其操作，而不使用不必要的注释前缀。 (SITES-25277)
* 现在，Assets侧边栏“编辑”按钮可提供更大的触控目标。 用户无需选择附近的元素，即可更可靠地激活控件。 (SITES-25221)
* 页面编辑器现在使用逻辑标题层次结构。 屏幕阅读器将页面标题标识为主要标题，将侧边栏标题标识为从属标题。 (SITES-25222)
* “注释”对话框现在会将其标题显示为语义标题。 屏幕阅读器用户可以识别标题，并通过标题命令导航对话框结构。 (SITES-25248)
* 现在，屏幕阅读器用户在过滤插入新组件列表时收到反馈。 搜索字段描述其过滤行为，状态消息报告结果计数。 (SITES-25251)
* 现在，侧边栏组件面板使用语义列表标记。 屏幕阅读器可以朗读项目数，并支持高效的列表导航。 (SITES-25214)
* “信息”按钮现在使用“组件”面板中的大图标。 用户可以更轻松地查找和识别每个控件。 (SITES-25217)
* 现在，当用户增加文本间距时，组件标题将保持可见。 长标题会换行，而不是截断或重叠附近的内容。 (SITES-25219)
* Assets侧边栏&#x200B;**编辑**&#x200B;按钮现在指示它打开一个新的浏览器选项卡。 可视提示和屏幕阅读器提示可在导航之前准备用户。 (SITES-25220)
* 现在，当工具栏打开时，“注释模式”将键盘焦点置于注释工具栏上。 键盘和屏幕阅读器用户可以按逻辑顺序移动控件，而无需从&#x200B;**关闭**&#x200B;按钮向后导航。 (SITES-24996)
* 为路径和标记字段选择按钮时，不再使用复选框图标。 更新后的图标显示控件将打开一个选择对话框，而不是更改选中的状态。 (SITES-25210)
* 现在，侧边栏组件面板中的过滤器字段已具有有效的可访问标签。 屏幕阅读器会朗读字段的用途，而不是依赖图标或占位符文本。 (SITES-25212)
* Assets侧边栏现在隐藏屏幕阅读器中的装饰性缩略图。 用户在资源网格中导航时，不会再听到两次资源名称。 (SITES-25213)
* 筛选器边栏中的折叠按钮现在显示具有足够对比度的焦点指示器。 键盘用户在导航筛选器类别时可以跟踪焦点。 (SITES-24986)
* Filters边栏现在显示单选按钮周围的清晰键盘焦点。 增加的对比度可帮助用户在过滤器选项中跟踪其位置。 (SITES-24987)
* 现在，在“过滤器”页面上加载状态消息符合最低文本对比度要求。 在卡片视图和列表视图之间切换时，用户可以阅读进度反馈。 (SITES-24991)
* 编辑器画布中的页面标题现在使用语义标题标记。 辅助型技术可以宣布标题并将其包含在标题导航中。 (SITES-24993)
* 现在，展开模拟器菜单可将键盘焦点移动到第一个菜单项。 折叠菜单可保持逻辑二级工具栏序列中的焦点。 (SITES-24954)
* “实时视图”表中的文本现在满足最低对比度要求。 在正常和悬停状态下，用户可以清楚地阅读Live Copy详细信息。 (SITES-24956)
* 引用边栏现在为其标题使用语义标题标记。 屏幕阅读器在初始加载期间和用户浏览文件夹时朗读标题。 (SITES-24967)
* 现在，卡片链接可清楚地描述其目标。 屏幕阅读器用户可以识别每个链接，而无需听到卡片的完整元数据。 (SITES-24975)
* 标题菜单按钮不再告诉屏幕阅读器它们打开了对话框。 屏幕阅读器而是会朗读每个按钮的展开或折叠状态，这可以准确描述菜单行为。 (SITES-24742)
* “删除”按钮上的文本现在可以在其红色背景中提供足够的对比度。 在确认删除之前，用户可以更轻松地识别操作。 (SITES-24772)
* 画布卡不再显示指向同一目标的单独图像和标题链接。 单个链接可减少重复的键盘停止和重复的屏幕阅读器公告。 (SITES-24947)
* 列表视图现在显示具有更突出视觉效果的拖放按钮。 更新了图标大小、重量和对比度，使控件更易于查找和使用。 (SITES-24951)
* 标题按钮现在提供简洁的辅助访问名称：搜索、应用程序、帮助、收件箱和用户。 屏幕阅读器不再在键盘导航期间朗读“可点击”或“图形”等冗余术语。 (SITES-24715)
* 应用程序导航中的链接现在可显示更强的视觉重点。 增加文本大小和粗细，可提高视力缺佳或色觉差异的用户的可读性。 (SITES-24723)
* 收件箱链接现在使用语义列表标记。 屏幕阅读器可以将链接识别为相关组，宣布项目计数，并支持更高效的导航。 (SITES-24730)
* “用户首选项”对话框中的工具提示控件现在会公开可访问的描述性名称。 屏幕阅读器在阅读工具提示内容之前会朗读每个控件的目的，而不是说“空白”。 (SITES-24732)
* 现在，每个过滤器边栏地标都包含一个唯一的可访问标签。 屏幕阅读器可以区分过滤器边栏和其他页面区域，并在导航期间对其进行识别。 (SITES-24686)
* 编辑器对话框现在将帮助和切换全屏按钮与标题元素分隔开。 屏幕阅读器可准确识别这些交互控件，并且不再将它们作为标题发布。 (SITES-24696)
* 现在， CSV报告按钮会在打开新的浏览器选项卡之前警告用户。 其可访问的标签可在激活之前将行为告知屏幕阅读器和键盘用户。 (SITES-24704)
* 过滤器边栏现在会为保存的搜索加载标签，并且始终选择搜索目录。 在焦点、键盘或鼠标交互过程中，“过滤器”按钮不再插入标签元素。 (SITES-24706)
* 现在，“关闭”和“删除位置”按钮提供了更大的接触目标。 用户无需选择相邻元素，即可更可靠地激活任一控件。 (SITES-24530)
* “删除位置”按钮及其焦点指示器现在满足最低对比度要求。 更强的对比度可帮助用户识别控制并跟踪键盘焦点。 (SITES-24531)
* 编辑器iframe现在包括画布、侧边栏、组件对话框和布局预览中的描述性标题。 屏幕阅读器可以在焦点进入时识别每个帧。 (SITES-24650)
* 改进的文本对比度使引用边栏消息更易于阅读。 此更改阐明请求选择或报告不可用引用的提示。 (SITES-24666)
* “组件”面板为每个信息图标提供了一个有意义的易访问标签。 屏幕阅读器可以一致地识别显示组件描述的控件。 (SITES-24500)
* 键盘焦点现在围绕着Byline的整个“显示描述”按钮。 可见的大纲可帮助用户跟踪其位置并避免激活其他控件。 (SITES-24503)
* Teaser组件对话框不再将帮助和切换全屏按钮作为标题显示。 屏幕阅读器将这两个控件朗读为按钮，并保留正确的标题结构。 (SITES-24525)
* Adobe Experience Manager标题控件可正确报告其展开或折叠状态。 该控件打开和关闭导航内容，以便屏幕阅读器接收有效的状态信息。 (SITES-24528)
* 筛选器结果将地球图标标记为装饰性并删除其可访问的名称。 屏幕阅读器会忽略这些图标，而不是宣布误导性的描述。 (SITES-3057)
* “时间扭曲”对话框现在将时间条目错误与相应的“小时”或“分钟”字段相关联。 屏幕阅读器会在验证消息旁边朗读受影响的字段。 (SITES-10980)
* 选定的内容树项目不再成为“更改文件”或“文件夹控制”标签的一部分。 屏幕阅读器可听到不含额外状态文本的清晰控件名称。 (SITES-24496)
* Assets侧边栏中的区域地标现在会显示不同的可访问名称。 屏幕阅读器用户可以毫不含糊地识别和导航每个区域。 (SITES-24497)
* 屏幕阅读器现在忽略轮播对话框的装饰性帮助和全屏图标。 键盘导航不再触发不必要的图标公告。 (SITES-2912)
* 屏幕阅读器现在跳过Teaser对话框中的装饰性工具栏图标。 帮助、全屏、格式和链接控制不再产生多余的公告。 (SITES-2934)


#### 管理员用户界面{#sites-adminui-65-lts-sp3}

* AEM现在允许管理员组成员解锁页面并模拟用户。 组成员可以通过其现有访问权限完成这两项管理任务。 (SITES-14732)
* 在作者在时间轴中选择&#x200B;**还原到此版本**&#x200B;后，Assets管理员视图现在会更新资产信息卡。 缩略图会立即显示还原的版本，并且不再显示过时的预览内容。 (SITES-46590)


#### 经典用户界面{#sites-classicui-65-lts-sp3}

印尼语语言副本属性显示正确的ID语言代码。 在作者创建或查看印度尼西亚语副本时，引用边栏不再取代IN。 (SITES-44918)


#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp3}

Assets控制台现在在用户应用搜索筛选器时进行响应。 更改内容片段模型筛选器会刷新结果，而不是保持当前资源列表不变。 (SITES-38686)主要


#### [!DNL Content Fragments] - 管理{#sites-admin-65-lts-sp3}

* Assets页面现在将锁定内容片段的工具提示本地化为本地化。 用户将鼠标悬停在锁定指示器上时，会看到翻译的&#x200B;**签出者**&#x200B;标签。 (SITES-42531)主要

* AEM在创建内容片段期间本地化提供的无效名称验证消息。 不支持的标题字符不再在非英语界面中触发英语文本。 (SITES-19796)
* AEM在内容片段创建期间翻译内容片段模型字符串。 在本地化环境中，Assets界面不再显示该标签的英语文本。 (SITES-22336)
* 内容片段服务不再依赖过时的功能切换逻辑。 简化的实施删除了依赖于切换的分支，并保持Service Pack行为一致。 (SITES-38688)
* AEM在计划的内容片段发布期间翻译后一个选项。 发布工作流与活动界面语言匹配。 (SITES-42532)
* AEM将翻译内容片段下载对话框中的主字符串。 元素部分与活动的界面语言匹配。 (SITES-42534)


#### [!DNL Content Fragments] — 片段编辑器{#sites-fragments-editor-65-lts-sp3}

* 内容片段编辑器现在正确放置富文本编辑器下拉菜单。 每个菜单都与其工具栏控件保持一致，并保持附近格式控件可见。 (SITES-44005)关键

* 编辑内容片段按钮现在出现，并立即用于引用多字段条目。 作者在编辑嵌入片段之前不再需要保存、关闭和重新打开父内容片段。 (SITES-43733)主要

* 当作者选择多行文本字段时，内容片段编辑器会显示一个焦点大纲。 大纲不再与附近控件重复或重叠。 (SITES-39253)
* 内容片段创建显示不含斜体样式的CJK占位符文本。 日语、朝鲜语、简体中文和繁体中文字符保持其预期外观。 (SITES-43548)
* 内容片段编辑器在作者保存或发布片段后刷新状态横幅。 作者可以确认“已修改”、“已保存”或“已发布”状态，而无需重新加载浏览器选项卡。 (SITES-45897)
* 在Granite UI发生更改后，内容片段编辑器会一致地验证字段。 更新的客户端库将恢复预期的验证行为。 (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp3}

* 当DAM文件名包含空格或非ASCII字符时，GraphQL JSON响应现在包括嵌入的图像引用。 客户端应用程序可以检索和渲染这些图像，而无需重命名资产。 (SITES-42191)主要
* 内容片段GraphQL API现在包括若干查询处理和响应处理更新。 这些更改防止出现重复的缓存标头和值，改进编码，保留持久查询状态信息，处理空标头，并返回相应的端点错误。 (SITES-40159)主要
* PersistedQueryServlet现在在有效的GraphQL Persisted查询中处理编码变量，而不记录虚假错误或警告。 查询会继续返回成功的响应，而日志会反映其实际执行状态。 (SITES-39354)主要

* 重新加载“GraphQL端点”页面会保留本地化的空状态消息。 不存在端点时，页面不再恢复为英语。 (SITES-43586)


<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp3}-->


#### [!DNL Content Fragments] - 模型编辑器{#sites-model-editor-65-lts-sp3}

* 内容片段模型控制台现在为名称包含本地化字符的配置显示上传的缩略图。 当配置名称使用非英语文本时，作者不再丢失缩略图预览。 (SITES-39242)主要

* 当作者向画布中添加组件时，内容片段模型编辑器即显示本地化的&#x200B;**字段标签**&#x200B;文本。 作者不再需要保存和重新打开模型即可查看翻译。 (SITES-45383)
* 内容片段模型编辑器对作者为复合组件选择无效模型类型时显示的验证消息进行本地化。 消息现在与活动区域设置匹配，而不是仅以英语显示。 (SITES-41117)
* 内容片段模型编辑器将模型锁定对话框中的所有文本本地化。 该对话框不再将英文按钮标签和说明与翻译的界面文本混合在一起。 (SITES-28592)



#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp3}

Headless内容片段REST API捆绑包删除过时的功能切换和相关条件代码。 支持的API行为保持不变，而捆绑包仅保留活动功能所需的切换。 (SITES-39113)



#### 组件控制台{#sites-component-console-65-lts-sp3}

内容查找器现在会列出名称中包含不可编码字符的资产，而不会失败或生成异常。 “组件实时使用情况”页面还连续加载大型结果集，而不会在滚动期间显示空行。 (SITES-44672)主要

<!--
#### Content API{#sites-content-api-65-lts-sp3}

#### Core backend{#sites-core-backend-65-lts-sp3}
-->

#### 核心组件{#sites-core-components-65-lts-sp3}

* 多字段组件现在为每个条目存储单独的远程资产选择。 作者可以选择、更改和保存远程图像，而无需跨每个多字段项目复制一个图像。 (SITES-42376)主要
* ThumbnailServlet现在在重定向对缺少资源的请求后停止处理。 此更改可防止在DAM和控制台浏览期间出现重复的空指针异常和过度错误记录。 (SITES-41238)主要


#### 营销活动集成{#sites-campaign-integration-65-lts-sp3}

现在，Campaign ContentServlet在内容请求期间保留JSON响应内容类型。 此更改会停止在从AEM 6.5.24升级后出现的重复`WARN`和`ERROR`日志条目。 (SITES-46902)主要


#### 体验片段{#sites-experiencefragments-65-lts-sp3}

作者现在可以在创建体验片段变体时浏览40多个模板。 每个附加页面都会保留原始文件夹过滤器，并显示下一个匹配的模板。 (SITES-41531)主要


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp3} -->


#### 发布项{#sites-launches-65-lts-sp3}

启动项促销活动历史记录现在会在站点时间轴中显示本地化文本。 时间线在支持的区域设置中翻译消息“已创建的版本”和“提升启动项之前”。 (SITES-13389)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp3} -->



#### MSM - 实时副本{#sites-msm-live-copies-65-lts-sp3}

* 在作者保存未更改的属性时，内容片段Live Copy文件夹现在保留cq:rolloutConfigs。 作者以后可以更新转出设置，而不会丢失现有配置。 (SITES-43729)关键

* 作者现在可以从Blueprint页面上的可编辑工具栏中转出组件更改。 转出完成时没有JavaScript错误，并且会将更改传播到Live Copy。 (SITES-46052)主要
* 现在，作者可以在升级后从Blueprint页面完成MSM转出。 转出对话框将加载可用的活动副本，并启用其转出控件而不是保持永久加载状态。 (SITES-43116)主要

* Live Copy概述现在可以在整个关系状态中应用本地化的日期格式。 **Live Copy Source上次修改时间**、**Live Copy上次修改时间**&#x200B;和&#x200B;**上次转出时间**&#x200B;字段与用户的区域设置匹配。 (SITES-40756)
* 现在，在一个请求中停用Blueprint父页面及其子页面会为每个路径生成一个转出事件。 转出管理器不再为同一子页面运行重复操作。 (SITES-44987)


#### 页面编辑器{#sites-pageeditor-65-lts-sp3}

* 现在，作者可以在保存页面属性期间创建并应用带有大写字母或空格的标记。 AEM会立即存储规范化的标记值并保留页面分配。 (SITES-42550)关键

* 滚动样式菜单不再从选定样式中删除高亮显示。 作者可以在查看其他可用选项时确认其当前选择。 (SITES-30874)主要

* 现在，当作者通过HTTP访问AEM时，会打开富文本编辑器链接按钮。 链接创建不再触发`crypto.randomUUID`错误。 (SITES-39467)
* 作者现在可以将配置的内容片段组件复制并粘贴到空布局容器中。 粘贴的组件保留其原始内容片段引用，不再显示&#x200B;*选择体验变量*&#x200B;错误。 (SITES-41586)
* 图像编辑器现在在混合内联编辑期间遵循自定义裁切比率。 每个图像放置目标都使用自己的配置，因此裁切选择以正确的方式在全屏模式之外应用。 (SITES-45771)

<!--
#### Replication{#sites-replication-65-lts-sp3}

#### Rich Text Editor{#sites-rte-65-lts-sp3}

#### Template Editor{#sites-template-editor-65-lts-sp3}

#### Universal editor {#sites-universal-editor-65-lts-sp3}

### [!DNL Assets]{#assets-65-lts-sp3}

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp3}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp3}
-->



<!--
### [!DNL Forms]{#forms-65-lts-sp3}
-->



### 基础 {#foundation-65-lts-sp3}

#### AEM Context Service {#foundation-aem-context-service-65-lts-sp3}

AEM 6.5 LTS引入了AEM Context Service支持。 此推出添加了服务API、代理集成、AMS配置、Experience Cloud集成、生产监控、操作Runbook和使用情况报告。 (GRANITE-65148)

#### Apache Felix {#foundation-apachefelix-65-lts-sp3}

现在，当发生间歇性配置错误时，AEM邮件服务会继续发送电子邮件。 管理员不再需要重新启动Day Communique 5 Mailer捆绑包来恢复电子邮件投放。 (GRANITE-66817)主要

<!--
#### Campaign{#foundation-campaign-65-lts-sp3}

#### Cloud Services{#foundation-cloudservices-65-lts-sp3}

#### Communities {#foundation-communities-65-lts-sp3}

#### Content distribution{#foundation-content-distribution-65-lts-sp3}

#### CRX {#foundation-crx-65-lts-sp3}

#### Granite{#foundation-granite-65-lts-sp3}

#### HTL{#foundation-htl-5-lts-sp3}

#### Integrations{#foundation-integrations-65-lts-sp3}

#### Jetty{#foundation-jetty-65-lts-sp3}
-->

#### 本地化{#foundation-localization-65-lts-sp3}

* “操作”控制台现在可以在运行状况报表中对以前未翻译的文本进行本地化。 用户可看到已翻译的状态消息、警告、维护结果和性能信息。 (NPR-44280)主要

* 审核日志维护任务现在显示本地化的免责声明。 管理员在配置自动审核日志清除之前，可以使用他们选择的语言查看合规性和法律指南。 (NPR-44188)
* 现在，当用户重新排序修改后的配置文件时，“编辑用户”页面会显示一个本地化的错误。 该消息清楚地说明，在用户保存其更改之前，已更改的用户档案无法移动。 (NPR-44282)
* AEM现在会在整个内容片段列表属性中将工具提示本地化。 翻译后的指南介绍了模型选择、标记过滤、内容路径、项目限制和排序设置。 (SITES-14969)
* 模板编辑器中的组件帮助链接现在会打开本地化的文档。 作者获得的指南与其选择的语言（而非仅包含英语的组件页面）匹配。 (SITES-15058)
* 组件策略编辑器现在对报告不可修改资源或节点创建失败的错误的本地化过程进行了说明。 模板作者会以他们选择的语言接收这些消息。 (SITES-17475)

<!-- #### Omnisearch{#foundation-omnisearch-65-lts-sp3} -->

#### 操作仪表板{#foundation-operations-dashboard-65-lts-sp3}

在客户升级AEM LTS后，`/system/health/systemalive.json`端点现在仍然可用。 更正的servlet上下文配置会阻止HTTP 404响应，并支持依赖端点的运行状况监控系统。 (GRANITE-69457)关键

#### 平台{#foundation-platform-65-lts-sp3}

默认HTL表达式选项允许列表现在可识别`decorationTagName`和`cssClassName`。 呈现标准响应式网格时，`error.log`不再充满重复的未知选项警告。 (GRANITE-67152)

<!--
#### Projects{#foundation-projects-65-lts-sp3}

#### Oak {#foundation-oak-65-lts-sp3}

#### Quickstart{#foundation-quickstart-65-lts-sp3} 
-->


#### 安全性{#foundation-security-65-lts-sp3}

**复制组**&#x200B;操作现在会打开预期的表单，而不是显示空白页面。 管理员可以输入新的组ID和说明，然后复制现有的安全组。 (NPR-44302)主要


<!-- #### Sling{#foundation-sling-65-lts-sp3} -->


#### 翻译{#foundation-translation-65-lts-sp3}

现在，翻译项目会随着工作流进度保持准确的状态计数。 启动项创建和状态传播遵循预期的工作流行为，从而消除不一致的项目元数据。 (NPR-43420)


#### 用户界面{#foundation-ui-65-lts-sp3}

* “国家/地区”标签现在以选定的界面语言显示。 本地化的界面不再显示英文标签。 (NPR-43883)
* 选择同级页面现在会激活复合多字段路径选取器中的&#x200B;**Select**。 作者无需放大浏览器窗口或重复选择即可确认新路径。 (GRANITE-69323)


<!-- #### WCM{#foundation-wcm-65-lts-sp3} -->


#### 工作流{#foundation-workflow-65-lts-sp3}

* 工作流包页面现在支持触屏UI页面编辑器中的内容树和可编辑的资源定义组件。 作者无需使用经典UI，即可导航包内容并检查或更新其组件。 (GRANITE-67348)主要
* 触屏UI页面编辑器现在呈现工作流包页面的内容树。 作者可以通过同一编辑器检查包结构并编辑资源定义组件。 (GRANITE-67186)主要

* 工作流变量对话框现在显示表单数据模型、JSON、XML和文档变量的正确控件。 作者在创建这些非原始变量时，不再看到原始HTML标记。 (GRANITE-67915)



## 关于 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 的平台的构建基础是更新版本的基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java™ 内容存储库：Apache Jackrabbit Oak 1.68.x。

Eclipse Jetty 11.0.x 被用作快速入门的 servlet 引擎。

### Java™ 支持  {#java-support}

* 支持 Java™ 17 和 Java™ 21。
* 为了获得最佳性能，请用其他值覆盖默认 GC 值。 有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* 如果 Oracle 未公开提供，Adobe 会分配 Java™ 17 和 Java™ 21 维护更新，以便客户在 AEM 相关项目中使用。

### Uberjar 包装 {#uber-jar-packaging}

适用于AEM 6.5 LTS SP3的UberJar使用AEM 6.5 LTS UberJar版本6.6.3。 您可以从 Maven 中央存储库检索相应的 UberJar 工件。 与 AEM 6.5 不同，AEM 6.5 LTS 将公共 API 和已弃用的 API 分开成两个不同的工件。

要使用公共 API 进行编译，请使用以下方法：

    ```xml
    &lt;依赖项>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;分类器>api&lt;/classifier>
    &lt;scope>已提供&lt;/scope>
    &lt;/dependency>
    `&#39;

如果您的代码还依赖于已弃用的 API，请添加以下内容：

    ``xml
    &lt;依赖项>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;classifier>deprecated-api&lt;/classifier>
    &lt;scope>已提供&lt;/scope>
    &lt;/dependency>
    `&#39;

另请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升级 {#upgrade}

* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 有关详细的升级说明，请参阅 [JEE 上的 AEM Forms 6.5 LTS SP1 升级指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## AEM 6.5 LTS 服务包升级最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

适用于：安装Service Pack 3 (SP3)的AEM 6.5 LTS（内部部署）客户。 SP3作为快速入门JAR提供。

**为什么这个升级做法很重要**
用于 AEM 6.5 LTS 的 SP2 以 Quickstart JAR 形式提供，而不是需要通过包管理器安装的 ZIP 文件。 内部部署客户通过替换Quickstart JAR、将其解压缩并重新启动来进行升级。 此方法与Adobe的标准升级过程保持一致。


**推荐的升级流程（创作或发布实例）**

1. 验证您的 AEM 6.5 LTS 实例运行正常且可访问。
1. 从软件分发下载 Quickstart JAR（例如 `cq-quickstart-6.6.x.jar`）。
1. 停止正在运行的实例。
1. 在AEM安装目录（`crx-quickstart/`外部）中，将以前的快速入门JAR替换为SP3 JAR。
1. 解压该 JAR 文件：

       ``java
     java -jar cq-quickstart-6.6.x.jar -unpack
     ``
   
   （根据需要调整堆标志。）

1. 将解压后的 JAR 重命名以匹配对应角色和端口，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 启动 AEM，并在用户界面（“帮助”>“关于”）及日志中确认升级是否成功。

**最佳实践**

* 在生产之前，先在较低环境/测试环境中运行升级。
* 开始之前，请先进行完整的、可恢复的备份（存储库和任何外部数据存储库）。
* 查看 Adobe 的就地升级指南及技术要求（LTS 建议使用 Java 17 或 21）。

>[!NOTE]
>
>上述文件名（例如 `cq-quickstart-6.6.x.jar`）反映了此 LTS 版本中 Quickstart 工件的命名方式；请务必使用从软件分发实际下载的文件名称。

## 安装和更新{#install-update}

有关设置要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 如果您直接从旧版 6.5 SP 升级到 LTS SP1，请按照从 6.5 [升级](/help/sites-deploying/upgrade.md)到 6.5 LTS GA 的说明进行操作。


有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)，该文档适用于LTS Service Pack更新。

>[!NOTE]
>
> 新安装 AEM 6.5 LTS 时，必须单独安装索引定义。 更多详细信息请参阅[这篇文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 安装并更新 AEM Forms 附加组件 {#install-update-aem-forms-add-on}

有关详细说明，请参阅[执行就地升级](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。


## 支持的平台 {#supported-platforms}

查找受支持平台的完整表格，包括对 [AEM 6.5 LTS 技术要求](/help/sites-deploying/technical-requirements.md)的支持等级。

>[!NOTE]
>
>建议与 AEM 6.5 LTS 一起使用 Java™ 17/Java™ 21 版本。


## 已弃用和已删除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe 不断审阅并改进产品功能，更新或取代旧版功能，提供更高的客户价值。 这些更改在实施时，仔细考虑了向后兼容性。

为了确保透明度，并允许进行充分的规划，Adobe 为 Adobe Experience Manager (AEM) 遵循了这种弃用流程：

* 首先宣布弃用。 已弃用的功能仍然可用，但不再得到增强。
* 不会在下一个主要版本发布之前移除。 单独通知计划好的移除时间线。
* 在功能移除之前，至少会提供一个发布周期，以便客户过渡到受支持的替代方案。

### 已弃用的功能 {#deprecated-features}

本节列出了 Adobe 在 AEM 6.5 LTS 中已弃用的功能。 通常情况下，Adobe 在未来版本中移除某些功能之前，会先弃用这些功能并提供替代方案。

建议客户检查其当前部署中是否使用了此类特性/功能。 制定计划以更改实施，从而使用提供的替代方案。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
| 快速入门 | Mongo API | Mongo API 现已弃用，已计划在未来的发行版本中移除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API 中的内容片段支持 | AEM 6.5 LTS SP2 为内容片段和模型管理提供了现代化的 OpenAPI，因此 AEM Assets REST API 中的旧版内容片段支持端点已弃用。<br>Adobe 打算在生命寿命结束公告之前保持这些旧版端点可用。 Adobe 不计划为已弃用的端点提供进一步的增强功能。 | 6.5 LTS SP2 |
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 在 AEM 中管理无头内容的首选编辑器有：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于进行可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于进行基于表单的编辑。 | 6.5 LTS GA |
| [!DNL Foundation] | 支持 com.adobe.granite.oauth.server | Adobe IMS 集成 | |

### 已移除的功能 {#removed-features}

此部分列出了 AEM 6.5 LTS 中已移除的功能。 之前的版本中已将这些功能标记为已弃用。

* 删除了对Adobe CRX存储库持久性的RDBMK支持。
* 在群集环境中，MongoMK 现在是存储库持久性的唯一受支持的选项。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
| Sites | 内容片段文本摘要 | 没有替代功能可用。 | 6.5 LTS SP3 |
| Commerce | 不支持 AEM CIF Classic。 | 迁移到 [AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解决方案 | 不支持社交/社区。 | 没有替代功能可用。 | 6.5 LTS GA |
| Screens | 不支持 Screens。 | 没有替代功能可用。 | 6.5 LTS GA |
| 资产 | 不支持 `dam-pim` 和 `dam-rating`，因为捆绑包取决于社交。 | 没有替代功能可用。 | 6.5 LTS GA |
| 资产 | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` 已被移除。 | 使用已添加的替代 api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS GA |
| 门户 | 不支持 AEM Portal Director。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 捆绑包 `com.adobe.granite.socketio` 已被移除。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 不支持 `com.adobe.granite.crx-explorer`。 | 没有替代功能可用。 | 6.5 LTS GA |
| Granite | 不支持 `crx2oak`。 | 选择相关版本的 [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | 不支持 `com.adobe.cq.cq-searchpromote-integration`。 | 没有替代功能可用。 | 6.5 LTS GA |
| Guava | 现在，AEM 中的所有 guava 依赖项都已移除，因此 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 捆绑包不再是 AEM 的一部分。 | 如果客户依赖 guava，可以自行添加 guava，或者在可能的情况下用 Java 收藏集或其他替代功能取代 guava 代码。 | 6.5 LTS GA |
| `We.Retail` | 不支持 `We-retail` 示例网站。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 不支持 `oak-solr-osgi` 捆绑包。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 不支持 `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom` 和 `org.apache.sling.atom.taglib`。 | 没有替代功能可用。 | 6.5 LTS GA |
| 开源 | 现在，`org.apache.commons.io` 包从 `org.apache.commons.commons-io` 导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | `javax.mail` 包正在从 `com.sun.javax.mail` 捆绑包中导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | `org.apache.jackrabbit.api` 包现在已从 `org.apache.jackrabbit.oak-jackrabbit-api` 捆绑包中导出。 | 无需更改。 | 6.5 LTS GA |
| 开源 | 不支持 `com.github.jknack.handlebars` | 选择相关[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS GA |

## 已知问题 {#known-issues}

### AEM Forms

* 在配置管理器中，如果未选择模块或者只选择了有限的组件，在 AEM Forms 6.5 LTS JEE Turnkey 自定义模式下引导启动时数据库初始化失败。 失败原因是缺少依赖项 (xalan-2.7.2.jar) 而导致出现错误。 将JAR文件添加到Adobe-livecycle-jboss.ear\lib解决了此问题。 (FORMS-24690)
* 在WebSphere® Liberty Profile上运行的Forms JEE LTS Service Pack 2部署中，电子邮件功能会失败。 尝试使用电子邮件功能时，服务器记录错误： `Could not convert socket to TLS`。 (FORMS-24692)
* 在JBoss®上运行的Forms JEE LTS上，与电子邮件相关的功能会失败。 尝试使用电子邮件功能时，服务器记录错误： `Error IMAPProvider not a subtype`。 要解决此问题，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear)安装修补程序。 (FORMS-24892)

### 离线压缩后，执行在线压缩时存储库损坏 (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

如果离线压缩以前是在 JCR 存储库上运行，在线压缩时用户可能会遇到存储库损坏的情况。 在这种场景中可能会发生 `SegmentNotFoundException` (SNFE)，可能导致存储库损坏。

要解决此问题，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip)安装热修复程序。 由于热修复程序包含一个低级 `oak-segment-tar` 捆绑包，因此实例会在安装后重新启动。

应用程序时，计划好实例的停机时间。 对于离线压缩，请使用相应的 [`oak-run` jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)，也在软件分发中提供。

>[!NOTE]
>
> * 对于任何 `oak-run` 操作，请使用 [`oak-run` 1.88.1-B006 jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)。
>
> * 通过设置系统属性 `oak.compaction.legacy=true` 启动 AEM。

### AEM 6.5 LTS SP2中缺少`com.adobe.granite.apicontroller`包(GRANITE-67640) {#missing-apicontroller-bundle-granite-67640}

AEM 6.5 LTS SP2中缺少`com.adobe.granite.apicontroller`包。 此捆绑包控制如何解析OSGi捆绑包，并可阻止捆绑包解析为其他捆绑包，这对于限制公开的API很有用。

若要使用此功能，请从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip)安装修补程序。

>[!NOTE]
>
> 要确保`com.adobe.granite.apicontroller`的默认配置不会引入影响现有自定义实施的意外解决限制，请在安装修补程序后验证所有已安装捆绑包的捆绑状态。

### Sling-Initial-Content (SP2) 不再支持 JSON 注释 {#json-comments-no-longer-supported-in-sling-initial-content}

这个问题影响了开发人员和管理员部署那些使用 `Sling-Initial-Content` 和 JSON 文件的 OSGi 捆绑包。

从 AEM 6.5 LTS SP2 开始，`Sling-Initial-Content` 捆绑包中使用的 JSON 文件不再接受注释（`//` 或 `/* */`）。 早期的 AEM 版本接受了注释，因为 `javax.json` 提供程序对此比较宽容。 AEM 6.5 LTS SP2 将 `org.apache.sling.jcr.contentloader` 升级为版本 2.6.0，后者将 JSON 解析器换为 `jakarta.json`。 虽然 [JSON 规范 (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) 未定义注释的语法，但由于 `javax.json` 提供程序的宽容性，较早的 AEM 版本接受注释。 `jakarta.json` 提供程序不提供此扩展。

沉默的错误：捆绑包激活时内容节点加载失败，没有为安装程序提供任何错误消息。 如果在升级到 SP2 后意外缺少内容，请检查 OSGi 安装程序日志中是否记录了 JSON 解析错误。 要识别受影响的捆绑包，请在 `Sling-Initial-Content` 清单头下面列出的 JSON 文件中搜索 `//` 或 `/* */`。

>[!CAUTION]
>
> 为避免在升级到AEM 6.5 LTS SP2后内容加载失败，请从`Sling-Initial-Content`捆绑包中的JSON文件中删除所有注释。

### Jackson捆绑包升级会影响GlobalLink连接器 {#jackson-upgrade-globallink-connector}

AEM 6.5 LTS SP3升级`jackson`捆绑包。 此更改会影响使用GlobalLink翻译连接器的部署。

如果您在低于3.4.0的版本中使用`gs4tr-globallink-adaptors-aem.core`捆绑包，请将该捆绑包升级到兼容版本。 版本3.4.0或更高版本适用于SP3中已升级的`jackson`捆绑包。

>[!NOTE]
>
> 在SP3更新之前或过程中，将`gs4tr-globallink-adaptors-aem.core`捆绑包升级到3.4.0或更高版本，以避免与GlobalLink连接器出现兼容性问题。


### 为 Sites Headless API 安装必需的 Oak 索引{#site-headless-api}

一些迁移到 Sites Headless 的 API 需要额外的 Oak 索引，才能提供完整功能。

若要使用以下功能，请安装`cq-dam-cfm-indices`包：

* 列出内容片段模型
* 列出内容片段
* 搜索 API
* 工作流

从 Adobe 软件分发门户下载索引包 [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fcq-dam-cfm-indices-1.1.5.zip)。

### 在使用仅 SSL 功能的情况下，Dispatcher 连接失败（已在 AEM 6.5 LTS SP1 及更高版本中修复）{#ssl-only-feature}

>[!NOTE]
>
> 此问题仅出现在 AEM 6.5 LTS GA 版本中。

在 AEM 部署中启用仅 SSL 功能后，会发生一个影响 Dispatcher 与 AEM 实例之间连接的已知问题。 启用此功能后，运行状况检查将失败，Dispatcher实例与AEM实例之间的通信将中断。 尤其是当客户尝试通过 `https + IP` 将 Dispatcher 与 AEM 实例连接时，会出现此问题。 它与 SNI（服务器名称指示）验证问题有关。

**影响**

* 健康检查失败，出现 HTTP 400 响应码。
* Dispatcher 与 AEM 实例之间的通信中断。
* 无法通过 Dispatcher 正确提供内容。
* 使用 HTTPS 与 Dispatcher 配置中的 IP 地址时连接失败。
* 通过 HTTPS + IP 连接时出现 HTTP 400“SNI 无效”的错误。

**受影响的环境**

* 具有 Dispatcher 配置的 AEM 部署。
* 启用了仅 SSL 功能的系统。
* 使用 `https + IP` 方法与 AEM 实例连接的 Dispatcher 配置。

**解决方案**

如果您遇到此问题，请联系Adobe客户支持。 有一个热修复 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 可以解决这个问题。 采用必要的热修复之前，不要尝试启用仅 SSL 功能。

## 包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下zip文件包含文本文档，其中列出了此Experience Manager 6.5 LTS Service Pack版本中包含的OSGi包和内容包：

* [OSGi包](/help/release-notes/assets/65lts_sp3_bundles.zip)
* [内容包](/help/release-notes/assets/65lts_sp3_packages.zip)

## 受限网站{#restricted-sites}

这些网站仅向客户开放。 如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

