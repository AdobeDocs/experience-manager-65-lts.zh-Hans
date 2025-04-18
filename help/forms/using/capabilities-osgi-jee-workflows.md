---
title: OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能
description: OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能
contentOwner: khsingh
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
feature: Adaptive Forms,AEM Forms on OSGi
role: User, Developer
exl-id: d0f54236-5dc2-4c64-87c5-85e5e85e8cf7
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 20%

---

# OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件箱和HTML Workspace {#aem-inbox-and-html-workspace}

您可以使用AEM收件箱在OSGi上运行和监视以Forms为中心的AEM工作流。 而HTML Workspace允许您运行和监控AEM Forms JEE工作流。 下表可帮助您了解AEM收件箱中OSGi上以Forms为中心的AEM工作流以及HTML Workspace中AEM Forms JEE工作流程的各种可用重要操作。

<table>
 <tbody>
  <tr>
   <td>操作</td>
   <td>AEM 收件箱</td>
   <td>HTML Workspace</td>
  </tr>
  <tr>
   <td>正在启动进程、任务或表单应用程序<br /> </td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交任务</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>将任务分配给组</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交到多个路由</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>跟踪任务历史记录和任务摘要</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>电子邮件通知</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>重新分配任务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>自适应表单的字段级附件</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>日历视图</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>任务级注释</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>队列（共享的个人队列，队列中的报销申请任务）</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>外出通知</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
    <tr>
   <td>自定义用户界面元素</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>将任务分配给多个用户</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM Forms JEE工作流上以表单为中心的AEM工作流(JEE流程管理上的AEM Forms)具有一组不同的功能。 下表可帮助您了解OSGi上以表单为中心的AEM工作流和JEE工作流上以AEM Forms为中心的工作流中提供的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi<br />上以表单为中心的AEM工作流 </td>
   <td>AEM Forms JEE工作流</td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与其他AEM解决方案集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>自定义电子邮件模板</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>定义任务优先级</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>任务在到期日期后超时</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流中的循环</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态选择被分派人 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>使用自定义元数据</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>电子签名(Adobe Sign)</td>
   <td>支持的<sup>[1]</sup></td>
   <td>支持的<sup>[5]</sup></td>
  </tr>
  <tr>
   <td>管理任务和表单应用程序</td>
   <td>支持的<sup>[2]</sup><br /> </td>
   <td>支持的<sup>[2]</sup></td>
  </tr>
  <tr>
   <td>文档服务</td>
   <td>支持的<sup>[3]</sup></td>
   <td>支持的<sup>[3]</sup></td>
  </tr>
  <tr>
   <td>将已完成的任务渲染为自适应表单或PDF文档</td>
   <td>支持</td>
   <td>支持[4]</td>
  </tr>
  <tr>
   <td>与通信管理集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>网关，不等待 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>用于存储数据的变量 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>OR， AND Split</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>用户头像</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在工作流结束时发送电子邮件</td>
   <td>支持<sup>[7]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>从工作流调用Web服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>工作流暂存</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>只读自适应表单</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>隐藏默认保存按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>“对工作流详细信息的粒度控制”部分</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>轮询/计划服务</td>
   <td>开箱即用</td>
   <td>需要自定义实施</td>
  </tr>
  <tr>
   <td>自适应Forms应用程序</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>汇编程序服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>PDF Generator服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>表单服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>输出服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>记录Assurance</td>
   <td>支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>执行脚本</td>
   <td>支持ECMAScript</td>
   <td>支持Java代码段</td>
  </tr>
  <tr>
   <td>汇编程序</td>
   <td>支持</td>
   <td>支持</td>
  </tr>  
  <tr>
   <td>HTML5 Forms，交互式PDF forms，表单集</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>进程报告</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>起点类别</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>批量任务审批 </td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用自定义名称保存草稿</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用现有进程数据启动进程<br /> </td>
   <td>不支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>将起点另存为草稿</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>经理视图</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>搜索模板</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与第三方应用程序集成</td>
   <td>不支持<sup>[6]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流应用程序或起点的任务级附件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>提醒电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在任务超时时更改标题</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>关于任务委派和任务声明的电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在不相交组之间进行委托</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>XSLT变换</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态任务优先级</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>动态标题</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
    <tr>
   <td>动态描述</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用以表单为中心的AEM工作流来签名已填写的自适应表单。 OSGi上以表单为中心的AEM Workflows支持表单外签名。 不支持[表单内签名](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)体验。

1. 您需要访问AEM收件箱才能在AEM Forms OSGi和HTML Workspace上运行和监控以表单为中心的工作流，从而运行和监控AEM Forms JEE工作流。
1. 本机AEM Forms文档服务适用于OSGi上以表单为中心的AEM工作流和JEE工作流上的AEM Forms 。 AEM Workflow在OSGi和AEM Forms JEE（流程管理）工作流中使用本机文档服务来处理以表单为中心的AEM工作流。
1. AEM Forms JEE工作流只能渲染自适应表单。 它不支持将自适应表单渲染为PDF文档。
1. AEM Forms JEE工作流没有适用于Adobe Sign的单独步骤。 您需要支持Adobe Sign的自适应表单才能使用AEM Forms JEE工作流。 有关详细信息，请参阅[Adobe Sign文档](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. 您可以使用[调用表单数据模型服务](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p)步骤来调用Web服务服务，并从第三方应用程序中发布或检索数据。
1. 您可以使用[发送电子邮件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step)步骤发送电子邮件。

## AEM收件箱和AEM Forms应用程序功能之间的差异 {#differences-between-aem-inbox-and-aem-forms-app-features}

启动以Forms为中心的工作流的两种主要方法是使用[AEM收件箱](../../forms/using/manage-applications-inbox.md)和AEM Forms应用程序。 但是，AEM收件箱和AEM Forms应用程序的功能有所不同。 AEM收件箱仅适用于以[Forms为中心的工作流](../../forms/using/aem-forms-workflow.md)，而AEM Forms应用程序同时适用于以Forms为中心的工作流和流程管理。

下表列出了AEM收件箱和AEM Forms应用程序的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>AEM 收件箱</strong></p> </td>
   <td><p><strong>AEM Forms 应用程序</strong></p> </td>
  </tr>
  <tr>
   <td><p>启动表单应用程序</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>提交任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>委派任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>跟踪任务历史记录和任务摘要</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加任务层附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>查看任务层附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>添加字段级附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>显示日历视图</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加注释</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
 </tbody>
</table>
