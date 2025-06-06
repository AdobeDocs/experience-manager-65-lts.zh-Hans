---
title: 监视文件夹的备份策略
description: 本文档介绍了受监视的文件夹如何受不同的备份和恢复方案的影响，这些方案的局限性和结果，以及如何最大限度地减少数据丢失。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5955deb0-9d1c-4b61-a202-41ef03a23cf8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# 监视文件夹的备份策略 {#backup-strategies-for-watched-folders}

本内容将介绍监视的文件夹如何受不同的备份和恢复方案的影响，这些方案的局限性和结果，以及如何最大限度地减少数据丢失。

*Watched文件夹*&#x200B;是一个基于文件系统的应用程序，该应用程序调用配置的服务操作，这些操作在watched文件夹层次结构中的以下文件夹之一中处理文件：

* 输入
* 暂存
* 输出
* 失败
* 保留

用户或客户端应用程序首先将该文件或文件夹放入输入文件夹中。 然后，服务操作将文件移动到暂存文件夹以进行处理。 服务执行指定的操作后，将修改的文件保存在输出文件夹中。 已成功处理的源文件将移至保留文件夹，处理失败的文件将移至失败文件夹。 启用观察文件夹的`Preserve On Failure`属性后，失败的已处理源文件将移至保留文件夹。 （请参阅[配置观察文件夹端点](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。）

您可以通过备份文件系统来备份观察文件夹。

>[!NOTE]
>
>此备份独立于数据库或文档存储备份和恢复过程。

## 观察文件夹的工作方式 {#how-watched-folders-work}

此内容描述观察文件夹文件操作过程。 在制定恢复计划之前了解此过程非常重要。 在此示例中，启用了watched文件夹的`Preserve On Failure`属性。 文件将按照其到达的顺序进行处理。

下表描述了在整个过程中对五个示例文件(file1、file2、file3、file4、file5)进行的文件操作。 在表中，x轴表示时间，如Time 1或T1，y轴表示观察文件夹层次结构中的文件夹，如Input。

<table>
 <thead>
  <tr>
   <th><p>文件夹</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>输入</p></td>
   <td><p>文件1、文件2、文件3、文件4</p></td>
   <td><p>文件2、文件3、文件4</p></td>
   <td><p>文件3，文件4</p></td>
   <td><p>文件4</p></td>
   <td><p>空</p></td>
   <td><p>文件5</p></td>
   <td><p>空</p></td>
  </tr>
  <tr>
   <td><p>暂存</p></td>
   <td><p>空</p></td>
   <td><p>文件1</p></td>
   <td><p>文件2</p></td>
   <td><p>文件3</p></td>
   <td><p>文件4</p></td>
   <td><p>空</p></td>
   <td><p>文件5</p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
  </tr>
  <tr>
   <td><p>失败</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>文件1 </p></td>
   <td><p>文件1，文件2 </p></td>
   <td><p>文件1，文件2 </p></td>
   <td><p>文件1、文件2、文件4 </p></td>
   <td><p>文件1、文件2、文件4 </p></td>
  </tr>
 </tbody>
</table>

以下文本描述了每次的文件操作：

**T1：**&#x200B;四个示例文件都放在输入文件夹中。

**T2：**&#x200B;服务操作将file1移到stage文件夹中进行操作。

**T3：**&#x200B;服务操作将file2移到stage文件夹中以进行操作。 它将file1的结果放置在输出文件夹中，并将file1移动到保留文件夹中。

**T4：**&#x200B;服务操作将file3放置到暂存文件夹中以进行操作。 它将file2的结果放置在输出文件夹中，并将file2放置在preserve文件夹中。

**T5：**&#x200B;服务操作将file4放置在阶段文件夹中以进行操作。 对file3的操作失败，服务操作将其置于失败文件夹中。

**T6：**&#x200B;服务操作将file5放置在输入文件夹中。 它将file4的结果放置在输出文件夹中，将file4放置在preserve文件夹中。

**T7：**&#x200B;服务操作将file5放置在阶段文件夹中以进行操作。

## 备份观察文件夹 {#backing-up-watched-folders}

建议您将整个监视文件夹文件系统备份到另一个文件系统。

## 正在恢复观察文件夹 {#restoring-watched-folders}

本节介绍如何恢复观察文件夹。 观察文件夹通常会调用在一分钟内完成的短暂进程。 在这种情况下，通过每小时执行一次的备份来恢复受监视的文件夹并不能防止数据丢失。

例如，如果在时间T1进行备份，而服务器在T7失败，则已经处理file1 、 file2 、 file3和file4。 在T1使用备份还原观察文件夹并不能防止数据丢失。

如果进行了较新的备份，则可以恢复文件。 恢复文件时，请考虑当前文件所在的观察文件夹层次结构文件夹：

**阶段：**&#x200B;在还原观察文件夹后再次处理此文件夹中的文件。

**输入：**&#x200B;在还原观察文件夹后再次处理此文件夹中的文件。

**结果：**&#x200B;不处理此文件夹中的文件。

**输出：**&#x200B;不处理此文件夹中的文件。

**保留：**&#x200B;不处理此文件夹中的文件。

## 最大限度地减少数据丢失的策略 {#strategies-to-minimize-data-loss}

在恢复观察文件夹时，以下策略可以最大限度地减少输出和输入文件夹数据丢失：

* 经常备份输出和故障文件夹（例如每小时），以避免丢失结果和故障文件。
* 将输入文件备份到watched文件夹以外的文件夹中。 这样可以确保在恢复后文件可用性，以防您在输出或故障文件夹中找不到文件。 确保您的文件命名方案一致。

  例如，如果以&#x200B;`%F.`*扩展名*&#x200B;保存输出，则输出文件将与输入文件同名。 这有助于您确定要处理的输入文件以及必须重新提交的输入文件。 如果在result文件夹中只看到file1_out文件，而不是file2_out、file3_out和file4_out，则必须重新提交file2、file3和file4。

* 如果可用的watched文件夹备份的时间早于处理作业所需的时间，则您应允许系统创建一个watched文件夹，并自动将文件放入输入文件夹中。
* 如果最新的可用备份不够新，则备份时间少于处理文件所需的时间，并且会恢复监视文件夹，则会在以下不同阶段之一中处理文件：

   * 输入文件夹中的&#x200B;**阶段1：**
   * **阶段2：**&#x200B;已复制到阶段文件夹，但尚未调用进程
   * **阶段3：**&#x200B;已复制到阶段文件夹并调用进程
   * **阶段4：**&#x200B;操作正在进行中
   * **阶段5：**&#x200B;返回的结果

  如果文件处于阶段1，则将对其进行操作。 如果文件位于阶段2或阶段3，请将它们放在输入文件夹中，以便再次进行操作。

  >[!NOTE]
  >
  >如果文件操作发生多次，将防止数据丢失，但结果可能会重复。

## 结论 {#conclusion}

由于监视文件夹的动态性和不断变化的特性，对于一天内备份的文件，应恢复监视文件夹。 最佳做法是备份结果，将输入文件夹存储在服务器上，并跟踪输入文件，以便在出现故障时可以重新提交作业。
