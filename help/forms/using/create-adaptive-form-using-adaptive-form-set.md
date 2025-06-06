---
title: 使用一组自适应表单创建自适应表单
description: 使用AEM Forms，将自适应表单整合在一起以创作单个大型自适应表单并了解其功能。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 1e9926ca-70ef-4777-8a79-f608df80ada1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 8%

---

# 使用一组自适应表单创建自适应表单{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

在工作流（如开立银行账户的申请）中，您的用户会填写多个表单。 您无需要求他们填写一组表单，而是可以将表单栈叠在一起并构建大型表单（父表单）。 将自适应表单添加到较大表单时，会将其添加为面板（子表单）。 添加一组子表单以创建父表单。 您可以根据用户输入显示或隐藏面板。 父表单的按钮（如提交和重置）将覆盖子表单的按钮。 要在父表单中添加自适应表单，您可以从资产浏览器中拖放该自适应表单（如自适应表单片段）。

可用的功能包括：

* 独立创作
* 显示/隐藏相应的表单
* 延迟加载

与使用单个组件创建父表单相比，独立创作和延迟加载等功能可提高性能。

>[!NOTE]
>
>您无法使用基于XFA的自适应表单/片段作为子表单或父表单。

## 幕后 {#behind-the-scenes}

您可以在父表单中添加基于XSD的自适应表单和片段。 父表单的结构与[任何自适应表单](../../forms/using/prepopulate-adaptive-form-fields.md)相同。 将自适应表单作为子表单添加时，它会作为面板添加到父表单中。 绑定子表单的数据存储在父表单XML架构的`afBoundData`部分的`data`根下。

例如，您的客户填写申请表。 表单的前两个字段是名称和身份。 其XML为：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

在应用程序中添加其他表单，以便客户填写其办公室地址。 子表单的架构根为`officeAddress`。 应用`bindref` `/application/officeAddress`或`/officeAddress`。 如果未提供`bindref`，则子表单将添加为`officeAddress`子树。 请参阅以下格式的XML：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

如果插入另一个允许客户提供住宅地址的表单，请应用`bindref` `/application/houseAddress or /houseAddress.`XML如下所示：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

如果要保留与架构根相同的子根名称（本示例中为`Address`），请使用索引的bindrefs。

例如，应用bindrefs `/application/address[1]`或`/address[1]`和`/application/address[2]`或`/address[2]`。 表单的XML为：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

您可以使用`bindRef`属性更改自适应表单/片段的默认子树。 `bindRef`属性允许您指定指向XML架构树结构中某个位置的路径。

如果子表单未绑定，则其数据存储在父表单的XML架构的`afUnboundData`部分的`data`根下。

您可以多次将自适应表单添加为子表单。 确保正确修改了`bindRef`，以便自适应表单的每个使用实例都指向数据根下的不同子根。

>[!NOTE]
>
>如果不同的表单/片段映射到相同的子根，则数据会被覆盖。

## 使用资源浏览器将自适应表单添加为子表单 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

执行以下步骤，使用资产浏览器将自适应表单添加为子表单。

1. 在编辑模式下打开父窗体。
1. 在侧栏中，单击&#x200B;**Assets** ![assets-browser](assets/assets-browser.png)。 在Assets下，从下拉列表中选择&#x200B;**自适应表单**。
   [![在Assets下选择自适应表单](assets/asset.png)](assets/asset-1.png)

1. 拖放要作为子表单添加的自适应表单。
   [![将自适应表单拖放到您的网站中](assets/drag-drop.png)](assets/drag-drop-1.png)您拖放的自适应表单已添加为子表单。
