---
title: 自定义 HTTP 标头
description: 了解如何在Adobe Experience Manager Commerce中配置自定义HTTP标头。
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: f25cd95c-4235-4430-8a51-38be1f39b880
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# 自定义 HTTP 标头 {#custom-http-headers}

## 概述 {#overview}

为了更好地控制其后端，作者可以配置将发送到商业引擎的自定义HTTP标头，以及CIF已发送的标头。 常见用例包括多商店设置，您可以在其中使用HTTP标头控制商务后端的响应。

>[!NOTE]
>
>开发人员始终可以使用GraphQL客户端配置来配置自定义HTTP标头。
>

## 配置 {#configuration}

要配置自定义HTTP标头，必须首先定义它们。 必须首先通过使用OSGi配置将自定义HTTP标头添加到`com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl`服务配置来定义它们。

您可以在项目的Cloud Service配置页面中配置HTTP标头的值：

1. 转到“工具”>“Cloud Service服务”>“CIF配置”中的“云配置”页面。
1. 打开现有配置或创建配置。
1. 转到“高级”选项卡，然后找到“自定义HTTP标头”多字段。 您可以选择之前定义的题头并为它们分配值。

使用上述Cloud Service配置的组件随每个GraphQL请求发送这些HTTP标头。

## 限制 {#restrictions}

虽然该服务允许定义任何标头名称，包括标准名称，但它们不可配置。 换句话说，您无法使用此功能覆盖标准HTTP标头。 可以在[mdn Web文档 — HTTP标头](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)下找到受限标头名称的列表。 除了这些标头之外，还有两个标头无法使用：

* &quot;Store&quot; — 由CIF用于识别Adobe Commerce商店
* &quot;Preview-Version&quot; — 由CIF用于检索暂存产品
