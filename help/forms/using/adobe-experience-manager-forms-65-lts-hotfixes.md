---
title: Adobe Experience Manager Forms 6.5 LTS SP1修补程序
description: 提供了有关如何下载和安装AEM Forms 6.5 LTS的修补程序的信息。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: ff5992fb29c9413cc60e1f0f14c52b1eeff3c3de
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 45%

---


# Adobe Experience Manager Forms 6.5 LTS修补程序{#aem-form-hotfix}

本文列出为解决已知问题、提高系统稳定性和增强AEM Forms 6.5 LTS的整体性能而实施的关键修复。


>[!NOTE]
>
> 这些热修复补丁是累积性的，其中包含所有先前的修复。当您将最新的热修复补丁应用于某个版本时，它不仅会解决最新的问题，还会同时集成此前所有的错误修复和功能改进。

## AEM Forms 6.5 LTS的修补程序 {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>热修复补丁下载链接（AEM 软件分发链接）</strong></td>
    <td><strong>修复的问题</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2025年9月9日</strong><br>
    <td>
    <ul>
    <li>Windows — 适用于Windows上的AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">修补程序2</a></li>
    <li>Linux — 适用于Linux上的AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">修补程序2</a></li>
     <li>macOS- MacOS上适用于AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">修补程序2</a></li>
    <td>
    <ul>
    <li>通过解决在启用服务器端验证(SSV)时提交可能失败的问题来增强表单提交的可靠性如果您遇到任何问题，请联系[Adobe Experience Manager Forms支持](https://business.adobe.com/in/support/main.html)
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## 下载并安装 OSGi 热修复补丁 {#download-install-hotfix}

请执行以下步骤以下载并安装该热修复补丁：

1. 从软件分发链接下载[热修复补丁](#hotfix-for-adaptive-forms)。
1. 提取热修复补丁存档文件，以获取 Experience Manager 包（.zip）和捆绑包（.jar）文件。
1. 通过[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上传并安装包（.zip）。
1. 打开配置管理器捆绑包 `https://server:host/system/console/bundles`，上传并安装捆绑包（.jar）。热修复补丁即已安装完成。
