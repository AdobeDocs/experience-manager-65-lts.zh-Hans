---
title: 设置PDFG网络打印机（仅限Windows）
description: 了解如何设置PDFG网络打印机（仅限Windows ）
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6e9c42d9-fb1d-432b-95b9-6e21706b2a3e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# 设置PDFG网络打印机（仅限Windows） {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

PDFG网络打印机允许用户从任何支持打印的应用程序生成PDF文档。 用户安装PDFG网络打印机后，名为&#x200B;*PDF生成器*&#x200B;的新打印机将出现在Windows控制面板的“打印机”部分中。 如果同名打印机已存在，则提示用户提供另一个名称。

从任何应用程序打印到此打印机，都会将文档(采用PostScript格式)发送到PDF Generator，后者将PostScript文件转换为PDF。 根据您配置PDF Generator的方式，它会将PDF文档作为电子邮件的附件发送给用户，将PDF文档转发到指定的AEM表单服务或流程，或同时执行这两项操作。

要设置PDFG网络打印机，需要执行以下步骤：

1. 配置电子邮件设置。 （请参阅[配置PDFG网络打印机的电子邮件设置](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)。）
1. 在管理控制台中，配置PDFG网络打印机设置。 （请参阅[配置PDFG网络打印机设置](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)。）
1. 确保在AEM表单数据库中为用户配置了有效的电子邮件地址，并将PDFGUserPermission分配给每个用户。<!-- Fix broken link See Setting up and organizing users -->
1. 确保在用户的计算机上安装了32位JRE6。
1. 在用户的计算机上安装打印机。 （请参阅[在用户计算机上安装PDFG网络打印机](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)。）

## 配置PDFG网络打印机的电子邮件设置 {#configure-email-settings-for-pdfg-network-printer}

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页上，单击provider.email_sendmail_service ，指定SMTP设置，然后单击“保存”。

## 配置PDFG网络打印机设置 {#configure-the-pdfg-network-printer-settings}

1. 在管理控制台中，单击“服务”>“PDF Generator”>“PDFG网络打印机”
1. 在Adobe PDF设置和安全设置列表中，选择要应用于生成的PDF的选项。 有关这些设置的详细信息，请参阅[配置Adobe PDF设置](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings)和[配置安全设置](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)。
1. 要将转换后的PDF发送回用户，请选择Email The Converted PDF File Back To The User选项并指定以下信息：

   * 用于向用户发送PDF的电子邮件地址
   * 电子邮件的主题
   * 电子邮件的页眉、正文和页脚。 在电子邮件中，&lt;receiverName>被替换为打印文档的用户全名。

1. 要将转换的PDF发送到AEM表单服务或流程，请选择将转换的PDF转发到指定的AEM表单服务或流程选项，并指定以下信息：

   * 要调用的服务的名称
   * 要调用的服务的操作的名称
   * 在服务或进程的component.xml文件中指定的输入参数的名称。 PDF文档将用作该输入参数的值。

1. 单击“保存”。

如果要还原为原始的默认电子邮件文本，请单击“还原电子邮件内容”。

## 在用户计算机上安装PDFG网络打印机 {#install-pdfg-network-printer-on-a-user-s-computer}

具有PDFG管理员或PDFG用户角色的用户可以安装PDFG网络打印机。 计算机上必须安装32位JDK。

1. （PDFG管理员）在管理控制台中，单击“服务”>“PDF Generator”>“PDFG网络打印机”。

   （PDFG用户）转到`http(s)://[host]:'port'/pdfgui`并单击“PDFG网络打印机安装”下的链接。

1. 在“PDFG Network Printer Installation（PDFG网络打印机安装）”下，单击链接。 提示输入用户帐户信息时，请指定您在步骤1中用于登录的用户名和密码。 出现一条消息，说明打印机已成功安装。

   ***注意&#x200B;**：如果用户密码更改，则用户必须在其计算机上重新安装PDFG网络打印机。 无法从管理控制台更新密码。*

1. 单击“确定”。
