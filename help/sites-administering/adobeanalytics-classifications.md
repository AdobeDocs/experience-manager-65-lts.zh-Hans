---
title: Adobe分类
description: 了解如何使用Adobe Classifications将分类数据导出到Adobe Analytics。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: f564bda3-4141-40b3-8c08-140d4da92e2c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Adobe分类{#adobe-classifications}

Adobe分类按计划方式将分类数据导出到[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。 导出程序是&#x200B;**com.adobe.cq.scheduled.exporter.Exporter**&#x200B;的实现。

要配置此功能，请执行以下操作：

1. 使用&#x200B;**导航**，选择&#x200B;**工具**、**云服务**，然后选择&#x200B;**旧版云服务**。
1. 滚动到&#x200B;**Adobe Analytics**&#x200B;并选择&#x200B;**显示配置**。
1. 单击Adobe Analytics配置旁边的&#x200B;**[+]**&#x200B;链接。

1. 在&#x200B;**创建框架**&#x200B;对话框中：

   * 指定&#x200B;**标题**。
   * 或者，您可以为将框架详细信息存储在存储库中的节点指定&#x200B;**名称**。
   * 选择&#x200B;**Adobe Analytics分类**

   然后单击&#x200B;**创建**。

   ![创建框架对话框](assets/aa-25.png)

1. 将打开&#x200B;**分类设置**&#x200B;对话框以进行编辑。

   ![分类设置对话框](assets/aa-classifications-settings.png)

   这些属性包括：

   | **字段** | **描述** |
   |---|---|
   | 已启用 | 选择&#x200B;**是**&#x200B;以启用Adobe分类设置。 |
   | 发生冲突时覆盖 | 选择&#x200B;**是**&#x200B;以覆盖所有数据冲突。 默认情况下，此项设置为&#x200B;**否**。 |
   | 删除已处理的项目 | 如果设置为&#x200B;**是**，则在导出已处理的节点后将其删除。 默认值为&#x200B;**False**。 |
   | 导出作业描述 | 输入Adobe分类作业的描述。 |
   | 通知电子邮件 | 输入Adobe分类通知的电子邮件地址。 |
   | 报表包 | 输入要为其运行导入作业的报表包。 |
   | 数据集 | 输入要为其运行导入作业的数据集关系ID。 |
   | 转换程序 | 从下拉菜单中，选择转换器实施。 |
   | 数据源 | 导航到数据容器的路径。 |
   | 导出时间表 | 选择导出计划。 默认每30分钟处理一次。 |

1. 单击&#x200B;**确定**&#x200B;以保存您的设置。

## 修改页面大小 {#modifying-page-size}

以页面形式处理记录。 默认情况下，Adobe分类会创建页面大小为1000的页面。

按照Adobe分类中的定义，页面最大大小可以是25000的，并且可以从Felix控制台进行修改。 在导出期间，Adobe Classifications会锁定源节点，以防止并发修改。 导出后、出错时或会话关闭时，节点会解锁。

要更改页面大小，请执行以下操作：

1. 导航到位于&#x200B;**https://&lt;host>：&lt;port>/system/console/configMgr**&#x200B;的OSGI控制台，然后选择&#x200B;**Adobe AEM Classifications Exporter**。

   ![aa-26](assets/aa-26.png)

1. 根据需要更新&#x200B;**导出页面大小**，然后单击&#x200B;**保存**。

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe Classifications以前称为SAINT导出器。

导出器可以使用转换器将导出数据转换为特定格式。 对于Adobe分类，提供了实现Transformer接口的子接口`SAINTTransformer<String[]>`。 此接口用于将数据类型限制为SAINT API使用的`String[]`，并具有标记器接口以查找要选择的此类服务。

在默认实现SAINTDefaultTransformer中，导出程序源的子资源被视为记录，属性名称作为键，属性值作为值。 **键**&#x200B;列自动添加为第一列 — 其值将是节点名称。 已忽略命名空间属性（包含`:`）。

*节点结构：*

* ID分类`nt:unstructured`

   * 1 `nt:unstructured`

      * 产品=我的产品名称（字符串）
      * 价格= 120.90（字符串）
      * 大小= M（字符串）
      * 颜色=黑色（字符串）
      * Color^Code = 101（字符串）

**SAINT标题和记录：**

| **键** | **产品** | **价格** | **大小** | **颜色** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | 我的产品名称 | 120.90 | 周一 | black | 101 |

这些属性包括：

<table>
 <tbody>
  <tr>
   <td><strong>属性路径</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>转换程序</td>
   <td>SAINTTransformer实现的类名</td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td>通知电子邮件地址。</td>
  </tr>
  <tr>
   <td>报告包</td>
   <td>要为其运行导入作业的报表包ID。 </td>
  </tr>
  <tr>
   <td>数据集</td>
   <td>要为其运行导入作业的数据集关系ID。 </td>
  </tr>
  <tr>
   <td>说明</td>
   <td>作业描述。<br /> </td>
  </tr>
  <tr>
   <td>覆盖</td>
   <td>用于覆盖数据冲突的标志。 默认值为<strong>false</strong>。</td>
  </tr>
  <tr>
   <td>checkdivision</td>
   <td>用于检查报表包兼容性的标记。 默认值为<strong>true</strong>。</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>用于在导出后删除已处理节点的标志。 默认值为<strong>false</strong>。</td>
  </tr>
 </tbody>
</table>

## 自动化Adobe分类导出 {#automating-adobe-classifications-export}

您可以创建自己的工作流，这样任何新导入都会启动该工作流，在&#x200B;**/var/export/**&#x200B;中创建适当且结构正确的数据，以便将其导出到Adobe分类。
