---
title: Adobe Experience Manager 6.5 LTS SP2的最新发行说明
description: 查找 Adobe Experience Manager 6.5 LTS 服务包 2 的当前版本信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: f75f02c1e10deb6eef788d6584229c045b88880d
workflow-type: tm+mt
source-wordcount: '6062'
ht-degree: 21%

---

# Adobe Experience Manager 6.5 LTS SP2的最新发行说明 {#release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2026年2月19日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS SP2中包含的内容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP2包括新增功能、客户请求的关键增强功能和错误修复。 还包括自 2025 年 3 月 6.5 LTS 首次发布以来推出的在性能、稳定性和安全性方面的改进。在 6.5 LTS 上[安装此服务包](#install-update)。

## 主要功能和增强功能

**AEM Sites**

AEM 6.5 LTS SP2现在包含用于[内容片段和模型管理](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/)和[启动项](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/)的OpenAPI。 这些API提供对内容片段和启动项的访问权限，以进行创作和计划。 它们使用与AEM as a Cloud Service相同的现代OpenAPI。


<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS 服务包 2 中修复的问题 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP2}

#### 辅助功能 {#sites-accessibility-65-lts-sp2}

* 当作者在编辑过程中将组件浏览器中的项目悬停在该组件上时，文本组件会失去键盘焦点。 这会中断键入并触发WCAG 3.2.1下的辅助功能故障。此修复可防止悬停样式切换焦点，并可在组件浏览器交互期间保持文本组件聚焦。 （SITES-35370）
* 更正了“描述”富文本字段中的焦点管理，该字段使用Tab键阻止了向前导航。 用户在RTE中卡住，因为组件依赖非标准键盘命令来转移焦点，这破坏了预期的对话框导航。 此更改强制标准键盘交互操作，并保留整个对话框中的逻辑选项卡排序。 （SITES-35228）
* 修复了站点编辑器中的问题，该问题在页面创作期间中断了预期行为并导致组件交互不一致。 作者遇到不可靠的UI响应，这干扰了标准编辑任务并降低工作流效率。 该更新细化了底层编辑器逻辑，并恢复了受影响组件之间稳定、可预测的交互。 （SITES-35227）
* 一种回归，破坏了页面编辑器中的资产选择器，并阻止其在特定页面编辑场景中加载。 现在，作者在编辑页面时选择或浏览资产时，可以正常打开并使用资产选择器。 此更改恢复对加载失败中断的资源选择工作流的一致访问权限。 （SITES-35226）
* 消除了站点编辑器中的问题，该问题在页面交互期间导致不一致行为并中断了标准创作工作流。 该缺陷导致意外的UI响应，干扰了组件配置和内容更新。 此更新可稳定受影响的功能，并恢复跨页面可靠执行编辑操作。 （SITES-35225）
* 消除了Sites创作界面中导致页面编辑期间出现不一致行为并中断正常工作流的缺陷。 作者遇到意外的UI响应，这些响应会干扰组件交互和内容更新。 此更新使受影响的功能更加稳定，并在所有编辑场景中恢复可靠、可预测的行为。 （SITES-35224）
* AEM Sites现在包括对图像的`alt`文本支持，以满足ADA和WCAG要求。 页面输出不再忽略`alt`属性，因此屏幕阅读器会收到正确的替换文本。 （SITES-27153）
* 修复了`Note Add`工具栏布局，以便“添加”按钮不再与320px视区宽度处的标题重叠。 改进了小屏幕重排，使控件在400%缩放期间保持可读性和可用性。 （SITES-25376）
* 修复了链接选择对话框错误导致的屏幕阅读器公告缺失问题。 UI现在通过状态消息容器发布错误文本，因此NVDA会在消息出现时立即读取消息。 （SITES-25368）
* 从侧边栏资产列表中删除了ARIA网格和网格单元格角色。 恢复标准列表语义和键盘焦点顺序，从而改进屏幕阅读器导航并减少额外的制表位。 （SITES-25361）
* 更正了侧边栏Assets中的焦点排序。 键盘用户现在可通过一致的选项卡路径执行每个资产操作，包括编辑。 （SITES-25360）
* 修复了Search Assets模式中视区宽度为320px的布局溢出问题。 模态内容现在会重新流动并保持可读状态，因此控件不再重叠或溢出对话框。 （SITES-25330）
* 更正了“编辑”按钮的NVDA输出。 NVDA现在会宣布“编辑”操作，而不是“按下预览按钮”。 （SITES-25320）
* 修复了导致静默或常规屏幕阅读器输出的未命名的人口统计工具栏文本输入。 现在，每个输入都公开一个清晰的基于标签的可访问名称，这改进了键盘和辅助技术导航。 （SITES-25316）
* 更正了“布局预览”导航期间“人口统计”工具栏的键盘焦点顺序。 选项卡导航现在直接从“人口统计”按钮移动到工具栏控件，而无需跳至辅助工具栏。 （SITES-25305）
* 修复了“编辑布局”标尺上“较小的Screens”和“平板电脑”标签的公告顺序不正确的问题。 屏幕阅读器现在会在正确的标尺标记处朗读这些标签，这些标记与页面布局相匹配。 （SITES-25291）
* 修复了“编辑布局”工具栏在200%缩放时溢出的问题。 内容现在保留在视区中，并保持可通过滚动访问。 （SITES-25288）
* 解决了批注叠加中焦点顺序不正确的问题。 键盘Tab键现在可在叠加控件和注释项之间循环。 父页面不再从叠加后获得焦点。 （SITES-25282）
* 修复了样本弹出框焦点处理问题。 该对话框现在将焦点移动到清晰的标题，并在该入口点开始屏幕阅读器输出。 NVDA不再不按顺序读取完整的对话框内容。 （SITES-25275）
* 修复了日期选取器关闭后的时间扭曲模式焦点处理问题。 `Escape`现在将焦点返回到日期选取器按钮。 日期选择现在将焦点置于日期选取器控件旁边的输入字段，从而防止焦点丢失和后台页面访问。 （SITES-25264）
* 修复了“删除注释”对话框的键盘焦点处理问题。 现在，“取消”将焦点返回到打开该对话框的`Delete`控件，而不是“确认十六进制值”控件。 取消后，屏幕阅读器不再朗读不相关的对话框内容。 （SITES-25258）
* 修复了“注释模式”对话框的焦点处理问题。 现在，打开对话框会将焦点置于对话框标题上，并阻止NVDA读取画布内容和无关的对话框文本。 键盘导航现在保留在对话框中，直到关闭。 （SITES-25257）
* 修复了320px宽度时的搜索模态布局问题。 模式内容现在可以干净地重排，并避免与树目录重叠。 用户可以查看结果并导航目录，而无需隐藏控件。 （SITES-25246）
* 搜索模式文本在文本间距增加后不再剪切。 树目录布局现在保持清晰的分离状态，因此标签和条目保持可读性。 用户现在可以在没有重叠或截断文本的情况下完成搜索和导航。 （SITES-25245）
* 激活注释现在将键盘焦点移动到注释内容，而不是退出注释按钮。 Tab键顺序遵循逻辑顺序，使相关控件无需反向导航即可访问。 （SITES-25241）
* 在键盘导航期间，“设置日期”和“退出时间扭曲”链接缺少可见的焦点指示器。 UI现在呈现一种独特的高对比度焦点样式，以便用户能够一眼就识别活动链接。 （SITES-25232）
* Teaser模式标头不再阻止键盘用户移动对话框。 键盘控件现在允许拾取、移动和放置操作，这提高了屏幕阅读器的可用性和整体可操作性。 （SITES-25226）
* AEM现在为“Teaser模式信息”按钮使用有意义的易访问标签。 屏幕阅读器会朗读一个清除操作名称，而不是默认的图标替换文本字符串。 （SITES-25223）
* 屏幕阅读器现在在用户激活编辑按钮时朗读正确的操作。 NVDA不再报告“预览按钮已按下”，这会导致键盘导航期间出现误导性反馈和混淆。 （SITES-25208）
* 现在，展开左边栏可将键盘焦点移动到第一个左边栏控件。 选项卡序列不再跳转到辅助工具栏或登陆中间列表，因此键盘用户无需反向导航即可访问左边栏内容。 （SITES-24998）
* 设备模拟器栏内容现在在320像素视区宽度下保持完全可见。 工具栏文本和控制自动换行，而不是截断，从而减少重叠并提高可读性。 （SITES-24953）
* AEM现在在模拟器工具栏中显示完整的iPhone设备标签。 文本不再以默认宽度截断，从而提高可读性和设备选择清晰度。 （SITES-24952）
* 列表视图表标题现在通过ARIA公开排序状态。 屏幕阅读器在列排序操作后公告升序或降序。 （SITES-24943）
* 在文本间距更改期间，AEM现在保留卡片视图中的“更多操作”菜单标签可见性。 菜单选项保留完整的文本，包括“快速发布”，并且在任何WCAG文本间距设置期间，菜单保持可读性。 （SITES-24941）
* 信息卡操作菜单栏现在会在信息卡视图中公开一个可访问的名称。 屏幕阅读器清晰地宣布了菜单栏的目的，语音控制可以通过名称来定位控制。 （SITES-24938）
* 卡片视图不再依赖导致屏幕阅读器行为混乱的ARIA网格语义。 UI现在为卡片内容和卡片操作栏提供有意义的角色和标签，这减少了键盘使用期间缺少的控件。 （SITES-24933）
* 现在，每当用户将工具提示图标悬停时，`Delete Modal`工具提示都会显示。 焦点操作现在显示相同的工具提示文本，这提高了鼠标和键盘用户的重复访问能力。 （SITES-24778）
* 现在，用户配置边栏后，左边栏导航会遵循预期的键盘焦点顺序。 Tab键焦点位于选定的左边栏区域而不是Switch Display，这可以提高屏幕阅读器导航的清晰度。 （SITES-24754）
* 修复了在“用户首选项”模式中的色板导航期间出现错误的NVDA反馈。 NVDA现在会读取接收焦点的样本的标签，从而删除误导性的颜色输出。 样本集现在支持一致的键盘导航和清晰的选择感知。 （SITES-24739）
* 减少了`Spin`控件的详细NVDA输出。 删除了重复输入标签的冗余组标签，因此NVDA会公告一次控制名称。 现在，键盘和屏幕阅读器导航功能可提供单一、清晰的公告。 （SITES-24725）
* “轮播”对话框现在将焦点置于对话框标题而不是“项目”选项卡。 取消并Esc将焦点还原到启动该对话框的控制项，这将减少详细的NVDA输出。 （SITES-24716）
* 现在，链接选择对话框会将编程标签与上一级树项目的屏幕标签保持一致。 箭头键导航会触发每个项目的可靠屏幕阅读器公告，并删除误导性的标签输出。 （SITES-24710）
* 现在，链接打开选择对话框在320-px视区下可正确重排。 内容不再超出模式或截断，并且模式不再显示水平滚动条。 （SITES-24709）
* 现在，链接打开选择对话框在“关闭”或“取消”后将键盘焦点恢复到该对话框触发器。 焦点不再跳转到链接输入，这可保持屏幕阅读器上下文稳定并减少额外导航。 （SITES-24707）
* 图像模式对话框现在遵循逻辑焦点顺序。 取消后，焦点不再跳过之前的控件，也不会落到页面标志上，并且用户会在退出后重新获得对配置按钮的关注。 （SITES-24693）
* 引用边栏模式对话框现在会捕获键盘焦点。 Tab键和Shift+Tab键停留在对话框控件中，并且焦点不再跳转到页面内容。 屏幕阅读器仅朗读对话框内容。 （SITES-24683）
* 现在，超链接路径选择模式将焦点设置在打开的对话框标题上。 取消关闭对话框并将焦点恢复到“打开选定内容对话框”按钮，从而防止焦点丢失和屏幕阅读器输出冗余。 （SITES-24672）
* “搜索”字段现在使用永久的屏幕标签，而不是占位符文本。 标签在输入期间保持可见，这提高了键盘、屏幕阅读器和语音用户的清晰度。 （SITES-24529）
* Teaser模式对话框现在将焦点设置在打开的对话框标题上。 关闭该对话框会将焦点返回到`Configure`控件，从而防止焦点丢失和屏幕阅读器输出过多。 （SITES-24522）
* 侧边栏Assets面板现在包含一个“关闭”控件。 “关闭”将键盘焦点返回到侧边栏切换开关中，并防止通过面板内容强制使用Tab键。 （SITES-24489）
* 键盘Tab键现在可访问管理员表格内的按钮和链接。 用户不再依赖箭头键单元格导航来查找交互式控件。 （SITES-24285）
* 图像组件对话框不再以图像形式显示装饰性帮助图标和全屏图标。 屏幕阅读器现在会跳过这些图标，继续将重点放在可操作控件和字段内容上。 （SITES-2940）
* 站点管理员现在从文件夹缩略图图标中删除图像角色。 辅助技术会跳过这些装饰性元素，将焦点集中在文件夹名称和操作上。 （SITES-2852）
* 内容树现在将键盘焦点路由到活动树项或第一个树项。 树容器不再充当空的Tab停止点，从而防止出现Shift+Tab焦点陷阱。 （SITES-1577）

