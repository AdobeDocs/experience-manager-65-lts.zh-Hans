---
title: 运行模式
description: 了解如何使用运行模式出于特定目的调整AEM实例。
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b21555f2-bc07-4653-a5da-966b9aa7ea1f
source-git-commit: 3370d62eafb9339a9f9c638f3fb2e2ce0f14d9ec
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# 运行模式{#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发、Intranet或其他。

您可以：

* [为每个运行模式定义配置参数集合](#defining-configuration-properties-for-a-run-mode)。

  基本配置参数集将应用于所有运行模式，然后您可以根据特定环境的目的调整其他配置参数集。 根据需要应用这些变量。

* [为特定模式定义要安装的其他包](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有设置和定义都存储在一个存储库中，并通过设置&#x200B;**运行模式**&#x200B;激活。

## 安装运行模式 {#installation-run-modes}

安装（或固定）运行模式在安装时使用，然后在实例的整个生命周期内固定，这些模式无法更改。

提供开箱即用的安装运行模式：

* `author`
* `publish`

这是两对互斥的运行模式；例如，您可以：

* 定义`author`或`publish`，而不是同时定义两者

>[!CAUTION]
>
>使用上述运行模式之一（创作、发布）时，安装时使用的值定义该安装的&#x200B;*整个生命周期*&#x200B;的运行模式。
>
>对于这些运行模式，您&#x200B;*无法在安装后更改它们*。

## 自定义运行模式 {#customized-run-modes}

您还可以创建自己的自定义运行模式。 这些功能可以结合使用以涵盖各种场景，例如：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 根据需要。.

每次启动时也可以选择定制的运行模式。

## 定义运行模式的配置属性 {#defining-configuration-properties-for-a-run-mode}

用于特定运行模式的配置属性值集合可以保存在存储库中。

运行模式由文件夹名称上的后缀指示。 这样，您可以将所有配置作为存储在一个存储库中。 例如：

* `config`

  适用于所有运行模式

* `config.author`

  用于作者运行模式

* `config.publish`

  用于发布运行模式

* `config.<run-mode>`

  用于适用的运行模式；例如，配置

有关定义这些文件夹中的单个配置节点以及为多种运行模式的组合创建配置的详细信息，请参阅存储库中的[OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。

>[!NOTE]
>
>对于[安装运行模式](#installation-run-modes)（例如，作者），安装后无法更改运行模式。 但是，对单个配置属性的更改将在重新启动后生效。

## 定义要为运行模式安装的其他包 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

还可以指定应该为特定运行模式安装的其他包。 对于这些定义，使用安装文件夹来保存捆绑包。 运行模式再次由前缀表示：

* `install.author`
* `install.publish`

这些文件夹的类型为`nt:folder`，应包含相应的包。

## 使用特定运行模式启动CQ {#starting-cq-with-a-specific-run-mode}

如果您为多种运行模式定义了配置，则需要定义要在启动时使用的配置。 有多种方法可指定要使用的运行模式；分辨率的顺序为：

1. [系统属性(](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [文件名检测](#filename-detection-renaming-the-jar-file)

当您使用应用程序服务器时，还可以[在web.xml](#defining-the-run-mode-in-web-xml-with-application-server)中定义运行模式。

### 使用sling.properties文件 {#using-the-sling-properties-file}

`sling.properties`文件可用于定义所需的运行模式：

1. 编辑配置文件：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下属性；以下示例适用于作者：

   `sling.run.modes=author`

### 使用 — r选项 {#using-the-r-option}

启动快速启动时，可以使用`-r`选项激活自定义运行模式。 例如，使用以下命令启动一个运行模式设置为dev的AEM实例。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在启动脚本中使用系统属性 {#using-a-system-property-in-the-start-script}

启动脚本中的系统属性可用于指定运行模式。

* 例如，使用以下选项将实例作为生产发布实例在美国启动：

  `-Dsling.run.modes=publish,prod,us`

### 文件名检测 — 重命名jar文件 {#filename-detection-renaming-the-jar-file}

通过在安装之前重命名安装jar文件，可以激活以下两种安装运行模式：

* 发布
* 作者

jar文件必须使用命名约定：

`cq5-<run-mode>-p<port-number>`

例如，通过命名jar文件来设置`publish`运行模式：

`cq5-publish-p4503`

### 在web.xml中定义运行模式（使用应用程序服务器） {#defining-the-run-mode-in-web-xml-with-application-server}

在使用应用程序服务器时，您还可以配置属性：

`sling.run.modes`

在文件中：

`WEB-INF/web.xml`

该文件位于AEM `war`文件中，应在部署之前更新。

有关详细信息，请参阅[将AEM与应用程序服务器一起安装](/help/sites-deploying/application-server-install.md)。
