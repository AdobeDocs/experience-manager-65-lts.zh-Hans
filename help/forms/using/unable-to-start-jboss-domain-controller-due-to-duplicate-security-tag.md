---
title: 无法启动JBoss域控制器
description: 在使用JBoss EAP 8的AEM Forms 6.5.1 LTS群集部署中，配置文件可能包含重复的标记。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# 无法启动JBoss域控制器

## 问题

在使用&#x200B;**JBoss EAP 8**&#x200B;的&#x200B;**AEM Forms 6.5.1 LTS**群集部署中，配置文件
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` （以及特定于数据库的变体）可能包含一个&#x200B;**重复的、打开的`<security>`标记**。

这会导致&#x200B;**无效的XML配置**，从而导致&#x200B;**JBoss域控制器启动失败**&#x200B;并阻止群集初始化成功。

## 应用到

* **产品：** AEM Forms 6.5.1 LTS
* **部署类型：**&#x200B;群集
* **应用程序服务器：** JBoss EAP 8.x
* **配置文件：**

   * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## 疑难解答步骤

1. 在域控制器启动过程中，可能会出现以下错误：

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. 打开相关配置文件：

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. 找到重复的开始标记`<security>`。

   **配置不正确：**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. 删除多余的开头`<security>`标记，以便更正配置，如下所示：

   **正确的配置：**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. 保存文件并启动JBoss域控制器。

6. 确保所有群集节点都一致地应用相同的经验证的配置。