#### 管理员用户界面{#sites-adminui-65-lts-sp2}

站点控制台列表视图设置未反映列表视图中显示的列。 该对话框打开，其中已清除复选框，且所选列计数不正确。 “修复同步”对话框的状态与活动的网格列一致，并更新计数器以匹配实际的列可见性。 （SITES-38576）

#### 经典用户界面{#sites-classicui-65-lts-sp2}

升级后，经典UI文本组件编辑显示原始HTML标记，而不是富文本。 Service Pack 2更正了经典UI RTE（富文本编辑器）渲染，以便编辑器显示格式化的内容并保留存储的标记。 该修复还会在重复编辑期间停止标记扩展并保存。 （SITES-38709）

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

Headless事件支持在6.5 LTS中缺少内容片段和模型所需的OSGi事件。 更新添加了事件捆绑包以及所需的依赖关系，并包括6.5 LTS版本。 内容片段和模型事件现在可以正确触发，并支持启动API工作流。 （SITES-35329）

#### [!DNL Content Fragments] - 管理{#sites-admin-65-lts-sp2}

* 调整了Sites创作界面中的组件处理，以停止页面更新期间的不规则行为。 该缺陷导致不可预测的编辑器响应，干扰了常规的内容修改并降低工作流效率。 该更新使编辑器逻辑与预期的交互模式一致，并在创作活动期间提供可靠的性能。 (SITES-35078)关键

