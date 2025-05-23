---
title: 查看系统信息
description: 了解如何查看资源监控图表以及运行AEM表单的服务器的相关信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6be4ce1d-39fe-4a25-9d4e-f1cbc593d2c7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 查看系统信息 {#view-system-information}

“系统”选项卡显示资源监控图表和运行AEM表单的服务器的相关信息。 要访问此信息，请在管理控制台中单击页面右上角的运行状况监视器。 如果在群集环境中运行AEM表单，则显示的信息适用于从“服务器”列表中选择的节点。

要将当前系统信息保存为属性文件，请单击“保存”。

“系统”选项卡的右侧窗格显示以下信息的图形表示：

* 作业和工作计数项
* 栈和已提交的栈使用情况
* 非栈和已提交的非栈使用情况

您可以沿时间轴拖动指针以获取特定时间点的值。

>[!NOTE]
>
>图形数据、服务器信息值和时钟时间每10分钟更新一次。 该信息不会实时显示。

“系统”选项卡的左窗格显示有关服务器或节点的以下信息：

**虚拟机：** Java虚拟机(JVM)版本。

**虚拟机供应商：** JVM的制造商。

**虚拟机版本：** JVM版本号

**计算机名：**&#x200B;安装AEM表单的服务器的主机名。

**启动时间：**&#x200B;服务器已运行的时间（以小时和分钟为单位）。

**Just-In-Time Compiler：**&#x200B;正在使用的编译器名称。

**编译时间：**&#x200B;编译所花费的时间。

**实时Threads数：** AEM表单系统中当前存在的线程总数。

**Threads峰值数：**&#x200B;系统上记录的最大实时线程数。

**加载的类数：**&#x200B;加载到JVM中的类数。

**卸载的类数：**&#x200B;从JVM卸载的类数。

**最小栈：**&#x200B;已使用的最小栈数量。

**最大栈：**&#x200B;已使用的最大栈数量。

**操作系统名称：**&#x200B;在AEM Forms服务器上运行的操作系统的名称。

**操作系统版本：**&#x200B;在AEM Forms服务器上运行的操作系统的版本号。

**操作系统Arch：** JVM正在其上运行的操作系统体系结构。

**处理器数：**&#x200B;系统上的处理器数。

**虚拟机参数：** JVM使用的参数。

**类路径：** JVM使用的类路径。

**库路径：** JVM使用的库路径。

**启动类路径：** JVM使用的启动类路径。

**应用程序服务器类型：**&#x200B;用于运行AEM表单的应用程序服务器的类型。

**应用程序服务器版本：**&#x200B;用于运行AEM表单的应用程序服务器的版本号。

**应用程序服务器供应商：**&#x200B;用于运行AEM表单的应用程序服务器的制造商。

**安装日期：**&#x200B;安装AEM表单的日期（格式为yyyy-mm-dd）。

**AEM表单版本：**&#x200B;已安装的AEM表单版本。

**修补程序版本：** AEM表单修补程序编号。

**数据库名称：** AEM表单使用的数据库类型。

**数据库版本：** AEM表单使用的数据库的版本号。

**数据库驱动器名称：** JVM用于连接到数据库的驱动程序的名称。

**数据库驱动程序版本：** JVM用于连接到数据库的驱动程序的版本。

使用&#x200B;**保存**&#x200B;按钮可以将此系统信息保存在属性文件中。
