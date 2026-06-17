---
title: Adobe Experience Manager 6.5 LTS SP2 的最新发行说明
description: 查找 Adobe Experience Manager 6.5 LTS 服务包 2 的当前版本信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 6795f085b5a4d1ac2836b6c6f2f4d09a5739e639
workflow-type: tm+mt
source-wordcount: '7708'
ht-degree: 97%

---


# Adobe Experience Manager 6.5 LTS SP2 的最新发行说明 {#release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | 服务包 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2026 年 2 月 19 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **强制热修复**：如要避免在安装 SP2 时发生离线压缩的 SNFE (SegmentNotFoundException) 问题，请安装[已知问题 – 在线压缩过程中存储库损坏](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146)中描述的热修复程序。

## [!DNL Adobe Experience Manager] 6.5 LTS SP2 中包含的内容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS SP2 包含新功能、客户要求的重要增强功能以及错误修复。 还包括自 2025 年 3 月 6.5 LTS 首次发布以来推出的在性能、稳定性和安全性方面的改进。 在 6.5 LTS 上[安装此服务包](#install-update)。

## 主要功能和增强功能

**AEM Sites**

AEM 6.5 LTS SP2 现在包含 OpenAPI，可用于[内容片段和模型管理](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/)和[发布](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/)。 使用这些 API 可访问内容片段和发布，以进行创作和计划。 它们使用与 AEM as a Cloud Service 相同的现代 OpenAPI。

**AEM 表单**

**AEM Forms 6.5 LTS SP2 中包含的内容**

* 添加了在 JBoss® EAP 8.0 中对 RDBMK 的支持。

* 添加了对WebSphere® Liberty Profile (WLP)的支持。 只有Oracle数据库和IBM® Sumeru JDK 21支持WLP。

* 增强了可视规则编辑器中的用户体验。 此次更新包括：

   * 保存后自动重新加载摘要视图，以显示更新后的规则状态

   * 显示“添加”/“删除”按钮并允许进行切换，不再隐藏这两个按钮

   * 保存规则的操作失败后，提供明确的反馈 (FORMS-21261)

* 添加了运行时应用程序编程接口 (API)，以切换 AEM Forms 中的旧版可扩展标记语言 (XML) 导出模式，由此取代 `Dcom.adobe.fd.forms.export.legacy` 参数。 此增强功能使用户能够更有效地切换导出模式，从而提高工作流的灵活性。 (FORMS-23115)

* 添加了自适应表单中对带有命名空间标记的 JavaScript 对象表示法 (JSON) 的支持。 此增强功能使用户能够更有效地使用 JSON 数据结构，从而提高数据集成和处理能力。 (FORMS-22519)

* 在规则编辑器中添加了一个“下载记录文档（DoR）/表单提交”的开箱即用 (OOTB) 按钮。 通过此增强功能，客户无需编写自定义代码即可使用 downloadDoR 函数，从而提高此函数的可用性和效率。 (FORMS-21263)

* 添加了自适应表单中对带有命名空间标记的 JavaScript 对象表示法 (JSON) 的支持。 此增强功能使用户能够更准确、更高效地预填表单，从而增强数据集成，减少手动输入错误。 (FORMS-10883)

<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS 服务包 2 中修复的问题 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### 辅助功能 {#sites-accessibility-65-lts-sp2}

