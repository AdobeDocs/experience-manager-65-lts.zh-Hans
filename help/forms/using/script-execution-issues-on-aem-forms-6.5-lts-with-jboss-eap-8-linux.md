---
title: 在使用JBoss EAP 8 (Linux)的AEM Forms 6.5 LTS上脚本执行失败
description: 在Linux环境中设置JBoss EAP 8.0时，在运行shell脚本或启动文件时可能会遇到某些错误
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---


# 在使用JBoss EAP 8 (Linux)的AEM Forms 6.5 LTS上脚本执行失败

## 问题

在&#x200B;**Linux**&#x200B;环境中设置&#x200B;**JBoss EAP 8.0 (AEM Forms 6.5.1 LTS)**&#x200B;时，在运行shell脚本或启动文件时，可能会遇到以下错误之一：

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

在&#x200B;**Windows**&#x200B;系统上创建或编辑Shell脚本或配置文件并包含&#x200B;**CRLF（回车+换行）**行结尾时，会发生这些错误。
Linux系统仅支持**LF（换行）**&#x200B;行结尾，并且Windows样式的行结尾会导致脚本执行失败。

## 应用到

* **JBoss EAP 8.0**
* **基于Linux/UNIX的操作系统**

## 疑难解答步骤

1. **识别受影响的文件**

   * 查看错误输出以识别导致失败的`.sh`脚本或配置文件。

2. **将文件转换为Unix格式**

   * 使用`dos2unix`实用程序将Windows样式行结尾转换为Unix格式：

     ```bash
     dos2unix <file_name>
     ```

   * 将`<file_name>`替换为引发错误的实际脚本或配置文件。

3. **如果需要，请重复**

   * 如果多个脚本受到影响，请对所有相关的`.sh`文件（例如，安装程序、LCM或JBoss启动脚本）重复转换。

4. **重新运行脚本**

   * 转换后，重新执行脚本以确认问题已得到解决。

将文件转换为Unix (LF)行结尾后，解决了`/bin/sh^M`和`$'\r': command not found`错误，JBoss脚本在Linux上成功执行。
