---
title: 支援的檔案格式和MIME型別
description: ' [!DNL Experience Manager Assets] as a [!DNL Cloud Service]支援的檔案格式和MIME型別。'
contentOwner: AG
feature: Asset Management, Renditions
role: User, Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 9%

---

# [!DNL Assets]支援的檔案格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]支援任何二進位檔案的基本內容管理功能 — 儲存、線上管理中繼資料、版本設定、上傳和下載等，不受其格式限制。 [!DNL Adobe Experience Manager Assets]支援多種檔案格式，而且每種產品功能對於不同格式都有不同的支援。

此外，[!DNL Experience Manager Assets]提供延伸支援，可產生預覽和轉譯，以及擷取中繼資料和文字，以編制全文檢索索引。 此延伸支援是使用[資產微服務](asset-microservices-configure-and-use.md)提供。

使用資產微服務的資產轉換重點包括：

* Adobe應用程式和服務產生的金鑰[Adobe檔案格式](#adobe-formats)，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 金鑰[影像檔案格式](#image-formats)。
* [Camera Raw檔案格式](#camera-raw-formats)，適用於各種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商(由Adobe Camera Raw提供)。
* 常見的[檔案格式](#document-formats)，包括Microsoft® Office和Open Document格式。
* [視訊](#video-formats)和[音訊](#audio-formats)格式範圍廣泛。

下列圖例說明每種格式的支援等級。

| 支援等級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| * | 請參閱表格下方的備註 |
| - | 不適用 |

## Adobe格式 {#adobe-formats}

| 檔案格式 | 產生縮圖 | 全文檢索擷取 | 中繼資料擷取 | 寬度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| 拼貼 | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| SBSAR | ✓ | - | ✓ | ✓ |
| 構思 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| 原始 | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*對於[!DNL Adobe InDesign]個檔案(INDD)，轉譯的大小是由內嵌在INDD檔案中的預覽所決定。 在[!DNL InDesign]中設定偏好設定（**[!UICONTROL 偏好設定>檔案處理>一律儲存預覽影像和檔案，預覽大小]**），以便您可以嵌入較大的轉譯。

## 影像格式 {#image-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 | 裁切 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI™ | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## 三維格式 {#support-3d-formats}

支援下列3D格式。

另請參閱[在Dynamic Media中使用3D資產](/help/assets/dynamic-media/assets-3d.md)。

| 格式 | 儲存空間 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media傳遞 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| 物件 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 美元z | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw]格式 {#camera-raw-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| 月 | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| 原始 | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## 檔案格式 {#document-formats}

資產管理功能支援的檔案格式如下。

| 檔案格式 | 產生縮圖 | 全文檢索擷取 | 寬度/高度 | 中繼資料管理 | [連線資產](use-assets-across-connected-assets-instances.md) | 完整檔案預覽 |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ | - |
| ODF | ✓ | ✓ | ✓ | - | - | - |
| ODM | ✓ | ✓ | ✓ | - | - | - |
| ODP | ✓ | ✓ | ✓ | - | - | - |
| ODS | ✓ | ✓ | ✓ | - | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| OFG | ✓ | ✓ | ✓ | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - | - |
| RTF | - | ✓ | - | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - | - |

## 視訊格式 {#video-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 | 預覽 | 輸出 |
| ----------- | -------------------- | ------------------- | ------------ | ------- | ------- |
| 3G2 | - | ✓ | - | - | - |
| 3GP | - | ✓ | - | - | - |
| AVI | ✓ | ✓ | ✓ | ✓ | - |
| DIVX | ✓ | - | ✓ | ✓ | - |
| F4V | ✓ | ✓ | ✓ | ✓ | - |
| FLV | ✓ | ✓ | ✓ | ✓ | - |
| M2T | ✓ | - | ✓ | ✓ | - |
| M2TS | ✓ | - | ✓ | ✓ | - |
| M2V | ✓ | - | ✓ | ✓ | - |
| M4V | ✓ | ✓ | ✓ | ✓ | - |
| MKV | ✓ | - | ✓ | ✓ | - |
| MOV | ✓ | ✓ | ✓ | ✓ | - |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | - |
| MPG | ✓ | ✓ | ✓ | ✓ | - |
| MTS | ✓ | - | ✓ | ✓ | - |
| MXF | ✓ | - | ✓ | ✓ | - |
| OGV | ✓ | - | ✓ | ✓ | - |
| QT | ✓ | - | ✓ | ✓ | - |
| R3D | - | ✓ | ✓ | ✓ | - |
| SWF | ✓ | - | ✓ | ✓ | - |
| WebM | ✓ | - | ✓ | ✓ | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | - |

## 音訊格式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service]提供AIF、ASF、M4A、MP3、WAV和WMA音訊格式的XMP中繼資料擷取支援。

## 支援的音訊和視訊轉譯輸入格式 {#audio-video-transcription-formats}

* FLV （含H.264和AAC轉碼器） (.flv)
* MXF (.mxf)
* MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video (WMV)/ASF (.wmv， .asf)
* AVI （未壓縮8位元/10位元） (.avi)
* MP4 (.mp4， .m4a， .m4v)
* Microsoft®數位視訊錄製(DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳大型資產時，有時中繼資料擷取作業會失敗。

## Dynamic Media — 支援的輸入視訊格式以進行轉碼 {#video-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
| --- | --- | --- | --- |
| AVI | A/V交錯 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft®Video 1 (MS-CRAM) |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF （向量動畫檔案） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate， Apple Animation |
| MP4 | MPEG-4 | H264/AVC （所有設定檔） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF‡案 | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | OGG | Theora， VP3， Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft®畫面(MSS2)、Microsoft®像片故事(WVP2) |

‡目前尚不支援將此視訊格式用於Dynamic Media中的互動式視訊，或用於Experience Manager Assets中的註解。

## Dynamic Media — 支援的檔案格式 {#document-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳遞動態轉譯 | 下載動態轉譯 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF （請參閱下方的「附註」） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>若是安全的PDF，僅支援上傳。

## Dynamic Media — 支援的光柵影像格式 {#image-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳遞動態轉譯 | 下載動態轉譯 | 設定支援此格式的型別 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [影像](/help/assets/dynamic-media/image-sets.md)、[混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)和[迴轉](/help/assets/dynamic-media/spin-sets.md) |
| [EPS](/help/assets/dynamic-media/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)、[混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)和[迴轉](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)、[混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)和[迴轉](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)、[混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)和[迴轉](/help/assets/dynamic-media/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡合併的影像會從PSD檔案中擷取。 它是由[!DNL Adobe Photoshop]產生並包含在PSD檔案中的影像。 視設定而定，合併的影像不一定是實際影像。

## Dynamic Media — 不支援的光柵影像格式 {#unsupported-raster-image-formats-dm}

[!DNL Dynamic Media]不支援下列點陣影像檔案格式的子型別&#x200B;**：

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色彩空間不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* 含有浮點數資料的TIFF檔案。
* 具有Lab色域的TIFF檔案。

## Dynamic Media — 支援的3D檔案格式 {#support-3d-formats-dynamic-media}

另請參閱[支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME型別 | 備註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif | |
| STL | 立體成型 | application/vnd.ms-pki.stl | |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *支援擷取和縮圖產生；尚未支援3D預覽。* USDZ是3D格式，可由Safari或iOS以原生方式檢視。 |

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)。
>* [支援的文字型資產智慧標籤檔案格式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
