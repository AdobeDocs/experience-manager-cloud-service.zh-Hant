---
title: 支援的檔案格式和MIME類型
description: ' [!DNL Experience Manager Assets] 支援的檔案格式和MIME類型為a [!DNL Cloud Service]。'
contentOwner: AG
feature: 資產管理，轉譯
role: Business Practitioner,Administrator
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 8%

---

# [!DNL Assets] 支援的檔案格式  {#supported-file-formats}

[!DNL Adobe Experience Manager] 支援基 [!DNL Cloud Service] 本的內容管理功能— 儲存、線上管理中繼資料、版本修訂、上傳和下載等等— 任何二進位檔案，不受其格式影響。[!DNL Adobe Experience Manager Assets] 支援多種檔案格式，而每種產品功能都支援不同格式。

此外，[!DNL Experience Manager Assets]還提供延伸支援，以產生預覽和轉譯，並擷取中繼資料和文字以進行全文索引。 此延伸支援是使用[asset microservices](asset-microservices-configure-and-use.md)提供。

使用資產微服務進行資產轉換的重點包括：

* 關鍵[Adobe檔案格式](#adobe-formats)由Adobe應用程式和服務產生，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 鍵[映像檔案格式](#image-formats)。
* [Camera Raw檔](#camera-raw-formats) 案格式，適用於各種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商(採用Adobe Camera Raw)。
* 常見的[檔案格式](#document-formats)，包括Microsoft Office和Open Document格式。
* 各種視訊 [和音訊](#video-formats)[格式.](#audio-formats)

下圖說明每種格式的支援等級。

| 支援等級 | 說明 |
| ------------- | --------------------------- |
| ý | 支援 |
| * | 請參閱表格下方的注釋 |
| - | 不適用 |

## Adobe格式{#adobe-formats}

| 檔案格式 | 產生縮圖 | 全文擷取 | 中繼資料擷取 | 寬度／高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ý | - | ý | ý |
| 拼貼 | - | - | ý | - |
| DN | ý | - | ý | ý |
| 創意 | - | - | ý | - |
| INDD | ý | - | ý | ý * |
| INDT | - | - | ý | - |
| PDF | ý | ý | ý | ý |
| PROTO | - | - | ý | - |
| PSB | ý | - | ý | ý |
| PSD | ý | - | ý | ý |
| XD | ý | - | ý | ý |

\*對於[!DNL Adobe InDesign]檔案(INDD)，轉譯的大小由INDD檔案中內嵌的預覽決定。 在[!DNL InDesign](**[!UICONTROL 「偏好設定」>「檔案處理」>「永遠儲存預覽影像與檔案」、「預覽大小」中設定偏好設定，以內嵌較大的轉譯。]**

## 影像格式{#image-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 | 裁切 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ý | - | ý | ý |
| EPS | - | ý | - | - |
| GIF | ý | ý | ý | ý |
| JPEG | ý | ý | ý | ý |
| PNG | ý | ý | ý | ý |
| RGB | ý | ý | ý | ý |
| RGBA | ý | ý | ý | ý |
| SGI | ý | ý | ý | ý |
| SVG | ý | - | ý | ý |
| TIFF | ý | ý | ý | - |

## [!DNL Dynamic Media] {#image-support-dynamic-media}中的影像格式

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 提供動態轉譯 | 下載動態轉譯 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ý | - | - | - | - |
| EPS | ý | ý | ý | ý | ý |
| GIF | ý | ý | ý | ý | ý |
| JPEG | ý | ý | ý | ý | ý |
| PICT | ý | - | - | - | - |
| PNG | ý | ý | ý | ý | ý |
| PSD   ‡ | ý | - | - | - | - |
| TIFF | ý | ý | ý | ý | ý |

‡合併的影像是從PSD檔案擷取。 它是由[!DNL Adobe Photoshop]產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

[!DNL Dynamic Media]中不支援的點陣影像檔案格式的下列子類型：

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色域不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* 具有浮點資料的TIFF檔案。
* 具有Lab色域的TIFF檔案。

## 3D格式{#support-3d-formats}

支援下列3D格式。

另請參閱[在Dynamic Media使用3D資產](/help/assets/dynamic-media/assets-3d.md)。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ý | ý | ý | - | ý | ý | - | - |
| gLB | ý | ý | ý | ý | ý | - | ý | ý |
| gLTF | ý | ý | ý | - | ý | - | ý | - |
| OBJ | ý | ý | ý | ý | ý | - | ý | ý |
| STL | ý | ý | ý | ý | ý | - | ý | ý |
| USDz | ý | ý | ý | ý | ý | - | - | ý |

## [!DNL Camera RAW] 格式  {#camera-raw-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ý | ý | ý |
| ARW | ý | ý | ý |
| CR2 | ý | ý | ý |
| CR3 | ý | ý | ý |
| CRW | ý | ý | ý |
| DCR | ý | ý | ý |
| DNG | ý | ý | ý |
| ERF | ý | ý | ý |
| FFF | ý | ý | ý |
| GPR | ý | ý | ý |
| IIQ | ý | ý | ý |
| KDC | ý | ý | ý |
| MEF | ý | ý | ý |
| MFW | ý | ý | ý |
| MOS | ý | ý | ý |
| MRW | ý | ý | ý |
| NEF | ý | ý | ý |
| NRW | ý | ý | ý |
| ORF | ý | ý | ý |
| PEF | ý | ý | ý |
| RAF | ý | ý | ý |
| RAW | ý | ý | ý |
| RW2 | ý | ý | ý |
| RWL | ý | ý | ý |
| SRF | ý | ý | ý |
| SRW | ý | ý | ý |
| X3F | ý | ý | ý |

## 文檔格式{#document-formats}

資產管理功能支援的檔案格式如下。

| 檔案格式 | 產生縮圖 | 全文擷取 | 寬度／高度 | 中繼資料管理 | [連線資產](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ý | ý |
| DOCX | ý | ý | ý | ý | ý |
| EPUB | - | ý | - | - | - |
| HTML | - | ý | - | ý | ý |
| ODF | ý | ý | ý | - | - |
| ODM | ý | ý | ý | - | - |
| ODP | ý | ý | ý | - | - |
| ODS | ý | ý | ý | - | - |
| ODT | ý | ý | ý | ý | ý |
| OFG | ý | ý | ý | - | - |
| PDF | ý | ý | ý | ý | ý |
| PPT | - | - | - | ý | ý |
| PPTX | ý | ý | ý | ý | ý |
| PS | - | - | ý | - | - |
| RTF | - | ý | - | ý | ý |
| TXT | - | ý | - | ý | ý |
| XLS | - | - | - | ý | ý |
| XLSX | ý | ý | ý | ý | ý |
| XML | - | ý | - | - | - |

## [!DNL Dynamic Media] {#document-support-dynamic-media}中的檔案格式

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 提供動態轉譯 | 下載動態轉譯 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ý | - | - | - | - |
| INDD | ý | - | - | - | - |
| PDF | ý | ý | ý | ý | ý |

## 視訊格式{#video-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ý | - |
| 3GP | - | ý | - |
| AVI | ý | ý | ý |
| DIVX | ý | - | ý |
| F4V | ý | ý | ý |
| FLV | ý | ý | ý |
| M2T | ý | - | ý |
| M2TS | ý | - | ý |
| M2V | ý | - | ý |
| M4V | ý | ý | ý |
| MKV | ý | - | ý |
| MOV | ý | ý | ý |
| MP4 | ý | ý | ý |
| MPEG | ý | ý | ý |
| MPG | ý | ý | ý |
| MTS | ý | - | ý |
| MXF | ý | - | ý |
| OGV | ý | - | ý |
| QT | ý | - | ý |
| R3D | - | ý | ý |
| SWF | ý | - | ý |
| WebM | ý | - | ý |
| WMV | ý | ý | ý |

## 用於轉碼{#video-dynamic-media-transcoding}的[!DNL Dynamic Media]中的視頻格式

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC（所有描述檔） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHDAvid AVR | Apple Intemiderate、Apple Animation |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft Photo Story(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V間隔 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | 西奧拉， VP3，狄拉克 | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| R3D、RM | 紅色原始影片 | MJPEG 2000 | - |
| RAM、RM | RealVideo | 不支援 | 實數G2(RV20)、實數8(RV30)、實數10(RV40) |
| FLAC | 原生Flac | 免費無損音訊轉碼器 | - |
| MJ2 | Motion JPEG 2000 | 動態JPEG 2000編碼解碼器 | - |

## 音訊格式{#audio-formats}

[!DNL Assets] as  [!DNL Cloud Service] XMP provides metadata recustration support for AIF, ASF, M4A, MP3, WAV, and WMA audio formats.

## 提示和限制{#limitations-and-tips}

* 目前，中繼資料擷取的檔案大小限制約為10 GB。 上傳超大型資產時，中繼資料擷取作業有時候會失敗。

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)
>* [支援的檔案格式，以智慧標籤文字資產](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

