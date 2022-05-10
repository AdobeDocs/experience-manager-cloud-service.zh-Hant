---
title: 支援的檔案格式和MIME類型
description: 支援的檔案格式和MIME類型 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service]。
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 77cba988368c07438835148d08f1e8cc6e469b7b
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 7%

---

# [!DNL Assets] 支援的檔案格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 支援任何二進位檔案的基本內容管理功能（儲存、線上管理元資料、版本控制、上載和下載等），與其格式無關。 [!DNL Adobe Experience Manager Assets] 支援多種檔案格式，每種產品功能都支援不同格式。

另外， [!DNL Experience Manager Assets] 為生成預覽和格式副本以及提取元資料和文本以進行全文索引提供了擴展支援。 此擴展支援使用 [資產微服務](asset-microservices-configure-and-use.md)。

使用資產微型服務進行資產轉換的亮點包括：

* 鍵 [Adobe檔案格式](#adobe-formats) 由Adobe應用程式和服務生產，包括 [!DNL Adobe Photoshop]。 [!DNL Adobe InDesign]。 [!DNL Adobe Illustrator]。 [!DNL Adobe XD]。 [!DNL Adobe Dimension], [!DNL Adobe Acrobat] 或PDF。
* 鍵 [成像檔案格式](#image-formats)。
* [Camera Raw檔案格式](#camera-raw-formats) 包括佳能、尼康、富士膠片、奧林匹斯和其他製造商(由Adobe Camera Raw提供)。
* 常用 [文檔格式](#document-formats)包括Microsoft辦公室和開放文檔格式。
* 各種視訊 [和音訊](#video-formats)[格式.](#audio-formats)

以下圖例說明了每種格式的支援級別。

| 支援級別 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| * | 請參閱表下的注釋 |
| - | 不適用 |

## Adobe格式 {#adobe-formats}

| 檔案格式 | 縮略圖生成 | 全文提取 | 元資料提取 | 寬/高 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| 拼貼 | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| 思想 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| 原始 | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*對於 [!DNL Adobe InDesign] 檔案(INDD)，格式副本的大小由嵌入在INDD檔案中的預覽確定。 在中配置首選項 [!DNL InDesign] (**[!UICONTROL 首選項>檔案處理>始終將預覽影像與文檔一起保存，預覽大小]**)以嵌入較大格式副本。

## 影像格式 {#image-formats}

| 檔案格式 | 縮略圖生成 | 元資料提取 | 寬/高 | 裁切 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## 3D格式 {#support-3d-formats}

支援以下3D格式。

另請參閱 [在Dynamic Media處理3D資產](/help/assets/dynamic-media/assets-3d.md)。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 訪問控制 | 縮略圖預覽 | 3D預覽 | Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

| 檔案格式 | 縮略圖生成 | 元資料提取 | 寬/高 |
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
| 探地雷達 | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| 脈衝電場 | ✓ | ✓ | ✓ |
| 皇家空軍 | ✓ | ✓ | ✓ |
| 原始 | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## 文檔格式 {#document-formats}

資產管理功能支援的文檔格式如下。

| 檔案格式 | 縮略圖生成 | 全文提取 | 寬/高 | 元資料管理 | [連線資產](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| 原設計製造 | ✓ | ✓ | ✓ | - | - |
| 耗氧潛能 | ✓ | ✓ | ✓ | - | - |
| 耗氧物質 | ✓ | ✓ | ✓ | - | - |
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

## 視頻格式 {#video-formats}

| 檔案格式 | 縮略圖生成 | 元資料提取 | 寬/高 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| 艾維 | ✓ | ✓ | ✓ |
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

## 音頻格式 {#audio-formats}

[!DNL Assets] 作為 [!DNL Cloud Service] 為XMPAIF、ASF、M4A、MP3、WAV和WMA音頻格式提供元資料提取支援。

## 支援的音頻和視頻轉錄輸入格式 {#audio-video-transcription-formats}

* FLV（帶H.264和AAC編解碼器）(.flv)
* MXF(.mxf)
* MPEG2-PS、MPEG2-TS、3GP(.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video(WMV)/ASF(.wmv、.asf)
* AVI（未壓縮的8位/10位）(.avi)
* MP4(.mp4、.m4a、.m4v)
* Microsoft數字錄像(DVR-MS)(.dvr-ms)
* 馬特羅斯卡/WebM(.mkv)
* 波/波(.wav)
* 快速時間(.mov)

## 提示和限制 {#limitations-and-tips}

* 當前，元資料提取的檔案大小限制約為15 GB。 上載超大資產時，有時元資料提取操作會失敗。

## Dynamic Media — 支援的用於轉碼的輸入視頻格式 {#video-dynamic-media-transcoding}

| 視頻檔案副檔名 | 容器 | 推薦的視頻編解碼器 | 不支援的視頻編解碼器 |
| --- | --- | --- | --- |
| 艾維 | A/V交織 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft視頻1(MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| M4V | AppleiTunes | H264/AVC | − |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| MOV,QT | Apple快速時間 | H264/AVC、AppleProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、松下DVCPro、AppleDV(DV25)、ApplePhotoSON、Avid DNxHD、JpegAVD AVR | Apple中級，Apple動畫 |
| MP4 | MPEG-4 | H264/AVC（所有配置檔案） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF? | MXF | Sony XDCAM、MPEG-2、MPEG-4、松下DVCPro | - |
| OGV,OGG | 奧格 | 蒂奧拉，VP3，狄拉克 | - |
| WebM | WebM | GoogleVP8 | - |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft照片(WVP2) |

？此視頻格式尚不支援用於Dynamic Media的互動式視頻或用於Experience Manager Assets的注釋。

## Dynamic Media — 支援的文檔格式 {#document-support-dynamic-media}

| 格式 | 上載（輸入格式） | 建立影像預設（輸出格式） | 預覽動態格式副本 | 提供動態格式副本 | 下載動態格式副本 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF（請參閱下面的注釋） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>對於安全PDF，僅支援上載。

## Dynamic Media — 支援的光柵影像格式 {#image-support-dynamic-media}

| 格式 | 上載（輸入格式） | 建立影像預設（輸出格式） | 預覽動態格式副本 | 提供動態格式副本 | 下載動態格式副本 | 設定支援此格式的類型 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [影像](/help/assets/dynamic-media/image-sets.md)。 [混合介質](/help/assets/dynamic-media/mixed-media-sets.md), [自旋](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)。 [混合介質](/help/assets/dynamic-media/mixed-media-sets.md), [自旋](/help/assets/dynamic-media/spin-sets.md) |
| 皮克 | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)。 [混合介質](/help/assets/dynamic-media/mixed-media-sets.md), [自旋](/help/assets/dynamic-media/spin-sets.md) |
| PSD? | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)。 [混合介質](/help/assets/dynamic-media/mixed-media-sets.md), [自旋](/help/assets/dynamic-media/spin-sets.md) |

？從PSD檔案中提取合併的影像。 它是由 [!DNL Adobe Photoshop] 並包含在PSD檔案中。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

## Dynamic Media — 不支援的光柵影像格式 {#unsupported-raster-image-formats-dm}

以下子類型的光柵影像檔案格式 *不* 支援 [!DNL Dynamic Media]:

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援具有非CMYK、RGB、灰度或點陣圖的色彩空間的PSD檔案。 不支援DuoTone、Lab和索引顏色空間。
* PSD深度大於16的檔案。
* TIFF具有浮點資料的檔案。
* TIFF具有實驗室顏色空間的檔案。

## Dynamic Media — 支援的3D檔案格式 {#support-3d-formats-dynamic-media}

另請參閱 [支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| 格爾布 | 二進位GL傳輸 | 模型/gltf二進位 | 將材料和紋理作為單個資源包括在內。 |
| OBJ | WaveFront 3D對象檔案 | 應用程式/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| 烏茲 | 通用場景描述Zip存檔 | model/vnd.usdz | *僅支援攝入；沒有可用的查看或交互。* USDZ是專有的3D格式，可由Safari或iOS以本機方式查看。 |

>[!MORELIKETHIS]
>
>* [使用資產微服務的資產處理](asset-microservices-overview.md)
>* [支援的檔案格式，用於智慧標籤基於文本的資產](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

