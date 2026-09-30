---
title: 自定义命名空间
description: 了解如何定义自定义命名空间并将其部署到AEM 6.5 LTS。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: cd14456d-a492-4b5c-8a82-1fbd4460dbd2
    internal-label: Java Content Repository
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%
---

# 自定义命名空间{#custom-namespaces}

了解如何定义自定义[命名空间](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/jcr/1.0/4.5_Namespaces.html)并将其部署到AEM 6.5 LTS。

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
