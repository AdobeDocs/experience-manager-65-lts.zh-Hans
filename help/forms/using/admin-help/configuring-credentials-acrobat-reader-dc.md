---
title: 配置凭据以用于Acrobat Reader DC扩展
description: 了解如何配置凭据以用于Acrobat Reader DC扩展。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 040a4db1-45e1-4501-8117-d2d41d4a73ea
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# 配置凭据以用于Acrobat Reader DC扩展{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

要对PDF文档应用使用权限，请使用Acrobat Reader DC扩展的有效凭据配置AEM表单。 可能在安装AEM Forms期间配置了凭据。 如果在运行Configuration Manager时未配置Acrobat Reader DC Extensions凭据，或者如果需要导入新的或替换凭据，可以使用“信任存储区管理”页面进行配置。

如果您使用的是评估凭据，则在移至生产环境时，请将其替换为生产凭据。 要更新已过期或评估凭据，请首先删除旧的Acrobat Reader DC Extensions凭据。

有关获取凭据的信息，请参阅[准备安装AEM表单（单服务器）](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf)。

信任存储区可以包含多个Acrobat Reader DC Extensions凭据。 指定其中一个凭据作为默认的Reader扩展凭据。 当Workbench用户无法确定在创建进程期间要使用的凭据时，将使用默认凭据。 以下规则适用于默认凭据：

* 如果导入Acrobat Reader DC Extensions凭据，并且Trust Store不包含其他Acrobat Reader DC Extensions凭据，则将其设置为默认值。
* 如果导入的Acrobat Reader DC Extensions凭据选择了“默认”选项，则默认类型将从现有默认凭据中删除。 导入的凭据成为默认值。
* 您无法删除默认的Acrobat Reader DC Extensions凭据。 要删除默认凭据，请先将另一个凭据设置为默认凭据。 此规则的一个例外是，如果只有一个凭据，则可以将其删除，即使它是默认凭据。
* 无法更新默认的Acrobat Reader DC Extensions凭据。

>[!NOTE]
>
>您还可以以编程方式导入和删除凭据。 (请参阅[使用AEM表单编程](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)。)

## 导入Acrobat Reader DC Extensions凭据 {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

1. 在管理控制台中，单击设置>信任存储区管理>本地凭据。
1. 单击导入，然后在“信任存储类型”下，选择“Acrobat Reader DC扩展凭据”。
1. （可选）要指明此凭据是与Acrobat Reader DC Extensions一起使用的默认凭据，请选择“默认”。
1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC Extensions中凭据的显示名称。 此别名还用于使用AEM表单SDK以编程方式访问凭据。

   >[!NOTE]
   >
   >别名会自动转换为大写以便显示。 在进程中引用别名时，该别名不区分大小写。

1. 单击选择文件以查找凭据，键入凭据的密码，然后单击确定。

   如果出现错误消息“由于文件格式不正确或密码不正确导致无法导入凭据”，请验证密码是否有效。

## 删除Acrobat Reader DC Extensions凭据 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，单击设置>信任存储区管理>本地凭据。
1. 选择凭据，然后单击“删除”。

## 替换Acrobat Reader DC Extensions凭据 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，单击设置>信任存储区管理>本地凭据。
1. 记下现有凭据的别名，然后选择该凭据并单击删除。
1. 使用完全相同的别名导入新凭据。
