---
title: AEM Forms 服务器性能优化
description: 要使AEM Forms以最佳方式执行，您可以微调缓存设置和JVM参数。 此外，使用Web服务器可以增强AEM Forms部署的性能。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 4009c85e-cb8a-4bed-a6ff-7c76fe78a47f
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# AEM Forms服务器的性能优化{#performance-tuning-of-aem-forms-server}

本文介绍了为减少瓶颈并优化AEM Forms部署性能而可以实施的策略和最佳实践。

## 缓存设置 {#cache-settings}

您可以使用AEM Forms Web Configuration Console中的&#x200B;**移动Forms配置**&#x200B;组件来配置并控制AEM的缓存策略，网址为：

* (OSGi上的AEM Forms) `https://'[server]:[port]'/system/console/configMgr`

<!--
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`
-->

缓存的可用选项如下：

* **无**：强制不缓存任何项目。 实际上，这会降低性能，并且由于缺少缓存而要求较高的内存可用性。
* **保守的**：指示仅缓存在渲染表单之前生成的中间工件，例如包含内联片段和图像的模板。
* **Aggressive**：强制缓存几乎所有可缓存的内容，包括渲染的HTML内容以及来自Conservative缓存级别的所有项目。 它可提供最佳性能，但也会占用更多内存来存储缓存的伪像。 积极主动的缓存策略意味着在缓存渲染的内容时，您可以在渲染表单时获得稳定的时间性能。

AEM Forms的默认缓存设置可能不足以达到最佳性能。 因此，建议使用以下设置：

* **缓存策略**：主动
* **缓存大小**（表单数）：根据需要
* **最大对象大小**：根据需要

![Mobile Forms配置](assets/snap.png)

>[!NOTE]
>
>如果使用AEM Dispatcher缓存自适应表单，则它还会缓存自适应表单，该表单包含具有预填充数据的表单。 如果从AEM Dispatcher缓存中提供此类表单，则可能会导致向用户提供预填或陈旧的数据。 因此，请使用AEM Dispatcher来缓存不使用预填充数据的自适应表单。 此外，Dispatcher缓存不会自动使缓存的片段失效。 因此，请不要使用此数据来缓存表单片段。 对于此类表单和片段，请使用[自适应表单缓存](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM参数 {#jvm-parameters}

为获得最佳性能，建议使用以下JVM `init`参数来配置`Java heap`和`PermGen`。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>推荐的设置适用于Windows 2008 R2 8 Core和Oracle HotSpot 1.7 （64位） JDK，应根据您的系统配置进行放大或缩小。

## 使用Web服务器 {#using-a-web-server}

自适应表单和HTML5表单渲染为HTML5格式。 根据窗体大小和窗体中的图像等因素，生成的输出可能会很大。 为了优化数据传输，推荐的方法是使用为请求提供服务的Web服务器压缩HTML响应。 此方法可减少响应大小、网络流量以及在服务器和客户端计算机之间流式传输数据所需的时间。

例如，执行以下步骤以使用JBoss®在Apache Web Server 2.0 32位上启用压缩：

>[!NOTE]
>
>以下说明不适用于32位Apache Web Server 2.0以外的任何服务器。 有关特定于任何其他服务器的步骤，请参阅相应的产品文档。

以下步骤演示了使用Apache Web Server启用压缩所需的更改

**获取适用于您的操作系统的Apache Web Server软件**

* Windows：从Apache HTTP Server项目站点下载Apache Web Server。
* Solaris™ 64位：从Sunfreeware for Solaris™网站下载Apache Web Server。
* Linux®：在Linux®系统上预安装了Apache Web Server。

Apache可以使用HTTP协议与CRX通信。 这些配置用于使用HTTP进行优化。

1. 在`APACHE_HOME/conf/httpd.conf`文件中取消注释以下模块配置。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >对于Linux®，默认`APACHE_HOME`为`/etc/httpd/`。

1. 在crx的端口4502上配置代理。
在`APACHE_HOME/conf/httpd.conf`配置文件中添加以下配置。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 启用压缩。 在`APACHE_HOME/conf/httpd.conf`配置文件中添加以下配置。

   用于HTML5表单的&#x200B;**&#x200B;**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **对于自适应表单**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   要访问crx服务器，请使用`https://'server':80`，其中`server`是运行Apache服务器的服务器的名称。

## 在运行AEM Forms的服务器上使用防病毒 {#using-an-antivirus-on-server-running-aem-forms}

在运行防病毒软件的服务器上可能会遇到性能变慢的问题。 始终开启的防病毒（即时扫描）软件可扫描系统的所有文件。 它可能会降低服务器的运行速度，并且AEM Forms的性能会受到影响。

为了提高性能，您可以指示防病毒软件从始终运行（按访问）扫描中排除以下AEM Forms文件和文件夹：

* AEM安装目录。 如果无法排除整个目录，请排除以下内容：

   * [AEM安装目录]\crx-repository\temp
   * [AEM安装目录]\crx-repository\repository
   * [AEM安装目录]\crx-repository\launchpad

<!--

* Application server temporary directory. The default location is:

    * (JBoss&reg;) [AEM installation directory]\jboss\standalone\tmp
    * (WebLogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
    * (WebSphere&reg;) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms on JEE only)** Global Document Storage (GDS) directory. The default location is:

    * (JBoss&reg;) [appserver root]/server/'server'/svcnative/DocumentStorage
    * (WebLogic) [appserverdomain]/'server'/adobe/LiveCycleServer/DocumentStorage
    * (WebSphere&reg;) [appserver root]/installedApps/adobe/'server'/DocumentStorage

* **(AEM Forms on JEE only)** AEM Forms Server logs and temporary directory. The default location is:

    * Server logs - [AEM Forms installation directory]\Adobe\AEM forms\[app-server]\server\all\logs
    * Temp directory - [AEM Forms installation directory]\temp
-->

>[!NOTE]
>
>* 如果您使用的是不同的GDS和临时目录位置，请打开`https://'[server]:[port]'/adminui`上的AdminUI，导航到&#x200B;**主页>设置>核心系统设置>核心配置**&#x200B;以确认该位置正在使用中。
>
>* 如果在排除建议的目录后AEM Forms服务器仍运行缓慢，则同时排除Java™可执行文件(java.exe)。
>
