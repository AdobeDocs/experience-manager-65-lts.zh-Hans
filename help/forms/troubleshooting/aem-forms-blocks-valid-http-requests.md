---
title: AEM Forms阻止有效的HTTP请求
description: AEM Forms XSS验证检查可以为使用自定义组件的客户阻止有效的HTTP请求。 了解如何识别问题并暂时放宽验证检查。
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%
---
# AEM Forms阻止有效的HTTP请求 {#aem-forms-blocks-valid-http-requests}

## 问题 {#issue}

AEM Forms包含安全检查，以防止跨站点脚本(XSS)攻击。 对于在AEM Forms中使用自定义组件的客户，这些检查会阻止某些有效的HTTP请求。 当请求被阻止时，服务器日志中会显示以下消息：

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>对于POST请求，参数的默认值为&#x200B;**1048576**。 对于GET请求，参数的默认值为&#x200B;**2000**。 要修改POST请求的参数值，请在服务器启动期间传递`com.adobe.idp.dsc.provider.rest.httpParamMaxSize`参数。

## 原因 {#cause}

XSS验证正则表达式比自定义组件发送的参数值格式更严格，因此AEM Forms拒绝了请求。

## 解决方法 {#resolution}

>[!CAUTION]
>
>删除安全检查会使系统容易遭受跨站点脚本(XSS)攻击。 删除安全检查仅作为临时解决方案。

要临时删除安全检查并允许所有HTTP请求，请执行以下操作：

1. 停止AEM Forms服务器。

1. 创建`[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear`文件的备份。

1. 从`adobe-livecycle-<server_name>.ear`文件中提取`esapi-helper-2.x.x.jar`文件。 `esapi-helper-2.x.x.jar`文件的位置因每个应用程序服务器而异：

   | 应用程序服务器 | esapi-helper-2.x.x.jar文件的位置 |
   | --- | --- |
   | Jboss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle Weblogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. 打开`[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties`和`[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties`文件进行编辑。

1. 将以下属性的值设置为`^[\\s\\S]*$`。 例如，`Validator.HTTPParameterName=^[\\s\\S]*$`。 保存并关闭文件。

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. 在`adobe-livecycle-<application_server_name>.ear`中打包更新的`esapi-helper-2.x.x.jar`。 将更新的`adobe-livecycle-<application_server_name>.ear`部署到应用程序服务器。

1. 启动AEM Forms服务器。

## 引用 {#references}

* [缓解JEE 6.5 LTS SP2上AEM Forms的服务器端请求伪造(SSRF)漏洞](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
