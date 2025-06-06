---
title: AEM常见问题解答
description: 使用这些常见问题解答来了解、配置和解决AEM中的常见工作流或问题。
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: b2e73e28-fa34-436d-8a20-848d353e3b8c
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# AEM常见问题解答 {#aem-faqs}

了解一些AEM故障排除和配置问题的答案。

## Sites {#sites}

### 如何配置无二进制分发？ {#how-do-i-configure-binary-less-distribution}

支持通过共享数据存储进行无二进制分发，并且涉及使用基于保险库的分发包导出程序（工厂PID： `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）包生成器的代理。

启用无二进制模式后，分发的内容包包含对二进制文件的引用，而不是实际的二进制文件。

#### 如何启用无二进制分发？ {#how-do-i-enable-binary-less-distribution}

要启用无二进制分发，请使用共享blob存储进行部署。
使用代理正在使用的工厂PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;检查OSGI配置中的`useBinaryReferences`属性。

#### 如何在AEM中为内容作者创建语言副本时启用权限？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

要创建语言复制功能，内容作者需要在`/content/projects`位置拥有权限。

如果还需要作者管理项目，则解决方法是将作者添加到`projects-administrators`组。

#### 在为项目创建语言副本时如何更改格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在创建翻译项目之前，在根中创建语言根和语言副本。

例如，
在`/content/geometrixx`处创建一个名为`fr_LU` (标题为法语（卢森堡）)的语言根。 随后，从“引用”面板创建页面的语言副本，并导航到`Create & Translate`中的`Create structure only`选项。 最后，创建翻译项目，然后将语言副本添加到翻译作业。

有关详细信息，请参阅下面的其他资源：

* [准备内容以进行翻译](/help/sites-administering/tc-prep.md)
* [管理翻译项目](/help/sites-administering/tc-manage.md)

#### 如何审核AEM功能（如登录尝试和ACL或权限更改）？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM引入了记录管理更改的功能，以便更好地进行故障排除和审核。 默认情况下，该信息记录在`error.log`文件中。 为了更便于监视，建议将它们重定向到单独的日志文件。
要将输出重定向到单独的日志文件，请参阅[如何在AEM中审核用户管理操作](/help/sites-administering/audit-user-management-operations.md)。

#### 如何默认启用SSL？ {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4随SSL向导提供，并提供用于配置Jetty和Granite Jetty SSL支持的用户界面。

要默认启用SSL，请参阅默认的[SSL](/help/sites-administering/ssl-by-default.md)。

#### 从移动应用程序(最好是React Native)中使用AEM的内容服务时，建议的架构是什么？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

内容服务基于Sling模型，并且AEM开发人员必须为导出的每个组件提供Sling模型pojo。

要了解如何从React应用程序使用AEM内容服务，请参阅[AEM内容服务入门](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)教程。

此外，如果开发人员希望导出组件树，他们还可以实现`ComponentExporter`和`ContainerExporter`接口，并使用`ModelFactory`对子组件进行迭代并返回其模型表示形式。 请参阅以下资源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling ：： Sling模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何禁用AEM 6.4调查弹出窗口？ {#how-to-disable-aem-survey-pop-up}

您可以使用触屏UI或Web控制台选择收集使用情况统计数据。 有关详细说明，请参阅[选择收集汇总的使用情况统计数据](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

#### 是否有重点介绍升级到AEM 6.4的主要功能的有用资源？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

请参阅[了解升级AEM的原因](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)，其中介绍了考虑升级到最新版本Adobe Experience Manager的客户的关键功能的概要细目。

## 资产 {#assets}

### 上传MP4文件（例如，使用拖放方法）时，为什么Assets工作流会重复其自身？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果用户上传的电影文件在资产节点下没有删除权限，则删除区块节点会失败，并且上传会重新启动。

#### 创建语言副本时，开箱即用配置的默认设置是什么？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

当您通过Touch UI （**引用** > **更新语言副本**）创建语言副本时，会在新语言下创建新的DAM文件夹，并从中引用资产。

这是现成配置的默认设置。 您可以在翻译配置中设置&#x200B;**翻译页面Assets** = **不翻译**。
对于AEM 6.4，**工具** > **云服务** > **翻译云服务**。

#### 如何禁用会导致AEM SegmentStore (AEM 6.3.1.1)呈指数增长的AEM组件？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以禁用OSGi组件禁用程序。 若要使用此服务，请参阅[OSGi组件禁用程序](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)。

作为解决方法，您还可以在每次AEM重新启动后通过UI或通过`curl`命令（如下示例）手动禁用组件。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自定义管理控制台？ {#how-to-customize-admin-consoles}

AEM提供了各种机制，让您能够自定义创作实例的控制台和页面创作功能。 要了解如何创建自定义控制台和自定义控制台的默认视图，请参阅[自定义控制台](/help/sites-developing/customizing-consoles-touch.md)。

#### 基于CoralUI 2的组件与基于CoralUI 3的组件有何区别？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

为Coral3创建了一组新的Granite UI Foundation的Sling组件，这些组件位于[/libs/granite/ui/components/coral/foundation下。](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html)对于基于CoralUI 2的组件有一个集合，对于基于CoralUI 3的组件有一个集合。 新集合将不仅仅是旧集合的复制粘贴，而是将被清理（例如，精简，删除已弃用的功能）。 因此，建议页面仅使用基于CoralUI 3或基于CoralUI 2的集。

要了解详细信息，请参阅[基于CoralUI 3的迁移指南](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)。

#### 如何在AEM Assets中自定义搜索组件？ {#how-to-customize-the-search-component-in-aem-assets}

若要了解搜索提升/排名以及进一步的实施信息，请参阅[简单搜索实施指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)。

简单搜索实施来自2017 Summit实验室AEM Search Demystified的材料。

#### 是否可以为WordPress构建插件，以便客户访问Adobe资产选取器来选择图像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是，使用WordPress的客户可以使用Adobe资产选取器从其AEM Assets服务器中选择图像，以添加到其WordPress网站上的帖子中。

有关详细信息，请参阅[资产选择器](../assets/search-assets.md#assetpicker)。
