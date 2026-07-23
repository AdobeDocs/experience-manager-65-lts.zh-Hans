---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS文档
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.zh-Hans
index: true
type: Documentation
solution: Experience Manager, Experience Manager 6.5 LTS
nudge: yes
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
  - id: ae206583-dab1-444b-b978-a37aad4a988c
usetq: true
landing-page-name: experience-manager-65-lts
landing-page-breadcrumb-title: AEM 6.5 LTS
version: Experience Manager 6.5 LTS
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: cef81ae3bc173efc490f9c7b98792c27d77caf7f
workflow-type: tm+mt
source-wordcount: 93
ht-degree: 2%

---


# 元数据供内部使用

GitHub创作系统中的元数据是分层的，并定义了以下相对于前一项的递增级别。

1. metadata.md
1. ToC
1. 文章

在metadata.md文件中定义的元数据应用到整个存储库，但可以在ToC和文章级别覆盖。 任何覆盖元数据的操作应在尽可能最低的级别进行。

experience-manager-cloud-service.en存储库中的元数据是最低要求。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` （仅在`/help/assets`下的核心资源内容上）
