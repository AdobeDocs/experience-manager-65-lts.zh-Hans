---
title: AEM Forms工作流中的变量
description: 创建一个变量，为该变量设置值，然后在AEM Forms工作流步骤中使用它。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 1a0d00f9-45f7-45af-ab34-d1c164980abb
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 1%

---

# AEM Forms工作流中的变量{#variables-in-aem-forms-workflows}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/variable-in-aem-workflows.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

工作流模型中的变量是一种根据其数据类型存储值的方法。 然后，可以在任何工作流步骤中使用变量的名称来检索存储在变量中的值。 您还可以使用变量名称来定义用于制定路由决策的表达式。

在AEM工作流模型中，您可以：

* [根据要存储的信息类型创建数据类型的变量](../../forms/using/variable-in-aem-workflows.md#create-a-variable)。
* [使用“设置变量”工作流步骤设置变量](../../forms/using/variable-in-aem-workflows.md#set-a-variable)的值。
* [在所有AEM Forms工作流步骤中使用变量](../../forms/using/variable-in-aem-workflows.md#use-a-variable)来检索存储的值，并在OR拆分和转到步骤中定义路由表达式。

变量是现有[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)接口的扩展。 您可以在ECMAScript中使用[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)访问使用变量保存的元数据。

## 创建变量 {#create-a-variable}

您可以使用工作流模型Sidekick中提供的“变量”部分创建变量。 AEM工作流变量支持以下数据类型：

* **原始数据类型**： Long、Double、Boolean、Date和String
* **复杂数据类型**： [文档](https://helpx.adobe.com/cn/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html)、[XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html)、[JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)和表单数据模型实例。

>[!NOTE]
>
>工作流仅支持使用ISO8601格式作为日期类型变量。

文档和表单数据模型数据类型需要[AEM Forms加载项包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。  使用ArrayList数据类型创建变量集合。 您可以为所有基元和复杂数据类型创建ArrayList变量。 例如，创建一个ArrayList变量并选择String作为子类型以使用该变量存储多个字符串值。

执行以下步骤可创建变量：

1. 在AEM实例上，导航到工具![工具](/help/forms/using/assets/hammer.png) >工作流>模型。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;并指定工作流模型的标题和可选名称。 选择模型并选择&#x200B;**[!UICONTROL 编辑]**。
1. 选择工作流模型Sidekick中可用的变量图标，然后选择&#x200B;**[!UICONTROL 添加变量]**。

   ![添加变量](assets/variables_add_variable_new.png)

1. 在添加变量对话框中，指定变量名称并选择变量类型。
1. 从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择数据类型，并指定以下值：

   * 原始数据类型 — 为变量指定可选的默认值。
   * JSON或XML — 指定可选的JSON或XML架构路径。 系统将此架构中可用的属性映射并存储到其他变量时，验证架构路径。
   * 表单数据模型 — 指定表单数据模型路径。
   * ArrayList — 指定集合的子类型。

1. 为变量指定可选描述，然后选择![done_icon](assets/done_icon.png)以保存更改。 变量将显示在左侧窗格中可用的列表中。

创建变量时，请考虑以下实践：

* 根据工作流程的要求创建任意数量的变量。 但是，要节约数据库资源，请使用所需的最少变量数，并在可能的情况下重复使用变量。
* 变量区分大小写。 确保在工作流程中使用相同的大小写引用变量。
* 避免在变量的名称中使用特殊字符

## 设置变量 {#set-a-variable}

您可以使用“设置变量”步骤来设置变量的值，并定义值的设置顺序。 变量按照变量映射在设置变量步骤中列出的顺序进行设置。

对变量值所做的更改只会影响发生更改的进程实例。 例如，在启动工作流并更改变量数据时，所做的更改仅影响工作流的该实例。 这些更改不会影响先前启动或随后启动的工作流的其它实例。

根据变量的数据类型，您可以使用以下选项设置变量的值：

* **文本：**&#x200B;当您知道要指定的确切值时，请使用选项。

* **表达式：**&#x200B;根据表达式计算要使用的值时，请使用选项。 表达式是在提供的表达式编辑器中创建的。

* **JSON点表示法：**&#x200B;使用选项从JSON或FDM类型变量中检索值。
* **XPATH：**&#x200B;使用选项从XML类型变量中检索值。

* **相对于有效负载：**&#x200B;当要保存到变量的值在相对于有效负载的路径上可用时，请使用选项。

* **绝对路径：**&#x200B;当要保存到变量的值在绝对路径上可用时，请使用选项。

您还可以使用JSON点表示法或XPATH表示法更新JSON或XML类型变量的特定元素。

### 添加变量之间的映射 {#add-mapping-between-variables}

执行以下步骤来添加变量之间的映射：

1. 在工作流编辑页面上，选择工作流模型Sidekick中可用的步骤图标。
1. 将&#x200B;**设置变量**&#x200B;步骤拖放到工作流编辑器中，选择该步骤并选择![configure_icon](assets/configure_icon.png) （配置）。
1. 在设置变量对话框中，选择&#x200B;**[!UICONTROL 映射]** > **[!UICONTROL 添加映射]**。
1. 在&#x200B;**映射变量**&#x200B;部分中，选择要存储数据的变量，选择映射模式，然后指定要在变量中存储的值。 映射模式因变量类型而异。
1. 映射更多变量以生成有意义的表达式。 选择![done_icon](assets/done_icon.png)以保存更改。

### 示例1：查询XML变量以设置字符串变量的值 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

选择XML类型的变量以存储XML文件。 查询XML变量以为XML文件中可用的属性设置字符串变量的值。 使用&#x200B;**为XML变量**&#x200B;字段指定XPATH来定义要存储在字符串变量中的属性。

在此示例中，选择一个&#x200B;**formdata** XML变量来存储&#x200B;**cc-app.xml**&#x200B;文件。 查询&#x200B;**formdata**&#x200B;变量以设置&#x200B;**emailaddress**&#x200B;字符串变量的值，以存储&#x200B;**cc-app.xml**&#x200B;文件中可用的&#x200B;**emailAddress**&#x200B;属性的值。

### 示例2：使用表达式存储基于其他变量的值 {#example2}

使用表达式计算变量的总和并将结果存储在变量中。

在此示例中，使用表达式编辑器定义表达式以计算&#x200B;**assetscost**&#x200B;和&#x200B;**balanceamount**&#x200B;变量的总和，并将结果存储在&#x200B;**totalvalue**&#x200B;变量中。

## 使用表达式编辑器 {#use-expression-editor}

您还可以在运行时使用表达式计算变量的值。 变量提供用于定义表达式的表达式编辑器。

使用表达式编辑器可以：

* 使用其他工作流变量、数字或数学表达式设置变量的值。
* 在数学表达式中使用工作流变量、字符串、数字或表达式
* 添加条件以设置变量的值。
* 在条件之间添加运算符。

![表达式编辑器](assets/variables_expression_editor_new.png)

它基于自适应表单规则编辑器，具有下列更改。 变量中的规则编辑器：

* 不支持函数。
* 不提供查看规则摘要的UI
* 没有代码编辑器。
* 不支持启用和禁用对象的值。
* 不支持设置对象的属性。
* 不支持调用Web服务。

有关详细信息，请参阅[自适应表单规则编辑器](../../forms/using/rule-editor.md)。

## 使用变量 {#use-a-variable}

可使用变量检索输入和输出或保存步骤的结果。 工作流编辑器提供两种类型的工作流步骤：

* 支持变量的工作流步骤
* 不支持变量的工作流步骤

### 支持变量的工作流步骤 {#workflow-steps-with-support-for-variables}

转到步骤、OR拆分步骤以及所有AEM Forms工作流步骤都支持变量。

#### OR拆分步骤 {#or-split-step}

OR拆分在工作流中创建拆分，之后只有一个分支处于活动状态。 此步骤允许您将条件处理路径引入工作流。 您可以根据需要将工作流步骤添加到每个分支。

您可以使用规则定义、ECMA脚本或外部脚本为分支定义路由选择表达式。

可以使用变量来定义使用表达式编辑器的路由选择表达式。 有关对“或拆分”步骤使用路由选择表达式的详细信息，请参阅[或拆分步骤](/help/sites-developing/workflows-step-ref.md#or-split)。

在此示例中，在定义路由选择表达式之前，使用[示例2](../../forms/using/variable-in-aem-workflows.md#example2)设置&#x200B;**totalvalue**&#x200B;变量的值。 如果&#x200B;**totalvalue**&#x200B;变量的值大于50000，则分支1处于活动状态。 同样，如果&#x200B;**totalvalue**&#x200B;变量的值小于50000，可以定义规则使Branch 2处于活动状态。

同样，选择外部脚本路径或指定路由表达式的ECMA脚本以计算活动分支。 选择&#x200B;**[!UICONTROL 重命名分支]**&#x200B;以指定分支的替代名称。

有关更多示例，请参阅[创建工作流模型](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)。

#### 转到步骤 {#go-to-step}

**跳转步骤**&#x200B;允许您根据路由表达式的结果，指定要执行的工作流模型中的下一步。

与OR拆分步骤类似，您可以使用规则定义、ECMA脚本或外部脚本为Goto步骤定义路由表达式。

您可以使用变量来定义使用表达式编辑器的路由表达式。 有关为“转至”步骤使用路由表达式的详细信息，请参阅[转至步骤](/help/sites-developing/workflows-step-ref.md#goto-step)。

![转到规则](assets/variables_goto_rule1_new.png)

在本例中，如果&#x200B;**actiontaked**&#x200B;变量的值等于&#x200B;**需要更多信息**，则“转至”步骤将审核信用卡申请指定为下一个步骤。

有关在“转至”步骤中使用规则定义的更多示例，请参阅[模拟For循环](/help/sites-developing/workflows-step-ref.md#simulateforloop)。

#### 以Forms工作流为中心的工作流步骤 {#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流步骤都支持变量。 有关详细信息，请参阅OSGi上的[以Forms为中心的工作流](../../forms/using/aem-forms-workflow-step-reference.md)。

### 不支持变量的工作流步骤 {#workflow-steps-without-support-for-variables}

您可以使用[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)界面访问工作流步骤中不支持变量的变量。

#### 检索变量值 {#retrieve-the-variable-value}

在ECMA脚本中使用以下API根据数据类型检索现有变量的值：

| 变量数据类型 | API |
|---|---|
| 原始（Long、Double、Boolean、Date和String） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName， type) |
| 文档 | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData()。getMetaDataMap()。get(&quot;docVar&quot;， Packages.com.adobe.aemfd.docmanager.Document.class)； |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.org.w3c.dom.Document.class)； |
| 表单数据模型 | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class)； |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.google.gson.JsonObject.class)； |

文档和表单数据模型变量数据类型需要[AEM Forms附加组件包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。

**示例**

使用以下API检索字符串数据类型的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新变量值 {#update-the-variable-value}

在ECMA脚本中使用以下API来更新变量的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**示例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

将&#x200B;**salary**&#x200B;变量的值更新为50000。

### 设置变量以调用工作流 {#apiinvokeworkflow}

您可以使用API来设置变量，并传递它们以调用工作流实例。

[workflowSession.startWorkflow](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-)使用模型、wfData和metaData作为参数。 使用MetaDataMap设置变量的值。

在此API中，使用metaData.put(variableName， value)将&#x200B;**variableName**&#x200B;变量设置为&#x200B;**value**；

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**示例**

将&#x200B;**doc**&#x200B;文档对象初始化为路径(&quot;a/b/c&quot;)，并将&#x200B;**docVar**&#x200B;变量的值设置为存储在文档对象中的路径。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

### 使用工作流变量在JCR外部存储敏感用户数据 {#jcr-independent-persistance}

使用Forms Workflow处理的数据可能包含敏感用户数据，如个人身份信息和敏感个人信息。 企业可以选择将数据从JCR存储存储存储到它们拥有并管理的外部数据存储中，由各种工作流步骤处理这些数据（并使用工作流变量进行传递）。 若要了解有关在外部存储中保留工作流数据的更多信息，请参阅[将工作流变量用于客户拥有的数据存储](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore)。
[!DNL Adobe Experience Manager]提供工作流API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer)以在外部Azure Blob存储中存储工作流变量。 有关使用API的详细信息，请参阅[使用工作流变量参数化敏感数据并将其存储在外部数据存储中](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)。

## 编辑变量 {#edit-a-variable}

1. 在编辑工作流页面上，选择工作流模型Sidekick中可用的“变量”图标。 左窗格中的变量部分显示所有现有变量。
1. 选择要编辑的变量名称旁边的![编辑](assets/edit.png) （编辑）图标。
1. 编辑变量信息并选择![done_icon](assets/done_icon.png)以保存更改。 您无法编辑变量的&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Type]**&#x200B;字段。

## 删除变量 {#delete-a-variable}

在删除变量之前，请从工作流中删除变量的所有引用。 确保在工作流中未使用变量。

执行以下步骤可删除变量：

1. 在编辑工作流页面上，选择工作流模型Sidekick中可用的“变量”图标。 左侧窗格中的“变量”部分显示所有现有变量。
1. 选择要删除的变量名称旁边的“删除”图标。
1. 选择![done_icon](assets/done_icon.png)以确认并删除该变量。

## 引用 {#references}

有关在AEM Forms工作流程步骤中使用变量的更多示例，请参阅[AEM工作流程中的变量](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html)。
