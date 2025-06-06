---
title: 包管理器
description: 了解使用包管理器进行AEM包管理的基础知识。
feature: Administering
role: Admin
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
exl-id: 6c0238ca-568e-4a46-a3cc-0b08a10cf324
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '3568'
ht-degree: 1%

---

# 包管理器 {#working-with-packages}

利用资源包，可以导入和导出存储库内容。 您可以使用包安装新内容、安装新功能、在实例之间传输内容以及备份存储库内容。

使用包管理器，您可以在AEM实例和本地文件系统之间传输包以进行开发。

## 什么是包？ {#what-are-packages}

包是一个zip文件，以文件系统序列化形式保存存储库内容，称为保险库序列化，它提供了易于使用和易于编辑的文件和文件夹表示形式。 包中包含的内容是使用过滤器定义的。

软件包还包含电子仓库元信息，包括过滤器定义和导入配置信息。 包中可以包含不用于包提取的其他内容属性，例如描述、可视化图像或图标。 这些附加内容属性仅供内容包使用者使用和参考。

>[!NOTE]
>
>包表示生成包时内容的当前版本。 它们不包括AEM保留在存储库中的任何先前版本的内容。

## 包管理器 {#package-manager}

包管理器会管理AEM安装中的包。 在您[分配了必要的权限](#permissions-needed-for-using-the-package-manager)之后，您可以使用包管理器执行各种操作，包括配置、生成、下载和安装包。

### 所需权限 {#required-permissions}

要创建、修改、上载和安装包，用户必须在以下节点上拥有适当的权限：

* 完全权限（不包括`/etc/packages`上的删除）
* 包含包内容的节点

>[!CAUTION]
>
>授予包的权限可能会导致敏感信息泄露和数据丢失。
>
>为了限制这些风险，强烈建议仅向专用子树授予特定组权限。

### 访问包管理器 {#accessing}

您可以通过三种方式访问包管理器：

1. 从AEM主菜单> **工具** > **部署** > **包**
1. 从[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)（使用顶部切换栏）
1. 直接访问`http://<host>:<port>/crx/packmgr/`

### 包管理器UI {#ui}

Package Manager分为四个主要功能区域：

* **左侧导航面板** — 此面板允许您对包列表进行筛选和排序。
* **包列表** — 这是实例上的包列表，按照左侧导航面板中的选择进行筛选和排序。
* **活动日志** — 此面板最初最小化，并展开以详细说明包管理器的活动，如生成或安装包时。 在“活动日志”选项卡中，还有其它按钮用于：
   * **清除日志**
   * **显示/隐藏**
* **工具栏** — 工具栏包含用于左侧导航面板和包列表的刷新按钮以及用于搜索、创建和上传包的按钮。

![包管理器UI](assets/package-manager-ui.png)

单击左侧导航面板中的选项会立即过滤包列表。

单击包名称可展开“包列表”中的条目以显示有关包的更多详细信息。

![扩展的包详细信息](assets/package-expand.png)

展开包详细信息时，可通过工具栏按钮对包执行许多操作。

* [编辑](#edit-package)
* [生成](#building-a-package)
* [重新安装](#reinstalling-packages)
* [下载](#downloading-packages-to-your-file-system)
* [共享](#share)

**更多**&#x200B;按钮下提供了其他操作。

* [删除](#deleting-packages)
* [范围](#package-coverage)
* [个内容](#viewing-package-contents-and-testing-installation)
* [重新包装](#rewrapping-a-package)
* [其他版本](#other-versions)
* [卸载](#uninstalling-packages)
* [测试安装](#viewing-package-contents-and-testing-installation)
* [验证](#validating-packages)
* [复制](#replicating-packages)

### 包状态 {#package-status}

包列表中的每个条目都有一个状态指示器，用于让您一眼就知道包的状态。 将鼠标悬停在状态上会显示工具提示，其中包含状态的详细信息。

![包状态](assets/package-status.png)

如果包已更改或从未生成，则状态将显示为链接，以便执行快速操作以重新生成或安装包。

## 包设置 {#package-settings}

资源包本质上是一组过滤器，以及基于这些过滤器的存储库数据。 使用包管理器UI，您可以单击包，然后单击&#x200B;**编辑**&#x200B;按钮以查看包的详细信息，包括以下设置。

* [常规设置](#general-settings)
* [包过滤器](#package-filters)
* [程序包依赖项](#package-dependencies)
* [高级设置](#advanced-settings)
* [程序包屏幕截图](#package-screenshots)

### 常规设置 {#general-settings}

您可以编辑各种包设置以定义包说明、依赖性和提供程序详细信息等信息。

在[创建](#creating-a-new-package)或[编辑](#viewing-and-editing-package-information)包时，**包设置**&#x200B;对话框可通过&#x200B;**编辑**&#x200B;按钮使用。 进行任何更改后，单击&#x200B;**保存**。

![编辑包对话框，常规设置](assets/general-settings.png)

| 字段 | 描述 |
|---|---|
| 名称 | 程序包的名称 |
| 组 | 要组织包，可以键入新组的名称或选择现有组 |
| 版本 | 用于版本的文本 |
| 描述 | 允许使用HTML标记进行格式化的包的简短描述 |
| 缩略图 | 与包列表一起显示的图标 |

#### 包缩略图 {#thumbnails}

缩略图提供了包中所包含内容的快速引用可视化表示形式。 然后，它显示在包列表中，可以帮助轻松识别包或包的类。

以下是用于正式包的惯例示例：

官方修补程序

![官方修补程序缩略图](assets/official-hotfix.png)

AEM正式安装扩展

![正式AEM安装或扩展缩略图](assets/official-installation.png)

Official Service Pack

![Official AEM Service Pack图标](assets/official-service-pack.png)

为您的包使用唯一图标。 请勿重用Adobe使用的图标。

### 包过滤器 {#package-filters}

过滤器标识要包含在包中的存储库节点。 **筛选器定义**&#x200B;指定了以下信息：

* 要包含的内容的&#x200B;**根路径**
* 在根路径下包含或排除特定节点的&#x200B;**规则**

使用&#x200B;**+**&#x200B;按钮添加规则。 使用&#x200B;**-**&#x200B;按钮删除规则。

规则是根据其顺序应用的，因此请使用&#x200B;**向上**&#x200B;和&#x200B;**向下**&#x200B;箭头按钮根据需要进行定位。

过滤器可以包含零个或多个规则。 未定义规则时，包将包含根路径下的所有内容。

您可以为包定义一个或多个筛选器定义。 使用多个筛选器以包含来自多个根路径的内容。

![筛选器选项卡](assets/edit-filter.png)

创建规则时，您可以定义正则表达式（也称为正则表达式、正则表达式或正则表达式），以指定要包含或排除的所有节点。

| 规则类型 | 描述 |
|---|---|
| include | Include将包括指定目录中与正则表达式匹配的所有文件和文件夹。 Include **将不会**&#x200B;包含指定根路径下的其他文件或文件夹。 |
| 排除 | 排除将排除与正则表达式匹配的所有文件和文件夹。 |

最常在首次[创建包时定义包筛选器。](#creating-a-new-package)但是，以后也可以编辑它们，此后应重新构建包以根据新的筛选器定义更新其内容。

>[!TIP]
>
>一个包可以包含多个过滤器定义，以便来自不同位置的节点可以轻松组合到一个包中。

>[!TIP]
>
>有关后台信息，请参阅[Apache Jackrabbit - Workspace Filter](https://jackrabbit.apache.org/filevault/filter.html)文档。

### 依赖项 {#dependencies}

![依赖关系选项卡](assets/dependencies.png)

| 字段 | 描述 | 示例/详细信息 |
|---|---|---|
| 测试方式 | 此包针对或与之兼容的产品名称和版本。 | `6.5` |
| 修复的问题 | 一个文本字段，用于列出此包中修复的错误的详细信息，每行一个错误 | - |
| 依赖于 | 列出安装时所需的其他包，以便当前包按预期运行 | `groupId:name:version` |
| 替换 | 此包替换的已弃用包的列表 | `groupId:name:version` |

### 高级设置 {#advanced-settings}

![高级设置选项卡](assets/advanced-settings.png)

| 字段 | 描述 | 示例/详细信息 |
|---|---|---|
| 名称 | 程序包提供程序的名称 | `WKND Media Group` |
| URL | 提供商URL | `https://wknd.site` |
| 链接 | 到提供程序页的特定于包的链接 | `https://wknd.site/package/` |
| 需要 | 定义安装包时是否存在任何限制 | **管理员** — 必须以管理员权限安装包&#x200B;<br>**重新启动** — 安装包后必须重新启动AEM |
| AC 处理 | 指定在导入包时如何处理包中定义的访问控制信息 | **忽略** — 保留存储库中的ACL <br>**覆盖** — 覆盖存储库中的ACL <br>**合并** — 合并这两组ACL <br>**合并保留** — 将内容中的访问控制项与随包一起提供的访问控制项合并，方法是添加内容中不存在的主体的访问控制项&#x200B;<br>**清除** — 清除ACL |

### 程序包屏幕截图 {#package-screenshots}

您可以将多个屏幕截图附加到包中，以提供内容显示方式的可视表示形式。

![屏幕截图选项卡](assets/screenshots.png)

## 包操作 {#package-actions}

可以对包执行许多操作。

### 创建资源包 {#creating-a-new-package}

1. [访问包管理器。](#accessing)

1. 单击&#x200B;**创建包**。

   >[!TIP]
   >
   >如果您的实例具有许多包，则可能已有文件夹结构。 在这种情况下，创建新包之前可以更轻松地导航到所需的目标文件夹。

1. 在&#x200B;**新建包**&#x200B;对话框中，输入以下字段：

   ![新包对话框](assets/new-package-dialog.png)

   * **包名称** — 选择一个描述性名称，以帮助您（和其他人）轻松识别包的内容。

   * **版本** — 这是一个文本字段，用于指示版本。 这会附加到包名称以形成zip文件的名称。

   * **组** — 这是目标组（或文件夹）名称。 组可帮助您组织包。 如果该组尚不存在，则会为其创建文件夹。 如果将组名称留空，它将在主包列表中创建包。

1. 单击&#x200B;**确定**&#x200B;以创建包。

1. AEM在包列表的顶部列出新包。

   ![新包](assets/new-package.png)

1. 单击&#x200B;**编辑**&#x200B;以定义[包内容。完成编辑设置后，](#package-contents)单击&#x200B;**保存**。

1. 您现在可以[生成](#building-a-package)您的包。

创建包后不必立即构建包。 未构建的包不包含任何内容，并且仅由包的过滤器数据和其他元数据组成。

### 构建资源包 {#building-a-package}

通常在[创建包](#creating-a-new-package)的同时生成包，但可在以后返回生成或重建包。 如果存储库中的内容已更改或包过滤器已更改，此功能会很有用。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击&#x200B;**生成**。 此时会出现一个对话框，要求您确认是否确实要生成包，因为任何现有的包内容都将被覆盖。

1. 单击&#x200B;**确定**。 AEM会生成资源包，并在活动列表中列出添加到资源包的所有内容。 完成后，AEM会显示一条确认消息，确认软件包已生成，（当您关闭对话框时）会更新软件包列表信息。

### 编辑资源包 {#edit-package}

将包上传到AEM后，您可以修改其设置。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击&#x200B;**编辑**&#x200B;并根据需要更新&#x200B;**[包设置](#package-settings)**。

1. 单击&#x200B;**保存**&#x200B;以进行保存。

您可能需要[重新生成包](#building-a-package)以根据您所做的更改更新其内容。

### 重新包装包 {#rewrapping-a-package}

生成包后，可以对其进行重新包装。 重新包装会更改包信息，但不更改包内容，如缩略图、描述等。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击&#x200B;**编辑**&#x200B;并根据需要更新&#x200B;**[包设置](#package-settings)**。

1. 单击&#x200B;**保存**&#x200B;以进行保存。

1. 单击&#x200B;**更多** > **重新包装**，此时将出现对话框要求确认。

### 查看其他包版本 {#other-versions}

由于包的每个版本都作为任何其他包出现在列表中，因此包管理器可以找到选定包的其他版本。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击&#x200B;**更多** > **其他版本**，将打开一个对话框，其中包含同一包的其他版本的列表以及状态信息。

### 查看包内容和测试安装 {#viewing-package-contents-and-testing-installation}

生成包后，可以查看其内容。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 要查看内容，请单击&#x200B;**更多** > **内容**，包管理器将在活动日志中列出包的全部内容。

   ![包内容](assets/package-contents.png)

1. 要试用安装，请单击&#x200B;**更多** > **测试安装**，包管理器将在活动日志中报告结果，就像已执行安装一样。

   ![测试安装](assets/test-install.png)

### 正在将包下载到您的文件系统 {#downloading-packages-to-your-file-system}

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击包详细信息区域中的&#x200B;**下载**&#x200B;按钮或包的链接文件名。

1. AEM会将包下载到您的计算机。

### 共享包 {#share}

包共享是一种用于分发内容包的集中式公共服务。 包共享已被[软件分发](#software-distribution)取代，并且此按钮不再有效。

### 从您的文件系统上传包 {#uploading-packages-from-your-file-system}

1. [访问包管理器。](#accessing)

1. 选择要将包上载到其中的组文件夹。

1. 单击&#x200B;**上传包**&#x200B;按钮。

1. 提供有关已上传文件包的必需信息。

   ![包上载对话框](assets/package-upload-dialog.png)

   * **包** — 使用&#x200B;**浏览……**&#x200B;按钮从本地文件系统中选择所需的包。
   * **强制上传** — 如果已存在具有此名称的包，则此选项将强制上传并覆盖现有包。

1. 单击&#x200B;**确定**&#x200B;将上载选定的包并相应地更新包列表。

包内容现在存在于AEM上，但若要使该内容可供使用，请确保[安装包](#installing-packages)。

### 验证包 {#validating-packages}

由于包可以修改现有内容，因此在安装之前验证这些更改通常很有用。

#### 验证选项 {#validation-options}

包管理器可以执行以下验证：

* [OSGi包导入](#osgi-package-imports)
* [叠加](#overlays)
* [ACL](#acls)

##### 验证 OSGi 包的导入情况 {#osgi-package-imports}

**检查的内容**

此验证检查所有JAR文件（OSGi包）的包，提取其`manifest.xml`（包含所述OSGi包所依赖的版本依赖项），并验证AEM实例是否以正确的版本导出所述依赖项。

**报告方式**

任何无法由AEM实例满足的版本化依赖项都会在包管理器的活动日志中列出。

**错误状态**

如果不满足依赖关系，则包中具有这些依赖关系的OSGi捆绑包将不会启动。 这会导致应用程序部署中断，因为依赖未启动的OSGi捆绑包的任何内容都将无法正常运行。

**错误解决**

要解决因未满足的OSGi捆绑包导致的错误，必须调整包含未满足的导入的捆绑包中的依赖项版本。

##### 验证覆盖 {#overlays}

**检查的内容**

此验证可确定正在安装的包是否包含目标AEM实例中已覆盖的文件。

例如，假定在`/apps/sling/servlet/errorhandler/404.jsp`处有一个现有的叠加，包中包含`/libs/sling/servlet/errorhandler/404.jsp`，这样它将更改`/libs/sling/servlet/errorhandler/404.jsp`处的现有文件。

**报告方式**

包管理器的活动日志中介绍了任何此类叠加。

**错误状态**

错误状态表示包尝试部署的文件已覆盖，因此包中的更改将被覆盖覆盖（因此“隐藏”），并且不会生效。

**错误解决**

要解决此问题，`/apps`中叠加文件的维护者必须审核对`/libs`中叠加文件的更改，并将所需的更改合并到叠加(`/apps`)中，然后重新部署叠加文件。

>[!NOTE]
>
>如果叠加的内容已正确并入叠加文件，则验证机制无法协调。 因此，即使进行了必要的更改，此验证仍将继续报告冲突。

##### 验证 ACL {#acls}

**检查的内容**

此验证会检查正在添加的权限、如何处理这些权限（合并/替换），以及当前权限是否会受到影响。

**报告方式**

包管理器的活动日志中介绍了相关权限。

**错误状态**

不能提供显式错误。 验证仅指示安装包是否会添加任何新ACL权限或是否会影响这些权限。

**错误解决**

使用验证提供的信息，可以在CRXDE中查看受影响的节点，并根据需要在包中调整ACL。

>[!CAUTION]
>
>作为最佳实践，建议软件包不要影响AEM提供的ACL，因为这样可能会导致意外行为。

#### 正在执行验证 {#performing-validation}

可以通过两种不同的方式验证包：

* [通过包管理器UI](#via-package-manager)
* [通过HTTP POST请求，例如使用cURL](#via-post-request)

在上传包后但在安装包之前应始终进行验证。

##### 通过包管理器验证包 {#via-package-manager}

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 要验证包，请单击&#x200B;**更多** > **验证**，

1. 在随后显示的模式对话框中，使用复选框选择验证类型，并通过单击&#x200B;**验证**&#x200B;开始验证。

1. 然后，所选验证将运行，结果将显示在包管理器的活动日志中。

##### 通过HTTP POST请求验证包 {#via-post-request}

POST请求采用以下形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

`type`参数可以是任何逗号分隔的无顺序列表，包括：

* `osgiPackageImports`
* `overlays`
* `acls`

如果未显式传递，`type`的值默认为`osgiPackageImports`。

使用cURL时，请执行与以下内容类似的语句：

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

在通过POST请求进行验证时，响应将作为JSON对象发送回。

### 查看程序包覆盖范围 {#package-coverage}

包由其过滤器定义。 您可以让包管理器将包的过滤器应用于现有存储库内容，以显示包的过滤器定义涵盖的存储库的内容。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开包详细信息。

1. 单击&#x200B;**更多** > **覆盖范围**。

1. 服务范围详细信息列在活动日志中。

### 安装包 {#installing-packages}

上传资源包只会将该资源包内容添加到存储库，但不可访问。 安装上传的包，以使用包的内容。

>[!CAUTION]
>
>安装包可能会覆盖或删除现有内容。 仅当您确保包不会删除或覆盖您需要的内容时，才上载包。

在安装包之前，包管理器会自动创建包含将被覆盖的内容的快照包。 如果您卸载包，将重新安装此快照。

>[!CAUTION]
>
>* 如果要安装数字资产，您必须：
>  首先，取消激活WorkflowLauncher。
>  使用OSGi控制台的“组件”菜单选项取消激活
>  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* 接下来，安装完成后，重新激活WorkflowLauncher。
>
>停用WorkflowLauncher可确保Assets导入程序框架在安装时不会（无意中）处理资源。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开要安装的包的包详细信息。

1. 单击项目详细信息中的&#x200B;**Install**&#x200B;按钮或包状态中的&#x200B;**Install**&#x200B;链接。

1. 对话框将请求确认，并允许指定其他选项。

   * **仅提取** — 仅提取包以便不创建快照，因此将无法卸载
   * **保存阈值** — 触发自动保存之前的临时节点数（如果遇到并发修改异常，则增加）
   * **提取子包** — 启用自动提取子包
   * **访问控制处理** — 指定安装包时如何处理包中定义的访问控制信息（选项与[高级包设置](#advanced-settings)相同）
   * **依赖关系处理** — 指定依赖关系在安装期间如何处理

1. 单击&#x200B;**安装**。

1. 活动日志详细说明了安装进度。

安装完成并成功后，将更新包列表，并在包状态中显示&#x200B;**Installed**。

### 重新安装包 {#reinstalling-packages}

重新安装软件包对[初始安装软件包时处理的已安装软件包执行相同的步骤。](#installing-packages)

### 基于文件系统的上载和安装 {#file-system-based-upload-and-installation}

安装包时，您可以完全放弃包管理器。 AEM可以检测放置在主机本地文件系统上特定位置的软件包，并自动上传和安装它们。

1. 在AEM安装文件夹下，jar和`license.properties`文件旁边有一个`crx-quicksart`文件夹。 在`crx-quickstart`下创建名为`install`的文件夹，生成路径`<aem-home>/crx-quickstart/install`。

1. 在此文件夹中，添加您的包。 它们将自动上传并安装到您的实例上。

1. 上载和安装完成后，您可以在包管理器中查看包，就像使用包管理器UI安装包一样。

如果实例正在运行，则在将其添加到包到`install`文件夹中时，将立即开始上载和安装

如果实例未运行，则按字母顺序在启动时安装放置在`install`文件夹中的包。

### 卸载包 {#uninstalling-packages}

卸载软件包会将存储库的内容还原为软件包管理器在安装之前自动生成的快照。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开要卸载的包的包详细信息。

1. 单击&#x200B;**更多** > **卸载**，从存储库中删除此包的内容。

1. 此时将显示一个对话框，请求确认并列出所做的所有更改。

1. 将删除包并应用快照。 该流程的进度将显示在活动日志中。

### 删除包 {#deleting-packages}

删除包只会从包管理器中删除其详细信息。 如果已经安装了此包，则不会删除安装的内容。

1. [访问包管理器。](#accessing)

1. 单击包名称，打开要从包列表中删除的包的包详细信息。

1. 包管理器会要求您确认是否要删除包。 单击&#x200B;**确定**&#x200B;以确认删除。

1. 资源包信息将被删除，详细信息将会在活动日志中报告。

### 复制资源包 {#replicating-packages}

复制包的内容以将其安装在发布实例上。

1. [访问包管理器。](#accessing)

1. 单击包名称，从包列表中打开要复制的包的包详细信息。

1. 单击&#x200B;**更多** > **复制**。

1. 将复制资源包，并在活动日志中报告详细信息。

## Software Distribution {#software-distribution}

AEM包可用于在AEM环境中创建和共享内容。

[Software Distribution](https://downloads.experiencecloud.adobe.com)是一项集中式服务，旨在简化AEM包的搜索和下载。

有关详细信息，请参阅[软件分发文档。](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=zh-Hans)

>[!NOTE]
>
>Package Manager当前未与Software Distribution集成，因为它与之前的Package Share服务集成。 因此，包管理器中的共享按钮以及指向包共享的其他链接不再有效。 解决方案是将包下载到本地磁盘。
