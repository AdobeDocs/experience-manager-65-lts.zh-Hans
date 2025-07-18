---
title: 无法在Google Chrome、Firefox、Microsoft&amp；reg；Edge、Microsoft&amp；reg；Internet Explorer或Apple Safari中打开基于XFA的PDF forms
description: 无法在Google Chrome、Firefox、Microsoft&amp；reg；Edge、Microsoft&amp；reg；Internet Explorer或Apple Safari中打开基于XFA的PDF forms
feature: Adaptive Forms,Document Services
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a28b084e-ec74-4c05-a90c-d447792faa41
source-git-commit: 9421c7d0b5cf80a0f2d2d82034091ffe4f875af6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 无法在Google Chrome、Firefox、Microsoft、Edge®Microsoft®Internet Explorer或Apple Safari中打开基于XFA的PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

许多近期的浏览器版本都包含自身对基于XFA的PDF forms的有限支持。 虽然这些浏览器可以打开基于XFA的PDF forms，但提供的功能有限。 如果您无法在新式浏览器中打开或提交基于XFA的PDF表单，请使用以下方法之一：

* 使用[Adobe® Acrobat®](https://www.adobe.com/acrobat.html)或[Adobe® Adobe® Reader®](https://get.adobe.com/reader/)，版本8或更高版本打开和提交基于XFA的PDF forms。
* 在Microsoft® Windows®上，Acrobat和Reader允许您配置以在“受保护的视图”模式下打开PDF，这将阻止打开基于XFA的PDF forms。 确保已禁用Acrobat或Reader中的受保护视图模式。 有关详细信息，请参阅[受保护的视图（仅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html)。
* (对于Forms开发人员) Adobe Experience Manager Forms还支持执行以下操作：

   * [将基于XFA的表单渲染到HTML5 Forms](/help/forms/using/introduction.md#key-capabilities-of-html-forms-br)，以便这些表单可以在支持HTML5的浏览器中打开，包括那些在iPad等移动设备上运行的浏览器。 表单的HTML5演绎版维护表单设计的布局，并支持嵌入到XFA表单模板中的大多数表单逻辑(如JavaScript、表单计算和表单验证)。
   * [将基于XFA的表单转换为移动响应式自适应Forms](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)。 这些表单提供响应式布局、个性化功能，并根据需要添加或删除字段或部分以动态适应用户响应。 此外，它们还为各种数据源提供现成的连接器、记录文档功能，并轻松连接到Adobe Analytics以进行性能评估。 有关详细信息，请参阅[主要特性和功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=zh-Hans)
这样，您在XFA表单中的技术投资就能得到保护，并继续为最终用户提供最佳体验。 有关详细信息，请参阅[Adobe Experience Manager Forms产品文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=zh-Hans)。