* 回归损坏了内容片段的Assets控制台列表视图，并在列表呈现期间触发了错误。 在删除preview-info后，更新会更正列表视图逻辑，并恢复稳定的列表输出。 控制台现在可正常显示内容片段，而不会出现任何故障，并使列表交互保持可用。 （SITES-38683）
* 内容片段编辑器现在本地化标记标签。 编辑器还会本地化收藏集标签，因此UI文本与选定的区域设置匹配。 （SITES-977）


#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-65-lts-sp2}

* 重构后，当功能切换保持禁用状态时，内容片段变体标记消失。 此修复程序可恢复对变体标记的支持，即使该切换保持关闭状态也是如此。 作者可以在内容片段编辑器中再次添加和查看变体标记。 (SITES-38682)关键
* 在作者从内容片段编辑器导航回之后，编辑的内容片段从Assets控制台列表中消失。 浏览器缓存返回了一个过时的列表并隐藏了更新的片段，直到手动刷新为止。 此修复程序为编辑器返回路径添加了缓存控制处理，以便列表正确重新加载并保持编辑后的片段可见。 (SITES-35374)关键

* 在最近的UI样式更改后，内容片段RTE显示布局和视觉问题。 Service Pack 2改进了RTE样式，以便工具栏和可编辑区域正确呈现并保持可读。 内容片段编辑器现在与页面编辑器的外观和行为一致。 （SITES-38684）
* 从Polaris资产选择器中删除IMS范围破坏了内容片段与投放端点的集成。 打开远程资产选择器并选择资产时，作者会遇到故障。 该更新重新添加所需的IMS范围并恢复稳定的投放层访问。 （SITES-35837）
* “关联内容”面板不再呈现硬编码的“未定义”占位符。 内容片段编辑器现在通过本地化资源解析该文本，因此编辑器可以看到翻译的UI文本。 （SITES-33675）
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* 内容片段编辑器现在在各个区域设置中显示翻译的“常规”选项卡标签。 编辑器会替换未本地化的选项卡文本，并从选项卡标题中删除内部ID。 （SITES-30715）
* 内容片段编辑器现在为允许的资源类型显示翻译的名称。 在作者配置内容引用限制时，选取器列表不再混合内部字符串和仅英语标签。 （SITES-29699）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* 优化了GraphQL查询验证处理，以停止因过滤器执行错误导致的部署失败。 缺陷会在应用程序启动期间产生异常，并阻止在受影响的环境中成功转出。 该修订版确保一致的验证行为，并支持顺利部署，而不会出现运行时查询验证中断的情况。 (SITES-34301)关键

