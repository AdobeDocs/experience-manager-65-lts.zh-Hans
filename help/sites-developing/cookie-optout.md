---
title: 配置Cookie用法
description: AEM提供的服务允许您配置并控制Cookie在网页中的使用方式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 219555d8-26e1-4047-b885-ec34084154c1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# 配置Cookie用法{#configuring-cookie-usage}

AEM提供的服务允许您配置并控制Cookie在网页中的使用方式：

* 可配置的服务器端服务维护一个可用的Cookie列表。
* JavaScript API允许您的JavaScript代码验证是否可以使用Cookie。

使用此功能可确保您的页面在有关Cookie使用方面符合用户的同意。

## 配置允许的Cookie {#configuring-allowed-cookies}

配置Adobe Granite选择退出服务，以指定如何在您的网页上使用Cookie。 下表描述了可以配置的属性。

要配置服务，您可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表描述了任一方法所需的属性。 对于OSGi配置，服务PID为`com.adobe.granite.optout`。

| 属性名称（Web 控制台） | OSGi 属性名称 | 描述 |
|---|---|---|
| 选择退出Cookie | optout.cookies | Cookie的名称，指示当存在于用户的设备上时，用户尚未同意使用Cookie。 |
| 选择禁用HTTP标头 | optout.headers | 表示用户尚未同意使用Cookie的HTTP标头的名称（如果存在）。 |
| 白名单Cookie | optout.whitelist.cookies | 对网站正常运行至关重要的且可在未经用户同意的情况下使用的Cookie列表。 |

## 验证Cookie使用情况 {#validating-cookie-usage}

使用客户端JavaScript调用Adobe Granite选择退出服务以验证您是否可以使用Cookie。 使用Granite.OptOutUtil JavaScript对象执行以下任意任务：

* 获取Cookie名称列表，以表明用户不同意使用Cookie进行跟踪。
* 获取可用的Cookie列表。
* 确定Web浏览器是否包含指示用户不同意使用Cookie进行跟踪的Cookie。
* 确定是否可使用特定Cookie。

granite.utils [客户端库文件夹](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)提供Granite.OptOutUtil对象。 将以下代码添加到页头JSP中，以包含指向JavaScript库的链接：

`<ui:includeClientLib categories="granite.utils" />`

例如，以下JavaScript函数决定在写入COOKIE_NAME Cookie之前是否允许使用该函数：

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil JavaScript对象 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil允许您确定是否允许使用Cookie。

### getCookieNames()函数 {#getcookienames-function}

Cookie的名称，如果存在，则表示用户未同意使用Cookie。

**参数**

无。

**返回**

Cookie名称的数组。

#### getWhitelistCookieNames()函数 {#getwhitelistcookienames-function}

无论用户是否同意，都可以使用的Cookie的名称。

**参数**

无。

**返回**

Cookie名称的数组。

#### isOptedOut()函数 {#isoptedout-function}

确定用户的浏览器是否包含表明未同意使用Cookie的任何Cookie。

**参数**

无。

**返回**

如果找到指示不同意的Cookie，则布尔值为`true`；如果没有Cookie指示不同意，则布尔值为`false`。

### maySetCookie(cookieName)函数 {#maysetcookie-cookiename-function}

确定在用户浏览器上是否可以使用特定Cookie。 此函数等同于使用`isOptedOut`函数来确定给定的Cookie是否包含在`getWhitelistCookieNames`函数返回的列表中。

**参数**

* cookieName：字符串。 Cookie的名称。

**返回**

如果可以使用`cookieName`，则布尔值为`true`；如果无法使用`cookieName`，则布尔值为`false`。
