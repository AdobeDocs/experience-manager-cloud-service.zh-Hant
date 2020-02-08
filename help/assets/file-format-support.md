---
title: Experience Manager Assets作為雲端服務支援的檔案格式和MIME類型
description: Experience Manager Assets作為雲端服務支援的檔案格式和MIME類型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# 資產支援的檔案格式 {#supported-file-formats}

Adobe Experience manager作為雲端服務，支援任何二進位檔案的基本內容管理功能——儲存、線上管理中繼資料、版本修訂、上傳和下載等，不受檔案格式限制。 此外，對於常用的檔案格式（例如影像、Adobe專有、檔案和視訊），它提供延伸支援，以產生預覽和轉譯，並擷取中繼資料和文字以進行全文索引。 此延伸支援是使用資產微 [型服務](asset-microservices-configure-and-use.md)。

具備延伸支援的檔案格式重點包括：

* 由Adobe應用程式和服務 [](#adobe-formats) （包括Adobe Photoshop、InDesign、Illustrator、XD、Dimension和Acrobat / PDF）所製作的主要Adobe檔案格式。
* 關鍵影 [像檔案格式](#image-formats)
* [Camera Raw檔案格式](#camera-raw-formats) ，適用於多種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商（採用Adobe Camera Raw）
* 常用 [檔案格式](#document-formats)，包括 [Microsoft Office](#microsoft-office-formats) (Word、Excel、PowerPoint)和 [Open Document](#opendocument-formats) 格式
* 各種視訊 [和音訊](#video-formats)[格式](#audio-formats)

## 詳細支援資訊的圖例 {#legend-for-detailed-support-information}

以下圖例說明功能的支援等級：

| 支援等級 | 說明 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 支援 |
| * | 請參閱表格下方的注釋 |
| - | 不適用 |

支援表的列提供以下資訊：

| 欄 | 說明 |
| ------------ | --------------------------------------------------------------- |
| 格式 | 資產原始二進位檔的檔案格式（副檔名） |
| GIF | 產生轉譯的GIF格式 |
| JPEG | 產生轉譯的JPEG格式 |
| PNG | 產生轉譯的PNG格式 |
| XMP | 從原始二進位元資料擷取中繼資料 |
| TXT | 從檔案擷取文字以建立索引 |
| 寬度／高度 | 支援定義轉譯的寬度和高度（像素） |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Adobe格式 {#adobe-formats}

| 檔案格式 | GIF | JPEG | PNG | TXT | XMP | 寬度／高度 |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| 拼貼 | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| 創意 | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\*對於INDD（InDesign檔案），轉譯的大小由內嵌於INDD檔案中的預覽決定。 在InDesign中設定偏好設定(「偏&#x200B;**[!UICONTROL 好設定」>「檔案處理」>「永遠儲存預覽影像與檔案、預覽大小」]**)，以內嵌較大的轉譯。

## 影像格式 {#image-formats}

| 檔案格式 | GIF | JPEG | PNG | XMP | 寬度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Camera RAW格式 {#camera-raw-formats}

| 檔案格式 | GIF | JPEG | PNG | XMP | 寬度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

## 檔案格式 {#document-formats}

| 檔案格式 | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| 文字 | ✓ | - |
| XML | ✓ | - |

## Microsoft office格式 {#microsoft-office-formats}

| 檔案格式 | GIF | JPEG | PNG | 文字 | 寬度／高度 |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## OpenDocument格式 {#opendocument-formats}

| 檔案格式 | GIF | JPEG | PNG | 文字 | 高度 |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## 視訊格式 {#video-formats}

| 檔案格式 | GIF | JPEG | PNG | XMP | 寬度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

## 音訊格式 {#audio-formats}

Assets as a Cloud Service提供XMP支援下列音訊格式：AIF、ASF、M4A、MP3、WAV和WMA。

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)

