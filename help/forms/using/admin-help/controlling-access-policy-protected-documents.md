---
title: 控制对受策略保护的文档的访问
description: 了解如何查看、管理和控制对受策略保护文档的访问。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 553c0a95-26e9-4d2c-b53d-846861c6a1d7
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 0%

---

# 控制对受策略保护的文档的访问 {#controlling-access-to-policy-protected-documents}

您可以控制收件人使用受策略保护文档的方式，而不管文档分发的范围如何。

使用“文档”页，您可以执行以下任务：

* 搜索并查看受策略保护文档的详细信息。 您可以查看有关文档名称、发布者名称、策略名称以及应用策略的日期的信息。 如果删除了保护文档的策略，您还可以在策略名称下看到已删除的策略ID。 用户可以查看和管理自己受策略保护的文档。 管理员可以查看和管理所有受策略保护的文档。
* 更改应用于文档的策略的详细信息。 用户可以编辑自己的策略，管理员可以编辑共享策略和个人策略，策略集协调员可以编辑他们具有权限的策略集中的共享策略。 您可以直接从“文档详细信息”页面访问与文档关联的策略。
* 撤销和恢复对受策略保护文档的访问权限。 管理员可以撤销和恢复对任何文档的访问权限。 策略集协调员（有权管理文档）可以从其策略集中撤销和恢复对使用共享策略的受策略保护文档的访问权限。 如果用户创建了保护文档的策略，或者该策略是允许此功能的共享策略，则用户可以撤销对其受策略保护文档的访问权限。
* 切换应用于文档的策略。 如果将策略应用到文档，则创建策略或共享策略启用此功能的用户可以切换策略。 策略集协调员可以从其策略集中切换策略。 管理员可以切换应用于任何文档的策略。

当文档受策略保护并且您撤销访问权限或切换应用的策略时，更改将按如下方式生效：

* 如果文档处于联机状态，除非用户打开了文档，否则将立即应用更改。 在这种情况下，用户必须关闭文档才能使更改生效。
* 如果收件人脱机使用文档（例如在笔记本电脑上），则下次收件人通过打开任何受策略保护的文档与Document Security同步时，更改将生效。

## 查看有关文档的信息 {#view-information-about-a-document}

对于“文档”页面上列出的每个文档，您可以看到文档名称、发布者名称、策略名称和文档受保护日期。 如果保护文档的策略已删除，则该策略ID将列在“策略名称”下。

您还可以在“文档详细信息”页面上查看有关特定文档的更多详细信息（如下所述）：

>[!NOTE]
>
>使用“文档详细信息”页面上的“策略名称”链接可访问在Microsoft Outlook中为附加到电子邮件的文档的收件人自动生成的策略。 这些策略不会显示在策略页面上。

**文档名称：**&#x200B;所选文档的名称。

**文档ID：** Document Security在将策略应用于文档时分配的唯一标识符。 document security使用此编号跟踪文档。

**文档状态：**&#x200B;文档状态（例如，活动或吊销。）

**发布者：**&#x200B;将策略附加到文档的用户的名称。

**策略名称：**&#x200B;用于保护文档的策略的名称。 您可以单击该名称以打开策略。 使用此链接可访问Acrobat为Outlook中附加到电子邮件的文档收件人生成的策略。 这些策略不会显示在“策略”页面上。

**策略类型：**&#x200B;应用于文档的策略类型。

**发布日期：**&#x200B;将策略应用到文档的日期。

**相关迭代：**&#x200B;如果文档具有相关迭代，则该项也会出现在列表中。 单击链接可查看文档的相关小版本列表。

用户可以查看有关其受保护文档的信息。 管理员可以查看任何用户受策略保护的文档的相关信息。 策略集协调员可以查看受策略保护且不受策略集保护的文档的相关信息。