* 当作者在编辑过程中将鼠标悬停在组件浏览器中的项目上时，“文本”组件会失去键盘焦点。 这会中断输入，并触发 WCAG 3.2.1 的一个无障碍性错误。 此修复防止了悬停样式移动焦点，在组件浏览器交互时保持“文本”组件获得焦点。 (SITES-35370)
* 修正了“描述”富文本字段中的焦点管理，该字段阻止了通过 Tab 键前进导航。 用户在 RTE 中卡住，因为组件依赖非标准键盘命令来移动焦点，这破坏了预期的对话框导航。 此更改强制使用标准键盘进行交互操作，维护了整个对话框中符合逻辑的 Tab 排序。 （SITES-35228）
* 修复了在 Sites 编辑器中创作页面时导致预期行为中断以及组件交互不一致的问题。 作者遇到不可靠的 UI 响应，这干扰了标准编辑任务，降低了工作流效率。 此更新改进了底层编辑器逻辑，恢复了受影响组件之间稳定、可预测的交互行为。 （SITES-35227）
* 一个回归破坏了页面编辑器中的资产选择器，阻止了在特定的页面编辑场景中加载选择器。 现在，作者在编辑页面过程中选择或浏览资产时，可以正常打开并使用资产选择器。 此更改恢复了对因加载失败而中断的资产选择工作流的稳定访问。 （SITES-35226）
* 消除了在 Sites 编辑器中导致页面交互行为不一致以及标准创作工作流中断的问题。 此错误导致了意外的 UI 响应，干扰了组件配置和内容更新。 此更新稳定了受影响的功能，恢复了在所有页面上可靠执行各种编辑操作。 （SITES-35225）
* 解决了 Sites 创作界面中导致页面编辑过程中出现不一致行为并中断正常工作流的问题。 作者遇到了意外的 UI 响应，干扰了组件交互和内容更新。 此更新稳定了受影响的功能，恢复了在所有编辑场景中可靠、可预测的行为。 （SITES-35224）
* AEM Sites 现在包括对图像的 `alt` 文本支持，以满足 ADA 和 WCAG 的要求。 页面输出不再忽略 `alt` 属性，确保屏幕阅读器获得正确的替换文本。 （SITES-27153）
* 修复了 `Note Add` 工具栏布局，使“添加”按钮在 320px 视口宽度情况下不再与标题重叠。 改进了小屏幕重排，使控件在 400% 缩放时保持可读性和可用性。 （SITES-25376）
* 修复了链接选择对话框错误导致的屏幕阅读器缺少公告的问题。 现在，UI 通过一个状态消息容器发布错误文本，因此 NVDA 会在消息出现时立即读取消息。 （SITES-25368）
* 移除了侧边栏资产列表中的 ARIA 网格和单元格角色。 恢复了标准的列表语义和键盘焦点顺序，从而改进了屏幕阅读器的导航，减少了额外的 Tab 停止位。 (SITES-25361)
* 修正了侧边栏资产中的焦点排序。 键盘用户现在可通过一致的 Tab 路径执行包括编辑在内的每一个资产操作。 （SITES-25360）
* 修复了在 320px 视口宽度情况下搜索资产模态中的布局溢出问题。 模态内容现在会重排并保持可读，使控件不再重叠或溢出对话框。 （SITES-25330）
* 修正了“编辑”按钮的 NVDA 输出。 NVDA 现在会公告“编辑”操作，而不是“已按下预览按钮”。 （SITES-25320）
* 修复了未命名的“人口统计”工具栏文本输入框导致屏幕阅读器输出无声或通用输出的问题。 现在，每个输入框都有一个清晰的基于标签的可访问名称，改进了键盘和辅助技术的导航。 （SITES-25316）
* 修正了布局预览导航时“人口统计”工具栏的键盘焦点顺序。 Tab 导航现在从“人口统计”按钮直接移动到工具栏控件，而不是跳到辅助工具栏。 （SITES-25305）
* 修复了编辑布局尺子上“较小屏幕”和“平板电脑”标签的公告顺序错误的问题。 屏幕阅读器现在会在正确的尺子标记处公告这些标签，与页面布局相符。 (SITES-25291)
* 修复了编辑布局工具栏在 200% 缩放时溢出的问题。 内容现在保留在视口中，可通过滚动方式访问。 （SITES-25288）
* 解决了注释叠加中焦点顺序错误的问题。 现在可以使用键盘上的 Tab 键在叠加控件和注释项之间循环切换。 父页面不再从叠加的后面获得焦点。 （SITES-25282）
* 修复了色板弹出窗口的焦点处理问题。 此对话框现在会将焦点移动到一个清晰的标题，在这个入口点开始屏幕阅读器输出。 NVDA 不再按错误顺序读取完整的对话框内容。 (SITES-25275)
* 修复了日期选取器关闭后的时间扭曲模态焦点处理问题。 `Escape` 现在会将焦点返回到日期选取器按钮。 日期选择现在会将焦点放在日期选取器控件旁边的输入字段上，从而防止焦点丢失和访问背景页面。 （SITES-25264）
* 修复了“删除注释”对话框的键盘焦点处理问题。 现在，“取消”会将焦点返回到打开此对话框的 `Delete` 控件，而不是“确认”十六进制值控件。 取消后，屏幕阅读器不再公告不相关的对话框内容。 （SITES-25258）
* 修复了注释模态对话框的焦点处理问题。 现在，打开对话框会将焦点放在对话框标题上，阻止 NVDA 读取画布内容和无关的对话框文本。 键盘导航现在保留在对话框中，直到对话框关闭。 （SITES-25257）
* 修复了 320px 宽度情况下的搜索模态布局问题。 模态内容现在可以整齐地重排，避免与树目录重叠。 用户可以查看结果，导航目录，没有被遮住的控件。 （SITES-25246）
* 文本间距增加后，搜索模态文本不再被剪切。 树目录布局现在保持清晰的分隔，使标签和条目一直清晰可读。 用户现在可以在文本不重叠且不被截断的情况下完成搜索和导航。 （SITES-25245）
* 现在，激活注释会将键盘焦点移动到注释内容，而不是退出注释的按钮。 Tab 键顺序遵循逻辑序列，不用反向导航即可到达相关控件。 （SITES-25241）
* 在键盘导航过程中，“设置日期”和“退出时间扭曲”链接缺少可见的焦点指示器。 UI 现在渲染一种独特的高对比度的焦点样式，使用户能够一眼就识别活跃的链接。 （SITES-25232）
* Teaser 模态标题不再阻止键盘用户移动对话框。 键盘控件现在允许拾取、移动和放置操作，这提高了屏幕阅读器的可用性和整体可操作性。 (SITES-25226)
* AEM 现在为 Teaser 模态信息按钮使用一个有意义的无障碍标签。 屏幕阅读器会读出一个清晰的操作名称，而不是默认图标替换文本字符串。 （SITES-25223）
* 屏幕阅读器现在会在用户按下编辑按钮时读出正确的操作。 NVDA 不再报告在键盘导航过程中导致误导性反馈和混淆的“按下了预览按钮”。 （SITES-25208）
* 现在，展开左侧边栏会将键盘焦点移动到第一个左侧边栏控件。 Tab 序列不再跳转到辅助工具栏或落到中间列表上，使键盘用户不用反向导航即可访问左侧边栏的内容。 （SITES-24998）
* 现在，设备模拟器栏的内容在 320 px 视口宽度的情况下保持完全可见。 工具栏文本和控件自动换行，不再被截断，从而减少了重叠，提高了可读性。 （SITES-24953）
* AEM 现在会在模拟器工具栏中显示完整的 iPhone 设备标签。 文本不再在默认宽度上截断，从而提高了可读性，设备选择更清晰。 （SITES-24952）
* 列表视图表头现在通过 ARIA 显示排序状态。 进行列排序操作后，屏幕阅读器会读出升序或降序。 （SITES-24943）
* 在文本间距更改过程中，AEM 现在保持卡片视图中的“更多操作”菜单标签可见。 菜单选项保持完整的文本，包括“快速发布”，在任何 WCAG 文本间距设置的过程中，菜单保持清晰可读。 （SITES-24941）
* 卡片操作菜单栏现在会在卡片视图中显示一个无障碍名称。 屏幕阅读器会清晰读出菜单栏的用途，语音控制可以通过名称来定位控件。 （SITES-24938）
* 卡片视图不再依赖会导致屏幕阅读器行为混乱的 ARIA 网格语义。 UI 现在为卡片内容和卡片操作栏提供有意义的角色和标签，这减少了键盘使用中缺少控件的情况。 (SITES-24933)
* 现在，只要用户将鼠标悬停在工具提示图标上，就会显示 `Delete Modal` 工具提示。 现在，焦点操作会显示相同的工具提示文本，这改善了鼠标和键盘用户的重复访问。 (SITES-24778)
* 用户配置边栏后，左边栏导航现在会遵循预期的键盘焦点顺序。 Tab 键焦点会落在选定的左侧边栏区域，而不是切换显示区域，这提高了屏幕阅读器的导航清晰度。 (SITES-24754)
* 修复了在“用户首选项”模态中色板导航时发生错误 NVDA 反馈的问题。 NVDA 现在会读出获得焦点的色板的标签，从而消除了误导性的颜色输出。 色板集现在支持一致的键盘导航和清晰的选择感知。 （SITES-24739）
* 减少了 `Spin` 控件的冗长 NVDA 输出。 移除了与输入标签重复的冗余组标签，因此 NVDA 只公告一次控件名称。 现在，键盘和屏幕阅读器导航功能可提供清晰的单次公告。 （SITES-24725）
* 轮播对话框现在将焦点放在对话框标题上，而不是“项”选项卡上。 “取消”和“退出”会将焦点恢复到启动此对话框的控件上，这减少了冗长的 NVDA 输出。 (SITES-24716)
* 现在，“链接选择”对话框会将程序化的标签与最后一级树项目的屏幕上标签对齐。 箭头键导航会为每一项触发可靠的屏幕阅读器公告，移除误导性的标签输出。 （SITES-24710）
* 现在，链接打开选择对话框在 320 px 视口的情况下会正确重排。 内容不再溢出模态或被截断，模态也不再显示水平滚动条。 （SITES-24709）
* 现在，链接打开选择对话框在“关闭”或“取消”后会将键盘焦点恢复到对话框的触发器。 焦点不再跳到链接输入，这可以保持屏幕阅读器上下文稳定，减少额外导航。 (SITES-24707)
* 图像模态对话框现在遵循一个符合逻辑的焦点顺序。 取消后，焦点不再跳过之前的控件，也不会落到页面地标上，退出后用户会重新获得配置按钮的焦点。 (SITES-24693)
* 引用边栏模态对话框现在会捕获键盘焦点。 Tab 键和 Shift+Tab 停留在对话框控件中，焦点不再转移到页面内容上。 屏幕阅读器仅读出对话框的内容。 (SITES-24683)
* 对话框打开时，超链接路径选择模态现在会将焦点放在对话框标题上。 “取消”会关闭对话框，并将焦点恢复到“打开选择对话框”按钮，从而防止焦点丢失和屏幕阅读器冗余输出。 (SITES-24672)
* 搜索字段现在使用一个永久性的屏幕上标签，而不是占位符文本。 标签在输入时保持可见，这为键盘、屏幕阅读器和语音用户提高了清晰度。 (SITES-24529)
* 现在，Teaser 模态对话框在打开时会将焦点设置在对话框标题上。 关闭对话框会将焦点返回到 `Configure` 控件，从而防止焦点丢失和屏幕阅读器输出过多。 (SITES-24522)
* 侧边栏资产面板现在包含一个“关闭”控件。 “关闭”将键盘焦点返回到侧边栏切换开关上，并阻止强制使用 Tab 键在面板内容之间切换。 （SITES-24489）
* 现在可以使用键盘 Tab 键到达管理表格中的按钮和链接。 用户不再依赖箭头键单元格导航来找到交互式控件。 (SITES-24285)
* 图像组件对话框不再将装饰性的帮助图标和全屏图标显示为图像。 屏幕阅读器现在会跳过这些图标，保持将焦点放在可操作控件和字段内容上。 (SITES-2940)
* 网站管理员现在可以从文件夹缩略图图标中移除图像角色。 辅助性技术会跳过这些装饰性元素，保持将焦点放在文件夹名称和操作上。 （SITES-2852）
* 内容树现在会将键盘焦点路由到活跃的树项目或第一个树项目上。 树容器不再用作空的 Tab 停止位，这防止了出现 Shift+Tab 焦点陷阱。 (SITES-1577)

