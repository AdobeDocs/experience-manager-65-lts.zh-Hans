---
title: 使用Agent UI准备和发送交互式通信
description: 利用代理UI，代理可以准备交互式通信并将其发送到发布流程。 代理在允许的情况下进行所需的修改，并将交互式通信提交至发布流程，如电子邮件或打印件。
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 2ccd8c75-e4d0-40f9-bc8f-352b408b5c62
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 0%

---

# 使用Agent UI准备和发送交互式通信 {#prepare-and-send-interactive-communication-using-the-agent-ui}

利用代理UI，代理可以准备交互式通信并将其发送到发布流程。 代理在允许的情况下进行所需的修改，并将交互式通信提交至发布流程，如电子邮件或打印件。

## 概述 {#overview}

创建交互式通信后，代理可以在Agent UI中打开交互式通信，并通过输入数据并管理内容和附件来准备特定于收件人的副本。 最后，Agent可以将交互式通信提交到后处理。

在使用代理UI准备交互式通信时，代理在将Agent UI提交到后处理之前管理Agent UI中的交互式通信的以下方面：

* **数据**：代理UI的“数据”选项卡在交互式通信中显示所有可编辑代理的变量和未锁定的表单数据模型属性。 这些变量/属性是在编辑或创建交互式通信中包含的文档片段时创建的。 数据选项卡还包括在XDP/打印渠道模板中构建的任何字段。 仅当交互式通信中有代理可编辑的任何变量、表单数据模型属性或字段时，才会显示“数据”选项卡。
* **内容**：在“内容”选项卡中，代理管理交互式通信中的内容，如文档片段和内容变量。 代理可以在文档片段的属性中创建交互式通信时，在这些文档片段中进行允许的更改。 如果允许，代理还可以重新排序、添加/删除文档片段和添加分页符。
* **附件**：仅当交互式通信具有任何附件或代理具有库访问权限时，“附件”选项卡才会显示在代理UI中。 代理可以或不可以更改或编辑附件。

## 使用代理UI准备交互式通信 {#prepare-interactive-communication-using-the-agent-ui}

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择相应的交互式通信，然后选择&#x200B;**[!UICONTROL 打开代理UI]**。

   >[!NOTE]
   >
   >仅当所选的交互式通信具有打印渠道时，代理UI才有效。

   ![openagentiui](assets/openagentiui.png)

   根据交互式通信的内容和属性，将显示代理UI，其中包含以下三个选项卡：“数据”、“内容”和“附件”。

   ![agentuitabs](assets/agentuitabs.png)

   继续输入数据、管理内容和管理附件。

### 输入数据 {#enter-data}

1. 在数据选项卡中，根据需要输入变量、表单数据模型属性和打印模板(XDP)字段的数据。 填写所有标有星号(&amp;amp；ast；)的必填字段以启用&#x200B;**提交**&#x200B;按钮。

   在交互式通信预览中选择数据字段值，以高亮显示数据选项卡中的相应数据字段，反之亦然。

### 管理内容 {#manage-content}

在“内容”选项卡中，管理交互式通信中的内容，如文档片段和内容变量。

