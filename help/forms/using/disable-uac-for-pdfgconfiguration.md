---
title: 禁用适用于JEE和OSGI的PDFG配置UAC
description: 了解如何为PDFG配置禁用UAC以修复Word到PDF转换的步骤。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 55f5d3bb-2a6f-4fac-9d33-7b39e4ca317f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# 无法在Windows Server上将Word或Excel文件转换为PDF {#unable-to-convert-word-excel-files-PDF}

## 问题 {#issue}

当用户尝试在Microsoft® Windows Server上将Word或Excel文件转换为PDF时，遇到以下错误：

*来自主转换器的错误消息：*
*ALC-PDG-015-003 — 系统无法打开输入文件。 再次提交文件或联系系统管理员。*


## 解决方案 {#solution}

执行以下操作：

1. 要访问系统配置实用程序，请转到&#x200B;**[!UICONTROL 开始>运行]**，然后输入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 单击&#x200B;**[!UICONTROL 工具]**&#x200B;选项卡，向下滚动并选择&#x200B;**[!UICONTROL 更改UAC设置]**。 单击&#x200B;**[!UICONTROL 启动]**，以便在新窗口中运行该命令。
1. 将滑块调整为从不通知级别。 完成后，关闭命令窗口并关闭“System Configuration（系统配置）”窗口。
1. 验证UAC的注册表设置是否设置为0（零）。 执行以下步骤进行验证：

   1. Microsoft®建议在修改注册表之前对其进行备份。 有关详细步骤，请参阅[如何在Windows中备份和还原注册表](https://support.microsoft.com/en-us/help/322756)。
   1. 打开Microsoft® Windows注册表编辑器。 要打开注册表编辑器，请转到“开始”>“运行”，键入regedit ，然后单击“确定”。
   1. 导航到`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。 确保EnableLUA的值设置为0（零）。
   1. 确保&#x200B;**EnableLUA**&#x200B;的值设置为0（零）。 如果该值不为0，则将该值更改为0。 关闭注册表编辑器。

1. 重新启动计算机。

## 应用于 {#appliesto}

此解决方案适用于JEE服务器上的AEM Forms和OSGi服务器上的AEM Forms 。
