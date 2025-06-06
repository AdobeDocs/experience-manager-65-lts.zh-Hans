---
title: AEM Forms应用程序疑难解答
description: 了解AEM Forms应用程序的常见问题以及如何对其进行故障诊断。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: e63c1dc2-9843-47ca-8f3c-c49720659aa0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# AEM Forms应用程序疑难解答 {#troubleshoot-aem-forms-app}

本文介绍了构建AEM Forms应用程序时可能显示的错误消息以及解决这些消息的步骤。

本文中的部分包括：

* [iOS用户的附件丢失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [工作区用户提交的HTML5表单草稿在门户上不可见](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [无法在AEM Forms应用程序中加载HTML5表单（未缓存）](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms无法在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支持的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle插件兼容性问题](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用户的附件丢失 {#attachment-loss-for-ios-users}

配置为在OSGi上与AEM Forms同步的iOS版AEM Forms应用程序仅支持字段级附件。 所有附件的名称都必须是唯一的。 如果多个附件具有相同的名称，则仅保留一个附件，而具有相同名称的所有其他附件都将丢失。 执行以下步骤，防止iOS设备上的用户丢失数据：

1. 在连接的服务器上，导航到&#x200B;**Adobe Experience Manager >工具>操作> Web控制台**。
1. 查找并单击&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**。
1. 在[!UICONTROL 自适应表单和交互式通信Web渠道配置]对话框中，启用&#x200B;**使文件名唯一**。

   如果&#x200B;**将文件名设为唯一**&#x200B;设置被禁用，则当用户尝试提交具有多个附件的自适应表单时，将会丢失数据。

1. 单击&#x200B;**保存**。

## 工作区用户提交的HTML5表单草稿在门户上不可见 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

对于在AEM Forms应用程序中通过&#x200B;**另存为草稿** HTML渲染配置文件启用的HTML5表单，工作区用户看不到保存的草稿。 要查看工作区用户在门户上提交的HTML5表单的已保存草稿，请执行以下步骤：

1. 打开CRXDE并使用管理员凭据登录。

   URL： `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路径中，在访问控制下的访问控制列表中，单击&#x200B;**+**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，单击“主体”字段中的组搜索按钮。
1. 在“选择主体”对话框的“名称”字段中，键入`PERM_WORKSPACE_USER`并单击&#x200B;**搜索**。
1. 在“选择主体”对话框中选择`PERM_WORKSPACE_USER`组，然后单击&#x200B;**确定**。
1. 在“添加新条目”对话框中，在“主体”字段中选择`PERM_WORKSPACE_USER`组。

   为用户组启用`jcr:read`权限。

1. 单击&#x200B;**确定**。

## 无法在AEM Forms应用程序中加载HTML5表单（未缓存） {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

当AEM Forms应用程序连接到旧版AEM Forms服务器时，未缓存的HTML5表单无法在AEM Forms应用程序中加载。

执行以下步骤来解决问题：

1. 在创作实例中，导航到&#x200B;**Adobe Experience Manager >工具>配置Workspace App离线服务>立即配置**。
1. 在&#x200B;**Workspace App离线服务**&#x200B;页面中，单击&#x200B;**手动资源缓存**。

   URL： https://&lt;服务器>：&lt;端口>/libs/fd/workspace-offline/content/config.html

1. 在&#x200B;**手动资源缓存**&#x200B;选项卡中，单击&#x200B;**+**&#x200B;按钮以添加CRX路径。
1. 在&#x200B;**添加新资源**&#x200B;字段中，键入/etc.clientlibs/fd/xfaforms/I18N/en_US.js并单击&#x200B;**添加**。
1. 单击&#x200B;**保存**。

## AEM Forms无法在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms应用程序中，如果表单路径或其任何资源包含大于或等于256个字符，则表单不会与连接的服务器同步。

修改表单的路径及其资源，将字符数减少到256个字符以下。

## 不支持的Gradle版本 {#unsupported-version-of-gradle}

**错误消息：**&#x200B;项目正在使用不受支持的Gradle版本。

在Android Studio中构建AEM Forms应用程序时显示错误消息。 出现此问题的原因是系统支持的Gradle版本不受支持。

**解决方案：**&#x200B;单击&#x200B;**修复Gradle包装并重新导入项目**&#x200B;以解决此问题。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle插件兼容性问题 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**错误消息：** Android Gradle插件和Gradle的版本不兼容。

当您从Android Studio用户界面的&#x200B;**生成**&#x200B;菜单中选择&#x200B;**生成APK**&#x200B;选项时，将显示错误消息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**分辨率：**&#x200B;打开&#x200B;**Gradle脚本** > **gradle-wrapper.properties**&#x200B;文件并编辑&#x200B;**distributionUrl**&#x200B;属性。

例如，Android Studio控制台建议将Gradle版本降级为3.5。编辑&#x200B;**的** distributionUrl **中的版本。gradle-wrapper.properties**&#x200B;文件。

再次选择&#x200B;**生成** > **生成APK**&#x200B;以解决错误并生成.apk文件。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
