---
title: 为自适应表单生成记录文档
description: 介绍如何为自适应表单生成记录文档(DoR)。
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 2d9ec8c4-330e-4474-97f4-1f434025683f
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '4283'
ht-degree: 3%

---

# 为自适应表单或自适应表单片段生成记录文档 {#generate-document-of-record-for-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |


## 概述 {#overview}

提交表单后，您的客户通常希望以打印或文档格式记录他们在表单中填写的信息，以供将来参考。 这称为记录文档。

本文介绍了如何为自适应Forms或自适应表单片段生成记录文档。

>[!NOTE]
>
>基于XFA的自适应表单不支持自动生成记录文档。 但是，您可以使用用于创建自适应表单作为记录文档的XDP。

## 自适应表单类型及其记录文档 {#adaptive-form-types-and-their-documents-of-record}

创建自适应表单时，可以选择表单模型。 您的选项包括：

* [表单模板](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
允许您为自适应表单选择XFA模板。 当您选择XFA模板时，可以为记录文档使用关联的XDP文件，如上所述。

* [XML架构](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
允许您为自适应表单选择XML架构定义。 在为自适应表单选择XML架构时，您可以：

   * 为记录文档关联XFA模板。 确保关联的XFA模板使用与您的自适应表单相同的XML架构
   * 自动生成记录文档

* 无
允许您创建没有表单模型的自适应表单。 系统会自动为您的自适应表单生成记录文档。

选择表单模型时，使用记录文档模板配置下可用的选项配置记录文档。 请参阅[记录文档模板配置](#document-of-record-template-configuration)。

## 自动生成记录文档 {#automatically-generated-document-of-record}

记录文档允许客户保留已提交表单的副本以进行打印。 当您自动生成记录文档时，每次更改表单时，其记录文档都会立即更新。 例如，对于选择美利坚合众国作为其国家/地区的客户，您将删除年龄字段。 当此类客户生成记录文档时，他们在记录文档中看不到年龄字段。

自动生成的记录文档具有以下优点：

* 它负责数据绑定。
* 它会自动隐藏在提交时标记为从记录文档中排除的字段。 无需额外工作。
* 本发明为记录文档模板的设计节省了时间。
* 它允许您使用不同的基本模板尝试不同的样式和外观，并为记录文档选择最佳的样式和外观。 样式外观是可选的，如果未指定样式，系统样式将设置为缺省值。
* 它确保表单中的任何更改都立即反映在记录文档中。

## 自动生成记录文档的组件 {#components-to-automatically-generate-a-document-of-record}

要为自适应表单生成记录文档，您需要以下组件：

**自适应表单**&#x200B;要为其生成记录文档的自适应表单。

**要为其生成记录文档的自适应表单片段**。

在AEM Designer中创建的&#x200B;**基本模板（推荐）** XFA模板（XDP文件）。 基本模板用于指定记录文档模板的样式和品牌信息。

查看记录文档的[基本模板](#base-template-of-a-document-of-record)

>[!NOTE]
>
>记录文档的基础模板也称为记录文档的元模板。

从自适应表单生成的&#x200B;**记录文档模板** XFA模板（XDP文件）。

请参阅[记录文档模板配置](#document-of-record-template-configuration)。

**表单数据**&#x200B;用户在自适应表单中填写的信息。 它与记录文档模板合并以生成记录文档。

## 自适应表单元素映射 {#mapping-of-adaptive-form-elements}

以下各节介绍自适应表单元素在记录文档中的显示方式。

### 字段 {#fields}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>对应的XFA组件</th>
   <th>默认情况下包含在记录文档模板中？</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>按钮</td>
   <td>按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td>复选框</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td>日期/时间字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>下拉列表</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>潦草签名</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>数值框</td>
   <td>数值字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密码框</td>
   <td>密码字段</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td>单选按钮</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文本字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>重置按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>“提交”按钮</td>
   <td><p>电子邮件提交按钮</p> <p>HTTP提交按钮</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>条款和条件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td> </td>
   <td>false</td>
   <td>在记录文档模板中不可用。 仅通过附件在记录文档中可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>对应的XFA组件</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表单<br /> </td>
   <td>可重复面板映射到可重复的子表单。</td>
  </tr>
 </tbody>
</table>

### 静态组件 {#static-components}

| 自适应表单组件 | 对应的XFA组件 | 注释 |
|---|---|---|
| 图像 | 图像 | 除非使用记录文档设置进行排除，否则TextDraw和Image组件（无论已绑定还是未绑定）始终显示在基于XSD的自适应表单的记录文档中。 |
| 文本 | 文本 |

>[!NOTE]
>
>在经典UI中，您获得不同的选项卡用于编辑字段属性。

### 表 {#tables}

自适应表单表组件（如页眉、页脚和行）映射到相应的XFA组件。 您可以将可重复面板映射到记录文档中的表格。

## 记录文档的基础模板 {#base-template-of-a-document-of-record}

基本模板为记录文档提供样式和外观信息。 它允许您自定义自动生成记录文档的默认外观。 例如，您希望在记录文档的页眉中添加公司徽标，在页脚中添加版权信息。 基础模板中的母版页用作记录文档模板的母版页。 母版页可以包含可应用于记录文档的页眉、页脚和页码等信息。 您可以使用基本模板将此类信息应用于记录文档，以自动生成记录文档。 使用基本模板可以更改字段的默认属性。

在设计基本模板时，请确保遵循[基本模板约定](#base-template-conventions)。

## 基本模板约定 {#base-template-conventions}

基本模板用于定义记录文档的页眉、页脚、样式和外观。 页眉和页脚可以包含公司徽标和版权文本等信息。 基础模板中的第一个母版页被复制并用作记录文档的母版页，该母版页包含页眉、页脚、页码或应在记录文档的所有页面上显示的任何其他信息。 如果使用的基础模板不符合基础模板约定，则基础模板中的第一个母版页仍用于记录文档模板中。 强烈建议您按照其约定设计基础模板，并将其用于自动生成记录文档。

**母版页惯例**

* 在基础模板中，应将根子表单命名为`AF_METATEMPLATE`，将母版页命名为`AF_MASTERPAGE`。

* 名为`AF_MASTERPAGE`的母版页位于`AF_METATEMPLATE`根子表单下，该母版页具有提取页眉、页脚和样式信息的首选项。

* 如果`AF_MASTERPAGE`不存在，则使用基本模板中存在的第一个母版页。

**字段的样式约定**

* 要对记录文档中的字段应用样式，基础模板在`AF_METATEMPLATE`根子表单下的`AF_FIELDSSUBFORM`子表单中提供字段。

* 这些字段的属性应用于记录文档中的字段。 这些字段应遵循`AF_<name of field in all caps>_XFO`命名约定。 例如，复选框的字段名称应为`AF_CHECKBOX_XFO`。

要创建基本模板，请在AEM Designer中执行以下操作。

1. 单击&#x200B;**文件>新建**。
1. 选择&#x200B;**基于模板**&#x200B;选项。

1. 选择&#x200B;**Forms — 记录文档**&#x200B;类别。
1. 选择&#x200B;**DoR基本模板**。
1. 单击&#x200B;**下一步**&#x200B;并提供所需信息。

1. （可选）修改要应用于记录文档中的字段的样式和外观。
1. 保存表单。

您现在可以将保存的表单用作记录文档的基础模板。
请勿修改或删除基本模板中存在的任何脚本。

**正在修改基模板**

* 如果您没有对基础模板中的字段应用任何样式，则建议从基础模板中删除这些字段，以便自动选取对基础模板的任何升级。
* 修改基本模板时，请勿删除、添加或修改脚本。

>[!NOTE]
>
>使用约定并严格遵循上述步骤设计基础模板。

## 记录文档模板配置 {#document-of-record-template-configuration}

配置表单的记录文档模板，让客户下载已提交表单的打印友好副本。 XDP文件用作记录文档模板。 客户下载的记录文档根据XDP文件中指定的布局进行格式设置。

执行以下步骤为自适应表单配置记录文档：

1. 在AEM创作实例中，单击&#x200B;**Forms > Forms和文档。**
1. 选择表单，然后单击&#x200B;**查看属性**。
1. 在“属性”窗口中，选择&#x200B;**表单模型**。
您还可以在创建表单时选择表单模型。

   >[!NOTE]
   >
   >在“表单模型”选项卡中，确保从&#x200B;**选择自**&#x200B;下拉列表中选择&#x200B;**架构**&#x200B;或&#x200B;**无**。 **[!UICONTROL 不支持将表单模板作为表单模型的基于XFA的表单或自适应表单的记录文档。]**

1. 在“表单模型”选项卡的“记录文档模板配置”部分中，选择以下选项之一：

   **无**&#x200B;如果不想为表单配置记录文档，请选择此选项。

   **将表单模板关联为记录文档模板**&#x200B;如果您有要用作记录文档模板的XDP文件，请选择此选项。 选择此选项时，将显示AEM Forms存储库中可用的所有XDP文件。 选择相应的文件。

   选定的XDP文件与自适应表单关联。

   **生成记录文档**&#x200B;选择此选项可使用XDP文件作为基础模板来定义记录文档的样式和外观。 选择此选项时，将显示AEM Forms存储库中可用的所有XDP文件。 选择相应的文件。

   >[!NOTE]
   >
   >确保在以下情况下用于创建自适应表单的架构与XFA表单的架构（数据架构）相同：
   >
   >
   >
   >    * 您的自适应表单基于架构
   >    * 您正在使用&#x200B;**关联表单模板作为记录文档的文档模板**&#x200B;选项
   >
   >

1. 单击&#x200B;**完成。**

## 自定义记录文档中的品牌信息 {#customize-the-branding-information-in-document-of-record}

生成记录文档时，您可以在记录文档选项卡上更改记录文档的品牌信息。 “记录文档”选项卡包括如下选项：徽标、外观、布局、页眉和页脚、免责声明，以及是否包括未选定的复选框和单选按钮选项。

要将您在“记录文档”选项卡中输入的品牌信息本地化，您需要确保正确设置浏览器的区域设置。 要自定义记录文档的品牌信息，请完成以下步骤：

1. 在记录文档中选择面板（根面板），然后选择![配置](assets/configure.png)。
1. 选择![dortab](/help/forms/using/assets/dortab.png)。 此时将显示记录文档选项卡。
1. 选择用于呈现记录文档的默认模板或自定义模板。 如果选择默认模板，则记录文档的缩略图预览将显示在“模板”下拉列表下方。

   ![brandingtemplate](/help/forms/using/assets/brandingtemplateupdate.png)

   如果选择选择自定义模板，请在AEM Forms服务器上浏览并选择XDP。 如果要使用AEM Forms服务器上尚未存在的模板，则需要先将XDP上传到AEM Forms服务器。

### 母版页属性(#master-page-properties)

根据您是选择默认模板还是自定义模板，以下部分或全部母版页属性将显示在“记录文档”选项卡中，如上图所示。 请适当指定以下内容：

* **徽标图像**：您可以选择使用自适应表单中的徽标图像、从DAM中选择徽标图像，或者从您的计算机上传徽标图像。
* **表单标题**
* **标题文本**
* **免责声明标签**
* **免责声明**
* **免责声明文本**

  <!--
    * **Accent Color**: The color in which header text and separator lines are rendered in the document or record PDF
    * **Font Family**: Font family of the text in the document of record PDF
    * **For Check Box and Radio Button components, show only the selected values**
    * **Separator for multiple selected value(s)**
    * **Include form objects that are not bound to data model**
    * **Exclude hidden fields from the document of record**
    * **Hide description of panels**
    -->

  如果您选择的自定义XDP模板包含多个母版页，则这些页面的属性将显示在&#x200B;**[!UICONTROL 记录文档]**&#x200B;选项卡的&#x200B;**[!UICONTROL 内容]**&#x200B;部分中。

  ![母版页属性](assets/master-page-properties.png)

  母版页属性包括徽标图像、页眉文本、表单标题、免责声明标签和免责声明文本。 您可以将自适应表单或XDP模板属性应用于记录文档。 默认情况下，AEM Forms将模板属性应用于记录文档。 您还可以定义母版页属性的自定义值。 有关如何在记录文档中应用多个母版页的信息，请参阅[将多个母版页应用到记录文档](#apply-multiple-master-pages-dor)。

  >[!NOTE]
  >
  >如果您使用的是使用Designer 6.3之前的版本创建的自适应表单模板，为了使重色和字体系列属性正常工作，请确保根子表单下的自适应表单模板中存在以下内容：

  ```xml
  <proto>
  <font typeface="Arial"/>
  <fill>
  <color value="4,166,203"/>
  </fill>
  <edge>
  <color value="4,166,203"/>
  </edge>
  </proto>
  ```

1. 要保存品牌策略更改，请选择“完成”。

## 记录文档中面板的表格和列布局 {#table-and-column-layouts-for-panels-in-document-of-record}

您的自适应表单可能很长，包含多个表单字段。 您可能不希望将记录文档另存为自适应表单的精确副本。 现在，您可以选择表格或列布局来将一个或多个自适应表单面板保存在记录文档PDF中。

在生成记录文档之前，在面板的设置中，选择该面板的记录文档的布局（表格或列）。 面板中的字段将在记录文档中相应组织。

![在记录文档中以表布局呈现的面板中的字段](assets/dortablelayout.png)

面板中的字段在记录文档中的表布局中渲染

![在记录文档中以列布局呈现的面板中的字段](assets/dorcolumnlayout.png)

面板中的字段在记录文档的列布局中渲染

## 记录文档设置 {#document-of-record-settings}

记录文档设置允许您选择要包含在记录文档中的选项。 例如，银行接受表单中的姓名、年龄、社会保险号码和电话号码。 该表单会生成银行帐号和分行详细信息。 您可以选择在记录文档中仅显示名称、社会保险编号、银行帐户和分行详细信息。

组件的记录文档设置位于其属性下。 要访问组件的属性，请选择该组件并在叠加中单击![cmppr](assets/cmppr.png)。 这些属性列在侧边栏中，您可以在该侧边栏中找到以下设置。

**字段级设置**

* **从记录文档排除**：将属性设置为true会从记录文档排除该字段。 这是名为`excludeFromDoR`的可编写脚本的属性。 其行为取决于&#x200B;**如果隐藏**&#x200B;表单级属性，则从DoR中排除字段。

* **将面板显示为表：**&#x200B;如果面板中的字段少于6个，则将属性设置为将面板显示为记录文档中的表。 仅适用于面板。
* **从记录文档排除标题：**&#x200B;设置属性会从记录文档排除面板/表的标题。 仅适用于面板和表格。
* **从记录文档排除描述：**&#x200B;设置属性从记录文档排除面板/表的描述。 仅适用于面板和表格。
* **[!UICONTROL 分页]** > **[!UICONTROL 放置]**：确定您选择放置面板的位置。
   * **[!UICONTROL 置入]** > **[!UICONTROL 置于上一项]**：将面板置于父面板中上一对象的后面。
   * **[!UICONTROL 放置]** > **[!UICONTROL 在内容区域中]** >内容区域的名称：将面板放置在指定的内容区域中。
   * **[!UICONTROL 放置]** > **[!UICONTROL 位于下一个内容区域的顶部]**：将面板置于下一个内容区域的顶部。
   * **[!UICONTROL 放置]** > **[!UICONTROL 内容区域顶部]** >内容区域名称：将面板放置在指定内容区域的顶部。
   * **[!UICONTROL 放置]** > **[!UICONTROL 在页面上]** >母版页的名称：将面板放置在指定的页面上。 如果未自动插入分页符，[!DNL AEM Forms]将添加分页符。
   * **[!UICONTROL 置入]** > **[!UICONTROL 下一页顶部]**：将面板置于下一页顶部。 如果未自动插入分页符，[!DNL AEM Forms]将添加分页符。
   * **[!UICONTROL 置入]** > **[!UICONTROL 页面顶部]** >母版页的名称：呈现指定的页面时，将面板置于页面顶部。 如果未自动插入分页符，[!DNL AEM Forms]将添加分页符。
* **[!UICONTROL 分页]** > **[!UICONTROL After]**：确定放置面板后要填充的区域。**[!UICONTROL After]**&#x200B;部分中有以下字段：
   * **[!UICONTROL After]** > **[!UICONTROL 继续填充父项]**：继续合并父面板中剩余要填充的所有对象的数据。
   * **[!UICONTROL After]** > **[!UICONTROL 转到下一个内容区域]**：在放置面板后开始填充下一个内容区域。
   * **[!UICONTROL After]** > **[!UICONTROL 转到内容区域]** >内容区域名称：在放置面板后开始填充指定的内容区域。
   * **[!UICONTROL After]** > **[!UICONTROL 转到下一页]**：在放置面板后开始填充下一页。
   * **[!UICONTROL After]** > **[!UICONTROL 转到页面]** >页面名称：在放置面板后开始填充指定的页面。
* **[!UICONTROL 分页]** > **[!UICONTROL 溢出]**：为跨页面的面板或表设置溢出。 **[!UICONTROL 溢出]**&#x200B;部分中有以下字段可用：
   * **[!UICONTROL 溢出]** > **[!UICONTROL 无]**：开始填充下一页。 如果未自动插入分页符，[!DNL AEM Forms]将添加分页符。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 转到内容区域]** >内容区域的名称：开始填充指定的内容区域。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 转到页面]** >页面名称：开始填充指定的页面。

  >[!NOTE]
  >
  > 分页属性不可用于自适应表单片段。

有关如何在记录文档中应用分页符和应用多个母版页的信息，请参阅[在记录文档中应用分页符](#apply-page-breaks-in-dor)和[将多个母版页应用于记录文档](#apply-multiple-master-pages-dor)。

**表单级别设置**

* **[!UICONTROL 基本]**
   * **模板：**&#x200B;您可以选择“默认”或“自定义”模板。

     ![替换文本](image.png)
   * **个性色：**&#x200B;您可以预定义[!UICONTROL 记录文档]的模板颜色。
   * **字体系列：**&#x200B;为[!UICONTROL 记录文档]文本选择字体类型。
   * **包括DoR中未绑定的字段：**&#x200B;设置属性包括来自[!UICONTROL 记录文档]中基于架构的自适应表单的未绑定字段。 默认情况下，它为true。
   * **隐藏时从DoR中排除字段：**&#x200B;设置属性以在提交表单时从[!UICONTROL 记录文档]中排除隐藏字段。 在服务器[&#128279;](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)上启用重新验证时，服务器会重新计算隐藏字段，然后再从[!UICONTROL 记录文档]中排除这些字段
* **[!UICONTROL 表单字段属性]**
   * 如果勾选选项&#x200B;**对于复选框和单选按钮组件，则仅显示选定的值**，它将生成仅具有选定值的DoR输出。
   * 可以为多个选定值选择分隔符，也可以选择任何其他分隔符类型。
   * 选项对齐
      * 垂直
      * 水平
      * 与自适应表单相同

     >[!NOTE]
     > 垂直对齐和水平对齐仅适用于以下情况     单选按钮和复选框
* **[!UICONTROL 母版页属性]**&#x200B;有关[母版页属性](#master-page-properties-master-page-properties)的详细信息，请单击

## 在记录文档中应用分页符 {#apply-page-breaks-in-dor}

您可以使用多种方法在记录文档中应用分页符。

要将分页符应用于记录文档，请执行以下操作：

1. 选择面板并选择![配置](/help/forms/using/assets/configure.png)
1. 展开&#x200B;**[!UICONTROL 记录文档]**&#x200B;以查看属性。

1. 在&#x200B;**[!UICONTROL 分页]**&#x200B;分区中，在&#x200B;**[!UICONTROL 放置]**&#x200B;字段中选择![文件夹](/help/forms/using/assets/folder-icon.png)。
1. 选择&#x200B;**[!UICONTROL 下一页顶部]**&#x200B;并选择&#x200B;**[!UICONTROL 选择]**。 您还可以选择&#x200B;**[!UICONTROL 页面顶部]**，选择母版页，然后选择&#x200B;**[!UICONTROL 选择]**&#x200B;以应用分页符。
1. 选择![保存](/help/forms/using/assets/save_icon.png)以保存属性。

所选面板将移至下一页。

## 将多个母版页应用于记录文档 {#apply-multiple-master-pages-dor}

如果您选择的自定义XDP模板包含多个母版页，则这些页面的属性将显示在[!UICONTROL 记录文档]选项卡的[!UICONTROL 内容]部分中。 有关详细信息，请参阅[自定义记录文档](#customize-the-branding-information-in-document-of-record)中的品牌信息。

通过将不同的母版页应用于自适应表单的组件，可以将多个母版页应用于记录文档。 使用记录文档属性的[分页](#document-of-record-settings)部分以应用多个母版页。

以下是如何将多个母版页应用于记录文档的示例：
将包含四个母版页的XDP模板上载到[!DNL AEM Forms]服务器。 默认情况下，[!DNL AEM Forms]将模板属性应用于记录文档。 [!DNL AEM Forms]还将模板中的第一个母版页属性应用于记录文档。

要将第二个母版页属性应用于面板，而将第三个母版页属性应用于后续面板，请执行以下步骤：

1. 选择要应用第二个母版页的面板，然后选择![配置](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 分页]**&#x200B;分区中，在&#x200B;**[!UICONTROL 放置]**&#x200B;字段中选择![文件夹](/help/forms/using/assets/folder-icon.png)。
1. 选择&#x200B;**[!UICONTROL 在页面]**&#x200B;上，选择第二个母版页并选择&#x200B;**[!UICONTROL 选择]**。
AEM Forms将第二个母版页应用于自适应表单中的面板和所有后续面板。
1. 在&#x200B;**[!UICONTROL 分页]**&#x200B;分区中，在&#x200B;**[!UICONTROL After]**&#x200B;字段中选择![文件夹](/help/forms/using/assets/folder-icon.png)。
1. 选择&#x200B;**[!UICONTROL 转到页面]**，选择第三个母版页，然后选择&#x200B;**[!UICONTROL 选择]**。
1. 选择![保存](/help/forms/using/assets/save_icon.png)以保存属性。
AEM Forms将第三个母版页应用于自适应表单中的面板和所有后续面板。

>[!NOTE]
>
> 您无法将多个母版页应用于自适应表单片段的记录文档。

## 使用记录文档时的主要注意事项 {#key-considerations-when-working-with-document-of-record}

处理自适应表单的记录文档时，请牢记以下注意事项和限制。

* 记录文档模板不支持富文本。 因此，任何富文本在静态自适应表单中或者由最终用户填写的信息中都会以纯文本的形式出现在记录文档中。
* 自适应表单中的文档片段未出现在记录文档中。 但是，支持自适应表单片段。
* 不支持为基于XML架构的自适应表单生成的记录文档中的内容绑定。
* 当用户请求呈现记录文档时，记录文档的本地化版本是应区域设置的要求创建的。 记录文档的本地化与自适应表单的本地化同时发生。 有关本地化记录文档和自适应表单的详细信息，请参阅[使用AEM翻译工作流本地化自适应表单和记录文档](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

## 使用自定义XCI文件

XCI文件可帮助您设置文档的各种属性。 <!-- Forms as a Cloud Service has a master XCI file.-->您可以使用自定义XCI文件覆盖在现有XCI文件中指定的一个或多个默认属性。 例如，您可以选择将字体嵌入文档，或者为所有文档启用标记属性。 下表指定了XCI选项：

| XCI选项 | 描述 |
|--- |--- |
| config/present/pdf/creator | 使用文档信息词典中的创建者条目标识文档创建者。 有关此词典的信息，请参阅[PDF参考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/pdf/producer | 使用文档信息词典中的制作者条目标识文档制作者。 有关此词典的信息，请参阅[PDF参考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/layout | 控制输出是单个面板还是分页。 |
| config/present/pdf/compression/level | 指定生成PDF文档时使用的压缩程度。 |
| config/present/pdf/fontInfo/embed | 控制输出文档中的字体嵌入。 |
| config/present/pdf/scriptModel | 控制输出PDF文档中是否包含XFA特定的信息。 |
| config/present/common/data/adjustData | 控制XFA应用程序在合并后是否调整数据。 |
| config/present/pdf/renderPolicy | 控制页面内容的生成是在服务器上完成还是延迟到客户端。 |
| config/present/common/locale | 指定输出文档中使用的默认区域设置。 |
| config/present/destination | 当由当前元素包含时，指定输出格式。 当由openAction元素包含时，指定在交互式客户端中打开文档时要执行的操作。 |
| config/present/output/type | 指定要应用于文件的压缩类型或要生成的输出类型。 |
| config/present/common/temp/uri | 指定表单URI。 |
| config/present/common/template/base | 在表单设计中提供URI的基本位置。 当此元素不存在或为空时，将使用窗体设计的位置作为基础。 |
| config/present/common/log/to | 控制日志数据或输出数据写入的位置。 |
| config/present/output/to | 控制日志数据或输出数据写入的位置。 |
| config/present/script/currentPage | 指定文档打开时的初始页面。 |
| config/present/script/exclude | 告知Forms as a Cloud Service要忽略哪些事件。 |
| config/present/pdf/linearized | 控制输出PDF文档是否线性化。 |
| config/present/script/runScripts | 控制Forms as a Cloud Service执行的脚本集。 |
| config/present/pdf/tagged | 控制是否在输出的PDF文档中包含标记。 在PDF上下文中，标记是文档中包含的其他信息，用于公开文档的逻辑结构。 标记有助于辅助功能和重新设置格式。 例如，页码可能会被标记为工件，这样屏幕阅读器就不会在文本中间朗读它。 虽然标记可以使文档更有用，但它们也会增加文档的大小以及创建文档所需的处理时间。 |
| config/present/pdf/fontInfo/alwaysEmbed | 指定嵌入到输出文档中的字体。 |
| config/present/pdf/fontInfo/neverEmbed | 指定不得嵌入到输出文档中的字体。 |
| config/present/pdf/pdfa/part | 指定文档遵循的PDF/A规范的版本号。 |
| config/present/pdf/pdfa/amd | 指定PDF/A规范的修订级别。 |
| config/present/pdf/pdfa/conformance | 指定与PDF/A规范的一致性级别。 |
| config/present/pdf/version | 指定要生成的PDF文档的版本 |
| config/present/pdf/version/map | 指定文档的回退字体 |


<!--

### Use a custom XCI file in your AEM Forms environment

  1. Add the custom XCI file to your development project.
  1. Specify the following inline property:(/help/implementing/deploying/configuring-osgi.md)
  1. Deploy the project to your AEM Forms environment. <!--Cloud Service environment
  
-->

### 在本地Forms开发环境中使用自定义XCI文件

1. 将XCI文件上传到本地开发环境。
1. 打开<!--Cloud Service SDK-->配置管理器。<!--The default URL is: <http://localhost:4502/system/console/configMgr>.-->
1. 找到并打开&#x200B;**[!UICONTROL 自适应Forms和交互式通信Web渠道]**&#x200B;配置。
1. 指定XCI文件的路径，然后单击&#x200B;**[!UICONTROL 保存]**。