1. 在Document Security页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。 “文档详细信息”页面将打开，显示有关文档的详细信息。 此页面还提供了撤销文档访问、切换策略和查看与此文档相关的事件的选项。

## 查看文档的相关小版本 {#view-related-iterations-for-a-document}

如果启用了跟踪相关小版本，则可以跟踪各个用户已保存的文档版本。 此功能仅受某些应用程序（如PTC Pro/ENGINEER Wildfire）的支持。

当多个用户协作并保存同一文档的不同版本时，此功能非常有用。 document security可以跟踪各种迭代；因此，您可以轻松查看不同版本的文档信息。

如果启用了此功能，则可以从“文档”页面查看文档的相关小版本。

1. 查看文档的文档详情页面。 （请参阅[查看有关文档的信息](controlling-access-policy-protected-documents.md#view-information-about-a-document)。）
1. 单击“查看相关小版本”。 仅当启用该功能时，该选项才可用。 此时将显示相关小版本的列表。 对于每个小版本，可以查看以下信息：

   * **迭代：**&#x200B;文件名。 它可能与原始文件名不同，并且末尾附加了一个版本号。
   * **发布者：**&#x200B;原始文档的发布者。
   * **创建者：**&#x200B;保存迭代的用户。
   * **创建日期：**&#x200B;保存迭代的日期和时间。
   * **策略：**&#x200B;保护迭代的策略。 不同的迭代可能受不同的策略保护。

1. 要显示该小版本的“文档详细信息”页面，请单击小版本的文件名。

## 撤销和恢复对文档的访问 {#revoking-and-reinstating-access-to-documents}

您可以撤销和恢复对受策略保护文档的访问权限：

**用户：**&#x200B;可以撤销或恢复对受其保护的文档的访问权限，这些文档通过其个人策略或共享策略进行保护，对于应用该策略的用户，这些共享策略启用了撤销功能。 无法撤销文档访问权限或切换策略的用户需要联系管理员。

**管理员：**&#x200B;可以撤销或恢复任何受策略保护文档的访问权限，包括受个人或共享策略保护的文档。 如果管理员撤销对受共享策略保护的文档的访问权限，则只有管理员可以恢复该文档的访问权限。

**策略集协调器：**&#x200B;可以撤销或恢复其策略集中的策略所保护的文档的访问权限。

当您撤销或恢复文档访问权限时，更改将在以下时间生效：

* 如果文档处于在线状态并已关闭，则下次收件人通过打开受策略保护的文档与Document Security同步时，更改将生效。
* 如果文档在线且处于打开状态，则更改将在收件人关闭文档时生效。
* 如果文档处于脱机状态（即正在没有Internet连接的情况下使用，例如在笔记本电脑上），则下次收件人与document security同步时，更改将生效。

**撤销对受策略保护文档的访问权限**

1. 在Document Security页面上，单击“文档”。
1. 选中相应文档旁边的复选框，然后单击“撤消”。 您可以一次撤消对多个文档的访问权限。
1. 选择在撤消文档后向尝试打开文档的用户显示的消息：

   * **常规消息：**&#x200B;指示作者已撤消文档
   * **文档已终止：**&#x200B;表示作者已终止文档
   * **文档已修订**：指示作者已修订文档

1. （可选）如果文档有较新版本可用，请输入URL并单击测试以验证该URL。
1. 单击“确定”，然后再次单击“确定”以返回“文档”页。

**恢复文档访问权限**

1. 在Document Security页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。
1. 单击取消撤销，然后单击确定。

## 切换应用于文档的策略 {#switch-a-policy-that-is-applied-to-a-document}

用户、策略集协调员和管理员可以切换应用于受策略保护文档的策略（您一次只能对文档应用一个策略）。 如果用户创建了策略，或者该策略是启用了此功能的共享策略，则用户可以切换应用于自己受策略保护的文档的策略。 否则，管理员或策略集协调员必须切换策略。 管理员可以为任何用户的受策略保护文档切换策略。 策略集协调员可以从其策略集中切换策略。

When you switch a policy, the new policy is enforced as follows:

* If the document is online and closed, the change takes effect the next time the recipient synchronizes with document security by opening any policy-protected document online.
* If document is online and open, the change takes effect when the user closes the document.
* If the document is offline (in use without an active Internet or network connection, such as on a laptop), the change is applied the next time the user synchronizes with document security by opening a policy-protected document online.

>[!NOTE]
>
>To permit anonymous access to a policy-protected document that currently does not have this access, remove the existing policy in the client application and then apply a policy that permits anonymous access. If you switch the policy, users still must log in to access the document.

1. 在Document Security页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。
1. Click Switch Policy. A list of up to 100 policies appears.
1. If the policy you want is not displayed, select Policy Name or Policy ID from the Find list, type the name or ID, and click Find.
1. Click a new policy in the list.
1. Click Switch Policy, and then click OK to return to the Documents page.

## Search for a document {#search-for-a-document}

You can search for documents on the Documents page by using a combination of date range criteria and the search criteria that are available in the list. These criteria include the document name, policy name, or all documents.

Some additional search options are only available to administrators:

**Document ID:** Unique ID number that document security assigns to the document when the policy is applied.

**Document name:** Name of the document.

**Publisher name:** Name of the user who attached the policy to the document. You can select the user from all domains or a specified domain.

**Policy ID:** ID number of the policy that is attached to the document.

**Policy name:** Name of the policy that is attached to the document.

**All documents:** All documents protected by administrators and users. Using the All Documents option to search may return a long list of documents.

1. 在Document Security页面上，单击“文档”。
1. 在“查找”列表中，选择所需的搜索条件。

   可以将条件指定为文档ID、文档名称、发布者名称、策略ID、策略名称或所有文档。

   如果指定发布者名称，请单击“通讯簿”图标并指定要搜索用户的域，然后单击“确定”以返回到“文档”搜索页。

1. （可选）在日期列表中，选择一个日期范围选项。 如果选择自定义日期，请在显示的框中以yyyy/mm/dd格式键入日期，或者使用日期选取器指定日期范围：

   * 单击日历以打开日期选取器。
   * 使用箭头查找年和月。
   * 单击日历上某月的某一天。
   * 单击“确定”以关闭日期选取器。

1. 单击“查找”。

## 对文档列表排序 {#sort-the-document-list}

您可以按列标题对文档列表进行排序。 列标题旁边的三角形图标指示当前使用哪一列进行排序。 向上三角形表示升序，向下三角形表示降序。

1. 在Document Security页面上，单击“文档”。
1. 单击相应的列标题。
1. 要更改排序顺序，请再次单击该列。

## 将封面页添加到受策略保护的文档 {#add-cover-page-to-policy-protected-documents}

如果存在大多数非Adobe PDF查看者，当您打开Document Security受保护的文档时，第一页显示为空白页，或者应用程序在没有打开文档的情况下中止。

您可以使用页面0（包装文档）支持来允许非Adobe PDF查看者打开受保护的文档并在文档中显示封面页。

>[!NOTE]
>
>在Adobe Reader/Acrobat或Mobile Reader中查看此类文档（包含页面0）时，默认情况下会打开受保护的文档。

**向受策略保护的文档添加封面页**

在Workbench中使用以下流程：

**保护
具有封面页的文档：**&#x200B;使用指定的策略保护PDF文档，并向该文档添加封面页

**提取受保护的文档：**&#x200B;从带有封面页的PDF文档提取受策略保护的PDF文档

使用以下Document Security API：

**protectDocumentWithCoverPage：**使用指定的策略保护给定PDF的安全，并返回包含封面页和受保护文档的文档作为附件
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument：**提取作为封面页文档附件的受保护文档。 可以使用protectDocumentWithCoverPage方法创建具有封面页的文档
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
