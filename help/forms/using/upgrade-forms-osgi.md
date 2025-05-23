---
title: 在OSGi上升级到AEM 6.5 Forms LTS
description: 您可以从AEM 6.5.22.0 Forms直接升级到AEM 6.5 Forms LTS。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: dd45dfe953a111ccbbc71e8e25a8a2577037587a
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# 在OSGi上升级到AEM 6.5 Forms LTS {#upgrade-to-aem-forms-osgi}

要[从AEM 6.5升级到AEM 6.5 LTS](/help/sites-deploying/upgrade.md)，请升级到AEM 6.5.22.0 Forms或更高版本。 支持从AEM 6.5.22.0直接升级到AEM 6.5 Forms LTS。

如果您使用的是AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 Forms或AEM 6.5 Forms，则无法直接升级到AEM 6.5 Forms LTS。 有关详细升级路径，请参阅[升级路径](/help/forms/using/upgrade.md)文档。

升级到Service Pack AEM Forms 6.5.22.0后，请按照以下步骤升级到AEM 6.5 LTS Forms：

1. 安装AEM Forms附加组件包。 以下列出了这些步骤：

   1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
   1. 选择标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 筛选器]**&#x200B;部分中：
      1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
      1. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
   1. 选择适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后选择&#x200B;**[!UICONTROL 下载]**。
   1. 打开[包管理器](/help/sites-administering/package-manager.md)，然后单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
   1. 选择包并单击&#x200B;**[!UICONTROL 安装]**。

      您还可以使用[AEM Forms发行版](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)文章中列出的直接链接下载包。

      安装包后，系统会提示您重新启动AEM实例。 **不立即停止服务器。**&#x200B;在停止AEM Forms服务器之前，请等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出现在&lt;crx-repository>/error.log文件中，并且日志稳定。 另请注意，一些软件包可以保持已安装状态。 您可以安全地忽略这些软件包的状态。


      **使用以下其他JVM命令行参数重新启动AEM实例**：
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      如果服务器是通过脚本或服务启动的，请相应地更新以包含上述内容，以便在后续重新启动后生效。

      >[!NOTE]
      >
      > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。

1. 执行安装后活动。

   * **运行迁移实用程序**

     迁移实用程序使自适应表单和以前版本的通信管理资产与AEM 6.5表单兼容。 您可以从AEM Software Distribution下载该实用程序。 有关配置和使用迁移实用程序的逐步信息，请参阅[迁移实用程序](../../forms/using/migration-utility.md)。

     如果您使用[示例将草稿和提交组件](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)与数据库集成并从以前的版本升级，请在执行升级后运行以下SQL查询：

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置Adobe Sign**

     如果您在早期版本的AEM Forms中配置了Adobe Sign，则从AEM Cloud Service重新配置Adobe Sign。 有关详细信息，请参阅[将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支持jQuery**

     在AEM 6.5 Forms中，jQuery的版本更新为3.2.1，jQuery UI的版本更新为1.12.1。AEM表单在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用的是任何其他jQuery版本，则在执行升级时不会显示任何问题。 但是，当您升级到AEM 6.5 Forms时：

      * 确保您的自定义组件（如果有）与支持的jQuery版本兼容。
      * 从自定义组件中删除不支持的API。 请参阅[升级指南](https://jquery.com/upgrade-guide/3.0/)以获取已删除的API列表。 例如，删除了对load()、.unload()和.error() API的支持。 使用.on()方法替换前面提到的API。 例如，将$(&quot;img&quot;)。load(fn)更改为$(&quot;img&quot;)。on(&quot;load&quot;， fn)。

   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置分析和报表**

     在AEM 6.4 Forms中，源的流量变量和印象的成功事件不可用。 因此，当您从AEM 6.2 Forms或之前的版本升级时，AEM Forms会停止向Adobe Analytics服务器发送数据，并且自适应表单的Analytics报表将不可用。 此外，AEM 6.4 Forms还为Form Analytics版本引入了流量变量，并为字段逗留时间引入了成功事件。 因此，请为您的AEM Forms环境重新配置分析和报表。 有关详细步骤，请参阅[配置分析和报表](../../forms/using/configure-analytics-forms-documents.md)。

1. 验证服务器是否升级成功，所有数据是否也迁移成功，服务器是否能够正常运行。

   * **验证捆绑的状态：**&#x200B;确保所有捆绑都处于活动状态。
   * **验证复制和反向复制：**&#x200B;发布、填写并提交一些迁移的表单。 同时验证提交的数据。
   * **验证对管理员和开发人员用户界面的访问权限：**&#x200B;从管理员帐户登录AEM实例，并验证您有权访问以下URL：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >在AEM 6.4 Forms中，crx-repository的结构发生了更改。 如果从6.3 Forms升级到AEM 6.5 Forms，请使用更改后的路径来重新创建自定义。 有关已更改路径的完整列表，请参阅[AEM中的Forms存储库重组](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)。
