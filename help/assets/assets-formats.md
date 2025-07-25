---
title: 支持的文件格式和MIME类型
description: ' [!DNL Assets] 和 [!DNL Dynamic Media] 支持的文件格式和MIME类型以及每种格式支持的功能。'
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: e48f7950-1b6e-4896-8abc-523552e42ed9
source-git-commit: 2a328b703d691a23ca46a4171624a4184a8392dd
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 12%

---

# [!DNL Adobe Experience Manager Assets]中支持的格式 {#assets-supported-formats}

[!DNL Experience Manager Assets]支持广泛的文件格式，并且每种功能对于不同的MIME类型都有不同的支持。 要将[!DNL Assets]与其他符合标准的数字资产管理(DAM)解决方案和桌面软件集成，请使用Adobe的[!DNL Extensible Metadata Platform] (XMP)。

使用图例了解支持级别。

| 支持级别 | 描述 |
| :-----------: | ------------------------------ |
| ✓ | 支持 |
| &#42; | 支持附加功能 |
| − | 不适用 |

## [!DNL Experience Manager]中支持的栅格图像格式 {#supported-raster-image-formats}

[!DNL Assets]中支持的光栅图像格式为：

| 格式化 | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | 编辑 | 元数据写回 | 见解 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡将从PSD文件中提取合并的图像。 它是由Adobe Photoshop生成的图像，包含在PSD文件中。 根据设置，合并的图像不一定是实际图像。

除上述信息外，请考虑以下事项：

* 对EPS文件的支持仅适用于光栅图像。 例如，默认情况下不支持生成EPS矢量图像的缩略图。 要添加支持，请[配置ImageMagick](best-practices-for-imagemagick.md)。 要集成第三方工具以启用其他功能，请参阅[基于命令行的媒体处理程序](media-handlers.md#command-line-based-media-handler)。

* 元数据写回在添加到`NComm`处理程序中时适用于PSB文件格式。

* 对于EPS文件，PostScript Document Structuring Convention (PS-Adobe)版本3.0或更高版本支持元数据写回。

## 支持的3D格式 {#support-3d-formats}

支持以下3D格式列表。

另请参阅[在Dynamic Media中使用3D资产。](/help/assets/assets-3d.md)

| 格式化 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| 对象 | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| 美元z | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## 支持的PDF光栅器库 {#supported-pdf-rasterizer-library}

Adobe PDF光栅器库为大型且内容密集的[!DNL Adobe Illustrator]和PDF文件生成高质量的缩略图和预览。 Adobe建议将PDF光栅器库用于：

* 要处理的资源密集型内容密集型AI/PDF文件。
* AI/PDF文件，默认情况下不为其生成缩略图。
* 具有Pantone匹配系统(PMS)颜色的AI文件。

请参阅[使用PDF光栅器](aem-pdf-rasterizer.md)。

## 支持的图像转码库 {#supported-image-transcoding-library}

Adobe图像转码库是一种图像处理解决方案，它执行核心图像处理功能，如编码、转码、重新取样和调整大小。

图像转码库支持JPG/JPEG、PNG（8位和16位）、GIF、BMP、TIFF/压缩的TIFF(32位TIFF文件和PTIFF文件除外)、ICO和ICN MIME类型。

请参阅[图像转码库](imaging-transcoding-library.md)。

## 支持的Camera Raw {#supported-camera-raw}

[!DNL Adobe Camera Raw]库允许[!DNL Assets]摄取原始图像。 请参阅[Camera Raw支持](camera-raw.md)。

## 支持的[!DNL Assets]文档格式 {#supported-document-formats}

资产管理功能支持的文档格式如下：

| 格式化 | 存储 | [元数据管理](metadata.md) | 全文<br>提取 | [元数据提取](metadata.md) | 缩略图<br>生成 | [子资产提取](managing-linked-subassets.md) | [元数据写回](xmp-writeback.md) | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| ePub | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## 支持的多媒体格式 {#supported-multimedia-formats}

| | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | FFmpeg转码 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## 支持的存档格式 {#supported-archive-formats}

下表介绍了支持的存档格式以及常用DAM工作流的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media 投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 其他支持的格式 {#other-supported-formats}

下面介绍了几种特定文件格式下常用DAM功能的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media 投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（使用自己的投放域配置时） | − | − | − | − | − | ✓ |

>[!NOTE]
>
>上传和分发JavaScript文件可能安全，也可能不安全。 如有必要，您可以使用叠加来阻止用户上传JS文件。

## 支持的MIME类型 {#supported-mime-types}

默认情况下，[!DNL Experience Manager]使用文件扩展名检测文件类型。 [!DNL Experience Manager]可以从文件的内容中检测它。 对于后者，在[!UICONTROL &#x200B; Web控制台的]Day CQ DAM Mime类型服务[!UICONTROL 中选择]从内容中检测MIME[!DNL Experience Manager]选项。

在CRXDE Lite中`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`处提供了支持的MIME类型列表。

| 文件扩展名 | MIME类型/ Internet媒体类型 | 默认jobParam值 | 允许的jobParam值 |
|---|---|---|---|
| 图像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 默认jobParam适用于所有图像MIME类型资源。<ul><li>[挖空背景选项](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html?lang=zh-Hans)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html?lang=zh-Hans)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html?lang=zh-Hans)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html?lang=zh-Hans)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html?lang=zh-Hans)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html?lang=zh-Hans)</li><li>[电子邮件设置](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html?lang=zh-Hans)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html?lang=zh-Hans)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html?lang=zh-Hans)</li></ul> |
| 3G2 | video/3gpp2 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| 3GP | video/3gpp | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| 人工智能 | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=zh-Hans)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=zh-Hans)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| BMP | image/bmp | | |
| CSS | 文本/CSS | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| M4V | video/x-m4v | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| MOV | video/quicktime | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| MPEG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| MPG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| OTF | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html?lang=zh-Hans) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=zh-Hans)</li><li>[illustratorOptions] (https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=zh-Hans</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html?lang=zh-Hans)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html?lang=zh-Hans)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF / TIFF | image/tiff | | |
| 测控 | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | video/dvd | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=zh-Hans) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media — 支持的用于转码的输入视频格式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|---|---|---|---|
| AVI | A/V交错 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft®视频1(MS-CRAM) |
| FLV， F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV， QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple中级，Apple动画 |
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | Ogg | 狄拉克副总裁Theora | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft® Screen (MSS2)、Microsoft® Photo Story (WVP2) |