* “编辑GraphQL端点”对话框现在显示本地化的UI字符串。 该对话框不再显示纯英文文本，例如“从配置中获取GraphQL架构”，并且相关标签在各个区域设置中正确呈现。 （SITES-34018）

#### [!DNL Content Fragments] - GraphQL查询编辑器{#sites-graphql-query-editor-65-lts-sp2}

* 优化了GraphQL查询验证处理，以停止因过滤器执行错误导致的部署失败。 缺陷会在应用程序启动期间产生异常，并阻止在受影响的环境中成功转出。 该修订版确保一致的验证行为，并支持顺利部署，而不会出现运行时查询验证中断的情况。 （SITES-35529）
* 当配置浏览器名称包含CJK字符时，GraphQL Explorer不再失败。 端点创建和保存的查询访问正常工作，并且GraphQL查询编辑器页面保持无错误。 （SITES-31616）

#### [!DNL Content Fragments] — 模型编辑器{#sites-model-editor-65-lts-sp2}

* 当重构将功能绑定到禁用的切换开关时，嵌套内容片段模型停止工作。 该修复程序无需切换更改即可恢复嵌套模型支持。 作者可以在模型编辑器中再次创建并使用嵌套模型。 (SITES-38681)关键

* 内容片段模型过滤器面板不再显示未本地化的字符串。 AEM现在显示所有区域设置的本地化过滤器标签和本地化状态值。 （SITES-30863）
* 内容片段模型编辑器现在呈现锁定警告对话框的本地化字符串。 UI用各种受支持语言的区域设置资源替换未本地化的英文消息。 （SITES-28592）

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM Headless需要一个专用发布分支来避免依赖关系，以及避免与主线内部版本的捆绑包版本冲突。 此更新添加了6.5lts版本的Headless分支，并使依赖项集和捆绑包版本保持一致。 Jenkins现在可以干净地构建Headless代码库，而不会出现版本冲突。 （SITES-36585）

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### 内容API{#sites-content-api-65-lts-sp2}

功能切换缺陷误报了页面管理API状态。 该更新会添加一个专用启用标志，并在现有切换旁评估该标志。 页面管理API现在显示稳定状态。 站点管理API仍处于试验阶段。 （SITES-39284）

#### 核心后端{#sites-core-backend-65-lts-sp2}

* 对站点创作体验进行了更改，以解决会中断标准页面编辑工作流的不一致行为。 在组件交互过程中，作者遇到意外结果，这会干扰内容更新并降低可靠性。 此更改将恢复稳定的编辑器行为，并确保在受影响的场景中一致地执行创作操作。 (SITES-35162)关键

