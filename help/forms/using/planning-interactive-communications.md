---
title: 教程：规划交互式通信
description: 规划交互式通信的剖析
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 8591214f-9c11-4cd3-b2a1-c83040507b20
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---

# 教程：规划交互式通信 {#tutorial-plan-the-interactive-communication}

规划交互式通信的剖析

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的步骤。 建议按时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

规划交互式通信的第一步是最终确定交互式通信的内容。 法律、金融、支持或营销等部门的主题专家可以帮助您最终确定内容。 内容定稿后，您必须对其进行分析以确定创建交互式通信所需的各种资源类型。

## Planning注意事项 {#planning-considerations}

交互式通信包括以下元素：

* **静态文本**&#x200B;大多包括交互式通信中本质上通用的部分，这些部分包括在与所有客户的通信中。 例如，页眉、页脚、问候语或免责声明。
* **来自后端系统（表单数据模型）的数据**&#x200B;特定于客户，并且与交互式通信动态合并。 例如，可以使用表单数据模型来获取策略编号或地址。
* 交互式通信打印和Web版本的&#x200B;**布局或模板**。
* **顺序**，交互式通信中出现各种文本段落。
* **由一线员工（代理UI）输入的数据**，该员工在发送前自定义通信。 例如，付款到期日期。

* 根据预定义条件填充的&#x200B;**条件数据**。 例如，生成交互式通信的日期。
* **存储在存储库中的图像**，如徽标和签名图像。 公司徽标等图像会出现在大多数或所有交互式通信中。
* **简化交互式通信中复杂数据的表示所需的图表和表**

## 互动式通信剖析 {#anatomy-of-the-interactive-communication}

完成用于创建交互式通信的内容和元素后，即可创建交互式通信剖析。 该解剖结构必须具有列在[规划注意事项](/help/forms/using/planning-interactive-communications.md#planning-considerations)部分中的详细信息。 根据我们的用例，以下是对电信运营商发送给客户的每月账单进行剖析的示例。

该解剖结构包含具有以下输入模式的数据：

* 静态文本
* 表单数据模型
* 代理 UI
* 条件数据
* 图像

在每个部分中，粗体文本表示静态文本。 数据库包括客户、账单和呼叫表。 表单数据模型可以从这些表中的任何表接收数据。 有关详细信息，请参阅[创建表单数据模型](/help/forms/using/create-form-data-model0.md)。

下表说明了交互式通信剖析中每个字段的数据源：

<table>
 <tbody>
  <tr>
   <td>分区</td>
   <td>静态文本</td>
   <td>FDM </td>
   <td>代理 UI</td>
   <td>图像</td>
  </tr>
  <tr>
   <td>帐单详细信息</td>
   <td><p>发票编号</p> <p>记帐日期</p> <p>帐单期间</p> <p>您的计划</p> </td>
   <td><p><strong>计划</strong>字段的值</p> <p>表 — 客户</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>发票编号</li>
     <li>记帐日期</li>
     <li>帐单期间</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>客户详细信息</td>
   <td><p>供应地点</p> <p>州代码</p> <p>手机号码</p> <p>备用联系电话</p> <p>关系编号</p> <p>连接数</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>名称</li>
     <li>地址</li>
     <li>手机号码</li>
     <li>备用联系电话</li>
     <li>关系编号</li>
    </ul> <p>表 — 客户</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>供应地点</li>
     <li>州代码</li>
     <li>连接数</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>账单摘要</td>
   <td><p>上一余额</p> <p>支付</p> <p>调整</p> <p>费用当前帐单期间</p> <p>应付金额</p> <p>到期日期</p> </td>
   <td><p><strong>费用当前帐单期间</strong>字段的值</p> <p>表 — 帐单</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>上一余额</li>
     <li>支付</li>
     <li>调整</li>
     <li>应付金额</li>
     <li>到期日期</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>费用汇总</td>
   <td><p>呼叫费用</p> <p>电话会议费用</p> <p>短信费用 </p> <p>移动互联网费用</p> <p>国家漫游费用</p> <p>国际漫游费用</p> <p>增值服务费用</p> <p>总费用</p> <p>应付总额</p> <p>“增值税服务费用”字段的条件</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>呼叫费用</li>
     <li>电话会议费用</li>
     <li>短信费用 </li>
     <li>移动互联网费用</li>
     <li>国家漫游费用</li>
     <li>国际漫游费用</li>
     <li>增值服务费用</li>
     <li>总费用（使用费用计算字段）</li>
     <li>应付总额（使用费计算字段）</li>
    </ul> <p>表 — 帐单</p> </td>
   <td>无字段</td>
   <td>—</td>
  </tr>
  <tr>
   <td>分项呼叫 — 传出</td>
   <td><p>列名：</p>
    <ul>
     <li>日期</li>
     <li>用时</li>
     <li>数字</li>
     <li>持续时间</li>
     <li>费用</li>
    </ul> </td>
   <td><p>所有值</p> <p>表 — 调用</p> </td>
   <td>无字段</td>
   <td>—</td>
  </tr>
  <tr>
   <td>立即付款</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>Paynow</td>
  </tr>
  <tr>
   <td>增值服务</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
