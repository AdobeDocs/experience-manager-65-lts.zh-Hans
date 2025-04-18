---
title: 用于处理元数据、图像和视频的配置文件
description: 配置文件是一组规则，用于定义要应用于上传到文件夹中的资产的选项。 指定要应用于所上传视频资产的元数据配置文件和视频编码配置文件。 对于图像资产，您还可以指定要应用于图像资产的成像配置文件，以正确裁剪它们。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
role: User, Admin
feature: Workflow,Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
exl-id: aa257d33-302c-4a01-be48-e4ff56700bfa
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# 用于处理元数据、图像和视频的配置文件{#profiles-for-processing-metadata-images-and-videos}

配置文件是将哪些选项应用于上传到文件夹的资源的指导方针。 例如，您可以指定要应用于上载的视频资产的元数据配置文件和视频编码配置文件。 或者，什么图像配置文件要应用于图像资产才能正确裁剪。

这些规则可以包括添加元数据、智能裁剪图像或建立视频编码配置文件。 在Adobe Experience Manager中，您可以创建三种类型的用户档案，以下链接将详细介绍这些用户档案：

* [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles)
* [图像配置文件](/help/assets/image-profiles.md)
* [视频配置文件](/help/assets/video-profiles.md)

您需要管理员权限才能创建、编辑和删除元数据、图像或视频配置文件。

创建元数据、图像或视频配置文件后，可将其分配给一个或多个文件夹，用作新上传资源的目标。

在Experience Manager Assets中使用用户档案的一个重要概念就是将其分配给文件夹。 在配置文件中，是元数据配置文件形式的设置，以及视频配置文件或图像配置文件。 这些设置处理文件夹及其任何子文件夹的内容。 因此，如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件对配置文件处理这些资产的方式有显着的影响。
通过使用一致且适用的文件和文件夹命名策略以及良好的元数据做法，您可以充分利用数字资产收藏集，并确保由正确的配置文件处理正确的文件。

>[!NOTE]
>
>您从一个文件夹移动到另一个文件夹的Assets不会重新处理。 例如，假设文件夹1具有分配给它的配置文件A，而文件夹2具有分配给它的配置文件B。 如果将资产从文件夹1移至文件夹2，则已移动的资产会保留其从文件夹1进行的原始处理。
>
>即使在分配了相同配置文件的两个文件夹之间移动资产时，也是如此。

## 重新处理文件夹中的资产 {#reprocessing-assets}

>[!NOTE]
>
>仅在Experience Manager 6.4.6.0或更高版本中适用于&#x200B;*Dynamic Media - Scene7模式*。

如果文件夹已具有您后来更改的现有处理配置文件，您可以重新处理该文件夹中的资产。

例如，假设您创建了一个图像配置文件并将其分配给一个文件夹。 您上传到文件夹的任何图像资产都会自动将图像配置文件应用于资产。 但是，稍后您决定为配置文件添加一个新的智能裁切比率。 现在，您只需运行&#x200B;*Dynamic Media重新处理* <!-- *Scene7: Reprocess Assets* -->工作流，而无需再次选择并将资产重新上传到文件夹。

您可以对首次处理失败的资产运行重新处理工作流。 因此，即使您尚未编辑处理配置文件或未应用处理配置文件，您仍可以随时对资产的文件夹运行重新处理工作流。

您可以选择将重新处理工作流的批大小从默认的50个资产调整到1000个资产。 在文件夹上运行&#x200B;_Scene7：重新处理Assets_&#x200B;工作流时，资产会分批分组，然后发送到Dynamic Media服务器进行处理。 处理之后，将在Experience Manager上更新整个批次集中每个资源的元数据。 如果批次大小很大，您可能会遇到处理延迟。 或者，如果批次大小太小，则可能会导致到Dynamic Media服务器的往返次数过多。

