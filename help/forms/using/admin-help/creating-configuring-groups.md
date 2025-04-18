---
title: 创建和配置组
description: 了解如何手动或动态创建组、编辑组、查看有关组的详细信息或删除组。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: e8824453-8891-40e0-9948-c0c0f0fdce62
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 0%

---

# 创建和配置组{#creating-and-configuring-groups}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

通过创建用户组，您可以将角色分配给组，而不是分配给单个用户。

提供了两种不同类型的组。 您可以手动创建组并将用户和其他组添加到其中。 您还可以创建动态组，以自动包含满足一组指定规则的所有用户。

如果用户属于多个组（例如，500个或更多）或这些组嵌套得很深（例如，30个级别），则用户响应速度可能会较慢。 如果您遇到此问题，可以将AEM表单配置为从特定域预取信息。 (请参阅[配置AEM表单以预取域信息](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information)。)

## 手动创建组 {#create-a-group-manually}

手动创建组时，可以向组添加用户和其他组，并为组分配角色。 您还可以将组与父组关联。

如果您正在使用Content Services（已弃用），则可以选择“域管理”页面上的“选择此选项以将用户和组推送到已注册的外部承担者存储提供程序”选项，以推送您在Content Services中创建的任何新用户或组的信息（已弃用）。

1. 在管理控制台中，单击“设置”>“用户管理”>“用户和组”，然后单击“新建组”。
1. 完成“常规设置”部分，然后单击“下一步”。 规范名称和组名称是必需属性。

   规范名称是组的唯一标识符。 域中的每个组和用户必须具有唯一的规范名称。 选中“系统生成”复选框以允许用户管理分配唯一值，或清除该复选框并指定“规范名称”的自定义值。

   避免在规范名称中使用下划线字符(_)，例如`sample_group`。 当您基于组的规范名称搜索组时，不会返回包含下划线字符的组。

1. 要将用户和组添加到此新组，请单击“查找用户/组”，然后执行以下任务：

   * 在“查找”框中，键入搜索条件。
   * 在“在”列表中，选择“用户”、“组”或“用户和组”。
   * 在使用列表中，选择名称、电子邮件或用户ID。
   * 选择域，选择要显示的项目数，然后单击“查找”。
   * 在搜索结果中，选中要添加到此新组的用户和组的复选框，然后单击“确定”。

1. 单击“下一步”。
1. 若要将此新组添加到其他现有组，请单击“查找组”，然后执行以下任务：

   * 在“查找”框中，键入搜索条件。
   * 选择域，选择要显示的项目数，然后单击“查找”。
   * 在搜索结果中，选中新组所属组的复选框，然后单击“确定”。

1. 单击“下一步”。
1. 要将角色分配给组，请单击“查找角色”，选中要分配给组的每个角色的复选框，然后单击“确定”。 组中的用户将继承在组级别分配的角色。
1. 单击“完成”。

## 创建动态组 {#create-a-dynamic-group}

在动态组中，不会单独选择属于该组的用户。 而是指定一组规则，并且符合这些规则的所有用户都会自动添加到动态组中。

使用以下两种方法之一创建动态组：

* 基于电子邮件域(如@adobe.com)启用动态组的自动创建。 启用此功能后，用户管理会为AEM表单数据库中的每个唯一电子邮件域创建一个动态组。 使用cron表达式可指定用户管理在AEM表单数据库中搜索新电子邮件域的频率。 这些动态组已添加到DefaultDom本地域，并命名为“具有&#x200B;*`[email domain]`*&#x200B;邮件ID的所有用户”。
* 根据指定的条件（包括用户的电子邮件域、描述、规范名称和域名）创建动态组。 要属于动态组，用户必须满足所有指定的标准。 要设置“或”条件，请创建两个不同的动态组，并将它们添加到本地组中。 例如，使用该方法创建一组属于@adobe.com电子邮件域或其规范名称包含ou=adobe.com的用户。 但是，用户不一定必须同时满足这两个条件。

动态组仅包含用户。 它不能包含其他组。 但是，动态组可以属于父组。

### 根据电子邮件域自动创建动态组 {#automatically-create-dynamic-groups-based-on-email-domains}

