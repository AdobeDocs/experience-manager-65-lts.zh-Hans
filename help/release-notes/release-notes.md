---
title: Adobe Experience Manager 6.5 LTS SP1 的最新发行说明
description: 查找 Adobe Experience Manager 6.5 LTS 服务包 1 的当前版本信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 12e2966754fe317c2a20951ee29b401425de486b
workflow-type: tm+mt
source-wordcount: '7223'
ht-degree: 71%

---

# Adobe Experience Manager 6.5 LTS SP1 的最新发行说明 {#release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 1 (SP1)，适用于GRANITE-61551 <!-- UPDATE FOR EACH NEW RELEASE -->的修补程序 |
| 类型 | 服务包发行 |
| 日期 | 2025年9月9日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fcq-6.5.lts.1-hotfix-GRANITE-61551-1.2.zip) |

<!-- OLD URL TO JAR
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) | -->


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS SP1 中包含的内容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS SP1 包含新功能、客户要求的重要增强功能以及错误修复。还包括自 2025 年 3 月 6.5 LTS 首次发布以来推出的在性能、稳定性和安全性方面的改进。在 6.5 LTS 上[安装此服务包](#install-update)。

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 6.5 LTS 服务包 1 中修复的问题 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 无障碍可访问性 {#sites-accessibility-65-lts-sp1}

* 修复了内容片段中的文本编辑器元素默认被截断的问题。文本编辑器中现在显示完整的内容，不会截断。(SITES-33005)
* 修复了点击 URL 路径会打开 Indigo 主页而不是正确的目标 URL 的问题。(SITES-33004)
* 修复了一个自定义 AEM 组件中的无障碍可访问性问题，该问题导致自动测试时不符合 ADA 合规要求。(SITES-30660)
* 通过确保文本在浅色背景上显示为黑色并满足 WCAG 2.0 对比度要求，修复了“警报”对话框和工作流消息中的 ADA 合规性问题。(SITES-30138)
* 修复了一个无障碍可访问性问题：AEM Sites 编辑器中的“类别”按钮缺少一个专门的标签，导致 JAWS 将其公告为“图像按钮菜单”，而不是提供描述的标签。(SITES-27497)
* 修复了一个无障碍可访问性问题：有效权限屏幕中的复选标记图标缺少替换文本，导致 JAWS 无法读取和传达其含义。(SITES-27272)
* 修复了一个无障碍可访问性问题：“权限”页面不提供用于移除用户或组权限的清晰的 JAWS 公告，使屏幕阅读器用户感到困惑。(SITES-27238)
* 修复了一个无障碍可访问性问题：错误消息仅显示为图标而没有描述性文本，导致 JAWS 无法在发生错误时公告错误。(SITES-27155)
* 修复了一个无障碍可访问性问题：JAWS 在 AEM 内部部署环境中读取到不正确且不清楚的按钮描述，包括该模块分区缺少 2 级标题的文本。(SITES-27152)
* 修复了一个无障碍可访问性问题：JAWS 在 AEM Assets 选项卡中筛选值后不公告结果数量。(SITES-27150)
* 修复了一个无障碍可访问性问题：创建文件夹后不显示确认，并且 JAWS 不在 Assets UI 中公告确认。(SITES-27141)
* 修复了 AEM Sites 中的一个无障碍可访问性问题。JAWS 不公告表单错误，焦点移到非交互式错误元素，按下 tab 移出焦点时不显示必填字段错误。(SITES-27138)
* 修复了一个无障碍可访问性问题：时间线按钮菜单缺少一个专门的标签，导致 JAWS 只读取“活动按钮菜单”而不提供清晰的描述。(SITES-27134)
* 修复了一个无障碍可访问性问题：JAWS 不公告容器项的操作或角色，只读取“痕迹导航 v1”和“按钮 v2”而不是描述性标签。(SITES-27131)
* 修复了一个无障碍可访问性问题：快速发布弹出窗口不提供正确的成功消息，导致屏幕阅读器不公告完成的反馈。(SITES-26912)
* 修复了 coral 列视图中的一个无障碍可访问性问题：ARIA 角色的元素需要子角色，但不包含子角色，导致不符合无障碍标准。(SITES-26898)
* 修复了一个无障碍可访问性问题：创建页面顶部导航中的“模板”和“属性”文本在“重排”模式下不可见，导致键盘和屏幕阅读器用户无法访问。(SITES-26895)
* 修复了一个无障碍可访问性问题：无法通过键盘导航访问顶部导航中的“搜索”、“解决方案”、“帮助”、“收件箱”和“用户”图标的工具提示。(SITES-26889)
* 修复了一个无障碍可访问性问题：基本选项卡表单字段不提供错误建议，导致在必填字段未填写时用户未获得指导。(SITES-26885)
* 修复了一个无障碍可访问性问题：NVDA 和 Narrator 屏幕阅读器在“创建”页面中不公告模板文件详细信息，导致用户无法以编程方式获得完整信息。(SITES-26884)
* 修复了一个无障碍可访问性问题：“基本”选项卡中“页面标题文本框”使用错误的名称，导致屏幕阅读器无法向用户提供准确的信息。(SITES-26879)
* 更新了按钮前景和背景颜色，以满足 WCAG 2.2 AA 最低对比度要求，为所有用户提高可读性和无障碍可访问性。(SITES-26877)
* 解决了创建页面顶部导航中的“模板”和“属性”文本在调整大小后消失的问题，确保了视力较差的用户的可见性和无障碍可访问性。(SITES-26872)
* 修复了应用“重排”后主页面上出现多个水平滚动条的问题，现在只显示一个滚动条，确保正确的可访问性和内容可见性。(SITES-26800)
* 修复了 AEM 页面编辑器中的一个无障碍可访问性问题：在激活“用户画像”、“购物车”或“放弃”等按钮后，键盘焦点会意外重置到“人口统计”工具栏的起始位置。现在，焦点保留在已激活的按钮上，以确保一致的键盘导航和屏幕阅读器工作流。(SITES-25306)
* 修复了页面标题和标记字段的无障碍标签关联问题。现在，AEM 界面在使用 JAWS 等屏幕阅读器时，能够正确关联“标题”和“页面标题”字段的无障碍标签。此项修复确保在页面创建、属性和移动工作流中正确读取标签，从而增强 ADA 合规性。(SITES-27149)
* 修复了时间线中注释输入字段缺少可视化标签的问题。为时间线中“注释”输入字段添加了可视化标签，以改善无障碍性。此更新确保屏幕阅读器能够准确公告字段标签。这种体验为所有用户改善了表单导航和提交，特别是为依赖辅助技术的用户带来便利。(SITES-26903)
* 修复了时间线注释中省略号按钮的键盘可访问性问题。为时间线中注释旁边的省略号（三个点）按钮启用了键盘导航功能。用户现在可以使用 Tab 键访问按钮并与之交互，改善了无障碍可访问性，方便依赖键盘进行导航的用户使用。(SITES-26891)
* 改进了 NVDA/Narrator 对选择对话框中搜索结果的公告。更新了“打开选择”对话框，现在使用 NVDA 或 Narrator 等屏幕阅读器时会公告是否找到搜索结果。此项改进可以帮助依赖辅助技术的用户在无需视觉确认的情况下了解搜索操作的结果。(SITES-26883)
* 修复了注释输入字段旁省略号图标的 ARIA 角色错误问题。更新了注释输入字段旁的省略号（三圆点）图标，现在使用正确的 ARIA 角色，确保屏幕阅读器能够准确识别该元素。此项改进提升了无障碍合规性，并优化了依赖于辅助技术的用户的使用体验。(SITES-26881)
* 修复了 Coral UI 组件中的无效 ARIA 属性问题。更新了 Coral UI 组件，确保所有 ARIA 属性均使用有效值，增强了无障碍合规性。特别是修复了此前错误分配无效值的问题，如 `aria-modal="dialog"`。此项增强功能使屏幕阅读器能够正确理解对话框元素，从而提升依赖于辅助技术的用户的无障碍可访问性。(SITES-26873)
* 改进了“重排”场景下的图标可见性和工具提示。优化了“重排”行为，确保&#x200B;**下载**、**重新处理资产**&#x200B;和&#x200B;**签出**&#x200B;图标的工具提示能够正确显示。重点修复了当视口调整大小或浏览器缩放设置更改时，图标及其标签可能变得不可见的无障碍可访问性问题。此项修复可以帮助视力低下的用户在“重排”过程中仍然能够看到图标，并会提供正确的图标说明。(SITES-26871)


#### 管理员用户界面{#sites-adminui-65-lts-sp1}

* 修复了一个无障碍可访问性问题：JAWS 在“创建网站”对话框中不公告列表角色，也不提供导航和激活指导。(SITES-30661)
* 屏幕阅读器对网站过滤视图中的状态消息的支持按预期工作，确保用户在视图之间切换时获得清晰及时的反馈。(SITES-24992)
* 过滤器边栏中的日期选取器完全显示在其容器内，提供足够的触摸目标尺寸，解决了剪切问题。(SITES-24988)
* 选定的过滤器标记现在使用与视觉呈现相匹配的语义 HTML 和 aria 标签，确保准确支持角色，为辅助性技术确保清晰操作。(SITES-24980)
* 在引用边栏区域添加了 aria 标签属性，为屏幕阅读器用户提供独特的描述性标签，确保在整个页面上一致识别地标。(SITES-24973)
* 更新了引用边栏，为大小调整和定位使用相对单位，使内容能够缩放并在 1280x1024 视口放大到 400% 时保持完整功能。(SITES-24972)
* 网站主页列表视图中已确认的表格元素包含适当的列标题角色，使屏幕阅读器能够公告每个数据单元的标题。(SITES-24942)
* NVDA 现在会公告树形目录中的修改日期，确保屏幕阅读器用户获得完整的资产详细信息。(SITES-24782)
* 解决了 NVDA 屏幕阅读器对 AEM Sites 的树形目录组件中各项的文本公告不完整的问题。NVDA 现在可以读取每项的全文，提高了无障碍可访问性和合规性。(SITES-24780)
* 为树形目录中的窗口分割添加了键盘可访问性，使用户仅使用键盘即可调整左侧栏的大小。(SITES-24779)
* 更新了帮助菜单搜索结果，现在包含列表项的正确 ARIA 角色，确保屏幕阅读器正确公告链接，提高无障碍可访问性。(SITES-24729)
* 修复了屏幕阅读器不公告“Y 个结果中的 X 个”状态消息的问题。或者，在网站过滤器面板中应用过滤器后显示“未找到结果”消息，确保用户获得正确的结果确认。(SITES-24720)
* 修正了应用程序导航中导航链接缺少角色分配的问题。添加了适当的 ARIA 角色，以确保屏幕阅读器正确识别和公告导航元素。(SITES-24719)
* 用按钮元素替换了特定过滤器标记的错误网格角色标记，并添加了可访问的名称，确保屏幕阅读器正确公告和识别标记。(SITES-24717)
* 添加了在执行多选时屏幕阅读器对引用边栏状态消息的公告，确保用户获得变更确认。(SITES-24678)
* 修正了搜索字段的行为，现在不自动公告第一个结果。屏幕阅读器现在会公告找到的结果数量，使用户能够导航列表而不会听到错误的焦点公告。(SITES-24658)
* 从列表视图的非交互式静态元素中删除了错误的 `aria-label` 属性，以防止屏幕阅读器公告误导性或不相关的信息。(SITES-24515)
* 更新了列表视图第一列中的复选框，使用“标题”列文本作为其可访问名称，确保屏幕阅读器准确传达表单字段的用途。(SITES-24514)
* 添加了适当的 ARIA 属性和实时区域支持，以便在屏幕阅读器用户在内容中导航时公告加载状态的消息。(SITES-24481)
* 更新了响应式设计，当内容在 1280×1024 宽度的视口中放大到 400% 时消除水平滚动，确保不用横向滚动也可看到完整内容。(SITES-24308)
* 按照逻辑顺序修正了网站管理员 UI 中的焦点导航，按下 Esc 后焦点返回到“全选”按钮，按下 Tab 后焦点移到下一个交互式元素。(SITES-24307)
* 更新了网站管理员 UI 中的焦点顺序，使 `<betty-titlebar-title>` 元素中的痕迹导航按钮在键盘导航过程中按照正确的顺序获得焦点。(SITES-24305)
* 验证了跳过链接功能，确保它将键盘焦点移到主要内容区域，从而允许键盘用户绕过标题元素并有效地访问内容。(SITES-24061)


#### 经典用户界面{#sites-classicui-65-lts-sp1}

修复了经典 UI 中复选框标签缺失，并且多个 UI 元素（包括日期搜索和非标准界面）中的 HTML 显示为编码文本的问题。(SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM 现已防止由图像资产中格式错误的 XMP 元数据导致的性能下降。包含无效或不合规 XMP 属性名称（例如名称中包含数字或结构不合格）的资产在处理过程中不再反复触发警告日志。系统会过滤掉有问题的元数据，确保资产摄取和验证能够顺利完成且无错误。(SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-65-lts-sp1}

在一位作者已签出内容片段的情况下，其他作者仍然可以发布该片段，这与签出功能的预期行为不符。此项修复可防止在签出内容片段时，其他用户在创作界面中看到或使用发布按钮。(SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 组件控制台{#sites-component-console-65-lts-sp1}

修复了产品列表组件中的一个问题，即“全选”复选框仅添加了初始页面中的前 20 个 SKU，而不是搜索结果中的所有 SKU。(SITES-29191)

#### 核心后端{#sites-core-backend-65-lts-sp1}

XMP 元数据格式不正确导致在 `ValidationDataServlet` 中处理图像资产时触发错误。此修复确保了对元数据的正确处理，并避免了对无效属性的重复解析。(SITE-30683)  

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - 实时副本{#sites-msm-live-copies-65-lts-sp1}

* 修复了在 AEM 6.5 内部部署中重新启用幽灵组件继承时发生的 JavaScript 错误 `ns.ui.alert is not a function`。(SITES-31993)
* 修复了在 AEM 6.5 中“稍后”推出选项在不选择日期的情况下允许继续的问题。(SITES-31374)

#### 页面编辑器{#sites-pageeditor-65-lts-sp1}

* 解决了 Teaser 模态中的一个问题，即在输入有效数据并解决错误后，“链接和操作”选项卡继续显示样式、图标和 aria 无效属性的错误。(SITES-25527)
* 修复了 Teaser 模态文本编辑器中列表和段落按钮未将其展开或折叠的状态传达给屏幕阅读器的问题，从而确保准确更新 aria 展开的属性。(SITES-25365)
* 修复了人口统计工具栏中的一个问题：使用键盘输入调整购物车滑块时，焦点会移到购物车按钮而不是保留在滑块上，问题修复后提高了键盘用户的导航效率。(SITES-25324)
* 通过为关联的 `<label>` 元素分配一个值，为人口统计工具栏中的购物车滑块添加了可访问的名称。此修复提高了与辅助技术的兼容性，为屏幕阅读器用户增强了可用性。(SITES-25322)
* 为人口统计工具栏下拉菜单中的按钮添加了 ARIA 角色和可访问的名称。此修复使辅助性技术能够正确识别，改进了键盘和屏幕阅读器用户的导航。(SITES-25315)
* 调整了人口统计工具栏布局，以防止在浏览器放大 200% 时内容溢出视口，确保无需水平滚动可访问所有控件。(SITES-25309)
* 修正了人口统计工具栏中的焦点管理，使键盘焦点保持在已激活的按钮上，而不是重置到工具栏的起始位置。(SITES-25306)
* 按钮标签重叠功能按设计预期工作，当具有相似屏幕宽度的模式被激活时，使用工具提示来显示标签。(SITES-25285)
* 注释模态包含一个可见的提交按钮，用户无需按下 Escape 键或点击模态以外即可提交注释。(SITES-25281)
* 注释模态包含一个铅笔图标按钮，允许用户提交注释，提供一种清晰易用的提交方法。(SITES-25269)
* 修正了注释和关闭注释按钮的屏幕阅读器公告，以提供准确、相关的反馈，并移除不相关或令人困惑的信息。(SITES-25268)
* AEM 编辑器页面的画布部分现在全面支持键盘无障碍访问功能。用户仅需使用键盘即可激活该部分的标题和编辑按钮，而无需依赖鼠标悬停。此更新确保符合 WCAG 2.1.1 要求，并提升了组件（如 Teaser、图像、轮播、布局、时间扭曲和注释模态）的可用性。(SITES-25256)
* 移除了宽度为 320px 的轮播模态中不必要的水平滚动，以确保视口中显示所有内容，无需横向导航。(SITES-25254)
* 移除了宽度为 320px 的图像模态中不必要的水平滚动，以确保视口中显示所有内容，无需横向导航。(SITES-25244)
* 移除了宽度为 320px 的 Teaser 模态中不必要的水平滚动，以确保视口中显示所有内容，无需横向导航。(SITES-25242)
* 为 Teaser 模态中的 `List` 和 `Paragraph Format` 两个弹出菜单启用了键盘导航。此修复允许用户使用箭头键访问和导航这两个菜单。(SITES-25235)
* 修正了注释和关闭注释按钮的屏幕阅读器公告，以提供与相关联的操作一致的准确、相关的反馈。(SITES-25234)
* 改进了 Teaser 模态中的帮助按钮标签，以清楚地描述其用途，并为所有用户（包括辅助技术用户）提供有意义的背景信息。(SITES-25224)
* 通过将模拟器尺子测量值与各设备关联起来，改进了屏幕阅读器用户的模拟器尺子。还用 aria-describedby 元素替换了工具提示。(SITES-24955)
* 未实施修复，因为“编辑”按钮按预期工作，提供信息上下文而不是执行操作。(SITES-24950)
* 编辑器页面上确认的焦点顺序遵循逻辑顺序，允许用户导航所有交互式元素，不会意外跳过或循环跳回。(SITES-24937)
* 当用户应用自定义文本间距设置时，预览模式画布现在会正确更新文本间距，确保所有内容区域的格式一致。(SITES-24936)
* 经过验证的预览按钮不再触发上下文或焦点状态变化，确保用户在页面视图更新之前有目的地激活该按钮。(SITES-24784)
* 为应用程序导航链接添加了正确的 ARIA 角色分配，使屏幕阅读器能够准确识别并公告导航项，改进了无障碍可访问性。(SITES-24718)
* 更新了“更改过滤器”按钮，以便告知屏幕阅读器展开和折叠状态，删除了多余的 ARIA 属性，调整了标签，以提供清晰、不重复的描述。(SITES-24713)
* 在链接选择对话框中添加了搜索结果状态消息的屏幕阅读器公告，确保用户在结果加载或未找到匹配项时获得确认。(SITES-24700)
* 添加了图像模态加载状态的屏幕阅读器公告，确保用户在模态加载并准备进行交互时获得反馈。(SITES-24697)
* 解决了 Teaser 模态内容在放大 200% 和 400% 时被粘性标题遮挡的无障碍问题，确保在页面放大时的完全可见性和可用性。(SITES-24523)
* 在搜索/过滤字段中添加了包含搜索结果数量的状态消息，使屏幕阅读器能够向用户公告结果。(SITES-24506)
* 添加了搜索/过滤字段中搜索结果数量的屏幕阅读器公告，确保用户在结果加载后立即获得反馈。(SITES-24505)
* 在侧边栏面板的选项卡列表中添加了可访问的名称，使屏幕阅读器能够按照 WAI-ARIA 指南公告其用途。(SITES-24492)
* 为含义不清的编辑器图标添加了描述性标签，确保所有用户清楚地了解每个按钮的功能。(SITES-24480)
* 启用了“画布”视图中分区标题和操作按钮的完全键盘可访问性，确保鼠标和键盘用户的操作一致。(SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### 通用编辑器 {#sites-universal-editor-65-lts-sp1}

* 修复了 QueryTokenService 中的一个竞争条件：在登录令牌服务返回结果之前如果触发了多个带有查询参数的请求，该竞争条件会导致登录失败。(SITES-30659)
* 修复了 UniversalEditorURLService 中的一个问题，即在 Felix ConfigMgr 中保存一个映射路径的数组时只保留第一项。(SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

修复了将资产从远程 DAM 同步到 Sites 本地 AEM 时资产中的已发布状态和与复制相关的属性被移除的问题。(Assets-48958)

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

解决了 OSGi 依赖循环阻止 HTL 脚本引擎工厂正常工作的问题，确保了正确的服务解析和脚本执行。(Granite-58275)

#### 集成{#foundation-integrations-65-lts-sp1}

* 从 `com.adobe.cq.cq-analytics-integration` 捆绑包中移除了 commons-httpclient 3.x 的使用，将其替换为 `org.apache.httpcomponents.httpclient` 4.5.13.B0001，以符合最新的 AEM 6.5 LTS 标准。(CQ-4360586)
* 从 AEM 中移除了已弃用的 Search&amp;Promote 集成捆绑包，以去除不使用的组件，减少维护开销。(CQ-4358030)
* 为 SiteCatalyst 集成添加了新的后端测试案例，以改进分析验证并确保更全面的覆盖。(CQ-4359991)
* 修复了“启动项配置”的“属性”部分中“公司和属性”下拉菜单不显示的问题。此外，尽管所有必填字段都已填写，“保存并关闭”仍会触发错误；在只有“标题”字段为空的情况下，“公司和属性”显示不正确的错误消息。(CQ-4359853)
* 从版本 6.6 中移除了 `searchpromote` servlet 路径条目，与 Search&amp;Promote 捆绑包移除保持一致。(CQ-4359523)
* 修复了目标存储库的 HTTP 测试案例，以确保准确验证并提高测试可靠性。(CQ-4359022)
* 从 integration-adobeims-console 模块中移除了 Guava 缓存使用，以消除 Guava 库依赖项。(CQ-4358710)
* 验证了 AEM 6.6 中的 DTM 集成工作流、收件箱任务和项目功能，确保在 AEM 6.5 中正常运行。(CQ-4358151)
* 验证了 AEM 6.6 中的内容洞察功能，确保在 AEM 6.5 中的兼容性和正常运行。(CQ-4357774)
* 验证了 AEM 6.6 中的云服务功能，确保在 AEM 6.5 中的兼容性和正常运行。(CQ-4357773)
* 验证了 AEM 6.6 中的 Adobe IMS 控制台集成，确保在 AEM 6.5 中的兼容性和正常运行。(CQ-4357772)
* 为 Test&amp;Target 集成更新了 Jenkins 管道，确保在 Java 17 上运行，解决 Selenium 测试失败问题，将选择测试移至 Playwright，并确保通过所有单元测试。(CQ-4357770)
* 通过更新构建和测试管道，使 DX 集成、工作流、收件箱和项目与 6.6.0 分支保持一致。还解决了升级兼容性问题，并验证了所有相关服务的稳定性和功能。(CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 本地化{#foundation-localization-65-lts-sp1}

* 将“权限”列表中“移除访问控制”对话框中的字符串本地化，以显示正确的翻译。(GRANITE-59427)
* 修复了模型编辑器的“OR 拆分属性”添加规则对话框中多个 UI 字符串（包括运算符和字段标签）的显示未本地化的问题。所有字符串的显示现在都已正确本地化。(CQ-4354014)
* 为工作流模型编辑对话框中的“显示描述”工具提示添加了缺失的翻译。(CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

解决了 AEM 在升级过程中将 `/apps/system/config` 中的现有配置文件重新创建或重命名，将 `.cfg.json` 文件替换为 `.config` 文件的问题。(GRANITE-58899)

#### 全方位搜索{#foundation-omnisearch-65-lts-sp1}

修复了占位符错误地显示为输入字段标签的无障碍可访问性问题。此问题导致搜索、AEM 体验片段、内容片段和内容片段模型中缺少字段标签。(Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 项目{#foundation-projects-65-lts-sp1}

* 解决了在日程表视图中删除项目时，尽管项目删除成功却显示不正确的错误弹出窗口的问题。(CQ-4358890)
* 修复了 Firefox 中“项目”视图中的“资产收集”卡片页脚与卡片边框重叠的问题。页脚现在正确对齐，不再重叠。(CQ-4353317)

#### 快速入门{#foundation-quickstart-65-lts-sp1}

* 更新了卸载脚本，调整了 Guava 捆绑包的版本范围，防止其在通过包管理器安装时被列入阻止列表。(GRANITE-59559)
* 通过修正界面中经典复选框的处理，修复了在编辑复制代理时复制 UI 中显示错误（`#1660`）的问题。(GRANITE-58302)
* 通过解决缺少服务权限、更新配置处理以及确保所需服务正确初始化，解决了运行使用 JDK 21 的 AEM 6.5 LTS 时 S3 数据存储库的多个启动错误。(GRANITE-57082)
* 定义了 AEM 6.5 的维护和支持策略。此修复包括以下内容：
   * 服务包 cadence。
   * 热修复 cadence。
   * 同时支持 AEM 6.6。
   * 更新了支持矩阵。
   * 附加组件所有权责任。(GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 将 Sling ResourceAccessSecurity 更新至版本 1.1.2，以解决在多个 `ResourceAccessGate` 引用初始化 `ResourceAccessSecurityImpl` 时发生的 `ClassCastException` 问题。(NPR-42750)
* 修复了 Adobe Stock 集成中许可证对话框显示为灰色的问题。导致此问题的原因是 `sunt:initList` 函数移除了必需的输入字段。该函数位于 Coral Foundation 客户端库中。更新了客户端库以保留必要的字段，确保启用正确的许可证对话框功能。(NPR-42748)
* 回溯移植了针对 Sling 脚本问题的修复，该问题导致包安装过程中出现 `DataTimeParseException` 和 `String.length()` 空指针异常。将 Sling 脚本更新至版本 2.8.3-1.0.10.6，以减少安装错误并提高稳定性。(NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### 用户界面{#foundation-ui-65-lts-sp1}

* 解决了 AEM Author UI 中用户组限制显示 41 个的问题。导致此问题的原因是 Granite UI 组选取器组件中默认限制批次。更新了组件以显示所有组，不再被截断。(NPR-42749)
* 解决了内部部署页面创建向导中的问题，即在编辑页面属性时未重新验证多字段组件中的必填字段。这个问题使得作者可以绕过验证，使用不完整的数据继续工作。(GRANITE-58826)
* 修正了 AEM 中帮助按钮的 ARIA 属性，以确保 JAWS 屏幕阅读器公告清晰、用户友好的标签，而不是显示未经翻译的图标和文本元数据。(GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 添加了 Java 17 对 AEM Translations 的支持，更新了翻译捆绑包、验证了 Java 包兼容性、移除了已弃用的依赖项，并通过全面测试确保完整功能。(CQ-4357525)
* 移除了不稳定的 Evergreen 测试 `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater`，以防止自动测试过程中发生虚假失败。(CQ-4298376)

#### 工作流{#foundation-workflow-65-lts-sp1}

* 添加了收件箱项中缺少的 `data-detailsurl` 属性，以防止在使用带有 Java 21 的 AEM 6.5 LTS 时 URL 中出现未定义的值。(GRANITE-60158)
* 修复了在运行使用 Java 21 的 AEM 6.5 LTS 时 `WorkflowToPublishEventService` 捆绑包的 `deactivate` 方法中的 NullPointerException，确保工作流服务正确关闭，不出现错误。(GRANITE-58151)
* 更新了工作流索引，以支持共享、离开办公室自定义和时间线查询问题解决方法。(GRANITE-52640)
* 更新了工作流索引，以支持共享、离开办公室自定义功能和时间线查询问题解决方法。(GRANITE-52294)
* 解决了程序升级到 AEM 版本 10912 时日志比较验证过程中日志失败错误增多的问题，确保了工作流的稳定执行。(GRANITE-44268)
* 更新了 Workflow 存储库中的 URL 清理方法，将 `url.searchParams` 替换为 `url.search`，从而增强了对易受攻击的 URL 的 XSS 保护。(CQ-4359585)
* 验证 AEM 6.6 Forms 中的工作流、收件箱和项目功能，以确保正确运行和集成。(CQ-4358777)
* 实施了通过 Jenkins 自动发布 Workflow 内容工件，实现了 AEM 6.5 中简化且一致的部署流程。(CQ-4358472)
* 修复了收件箱创建任务工作流中的一个问题：尽管任务已创建，但由于 JavaScript 语法错误，“添加任务”对话框在点击“提交”后不关闭。(CQ-4355336)
* 修复了由于缺少 `isEndUserConfigurationEnabled` 属性定义而导致无法保存收件箱视图配置的问题。(CQ-4287757)

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

## 安装和更新AEM Forms加载项 {#install-update-aem-forms-add-on}

有关详细说明，请参阅[执行就地升级](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。



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

### 已移除的功能  {#removed-features}

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

## 包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此 [!DNL Experience Manager] 6.5 LTS 服务包 1 发行版本中包含的 OSGi 捆绑包和内容包：

* [Experience Manager 6.5 LTS 服务包 1](/help/release-notes/assets/65lts_sp1_bundles.txt) 中包含的 OSGi 捆绑包列表 <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS 服务包 1](/help/release-notes/assets/65lts_sp1_packages.txt) 中包含的内容包列表 <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站只提供给客户。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/customer-one/using/home)。