请参阅[调整重新处理工作流的批次大小](#adjusting-load)。

>[!NOTE]
>
>如果执行从Dynamic Media Classic到Experience Manager的资源批量迁移，则必须在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
>
>必须在Dynamic Media服务器上禁用迁移发布代理，以便重新处理工作流可按预期运行。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job, and so on, until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**要重新处理文件夹中的资源：**

1. 在Experience Manager中，从Assets页面导航到已分配处理配置文件且要为其应用&#x200B;**[!UICONTROL Dynamic Media重新处理]**&#x200B;工作流的资源文件夹，

   在卡片视图中，如果文件夹已经分配了处理配置文件，则文件夹名称的正下方会显示配置文件的名称。

1. 选择文件夹。

   * 工作流会递归考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个具有资产的子文件夹，则工作流会重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，您应避免在具有1000个以上资产的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中选择&#x200B;**[!UICONTROL 时间轴]**。
1. 在页面的左下角附近，在“评论”字段的右侧，选择克拉图标( **^** )。

   ![重新处理资源工作流1](/help/assets/assets/reprocess-assets1.png)

1. 选择&#x200B;**[!UICONTROL 启动工作流]**。
1. 从&#x200B;**[!UICONTROL 启动工作流]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL Dynamic Media重新处理]**。
1. （可选）在&#x200B;**输入工作流标题**&#x200B;文本字段中，输入工作流的名称。 如有必要，您可以使用名称来引用工作流实例。

   ![重新处理资源2](/help/assets/assets/reprocess-assets2.png)

1. 选择&#x200B;**[!UICONTROL 开始]**，然后选择&#x200B;**[!UICONTROL 确认]**。

   要监视工作流或检查其进度，请从Experience Manager主控制台页面中选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]**。 在“工作流实例”页面上，选择一个工作流。 在菜单栏上，选择&#x200B;**[!UICONTROL 打开历史记录]**。 您还可以从同一个“工作流实例”页面终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批次大小 {#adjusting-load}

（可选）重新处理工作流中的默认批次大小是每个作业50个资产。 此最佳批次大小由平均资源大小以及运行重新处理的资源的MIME类型控制。 值越高，表示在单个重新处理作业中有多个文件。 因此，处理横幅会在Experience Manager资源上停留较长时间。 但是，如果平均文件大小较小（1 MB或更小），Adobe建议将该值增加到几个100，但不能超过1000。 如果平均文件大小较大（如数百MB），Adobe建议您将批次大小降低到10。

**要选择性地调整重新处理工作流的批次大小：**

1. 在Experience Manager中，选择&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;以访问全局导航控制台，然后选择&#x200B;**[!UICONTROL 工具]** （锤子）图标> **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面的“卡片视图”或“列表视图”中，选择&#x200B;**[!UICONTROL Dynamic Media重新处理]**。

   在卡片视图中选择了Dynamic Media重新处理工作流的![工作流模型页面](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具栏上，选择&#x200B;**[!UICONTROL 编辑]**。 新的浏览器选项卡将打开Dynamic Media重新处理工作流模型页面。
1. 在“Dynamic Media重新处理”工作流页面的右上角附近，选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以“解锁”该工作流。
1. 在工作流中，选择Scene7批量上传组件以打开工具栏，然后选择工具栏上的&#x200B;**[!UICONTROL 配置]**。

   ![Scene7批量上传组件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批量上载到Scene7 — 步骤属性]**&#x200B;对话框中，设置以下内容：
   * 在&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**&#x200B;文本字段中，根据需要输入作业的新标题和描述。
   * 如果您的处理程序将前进到下一步，请选择&#x200B;**[!UICONTROL 处理程序前进]**。
   * 在&#x200B;**[!UICONTROL 超时]**&#x200B;字段中，输入外部进程超时（秒）。
   * 在&#x200B;**[!UICONTROL 周期]**&#x200B;字段中，输入轮询间隔（秒），以测试外部进程的完成情况。
   * 在&#x200B;**[!UICONTROL 批处理字段]**&#x200B;中，输入Dynamic Media服务器批处理上传作业中要处理的资产最大数量(50-1000)。
   * 如果要在达到超时时前进，请选择&#x200B;**[!UICONTROL 在超时时前进]**。 如果要在达到超时时间时转至收件箱，请取消选择。

   ![属性对话框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批量上载到Scene7 — 步骤属性]**&#x200B;对话框的右上角，选择&#x200B;**[!UICONTROL 完成]**。

1. 在Dynamic Media重新处理工作流模型页面的右上角，选择&#x200B;**[!UICONTROL 同步]**。 当您看到&#x200B;**[!UICONTROL 已同步]**&#x200B;时，工作流运行时模型已成功同步并准备好重新处理文件夹中的资产。

   ![同步工作流模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 关闭显示Dynamic Media重新处理工作流模型的浏览器选项卡。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.-->
