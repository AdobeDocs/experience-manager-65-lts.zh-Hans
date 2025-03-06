---
title: 手势自定义
description: 了解如何在AEM Forms应用程序上自定义手势。 您可以自定义手势，以提供与应用程序交互的不同方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: d89005b3-8478-4b74-b28b-200c121eea3a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 手势自定义 {#gesture-customization}

您可以自定义AEM Forms应用程序的手势，以便提供与该应用程序交互的不同方法。 例如，您可以添加新的手势以打开或关闭任务或起点。

## 在AEM Forms应用程序中自定义手势 {#to-customize-gestures-in-aem-forms-app}

在AEM Forms应用程序中，向左轻扫可打开新任务或起点，而向右轻扫则不执行任何操作。 以下示例提供了在AEM Forms应用程序中执行右键单击手势时打开新任务或起点的步骤。

1. 打开您的项目。

   * 对于iOS，在Xcode中打开`Capture.xcodeproj`
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，在Visual Studio中打开`MWSWindows.sln`。

1. 导航到视图文件夹并打开`task.js`文件以进行编辑。

   * 在Xcode中，导航到&#x200B;**Capture > www > wsmobile > js > runtime > views**&#x200B;文件夹。
   * 在Eclipse中，导航到&#x200B;**assets > www > wsmobile > js > runtime > views**&#x200B;文件夹。
   * 在Visual Studio中，导航到&#x200B;**MWSWindows > www > wsmobile > js >运行时>视图**&#x200B;文件夹。

   >[!NOTE]
   >
   >task.js文件包含与任务或“起点”列表中列出的每个任务或“起点”相关联的骨干视图。

1. 在`task.js`文件中，搜索视图的events属性。

   events属性是一个映射，每个条目的格式为：

   `"EventName Selector": "Function"`

   当您在`Selector`指定的JavaScript元素上触发名为`EventName`的HTML事件时，将调用`Function`。

1. 查找

   * &quot;select .taskContentArea&quot; ： &quot;onTaskClick&quot;，

     &quot;select .taskOpenArea&quot; ： &quot;onTaskClick&quot;，

     &quot;select .task-content&quot; ： &quot;onTaskClick&quot;，

     &quot;select .last_empty_div&quot; ： &quot;onTaskClick&quot;，

   并将其替换为

   * &quot;轻扫.taskContentArea&quot; ：&quot;onTaskClick&quot;，

     &quot;轻扫.taskOpenArea&quot; ：&quot;onTaskClick&quot;，

     &quot;轻扫.task-content&quot; ：&quot;onTaskClick&quot;，

     &quot;轻扫.last_empty_div&quot; ：&quot;onTaskClick&quot;，

1. 保存并关闭`task.js`文件。
1. 构建并运行AEM Forms应用程序。 现在，您可以使用左滑动和右滑动来打开。

同样，您可以对其他视图中的各种手势、HTML元素和函数组合进行更改。
