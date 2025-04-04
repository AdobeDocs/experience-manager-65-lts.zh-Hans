---
title: 管理表单简介
description: AEM Forms提供了用于管理自适应Forms和相关资源的工具。 本文介绍了关键表单管理功能和用户界面元素。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User
exl-id: 7ec29926-a5f6-4080-a981-597f9632f6e8
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 1%

---

# 管理表单简介 {#introduction-to-managing-forms}

AEM [!DNL Forms]提供了简单但功能强大的用户界面，用于创建和管理表单、文档、主题、书信、文档片段、数据字典和相关资源。 它有助于管理表单、文档和相关资产的完整生命周期 — 从开发人员的桌面到产品
它位于供最终用户使用的门户服务器上。 您可以使用AEM [!DNL Forms]用户界面执行以下操作：

* 访问AEM [!DNL Forms]组件
* 访问AEM [!DNL Forms]配置

>[!NOTE]
>
>有关其他AEM工具和选项的详细信息，请参阅[创作](/help/sites-authoring/author.md)。

## 访问AEM Forms组件 {#access-aem-forms-components}

除了创建表单、文档和相关资源选项外，AEM还提供了创建站点、资源、管理AEM实例等选项。 您可以单击![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager徽标以导航到所有可用的工具。 除了指向其他组件控制台的链接之外，它还包含AEM [!DNL Forms]的链接。 要导航到AEM [!DNL Forms]，请单击Experience Manager徽标![adobeexperiencemanager](assets/adobeexperiencemanager.png) >导航![compass](assets/compass.png) > **[!UICONTROL Forms]**。 将显示以下控制台的链接：

* 表单和文档
* 主题
* 书信
* 文档片段
* 数据字典

  ![AEM Forms控制台](assets/aem_forms_console_new.png)

### 表单和文档  {#forms-documents}

Forms &amp; Documents提供了用于创建交互式通信、自适应表单、自适应表单片段和表单集的选项。<!--Only for AEM [!DNL Forms] on JEE, Forms & Documents provides an option to import files from local storage and sync AEM [!DNL Forms] assets with Workbench.-->

创建按钮是创建或上传AEM [!DNL Forms]资源的过程的起点。 它为您提供了创建以下内容的选项：

* **交互式通信**：交互式通信是基于HTML的个性化、交互式且设备友好的数字通信、报表或文档。 交互式通信本质上属于响应式，可根据用户设备和设置自动更改布局和设计。 有关详细信息，请参阅[交互式通信概述](/help/forms/using/interactive-communications-overview.md)

* **自适应表单：**&#x200B;自适应表单是吸引人的响应式表单。 您可以创作自适应表单，通过基于用户响应、设备或工作环境添加或删除表单部分来动态适应用户输入。 [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md)文章提供了有关自适应表单的详细信息。

* **自适应表单片段：**&#x200B;虽然每个表单都针对特定目的而设计，但大多数表单中都存在一些通用区段，如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 您可以为此类部分创建单个资源。 这些可重用的独立区段称为自适应表单片段。 有关详细信息，请参阅[自适应表单片段](../../forms/using/adaptive-form-fragments.md)文章。

* **表单集：**&#x200B;表单集是分组在一起并作为单个表单集提供给最终用户的HTML5表单的集合。 当最终用户开始填写表单集时，表单会无缝地从一个表单转换为另一个表单。 最后，用户只需一次单击即可将所有表单作为单个实体提交。 有关详细信息，请参阅AEM Forms中的[表单集](../../forms/using/formset-in-aem-forms.md)。

* **文件夹：** AEM [!DNL Forms]用户界面使用文件夹排列资源。 它支持两种类型的文件夹：

   * **常规文件夹：**&#x200B;这些文件夹用于在AEM [!DNL Forms]用户界面中创建的资源。 这些文件夹没有严格的文件夹结构。 您可以重命名、创建子文件夹，并将自适应表单、交互式通信、自适应表单片段、表单模板(XDP)、PDF forms、文档和相关资源存储在这些文件夹中。
   * 在迁移Workbench进程（LiveCycle存档）并与Forms [!DNL Forms]用户界面同步时，将创建&#x200B;**Forms Workflow文件夹：** AEM工作流文件夹。 不允许重命名、创建子文件夹、创建交互式通信、自适应表单片段或交互式通信。 也不允许删除版本文件夹或者创建并上传与版本文件夹平行的自适应表单、自适应表单片段或交互式通信。

  ![文件夹](assets/folders.png)

  **A.**&#x200B;常规文件夹&#x200B;**B.** Forms Workflow文件夹

Forms和“文档”面板还提供以下选项：

* **从本地存储导入文件：**&#x200B;您可以导入PDF forms和文档、表单模板（XFA表单）和其他资源（XSD的图像和XML架构）。 有关分步说明，请参阅[将资产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md)。
* **将AEM Forms资源与Workbench同步：**&#x200B;您可以使用“来自Workbench的文件”选项在AEM Forms用户界面与Workbench之间同步资源。 它确保AEM [!DNL Forms]用户界面和Workbench的crx存储库资源选择中的所有资源都可用。

### 主题  {#themes}

主题包含组件和面板的样式详细信息。 主题具有独立的标识。 因此，您可以在多个自适应表单上重复使用主题。 您可以为组件指定样式，或修改表单中使用的各种组件的CSS属性。 样式包括诸如背景颜色、状态颜色、透明度和大小等属性。 您可以将自定义项保存在主题中，并将其作为预设移植到表单的组件上。 将主题添加到表单时，指定的样式会反映在表单的相应组件上。 使用AEM 6.2 [!DNL Forms]，您可以创建主题并将它们应用于表单。

有关创建和使用主题的信息，请参阅AEM Forms中的[主题](../../forms/using/themes.md)。

### 书信  {#letters}

AEM [!DNL Forms]信件是一种安全、个性化的交互式通信。 您可以使用AEM [!DNL Forms]以简化的流程从预批准和自定义创作的内容中快速汇编信件（也称为对应）。

有关创建和使用书信的信息，请参阅[创建书信](../../forms/using/create-letter.md)。

### 文档片段 {#document-fragments}

文档片段是可重复使用的通信部分或组件，您可以使用它们来撰写信件。 文档片段的类型为文本、列表、条件和布局片段。 有关创建和使用文档片段的信息，请参阅[创建文档片段](/help/forms/using/document-fragments.md)。

### 数据字典 {#data-dictionaries}

通常，业务用户不需要了解元数据表示法，如XSD（XML架构）和Java类。 但是，它们通常需要访问这些数据结构和属性才能构建解决方案。 AEM [!DNL Forms]使用数据字典，使业务用户能够使用来自后端数据源的信息，而无需了解其基础数据模型的技术详细信息。

有关创建和使用数据字典的信息，请参阅创建[数据字典文章](../../forms/using/data-dictionary.md)

## 访问AEM [!DNL Forms]配置 {#accessing-aem-forms-configurations}

AEM“工具”面板包含用于各种组件的工具。 要导航到特定于AEM Forms的工具，请单击Experience Manager徽标![adobeexperiencemanager](assets/adobeexperiencemanager.png) >工具![hammer](assets/hammer.png) > **[!UICONTROL Forms]**。 将显示用于执行以下功能的工具：

* **配置Watched文件夹：**&#x200B;管理员可以配置网络文件夹（称为watched文件夹），以便当用户在watched文件夹中放置文件(如PDF文件)时，将启动预配置的操作并处理该文件。 有关详细信息，请参阅[创建和配置观察文件夹](/help/forms/using/creating-configure-watched-folder.md)。
* **配置Forms App脱机服务：** AEM [!DNL Forms] App脱机服务缓存表单中使用的资源的路径或URL。 缓存表单中使用的资源的路径或URL可提高服务器端性能。 要配置AEM Forms应用程序的服务器端脱机组件，请参阅[在脱机模式下工作](/help/forms/using/work-offline-mode.md)。

  ![AEM Forms工具](assets/aem_forms_tools_new.png)

* **配置PDF Generator：**&#x200B;管理员可以配置AEM [!DNL Forms] PDF Generator设置、添加用户帐户，以及将配置导入或导出到PDF Generator。
* **发布通信管理Assets：** AEM [!DNL Forms]允许您同时发布来自创作实例的所有字母、文档片段和数据字典以及相关依赖项。 已发布的资产包括所有相应的管理资产和相关依赖项。 有关详细信息，请参阅[发布和取消发布表单和文档](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)。
* **导出通信管理Assets：**&#x200B;您可以从AEM [!DNL Forms]实例以包形式下载所有通信管理资源和相关依赖项。 有关详细步骤，请参阅[将资产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 用户界面的常见元素 {#commonelements}

* **左边栏：**&#x200B;您可以单击左边栏图标![railleftpng](assets/railleftpng.png)以显示AEM [!DNL Forms]的时间轴和引用功能。

   * **时间线：**&#x200B;您可以添加和查看可在时间线中审阅的资产评论。 有关详细说明，请参阅[创建和管理表单中资产的审核](../../forms/using/create-reviews-forms.md)。
   * **引用：** AEM [!DNL Forms]资源可用于多个AEM [!DNL Forms]资源。 例如，一个文档片段可以在多个字母中使用。 引用是所选资产使用的资产（其他表单或资源）列表，也是所选资产正在使用的其他资产列表。

* **痕迹导航：**&#x200B;痕迹导航表示当前控制台或文件夹的标题。 您可以单击痕迹导航选项在层次结构中较高级别的文件夹之间导航。
* **视图切换器：**&#x200B;您可以单击“视图切换器”图标![viewlist](assets/viewlist.png)或![viewcard](assets/viewcard.png)在列表视图和卡片视图之间快速切换。 有关常见用户界面组件的详细信息，请参阅[创作](/help/sites-authoring/author.md)。
* **搜索：**&#x200B;搜索选项![搜索](assets/search.png)提供快速查找和跳转到所需内容和工具的功能。 键入内容或产品功能的名称，并从建议中进行选择，例如，键入“文档”可快速查找并导航到&#x200B;**[!UICONTROL Forms和文档]**&#x200B;或文档片段控制台。 有关搜索的详细信息，请参阅AEM 6.2 [搜索](/help/sites-authoring/search.md)文章

* **操作工具栏**：选择资源时，操作工具栏显示在资源列表上方。 它包含选定资产的所有管理工具。 您可以将鼠标悬停在工具图标上以查看描述其功能的工具提示

>[!NOTE]
>
>当用户搜索Forms和文档的任意控制台时，边栏仅包含&#x200B;**筛选器和选项**。 您可以使用“筛选器和选项”来执行高级搜索。

* **操作工具栏**：选择资源时，操作工具栏显示在资源列表上方。 它包含选定资产的所有管理工具。 您可以将鼠标悬停在工具图标上以查看描述其功能的工具提示

  自适应表单的![操作工具栏](assets/action_toolbar_new.png)

  自适应表单的操作工具栏