‡尚不支持将此视频格式与Dynamic Media中的交互式视频一起使用，也不支持将其与Experience Manager Assets中的批注一起使用。

## Dynamic Media — 支持的文档格式 {#supported-document-formats-dynamic-media}

| 格式化 | 上传<br> （输入格式） | 创建<br>图像<br>预设<br>（输出格式） | 预览<br>动态<br>呈现版本 | 投放<br>动态<br>演绎版 | 下载<br>动态<br>呈现版本 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)（请参阅下面的注释） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>对于安全PDF，仅支持上传。

除了上述功能外，请考虑以下事项：

* 要使用Dynamic Media为PDF文件生成动态演绎版，请参阅[Adobe Illustrator (AI)、Postscript (EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media预览和生成AI文件的动态演绎版，请参阅[Adobe Illustrator (AI)、Postscript (EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media为INDD文件生成动态演绎版，请参阅[InDesign (INDD)文件格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## Dynamic Media — 支持的栅格图像格式 {#supported-raster-image-formats-dynamic-media}

| 格式化 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 投放动态演绎版 | 下载动态演绎版 | 设置支持此格式的类型 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [图像](/help/assets/image-sets.md)、[混合媒体](/help/assets/mixed-media-sets.md)和[旋转](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/image-sets.md)、[混合媒体](/help/assets/mixed-media-sets.md)和[旋转](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/image-sets.md)、[混合媒体](/help/assets/mixed-media-sets.md)和[旋转](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/image-sets.md)、[混合媒体](/help/assets/mixed-media-sets.md)和[旋转](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡将从PSD文件中提取合并的图像。 它是由Adobe Photoshop生成的图像，包含在PSD文件中。 根据设置，合并的图像不一定是实际图像。

* 对EPS文件的支持仅适用于光栅图像。 例如，默认情况下不支持生成EPS矢量图像的缩略图。 要添加支持，请[配置ImageMagick](best-practices-for-imagemagick.md)。 要集成第三方工具以启用其他功能，请参阅[基于命令行的媒体处理程序](media-handlers.md#command-line-based-media-handler)。

* 要使用[!DNL Dynamic Media]预览和生成EPS文件的动态演绎版，请参阅[Adobe Illustrator (AI)、Postscript (EPS)和PDF文件格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 对于EPS文件，PostScript Document Structuring Convention (PS-Adobe)版本3.0或更高版本支持元数据写回。

## Dynamic Media — 不支持的栅格图像格式 {#unsupported-image-formats-dynamic-media}

以下列表介绍了Dynamic Media中不支持&#x200B;*的*&#x200B;光栅图像文件格式的子类型。

* IDAT区块大小大于100 MB的PNG文件。
* psb文件。
* 不支持色彩空间不是CMYK、RGB、灰度或位图的PSD文件。 不支持DuoTone、Lab和Indexed色彩空间。
* 位深度大于16的PSD文件。
* 包含浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media — 支持的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支持以下3D格式。

另请参阅[在Dynamic Media中使用3D资产](/help/assets/assets-3d.md)。

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取；不可查看或交互。* USDZ是一种专有的3D格式，可供Safari和iOS设备本机查看。 |

>[!MORELIKETHIS]
>
>* [启用基于MIME类型的Assets和Dynamic Media Classic上载作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [为上载作业参数支持配置基于MIME类型的](config-dynamic.md)。
