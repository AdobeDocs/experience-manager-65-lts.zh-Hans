---
title: Adobe Experience Manager 6.5 LTS SP1的最新发行说明
description: 查找 Adobe Experience Manager 6.5 LTS 服务包 1 的当前版本信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 516fb71493cad9d4f4105bb09f56fe95d2971974
workflow-type: tm+mt
source-wordcount: '7204'
ht-degree: 14%

---

# Adobe Experience Manager 6.5 LTS SP1的最新发行说明 {#release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 1 (SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2025年8月28日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS SP1中包括的内容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP1包括新增功能、客户请求的关键增强功能和错误修复。 此外，还包括自2025年3月推出6.5 LTS以来发布的性能、稳定性和安全性改进。 在6.5 LTS上[安装此Service Pack](#install-update)。

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 修复了6.5 LTS Service Pack 1中的问题 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 辅助功能 {#sites-accessibility-65-lts-sp1}

* 修复了内容片段中的文本编辑器元素默认被截断的问题。 文本编辑器现在显示完整内容而不截断。 (SITES-33005)
* 修复了单击URL路径会打开Indigo的主页而不是正确的目标URL的问题。 (SITES-33004)
* 修复了自定义AEM组件中在自动测试期间导致ADA合规性失败的可访问性问题。 (SITES-30660)
* 通过确保文本以黑色浅色背景显示并符合WCAG 2.0对比度要求，修复了“警报”对话框和“工作流消息”中的ADA合规性问题。 (SITES-30138)
* 修复了AEM Sites编辑器中的“Category”按钮缺少特定标签而导致的JAWS将其宣告为“Images button menu”而不是提供描述性标签的辅助功能问题。 (SITES-27497)
* 修复了“有效权限”屏幕中的复选标记图标缺少替换文本，从而阻止JAWS阅读和传达其含义的辅助功能问题。 (SITES-27272)
* 修复了以下辅助功能问题：权限页面未提供用于删除用户或组权限的清晰JAWS公告，从而导致屏幕阅读器用户混淆。 (SITES-27238)
* 修复了错误消息仅显示为没有描述性文本的图标从而阻止JAWS在错误发生时宣布错误的辅助功能问题。 (SITES-27155)
* 修复了JAWS在AEM On-Premise环境中读取不正确和不清晰的按钮描述时的辅助功能问题，包括模块部分缺少标题级别2文本。 (SITES-27152)
* 修复了在AEM Assets选项卡中过滤值后，JAWS未公告结果数量的辅助功能问题。 (SITES-27150)
* 修复了创建文件夹时没有显示确认并且JAWS没有在Assets UI中声明该文件夹的辅助功能问题。 (SITES-27141)
* 修复了AEM Sites中的辅助功能问题。 JAWS未公告表单错误，焦点移至非交互式错误元素，并且选项卡退出时无法显示必填字段错误。 (SITES-27138)
* 修复了时间表按钮菜单缺少特定标签导致JAWS只读“活动按钮菜单”而没有提供清晰说明的辅助功能问题。 (SITES-27134)
* 修复了JAWS未公告容器项目的操作或角色的辅助功能问题，该问题仅读取“痕迹导航v1”和“按钮v2”而不是描述性标签。 (SITES-27131)
* 修复了快速发布弹出窗口未提供正确的成功消息从而阻止屏幕阅读器宣布完成反馈的辅助功能问题。 (SITES-26912)
* 修复了coral-column视图中的辅助功能问题，该问题导致具有需要子角色的ARIA角色的元素不包含这些元素，从而不遵守辅助功能标准。 (SITES-26898)
* 修复了辅助功能问题：在“重排”模式下，创建页面顶部导航中的“模板”和“属性”文本不可见，从而阻止键盘和屏幕阅读器用户进行访问。 (SITES-26895)
* 修复了辅助功能问题，该问题导致无法使用键盘导航访问顶部导航中的“搜索”、“解决方案”、“帮助”、“收件箱”和“用户”图标的工具提示。 (SITES-26889)
* 修复了基本选项卡表单字段未提供错误建议从而阻止用户在必填输入字段留空时收到指导的可访问性问题。 (SITES-26885)
* 修复了NVDA和讲述人屏幕阅读器未在创建页面中公告模板文件详细信息，从而导致用户无法以编程方式接收完整信息的辅助功能问题。 (SITES-26884)
* 修复了在“基本”选项卡中对“页面标题文本框”使用错误名称而导致屏幕阅读器无法向用户提供准确信息的辅助功能问题。 (SITES-26879)
* 更新了按钮前景色和背景色以满足WCAG 2.2 AA最低对比度要求，从而提高所有用户的可读性和可访问性。 (SITES-26877)
* 解决了导致创建页面顶部导航中的“模板”和“属性”文本在调整大小后消失的问题，确保弱视用户的可见性和可访问性。 (SITES-26872)
* 修复了在应用“重排”后导致主页上显示多个水平滚动条的问题，确保显示单个滚动条以提供适当的辅助功能和内容可见性。 (SITES-26800)
* 修复了AEM页面编辑器中的辅助功能问题：在激活“角色”、“购物车”或“已放弃”等按钮后，键盘焦点意外地重置为人口统计工具栏的开始。 现在，焦点仍然在激活的按钮上，以支持一致的键盘导航和屏幕阅读器工作流。 (SITES-25306)
* 修复了页面标题和标记字段的辅助功能标签关联问题。 在使用JAWS等屏幕阅读器时，AEM界面现在可以正确地将辅助功能标签与“标题”和“页面标题”字段相关联。 此修复确保正确读取标签，并提高了页面创建、属性和移动工作流中的ADA合规性。 (SITES-27149)
* 修复了时间轴中注释输入字段缺少可视标签的问题。 修复了时间线部分下“评论”输入字段缺少可视标签的问题，从而提高辅助功能。 此更新确保屏幕阅读器可以准确地朗读字段标签。 此体验可增强所有用户（尤其是依赖辅助技术的个人）的表单导航和提交。 (SITES-26903)
* 修复了时间轴注释中省略号按钮的键盘辅助功能。 为时间线部分下的注释旁边的省略号（三个点）按钮启用键盘导航。 用户现在可以使用Tab键访问按钮并与之交互，从而提高依赖仅键盘导航的用户的可访问性。 (SITES-26891)
* 改进了在选择对话框中针对搜索结果的NVDA/讲述人公告。 更新了“打开选择”对话框，以宣布在使用屏幕阅读器（如NVDA或“讲述人”）时是否找到搜索结果。 这项改进可帮助依赖辅助技术的用户了解其搜索操作的结果，而无需视觉确认。 (SITES-26883)
* 更正了评论输入字段旁边的省略号图标的ARIA角色。 更新了评论输入字段旁边的省略号（三个点）图标以使用正确的ARIA角色，确保屏幕阅读器可以准确识别元素。 这项改进增强了辅助功能的合规性，改善了依赖辅助技术的用户的体验。 (SITES-26881)
* 更正了Coral UI组件中的无效ARIA属性。 更新了Coral UI组件以确保所有ARIA属性都使用有效值，从而提高辅助功能合规性。 特别是，解决了错误分配`aria-modal="dialog"`等无效值的情况。 此增强功能使屏幕阅读器能够正确解释对话框元素，从而提高依赖辅助技术的用户的辅助功能。 (SITES-26873)
* 改进了重排方案中图标的可见性和工具提示。 增强了重排行为，以确保为&#x200B;**下载**、**重新处理资源**&#x200B;和&#x200B;**签出**&#x200B;图标正确显示工具提示。 重点关注在调整视区大小或更改浏览器缩放设置时，图标及其标签会变得不可见的辅助功能问题。 此修复程序通过维持可见性并在重排期间提供适当的图标描述，为视力缺佳的用户提供支持。 (SITES-26871)


#### 管理员用户界面{#sites-adminui-65-lts-sp1}

* 修复了JAWS在“创建站点”对话框中未公告列表角色或提供导航和激活说明的辅助功能问题。 (SITES-30661)
* 站点过滤器视图中的屏幕阅读器支持状态消息按预期工作，确保用户在视图之间切换时收到清晰及时的反馈。 (SITES-24992)
* 筛选器边栏中的日期选取器完全显示在其容器中，提供了足够的接触目标大小并消除了剪切问题。 (SITES-24988)
* 现在，选定的过滤器标记使用与可视化演示文稿匹配的语义HTML和aria标签，从而确保对辅助型技术的准确角色支持和清晰的操作。 (SITES-24980)
* 在引用边栏区域中添加了aria-label属性，以便为屏幕阅读器用户提供唯一的描述性标签，并确保整个页面具有一致的标志性标识。 (SITES-24973)
* 更新了引用边栏，以使用相对单位进行大小调整和定位，使内容能够缩放，并在在1280x1024视区缩放到400%时保持完全可用。 (SITES-24972)
* 站点主页列表视图中已确认的表元素包含适当的列标题角色，使屏幕阅读器能够朗读每个数据单元格的标题。 (SITES-24942)
* NVDA现在会在树目录中公布修改日期，以确保屏幕阅读器用户收到完整的资产详细信息。 (SITES-24782)
* 修复了NVDA屏幕阅读器在AEM Sites的树目录组件中宣布项目文本不完整的问题。 NVDA现在会读取每个项目的全文，从而提高可访问性和合规性。 (SITES-24780)
* 向“树目录”中的“窗口分隔器”添加了键盘辅助功能，使用户能够仅使用键盘调整左侧栏的大小。 (SITES-24779)
* 更新了“帮助”菜单搜索结果，以包含列表项正确的ARIA角色，从而确保屏幕阅读器正确宣布链接，以提高辅助功能。 (SITES-24729)
* 修复了屏幕阅读器未公告“X of Y results”状态消息的问题。 或者，在站点过滤器面板中应用过滤器后显示“未找到结果”消息，以确保用户收到正确的结果确认。 (SITES-24720)
* 更正了应用程序导航中导航链接缺少的角色分配。 添加了适当的ARIA角色，以确保屏幕阅读器能够正确识别和朗读导航元素。 (SITES-24719)
* 使用按钮元素替换所选过滤器标记的不正确网格角色标记，并添加可访问的名称，以确保屏幕阅读器正确声明和识别标记。 (SITES-24717)
* 在执行多项选择时，为引用边栏状态消息添加了屏幕阅读器公告，确保用户会收到更改确认。 (SITES-24678)
* 更正了搜索字段行为，以便不会自动宣布第一个结果。 屏幕阅读器现在会朗读找到的结果数量，使用户能够在列表中导航而不会产生错误的焦点公告。 (SITES-24658)
* 从列表视图中的非交互静态元素中删除了错误的`aria-label`属性，以防止屏幕阅读器发布误导性或不相关的信息。 (SITES-24515)
* 更新了列表视图第一列中的复选框，以使用标题列文本作为无障碍名称，确保屏幕阅读器准确地传达表单字段的用途。 (SITES-24514)
* 添加了适当的ARIA属性和实时区域支持，以便在内容导航时向屏幕阅读器用户宣布加载状态消息。 (SITES-24481)
* 更新了响应式设计，当视区宽度为1280×1024且内容缩放到400%时，无需水平滚动，从而确保完全可见且无需侧滚动。 (SITES-24308)
* 更正了站点管理员UI中的焦点导航以遵循逻辑顺序，在按Esc后将焦点返回到“全选”按钮，并在按Tab后将焦点移动到下一个交互式元素。 (SITES-24307)
* 更新了站点管理UI中的焦点顺序，以便在键盘导航期间，`<betty-titlebar-title>`元素中的痕迹导航按钮将以正确的顺序接收焦点。 (SITES-24305)
* 已验证跳过链接功能，以确保将键盘焦点移动到主内容区域，从而允许键盘用户绕过标题元素并有效访问内容。 (SITES-24061)


#### 传统用户界面{#sites-classicui-65-lts-sp1}

修复了经典UI中缺少复选框标签，并且HTML在多个UI元素（包括日期搜索和非标准界面）中显示为编码文本的问题。 (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM现在可以防止图像资源中XMP元数据的格式错误导致性能下降。 包含无效或不合规的Assets XMP属性名称（例如具有数值区段或不合格结构的属性名称）在处理期间不再触发重复的警告日志。 系统会过滤掉有问题的元数据，以确保资产摄取和验证已完成，并且没有错误。 (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] — 片段编辑器{#sites-fragments-editor-65-lts-sp1}

其他作者仍可以发布内容片段，即使其他作者签出了它们，这违反了签出功能的预期行为。 此修复可防止其他用户查看或使用签出内容片段时在创作界面中的发布按钮。 (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 组件控制台{#sites-component-console-65-lts-sp1}

修复了产品列表组件中，“全选”复选框仅从初始页面添加了前20个SKU，而不是搜索结果中的所有SKU的问题。 (SITES-29191)

#### 核心后端{#sites-core-backend-65-lts-sp1}

处理`ValidationDataServlet`中的图像资源时，XMP元数据的格式不正确触发了错误。 此修复可确保合规的元数据处理，并避免冗余解析无效属性。 (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM — 活动副本{#sites-msm-live-copies-65-lts-sp1}

* 修复了在AEM 6.5内部部署中重新启用幽灵组件继承时发生的JavaScript错误`ns.ui.alert is not a function`。 (SITES-31993)
* 修复了允许转出“稍后”选项在AEM 6.5中继续而不选择日期的问题。 (SITES-31374)

#### 页面编辑器{#sites-pageeditor-65-lts-sp1}

* 解决了Teaser模式中的一个问题：在有效的数据输入和错误解决后，链接和操作选项卡继续显示错误样式、图标和aria-invalid属性。 (SITES-25527)
* 修复了Teaser模式文本编辑器中的问题：列表和段落按钮无法向屏幕阅读器传达其展开或折叠状态，从而确保准确的aria展开属性更新。 (SITES-25365)
* 修复了人口统计工具栏中的一个问题：通过键盘输入调整购物车滑块可将焦点移动到购物车按钮，而不是保留对滑块的关注，从而提高键盘用户的导航效率。 (SITES-25324)
* 通过为其关联的`<label>`元素分配值，向人口统计工具栏中的购物车滑块添加了可访问的名称。 此修复提高了与辅助技术的兼容性，并增强了屏幕阅读器用户的可用性。 (SITES-25322)
* 向人口统计工具栏下拉列表中的按钮添加了ARIA角色和可访问名称。 此修复通过辅助技术实现了正确识别，并改进了键盘和屏幕阅读器用户的导航功能。 (SITES-25315)
* 已调整人口统计工具栏布局，以防止在浏览器按200%缩放时内容溢出视区，确保所有控件保持可访问状态且不会进行水平滚动。 (SITES-25309)
* 更正了人口统计工具栏中的焦点管理，使键盘焦点始终位于已激活的按钮上，而不是将焦点重置为工具栏的起始位置。 (SITES-25306)
* 按钮标签重叠按设计发挥作用，当具有相似屏幕宽度的模式处于活动状态时，使用工具提示显示标签。 (SITES-25285)
* 注释模式包含一个可见的提交按钮，允许用户提交注释，而无需依赖Esc键或在模式之外单击。 (SITES-25281)
* 注释模式包括一个钢笔图标按钮，允许用户提交注释，提供了一种清晰易用的提交方法。 (SITES-25269)
* 更正了“注释”和“关闭注释”按钮的屏幕阅读器公告，以提供准确、相关的反馈，并删除不相关或令人困惑的信息。 (SITES-25268)
* AEM编辑器页面中的画布部分现在支持完全的键盘辅助功能。 用户只需使用键盘即可激活节标题和编辑按钮，而无需依赖鼠标悬停。 此更新确保符合WCAG 2.1.1并提高跨组件（例如Teaser、图像、轮播、布局、时间扭曲和注释模式）的可用性。 (SITES-25256)
* 删除了轮播模式中宽度为320px的不必要的水平滚动，以确保所有内容都显示在视区中，而无需端对端导航。 (SITES-25254)
* 删除了图像模式中宽度为320px的不必要的水平滚动，以确保所有内容都显示在视区中，而无需侧对侧导航。 (SITES-25244)
* 删除了Teaser模式中宽度为320px的不必要的水平滚动，以确保所有内容都显示在视区中而无需端对端导航。 (SITES-25242)
* 在Teaser模式中为`List`和`Paragraph Format`弹出菜单启用了键盘导航。 此修复允许用户使用箭头键访问和导航这些菜单。 (SITES-25235)
* 更正了“注释”和“关闭注释”按钮的屏幕阅读器公告，以提供与相关操作一致的准确、相关的反馈。 (SITES-25234)
* 改进了Teaser模式中的“帮助”按钮标签，以清晰地描述其用途并为所有用户（包括辅助型技术用户）提供有意义的上下文。 (SITES-25224)
* 通过将标尺度量与屏幕阅读器用户各自的设备相关联，改进了屏幕阅读器用户的模拟器标尺。 此外，将工具提示替换为aria-descripted by元素。 (SITES-24955)
* 未实施任何修复，因为“编辑”按钮按预期工作，并提供信息上下文而不是执行操作。 (SITES-24950)
* 已确认编辑器页面上的焦点顺序遵循逻辑顺序，允许用户浏览所有交互元素，而不会意外跳过或环回。 (SITES-24937)
* 已确认当用户应用自定义文本间距设置时，“预览”模式画布会正确更新文本间距，从而确保所有内容区域的格式一致。 (SITES-24936)
* 已验证的“预览”按钮不再触发焦点中的上下文或状态更改，从而确保用户在页面视图更新之前有意地激活该按钮。 (SITES-24784)
* 向应用程序导航链接添加了正确的ARIA角色分配，使屏幕阅读器能够准确识别并公告导航项目，从而提高辅助功能。 (SITES-24718)
* 更新了更改筛选器按钮以向屏幕阅读器宣布展开和折叠状态，删除了多余的ARIA属性，并调整了标签以提供清晰、非重复的说明。 (SITES-24713)
* 在“链接选择”对话框中添加了搜索结果状态消息的屏幕阅读器公告，以确保用户在结果加载或未找到匹配项时收到确认。 (SITES-24700)
* 添加了有关图像模态加载状态的屏幕阅读器公告，以确保用户在模态加载并准备好交互时收到反馈。 (SITES-24697)
* 解决了粘滞标题在200%和400%缩放下遮住了Teaser模式内容的辅助功能问题，确保在使用页面缩放时完全可见性和可用性。 (SITES-24523)
* 向“搜索/过滤器”字段添加了一条包含搜索结果数的状态消息，使屏幕阅读器可以向用户公告结果。 (SITES-24506)
* 在“搜索/过滤器”字段中添加了有关搜索结果数量的屏幕阅读器公告，以确保用户在加载结果时立即收到反馈。 (SITES-24505)
* 在“侧边栏”面板的选项卡列表中添加了一个辅助功能名称，使屏幕阅读器能够按照WAI-ARIA准则朗读其用途。 (SITES-24492)
* 为不明确的编辑器图标添加了描述性标签，确保所有用户都清楚地了解每个按钮的功能。 (SITES-24480)
* 为“画布”视图中的章节标题和操作按钮启用了完整的键盘辅助功能，确保鼠标和键盘用户操作一致。 (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Universal Editor {#sites-universal-editor-65-lts-sp1}

* 修复了QueryTokenService中的竞争条件，该条件会导致在登录令牌服务返回结果之前触发了查询参数的多个请求时导致错误登录。 (SITES-30659)
* 修复了UniversalEditorURLService中的一个问题：在Felix ConfigMgr中保存映射路径数组时，只保留第一个项目。 (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

修复了将资产从远程DAM同步到站点本地AEM时从资产中删除已发布状态和与复制相关的资产的问题。 (Assets-48958)

<!--
#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp1}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp1}



### [!DNL Forms]{#forms-65-lts-sp1}


#### Forms Designer 

#### Forms

#### Forms JEE 
 
#### Forms Captcha {#forms-captcha-65-lts-sp1} 

#### XMLFM {#forms-xmlfm-65-lts-sp1}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp1}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp1} -->



### 基础 {#foundation-65-lts-sp1}

<!--
#### Apache Felix {#foundation-apachefelix-65-lts-sp1}

#### Campaign{#foundation-campaign-65-lts-sp1}

#### Cloud Services{#foundation-cloudservices-65-lts-sp1}



#### Communities {#foundation-communities-65-lts-sp1}

#### Content distribution{#foundation-content-distribution-65-lts-sp1}

#### CRX {#foundation-crx-65-lts-sp1}

#### Granite{#foundation-granite-65-lts-sp1} -->

#### HTL{#foundatoin-htl-5-lts-sp1}

解决了阻止HTL脚本引擎工厂正常运行的OSGi依赖项循环，确保正确地解析服务和执行脚本。 (Granite-58275)

#### 集成{#foundation-integrations-65-lts-sp1}

* 已从`com.adobe.cq.cq-analytics-integration`捆绑包中删除commons-httpclient 3.x的用法，并将其替换为`org.apache.httpcomponents.httpclient` 4.5.13.B0001，以符合最新的AEM 6.5 LTS标准。 (CQ-4360586)
* 从AEM中删除了已弃用的Search&amp;Promote集成捆绑包，从而消除未使用的组件并减少维护开销。 (CQ-4358030)
* 为SiteCatalyst集成添加了新的后端测试案例，以改进分析验证并确保更全面的覆盖范围。 (CQ-4359991)
* 修复了Launch配置的Properties部分中未显示Company和Property下拉列表的问题。 此外，尽管填写了所有必填字段，“保存并关闭”仍会触发错误，并且当只有“标题”字段为空时，为公司和属性显示的错误消息不正确。 (CQ-4359853)
* 已从版本6.6中删除`searchpromote` servlet路径条目，以与删除Search&amp;Promote捆绑包保持一致。 (CQ-4359523)
* 修复了Target存储库的HTTP测试案例，以确保准确验证并提高测试可靠性。 (CQ-4359022)
* 从integration-adobeims-console模块中删除了Guava缓存用法，以消除Guava库依赖项。 (CQ-4358710)
* 已验证AEM 6.6中的DTM集成工作流程、收件箱任务和项目功能，以确保AEM 6.5可正常运行。 (CQ-4358151)
* 已验证AEM 6.6中的内容Insight功能，以确保AEM 6.5中的兼容性和可正常操作。 (CQ-4357774)
* 验证了AEM 6.6中的云服务功能，以确保在AEM 6.5中兼容并正确运行。 (CQ-4357773)
* 已验证AEM 6.6中的Adobe IMS控制台集成，以确保AEM 6.5兼容并正常运行。 (CQ-4357772)
* 更新了Jenkins管道，以便Test&amp;Target集成在Java 17上运行，解决失败的Selenium测试，将选定的测试移到Playwright，并确保所有单元测试都通过。 (CQ-4357770)
* 通过更新生成和测试管道，使DX集成、工作流、收件箱和项目与6.6.0分支保持一致。 此外，解决升级兼容性问题，并验证所有受影响的服务的稳定性和功能。 (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 本地化{#foundation-localization-65-lts-sp1}

* 将“删除访问控制”对话框中的字符串从“权限”列表中本地化，以显示正确的翻译。 (GRANITE-59427)
* 修复了模型编辑器的“或拆分属性”的“添加规则”对话框中，多个UI字符串（包括运算符和字段标签）显示为未本地化的问题。 现在，所有字符串均以正确的本地化方式显示。 (CQ-4354014)
* 在“工作流模型编辑”对话框中为“显示描述”工具提示添加了缺少的翻译。 (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

解决了在升级期间AEM在`/apps/system/config`下重新创建或重命名现有配置文件的问题，将`.cfg.json`文件替换为`.config`文件。 (GRANITE-58899)

#### 全能搜索{#foundation-omnisearch-65-lts-sp1}

修复了占位符错误地显示为输入字段标签的辅助功能问题。 此问题导致搜索、AEM体验片段、内容片段和内容片段模型中缺少字段标签。 (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 项目{#foundation-projects-65-lts-sp1}

* 解决了在日历视图中删除项目时，尽管成功删除了项目，但显示错误弹出窗口的问题。 (CQ-4358890)
* 修复了Firefox中的一个问题：项目视图中的“资产收藏集”卡页脚与卡边框重叠。 现在，页脚正确对齐，没有重叠。 (CQ-4353317)

#### 快速入门{#foundation-quickstart-65-lts-sp1}

* 列入阻止列表更新了uninstall脚本以调整Guava捆绑包的版本范围，从而防止在通过Package Manager安装捆绑包时对其进行安装。 (GRANITE-59559)
* 通过更正界面中经典复选框的处理，修复了在编辑复制代理时复制UI中显示错误(`#1660`)的问题。 (GRANITE-58302)
* 通过解决缺少的服务权限问题、更新配置处理和确保所需的服务正确初始化，解决了运行带有JDK 21的AEM 6.5 LTS时S3数据存储区的多个启动错误。 (GRANITE-57082)
* 定义了AEM 6.5的维护和维护策略。此修复包括以下内容：
   * Service Pack频率。
   * 修补程序频率。
   * 与AEM 6.6并行支持。
   * 更新了支持列表。
   * 附加所有权责任。 (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 已将Sling ResourceAccessSecurity更新到版本1.1.2，以解决在初始化`ClassCastException`的多个`ResourceAccessGate`引用时发生的`ResourceAccessSecurityImpl`。 (NPR-42750)
* 修复了Adobe Stock集成中“许可证”对话框显示为灰色的问题。 此问题是由于`sunt:initList`函数删除了必需的输入字段所致。 该函数可在Coral Foundation客户端库中找到。 更新了客户端库以保留必要的字段，从而启用适当的许可证对话框功能。 (NPR-42748)
* 对导致包安装期间出现`DataTimeParseException`和`String.length()`空指针异常的Sling脚本问题修复了反向移植。 已将Sling脚本更新到版本2.8.3-1.0.10.6，以减少安装错误并提高稳定性。 (NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### 用户界面{#foundation-ui-65-lts-sp1}

* 解决了AEM创作UI中将用户组显示限制为41个的问题。 此问题是由于Granite UI组选取器组件中的默认批次限制造成的。 更新了组件以显示所有组而不截断。 (NPR-42749)
* 解决了在编辑页面属性时，本地页面创建向导中多字段组件中的必填字段未重新验证的问题。 此问题反过来又允许作者绕过验证并继续处理不完整的数据。 (GRANITE-58826)
* 更正了AEM中帮助按钮的ARIA属性，以确保JAWS屏幕阅读器朗读出一个清晰、用户友好的标签，而不是显示未翻译的图标和文本元数据。 (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 通过更新翻译包、验证Java包兼容性、删除已弃用的依赖项以及通过全面测试确保完整功能，增加了对AEM翻译的Java 17支持。 (CQ-4357525)
* 已删除不稳定的常绿测试`com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater`，以防止在自动测试期间出现错误失败。 (CQ-4298376)

#### 工作流{#foundation-workflow-65-lts-sp1}

* 在收件箱项目中添加了`data-detailsurl`缺失属性，以防止在将AEM 6.5 LTS与Java 21结合使用时，未定义的值显示在URL中。 (GRANITE-60158)
* 修复了使用Java 21运行AEM 6.5 LTS时`deactivate`捆绑包的`WorkflowToPublishEventService`方法中的NullPointerException，确保正常关闭工作流服务且没有错误。 (GRANITE-58151)
* 更新了工作流索引以支持共享、外出自定义和解决时间线查询问题。 (GRANITE-52640)
* 更新了工作流索引以支持共享、“不在办公室”自定义功能以及时间线查询问题的解决。 (GRANITE-52294)
* 解决了在程序升级到AEM发行版10912的日志比较验证期间增加的错误日志失败情况，确保稳定的工作流执行。 (GRANITE-44268)
* 更新了工作流存储库中的URL清理方法以将`url.searchParams`替换为`url.search`，从而改进了针对易受攻击URL的XSS保护。 (CQ-4359585)
* 已在AEM 6.6 Forms中验证工作流程、收件箱和项目功能，以确保正确操作和集成。 (CQ-4358777)
* 实现了通过Jenkins发布工作流内容工件的自动化，从而在AEM 6.5中实现了简化且一致的部署流程。 (CQ-4358472)
* 修复了在“收件箱创建任务”工作流中，“添加任务”对话框在单击提交后未关闭（尽管正在创建任务）的问题，原因是JavaScript语法错误。 (CQ-4355336)
* 修复了由于`isEndUserConfigurationEnabled`缺少属性定义而阻止保存收件箱视图配置的问题。 (CQ-4287757)

## Forms

### 表单设计器

* 当用户使用exportDataAPI导出基于XFA的PDF的数据时，生成的XML与使用Acrobat Reader手动导出的XML数据相比，显示差异。 与Acrobat Reader生成的输出相比，输出中缺少某些字段的值。 (LC-3922791)
* 在Workbench中使用“输出服务”生成带标记的PDF时，会在目录项的引用标记下添加一个意外的标签标记。 (LC-3922756)
* 使用输出服务将动态的、可填充的PDF拼合为PDF/A格式时，不保留动态状态。 这会导致数据丢失和潜在的合规性问题，尤其是在启用标记的情况下。 (LC-3922708)
* 当用户在AEM Forms Designer中对齐字段字幕且对其底部或右侧对齐时，标记树仅包含字幕而不包含相应的值，从而导致辅助功能标记不完整。 (LC-3922619)
* 生成的PDF中的二维码变得无法读取。 二维码的替换文本也无法通过辅助功能测试，从而影响屏幕阅读器兼容性。 (LC-3922551)
* 当用户在Agent UI中渲染信件时，由于FormService render() API，内容无法正确显示。 (LC-3922461)
* 当用户尝试从AEM Forms中具有下沉方形样式的XDP创建PDF/A文件时，会导致边框渲染问题。 (LC-3922180)
* 将绑定到XSD架构的动态表单扁平化会导致部分数据丢失，因为最终的PDF中不会保留某些绑定表单数据。 (LC-3922008)
* 当用户尝试使用AEM Forms 6.5.13及更高版本中的extractData API从交互式PDF导出数据时，与手动导出相比，这会导致数据缺失。 (LC-3921983)
* 用户面临一个辅助功能合规性问题：使用AEM Forms Designer或输出服务将XDP表单转换为静态PDF而不是创建单个统一链接标记时，会创建多个Link-OBJR标记。 (LC-3921977)

### 自适应表单

* 在AEM Forms中，在根面板上启用“允许标题使用富文本”会导致嵌套面板上的“从记录文档排除标题”错误地隐藏根面板的标题。 它会在生成的记录文档中进行此操作。 (FORMS-19696)
* 系统忽略通过JSON架构中的aem:resourceType分配的自定义sling:afProperties。 在渲染期间忽略自定义资源类型。 (FORMS-19691)
* 当用户使用URI提交带有预填充附件的自适应表单时，由于缺少二进制数据，表单提交失败并出现NullPointerException。 (FORMS-19371) (FORMS-19486)
* 当用户在“Forms和文档”部分下上传PDF时，时间轴功能停止运行。 (FORMS-19407)(FORMS-19234)
* 当用户使用AEM Forms中的现成(OOTB)文件附件组件上传文件时，会识别安全漏洞。 这个问题可能导致未经授权的实体拦截提交流程。 (FORMS-19271)
* 当用户在AEM Forms中配置现成的自适应表单以自动生成记录文档(DoR)时，Acrobat Reader文档属性中的“标题”字段不显示捕获的DoR标题。 默认情况下，表单标题不会代替文件名出现。 (FORMS-19263)
* 当用户在Agent UI中打开交互式通信时，无法完全擦除预填充的数据；移除后，它将自动使用相同的数据重新填充。 (FORMS-19151)
* 当用户在Agent UI中预览日期字段时，日期意外变化。 出现此问题的原因是VM的UTC设置与系统对日期的解释之间存在时区差异。 (FORMS-19115)
* 当用户提交表单时，文件附件可能会重复，从而导致同一文件被多次上传。 (FORMS-19045)(FORMS-19051)
* 在Document Security中将协调员添加到策略集在生产环境和较低环境中均失败。 (FORMS-18603、FORMS-18212、FORMS-19697)
* 当用户使用空字段在桌面模式下单击“日期选取器 — 日历 — 图标”时，由于未定义的_$focusedDate变量将发生错误，并会中断关联的自定义脚本。 (FORMS-18483)(FORMS-18268)
* 当客户预览信件时，“字数金额”字段无法正确显示或更新数字值，导致对齐错误和内容中缺少空格。 (FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004)
* 当客户在RHEL上预览保存的书信时，内容未对齐，缺少空格，并出现意外字符，如“x”。 (FORMS-18422)(FORMS-17641)
* 当用户在AEM Forms中的选项卡之间导航时，在第一个选项卡上选择组件会变得无响应。 (FORMS-18345)
* 当用户使用WebToPDF选项将HTML文件转换为PDF时，输出PDF缺少标题部分，包括元数据和标题标记。 (FORMS-18223、FORMS-17835、FORMS-19642、FORMS-18224)
* 在AEM JEE Process Manager SDK中，当用户调用retryAction(long actionOid)方法时，系统会错误地重试tb_action_instance表中找到的第一个操作。 即使提供了特定的操作ID或ID为空，也会发生此工作流，从而导致意外行为。 (FORMS-18187)
* 用户遇到问题，即保存的草稿和提交功能失败但未显示任何错误消息。 (FORMS-18069)
* 从基于XSD的基础组件转换为核心组件会阻止在JSON架构中实施跨文件引用，从而影响自适应Forms迁移。 (FORMS-18065)
* 当用户在代理UI中预览信件时，由于IC时间转换问题，日期字段显示不正确的值。 这些差异源于VM环境与系统对时间的解释（UTC与本地时间）之间的时区差异。 (FORMS-17988) (FORMS-17248)
* 当用户在AEM Forms中使用通知IC模板预览信件时，PDF的生成时间存在显着差异，从1.5秒到超过10秒不等，即使是在同一服务器上。 这种不一致性会影响业务关键型工作流。 (FORMS-17951)
* 当用户使用“数据源”选项将自适应表单中的涂写签名对象绑定到XDP时，无法保存更改。 原因在于，即使使用有效值，仍存在长宽比验证错误。 (FORMS-17587)
* 当用户使用具有用于文档片段的许多隐藏字段的特定XDP时，AEM会创建CRX节点，并将cm:optional属性设置为false，从而导致交互式通信(IC)提交失败。 (FORMS-17538)
* 当客户预览信件时，如果定义了商机和Frac的数字限制，则数字框字段无法正确处理负值。 此问题因使用parseFloat而发生，它将减号视为数字的一部分。 (FORMS-17451)
* 预览信件时，注意到Adobe.json文件中使用了“*”通配符，这引起了对其用途和潜在修改的关注。 (FORMS-17317)
* 当用户在“申请固定费率储蓄者”联合帐户上使用屏幕阅读器时，标题被错误地宣布为可点击，导致辅助功能问题。 (FORMS-17038)
* 嵌入表单时，生成的iframe缺少title属性，从而导致出现辅助功能合规性问题。 (FORMS-17010)
* 使用Forms Manager UI下载表单时，始终包含关联的依赖项，例如主题和片段。 (FORMS-15811)
* 当用户访问移动设备上的表单(iOS和Android™)时，第一页上的“下一个”和“上一个”按钮被禁用。 但是，屏幕阅读器不会将其标识为已禁用。 (FORMS-15773)
* 当用户保存启用了片段和延迟加载的大型表单时，无法检索草稿，并中断工作流。 (FORMS-19890和FORMS-19808)
* 用户在基于核心组件的自适应表单中保存表单属性时遇到问题。 出现此情况是因为包含了来自基于基础组件编辑器的自适应表单的冗余脚本，这将导致基于核心组件的自适应表单中出现冲突。 编辑者。 (FORMS-17474)
* 用户遇到了Adobe Sign GovCloud签名页面无法在iframe中呈现的问题。 (FORMS-16803)
* 用户在为核心组件自适应Forms (AF)片段选择引用时遇到错误。 出现错误消息“无法渲染引用：不是绝对路径”，阻止正确渲染引用。 (FORMS-19678)
* 增加了对Acrobat DC多线程转换的支持，使用户能够更有效地同时执行Word、Excel和PowerPoint文档到PDF文档的转换。 (FORMS-21310)
* 添加了将`com.adobe.granite.toggle.impl.dev`捆绑包包含在AEM Service Pack 24中的功能，通过将其从Forms加载项中删除，可简化开发流程。 (FORMS-20139)
* 从forms-foundation中删除了FeatureToggleRenderConditionServlet，从forms加载项中删除了com.adobe.granite.toggle.impl.dev包。 此更新可确保在Forms加载项安装后，正确解析渲染条件，从而改善客户的组件功能。 (FORMS-20138)
* 由于自适应Forms中的查询运行时间较长，用户体验到性能缓慢。 此更新将反向移植查询更改以提高效率。 客户现在可以创建具有标记名称aemformsAFReferences的索引。 (FORMS-21411)
* 使用WebtoPDF将HTML转换为可移植文档格式(PDF)时，用户遇到标题位置未对齐的问题。 此问题会影响文档布局一致性和输出的可读性。 (FORMS-21502和FORMS-21540)
* 尽管成功进行了PreFlight验证，但用户仍遇到PDF/A-1b验证失败。 此问题会影响使用PDF验证工具的企业客户的文档合规性检查。 (FORMS-20196)
* 用户在UI中遇到未翻译的字符串，导致混淆和难以理解界面。 (FORMS-6542)
* 用户遇到电子邮件通知问题。 发送电子邮件工作流步骤无法发送电子邮件，影响自动通信流程。 (FORMS-17961)
* 用户遇到表单工作流测试失败，这影响了他们高效完成工作流流程的能力。 (FORMS-16231)
* 用户无法在AEM表单中使用PDF文件的时间线功能。 此问题会影响用户有效跟踪文档更改和修订的能力。 在PDF表单区域的“Forms和文档”部分下上传任何AEM时，时间轴视图停止运行。 (FORMS-19408)
* 用户与OData交互时会遇到空指针异常。 这会导致数据检索过程中断。 (FORMS-20348)
* 在删除开源Java库Guava之后，删除了google.common.collect库。 此更新确保使用自适应Forms的企业客户拥有更好的兼容性和性能。 (FORMS-17031)

### Forms验证码

* 为基于基础组件的自适应Forms添加了Hcaptcha和Turnstile支持。 (FORMS-16562)
* 用户在创建Captcha配置对话框中遇到图标重叠问题。 填写必填字段时，信息图标与错误图标重叠，导致配置设置期间出现混淆。 (FORMS-16916)
* 用户在基于基础组件的自适应Forms中遇到为reCAPTCHA选取的配置不正确。 未为表单选择配置容器时，`conf/global`文件夹中的多个配置导致了问题。 (FORMS-19237)
* 用户遇到了reCAPTCHA无法呈现的问题。 这会影响企业客户的表单提交和安全验证。 (FORMS-17136和FORMS-19596)
* 用户遇到了reCAPTCHA enterprise的大小未反映在用户界面(UI)中的问题。 (FORMS-16574)
* 由于“ReCaptchaConfigurationServiceImpl”中的ResourceResolver未关闭，用户遇到了ReCaptcha功能问题，导致在表单提交期间间歇性验证失败。 (FORMS-19241)
* 在Sites中创作表单时，用户遇到reCAPTCHA验证问题。 AEM表单未正确识别表单名称，导致验证失败。 (FORMS-20486)
* 即使企业reCAPTCHA得分为1.0，用户仍会提交表单，从而导致潜在的安全风险。 (FORMS-16766){{$include }}
* 通过将提交错误代码更新为400，改进了自适应Forms中的reCAPTCHA警报。 此外，改进了日志警报以区分超时、过期和机器人检测故障，从而提高故障排除的准确性和系统可观察性。 (FORMS-19240)
* 在AEM Forms中使用reCAPTCHA集成时，关闭了ReCaptchaConfigurationServiceImpl中的未关闭的ResourceResolver实例，以防止潜在的资源泄漏并提高系统稳定性。 (FORMS-19242)
* 通过确保/conf/global文件夹中存在多个条目时每个表单绑定正确的配置，改进了AEM Forms的验证码配置处理。 如果未明确选择配置容器，则防止意外使用错误的验证码设置。 (FORMS-19239)

### 表单管理用户界面

* 用户在Forms >创建Watchfolder > Watchfolder创建过程中遇到未本地化的字符串。 创建watchfolder时，未找到“Watchfolder creation”和“Watchfolder created successfully”等字符串，这会影响用户界面体验。 (FORMS-15234)

## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

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

## 安装和更新 {#install-update}

有关设置要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 如果您从旧的6.5 SP直接升级到LTS SP1，请按照6.5到6.5 LTS GA [升级](/help/sites-deploying/upgrade.md)的说明操作。


有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 新安装 AEM 6.5 LTS 时，必须单独安装索引定义。更多详细信息请参阅[这篇文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 支持的平台 {#supported-platforms}

查找受支持平台的完整表格，包括对 [AEM 6.5 LTS 技术要求](/help/sites-deploying/technical-requirements.md)的支持等级。

>[!NOTE]
>
>建议与 AEM 6.5 LTS 一起使用 Java™ 17/Java™ 21 版本。


## 已弃用和已删除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe 不断审查产品功能，通过更新或取代旧功能来提高客户价值。这些改变都仔细考虑了向后兼容的情况。

沟通有关即将删除或取代 Adobe Experience Manager (AEM) 功能的消息时，适用以下规则：

1. 首先宣布弃用。已弃用的功能仍然可供使用，但不再继续改进。
1. 最早会在下一个主要版本中移除已弃用的功能。移除的实际目标日期会计划稍后公布。

在实际移除之前，此过程将为客户提供至少一个发布周期时间，使客户的实施能够适应功能弃用后的新版本或后续版本。

### 已弃用的功能  {#deprecated-features}

本节列出了 Adobe 在 AEM 6.5 LTS 中已弃用的功能。通常情况下，Adobe 在未来版本中移除某些功能之前，会先弃用这些功能并提供替代方案。


建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，使用所提供的替代功能更改自己的实施。

| 区域 | 专题 | 替换 | 版本 (SP) |
| --- | --- | --- | --- |
| Sites | [SPA 编辑器](/help/sites-developing/spa-overview.md) | 管理 AEM 中的 Headless 内容时首选以下编辑器：<br>- [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。 | 6.5 LTS GA |

### 已移除的功能 {#removed-features}

此部分列出了 AEM 6.5 LTS 中已移除的功能。之前的版本中已将这些功能标记为已弃用。

| 区域 | 专题 | 替换 | 版本 (SP) |
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

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

### AEM 6.5.21-6.5.23 和 AEM 6.5 LTS GA 中的 JSP 脚本包问题

AEM 6.5.21、6.5.22、6.5.23 和 AEM 6.5 LTS GA 附带 `org.apache.sling.scripting.jsp:2.6.0` 捆绑包，其中包含一个已知问题。此问题经常在 AEM 实例处理许多并发请求而导致高负载的情况下发生。

发生此问题时，错误日志中可能会出现以下异常之一，并会引用 `org.apache.sling.scripting.jsp:2.6.0`：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

有一个热修复 [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) 可以解决这个问题。

### 具有仅SSL功能的Dispatcher连接失败(已在AEM 6.5 LTS SP1及更高版本中修复){#ssl-only-feature}

>[!NOTE]
>
> 此问题仅在AEM 6.5 LTS GA版本中出现。

在 AEM 部署中启用仅 SSL 功能后，会发生一个影响 Dispatcher 与 AEM 实例之间连接的已知问题。启用此功能后，健康检查可能会失败，并且 Dispatcher 和 AEM 实例之间的通信可能会中断。尤其是当客户尝试通过 `https + IP` 将 Dispatcher 与 AEM 实例连接时，会出现此问题。它与 SNI（服务器名称指示）验证问题有关。

**影响：** 

* 健康检查失败，出现 HTTP 400 响应码
* Dispatcher 与 AEM 实例之间的通信中断
* 无法通过 Dispatcher 正确提供内容
* 使用 HTTPS 与 Dispatcher 配置中的 IP 地址时连接失败
* 通过 HTTPS + IP 连接时出现 HTTP 400“SNI 无效”的错误

**受影响的环境：**

* 具有 Dispatcher 配置的 AEM 部署
* 启用了仅 SSL 功能的系统
* 使用 `https + IP` 方法与 AEM 实例连接的 Dispatcher 配置

**解决方法：**
如果您遇到此问题，请联系 Adobe 客户支持部门。有一个热修复 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 可以解决这个问题。采用必要的热修复之前，不要尝试启用仅 SSL 功能。

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此[!DNL Experience Manager] 6.5 LTS Service Pack 1版本中包含的OSGi包和内容包：

* [Experience Manager 6.5 LTS Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt)中包含的OSGi包列表<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt)中包含的内容包列表<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站只提供给客户。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/customer-one/using/home)。

