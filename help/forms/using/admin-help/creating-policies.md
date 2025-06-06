---
title: 创建和管理策略
description: 策略是一组机密性设置和用户，用户可以访问应用了该策略的文档。 您可以使用AEM表单创建和管理各种类型的策略。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e8faf76e-5287-4b0c-b440-f348443287f3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 0%

---

# 创建和管理策略 {#creating-and-managing-policies}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

*策略*&#x200B;定义了一组机密性设置以及可以访问应用了该策略的文档的用户。 *策略集*&#x200B;用于对具有共同业务目的的一组策略进行分组。 然后，这些策略集将提供给系统中的部分用户。 有关策略的详细信息，请参阅[策略和受策略保护的文档](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents)。

## 策略类型 {#types-of-policies}

Document Security提供了以下类型的策略。

**个人策略**

用户可以创建、编辑、复制、删除和应用自己的策略，并使用适合特定情况的设置。 只有创建策略的人和管理员可以访问该个人策略。 个人策略显示在“策略”页的“我的策略”选项卡上。

如果管理员启用此权能，受邀用户还可以创建、编辑、复制和删除个人策略。

**共享策略**

管理员和策略集协调员根据贵组织为不同类型的文档和用户标识的机密性要求创建共享策略。 共享策略包含在策略集中，并且对于特定策略集可供所有授权用户（文档发布者、策略集协调者和文档收件人）使用。 管理员和策略集协调员可以启用和禁用共享策略。 共享策略显示在“策略”页的“策略集”选项卡上的策略集中。

首次安装Document Security时，它包含一个名为&#x200B;*Restrict to All Principals*&#x200B;的共享策略。 当将此策略应用于文档时，任何可以登录Document Security的用户都可以访问该文档。 此策略位于名为&#x200B;*全局策略集*&#x200B;的策略集中。 默认情况下，不启用此策略。 如果它适合您组织的需要，则可以启用它。

**Microsoft® Outlook自动生成的策略**

