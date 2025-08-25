---
title: 常见技术问题解答 (FAQ)
description: 有关 AEM 6.5 LTS 的常见技术问题解答。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f983fc1edc613feaa070c4e82a92aabab9d50cbb
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 99%

---

# AEM 6.5 LTS 技术问题 FAQ {#technical-faq}

本页旨在解答有关 AEM 6.5 LTS 的一些常见技术问题。

## 技术问题 FAQ

### `/systemalive` 端点在 AEM 6.5 LTS 中不再可用。

为提供 `/systemalive` 端点而配置的 Felix System Ready 捆绑包现已弃用，并被 Apache Felix Health Checks 取代。AEM 6.5 LTS 中不再包含此捆绑包。

`/system/health` 提供新的健康检查端点，通过 Apache Felix Health Checks 实施。

有关 Felix Health Check 框架的详细文档，请参阅 [felix 文档](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy 控制台支持

由于缺少 guava 依赖项，AEM 6.5 中使用的 AEM Groovy 控制台版本可能无法在 AEM 6.5 LTS 中运行。新的受支持的 AEM Groovy 控制台版本为 [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)。

### AEM 6.5 LTS 是否支持用户同步？

是的，AEM 6.5 LTS 支持用户同步。AEM 6.5 和 6.5 LTS 两者的用户同步功能没有变化。

### Maven Central 上的 Uber JAR 好像损坏了——这是什么问题？

请验证您使用的 Uber JAR 有 `apis` 分类器。请注意，AEM 6.5 LTS 中 Uber JAR 的包装结构发生了变化。有关详细信息，请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

## 获取额外帮助

如果您遇到的问题这里没有提到：
* 请查看[发行说明](/help/release-notes/release-notes.md)了解已知问题。
* 如需帮助，请与 Adobe 支持部门联系。