1. 单击设置>用户管理>配置>配置高级系统属性。
1. 在“自动创建动态组”下，选中复选框。
1. 指定用户管理器何时检查新电子邮件域。 该时间应晚于域同步时间，因为仅当完成域同步后，创建动态组才是逻辑的。

   * 要启用每日自动同步，请在“每日发生”框中以24小时格式键入时间。 保存设置时，此值将转换为cron表达式，该表达式显示在下面的框中。
   * 要安排在一周或一个月中的某一天或某一特定月份进行同步，请在框中选择键入相应的cron表达式。 默认值为`0 00 4 ? * *`（表示在每天凌晨4点查看）。

     cron表达式的使用基于Quartz开源作业调度系统1.4.0版。

1. 单击“保存”。

### 根据指定的条件创建动态组 {#create-a-dynamic-group-based-on-specified-criteria}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 单击“新建动态组”。
1. 完成“常规设置”部分。 组名称是必需属性。 您可以将组分配给任何配置的域。
1. 在“动态组条件”下，指定一个或多个用于填充动态组的属性。

   >[!NOTE]
   >
   >使用Equals运算符时，“电子邮件”、“描述”和“规范名称”属性区分大小写。 使用Starts With、Ends With或Contains运算符时，它们不区分大小写。

   **电子邮件：**&#x200B;用户的电子邮件域，如`@adobe.com`。

   **描述：**&#x200B;用户的描述，如“计算机科学家”

   **规范名称：**&#x200B;用户的规范名称，如`ou=adobe.com`

   **域名：**&#x200B;用户所属的域名，如`DefaultDom`。 使用Contains运算符时，“域名”属性区分大小写。 它与Starts With、Ends With或Equals运算符不区分大小写。

1. 单击测试。 “测试”页面会显示前200个符合所规定标准的用户。 单击“关闭”。
1. 如果测试返回了预期结果，请单击“下一步”。 否则，请编辑动态组标准并再次进行测试。
1. 要将动态组添加到父组，请单击“查找组”，然后执行以下任务：

   * 在“查找”框中，键入搜索条件。
   * 选择域，选择要显示的项目数，然后单击“查找”。
   * 在搜索结果中，选中动态组所属组的复选框，然后单击“确定”。

1. 单击“下一步”。
1. 要将角色分配给动态组，请单击“查找角色”，选中要分配给该组的每个角色的复选框，然后单击“确定”。 组中的用户将继承在组级别分配的角色。
1. 单击“完成”。

## 查看有关组的详细信息 {#view-details-about-a-group}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 在“在”列表中，选择“组”，然后单击“查找”。 搜索结果将列在页面底部。 您可以通过单击任意列标题对列表进行排序。
1. 单击组的名称可显示有关的详细信息。 此时将显示“组详细信息”页面。
1. 要查看组的直接成员，请单击“子主用户”。

## 编辑组 {#edit-a-group}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 要查找要编辑的组，请执行以下任务：

   * 在“查找”框中，键入搜索条件。
   * 在使用列表中，选择名称或电子邮件。
   * 在“在”列表中，选择“组”。
   * 选择域，选择要显示的项目数，然后单击“查找”。
   * 在搜索结果中，单击要编辑的组的名称。

1. 在“详细信息”选项卡上，编辑常规设置并单击“保存”。
1. 要编辑关联的组，请单击“父组”选项卡，然后执行以下任务：

   * 要查找要添加到关联的组，请单击“查找组”并完成搜索信息。
   * 要添加组，请选中要添加组的复选框，单击“确定”，然后单击“保存”。
   * 要删除关联的组，请选中要删除的组的复选框，单击“删除”，单击“确定”，然后单击“保存”。

1. 要编辑组中的用户和组，请单击“子承担者”选项卡，然后执行以下任务：

   * 要查找要添加的用户和组，请单击“查找用户/组”并完成搜索信息。
   * 要添加用户或组，请选中用户或组的复选框，单击“确定”，然后单击“保存”。
   * 要删除用户或组，请选中该用户或组的复选框，单击“删除”，单击“确定”，然后单击“保存”。

1. 要编辑角色分配，请单击“角色分配”选项卡，然后执行以下任务：

   * 要查找要分配给组的角色，请单击“查找角色”。
   * 要添加角色，请选中该角色的复选框，单击“确定”，然后单击“保存”。
   * 要取消分配角色，请选中该角色的复选框，单击取消分配，然后单击保存。

## 删除组 {#delete-a-group}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 在“查找”列表中选择“组”，然后单击“查找”。
1. 选中要删除的组的复选框，单击删除，然后单击确定。