1. 选择&#x200B;**[!UICONTROL 内容]**。 此时将显示交互式通信的内容选项卡。

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. 根据需要在“内容”选项卡中编辑文档片段。 要使焦点位于内容层次结构中的相关片段，您可以在交互式通信预览中选择相关行或段落，或者直接在内容层次结构中选择片段。

   例如，在下图的预览中选择了行为“Make a payment online ... ”（立即在线付款……）的文档片段，并在“Content”（内容）选项卡中选择了相同的文档片段。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   在“内容”或“数据”选项卡中，通过点按预览左上角的“在内容中突出显示选定的模块” (![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以禁用或启用在预览中点按/选择相关文本、段落或数据字段时转到文档片段的功能。

   在创建交互式通信时可由代理编辑的片段具有编辑选定内容(![iconeditselectedcontent](assets/iconeditselectedcontent.png))图标。 选择编辑选定内容图标以在编辑模式下启动片段并在其中进行更改。 使用以下选项设置文本格式并管理文本：

   * [格式化选项](#formattingtext)

      * [从其他应用程序复制粘贴带格式的文本](#pasteformattedtext)
      * [突出显示文本的各个部分](#highlightemphasize)

   * [特殊字符](#specialcharacters)
   * [键盘快捷键](/help/forms/using/keyboard-shortcuts.md)

   有关代理用户界面中各种文档片段可用的操作的详细信息，请参阅[代理用户界面中可用的操作和信息](#actionsagentui)。

1. 要将分页符添加到交互式通信的打印输出中，请将光标放在要插入分页符的位置，并选择之前分页符或之后分页符(![pagebreakbeforeafter](assets/pagebreakbeforeafter.png))。

   在交互式通信中插入显式分页符占位符。 要查看显式分页符对交互式通信的影响，请参阅打印预览。

   ![explicitpagebreak](assets/explicitpagebreak.png)

   继续管理交互式通信的附件。

### 管理附件 {#manage-attachments}

1. 选择&#x200B;**[!UICONTROL 附件]**。 在创建交互式通信时，代理UI将显示设置的可用附件。

   您可以通过点按视图图标来选择不随交互式通信一起提交附件，也可以选择附件中的十字以从交互式通信中删除它（如果允许代理删除或隐藏附件）。 对于创建交互式通信时指定为必填的附件，“查看”和“删除”图标处于禁用状态。

   ![附件sagentui](assets/attachmentsagentui.png)

1. 选择库访问权限(![libraryaccess](assets/libraryaccess.png))图标可访问内容库，以将DAM资产作为附件插入。

   >[!NOTE]
   >
   >只有在创建交互式通信时启用了库访问（在打印渠道的“文档容器”属性中），库访问图标才可用。

1. 如果在创建交互式通信时未锁定附件的顺序，则可以通过选择附件并点按向下和向上箭头来重新排序附件。
1. 使用Web预览和打印预览功能，查看这两个输出是否符合您的要求。

   如果您认为预览效果令人满意，请选择&#x200B;**[!UICONTROL 提交]**&#x200B;以提交/将交互式通信发送到发布进程。 或者，要进行更改，请退出预览以返回到进行更改的页面。

## 设置文本格式 {#formattingtext}

在代理UI中编辑文本片段时，工具栏会根据您选择的编辑类型而发生更改：字体、段落或列表：

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) ![字体工具栏](do-not-localize/fonttoolbar.png)

字体工具栏

![段落工具栏](do-not-localize/paragraphtoolbar.png)

段落工具栏

![列表工具栏](do-not-localize/listtoolbar.png)

列表工具栏

### 突出显示/强调文本部分 {#highlightemphasize}

要高亮显示\强调可编辑片段中的文本部分，请选择该文本，然后选择“高亮显示颜色”。

![highlighttextagentui](assets/highlighttextagentui.png)

### 粘贴格式化文本 {#pasteformattedtext}

![粘贴文本](assets/pastedtext.png)

### 在文本中插入特殊字符 {#specialcharacters}

代理UI已内置对210个特殊字符的支持。 管理员可以[通过自定义](/help/forms/using/custom-special-characters.md)添加对更多/自定义特殊字符的支持。

#### 附件投放 {#attachmentdelivery}

* 使用服务器端API作为交互式或非交互式PDF呈现交互式通信时，呈现的PDF包含附件作为PDF附件。
* 在使用代理UI提交过程中加载与交互式通信关联的后处理时，附件将作为List&lt;com.adobe.idp.Document> inAttachmentDocs参数传递。
* 投放机制工作流（如电子邮件和打印）也随交互式通信的PDF版本一起投放附件。

## 代理用户界面中可用的操作和信息 {#actionsagentui}

### 文档片段 {#document-fragments}

![ ](do-not-localize/contentoptionsdocfragments.png)

* **向上/向下箭头**：用于在交互式通信中向上或向下移动文档片段的箭头。
* **删除**：如果允许，请从交互式通信中删除文档片段。
* **在**&#x200B;前插入分页符（适用于目标区域的子片段）：在文档片段前插入分页符。
* **缩进**：增加或减少文档片段的缩进。
* **在**&#x200B;后面插入分页符（适用于目标区域的子片段）：在文档片段后面插入分页符。

![docfragoptions](assets/docfragoptions.png)

* 编辑（仅限文本片段）：打开富文本编辑器以编辑文本文档片段。 有关详细信息，请参阅[设置文本格式](#formattingtext)。

* 选择（眼睛图标）：包含\排除交互式通信中的文档片段。
* 未填写的值（信息）：指示文档片段中未填写的变量的数量。

### 列出文档片段 {#list-document-fragments}

![列表选项](assets/listoptions.png)

* 插入空白行：插入新的空白行。
* 选择（眼睛图标）：包含\排除交互式通信中的文档片段。
* 跳过项目符号/编号：如果要跳过列表文档片段中的项目符号/编号，请启用此选项。
* 未填写的值（信息）：指示文档片段中未填写的变量的数量。

## 将交互式通信另存为草稿 {#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，并稍后检索草稿以继续处理。 您可以为每个草稿指定不同的名称来标识它。

Adobe建议按顺序执行这些指令，以成功地将交互式通信另存为草稿。

### 启用另存为草稿功能 {#before-save-as-draft}

缺省情况下，“另存为草稿”功能未启用。 执行以下步骤以启用该功能：

1. 实施[ccrDocumentInstance](https://helpx.adobe.com/cn/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html)服务提供程序接口(SPI)。

   SPI允许您使用草稿ID作为唯一标识符将交互式通信的草稿版本保存到数据库中。 这些说明假定您事先知道如何使用Maven项目构建OSGi捆绑包。

   有关示例SPI实现，请参阅[示例ccrDocumentInstance SPI实现](#sample-ccrDocumentInstance-spi)。
1. 打开`http://<hostname>:<port>/ system/console/bundles`并选择&#x200B;**[!UICONTROL 安装/更新]**&#x200B;以上传OSGi包。 验证上传的包的状态是否显示为&#x200B;**活动**。 如果包的状态未显示为&#x200B;**活动**，请重新启动服务器。
1. 转到 `https://'[server]:[port]'/system/console/configMgr`.
1. 选择&#x200B;**[!UICONTROL 创建通信配置]**。
1. 选择&#x200B;**[!UICONTROL 使用CCRDocumentInstanceService启用“保存”]**，然后选择&#x200B;**[!UICONTROL 保存]**。

### 将交互式通信另存为草稿 {#save-as-draft-agent-ui}

执行以下步骤，将交互式通信另存为草稿：

1. 在Forms Manager中选择交互式通信，然后选择&#x200B;**[!UICONTROL 打开代理UI]**。

1. 在代理UI中进行适当的更改，然后选择&#x200B;**[!UICONTROL 另存为草稿]**。

1. 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中指定草稿的名称，然后选择&#x200B;**[!UICONTROL 完成]**。

将交互式通信另存为草稿后，选择&#x200B;**[!UICONTROL 保存更改]**&#x200B;以保存对草稿所做的任何进一步更改。

### 检索交互式通信的草稿 {#retrieve-draft}

将交互式通信另存为草稿后，您可以检索它以继续对其进行处理。 使用以下方式检索交互式通信：

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid]引用将交互式通信另存为草稿后生成的草稿版本的唯一标识符。

### ccrDocumentInstance SPI实施示例 {#sample-ccrDocumentInstance-spi}

实施`ccrDocumentInstance` SPI以将交互式通信另存为草稿。 以下是`ccrDocumentInstance` SPI的实现示例。

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

`save`、`update`、`get`和`getAll`操作调用数据库服务以将交互式通信另存为草稿、更新交互式通信、从数据库中检索数据以及检索数据库中可用的所有交互式通信的数据。 此示例使用`mySQLDataBaseServiceCRUD`作为数据库服务的名称。

下表说明了`ccrDocumentInstance` SPI实现的示例。 它演示了在示例实现中，`save`、`update`、`get`和`getAll`操作如何调用数据库服务。

<table> 
 <tbody>
 <tr>
  <td><p><strong>操作</strong></p></td>
  <td><p><strong>数据库服务示例</strong></p></td> 
   </tr>
  <tr>
   <td><p>您可以为交互式通信创建草稿，也可以直接提交草稿。 保存操作的API检查交互式通信是否作为草稿提交，并且包括草稿名称。 然后，API使用Save作为输入方法调用mySQLDataBaseServiceCRUD服务。</p></br><img src="assets/save-as-draft-save-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服务验证Save作为输入方法，并生成自动生成的草稿ID并将其返回给AEM。 生成草稿ID的逻辑可能会因数据库而异。</p></br><img src="assets/save-operation-service.png"/></td>
   </tr>
  <tr>
   <td><p>更新操作的API可检索交互式通信草稿的状态，并检查交互式通信是否包含草稿名称。 API调用mySQLDataBaseServiceCRUD服务来更新数据库中的该状态。</p></br><img src="assets/save-as-draft-update-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服务验证Update作为输入方法，并在数据库中保存交互式通信草稿的状态。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>获取操作的API检查交互式通信是否包含草稿ID。 然后，API使用Get作为输入方法调用mySQLDataBaseServiceCRUD服务，以检索交互式通信的数据。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服务验证Get作为输入方法，并根据草稿ID检索交互式通信的数据。</p></br><img src="assets/get-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>getAll操作的API调用mySQLGetALLData服务以检索数据库中保存的所有交互式通信的数据。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLData服务检索数据库中保存的所有Interactive Communications的数据。</p></br><img src="assets/getall-operation-service.png"/></td>
   </tr>
  </tbody>
</table>

以下是作为实施一部分的`pom.xml`文件示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
         xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>确保在`pom.xml`文件中将`aemfd-client-sdk`依赖项更新为6.0.160。