* 改进了Sites创作行为，以解决在组件交互期间中断页面编辑并导致结果不一致的问题。 作者遇到了意外的UI响应，这些响应会干扰内容更新并降低工作流的可靠性。 此更改可恢复稳定的编辑器状态管理，并确保在受影响的场景中可预见地执行创作操作。 （SITES-34499）

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### 发布项{#sites-launches-65-lts-sp2}

* 站点时间轴在启动项促销活动期间显示硬编码英语文本：“在启动项促销活动之前创建版本……”。 更新将硬编码字符串替换为本地化的消息处理。 时间轴现在显示本地化文本，并使条目与标准AEM本地化行为保持一致。 （SITES-39157）
* 当作者使用提升当前页面和子页面提升子部分时，启动项提升作用域已偏移。 AEM还会提升不相关的页面，并引起意外的实时网站修改。 此修复程序更正了Launch作用域的计算，因此仅提升所选的子树。 （SITES-38315）
* 启动项中的内容片段未参与`damAssetLucene`索引，搜索结果和查询效率有限。 此更改将Launch内容片段路径添加到索引定义。 搜索和自定义查询现在可在`/content/launches`下找到内容片段。 （SITES-35634）
* 启动项UI显示了内容片段启动项控件，即使产品未在触屏UI中公开内容片段启动项也是如此。 此更改会从cq-launches-content中剥离内容片段启动代码路径，并调整Launch列表筛选。 作者现在可以看到一致的页面启动选项，但没有内容片段启动条目。 （SITES-35633）
* AEM 6.5 LTS快速入门缺少所需的启动包和先决条件，这会阻止启动项OpenAPI启用。 该更新添加启动项包和所需的依赖项，例如量度支持、DAM-cfm更新和队列配置。 现在可在6.5 LTS快速启动上运行、且包含所需运行时组件的启动项API。 （SITES-35297）
* CF Launches打包提取了较新的依赖项版本和不必要的GraphQL库，这会使AEM 6.5 LTS集成复杂化。 此更改使依赖项版本与AEM 6.5 LTS基线保持一致，并剥离未使用的GraphQL依赖项。 包分辨率现在保持不变，并且CF Launch启动保持稳定。 （SITES-35295）
* AEM Launch现在为6.5 LTS分支运行专用的Jenkins管道。 管道每夜运行一次，以生成并通过电子邮件发送故障警报。 该设置增加了测试覆盖率并提前捕获回归。 （SITES-35293）
* AEM 6.5 LTS现在发布了更新的Launches API捆绑包，其中包含已调整的人工因素版本。 该捆绑包将跟踪主代码行，同时保留正确的6.5 LTS发行版本。 此更新稳定了6.5 LTS栈栈中的Launches API消耗。 （SITES-35292）
* AEM 6.5 LTS现在包含一个更新的launches-core捆绑包，该捆绑包具有对齐的依赖项版本。 此更新添加了“片段UUID”和“引用UUID”数据类型的启动项核心处理。 现在，启动项处理可保持启动项和内容片段工作流之间的行为一致。 （SITES-35290）
* 改进了站点编辑器，以解决中断正常页面创作工作流的不一致行为。 作者遇到意外的组件交互，这会干扰内容更新并降低编辑可靠性。 此更改可恢复一致的UI状态管理，并确保在受影响的场景中可预见地执行创作操作。 （SITES-35138）
* Launches Edit现在显示本地化的错误文本，而不是硬编码的`Provided path is not a launch`字符串。 现在，当Edit收到无效的启动路径时，UI会呈现跨语言的翻译消息传递。 （SITES-33360）
* AEM 6.5 LTS现在包括启动项OpenAPI侧端口工作。 此更新将启动项API包、内容包和所需的快速启动工件引入奇偶校验，并支持具有稳定CI验证的内容片段启动项OpenAPI方案。 （SITES-32050）
* 启动项UI现在会本地化覆盖的模板标签。 模板覆盖详细信息现在显示已翻译文本而非仅英文字符串。 （SITES-29525）
* AEM解决了&#x200B;**站点** > **启动项** > **编辑**&#x200B;中缺少本地化键的问题。 用户现在会看到已翻译的错误消息，而不是原始“无法更新启动项源列表”字符串。 （SITES-21499）
* 启动项提升UI现在显示本地化的状态标签和操作。 预览区域显示&#x200B;**已删除**、**新建**&#x200B;和&#x200B;**视图**&#x200B;的已翻译文本，而不是原始英文字符串。 （SITES-13540）
* 现在，创建启动项时会显示本地化的错误消息。 UI不再显示原始英文字符串，如`Unable to create launch page`、`Source root resource is not a page`或`Mandatory parameter is missing`。 （SITES-13085）


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - 实时副本{#sites-msm-live-copies-65-lts-sp2}

* 在内容更改期间，管理员对MSM推送修改处理的可见性有限。 此修复添加有关MSM事件接收和转出执行的详细日志记录。 Debug输出现在显示触发了哪些事件、更改了哪些内容路径以及谁触发了更改。 （SITES-38029）
* AEM修复了Blueprint转出日期字段上的本地化布局问题。 日期提示现在符合控件并且在支持的语言（包括`fr_FR`）中保持可读性。 （SITES-14961）

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### 复制{#sites-replication-65-lts-sp2}

页面编辑器发布现在可处理包含选择器或后缀的URL。 发布的请求现在会发送JCR页面路径，而不是选择器或后缀URL字符串，因此激活会完成，内容会启用。 复制现在会在失败时返回错误状态，从而阻止出现误的“发布已启动”消息。 （NPR-43288）

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### 模板编辑器{#sites-template-editor-65-lts-sp2}

对于某些区域设置，模板状态文本垂直显示在&#x200B;**工具** > **常规** > **模板**&#x200B;中。 “已过时”标签破坏了布局，读为一列字符。 该修复程序会更正模板状态样式，以使标签在单个水平线上呈现。 （SITES-36797）

#### 通用编辑器 {#sites-universal-editor-65-lts-sp2}

* 已将OSGi默认配置设置为`preview=true`，并强制通用编辑器在预览模式下启动。 此更新更正默认值并恢复标准的生产条目行为。 除非管理员明确启用预览模式，否则通用编辑器现在会在生产模式下打开。 （SITES-37193）
* 在开发和暂存环境中，“通用编辑器打开”命令现在默认为预览模式。 该命令会添加preview=true，这样可保持作者检查与预览上下文一致，并避免意外打开生产环境。 （SITES-33839）

### [!DNL Assets]{#assets-65-lts-sp2}

Assets Relate现在适用于包含空格的文件名。 更新的“关系”客户端逻辑现在可以正确处理包含空间的路径，并避免在关系选择期间出现`undefined`源错误。 现在将打开“关系”对话框并保存关系，而不使用UI挂起或旋转器。 DAM用户无需重命名文件即可关联、派生和取消关联资源。 (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 新的Dynamic Media视频播放器集成（限量推出） — 现在，AEM 6.6快速入门中提供了新的Dynamic Media视频播放器体验。 此增强功能目前仅作为受控转出的一部分为初始客户启用。 (Assets-60165)
* 解决了视频属性对话框中的选择缩略图选项未打开资产选取器的问题，恢复了用户为视频资产选择自定义缩略图的功能。 (Assets-58926)
* 在Dynamic Media视频中，增加了在“字幕和音轨语言”下拉列表中选择阿拉伯语的支持，使作者能够直接在AEM中管理阿拉伯语字幕。 (Assets-61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->


<!--
### [!DNL Forms]{#forms-65-lts-sp2}

#### Forms Designer

#### Forms

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

* Sling资源访问安全现在在1.1.2版上运行。当多个ResourceAccessGateHandler服务注册时，ResourceAccessSecurityImpl在初始化期间不再引发ClassCastException。 初始化现在可以可靠完成，并避免在具有多个处理程序的环境中启动失败。 （NPR-42750）
* JMX控制台和Web控制台现在为控制台CSS资源发送`Content-Type: text/css header`。 严格的MIME检查不再阻止样式表加载，因此`/system/console/jmx` UI将以正常样式呈现。 (GRANITE-63677)
* AEM现在可避免在生成的`contributor`中为`WEB-INF/resources/provisioning/model.txt`组输入重复的ACL条目。 WAR输出现在包含一个一致的ACL块，以防止在查看期间混淆权限差异。 (GRANITE-63269)
* 在捆绑刷新操作期间，AEM列入阻止列表 列入允许列表不再清除反序列化防火墙和设置。 更新了筛选器注册逻辑，使活动防火墙实例与保存的配置保持一致，因此无需重新启动即可保持启用保护状态。 (GRANITE-61382)
* Felix Web控制台在访问`NullPointerException`期间不再引发间歇性`/system/console`错误。 更新了ServiceTracker处理，防止出现null跟踪器状态。 在重复请求和自动验证期间，控制台登录和导航保持稳定。 (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

升级Service Pack后打开JSP文件时，CRXDE Lite不再显示空白选项卡。 AEM现在提供了匹配的CodeMirror核心和附加代码，可防止严重的浏览器错误并保持编辑器可用。 (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

表达式安全验证器现在处理空或null OSGi配置值。 它应用安全默认值，忽略空数组，并记录清晰的日志，从而防止NullPointerException和不可预测的验证结果。 （NPR-43163）

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 集成{#foundation-integrations-65-lts-sp2}

现在，即使存在开始和结束日期，AEM也会同步Adobe Target活动。 Target有效负载现在将活动日期格式化为完整的ISO 8601时间戳，包括秒、毫秒和时区。 Target不再拒绝具有`InvalidJson.Json`的请求。 计划的活动现在会迁移到同步状态，而不是保持不同步。 （CQ-4360733）

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 



#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS Service Pack 2需要S3 Connector 1.60.10或更高版本。 S3数据存储配置现在包括`crossRegionAccess`和`mode`，因此管理员可以启用跨区域存储段访问并在需要时将存储切换到GCP。 `s3EndPoint`现在需要与`s3Region`对齐的区域，或者它保持为空以便驱动程序生成终结点。 (GRANITE-64873)


#### 快速入门{#foundation-quickstart-65-lts-sp2}

* Sling更新了管理登录允许列表，以使用包含术语和新的配置PID。 此更改与Sling JCR Base 3.2.0一致。 (GRANITE-63756)

  **影响**

   * Sling弃用这些PID，您应该从配置中删除它们：
      * 工厂PID： `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * 全局PID： `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
这些旧配置使用属性，如`whitelist.name`和`whitelist.bundles`。

   * Sling仍为已弃用的PID提供部分向后兼容性，但不要将其用于新配置。 请改用较新的`LoginAdminAllowList.*` PID。
   * 不要同时运行已弃用和新的列入允许列表配置。 混合配置可能会产生歧义并产生意外行为。 迁移到AEM 6.5 LTS SP2时，请完全删除已弃用的PID。

  **您应该做什么**

   1. 查找使用`LoginAdminWhitelist*` PID的允许列表配置。
   1. 将它们替换为相应的新PID：

      * 工厂PID： `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * 全局PID： `org.apache.sling.jcr.base.LoginAdminAllowList`

      列入允许列表有关其他详细信息，请参阅[管理登录的已弃用包](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login)。

* AEM 6.5 LTS SP2将更新Sling、Oak和Felix的基础层捆绑包集。 这些升级增强了核心运行时的稳定性，并在整个平台上调整依赖项版本。 (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311) -->

#### Sling{#foundation-sling-65-lts-sp2}

AEM现在包括Sling Engine 2.16.6。此更改消除了安全工具标记的XSS违规，并提高了核心渲染的安全性和稳定性。 （NPR-43105）

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

由于XLIFF格式问题，AEM翻译在Java 17或Java 21上不再失败。 导出管道现在可生成翻译提供商接受的符合标准的XLIFF。 此更改将删除翻译作业中断，并恢复AEM和翻译服务之间的可预测切换。 现在，翻译工作流在受支持的Java运行时保持稳定。 （CQ-4360217）

#### 工作流{#foundation-workflow-65-lts-sp2}

在工作流通知处理期间，EmailNotificationService-Processor不再触发重复的“未找到区段”错误。 更新的异常处理检测到SegmentNotFoundException并停止处理循环，而不是继续无效读取。 在收件箱和工作项访问期间，工作流执行保持稳定，并记录噪音下降。 (GRANITE-62635)




## 关于 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 的平台的构建基础是更新版本的基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java™ 内容存储库：Apache Jackrabbit Oak 1.68.x。

Eclipse Jetty 11.0.x 被用作快速入门的 servlet 引擎。

### Java™ 支持  {#java-support}

* 支持 Java™ 17 和 Java™ 21。
* 为了获得最佳性能，请用其他值覆盖默认 GC 值。有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* 如果 Oracle 未公开提供，Adobe 会分配 Java™ 17 和 Java™ 21 维护更新，以便客户在 AEM 相关项目中使用。

### Uberjar 包装 {#uber-jar-packaging}

* AEM 6.5 LTS 的 Uberjar 包装略有不同。有关详细信息，请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升级 {#upgrade}

* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 有关详细的升级说明，请参阅JEE上的[AEM Forms 6.5 LTS SP1升级指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### AEM 6.5 LTS 服务包升级最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**环境**
适用于：安装Service Pack 2 (SP2)的AEM 6.5 LTS（内部部署）客户。 SP2作为快速入门JAR提供。

**为什么这很重要**
适用于AEM 6.5 LTS的SP2以快速入门JAR的形式提供，而不是以通过包管理器安装的ZIP形式提供。 内部部署客户可通过替换 Quickstart JAR、解压并重新启动的方式进行升级。此方法与 Adobe 的就地升级流程保持一致。

**推荐的升级流程（创作或发布实例）**

1. 验证您的AEM 6.5 LTS实例是否健康且可访问。
1. 从Software Distribution下载快速入门JAR（例如，`cq-quickstart-6.6.x.jar`）。
1. 停止正在运行的实例。
1. 在AEM安装目录（`crx-quickstart/`外部）中，将以前的快速入门JAR替换为SP2 JAR。
1. 解压该 JAR 文件：

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   （根据需要调整堆标志。）

1. 将解压后的 JAR 重命名以匹配对应角色和端口，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 启动 AEM，并在用户界面（“帮助”>“关于”）及日志中确认升级是否成功。

**良好维护规范**

* 在生产环境升级前，先在较低环境或测试环境中执行升级操作。
* 在开始之前，请先进行完整、可恢复的备份（存储库以及任何外部数据存储）。
* 查看 Adobe 的就地升级指南及技术要求（LTS 建议使用 Java 17 或 21）。

>[!NOTE]
>
>上面显示的文件名（例如，`cq-quickstart-6.6.x.jar`）反映了为此LTS发行版观察到的快速入门工件命名；始终使用您从Software Distribution下载的确切文件名。

## 安装和更新{#install-update}

有关设置要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 如果您从旧的6.5 SP直接升级到LTS SP1，请按照6.5到6.5 LTS GA [升级](/help/sites-deploying/upgrade.md)的说明操作。


有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 新安装 AEM 6.5 LTS 时，必须单独安装索引定义。更多详细信息请参阅[这篇文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 安装并更新 AEM Forms 附加组件 {#install-update-aem-forms-add-on}

有关详细说明，请参阅[执行就地升级](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。


## 支持的平台 {#supported-platforms}

查找受支持平台的完整表格，包括对 [AEM 6.5 LTS 技术要求](/help/sites-deploying/technical-requirements.md)的支持等级。

>[!NOTE]
>
>建议与 AEM 6.5 LTS 一起使用 Java™ 17/Java™ 21 版本。


## 已弃用和已删除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe不断检讨和改进产品功能，以通过使旧功能现代化或替换旧功能而为客户提供更大的价值。 实施这些更改时会仔细考虑向后兼容性。

为了确保透明度并允许进行充分的规划，Adobe将遵循Adobe Experience Manager (AEM)的弃用流程：

* 首先宣布弃用。 已弃用的功能仍然可用，但不再增强。
* 删除不会早于下一个主要版本。 计划的删除时间表单独通知。
* 在功能被移除之前，至少会为客户提供一个发布周期以过渡到受支持的替代方案。

### 已弃用的功能  {#deprecated-features}

本节列出了 Adobe 在 AEM 6.5 LTS 中已弃用的功能。通常情况下，Adobe 在未来版本中移除某些功能之前，会先弃用这些功能并提供替代方案。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，使用所提供的替代功能更改自己的实施。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
| 快速入门 | Mongo API | Mongo API现已弃用，并计划在未来版本中删除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API中的内容片段支持 | AEM 6.5 LTS SP2为内容片段和模型管理提供了现代化的OpenAPI，因此现已弃用AEM Assets REST API中的旧版内容片段支持端点。<br>Adobe打算在生命周期结束公告之前保持这些旧端点可用。 Adobe不计划为已弃用的端点提供进一步的增强功能。 | 6.5 LTS SP2 |
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 管理 AEM 中的 Headless 内容时首选以下编辑器：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。 | 6.5 LTS GA |
| [!DNL Foundation] | 支持 com.adobe.granite.oauth.server | Adobe IMS 集成 |  |

### 已移除的功能  {#removed-features}

此部分列出了 AEM 6.5 LTS 中已移除的功能。之前的版本中已将这些功能标记为已弃用。

* 删除了对CRX存储库持久性的RDBMK支持。
* 在群集环境中，MongoMK现在是存储库持久性唯一支持的选项。

| 区域 | 专题 | 替换 | 版本（SP） |
| --- | --- | --- | --- |
| Commerce | 不支持 AEM CIF Classic。 | 迁移到 [AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解决方案 | 不支持社交/Communities。 | 没有替代功能可用。 | 6.5 LTS GA |
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

### 为Sites Headless API安装所需的Oak索引{#site-headless-api}

一些迁移到Sites Headless的API需要额外的Oak索引才能实现完整功能。

安装`cq-dam-cfm-indices`包以使用下列功能：

* 列出内容片段模型
* 列出内容片段
* 搜索API
* 工作流

从Adobe软件分发门户下载索引包[cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)。

### 在使用仅 SSL 功能的情况下，Dispatcher 连接失败（已在 AEM 6.5 LTS SP1 及更高版本中修复）{#ssl-only-feature}

>[!NOTE]
>
> 此问题仅出现在 AEM 6.5 LTS GA 版本中。

在 AEM 部署中启用仅 SSL 功能后，会发生一个影响 Dispatcher 与 AEM 实例之间连接的已知问题。启用此功能后，健康检查可能会失败，并且 Dispatcher 和 AEM 实例之间的通信可能会中断。尤其是当客户尝试通过 `https + IP` 将 Dispatcher 与 AEM 实例连接时，会出现此问题。它与 SNI（服务器名称指示）验证问题有关。

**影响**

* 健康检查失败，出现 HTTP 400 响应码
* Dispatcher 与 AEM 实例之间的通信中断
* 无法通过 Dispatcher 正确提供内容
* 使用 HTTPS 与 Dispatcher 配置中的 IP 地址时连接失败
* 通过 HTTPS + IP 连接时出现 HTTP 400“SNI 无效”的错误

**受影响的环境**

* 具有 Dispatcher 配置的 AEM 部署
* 启用了仅 SSL 功能的系统
* 使用 `https + IP` 方法与 AEM 实例连接的 Dispatcher 配置

**解决方案**

如果您遇到此问题，请联系Adobe客户支持。 有一个热修复 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 可以解决这个问题。采用必要的热修复之前，不要尝试启用仅 SSL 功能。

## 包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此 [!DNL Experience Manager] 6.5 LTS 服务包 1 发行版本中包含的 OSGi 捆绑包和内容包：

* [Experience Manager 6.5 LTS 服务包 1](/help/release-notes/assets/65lts_sp1_bundles.txt) 中包含的 OSGi 捆绑包列表 <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS 服务包 1](/help/release-notes/assets/65lts_sp1_packages.txt) 中包含的内容包列表 <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站仅向客户开放。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [在 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

