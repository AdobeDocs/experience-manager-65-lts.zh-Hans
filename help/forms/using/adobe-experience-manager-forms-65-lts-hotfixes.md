---
title: Adobe Experience Manager Forms 6.5 LTS修补程序
description: 提供了有关如何下载和安装AEM Forms 6.5 LTS的修补程序的信息。 对于AEM 6.5（非LTS），请参阅AEM 6.5 Forms修补程序一文。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
source-git-commit: 989d83cfc56f7a7d4e2aea5a7ac1ca444d505859
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 11%
---
# Adobe Experience Manager Forms 6.5 LTS修补程序{#aem-form-hotfix}

本文列出为解决已知问题、提高系统稳定性和增强AEM Forms 6.5 LTS的整体性能而实施的关键修复。


本文适用于AEM Forms 6.5 LTS。 对于AEM 6.5（非LTS）部署，请参阅[Adobe Experience Manager Forms修补程序](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/release-notes/aem-forms-hotfix)。

>[!NOTE]
>
> 这些热修复补丁是累积性的，其中包含所有先前的修复。 当您将最新的热修复补丁应用于某个版本时，它不仅会解决最新的问题，还会同时集成此前所有的错误修复和功能改进。

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
      <strong>2026年9月21日</strong><br>
      <em>适用于：</em> AEM Forms 6.5 LTS Service Pack 2 JEE部署(JBoss、WebLogic、WebSphere)<br>
    </td>
    <td>
    <p><strong>要安装此修补程序，请按照以下顺序完成这些步骤：</strong></p>
    <p><strong>步骤1：安装修补程序</strong></p>
    <ul>
    <strong>JBoss：</strong>
    <li>Windows — 适用于JBoss JEE服务器的Windows上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">修补程序</a></li>
    <li>Linux — 适用于Linux上的AEM Forms 6.5 LTS SP2的修补程序，适用于JBoss JEE服务器</a><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz"></li>
    <strong>WebLogic：</strong>
    <li>Windows — 适用于Weblogic JEE服务器的Windows上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">修补程序</a></li>
    <li>Linux — 适用于Linux上的AEM Forms 6.5 LTS SP2的修补程序，适用于Weblogic JEE服务器</a><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz"></li>
    <strong>WebSphere：</strong>
    <li>Windows - Windows上适用于AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">修补程序（适用于Websphere JEE服务器）</a></li>
    <li>Linux — 适用于Linux上的AEM Forms 6.5 LTS SP2的修补程序，用于Websphere JEE服务器</a><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz"></li>
    </ul>
    <p>使用标准AEM Forms on JEE修补程序安装过程安装修补程序。 <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>步骤2：安装漏洞修复捆绑包</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">适用于AEM Forms 6.5 LTS SP2的漏洞修复捆绑包</a></li>
    </ul>
    <ol>
    <li>在<code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>处打开OSGi控制台。</li>
    <li>单击<strong>安装/更新</strong>。</li>
    <li>选中<strong>启动包</strong>和<strong>刷新包</strong>复选框。</li>
    <li>单击<strong>选择文件</strong>，然后上载下载的捆绑包。</li>
    <li>等待日志设置完毕，并且包显示为<strong>活动</strong>。</li>
    </ol>
    <p><strong>步骤3：更新AEM Forms Workbench安装程序</strong></p>
    <p>您必须更新到最新的AEM Forms Workbench安装程序。 从<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">AEM Forms Workbench安装程序</a>下载它。</p>
    <p><strong>步骤4：更新客户端库文件（开发人员）</strong></p>
    <p>此修补程序包含对SDK客户端库<code>adobe-livecycle-client.jar</code>的主要更新（请参阅<a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">包含AEM Forms Java库文件</a>）。 如果项目使用此JAR文件，请在安装修补程序后更新项目类路径中的<code>adobe-livecycle-client.jar</code>。 最新版本位于<code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>。</p>
    <p>此修补程序是累积性的，因此您可以将其应用于AEM Forms 6.5 LTS Service Pack 2或更早版本的Service Pack，而无需先安装Service Pack 2。</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b>在Apache Shiro更新到版本2.1.0后，JEE上的AEM Forms无法通过Shiro安全管理器的<code>NoClassDefFoundError</code>进行引导。 此修补程序将恢复成功的引导。</li>
    <li>JEE上的<b>FORMS-26819</b> AEM Forms失败，并出现<code>org.owasp.esapi.reference.JavaLogFactory</code>的“未找到类”错误。 此修补程序解析缺少的类。</li>
    <li><b>FORMS-26584、FORMS-26589</b>升级到AEM Forms 6.5 LTS后，TaskManager端点将被删除。 此修补程序可恢复TaskManager端点。</li>
    <li><b>FORMS-26569</b>在JEE上，由于安全的XML生成器，配置管理器MergeEars步骤失败并出现DOCTYPE声明错误(<code>ALC-LCM-010-200</code>)。 此修补程序允许MergeEars步骤完成。</li>
    <li>IBM WebSphere Liberty部署中缺少<b>FORMS-25063</b>应用程序级日志。 此修补程序可恢复应用程序级别的日志记录。</li>
    <li><b>FORMS-24892</b>在JBoss上，电子邮件失败并显示“IMAPProvider不是子类型”。 此修补程序可恢复JBoss上的电子邮件功能。</li>
    <li>在WebSphere Liberty配置文件(WLP)上，<b>FORMS-24692</b>电子邮件失败并显示“无法将套接字转换为TLS”。 此修补程序通过WLP上的TLS还原电子邮件。</li>
    <li><b>FORMS-26688</b>已将Gibson库更新到版本6.0.29665850。</li>
    <li><b>FORMS-25222</b>反向移植SAML断言验证改进。</li>
    <li><b>FORMS-26733、FORMS-26734</b>已将Apache Log4j更新到版本2.25.5。</li>
    <li>此修补程序还包括安全修补程序。</li>
    </ul>
    <p><strong>内部版本：</strong> AEMForms-6.6.0-0008</p>
    </td>
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
1. 打开配置管理器捆绑包 `https://server:host/system/console/bundles`，上传并安装捆绑包（.jar）。 热修复补丁即已安装完成。
