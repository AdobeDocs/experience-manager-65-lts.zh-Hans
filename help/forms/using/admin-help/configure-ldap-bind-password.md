---
title: 配置LDAP绑定口令
description: 了解在将配置文件导入其他系统之前，如何配置绑定密码字段。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 33e0f81f-7867-4c59-a9e5-75bf5182a27c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 配置LDAP绑定口令{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

为避免安全风险，未配置导出配置文件(config.xml)中的绑定密码字段。 在将配置文件导入另一个系统之前，请确保配置此密码。 此密码将覆盖存储在数据库中的现有密码。 Null口令不会覆盖现有的非Null口令值。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 要将当前配置设置导出到文件，请单击“导出”并将配置文件保存到其他位置。
1. 在文件中，找到`Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig`节点。 示例如下：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   键入`bindpassword`的值并保存更改。

1. 在文件中，找到`Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`节点。 示例如下：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   键入`bindpassword`的值并保存更改。

1. 要导入更新的文件，请在“用户管理”中单击“配置”>“导入和导出配置文件”。
1. 单击“浏览”查找文件，单击“导入”，然后单击“确定”。
