---
title: 工作流步骤参考
description: 有关Adobe Experience Manager中的工作流，请参阅此步骤参考。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: e82d97c2-c26a-48df-9210-47dc017c68c8
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '3226'
ht-degree: 2%

---

# 工作流步骤参考 {#workflow-step-reference}

工作流模型由一系列各种类型的步骤组成。 根据类型，可以使用参数和脚本配置并扩展这些步骤，以提供所需的功能和控制。

>[!NOTE]
>
>本节介绍标准工作流步骤。
>
>有关特定于模块的步骤，请参阅以下内容：
>
>* [AEM Forms工作流步骤参考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒体处理程序和工作流处理Assets](/help/assets/media-handlers.md)
>

## 步骤属性 {#step-properties}

每个步骤组件都有一个&#x200B;**步骤属性**&#x200B;对话框，允许您定义和编辑所需的属性。

### 步骤属性 — 常用选项卡 {#step-properties-common-tab}

在属性对话框的&#x200B;**常用**&#x200B;选项卡上，以下属性的组合可用于大多数工作流步骤组件：

* **标题**
步骤的标题。

* **描述**
步骤的描述。

* **工作流阶段**

  用于将[阶段](/help/sites-developing/workflows.md#workflow-stages)应用于步骤的下拉选择器。

* **超时**

  步骤“超时”之前的一段时间。
您可以选择： **关闭**、**立即**、**1h**、**6h**、**12h**、**24h**。

* **超时处理程序**

  步骤超时时控制工作流的处理程序。 例如，`Auto Advancer`

* **处理程序前进**

  选择此选项可自动将工作流前进到执行后的下一个步骤。 如果未选中，则实施脚本必须处理工作流提升。

### 步骤属性 — 用户/组选项卡 {#step-properties-user-group-tab}

在属性对话框的&#x200B;**用户/组**&#x200B;选项卡上，以下属性可用于许多工作流步骤组件：

* **通过电子邮件通知用户**

   * 当工作流到达步骤时，通过向参与者发送电子邮件通知参与者。
   * 如果启用，会向属性&#x200B;**用户/组**&#x200B;定义的用户发送电子邮件，如果定义了组，则会向组的每个成员发送电子邮件。

* **用户/组**

   * 下拉选择框允许您导航到用户或组并选择它们。
   * 如果将步骤分配给特定用户，则只有此用户才能执行该步骤。
   * 如果将步骤分配给整个组，则当工作流达到此步骤时，该组中的所有用户都会在其&#x200B;**工作流收件箱**&#x200B;中执行该操作。
   * 有关详细信息，请参阅[参与工作流](/help/sites-authoring/workflows-participating.md)。

## AND 拆分 {#and-split}

**AND Split**&#x200B;在工作流中创建拆分，然后两个分支均处于活动状态。 您可以根据需要向每个分支添加工作流步骤。 此步骤可让您在工作流中引入多个处理路径。 例如，您可以允许并行执行某些审阅步骤，从而节省时间。

![wf-26](assets/wf-26.png)

### AND拆分 — 配置 {#and-split-configuration}

要配置拆分，请执行以下操作：

* 编辑&#x200B;**AND拆分属性**：

   * **拆分名称**：分配名称以供说明
   * 选择所需的分支数；2、3、4或5。

* 根据需要将工作流步骤添加到分支。

  ![wf-27](assets/wf-27.png)

## 容器步骤 {#container-step}

容器步骤会启动另一个作为子工作流执行的工作流模型。

利用此容器，可重复使用工作流模型以实施常见的步骤序列。 例如，翻译工作流模型可用于多个编辑工作流。

![wf-28](assets/wf-28.png)

### 容器步骤 — 配置 {#container-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **容器**

   * **子工作流**：选择要启动的工作流。

## 跳转步骤 {#goto-step}

**跳转步骤**&#x200B;允许您指定要在工作流模型中执行的下一个步骤。 您可以将规则定义、外部脚本或ECMA脚本指定为路由表达式，以评估工作流模型的下一步。

* 如果指定的条件为true，则完成&#x200B;**跳转步骤**，工作流引擎将执行指定的步骤。
* 如果指定的条件不为true，则完成&#x200B;**跳转步骤**，而常规的路由逻辑将决定下一个要执行的步骤。

通过&#x200B;**跳转步骤**，您可以在工作流模型中实施高级路由结构。 例如，要实施循环，可以定义&#x200B;**Goto Step**&#x200B;以执行工作流中的前一个步骤，路由表达式将评估循环条件。

### 跳转步骤 — 配置 {#goto-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **目标步骤**：选择评估路由表达式的条件后要执行的步骤。
   * **路由表达式**：选择规则定义、外部脚本或确定是否执行&#x200B;**目标步骤**&#x200B;的ECMA脚本。

      * **规则定义：**&#x200B;使用[表达式编辑器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor)定义规则。
      * **外部脚本：**&#x200B;外部脚本的路径。
      * **ECMA脚本**：用于确定是否执行&#x200B;**跳转步骤**&#x200B;的脚本。

#### 模拟for循环 {#simulating-a-for-loop}

模拟“for循环”要求您保持已发生的循环迭代次数的计数：

* 计数通常表示工作流中执行的项目的索引。
* 计数将作为循环的退出条件评估。

例如，要实施一个在多个JCR节点上执行操作的工作流，您可以使用循环计数器作为节点的索引。 若要保留该计数，请在工作流实例的数据映射中存储`integer`值。 若要递增计数并将计数与退出条件进行比较，请使用&#x200B;**跳转步骤**&#x200B;的脚本。

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 使用规则定义模拟for循环 {#simulateforloop}

也可以使用“规则定义”作为路由表达式来模拟for循环。 [创建Long数据类型的&#x200B;**count**&#x200B;变量](/help/forms/using/variable-in-aem-workflows.md#create-a-variable)。 在&#x200B;**[设置变量](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)**&#x200B;步骤中使用&#x200B;**表达式**&#x200B;作为映射模式，以便在&#x200B;**设置变量**&#x200B;步骤的每次执行时将&#x200B;**count**&#x200B;变量的值设置为&#x200B;**count + 1**。

![模拟循环](assets/variable_use_case_count_new.png)

在&#x200B;**Goto Step**&#x200B;中，使用&#x200B;**Set Variable**&#x200B;作为&#x200B;**目标步骤**，使用&#x200B;**count &lt; 5**&#x200B;作为路由表达式。

![模拟for循环的条件](assets/variable_use_case_count1_new.png)

**Set Variable**&#x200B;步骤重复运行，每次运行&#x200B;**count**&#x200B;变量的值将递增1，直至达到5。

## OR 拆分 {#or-split}

**OR拆分**&#x200B;在工作流中创建拆分，之后只有一个分支处于活动状态。 此步骤允许您将条件处理路径引入工作流。 您可以根据需要向每个分支添加工作流步骤。

>[!NOTE]
>
>请参阅[OR拆分步骤](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable)

使用OR拆分进行![分支](assets/variables_orsplit_new.png)

### OR拆分 — 配置 {#or-split-configuration}

要配置拆分，请执行以下操作：

* 编辑&#x200B;**OR拆分属性**：

   * **公共**

      * 指定拆分名称。

   * **分支(*x)***

      * **添加分支：**&#x200B;向步骤中添加更多分支。
      * **选择路由表达式**：要计算活动分支，请选择路由表达式。 可能的值包括：规则定义、外部脚本和ECMA脚本。
      * **单击以添加表达式**：如果选择&#x200B;**规则定义**&#x200B;作为路由表达式，则添加表达式以评估活动分支。
      * **脚本路径**：如果选择&#x200B;**外部脚本**&#x200B;作为路由表达式，则指向包含用于评估活动分支的脚本的文件的路径。
      * **脚本**：如果选择&#x200B;**ECMA脚本**&#x200B;作为路由表达式，请在框中添加脚本以评估活动分支。
      * **默认路由**：如果有多个分支，则遵循默认分支。 您只能指定一个分支作为默认分支。

  >[!NOTE]
  >
  >    * 每次根据路由表达式评估一个分支。
  >    * 将从上到下评估分支。
  >    * 执行第一个计算为true的脚本。
  >    * 如果没有分支的计算结果为true，则工作流不会前进。
  >
  >

  >[!NOTE]
  >
  >请参阅[为OR拆分](/help/sites-developing/workflows-models.md#defineruleecmascript)定义规则。

* 根据需要将工作流步骤添加到分支。

## 参与者步骤和选择器 {#participant-steps-and-choosers}

### 参与者步骤 {#participant-step}

**参与者步骤**&#x200B;允许您为特定操作分配所有权。 仅当用户手动确认该步骤时，工作流才会继续。 当您希望某个人对工作流执行操作时，可使用此工作流。 例如，审阅步骤。

虽然不直接相关，但在分配操作时必须考虑用户授权；用户必须具有对工作流有效负载页面的访问权限。

#### 参与者步骤 — 配置 {#participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)

>[!NOTE]
>
>在以下情况下，将始终通知工作流启动器：
>
>* 工作流已完成（已完成）。
>* 工作流已中止（已终止）。
>

>[!NOTE]
>
>必须配置某些属性以启用电子邮件通知。 您还可以自定义电子邮件模板或添加新语言的电子邮件模板。 要在AEM中配置电子邮件通知，请参阅[配置电子邮件通知](/help/sites-administering/notification.md#configuringemailnotification)。

### 对话框参与者步骤 {#dialog-participant-step}

使用&#x200B;**对话框参与者步骤**&#x200B;从分配工作项的用户那里收集信息。 此步骤可用于收集稍后在工作流中使用的少量数据。

完成步骤后，**完成工作项**&#x200B;对话框包含您在对话框中定义的字段。 在字段中收集的数据存储在工作流有效负荷的节点中。 然后，后续工作流步骤可以从存储库中读取值。

要配置该步骤，请指定要为其分配工作项的组或用户，以及对话框的路径。

#### 对话框参与者步骤 — 配置 {#dialog-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **对话框**

   * **对话框路径**：您创建的[对话框的对话框节点的路径](#dialog-participant-step-creating-a-dialog)。

#### 对话框参与者步骤 — 创建对话框 {#dialog-participant-step-creating-a-dialog}

要创建对话框，必须创建对话框：

* 确定所得数据在有效负载[&#128279;](#dialog-participant-step-storing-data-in-the-payload)中的存储位置。
* [定义对话框；包括定义用于收集和保存数据的字段](#dialog-participant-step-dialog-definition)。

#### 对话框参与者步骤 — 在有效负荷中存储数据 {#dialog-participant-step-storing-data-in-the-payload}

您可以将构件数据存储在工作流有效负载或工作项元数据中。 构件节点的`name`属性的格式决定了数据的存储位置。

* **使用有效负载**&#x200B;存储数据

   * 要将构件数据存储为工作流有效负荷的属性，请为构件节点的name属性的值使用以下格式：

     `./jcr:content/nodename`

   * 该数据存储在有效负荷节点的`nodename`属性中。 如果节点不包含该属性，则会创建属性。
   * 与有效负载一起存储时，后续使用具有相同有效负载的对话框会覆盖属性的值。

* **与工作项一起存储数据**

   * 要将小部件数据存储为工作项元数据的属性，请为name属性的值使用以下格式：

     `nodename`

   * 该数据存储在工作项`metadata`的`nodename`属性中。 如果之后对同一有效负载使用该对话框，则数据将保留。

#### 对话框参与者步骤 — 对话框定义 {#dialog-participant-step-dialog-definition}

1. **对话框结构**

   对话框参与者步骤的对话框与为创作组件创建的对话框类似。 它们存储在以下位置：

   `/apps/myapp/workflow/dialogs`

   标准触屏UI的对话框具有以下节点结构：

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >请参阅[创建和配置对话框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)。

1. **对话框路径属性**

   **Dialog参与者步骤**&#x200B;具有&#x200B;**Dialog Path**&#x200B;属性（以及[参与者步骤](#participant-step)的属性）。 **Dialog Path**&#x200B;属性的值是您的对话框`dialog`节点的路径。

   例如，该对话框包含在存储在节点中的名为`EmailWatch`的组件中：

   `/apps/myapp/workflows/dialogs`

   对于触屏优化UI，以下值用于&#x200B;**对话框路径**&#x200B;属性：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例对话框定义**

   以下XML代码段表示在有效负荷内容的`watchEmail`节点中存储`String`值的对话框。 标题节点表示[TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html)组件：

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   在触屏优化UI中，此示例会生成一个对话框，如下所示：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 动态参与者步骤 {#dynamic-participant-step}

**动态参与者步骤**&#x200B;组件与&#x200B;**[参与者步骤](#participant-step)**&#x200B;类似，不同之处在于参与者是在运行时自动选择的。

要配置该步骤，请选择一个&#x200B;**参与者选择器**&#x200B;和一个对话框，该选择器标识要为其分配工作项的参与者。

#### 动态参与者步骤 — 配置 {#dynamic-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参与者选择器**

   * **参与者选择器**：您创建的[参与者选择器](#developingtheparticipantchooser)的名称。
   * **参数**：任何必需的参数。
   * **电子邮件**：是否应向用户发送电子邮件通知。

* **对话框**

   * **对话框路径**：您创建的[对话框的对话框节点的路径（与&#x200B;**对话框参与者步骤**&#x200B;一样）](#dialog-participant-step-creating-a-dialog)。

#### 动态参与者步骤 — 开发参与者选择器 {#dynamic-participant-step-developing-the-participant-chooser}

创建参与者选择器。 因此，您可以使用任何选择逻辑或标准。 例如，参与者选择器可以选择（在组内）工作项最少的用户。 您可以创建任意数量的参与者选择器，以与工作流模型中&#x200B;**动态参与者步骤**&#x200B;组件的不同实例一起使用。

创建一个OSGi服务或一个ECMAScript ，用于选择要将工作项分配到的用户。

* **ECMAscript**

  脚本必须包含一个名为getParticipant的函数，该函数将用户ID作为`String`值返回。 将自定义脚本存储在`/apps/myapp/workflow/scripts`文件夹或子文件夹中。

  标准AEM实例中包含一个示例脚本：

  `/libs/workflow/scripts/initiator-participant-chooser.ecma`

  >[!CAUTION]
  >
  >请勿更改`/libs`路径中的任何内容。
  >
  >
  >原因是下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时可能会被覆盖）。

  此脚本选择工作流发起者作为参与者：

  ```
  function getParticipant() {
      return workItem.getWorkflow().getInitiator();
  }
  ```

  >[!NOTE]
  >
  >**工作流发起者参与者选择器**&#x200B;组件扩展&#x200B;**动态参与者步骤**&#x200B;并将此脚本用作步骤实现。

* **OSGi服务**

  服务必须实现[com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html)接口。 该界面定义了以下成员：

   * `SERVICE_PROPERTY_LABEL`字段：使用此字段指定参与者选择器的名称。 该名称出现在&#x200B;**动态参与者步骤**&#x200B;属性的可用参与者选择器列表中。

   * `getParticipant`方法：以`String`值的形式返回动态解析的主体ID。

  >[!CAUTION]
  >
  >`getParticipant`方法返回动态解析的主体ID。 此id可以是组id或用户id。
  >
  >
  >但是，当返回参与者列表时，组ID只能用于&#x200B;**参与者步骤**。 对于&#x200B;**动态参与者步骤**，返回空列表且无法用于委派。

  若要使您的实现对&#x200B;**动态参与者步骤**&#x200B;组件可用，请将Java™类添加到导出服务的OSGi捆绑包中，并将该捆绑包部署到AEM服务器。

  >[!NOTE]
  >
  >**随机参与者选择器**&#x200B;是选择随机用户(`com.day.cq.workflow.impl.process.RandomParticipantChooser`)的示例服务。 **随机参与者选择** r步骤组件示例扩展了&#x200B;**动态参与者步骤**，并将此服务用作步骤实现。

#### 动态参与者步骤 — 参与者选择器服务示例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java™类实现`ParticipantStepChooser`接口。 此类将返回启动工作流的参与者的姓名。 代码使用的逻辑与示例脚本(`initiator-participant-chooser.ecma`)使用的逻辑相同。

`@Property`注释将`SERVICE_PROPERTY_LABEL`字段的值设置为`Workflow Initiator Participant Chooser`。

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

在&#x200B;**动态参与者步骤**&#x200B;属性对话框中，**参与者选择器**&#x200B;列表包含表示此服务的项`Workflow Initiator Participant Chooser (script)`。

启动工作流模型时，日志会指示启动工作流的用户ID以及分配了工作项的用户ID。 在此示例中，`admin`用户启动了该工作流。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表单参与者步骤 {#form-participant-step}

**表单参与者步骤**&#x200B;会在工作项打开时显示表单。 当用户填写并提交表单时，字段数据存储在工作流有效负荷的节点中。

要配置该步骤，请指定要为其分配工作项的组或用户，以及窗体的路径。

>[!CAUTION]
>
>本节介绍用于页面创作[&#128279;](/help/sites-authoring/default-components-foundation.md#form)的基础组件的Forms部分。

#### 表单参与者步骤 — 配置 {#form-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **表单**

   * **表单路径**：您创建的[表单的路径](#form-participant-step-creating-the-form)。

#### 表单参与者步骤 — 创建表单 {#form-participant-step-creating-the-form}

创建正常用于&#x200B;**表单参与者步骤**&#x200B;的表单。 但是，表单参与者步骤的表单必须具有以下配置：

* 表单&#x200B;**组件的**&#x200B;开始必须将&#x200B;**Action Type**&#x200B;属性设置为`Edit Workflow Controlled Resource(s)`。
* 表单&#x200B;**组件的** Start必须具有`Form Identifier`属性的值。
* 表单组件必须将&#x200B;**元素名称**&#x200B;属性设置为存储字段数据的节点的路径。 路径必须在工作流有效负荷内容中找到节点。 该值使用以下格式：

  `./jcr:content/path_to_node`

* 该表单必须包含&#x200B;**工作流提交按钮**&#x200B;组件。 您未配置组件的任何属性。

工作流的要求决定了字段数据的存储位置。 例如，字段数据可用于配置页面内容的属性。 **元素名称**&#x200B;属性的以下值将字段数据存储为`jcr:content`节点的`redirectTarget`属性的值：

`./jcr:content/redirectTarget`

在以下示例中，字段数据用作有效负荷页面上&#x200B;**Text**&#x200B;组件的内容：

`./jcr:content/par/text_3/text`

第一个示例可用于`cq:Page`组件呈现的任何页面。 第二个示例只能在有效负荷页面包含ID为`text_3`的&#x200B;**Text**&#x200B;组件时使用。

表单可位于存储库中的任意位置，但必须授权工作流用户阅读表单。

### 随机参与者选择器 {#random-participant-chooser}

**随机参与者选择器**&#x200B;步骤是一个参与者选择器，它将生成的工作项分配给从列表中随机选择的用户。

![wf-31](assets/wf-31.png)

#### 随机参与者选择器 — 配置 {#random-participant-chooser-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参数**

   * **参与者**：指定可供选择的用户列表。 要将用户添加到列表，请单击&#x200B;**添加项**，然后键入用户节点的主目录路径或用户ID。 用户的顺序不会影响分派工作项的可能性。

### 工作流发起者参与人选择器 {#workflow-initiator-participant-chooser}

**工作流发起者参与者选择器**&#x200B;步骤是一个参与者选择器，它将生成的工作项分配给启动工作流的用户。 除&#x200B;**常用**&#x200B;属性外，没有要配置的属性。

#### 工作流发起者参与人选择器 — 配置 {#workflow-initiator-participant-chooser-configuration}

要配置该步骤，请使用以下选项卡进行编辑：

* [通用](#step-properties-common-tab)

## 进程步骤 {#process-step}

**进程步骤**&#x200B;执行ECMAScript或调用OSGi服务以执行自动处理。

![wf-32](assets/wf-32.png)

### 流程步骤 — 配置 {#process-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **进程**：要执行的进程实现。 使用下拉菜单选择ECMAScript或OSGi服务。 有关以下内容的信息：

      * 标准ECMAScript和OSGi服务，请参阅[进程步骤的内置进程](/help/sites-developing/workflows-process-ref.md)。
      * 为流程步骤创建ECMAScript，请参阅[使用ECMAScript实施流程步骤](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。
      * 正在为进程步骤创建OSGi服务，请参阅[使用Java™类实施进程步骤](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)。

   * **处理程序前进**：选择此选项可自动将工作流前进到执行后的下一个步骤。 如果未选中，则实施脚本必须处理工作流提升。
   * **参数**：要传递给进程的参数。

## 设置变量 {#set-variable}

“设置变量”步骤允许您设置变量的值并定义值的设置顺序。 变量将按照变量映射在“设置变量”步骤中列出的顺序进行设置。

![添加映射以设置变量](assets/set_variable_addmappingnew.png)

### 设置变量 — 配置 {#setvariable}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **选择变量：**&#x200B;使用此选项选择一个变量来设置其值。
   * **选择映射模式：**&#x200B;要设置变量的值，请选择映射模式。 根据变量的数据类型，您可以使用以下选项设置变量的值：

      * **文本：**&#x200B;当您知道要指定的确切值时，请使用选项。
      * **表达式：**&#x200B;根据表达式计算要使用的值时，请使用选项。 表达式是在提供的表达式编辑器中创建的。
      * **JSON点表示法：**&#x200B;使用选项从JSON或FDM类型变量中检索值。
      * **XPATH：**&#x200B;使用选项从XML类型变量中检索值。
      * **相对于有效负载：**&#x200B;当要保存到变量的值在相对于有效负载的路径上可用时，请使用选项。
      * **绝对路径：**&#x200B;当要保存到变量的值在绝对路径上可用时，请使用选项。

   * **指定值：**&#x200B;要映射到变量，请指定值。 在此字段中指定的值取决于映射模式。
   * **添加映射：**&#x200B;使用此选项可添加更多映射以设置变量的值。
