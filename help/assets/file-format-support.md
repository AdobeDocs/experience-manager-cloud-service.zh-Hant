---
title: Experience Manager Assets作為雲端服務支援的檔案格式和MIME類型
description: Experience Manager Assets作為雲端服務支援的檔案格式和MIME類型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b44e6a522b6f2363daa40c6c6f9640ba2fadd35e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 8%

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager雲端服務支援基本的內容管理功能— 儲存、線上管理中繼資料、版本修訂、上傳和下載等等— 任何二進位檔案，不受其格式影響。 Adobe Experience Manager Assets支援多種檔案格式，而每種產品功能都支援不同格式。

此外，Experience Manager Assets還提供延伸支援，可產生預覽和轉譯，並擷取中繼資料和文字以建立全文索引。 此延伸支援是使用資產微 [型服務](asset-microservices-configure-and-use.md)。

使用資產微服務進行資產轉換的重點包括：

* 由Adobe應用程式和服務 [](#adobe-formats) （包括Adobe Photoshop、Adobe InDesign、Adobe Illustrator、Adobe XD、Adobe Dimension和Adobe Acrobat或PDF）所製作的主要Adobe檔案格式。
* 關鍵影 [像檔案格式](#image-formats)。
* [Camera Raw檔案格式](#camera-raw-formats) ，適用於各種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商（採用Adobe Camera Raw）。
* 常用 [檔案格式](#document-formats)，包括Microsoft Office和Open Document格式。
* 各種視訊 [和音訊](#video-formats)[格式.](#audio-formats)

下圖說明支援等級。

| 支援等級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| * | 請參閱表格下方的注釋 |
| - | 不適用 |

## Adobe格式 {#adobe-formats}

| 檔案格式 | 產生縮圖 | 全文擷取 | 中繼資料擷取 | 寬度／高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| 拼貼 | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| 創意 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*對於 [!DNL Adobe InDesign] 檔案(INDD)，轉譯的大小由內嵌於INDD檔案中的預覽決定。 在(「偏好設定」>「 [!DNL InDesign] 檔案處理」>「永遠儲存預覽影像與檔案」、「預覽大小」****)中設定偏好設定，以內嵌較大的轉譯。

## 影像格式 {#image-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 | 裁切 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## 影像格式 [!DNL Dynamic Media] {#image-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 提供動態轉譯 | 下載動態轉譯 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD‡ | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

‡合併的影像是從PSD檔案擷取。 它是由PSD檔案產生並 [!DNL Adobe Photoshop] 包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

下列不支援的點陣影像檔案格式子類型 [!DNL Dynamic Media]:

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色域不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* 具有浮點資料的TIFF檔案。
* 具有Lab色域的TIFF檔案。

## 支援3D格式 {#support-3d-formats}

支援下列3D格式清單。

請參 [閱在動態媒體中使用3D資產。](/help/assets/dynamic-media/assets-3d.md)

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |  |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ |  | ✓ |  |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 |
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
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## 檔案格式 {#document-formats}

資產管理功能支援的檔案格式如下。

| 檔案格式 | 產生縮圖 | 全文擷取 | 寬度／高度 | 中繼資料管理 | [連線資產](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## 檔案格式 [!DNL Dynamic Media] {#document-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 提供動態轉譯 | 下載動態轉譯 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## 視訊格式 {#video-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
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
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## 轉碼中的視 [!DNL Dynamic Media] 訊格式 {#video-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC（所有描述檔） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHDAvid AVR | Apple Intemiderate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft Photo Story(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V間隔 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | 西奧拉， VP3，狄拉克 |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | 馬特羅斯卡 | H264/AVC |  |
| R3D、RM | 紅色原始影片 | MJPEG 2000 |  |
| RAM、RM | RealVideo | 不支援 | 實數G2(RV20)、實數8(RV30)、實數10(RV40) |
| FLAC | 原生Flac | 免費無損音訊轉碼器 |  |
| MJ2 | Motion JPEG 2000 | 動態JPEG 2000編碼解碼器 |  |

## 音訊格式 {#audio-formats}

Assets as a Cloud Services為AIF、ASF、M4A、MP3、WAV和WMA音訊格式提供XMP中繼資料擷取支援。

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)

