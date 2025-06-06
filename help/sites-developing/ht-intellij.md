---
title: 如何使用IntelliJ IDEA开发AEM项目
description: 了解如何使用IntelliJ IDEA开发Adobe Experience Manager项目。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 4def21ee-d7de-45a8-a7df-062dd2d1a3ba
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 如何使用IntelliJ IDEA开发AEM项目{#how-to-develop-aem-projects-using-intellij-idea}

## 概述 {#overview}

要开始在IntelliJ上开发AEM，需要执行以下步骤。

本主题的其余部分将更详细地解释每个步骤。

* 安装IntelliJ
* 基于Maven设置您的AEM项目
* 在Maven POM中为IntelliJ准备JSP支持
* 将Maven项目导入IntelliJ

>[!NOTE]
>
>本指南基于IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1。

### 安装IntelliJ IDEA {#install-intellij-idea}

从[JetBrains](https://www.jetbrains.com/idea/download/)的“下载”页面下载IntelliJ IDEA。

然后，按照该页面上的安装说明进行操作。

### 基于Maven设置您的AEM项目 {#set-up-your-aem-project-based-on-maven}

接下来，使用Maven设置项目，如[如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)中所述。

要开始使用IntelliJ IDEA中的AEM项目，[在5分钟内快速入门](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)中的基本设置便已足够。

### 为IntelliJ IDEA准备JSP支持 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA还可以在使用JSP时提供支持，例如：

* 自动完成标记库
* 感知由`<cq:defineObjects />`和`<sling:defineObjects />`定义的对象

要使其正常工作，请按照[使用Apache Maven构建AEM项目的操作方法](/help/sites-developing/ht-projects-maven.md)中的[使用JSP的操作方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中的说明操作。

### 导入Maven项目 {#import-the-maven-project}

1. 在IntelliJ IDEA中打开&#x200B;**导入**&#x200B;对话框，方法是

   * 在欢迎屏幕上选择&#x200B;**导入项目**（如果尚未打开任何项目）
   * 从主菜单中选择&#x200B;**文件>导入项目**

1. 在导入对话框中，选择项目的POM文件。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 继续使用默认设置，如下面的对话框中所示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 通过单击&#x200B;**下一步**&#x200B;和&#x200B;**完成**&#x200B;继续下列对话框。
1. 现在，您已设置使用IntelliJ IDEA进行AEM开发

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA调试JSP {#debugging-jsps-with-intellij-idea}

使用IntelliJ IDEA调试JSP时，必须执行以下步骤

* 在项目中设置Web Facet
* 安装JSR45支持插件
* 配置调试配置文件
* 为调试模式配置AEM

#### 在项目中设置Web Facet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA必须了解在何处查找用于调试的JSP。 由于IDEA无法解释`content-package-maven-plugin`设置，因此必须手动对其进行配置。

1. 转到&#x200B;**文件>项目结构**
1. 选择&#x200B;**Content**&#x200B;模块
1. 单击模块列表上方的&#x200B;**+**&#x200B;并选择&#x200B;**Web**
1. 作为Web资源目录，选择项目的`content/src/main/content/jcr_root subdirectory`，如下面的屏幕快照所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安装JSR45支持插件 {#install-the-jsr-support-plugin}

1. 转到IntelliJ IDEA设置中的&#x200B;**插件**&#x200B;窗格
1. 导航到&#x200B;**JSR45集成**&#x200B;插件，并选中它旁边的复选框
1. 单击&#x200B;**应用**
1. 请求时重新启动IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置调试配置文件 {#configure-a-debug-profile}

1. 转到&#x200B;**运行>编辑配置**
1. 点击&#x200B;**+**&#x200B;并选择&#x200B;**JSR45 Remote**
1. 在配置对话框中，选择&#x200B;**应用程序服务器**&#x200B;旁边的&#x200B;**配置**&#x200B;并配置通用服务器
1. 如果要在开始调试时打开浏览器，请将起始页设置为适当的URL
1. 如果使用vlt自动同步，则删除所有&#x200B;**启动前**&#x200B;任务；如果不使用，则配置相应的Maven任务
1. 在&#x200B;**启动/连接**&#x200B;窗格中，根据需要调整端口
1. 复制IntelliJ IDEA建议的命令行参数

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 为调试模式配置AEM {#configure-aem-for-debug-mode}

最后一步是使用IntelliJ IDEA建议的JVM选项启动AEM。

直接启动AEM jar文件并添加这些选项，例如，使用以下命令行：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

您还可以将这些选项添加到`crx-quickstart/bin/start`中的启动脚本，如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 开始调试 {#start-debugging}

现在，您已准备好在AEM中调试JSP。

1. 选择&#x200B;**运行>调试>调试配置文件**
1. 在组件代码中设置断点
1. 访问浏览器中的页面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA调试包 {#debugging-bundles-with-intellij-idea}

可以使用标准通用远程调试连接调试捆绑包中的代码。 您可以按照远程调试[&#128279;](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter)上的Jetbrain文档进行操作。
