---
title: 请求分析脚本
description: 制作request analysis脚本是为了便于分析access.log文件，生成可读报告供以后处理
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 9fe575ad-1e8d-460f-a933-ddc2e927a6e8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# 请求分析脚本{#request-analysis-script}

## 下载 {#download}

编写此脚本是为了便于分析`access.log`文件，生成可读报告供以后处理。

[获取文件](assets/analyse-access.sh)

## 描述 {#description}

编写此脚本是为了便于分析`access.log`文件，生成可读报告供以后处理。

它生成整体请求数、GET与POST、随时间变化的请求分布等等。

输出采用Markdown语法，因此将更易于用pandoc等工具转换为PDF，或在Markdown查看器等插件的浏览器中显示。

它可以分析命令行上提供的自定义路径。

从文件中用于指示如何运行的注释获取：

分析CQ `access.log`推断各种信息并在`stdout`上生成Markdown输出。

## 用途 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供要在命令行上分析的其他自定义路径

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可通过简单管道保存输出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
