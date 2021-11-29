---
title: 支援的檔案格式和MIME類型
description: 支援的檔案格式和MIME類型 [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 6c17b048631a7f61305ec4f0a4f84c4b0577aec0
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 8%

---

# [!DNL Assets] 支援的檔案格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 支援任何二進位檔案的基本內容管理功能（儲存、線上管理元資料、版本設定、上傳和下載等），不受其格式影響。 [!DNL Adobe Experience Manager Assets] 支援多種檔案格式，每種產品功能對不同格式的支援各不相同。

此外， [!DNL Experience Manager Assets] 提供延伸支援，以產生預覽和轉譯，以及擷取中繼資料和文字以建立全文索引。 此延伸支援的提供方式為 [資產微服務](asset-microservices-configure-and-use.md).

使用資產微服務進行資產轉換的重點包括：

* 金鑰 [Adobe檔案格式](#adobe-formats) 由Adobe應用程式和服務產生，包括 [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]，和 [!DNL Adobe Acrobat] 或PDF。
* 金鑰 [影像檔案格式](#image-formats).
* [Camera Raw檔案格式](#camera-raw-formats) 包括佳能、尼康、富士膠片、奧林匹斯和其他製造商(由Adobe Camera Raw提供)。
* 常見 [檔案格式](#document-formats)，包括Microsoft Office和Open Document格式。
* 各種視訊 [和音訊](#video-formats)[格式.](#audio-formats)

下圖說明每種格式的支援級別。

| 支援層級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| * | 請參閱表格下方的備注 |
| - | 不適用 |

## Adobe格式 {#adobe-formats}

| 檔案格式 | 縮圖產生 | 全文擷取 | 中繼資料擷取 | 寬度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| 構想 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*針對 [!DNL Adobe InDesign] 檔案(INDD)，則格式副本的大小由嵌入在INDD檔案中的預覽確定。 在 [!DNL InDesign] (**[!UICONTROL 首選項>檔案處理>始終使用文檔保存預覽影像，預覽大小]**)以內嵌大型轉譯。

## 影像格式 {#image-formats}

| 檔案格式 | 縮圖產生 | 中繼資料擷取 | 寬度/高度 | 裁切 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## 影像格式 [!DNL Dynamic Media] {#image-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳送動態轉譯 | 下載動態轉譯 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PSD協定 | ✓ | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

*從PSD檔案擷取合併的影像。 這是由 [!DNL Adobe Photoshop] 和包含在PSD檔案中。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

下列不支援的點陣影像檔案格式子類型 [!DNL Dynamic Media]:

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援具有CMYK、RGB、灰度或點陣圖以外的顏色空間的PSD檔案。 不支援DuoTone、Lab和索引色空間。
* PSD位深度大於16的檔案。
* TIFF具有浮點資料的檔案。
* TIFF具有Lab色域的檔案。

## 3D格式 {#support-3d-formats}

支援下列3D格式。

另請參閱 [在Dynamic Media中使用3D資產](/help/assets/dynamic-media/assets-3d.md).

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

| 檔案格式 | 縮圖產生 | 中繼資料擷取 | 寬度/高度 |
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
| MOS | ✓ | ✓ | ✓ |
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

資產管理功能支援的文檔格式如下。

| 檔案格式 | 縮圖產生 | 全文擷取 | 寬度/高度 | 中繼資料管理 | [連線資產](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## 文檔格式 [!DNL Dynamic Media] {#document-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳送動態轉譯 | 下載動態轉譯 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |

## 視訊格式 {#video-formats}

| 檔案格式 | 縮圖產生 | 中繼資料擷取 | 寬度/高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## 視訊格式 [!DNL Dynamic Media] 轉碼 {#video-dynamic-media-transcoding}

| 影片副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
| --- | --- | --- | --- |
| AVI | A/V插播 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC, Flix VP6, H263, Sorenson | SWF（向量動畫檔案） |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC、Apple ProRes422 HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple中級，Apple動畫 |
| MP4 | MPEG-4 | H264/AVC（所有配置檔案） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF |  | 媒體交換格式。<br>Apple ProRes422 | - |
| 奧格夫、奧格 | 奧格 | 蒂奧拉，VP3，狄拉克 | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft Screen(MSS2)、Microsoft Photo Story(WVP2) |

## 音訊格式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] 為AIF、ASF、M4A、MP3、WAV和WMA音頻格式提供XMP元資料提取支援。

## 支援的音頻和視頻轉錄輸入格式 {#audio-video-transcription-formats}

* FLV（帶H.264和AAC編解碼器）(.flv)
* MXF(.mxf)
* MPEG2-PS、MPEG2-TS、3GP(.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video(WMV)/ASF(.wmv、.asf)
* AVI（未壓縮8位/10位）(.avi)
* MP4(.mp4、.m4a、.m4v)
* Microsoft數位視訊錄制(DVR-MS)(.dvr-ms)
* 馬特羅斯卡/WebM(.mkv)
* 波/波(.wav)
* QuickTime(.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳非常大型的資產時，有時中繼資料擷取作業會失敗。

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)
>* [支援的檔案格式，適用於文字型資產的智慧標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

