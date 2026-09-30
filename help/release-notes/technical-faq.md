---
title: 常见技术问题解答 (FAQ)
description: 有关 AEM 6.5 LTS 的常见技术问题解答。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 78%
---
# AEM 6.5 LTS 技术常见问题解答 {#technical-faq}

本页旨在解答有关 AEM 6.5 LTS 的一些常见技术问题。

## 技术问题 FAQ

### `/systemalive` 端点在 AEM 6.5 LTS 中不再可用。

为提供 `/systemalive` 端点而配置的 Felix System Ready 捆绑包现已弃用，并被 Apache Felix Health Checks 取代。 AEM 6.5 LTS 中不再包含此捆绑包。

`/system/health` 提供新的健康检查端点，通过 Apache Felix Health Checks 实施。

有关 Felix Health Check 框架的详细文档，请参阅 [felix 文档](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy Console 支持

由于缺少 guava 依赖项，AEM 6.5 中使用的 AEM Groovy Console 版本可能无法在 AEM 6.5 LTS 中运行。 新的受支持的 AEM Groovy Console 版本为 [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)。

#### AEM Groovy Console 所需的其他配置

如果您使用 AEM Groovy Console，就必须为 `com.adobe.granite.apicontroller.FilterResolverHookFactory` 明确添加以下 OSGi 配置。 将 `aem-groovy-console-bundle` 添加到 `org.apache.sling.distribution.api` 键的允许捆绑包列表中，扩展平台默认值：

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### AEM 6.5 LTS 是否支持用户同步？

是的，AEM 6.5 LTS 支持用户同步。 AEM 6.5 和 6.5 LTS 两者的用户同步功能没有变化。

### Maven Central 上的 Uber JAR 好像损坏了——这是什么问题？

请验证您使用的 Uber JAR 有 `apis` 分类器。 请注意，AEM 6.5 LTS 中 Uber JAR 的包结构发生了变化。 有关详细信息，请参阅[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### AEM 6.5 LTS是否支持`jakarta.*`包命名空间（例如，`jakarta.annotation`）？

不会。 AEM 6.5 LTS不支持迁移到`jakarta.*`包命名空间的Sling工件。 在您的代码和依赖项中使用`javax.*`等效项 — 例如，在Sling模型中使用`javax.annotation.PostConstruct`而非`jakarta.annotation.PostConstruct`。 AEM 6.5 LTS中的Sling模型实现仅识别`javax.*`注释，因此在初始化期间静默忽略`jakarta.*`注释。

有关详细信息，请参阅知识库文章[在AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-30339)上带有`jakarta.annotation.PostConstruct`的Sling模型失败。

## 获取额外帮助

如果您遇到的问题这里没有提到：
* 请查看[发行说明](/help/release-notes/release-notes.md)了解已知问题。
* 如需帮助，请与 Adobe 支持部门联系。
