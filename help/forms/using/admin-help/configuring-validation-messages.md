---
title: 配置验证消息
description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1172f1f2-b297-4021-a9ee-507b0a4e628a
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 4%

---

# 配置验证消息 {#configuring-validation-messages}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

For forms that are rendered as HTML, form validation errors that occur are displayed for the user. You can customize how validation messages are displayed. Depending on where the validation messages are displayed, you can also control the location of the message in the form and the size of the frame border.

## Specify how validation messages are displayed {#specify-how-validation-messages-are-displayed}

1. In administration console, click Services > forms.
1. Under Validation Output, in the Reporting list, select one of the following options:

   **Message box:** To display validation messages in a separate dialog box.

   **Frame:** To display validation messages within a frame of the same window.

   **No Frame:** To display validation messages in the same window. This value is the default.

   **Via API (with data):** To return the validation messages through the API (with data). The validation messages are not displayed on the screen.

   **Via API (with form):** To return the validation messages through the API (with the form). The validation messages are not displayed on the screen.

   **None:** To not display validation messages.

1. 单击“保存”。

## Specify the location of validation messages relative to the form returned in the web browser {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

When Reporting is set to Frame or No Frame, you can specify the location of validation messages.

1. Under Validation Output, in the Position list, select one of the following options:

   **Left:** To display validation messages on the left side of the web browser.

   **Right:** To display validation messages on the right side of the web browser.

   **Top**: To display validation messages at the top of the web browser. This value is the default.

   **Bottom**: To display validation messages at the bottom of the web browser.

1. 单击“保存”。

## 指定框架边框大小 {#specify-the-frame-border-size}

当“报告”设置为“帧”时，可以指定帧边框大小。

1. 在“验证输出”下的“边框大小”框中，键入框架边框的大小（以像素为单位）。

   边框大小必须等于或大于0。 默认值为 1。

1. 单击“保存”。
