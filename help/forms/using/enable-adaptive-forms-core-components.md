---
title: 如何在AEM 6.5 Forms上启用自适应Forms核心组件？
description: 分步指南可帮助您在AEM 6.5 Forms环境中启用自适应Forms核心组件。
keywords: 启用核心组件、核心组件自适应Forms、6.5上的核心组件、AEM 6.5上的自适应Forms核心组件、AEM 6.5上的AF核心组件、AEM 6.5 Forms核心组件
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: a163598d-0a6e-45a8-b3b2-1f260007952b
source-git-commit: f21858421f2e84643fab1add5116b033cb6dd122
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在AEM 6.5 Forms上启用自适应Forms核心组件 {#enable-adaptive-forms-core-components}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

启用自适应Forms核心组件允许您从AEM 6.5 Forms环境开始创建、发布和交付基于[核心组件的自适应Forms](create-an-adaptive-form-core-components.md)和[Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=zh-Hans)。

要在AEM 6.5 Forms环境中启用自适应Forms核心组件，请在所有创作和发布实例上设置并部署基于[AEM Archetype 41或更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans)的项目（启用表单选项）。

本文介绍了如何在您的AEM 6.5 Forms环境中设置和部署基于AEM原型的Archetype 41或更高版本以启用自适应Forms核心组件。 您可以参阅下面的列表，了解有关启用Forms核心组件的&#x200B;**AEM 6.5**&#x200B;兼容版本：

## 先决条件 {#prerequisites}

在AEM 6.5 LTS Forms环境中启用自适应Forms核心组件之前：

* 安装[Apache Maven](https://maven.apache.org/download.cgi)的最新版本。

* 安装纯文本编辑器。 例如，Microsoft Visual Studio Code。

## 创建和部署最新的基于AEM原型的项目

要创建基于AEM Archetype 41或[稍后](https://github.com/adobe/aem-project-archetype)的项目并将其部署到所有创作实例和发布实例，请执行以下操作：

1. 以管理员身份登录到您的计算机，托管并运行AEM 6.5 Forms实例。
1. 打开命令提示符或终端，然后运行以下命令以创建AEM Archetype项目（已启用表单选项）：

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux或Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   执行上述命令时，请务必考虑以下几点：

   * 请勿将`aemVersion`属性的值从`6.5.15.0`更改为其他任何内容。

   * 将`archetypeVersion`属性设置为`41`或更高版本。 有关最新版本，请参阅[AEM项目原型](https://github.com/adobe/aem-project-archetype)文档中的系统要求部分。

   * 更新命令以反映环境的特定值，包括`appTitle`、`appId`和`groupId`。 此外，将`includeFormsenrollment`属性的值设置为`y`。 如果您使用Forms Portal，请设置`includeExamples=y`选项以将Forms Portal核心组件包含在您的项目中。


1. （仅适用于基于Archetype版本41的项目）创建AEM Archetype项目后，请为基于核心组件的自适应Forms启用主题。 要启用主题，请执行以下操作：

   1. 打开[AEM原型项目文件夹]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html以进行编辑：

   1. 在第21行添加以下代码：

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![在第21](/help/forms/using/assets/code-to-enable-themes.png)行添加上述代码

   1. 保存并关闭该文件。

1. 更新项目以包含最新版本的Forms核心组件：

   1. 打开[AEM原型项目文件夹]/pom.xml进行编辑。
   1. 将`core.forms.components.version`和`core.forms.components.af.version`的版本设置为[最新的Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=zh-Hans#aem-as-form-version-history)版本，并确保两者具有与表中提到的&#x200B;**Forms核心组件**&#x200B;相同的版本，并设置`core.wcm.components.version`的版本，如[WCM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html?lang=zh-Hans)中所提供。

      >[!WARNING]
      >
      >* 使用版本45创建Archetype项目时，`[AEM Archetype Project Folder]/pom.xml`最初将forms核心组件版本设置为1.1.28。在构建或部署原型项目之前，请将Forms核心组件版本更新为1.1.26。您可以在[AEM 6.5 Forms版本历史记录](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=zh-Hans#aem-as-form-version-history)中找到最新版本。

      >[!NOTE]
      >
      >* 如果设置了任何其他拓扑，请确保将提交、预填充和其他 URL 添加到 Dispatcher 层的允许列表。

   1. 保存并关闭该文件。


1. 成功创建AEM原型项目后，为您的环境构建部署包。 要构建包，请执行以下操作：

   1. 导航到AEM原型项目的根目录。

   1. 运行以下命令为您的环境构建AEM原型项目：

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   成功构建AEM原型项目后，将生成一个AEM包。 您可以在[AEM原型项目文件夹]\all\target\[appid].all-[version].zip中找到该包

1. 使用[包管理器](/help/sites-administering/package-manager.md)在所有创作实例和发布实例上部署[AEM原型项目文件夹]\all\target\[appid].all-[version].zip包。

>[!NOTE]
>
>
>
> * 如果在发布实例上访问登录对话框时遇到困难，要通过包管理器安装包，请尝试使用URL `http://[Publish Server URL]:[PORT]/system/console`登录。 这使您可以在发布实例上访问登录页面，从而允许您继续安装过程。
> * 将原型项目部署到您的环境后，请勿将其删除或放弃。 要将自定义主题和新的自适应Forms核心组件主题添加到您的环境中，需要原型项目。

为您的环境启用了核心组件。 将基于空核心组件的自适应表单模板和画布3.0主题部署到您的环境，使您能够[创建基于核心组件的自适应Forms](create-an-adaptive-form-core-components.md)。

## 常见问题解答

### 什么是核心组件？

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)是一组用于 AEM 的标准化 Web 内容管理 (WCM) 组件，以缩短您网站的开发时间并降低维护成本。

### 在启用核心组件上添加了哪些功能？


为您的环境启用自适应表单核心组件时，将有一个空白的基于核心组件的自适应表单模板和 Canvas 3.0 主题添加到您的环境。为您的环境启用自适应表单核心组件后，您可以：

* 创建基于核心组件的自适应Forms。
* 创建基于核心组件的自适应表单模板。
* 为基于核心组件的自适应表单模板创建自定义主题。
* 向需要表单Headless表示的渠道（如移动设备、Web、本机应用程序和服务）提供基于核心组件的自适应表单的JSON表示。

## 后续内容

* [创建基于核心组件的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)
* [创建自适应表单或将其添加到AEM Sites页面或体验片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [为基于核心组件的自适应Forms创建主题](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [为基于核心组件的自适应Forms创建模板](template-editor.md)
