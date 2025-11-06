---
title: 支援的檔案格式
description: ' [!DNL Assets view] 各種使用案例支援的檔案格式'
role: User, Leader, Admin, Developer
contentOwner: AG
exl-id: 5936ace2-318e-4888-9ad4-23e6f6bfb857
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# [!DNL Assets view] 的檔案格式支援 {#file-format-support}

[!DNL Assets view] 支援各式各樣的檔案格式，而且每種功能對於不同的檔案類型都有不同的支援。

* ![影像檔案類型圖示](assets/image-icon.svg) 影像：JPG、PNG、GIF、TIFF 和其他
* ![creative cloudtype 圖示](assets/creative-cloud-files.svg) Creative Cloud 檔案：PSD、PSB、AI 和 INDD
* ![相機類型圖示](assets/camera-icon.svg) Camera RAW 檔案：CR2/CR3、NEF、SRW/SRF 和其他
* ![文字檔案類型圖示](assets/document-icon.svg) 文件：DOCX、PDF、PPTX 和 XLSX
* ![影片檔案類型圖示](assets/video-icon.svg) 影片：MP4

[!DNL Assets view] 支援任何二進位檔案格式和基本服務，例如儲存、上傳、複製、移動、刪除和新增中繼資料。

[!DNL Assets view] 也支援各式各樣領先相機製造商的 Camera RAW 檔案 (採用 Adobe Camera Raw 技術)，包括 Canon (CR2/CR3)、Nikon (NEF)、Sony (SRW/SRF)、Fujifilm (RAF)、Olympus (ORF) 和其他廠商。

各種檔案類型對於使用案例和功能有不同程度的支援，如下所述。請參閱圖例以了解支援程度。

| 支援程度 | 說明 |
|-------------------|-------------------------|
| ✓ | 支援 |
| ✓‡ | 有條件支援 |
| − | 不適用 |

## 新增、上傳和檢視資產 {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| 資產類型 | [瀏覽](/help/assets/navigate-assets-view.md) | 複製 | [上傳](/help/assets/add-delete-assets-view.md) | 建立 | [刪除](/help/assets/add-delete-assets-view.md#delete-assets) | 詳細資料 | 影像縮放 | [最近檢視的項目](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| 點陣圖 | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| RAW 檔案 | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| 資料夾 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| MP4 影片 | ✓ | ✓ | ✓ | − | ✓ | ✓‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD、PSB、AI 和 INDD | ✓ | ✓ | ✓ | − | ✓ | ✓‡ | − | ✓ |
| 其他二進位檔案 | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## 搜尋、使用和編輯資產 {#support-to-search-use-edit}

| 資產類型 | [下載](/help/assets/manage-organize-assets-view.md#download) | 拖放 | [影像編輯器](/help/assets/edit-images-assets-view.md) | [搜尋](/help/assets/search-assets-view.md) | [智慧標記](/help/assets/metadata-assets-view.md#tags) | [重新命名](/help/assets/manage-organize-assets-view.md) | [版本](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| 點陣圖 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW 檔案 | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| 資料夾 | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| 影片 | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| CC Libraries | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD 和 PSB | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| AI 和 INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| 其他二進位檔案 | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## 檢閱資產和共同作業 {#support-to-review-collaborate}

| 資產類型 | 注釋 | 評論 | 建立任務和檢閱 |
|---------------|----------|----------|-------------------------|
| 點陣圖 | ✓ | ✓ | ✓ |
| RAW 檔案 | ✓ | ✓ | ✓ |
| 資料夾 | − | − | − |
| 影片 | − | ✓ | ✓ |
| CC Libraries | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD、PSB、AI 和 INDD | − | ✓ | ✓ |
| 其他二進位檔案 | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## 其他資產管理任務 {#support-to-manage-assets}

| 資產類型 | [中繼資料](/help/assets/metadata-assets-view.md) | [轉譯](/help/assets/add-delete-assets-view.md#renditions) | [垃圾桶](/help/assets/add-delete-assets-view.md#delete-assets) | 複製 | 移動 |
|---------------|-------------------|------------|----------|----------|----------|
| 點陣圖 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW 檔案 | ✓ | ✓ | ✓ | ✓ | ✓ |
| 資料夾 | ✓ | − | ✓ | ✓ | ✓ |
| 影片 | ✓ | − | ✓ | ✓ | ✓ |
| CC Libraries | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| AI 和 INDD | ✓ | − | ✓ | ✓ | ✓ |
| PSD 和 PSB | ✓ | ✓ | ✓ | ✓ | ✓ |
| 其他二進位檔案 | ✓ | − | ✓ | ✓ | ✓ |

[!DNL Adobe Asset Link] 的使用者可以從支援的 [!DNL Adobe Creative Cloud] 桌面應用程式上傳和簽入 (上傳新版本) 檔案到 [!DNL Assets view] 存放庫。

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD, PSB           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## 後續步驟 {#next-steps}

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/zh-hant?support-solution=General#support)