#### 管理员用户界面{#sites-adminui-65-lts-sp2}

网站控制台列表视图设置未反映出列表视图中显示的列。 对话框打开后，复选框全部被清除，并且选中的列数不正确。 此修复将对话框状态与活跃的网格列同步，并更新计数器，以匹配实际的列可见性。 (SITES-38576)

#### 经典用户界面{#sites-classicui-65-lts-sp2}

升级后，经典 UI 文本组件编辑显示的是原始 HTML 标记，而不是富文本。 服务包 2 修正了经典 UI RTE（富文本编辑器）渲染，因此编辑器显示经过格式设置的内容，并保留存储的标记。 此修复还防止了在重复进行编辑和保存时标记扩展。 (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

在 6.5 LTS 中，无头事件支持缺少内容片段和模型所需的 OSGi 事件。 此更新添加了事件捆绑包以及所需的依赖项，并包含了 6.5 LTS 版本。 内容片段和模型事件现在可以正确触发，并支持发布 API 工作流。 (SITES-35329)

#### [!DNL Content Fragments] - 管理{#sites-admin-65-lts-sp2}

* 调整了 Sites 创作界面中的组件处理，以防止页面更新时发生无规律行为。 此错误导致了不可预测的编辑器响应，干扰了常规内容更改，降低了工作流效率。 此更新使编辑器逻辑符合预期的交互模式，在创作活动中提供可靠的性能。 (SITES-35078) 重要

* 一个回归破坏了内容片段的 Assets 控制台列表视图，并在列表渲染时触发了错误。 此更新修正了移除预览信息后的列表视图逻辑，恢复了稳定的列表输出。 控制台现在可正常显示内容片段，不再出现任何错误，保持列表交互可正常使用。 (SITES-38683)
* 内容片段编辑器现在会将标记标签本地化。 编辑器还会将收藏集标签本地化，因此 UI 文本符合选定的区域设置。 (SITES-977)


#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-65-lts-sp2}

* 当功能切换开关在重构后保持禁用状态时，内容片段变体标记消失。 此修复恢复了对变体标记的支持，包括切换开关保持关闭的情况下。 作者可以在内容片段编辑器中重新添加和查看变体标记。 (SITES-38682) 重要
* 作者从内容片段编辑器导航返回后，编辑的内容片段从 Assets 控制台列表中消失。 浏览器缓存返回了一个过时的列表，隐藏了更新的片段，直到进行手动刷新。 此修复为编辑器返回路径添加了缓存控件处理，使列表正确重新加载，并保持编辑后的片段可见。 (SITES-35374) 重要

* 在最近几次更改 UI 样式设置后，内容片段 RTE 显示出布局和可视化方面的问题。 服务包 2 改进了 RTE 样式设置，使工具栏和可编辑区域正确渲染，并保持清晰可读。 内容片段编辑器现在与页面编辑器的外观和行为保持一致。 (SITES-38684)
* 从 Polaris 资产选择器中移除 IMS 范围后，破坏了内容片段与传递端点的集成。 打开远程资产选择器并选择资产时，作者会遇到错误。 此更新重新添加了所需的 IMS 范围，恢复了稳定的传递层访问。 （SITES-35837）
* “关联内容”面板不再呈现硬编码的“未定义”占位符。内容片段编辑器现在通过本地化资源解析该文本，因此编辑器可以看到翻译的UI文本。(SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* 内容片段编辑器现在会在所有区域设置中都显示翻译过的“一般”选项卡标签。 编辑器会替换未本地化的选项卡文本，从选项卡标题中移除内部 ID。 (SITES-30715)
* 对于未被允许的资产类型，内容片段编辑器现在会显示翻译过的名称。 作者配置内容引用限制时，选取器列表不再混合内部字符串和只用英语的标签。 (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* 改进了 GraphQL 查询验证处理，以防止因筛选执行错误而导致部署失败。 此错误导致了应用程序启动时出现异常，使得在受影响的环境中部署不成功。 此修复确保了一致的验证行为，支持顺利部署，使运行时查询验证不再中断。 (SITES-34301) 重要

* “编辑 GraphQL 端点”对话框现在显示本地化的 UI 字符串。 此对话框不再显示只用英语的文本，例如“GraphQL schema is taken from configuration”（从配置中获取 GraphQL 架构），相关标签可在所有区域设置中正确渲染。 (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 查询编辑器{#sites-graphql-query-editor-65-lts-sp2}

* 改进了 GraphQL 查询验证处理，以防止因筛选执行错误而导致部署失败。 此错误导致了应用程序启动时出现异常，使得在受影响的环境中部署不成功。 此修复确保了一致的验证行为，支持顺利部署，使运行时查询验证不再中断。 (SITES-35529)
* 当配置浏览器的名称中包含 CJK 字符时，GraphQL Explorer 不再出错。 端点创建和已保存查询的访问现在可正常工作，GraphQL 查询编辑器页面保持正确无误。 (SITES-31616)

#### [!DNL Content Fragments] - 模型编辑器{#sites-model-editor-65-lts-sp2}

* 当重构操作将此功能与禁用的切换开关绑定时，嵌套内容片段模型停止工作。 此修复恢复了嵌套模型支持，不再需要切换改变。 作者可以在模型编辑器中重新创建并使用嵌套模型。 (SITES-38681) 重要

* 内容片段模型筛选面板不再显示未本地化的字符串。 AEM 现在会在所有区域设置下显示本地化的筛选标签和本地化的状态值。 (SITES-30863)
* 内容片段模型编辑器现在会为锁定警告对话框渲染本地化的字符串。 UI 会在所有受支持的语言中用区域设置资源替换未本地化的英语消息。 (SITES-28592)

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM Headless 需要一个专门的发布分支，以避免与主线版本之间的依赖项及捆绑包版本的冲突。 此更新添加了一个 `release/6.5lts` 无头分支，使依赖集和捆绑包版本保持一致。 Jenkins 现在可以整齐地构建无头代码库，不再出现版本冲突。 (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### 内容 API{#sites-content-api-65-lts-sp2}

一个功能切换错误导致误报了页面管理 API 状态。 此更新添加了一个专门的启用标志，将其与现有的切换开关一起进行评估。 页面管理 API 现在显示稳定的状态。 网站管理 API 保持试验性。 (SITES-39284)

#### 核心后端{#sites-core-backend-65-lts-sp2}

* 对 Sites 创作体验进行的更改，以解决导致标准页面编辑工作流中断的行为不一致的问题。 作者在组件交互过程中遇到意外结果，这干扰了内容更新，降低了可靠性。 此更改恢复了稳定的编辑器行为，确保了在各种受影响的场景中一致地执行创作操作。 (SITES-35162) 重要

* 改进了 Sites 创作行为，解决了在组件交互时页面编辑中断并导致结果不一致的问题。 作者遇到了意外的 UI 响应，这干扰了内容更新，降低了工作流的可靠性。 此更改恢复了稳定的编辑器状态管理，确保了在各种受影响的场景中可预测地正确执行创作操作。 (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### 发布项{#sites-launches-65-lts-sp2}

* Sites 时间线在发布提升操作中显示硬编码的英语文本：“Created version ... before promoting launch”（在发布提升之前创建了版本…）。 此更新将硬编码的字符串替换为使用本地化的消息。 时间线现在显示本地化的文本，使此条目与标准 AEM 本地化行为保持一致。 (SITES-39157)
* 当作者通过“提升当前页面和子页面”来提升子分区时，发布提升的范围发生偏移。 AEM 还提升了不相关的页面，导致实时网站发生意外更改。 此修复修正了发布范围的计算，确保只有选定的子树进行提升。 (SITES-38315)
* 发布中的内容片段未加入 `damAssetLucene` 索引，搜索结果和查询效率受到限制。 此更改将发布内容片段路径添加到索引定义中。 现在，搜索和自定义查询可找到 `/content/launches` 下的内容片段。 (SITES-35634)
* 即使产品在触屏 UI 中不显示内容片段发布，发布 UI 仍然显示内容片段发布的控件。 此更改去除了 cq-launches-content 中的内容片段发布代码路径，调整了发布列表筛选。 作者现在可以看到一致的页面发布选项，而没有内容片段发布条目。 (SITES-35633)
* AEM 6.5 LTS 快速启动缺少必需的发布捆绑包和先决条件，这阻止了发布 OpenAPI 的启用。 此更新添加了发布捆绑包和必需的依赖项，例如量度支持、DAM-cfm 更新和队列配置。 发布 API 现在可以在 6.5 LTS 快速启动上运行，且包含必需的运行时组件。 (SITES-35297)
* CF 发布打包时提取了更新的依赖项版本和不必要的 GraphQL 库，这使 AEM 6.5 LTS 集成变得复杂。 此更改使依赖项版本符合 AEM 6.5 LTS 基线，去除了不使用的 GraphQL 依赖项。 捆绑包的解析现在保持一致，CF 发布的启动保持稳定。 (SITES-35295)
* AEM 发布现在为 6.5 LTS 分支运行一个专门的 Jenkins 管道。 管道运行每晚构建版本，通过电子邮件发送错误警报。 此设置提高了测试覆盖范围，可尽早捕获回归错误。 (SITES-35293)
* AEM 6.5 LTS 现在推出经过更新的工件版本一致的发布 API 捆绑包。 此捆绑包会跟踪主要代码行，同时保持正确的 6.5 LTS 发行版本。 此更新稳定了在 6.5 LTS 技术栈中各处的发布 API 消耗。 (SITES-35292)
* AEM 6.5 LTS 现在包含一个经过更新的依赖项版本一致的发布核心捆绑包。 此更新添加了“片段 UUID”和“引用 UUID”两种数据类型的发布核心处理。 现在，发布处理可在所有发布和内容片段工作流中保持行为一致。 (SITES-35290)
* 改进了 Sites 编辑器，解决了导致正常页面创作工作流中断的行为不一致的问题。 作者遇到意外的组件交互，这干扰了内容更新，降低了编辑可靠性。 此更改恢复了一致的 UI 状态管理，确保了在各种受影响的场景中可预测地正确执行创作操作。 (SITES-35138)
* 发布编辑现在显示的是本地化的错误文本，而不是硬编码的 `Provided path is not a launch` 字符串。 现在，当“编辑”获得无效的发布路径时，UI 会在所有语言下渲染翻译过的消息。 (SITES-33360)
* AEM 6.5 LTS 现在包含发布 OpenAPI 侧端口工作。 此更新将发布 API 捆绑包、内容包和所需的快速启动工件的版本对齐，并为内容片段发布 OpenAPI 场景启用了稳定的 CI 验证。 (SITES-32050)
* 发布 UI 现在会将覆盖的模板标签本地化。 模板覆盖详细信息现在显示翻译过的文本，而不是只有英语的字符串。 (SITES-29525)
* AEM 解决了 **Sites** > **发布** > **编辑**&#x200B;中缺少本地化键的问题。 用户现在会看到翻译过的错误消息，而不是原始的“Unable to update launch source list”字符串（“无法更新发布源列表”）。 (SITES-21499)
* 发布提升 UI 现在显示本地化的状态标签和操作。 预览区域现在显示翻译过的&#x200B;**已删除**、**新建**&#x200B;和&#x200B;**视图**&#x200B;文本，而不是原始的英语字符串。 (SITES-13540)
* 现在，创建发布时会显示本地化的错误消息。 UI 不再显示原始的英语字符串，如 `Unable to create launch page`、`Source root resource is not a page` 或 `Mandatory parameter is missing`。 （SITES-13085）


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - 实时副本{#sites-msm-live-copies-65-lts-sp2}

* 更改内容时，管理员对 MSM 推送更改处理的可见性受到限制。 此修复添加了有关 MSM 事件接收和转出执行的详细日志记录。 调试输出现在会显示哪些事件触发、哪些内容路径改变、谁触发了这些更改。 (SITES-38029)
* AEM 修复了 Blueprint 转出日期字段上的本地化布局问题。 日期提示词现在适合控件，在所有受支持的语言（包括`fr_FR`）中确保可读性。 (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### 复制{#sites-replication-65-lts-sp2}

页面编辑器发布操作现在可以处理包含选择符或后缀的 URL。 所发布的请求现在会发送 JCR 页面路径，而不是选择符或后缀 URL 字符串，因此可完成激活，内容可上线。 复制操作现在会在失败时返回一个错误状态，从而防止出现“发布已开始”的假消息。 (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### 模板编辑器{#sites-template-editor-65-lts-sp2}

对于有些区域设置，模板状态文本会在&#x200B;**工具** > **一般** > **模板**&#x200B;中垂直显示。 “已过时”标签破坏了布局，显示为一列字符。 此修复修正了模板状态样式设置，使标签在一个水平线上渲染。 (SITES-36797)

#### 通用编辑器 {#sites-universal-editor-65-lts-sp2}

* OSGi 默认配置已设置为 `preview=true`，强制通用编辑器在预览模式下启动。 此更新修正了默认值，恢复了标准生产进入行为。 除非管理员明确启用预览模式，否则通用编辑器现在会在生产模式下打开。 (SITES-37193)
* 在开发和暂存环境中，通用编辑器打开命令现在默认为预览模式。 此命令添加了 `preview=true`，这可以使作者检查与预览上下文保持一致，避免意外打开生产环境。 (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Assets Relate 现在可使用包含空格的文件名。 现在，更新后的 Relate 客户端逻辑可以正确处理包含空格的路径，避免在选择关系时出现 `undefined` 来源的错误。 现在，Relate 对话框会打开并保存关系，不再发生 UI 卡顿或出现旋转器。 DAM 用户无需重命名文件即可关联、获取资产以及将资产取消关联。 (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 新的 Dynamic Media 视频播放器集成（限量推出）：现在，AEM 6.6 快速启动中提供新的 Dynamic Media 视频播放器体验。 此增强功能目前仅作为可控推出功能的一部分为初始客户启用。 (Assets-60165)
* 解决了视频属性对话框中的选择缩略图选项不能打开资产选取器的问题，恢复了用户为视频资产选择自定义缩略图的功能。 (Assets‑58926)
* 在 Dynamic Media 视频中，在“字幕和音轨语言”下拉列表中增加了阿拉伯语选项，使作者能够直接在 AEM 中管理阿拉伯语字幕。 (Assets‑61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->

<!--
#### Forms Designer
-->

### [!DNL Forms]{#forms-65-lts-sp2}

* 用户遇到表单数据模型 (FDM) 编辑器 `Data Source / Enter Keyword` 功能方面的问题。 此问题影响了搜索和选择数据源的能力。 (FORMS-23971)
* 在移动设备上，自适应表单中的表格组件在顶部渲染了一个隐藏的标题，导致屏幕阅读器读出错误的内容。 这影响了依赖屏幕阅读器进行导航的用户。 (FORMS-23754)
* 用户遇到基于核心组件的自适应表单引用了标记为 granite:InternalArea 的资源类型的问题，这影响了内部部署表单附加组件中多个 granite 组件的功能。 (FORMS-23632)
* 升级到 AEM 6.5 LTS SP1 后，表单提交失败。 用户遇到缺少 com.adobe.cq.social.commons.CollabUtil 的情况，这导致出现 JSP 编译错误和电子邮件操作失败。 (FORMS-23457)
* 用户遇到在基于基础组件的自适应表单中 hCaptcha 未正确翻译的问题。 这影响了非英语用户正确完成表单的能力。 (FORMS-23426)
* 用户遇到表单提交失败的问题，出现了 SAXParseException：“序言中不允许包含内容” (HTTP 500)。 出现此问题的原因是预填充数据 XML 中有 null 值，导致服务器端 XML 解析失败。 (FORMS-22633)
* 用户遇到了自适应表单未通过 Web 内容无障碍准则 (WCAG) 审核的问题。 原因是表单的 Tab 导航标记无效。 也就是说，非列表元素被渲染为一个只允许包含列表项的列表的直接子元素。 此问题使表单无法通过无障碍性验证器，影响了必须满足法律或内部合规性要求的组织。 (FORMS-22101)
* 用户遇到记录文档 (DoR) /提交 PDF 的无障碍性问题，文档中的空白表单字段未标记为表单元素。 这给屏幕阅读器带来了困难，影响了残障用户有效进行导航和完成表单的能力。 (FORMS-21989)
* 用户遇到了在加载表单时子面板中组件的脚注不显示的问题。 当有脚注的项目是页面上的最后一个组件时，会发生此问题。 (FORMS-21925)
* 用户在 AEM Forms 编辑器中选择组件时遇到问题。 在选项卡之间导航并返回到第一个选项卡时，有些容器变成不可选，使用户无法轻松地识别和交互。 (FORMS-21814)
* 用户在自适应表单仪表板中遇到安全漏洞。 具体而言，在 startpointcontrol.js 文件中发现了一个跨网站脚本 (XSS) 问题，它可能会允许执行恶意脚本。 (FORMS-20679)
* AEM Forms 6.5 LTS 在 JBoss® EAP 8 上的群集部署中，`domain/configuration/domain_oracle.xml`、`domain_mysql.xml` 和 `domain_mssql.xml` 文件不再包含重复的 `<security>` 标记，此标记导致了无效的 XML 并阻止了域控制器启动。 (FORMS-24687)
* 在 Turnkey 模式下，现在可在全新安装和升级时正确应用数据库端口更新。 在全新安装模式下，用户可以从所有可用端口中进行选择，在升级模式下，可以在升级时正确引用 lc_turnkey.xml 中更新的数据库端口。 (FORMS-24689)
* 在 Linux®上设置 JBoss® EAP 8.0 时，在 Windows 上更改的 Shell 脚本不再因 CRLF 行末尾而导致出现 `/bin/sh^M: bad interpreter or $'\r': command not found` 错误。 (FORMS-24688)
* 在 JBoss® EAP 8 上运行的 Forms JEE LTS 部署中，Reader 扩展 UI 可能会失败，并显示内部服务器错误。 (FORMS-24894)
* 在 Linux® 上，如果 Forms JEE LTS 配置管理器在运行时 `configurationManager/config/solcomp/LFS_Foundation.properties` 中的 `OSFileSetIntendedFor` 值未设置或不正确，会阻止为 Linux® 正确进行量身定制的配置，用户就会遇到运行时或部署问题。 安装之后并在运行配置管理器之前，请在这个文件中设置 `OSFileSetIntendedFor=Linux`。 (FORMS-24741)

<!--
#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### 基础 {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* Sling 资源访问安全现在在 1.1.2 版本上运行。 当多个 ResourceAccessGateHandler 服务注册时，ResourceAccessSecurityImpl 在初始化时不再抛出 ClassCastException。 现在可以可靠完成初始化，避免了在具有多个处理程序的环境中启动失败。 （NPR-42750）
* JMX 控制台和网页控制台现在会为控制台 CSS 资源发送一个 `Content-Type: text/css header`。 严格的 MIME 检查不再阻止样式表加载，因此 `/system/console/jmx` UI 会以正常样式渲染。 (GRANITE-63677)
* AEM 现在会避免在生成的 `WEB-INF/resources/provisioning/model.txt` 中 `contributor` 组有重复的 ACL 条目。 WAR 输出现在包含一个一致的 ACL 块，这防止了混淆审阅时的权限区别。 (GRANITE-63269)
* 在捆绑包刷新操作中，AEM 不再清除反序列化防火墙阻止列表和允许列表设置。 更新了筛选条件注册逻辑，使活跃的防火墙实例与已保存的配置保持一致，这样无需重新启动就能确保启用了保护。 (GRANITE-61382)
* Felix 网页控制台在访问 `/system/console` 时不再间歇性抛出 `NullPointerException` 错误。 更新了 ServiceTracker 处理程序，防止出现 null 跟踪器状态。 在重复请求和自动验证时，控制台登录和导航保持稳定。 (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

服务包升级后，打开 JSP 文件时 CRXDE Lite 不再显示一个空白选项卡。 AEM 现在提供匹配的 CodeMirror 核心和附加组件代码，这可防止严重的浏览器错误，保持编辑器可用。 (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

表达式安全验证器现在能处理 OSGi 配置值为空或 null 的情况。 它应用安全默认值，忽略空数组，记录清晰的日志，从而防止 NullPointerException 和不可预测的验证结果。 (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 集成{#foundation-integrations-65-lts-sp2}

即使存在开始和结束日期，AEM 现在也会同步 Adobe Target 活动。 Target 负载现在可将活动日期的格式设置为完整的 ISO 8601 时间戳，包括秒、毫秒和时区。 Target 不再拒绝包含 `InvalidJson.Json` 的请求。 已计划的活动现在会迁移到一个同步状态，而不再保持不同步。 （CQ-4360733）

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 

#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS 服务包 2 需要 S3 连接器 1.60.10 或更高版本。 S3 数据存储库配置现在包括 `crossRegionAccess` 和 `mode`，因此管理员可以启用跨区域存储桶访问权限，并在需要时将存储库切换到 GCP。 `s3EndPoint` 现在需要一个与 `s3Region` 一致的区域，或者它保持为空，使驱动程序生成端点。 (GRANITE-64873)


#### 快速入门{#foundation-quickstart-65-lts-sp2}

* Sling 更新了管理登录允许列表，以使用包含的术语和新的配置 PID。 此更改与 Sling JCR Base 3.2.0 一致。 (GRANITE-63756)

  **影响**

   * Sling 弃用了这些 PID，您应该从配置中将它们移除：
      * 工厂 PID：`org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * 全局 PID： `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
这些较旧的配置使用属性，如 `whitelist.name` 和 `whitelist.bundles`。

   * Sling 仍为已弃用的 PID 提供部分向后兼容性，但不要将它们用于新配置。 请改用较新的 `LoginAdminAllowList.*` PID。
   * 不要同时运行已弃用的和新的允许列表配置。 混合配置可能会产生歧义，导致意外行为。 如果您迁移到 AEM 6.5 LTS SP2，请完全移除已弃用的 PID。

  **您应该怎么做**

   1. 查找使用 `LoginAdminWhitelist*` PID 的允许列表配置。
   1. 将它们替换为适当的新 PID：

      * 工厂 PID：`org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * 全局 PID：`org.apache.sling.jcr.base.LoginAdminAllowList`

      有关其他详细信息，请参阅[已弃用的管理登录用允许列表捆绑包方法](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login)。

* AEM 6.5 LTS SP2 更新了 Sling、Oak 和 Felix 的基础层捆绑包集。 这些升级增强了核心运行时的稳定性，在整个平台上对齐了依赖项版本。 (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311)
-->

#### Sling{#foundation-sling-65-lts-sp2}

AEM 现在包括 Sling Engine 2.16.6。 此更改消除了由安全工具标记的 XSS 违规，提高了核心渲染的安全性和稳定性。 （NPR-43105）

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

Java 17 或 Java 21 上的 AEM 翻译不再因 XLIFF 格式问题而失败。 导出管道现在可生成翻译提供程序接受的符合标准的 XLIFF。 此更改消除了翻译作业中断问题，恢复了 AEM 和翻译服务之间可预测的传递。 现在，翻译工作流在所有受支持的 Java 运行时保持稳定。 (CQ-4360217)

#### 工作流{#foundation-workflow-65-lts-sp2}

处理工作流通知时，EmailNotificationService 处理器不再反复触发“未找到区段”错误。 更新后的异常处理程序检测到 SegmentNotFoundException 后会停止处理循环，而不是继续无效读取。 访问收件箱和工作项时，工作流执行保持稳定，日志噪声下降。 (GRANITE-62635)




## 关于 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 的平台的构建基础是更新版本的基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java™ 内容存储库：Apache Jackrabbit Oak 1.68.x。

Eclipse Jetty 11.0.x 被用作快速入门的 servlet 引擎。

### Java™ 支持  {#java-support}

* 支持 Java™ 17 和 Java™ 21。
* 为了获得最佳性能，请用其他值覆盖默认 GC 值。 有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* 如果 Oracle 未公开提供，Adobe 会分配 Java™ 17 和 Java™ 21 维护更新，以便客户在 AEM 相关项目中使用。

### Uberjar 包装 {#uber-jar-packaging}

用于 AEM 6.5 LTS SP2 的 UberJar 使用 AEM 6.5 LTS UberJar 版本 6.6.2。 您可以从 Maven 中央存储库检索相应的 UberJar 工件。 与 AEM 6.5 不同，AEM 6.5 LTS 将公共 API 和已弃用的 API 分开成两个不同的工件。

要使用公共 API 进行编译，请使用以下方法：

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

如果您的代码还依赖于已弃用的 API，请添加以下内容：

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

另请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升级 {#upgrade}

* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 有关详细的升级说明，请参阅 [JEE 上的 AEM Forms 6.5 LTS SP1 升级指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### AEM 6.5 LTS 服务包升级最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**环境**
适合：安装服务包 2 (SP2) 的 AEM 6.5 LTS（内部部署）客户。 SP2 以 Quickstart JAR 形式交付。

**为什么这个升级做法很重要**
用于 AEM 6.5 LTS 的 SP2 以 Quickstart JAR 形式提供，而不是需要通过包管理器安装的 ZIP 文件。 内部部署客户可通过替换 Quickstart JAR、解压并重新启动的方式进行升级。 此方法与 Adobe 的就地升级流程保持一致。

**推荐的升级流程（创作或发布实例）**

1. 验证您的 AEM 6.5 LTS 实例运行正常且可访问。
1. 从软件分发下载 Quickstart JAR（例如 `cq-quickstart-6.6.x.jar`）。
1. 停止正在运行的实例。
1. 在 AEM 安装目录中（`crx-quickstart/` 目录之外），将原有的 Quickstart JAR 替换为 SP2 JAR。
1. 解压该 JAR 文件：

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   （根据需要调整堆标志。）

1. 将解压后的 JAR 重命名以匹配对应角色和端口，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 启动 AEM，并在用户界面（“帮助”>“关于”）及日志中确认升级是否成功。

**良好维护规范**

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


有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

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

建议客户检查其当前部署中是否正在使用此功能。 制定更改实施的计划，改用提供的替代方案。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
| 快速入门 | Mongo API | Mongo API 现已弃用，已计划在未来的发行版本中移除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API 中的内容片段支持 | AEM 6.5 LTS SP2 为内容片段和模型管理提供了现代化的 OpenAPI，因此 AEM Assets REST API 中的旧版内容片段支持端点已弃用。<br>Adobe 打算在生命寿命结束公告之前保持这些旧版端点可用。 Adobe 不计划为已弃用的端点提供进一步的增强功能。 | 6.5 LTS SP2 |
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 在 AEM 中管理无头内容的首选编辑器有：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于进行可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于进行基于表单的编辑。 | 6.5 LTS GA |
| [!DNL Foundation] | 支持 com.adobe.granite.oauth.server | Adobe IMS 集成 |  |

### 已移除的功能 {#removed-features}

此部分列出了 AEM 6.5 LTS 中已移除的功能。 之前的版本中已将这些功能标记为已弃用。

* 对 CRX 存储库持久性的 RDBMK 支持已移除。
* 在群集环境中，MongoMK 现在是存储库持久性的唯一受支持的选项。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
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

* 在配置管理器中，如果未选择模块或者只选择了有限的组件，在 AEM Forms 6.5 LTS JEE Turnkey 自定义模式下引导启动时数据库初始化失败。 失败原因是缺少依赖项 (xalan-2.7.2.jar) 而导致出现错误。 将 JAR 文件添加到 adobe-livecycle-jboss.ear\lib 解决了这个问题。 (FORMS-24690)
* 在 JBoss®上运行的 Forms JEE LTS 上，与电子邮件相关的功能可能会失败。 尝试使用电子邮件功能时，服务器记录错误： `Error IMAPProvider not a subtype`。 (FORMS-24892)
* 在WebSphere® Liberty Profile上运行的Forms JEE LTS Service Pack 2部署中，电子邮件功能可能会失败。 尝试使用电子邮件功能时，服务器记录错误： `Could not convert socket to TLS`。 (FORMS-24692)

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

从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip)安装修补程序以使用此功能。

>[!NOTE]
>
> 安装该修补程序后，请验证所有已安装捆绑包的捆绑状态，以确保`com.adobe.granite.apicontroller`的默认配置未引入可能会影响现有自定义实施的意外解决限制。

### Sling-Initial-Content (SP2) 不再支持 JSON 注释 {#json-comments-no-longer-supported-in-sling-initial-content}

这个问题影响了开发人员和管理员部署那些使用 `Sling-Initial-Content` 和 JSON 文件的 OSGi 捆绑包。

从 AEM 6.5 LTS SP2 开始，`Sling-Initial-Content` 捆绑包中使用的 JSON 文件不再接受注释（`//` 或 `/* */`）。 早期的 AEM 版本接受了注释，因为 `javax.json` 提供程序对此比较宽容。 AEM 6.5 LTS SP2 将 `org.apache.sling.jcr.contentloader` 升级为版本 2.6.0，后者将 JSON 解析器换为 `jakarta.json`。 虽然 [JSON 规范 (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) 未定义注释的语法，但由于 `javax.json` 提供程序的宽容性，较早的 AEM 版本接受注释。 `jakarta.json` 提供程序不提供此扩展。

沉默的错误：捆绑包激活时内容节点加载失败，没有为安装程序提供任何错误消息。 如果在升级到 SP2 后意外缺少内容，请检查 OSGi 安装程序日志中是否记录了 JSON 解析错误。 要识别受影响的捆绑包，请在 `Sling-Initial-Content` 清单头下面列出的 JSON 文件中搜索 `//` 或 `/* */`。

>[!CAUTION]
>
> 请移除您的 `Sling-Initial-Content` 捆绑包中 JSON 文件的所有注释，以免在升级到 AEM 6.5 LTS SP2 后内容加载失败。

### 为 Sites Headless API 安装必需的 Oak 索引{#site-headless-api}

一些迁移到 Sites Headless 的 API 需要额外的 Oak 索引，才能提供完整功能。

安装 `cq-dam-cfm-indices` 包，以使用以下功能：

* 列出内容片段模型
* 列出内容片段
* 搜索 API
* 工作流

从 Adobe 软件分发门户下载索引包 [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)。

### 在使用仅 SSL 功能的情况下，Dispatcher 连接失败（已在 AEM 6.5 LTS SP1 及更高版本中修复）{#ssl-only-feature}

>[!NOTE]
>
> 此问题仅出现在 AEM 6.5 LTS GA 版本中。

在 AEM 部署中启用仅 SSL 功能后，会发生一个影响 Dispatcher 与 AEM 实例之间连接的已知问题。 启用此功能后，健康检查可能会失败，并且 Dispatcher 和 AEM 实例之间的通信可能会中断。 尤其是当客户尝试通过 `https + IP` 将 Dispatcher 与 AEM 实例连接时，会出现此问题。 它与 SNI（服务器名称指示）验证问题有关。

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

如果您遇到这个问题，请联系 Adobe 客户支持部门。 有一个热修复 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 可以解决这个问题。 采用必要的热修复之前，不要尝试启用仅 SSL 功能。

## 包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下zip文件包含文本文档，其中列出了此Experience Manager 6.5 LTS Service Pack版本中包含的OSGi包和内容包：

* [OSGi包](/help/release-notes/assets/65lts_sp2_bundles.zip)
* [内容包](/help/release-notes/assets/65lts_sp2_packages.zip)

## 受限网站{#restricted-sites}

这些网站仅向客户开放。 如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

