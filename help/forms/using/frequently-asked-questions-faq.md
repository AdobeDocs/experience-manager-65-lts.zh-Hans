---
title: 自适应Forms、HTML5表单和AEM Forms的常见问题解答(FAQ)
description: 有关自适应Forms、HTML5表单和AEM Forms的布局、脚本支持和范围的常见问题解答(FAQ)。
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 69c71f6e-a802-45da-a931-28436c7fc1f6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 4%

---

# 常见问题解答（FAQ） {#frequently-asked-questions-faq}

1. 为什么中的条形码和签名字段未显示在我的HTML 5表单中？

   回答：条形码和签名字段在HTML或移动设备场景中无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名涂写字段，该字段可用于代替签名字段。 还可以添加用于条形码的[自定义构件](../../forms/using/custom-widgets.md)并将其集成。
