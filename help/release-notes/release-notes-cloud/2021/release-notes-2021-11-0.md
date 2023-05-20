---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版發行說明。'
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 58%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本期(2021.11.0)是2021年12月16日。
以下版本(2022.1.0)是2022年2月3日。

## 發行影片 {#release-video}

看看 [2021年12月發佈概述](https://video.tv.adobe.com/v/339278) 視頻，瞭解2021.11.0版（2021年11月）中添加的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* Dynamic MediaImage Smart Crop and Swatch現在由Sensei最新的服務提供支援，這些服務生產改良的作物和色板。 此外，已啟動增強，以生成不同的作物內容，對於相同的長寬比，但跨不同的解析度。 此外，如果「影像配置檔案」中的寬度和高度沒有變化，則在重新處理時將保留任何手動編輯。

### 中的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

* [!DNL Dynamic Media]  — 現在，您可以使AEM用Dynamic Media介面配置常規設定和發佈設定，而不必通過Dynamic Media Classic案頭應用程式。

* [!DNL Dynamic Media] 現在支援MXF視頻的接收、預覽、播放和發佈。 尚不支援MXF視頻的注釋和可購物視頻。

* 在配置遠程DAM和站點部署之間的連接後，遠程DAM上的資產可在站點部署中使用。 您現在可以執行 [更新、刪除、更名和移動操作](/help/assets/use-assets-across-connected-assets-instances.md) 資料夾。 這些更新在站點部署中自動可用，但有一些延遲。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

* **記錄文檔的自定義字型和使用Communications API建立的PDF文檔**:現在，您可以在使用Communications API生成的PDF文檔中使用品牌批准的字型，以符合您的組織要求。

* **Forms門戶**:您可以使用 [Forms門戶](/help/forms/configure-forms-portal.md) 列出已發佈的自適應表單。 它可幫助站點訪問者發現所有可用表格。 此外，訪問者可以使用表單門戶來保存和訪問自適應表單的草稿，並查看已提交自適應表單的PDF版本。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 基於Commerce可擴展的Peregrine元件的擴展myAccount元件

![擴展的myAccount元件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可以使用其他建議類型建立臨時商務產品Recommendations

* 在店面中支援禮品AEM卡

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.11.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 發行日期是 2021 年 11 月 04 日。下一個版本計畫於 2021 年 12 月 09 日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以善用新的前端管道以加速的方式專門部署前端計劃碼。 請參閱 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)來了解更多資訊。

   >[!IMPORTANT]
   >您必須處於版AEM本 `2021.10.5933.20211012T154732Z` 或更高版本，以利用新的前端管道。

* 透過以更有效的方式執行計劃碼分析來顯著減少計劃碼品質管道期限，而不需要建置整個 AEM 影像。此變更會在發佈後的未來幾週內逐步展開。

* Git 認可識別碼現在會顯示在管道執行詳細資訊中，如此將更易追蹤產生的計劃碼。

* 計劃建立現在可以透過公開顯示的 API 獲得。

* 環境建立現在可以透過公開顯示的 API 獲得。

* `x-request-id` 回應標題現可於 [www.adobe.io](https://www.adobe.io/) 網站上的 API Playground 中看到。此標題在提交客戶服務問題以進行故障排除時非常有用。

* 身為使用者，零管道的管道卡為我提供了適當的指引。

* 新活動頁面現已可用，其中可以查看管道和計劃碼執行等活動及其關聯的詳細資訊。長期下來，此頁面所列活動範圍會擴展，並提供詳細資訊。

* 新管道現在可以使用懸浮「狀態跨距」(status popover) 來輕鬆查看詳細資訊摘要。可以查看管道執行及其相關詳細資訊。

* 編輯管道 API 現在支援變更部署階段中使用的環境。

* 已針對大型套件引入了 OakPal 掃描流程中的最佳化。

* 品質問題 CSV 檔案現在包含每個品質問題的時間戳。

### 錯誤修正 {#bug-fixes-nov}

* 某些非正統的組建設定會將不必要的檔案儲存在管道的 Maven 成品快取中，導致在啟動和停止組建容器時形成無關的網路 I/O。

* 如果部署階段不存在，管道 PATCH API 將失敗。

* `ClientlibProxyResourceCheck`當存在具有通用基本路徑的用戶端庫時，品質規則會產生誤判問題。

* 達到最大存放庫數時的錯誤訊息未指定錯誤原因。

* 在極少數情況下，由於對某些回應計劃碼的重試處理不當，管道會失敗。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.22版的發佈日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測並報告所使用的ACS共用版本。
* 能夠檢測和報告組中的用戶和子組數。
* 能夠檢測並報告超過16MB的MongoDB中的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 對Foundation元件的檢測進行細化，減少漏檢。
* 對於AEM Forms客戶，BPA消息 `EMAIL_PDF_SUBMIT_ACTION` 未在AEMas a Cloud Service上可用
