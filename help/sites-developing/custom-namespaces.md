---
title: 自定义命名空间
description: 了解如何定义自定义命名空间并将其部署到AEM 6.5 LTS。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 475a77e8e4ff0ecd19a939fd3b3c9294adf24997
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 8%

---


# 自定义命名空间{#custom-namespaces}

了解如何定义自定义[命名空间](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html)并将其部署到AEM 6.5 LTS。

自定义命名空间是`:`之前的JCR属性的可选部分。 AEM使用多个命名空间，例如：

+ JCR系统属性为`jcr`
+ 用于AEM（以前称为Adobe CQ）属性的`cq`
+ 特定于DAM资源的AEM资产的`dam`
+ 都柏林核心属性的`dc`

...和其他很多人。

命名空间可用于表示属性的范围和用途。 创建自定义命名空间（通常是您的公司名称）有助于明确识别AEM实施特定的节点或资产，并包含特定于您的业务的数据。

自定义命名空间在[Sling存储库初始化(repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html)脚本中进行管理，并在项目的配置包（例如，`ui.config`）中部署为OSGi配置。

## 资源 {#resources}

+ [Sling存储库初始化(repoinit)文档](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## 代码 {#code}

以下代码用于配置`wknd`命名空间。

### RepositoryInitializer OSGi配置

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{
    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

这允许在AEM中使用使用`wknd`命名空间的自定义属性（由`register namespace`指令后的第一个参数表示）。 有关更高级的脚本定义，请查看[Sling存储库初始化(repoinit)文档](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)中的示例。
