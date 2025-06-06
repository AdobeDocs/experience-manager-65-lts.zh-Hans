---
title: 与Adobe Sign集成 | 处理用户数据
description: 了解AEM Forms与Adobe Sign的集成，以在自适应表单中进行电子签名。 它支持各种工作流的多个签名选项。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
exl-id: 90521ad8-703e-402b-81dd-4c06f5894358
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 与Adobe Sign集成 | 处理用户数据 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms]与[!DNL &#x200B; Adobe Sign]集成以启用自适应表单中的电子签名工作流，以处理法律、销售、工资单、人力资源管理工作流的表单或协议。 它允许单个和多用户签名、顺序和同步签名工作流、以匿名或登录用户身份签名表单以及多种验证用户的方法。

当签名者或多个签名者签名并提交自适应表单时，将生成包含签名者相关信息的[!DNL Adobe Sign]协议。

有关[!DNL AEM Forms]与[!DNL Adobe Sign]集成的详细信息，请参阅[在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 用户数据和数据存储 {#data}

[!DNL Adobe Sign]启用的自适应表单包含有关签名者的信息，并且可能包含该自适应表单收集的其他用户数据。 [!DNL Adobe Sign]服务使用协议中的签名保存用户数据。 协议保存在[!DNL AEM Forms]云服务中配置的[!DNL Adobe Sign]服务器上。 此外，如果自适应表单配置为使用Forms Portal提交操作，则协议数据与表单数据一起保存在Forms Portal数据存储中。

## 访问和删除用户数据 {#access-and-delete-user-data}

用户数据在协议内收集，但未保存在任何服务表中。 [!DNL Adobe Sign]使管理员能够自行选择管理他们在服务中控制的数据。 [!DNL Adobe Sign]服务上的隐私管理员可以根据请求者的电子邮件地址列出或删除协议。

[!DNL Adobe Sign]提供一个Web应用程序，该应用程序允许按参与者搜索协议，并在必要时删除协议。 有关详细信息，请参阅[Adobe Sign — 功能：删除用户信息](https://helpx.adobe.com/cn/sign/help/adobesign_gdpr_user_deletion.html)。

配置为使用Forms Portal提交操作的自适应表单的协议数据也保存在Forms Portal数据存储中。 要访问和删除Forms Portal数据存储中的数据，请参阅[Forms Portal | 正在处理用户数据](/help/forms/using/forms-portal-handling-user-data.md)。