使用Acrobat，您可以将策略应用到在Microsoft® Outlook中作为电子邮件附件发送的文档。 在Outlook中，可以使用现有策略保护文档。 或者，您也可以使用Acrobat通过默认机密性设置生成的自动生成策略，该策略适用于附加到电子邮件的文档。 (请参阅&#x200B;*[Acrobat帮助](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*。)

>[!NOTE]
>
>要使策略在Outlook中可用，您必须在Acrobat中将策略设置为收藏。 所有其他策略（包括您作为发布者的策略）不会显示在Outlook中。

## 谁可以创建和管理策略和策略集 {#who-can-create-and-manage-policies-and-policy-sets}

与策略和策略集交互的方式取决于您在组织内的角色：

**用户：**&#x200B;用户可以创建、编辑和删除其个人策略。 如果管理员启用此功能，受邀用户也可以创建个人策略。

**策略集协调员：**&#x200B;策略集协调员可以在被指定为协调员的策略集中创建和管理共享策略。 策略集协调员通常是组织内的专家，可以最好地编写特定策略集中的策略。

**管理员：**&#x200B;管理员可以编辑任何用户的个人策略。 他们可以创建共享策略。 他们还可以创建、编辑和删除策略集，以及指定策略集协调器。

有关各种Document Security角色的详细信息，请参阅[关于Document Security用户](/help/forms/using/admin-help/document-security.md#about-document-security-users)。

## 创建和编辑策略 {#creating-and-editing-policies}

用户可以创建或编辑个人策略供自己使用。 管理员和策略集协调员可以为您的组织创建或编辑共享策略。

### 编辑策略的注意事项 {#considerations-for-editing-policies}

在编辑策略时，更改会影响策略当前保护的文档，以及之后策略保护的文档。 例如，如果从应用于文档的策略中删除收件人，则收件人无法再打开该文档。

文档的状态决定了更改何时生效：

* 如果文档处于联机状态，除非用户打开了文档，否则将立即应用更改。 在这种情况下，用户必须关闭文档才能使更改生效。
* 如果收件人脱机使用该文档（例如，在笔记本电脑上），则更改会在收件人下次联机该文档时生效。 然后，它通过打开任何受策略保护的文档与Document Security同步。

>[!NOTE]
>
>在Microsoft® Outlook中，Acrobat为附加到电子邮件的文档收件人自动生成的策略不会出现在策略列表中。 您只能通过打开关联文档的文档详情页面来查看这些策略。

在编辑策略时，以下限制适用：

* 只有在管理员启用此功能时，受邀用户才能编辑策略。 如果无法编辑策略，则“编辑”选项将不可用。
* 策略集协调员只有在拥有正确的权限时才可以编辑策略集中的策略。 超级用户或策略集管理员在Document Security管理员界面中设置这些权限。
* 如果策略配置了自创建策略后管理员删除的水印，则编辑并保存策略时，将不再将此水印应用于文档。 只要不编辑策略，已删除的水印仅对现有策略保持有效。 如果编辑策略，则必须选择另一个水印来替换已删除的水印。
* 您不能通过编辑应用的策略来授予对文档的匿名访问权限。 如果编辑策略，用户仍必须登录才能访问该文档。 若要对此文档应用匿名访问，请先删除客户端应用程序中的策略，然后应用另一个允许匿名访问的策略。
* 在Microsoft Outlook中，Acrobat为附加到电子邮件的文档收件人自动生成的策略不会出现在策略列表中。 要访问此策略，请在“文档”页面上找到文档，打开“文档详细信息”页面，然后单击文档详细信息列表中的策略名称。

**创建或编辑策略**

1. 在Document Security页面上，单击策略，然后单击以下选项卡之一：

   * 要创建或编辑个人策略，请单击“我的策略”选项卡。
   * 要创建或编辑共享策略，如果具有权限，请单击“策略集”选项卡，单击相应的策略集名称，然后单击“策略”选项卡。

1. 单击新建或从列表中选择要编辑的策略。
1. 在名称框中，键入唯一标识策略的名称。 在“描述”框中，描述策略的用途以及何时使用策略。 如果策略位于策略集中，则所有指定用户的名称和描述都会显示在策略列表中。 个人策略仅供用户和管理员使用。

   名称或描述中不能使用以下字符：

   * 小于号(&lt;)
   * 大于号(>)
   * 与号(&amp;)
   * 单引号(&#39;)
   * 双引号(“)
   * 反斜线(\)
   * 正斜杠(/)

   如果在名称或描述中使用了以下字符，则它们会转换为空格：

   * 回车（ASCII字符13）
   * 换行（ASCII字符10）。

   >[!NOTE]
   >
   >您可以创建包含扩展字符的策略名称；但是，当在两个字符串之间进行比较时，重音和非重音字符（如“e”和“é”）被视为相同。 当有人创建策略时，将进行比较以检查是否存在同名策略。 比较无法区分相同的名称，重音字符除外。 假定策略已添加到数据库，但未添加新策略。

1. 将用户和组添加到策略并设置适当的权限。 （请参阅[用户和组](creating-policies.md#users-and-groups)。）
1. 在常规设置下，选择相应的选项。 （请参阅[常规设置](creating-policies.md#general-settings)。）
1. （可选）如果适用，请选择外部授权提供方并指定其属性。 如果不想使用外部授权提供程序，请单击“删除默认提供程序”。

   外部授权提供程序用于设置策略中的属性，在选中时，外部授权提供程序将使用此信息来评估策略。 可用属性由管理员和安装软件的人配置。

1. 在高级设置下，选择相应的选项。 （请参阅[高级设置](creating-policies.md#advanced-settings)。）
1. 在“不可更改高级设置”下，选择相应的选项。 （请参阅[不可更改的高级设置](creating-policies.md#unchangeable-advanced-settings)。）
1. 单击“保存”。 该策略将显示在策略列表中。 新策略旁边会显示一个带有红色圆圈的图标，表示该策略仍处于禁用状态。

   要使策略可供用户使用，请启用该策略。 （请参阅[启用或禁用共享策略](creating-policies.md#enable-or-disable-shared-policies)。）

### 用户和组 {#users-and-groups}

在“用户和组”区域中，指定有权访问受策略保护的文档的用户。 对于您指定的每个用户或组，您还可以设置文档使用权限。

>[!NOTE]
>
>文档发布者是使用策略保护文档的用户。 默认情况下，此用户始终包含在策略中，具有完全访问权限，包括吊销和策略切换功能。 但是，管理员可以更改文档发布者对共享策略的访问权限。 例如，管理员可以限制文档发布者撤销文档访问权限或切换策略。

**添加用户或组：**&#x200B;要添加用户或用户组，请单击“添加用户或组”，然后单击“高级搜索”，以便查找用户或组。 用户包括贵组织的内部用户和已向Document Security注册的受邀用户。 选择此选项时，将显示“添加用户或组”页：

* 在“查找”框中，键入用户或组名或电子邮件地址。
* 在使用列表中，选择名称或电子邮件。
* 在“类型”列表中，选择“用户”或“组”。
* 从“In（范围）”列表中选择要搜索的域，然后单击“Find（查找）”。
* 返回结果时，选择要添加的用户或组，然后单击“添加”。

>[!NOTE]
>
>如果您输入了正确的受邀用户名或电子邮件地址，但未返回任何结果，则该用户可能尚未注册，或者该帐户可能已被删除。 您可以尝试将用户添加为受邀用户类型或与管理员联系。

**邀请新用户：**&#x200B;若要添加受邀用户，请单击“邀请新用户”，在出现的框中键入该用户的电子邮件地址，然后单击“邀请”。 仅当管理员启用此选项时，它才可用。 将新的受邀用户添加到策略时，如果尚未邀请用户注册，则Document Security会发送注册邀请电子邮件。 用户必须使用电子邮件中的链接创建帐户，然后必须激活该帐户。

注册后，受邀用户可以使用他们有权访问的受策略保护文档。 根据管理员启用的权能，外部用户可能有权将策略应用到文档、创建、编辑和删除策略，以及将其他外部用户添加到策略中。

**添加匿名用户：**&#x200B;若要允许匿名用户访问，请单击“添加匿名用户”。 仅当管理员为Document Security启用了匿名用户访问时，此选项才可用。 （请参阅配置Document Security服务器。） 此选项授予每个人访问此策略保护的文档的权限，无论他们是否具有Document Security帐户。 如果选择此选项，则无法将其他类型的用户添加到策略中。

>[!NOTE]
>
>要允许对当前没有受策略保护的文档进行匿名访问，请删除现有策略，然后应用允许匿名访问的策略。 如果切换或更改现有策略，用户仍必须登录才能访问该文档。

#### 指定用户和组的文档权限 {#specify-the-document-permissions-for-users-and-groups}

您可以一次为一个用户或组指定文档权限，也可以从列表中选择多个用户和组，并使用列标题区域中的选项更改其权限。

默认情况下，所有受策略保护的文档都具有允许用户在线打开它们的权限。

“权限和选项”选项卡显示在Document Security中。

这些文档权限在“权限”选项卡上提供。 您可以将这些权限应用于PDF、PTC Pro/E和Microsoft Office文件。

**打印：**&#x200B;允许用户打印受此策略保护的文档。 对于Office和Pro/E文件，可以选中“打印”复选框以允许打印，或清除该复选框以防止打印。 如果选中显示PDF的自定义权限复选框，则可以从以下选项中进行选择：

**不允许：**&#x200B;不允许用户打印PDF。

**允许：**&#x200B;用户允许打印PDF。

**低分辨率。 仅允许**&#x200B;用户以低分辨率打印PDF。

**修改：**&#x200B;允许用户修改受此策略保护的文档。 对于Office和Pro/E文件，您可以选中“修改”复选框以允许修改，或清除该复选框以防止修改。 如果选中显示PDF的自定义权限复选框，则可以从以下选项中进行选择：

**不允许：**&#x200B;不允许用户修改PDF。

**任何：**&#x200B;用户可以修改PDF。

**协作：**&#x200B;允许用户使用Adobe Acrobat中的“协作”选项与他人协作。 此权限允许用户复制表单数据，即使策略中未明确提供复制权限。

**更改页面：**&#x200B;允许用户在PDF中添加和删除页面以及编辑内容。

**填写并签名：**&#x200B;允许用户在PDF上填写表单字段并签名。

**复制：**&#x200B;允许用户从受此策略保护的文档复制文本。

**屏幕Reader：**&#x200B;如果您选中“显示PDF的自定义权限”复选框，则会显示此权限。 选择此选项时，Adobe Acrobat有权将临时标记添加到PDF，以提高其通过屏幕阅读器可读性。

这些文档权限在“选项”选项卡上提供。 您可以将这些权限应用于PDF、PTC Pro/E和Microsoft Office文件：

**脱机：**&#x200B;允许用户脱机查看受此策略保护的文档。

**权限有效期：**&#x200B;选择权限始终有效或设置文档权限有效期。 如果选择有效期，请单击日历图标以选择日期，并使用箭头指定24小时制的时间。

对于共享策略，管理员可以为文档发布者（将策略应用到文档的用户）禁用以下权限：

**撤销：**&#x200B;允许文档发布者撤销文档访问权限。

**切换：**&#x200B;允许文档发布者切换策略权限。

### 常规设置 {#general-settings}

“常规设置”区域包含以下设置：

**有效期：**&#x200B;授权收件人可以访问受策略保护的文档的时间段。 您可以从以下有效期选项中进行选择：

**文档在以下时间后无效：**&#x200B;自文档受保护后指定天数内可访问该文档。

**文档在此日期之后无效：**&#x200B;文档从策略应用到文档的日期到指定的结束日期有效。

**有效起始日期，有效终止日期：**&#x200B;在指定的日期内，文档有效。 在适用的情况下，您可以使用日历通过单击日历图标来选择日期。

**文档始终有效：**&#x200B;文档有效期未过期。

>[!NOTE]
>
>有效日期基于Document Security系统的时区，而不是基于本地计算机的时区。

**审核：**&#x200B;启用或禁用与受策略保护文档关联的事件的审核。 例如，Document Security可以记录尝试打开文档等事件。 已审计的事件显示在“事件”页面上的列表中。 如果不选择此选项，则Document Security不会记录与策略关联的文档的事件。

>[!NOTE]
>
>管理员还必须在“审核和隐私设置”配置页面上启用服务器审核，才能使审核功能正常工作。

**扩展使用跟踪：**&#x200B;启用或禁用扩展使用跟踪。 Document Security支持跟踪与对PDF文件执行的各种操作相关联的用户事件。 可以使用Java脚本访问Document Security对象。 单击按钮、播放多媒体文件或保存文件是从受策略保护的PDF触发的事件的一些示例。 使用document security对象，您还可以检索用户信息。 可以从全局级别或策略级别的Document Security Server启用事件跟踪。

**自动脱机租赁期：**&#x200B;收件人可以脱机使用受策略保护的文档的最大天数（没有活动的Internet或网络连接）。 租赁期到期后，收件人必须再次同步文档才能继续使用它。

### 外部授权提供程序 {#external-authorization-providers}

选择外部身份验证提供程序（如果已配置任何提供程序）。 列出了可用的提供程序。

### 身份验证设置 {#authentication-settings}

您可以覆盖在服务器上配置的身份验证设置，并指定与此策略相关的身份验证选项。 选择“覆盖全局身份验证设置”，然后选择与此策略相关的身份验证选项。 可以使用以下身份验证选项：

**允许用户名密码身份验证：**&#x200B;如果希望在连接到服务器时允许客户端应用程序使用用户名/密码身份验证，请选择此选项。

**允许Kerberos身份验证：**&#x200B;如果要在连接到服务器时允许客户端应用程序使用Kerberos身份验证，请选择此选项。

**允许客户端证书身份验证：**&#x200B;如果希望在连接到服务器时允许客户端应用程序使用证书身份验证，请选择此选项。

**允许扩展身份验证**&#x200B;选择以启用扩展身份验证。 选择此选项可使客户端应用程序使用扩展身份验证。 扩展身份验证为Document Security服务器上配置的自定义身份验证流程和不同的身份验证选项提供

如果您正在覆盖全局身份验证设置，则可以选择与此策略相关的身份验证选项。 例如，如果在服务器上启用了三个身份验证选项（用户名和密码、客户端证书以及扩展身份验证），则可以覆盖该全局设置并仅为此策略选择扩展身份验证。 确保服务器上已配置您在此处选择的身份验证选项。 在此示例中，您无法选择Kerberos作为身份验证选项，因为它未在服务器上配置。

>[!NOTE]
>
>Apple Mac OS X 11.0.6及更高版本中的Adobe Acrobat支持扩展身份验证。

### 高级设置 {#advanced-settings}

高级设置区域包含以下设置：

**动态水印：**&#x200B;选择要动态显示在文档页面上的水印（例如，当收件人打印文档时）。 动态水印对文档进行唯一标识，有助于确保文档的机密性，防止版权侵犯。 例如，管理员可以配置一个动态水印，以显示当前日期、用户名或文档使用者的标识符。 或者，用于保护文档的策略的名称。 如果进行了配置，水印还可以显示自定义文本或图形元素。 管理员可配置水印选项，管理员和用户可以将其应用于策略。

（请参阅[配置动态水印](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)。）

如果您正在编辑策略，并且管理员删除了您之前为此策略选择的已配置水印，则“编辑策略”页上将显示一条注释。 在这种情况下，如果要保存编辑的文档，请选择新水印（如果要在文档上显示水印）。

>[!NOTE]
>
>对于提供匿名用户访问权限的策略，匿名用户的用户名和标识符不显示为水印，即使您选择此类型的水印也是如此。

**仅对PDF使用认证的Acrobat插件：**&#x200B;如果为策略选择了此选项，则此选项指定在打开受策略保护的文档时，Acrobat 8.0及更高版本必须以认证模式运行。 当Acrobat以认证模式运行时，不会加载任何第三方插件。

如果您担心文档收件人会编写一个插件，该插件可能会绕过Acrobat 8.0及更高版本中的任何文档保护，请选择此选项。 如果您的文档收件人必须使用Acrobat中的第三方插件与文档交互，请勿选择此选项。

此选项仅在Acrobat 8.0或更高版本中启用认证模式；管理员必须禁用Acrobat 7.0的访问权限。

（请参阅[配置Document Security服务器](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)。）

此选项不适用于Adobe Reader。

**访问被拒绝的错误消息：**&#x200B;向未经许可尝试打开受策略保护文档的任何人显示的消息。 此消息会显示在Acrobat中。 无法显示此消息的客户端会显示默认消息，指示访问被拒绝。

### 不可更改的高级设置 {#unchangeable-advanced-settings}

“不可更改高级设置”区域包含以下设置。 保存策略后，无法更改这些设置。

**加密算法和密钥长度：**&#x200B;用于保护您的文档。 您可以从以下选项中进行选择：

* AES 128位
* AES 256位。 只有Acrobat 9.0及更高版本支持此选项。 要对PDF文件使用AES 256加密，请获取并安装Java加密扩展(JCE)无限强度管辖策略文件。 这些文件替换[JAVE_HOME]/lib/security文件夹中的local_policy.jar和US_export_policy.jar文件。 例如，如果您使用的是Sun JDK 1.6，请将下载的文件复制到[dep root]/Java/jdk1.6.0_26/lib/security文件夹。 您可以从[Java SE下载](https://java.sun.com/javase/downloads/index.jsp)下载这些文件。
* 不加密。 Acrobat 9.0及更高版本当前支持此选项。 如果选择此选项，“文档限制”选项将禁用。 如果要使用Document Security进行文档审核或版本控制，但不希望加密文档，则此选项可能很有用。

**文档限制：**&#x200B;选择要加密的PDF文档组件。 其他客户端应用程序加密整个文档，但不加密链接或嵌入的文件。 您可以从以下选项中进行选择：

* 整个文档，包括其附件和元数据。 *元数据*&#x200B;是有关文档及其内容的信息，可通过文档“属性”对话框或Acrobat“高级”菜单查看这些信息。 在Acrobat中，您可以将不同类型的文件（例如，文本、音频和视频文件）附加到PDF文档。
* 文档及其附件，但不包括元数据。
* 仅限文档附件。 您可以加密PDF文件的附件，而无需加密文档内容。

## 启用或禁用共享策略 {#enable-or-disable-shared-policies}

要使共享策略可用，管理员或策略集协调员必须启用它。 您可以启用新策略或以前禁用的策略。 对于受该策略保护的文档，仍将强制实施您禁用的共享策略。

禁用策略旁边将显示一个红色的X。

>[!NOTE]
>
>管理员无法禁用个人策略，用户也无法启用和禁用自己的策略。

1. 在Document Security页面上，单击“策略”，然后单击“策略集”选项卡。
1. 单击相应的策略集名称，然后单击“策略”选项卡。
1. 选中相应策略旁边的复选框，单击“启用”或“禁用”，然后单击“确定”。

## 查看有关策略的信息 {#view-information-about-a-policy}

使用“我的策略”选项卡，您可以搜索个人策略。

管理员创建的策略集列在“策略”页的“策略集”选项卡上。 它们包含有关策略集的信息，包括其名称、创建和修改日期以及说明。 单击策略集名称，以便查看其详细信息。 有权管理策略的策略集协调员可以在特定策略集中创建共享策略。

在创建或编辑策略时，会显示一个页面，您可以在其中配置策略名称、权限级别、机密性设置以及要包含在策略中的收件人。

管理员可以为策略配置以下机密性设置：

* 一般文档机密性选项，如文档有效期和离线租赁期
* 授权用户，以及每个用户的文档限制和权限
* 高级文档机密性选项，包括动态水印和文档加密

用户可以查看他们创建的策略以及他们有权访问的任何共享策略。 管理员可以查看位于Document Security中的所有共享策略和个人策略。

您可以查看有关列表中显示的策略的更多详细信息，包括策略中包含的用户或组以及为这些用户指定的机密性设置。

>[!NOTE]
>
>Acrobat为Microsoft Outlook中附加到电子邮件的文档收件人自动生成的策略不会出现在策略列表中。 您只能通过打开关联文档的文档详情页面来查看这些策略。

1. 在Document Security页面上，单击“策略”，然后单击“我的策略”选项卡。
1. 填写搜索信息，以便可以搜索个人策略。
1. 从列表中选择相应的策略。
1. 在“策略详细资料”页上，您可以查看有关策略的详细资料、编辑策略或查看与策略相关的事件。

## 搜索策略 {#search-for-policies}

管理员可以搜索共享策略以及由其他用户创建的个人策略。

1. 要搜索共享策略，请单击“策略”，然后单击“策略集”选项卡。 单击列表中的策略集，然后单击“策略”选项卡。

   要搜索个人策略，请在Document Security页面上单击“策略”，然后单击“我的策略”选项卡。

1. 在“查找”列表中，选择以下选项之一：

   **策略ID：**&#x200B;用户创建策略时生成的策略标识号。 键入确切的策略ID。

   **策略名称：**&#x200B;策略的名称。 您可以搜索策略名称的一部分或全部。

1. 在文本框中，键入相应的值。 例如，如果您选择了策略名称，请键入要搜索的策略名称。
1. 在“显示”列表中，选择要显示的结果数，然后单击“查找”。 将显示搜索结果。
1. （可选）要查看策略详细信息，请单击策略。

## 复制策略 {#copy-a-policy}

您可以复制现有策略，并使用新的名称和描述进行保存。 复制策略是使用现有设置创建策略的有效方法。

仅当管理员启用此功能时，外部用户才能复制策略。 如果无法创建策略，则复制选项将不可用。

1. 在Document Security页面上，单击“策略”，然后单击“我的策略”选项卡。
1. 从列表中选择相应的策略。
1. 在“策略详细信息”页面上，单击“复制”。
1. 在“New Policy Name（新策略名称）”框中，键入新策略名称。 （可选）键入新的说明。

   名称或描述中不能使用以下字符：

   * 小于号(&lt;)
   * 大于号(>)
   * 与号(&amp;)
   * 单引号(&#39;)
   * 双引号(“)
   * 反斜线(\)
   * 正斜杠(/)

   如果在名称或描述中使用了以下字符，则它们会转换为空格：

   * 回车（ASCII字符13）
   * 换行（ASCII字符10）。

   >[!NOTE]
   >
   >您可以创建包含扩展字符的策略名称；但是，当在两个字符串之间进行比较时，重音和非重音字符（如“e”和“é”）被视为相同。 当有人创建策略时，将进行比较以检查是否存在同名策略。 比较无法区分相同的名称，重音字符除外。 假定策略已添加到数据库，但未添加新策略。

1. 单击“确定”。

## 删除策略 {#delete-a-policy}

您可以删除已创建的策略。 管理员可以删除任何用户创建的策略。 策略集协调员可以删除其策略集中的策略。 对于受该策略保护的文档，仍会强制删除策略。 您可以一次删除多个策略。

只有当管理员启用此功能时，受邀用户才能删除策略。 如果无法删除策略，则删除选项不可用。

1. 在Document Security页面上，单击“策略”。
1. 单击“我的策略”选项卡。
1. 要删除共享策略，请单击“策略集”选项卡，然后单击相应的策略集名称。
1. 选中相应策略旁边的复选框，然后单击“删除”，然后单击“确定”。

>[!NOTE]
>
>使用客户端应用程序从文档中删除策略。 (请参阅Acrobat帮助或相应的Acrobat Reader DC扩展帮助。)

## 对策略列表进行排序 {#sort-the-policy-list}

您可以按列标题对策略列表进行排序，以便更轻松地查找策略。 列标题旁边的三角形图标表示当前使用哪一列进行排序。 向上三角形表示升序，向下三角形表示降序。

1. 在Document Security页面上，单击“策略”，然后单击“策略集”选项卡。
1. 选择一个策略集，然后单击“策略”选项卡。
1. 单击相应的列标题。
1. 要更改排序顺序，请再次单击该列。
