---
title: 从AEM工作流启动Document Services API
description: 了解如何在DDX或提供的输入上调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: User, Developer
exl-id: 22a7744e-0af6-4aac-a8a1-156b563c627c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 从AEM工作流启动Document Services API  {#initiate-document-services-apis-from-aem-workflow}

## 汇编程序 {#assembler}

AEM Forms提供自定义工作流以调用以下Assembler服务API：

* **invoke**：对提供的输入调用输入DDX中指定的操作。
* **toPDFA**：将输入的PDF文档转换为PDF/A文档。

### 调用DDX工作流 {#invoke-ddx-workflow}

**调用DDX**&#x200B;工作流将调用`Invoke`汇编程序服务API，可用于汇编或分解文档、向PDF添加水印等。

1. 将&#x200B;**[!UICONTROL 调用DDX]**&#x200B;工作流步骤拖动到Sidekick中的“Forms Workflow”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、环境选项和输出文档，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档 {#input-documents}

调用DDX工作流需要以下输入文档：

* **DDX**：它是调用DDX工作流步骤的必需输入，可以通过从DDX输入下拉列表中选择以下选项之一来指定。

   * *相对于有效负荷*： DDX输入文件相对于工作流项的有效负荷文件夹。
   * *使用有效负载*：工作流项目的有效负载用作输入DDX文档。
   * *绝对路径*： CRX存储库中DDX文档的绝对路径。

* **从PayLoad创建映射**：在选中时，有效负荷文件夹下的所有文档都将添加到汇编程序中`invoke` API的输入文档映射中。 每个文档的节点名称在映射中用作键。

* **输入文档的映射**：指定输入文档的映射。 您可以添加任意数量的条目，其中每个条目在映射中指定文档的键和文档的源。

#### 环境选项 {#environment-options}

环境选项选项卡允许您为调用API设置各种处理选项。

* *作业日志级别*：指定处理日志的日志级别。
* *仅验证*：检查输入DDX的有效性。

* *出错时失败*：指定如果出现错误，对Assembler服务的调用是否应失败。 默认值为False。

#### 输出文档 {#output-documents}

根据输入DDX，调用API可以生成多个输出文档。 “输出文档”选项卡允许您选择保存输出文档的位置。

1. *将输出保存在有效负荷中*：将输出文档保存在有效负荷文件夹中，如果有效负荷是文件则覆盖有效负荷。
1. *输出文档的映射*：允许您通过为每个输出文档添加一个条目来明确指定保存每个输出文档的位置。 每个条目都指定文档及其保存位置。 输出文档可能会覆盖有效负载或保存在有效负载文件夹下。 当有多个输出文档时，此插件非常有用。

1. *作业日志*：指定保存作业日志文档的位置，这有助于排除故障。

### 转换为PDF/A工作流 {#convert-to-pdf-a-workflow}

转换到PDF/A工作流步骤将调用`toPDFA`汇编程序服务API。 它用于将PDF文档转换为PDF/A兼容文档。

1. 将&#x200B;**[!UICONTROL ConvertToPDFA]**&#x200B;工作流步骤拖动到Sidekick中“Forms Workflow”选项卡下。

1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、转换选项和输出文档，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档 {#input-documents-1}

通过下列方式之一指定要转换为PDF/A兼容文档的文档源。

* *相对于有效负荷*：输入文档相对于工作流项目的有效负荷文件夹。
* *使用有效负载*：将工作流项目的有效负载用作输入文档。
* *绝对路径*： CRX存储库中输入文档的绝对路径。

#### 转换选项 {#conversion-options}

转化选项允许您指定更改PDF/A转化过程的选项。

* *符合性* ：指定输出PDF/A必须符合的PDF/A标准。
* *结果级别* ：指定要用于PDF/A转换日志的日志级别。
* *签名* ：指定转换期间必须如何处理输入文档中的签名。
* *色彩空间* ：指定要用于输出PDF/A文档的预定义色彩空间。
* *验证*&#x200B;转换：指定转换后的PDF/A文档在转换后是否应验证PDF/A的合规性。
* *作业日志级别* ：指定用于处理日志的日志级别。

* *元数据扩展架构* ：指定用于PDF文档元数据中XMP属性的元数据扩展架构的路径。

#### 输出文档 {#output-documents-1}

“输出文档”选项卡允许您指定输出文档的目标

* *PDFA文档*：指定保存转换后的PDF/A文档的位置。 它可以覆盖有效负载文档或保存在有效负载文件夹下。
* *转换日志*：指定转换日志的保存位置。 它可以覆盖有效负荷文档，也可以保存在有效负荷文件夹下。

## Forms {#forms}

渲染PDF表单工作流是`renderPDFForm`Forms服务API的包装器，用于使用XDP模板和数据xml创建PDF表单。

### 呈现PDF表单工作流 {#render-pdf-form-workflow}

1. 在Sidekick中，将渲染PDF表单工作流步骤拖动到Forms Workflow选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档 {#input-documents-2}

* *模板文件*：指定XDP模板的位置。 它是必填字段。

* *数据文档*：指定需要与模板合并的数据xml的位置。

#### 输出文档 {#output-documents-2}

* *输出文档*： — 指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters}

* *内容根*：指定存储输入XDP模板中使用的片段或图像的存储库中的文件夹的路径。
* *提交URL*：为生成的PDF表单指定默认提交URL。
* *区域设置*：为生成的PDF表单指定默认区域设置。
* *Acrobat版本*：为生成的PDF表单指定目标Acrobat版本。
* *标记的PDF*：指定是否使生成的PDF可访问。
* *XCI文档*：指定XCI文件的路径。

## 输出 {#output}

生成非交互式PDF工作流是`generatePDFOutput`输出服务API的包装器。 用于从XDP模板和数据xml生成非交互式PDF文档。

### 生成非交互式PDF输出工作流   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 在Sidekick中，将生成非交互式PDF输出工作流拖动到Forms Workflow选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档 {#input-documents-3}

* *模板文件*：指定XDP模板的位置。 它是必填字段。

* *数据文档*：指定需要与模板合并的数据xml的位置。

#### 输出文档 {#output-document}

*输出文档*：指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters-1}

* *内容根*：指定存储输入XDP模板中使用的片段或图像的存储库中的文件夹的路径。
* *区域设置*：指定生成的PDF表单的默认区域设置。
* *Acrobat版本*：为生成的PDF表单指定目标Acrobat版本。
* 线性化PDF：指定是否优化生成的PDF以进行Web查看。
* *标记的PDF*：指定是否使生成的PDF可访问。
* *XCI文档*：指定XCI文件的路径。
