---
title: 支援的檔案格式和MIME類型
description: ' [!DNL Experience Manager Assets] as a [!DNL Cloud Service]支援的檔案格式和MIME類型。'
contentOwner: AG
feature: 資產管理，轉譯
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 4b7dc19d691e8077600f56ce57dc72749f157234
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 8%

---

# [!DNL Assets] 支援的檔案格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a支 [!DNL Cloud Service] 援任何二進位檔案的基本內容管理功能（儲存、線上管理元資料、版本設定、上傳和下載等），不受其格式影響。[!DNL Adobe Experience Manager Assets] 支援多種檔案格式，每種產品功能對不同格式的支援各不相同。

此外，[!DNL Experience Manager Assets]還提供擴展支援，用於生成預覽和格式副本，以及提取元資料和文本以進行全文索引。 此擴展支援使用[資產微服務](asset-microservices-configure-and-use.md)提供。

使用資產微服務進行資產轉換的重點包括：

* 鍵[Adobe檔案格式](#adobe-formats)由Adobe應用程式和服務產生，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 索引鍵[影像檔案格式](#image-formats)。
* [Camera Raw的](#camera-raw-formats) 檔案格式，適用於多種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商(由Adobe Camera Raw提供技術支援)。
* 常見[文檔格式](#document-formats)，包括Microsoft Office和Open Document格式。
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

\*對於[!DNL Adobe InDesign]檔案(INDD)，格式副本的大小由INDD檔案中嵌入的預覽確定。 在[!DNL InDesign]（**[!UICONTROL 首選項>檔案處理>始終使用文檔保存預覽影像，預覽大小]**）中配置首選項以嵌入較大的格式副本。

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

## [!DNL Dynamic Media]中的影像格式 {#image-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳送動態轉譯 | 下載動態轉譯 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PSD   * | ✓ | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

*從PSD檔案擷取合併的影像。 它是由[!DNL Adobe Photoshop]生成並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

[!DNL Dynamic Media]中不支援的光柵影像檔案格式的以下子類型：

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援使用CMYK、RGB、灰度或點陣圖以外的顏色空間的PSD檔案。 不支援DuoTone、Lab和索引色空間。
* 位深度大於16的PSD檔案。
* 具有浮點資料的TIFF檔案。
* 具有Lab色域的TIFF檔案。

## 3D格式 {#support-3d-formats}

支援下列3D格式。

另請參閱[在Dynamic Media中使用3D資產](/help/assets/dynamic-media/assets-3d.md)。

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
| EPUB | - | ✓ | - | - | - |
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
| TXT | - | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## [!DNL Dynamic Media]中的文檔格式 {#document-support-dynamic-media}

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

## 用於轉碼的[!DNL Dynamic Media]中的視頻格式 {#video-dynamic-media-transcoding}

| 影片副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC（所有配置檔案） | - |
| MOV, QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Meditrate,Apple動畫 |
| FLV、F4V | AdobeFlash | H264/AVC, Flix VP6, H263, Sorenson | SWF（向量動畫檔案） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft照片(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V插播 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| 奧格夫、奧格 | 奧格 | 蒂奧拉，VP3，狄拉克 | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、松下DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| R3D、RM | 紅色原始視頻 | MJPEG 2000 | - |
| RAM、RM | RealVideo | 不支援 | Real G2(RV20)、Real 8(RV30)、Real 10(RV40) |
| FLAC | 原生片段 | 免費無損音頻編解碼器 | - |
| MJ2 | 動作JPEG 2000 | 運動JPEG 2000編解碼器 | - |

## 音訊格式 {#audio-formats}

[!DNL Assets] as a提 [!DNL Cloud Service] 供XMP中繼資料擷取支援，以支援AIF、ASF、M4A、MP3、WAV和WMA音訊格式。

## 提示和限制 {#limitations-and-tips}

* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳超大型資產時，有時中繼資料擷取作業會失敗。

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)
* [支援的檔案格式，適用於文字型資產的智慧標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

