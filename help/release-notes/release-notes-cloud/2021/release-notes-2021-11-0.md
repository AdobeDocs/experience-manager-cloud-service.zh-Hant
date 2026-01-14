---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版發行說明。'
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 55%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]目前版本(2021.11.0)的發行日期為2021年12月16日。
下列版本(2022.1.0)的發行日期為2022年2月3日。

## 發行影片 {#release-video}

請觀看[2021年12月版本總覽](https://video.tv.adobe.com/v/339278)影片，瞭解2021.11.0 （2021年11月）版本新增的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* Dynamic Media影像智慧型裁切和色票現在由最新的Adobe AI服務提供支援，可製作出更佳裁切和色票成果。 此外，已啟動增強功能以產生相同縱橫比但跨不同解析度的不同裁切內容。 此外，如果「影像設定檔」中的寬度和高度沒有變化，則在重新處理時會保留任何手動編輯。

### [!DNL Assets]發行前管道中的新功能 {#assets-prerelease-features}

* [!DNL Dynamic Media] — 您現在可以使用AEM Dynamic Media介面進行設定，包括一般設定和發佈設定，而不必透過Dynamic Media Classic案頭應用程式來進行。

* [!DNL Dynamic Media]現在支援MXF影片的擷取、預覽、播放和發佈。 尚不支援MXF影片的附註和可訂購影片。

* 在設定遠端DAM和Sites部署之間的連線後，遠端DAM上的資產可在Sites部署中使用。 您現在可以在遠端DAM資產或資料夾上執行[更新、刪除、重新命名和移動操作](/help/assets/use-assets-across-connected-assets-instances.md)。 這些更新會在Sites部署中自動提供，但會有一些延遲。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

* **使用Communications API建立的記錄檔案和PDF檔案的自訂字型**：您現在可以在使用Communications API產生的PDF檔案中使用品牌核准的字型，以符合您的組織要求。

* **Forms入口網站**：您可以使用[Forms入口網站](/help/forms/configure-forms-portal.md)，在AEM Sites頁面上列出您已發佈的最適化表單。 這有助於網站訪客發現所有可用表單。 此外，訪客可以使用Forms入口網站來儲存和存取最適化表單的草稿，並檢視已提交最適化表單的PDF版本。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 以Commerce的可擴充Peregrine元件為基礎的擴充myAccount元件

![延伸myAccount元件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可使用其他建議型別來建立臨機Commerce產品建議

* 支援AEM Storefront中的禮品卡

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.11.0中Cloud Manager的發行說明

### 發行日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0中Cloud Manager的發行日期為2021年11月4日。
下一版本計畫於2021年12月9日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以使用新的前端管道以加速的方式專門部署前端代碼。請參閱 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)來了解更多資訊。

  >[!IMPORTANT]
  >您必須使用AEM版本`2021.10.5933.20211012T154732Z`或更高版本才能使用新的前端管道。

* 透過以更有效的方式執行程式碼分析來顯著減少程式碼品質管道期限，而不需要建置整個 AEM 影像。此變更會在發佈後的未來幾週內逐步展開。

* Git 認可識別碼現在會顯示在管道執行詳細資訊中，如此將更易追蹤產生的程式碼。

* 計畫建立現在可以透過公開顯示的 API 獲得。

* 環境建立現在可以透過公開顯示的 API 獲得。

* `x-request-id` 回應標題現可於 [www.adobe.io](https://www.adobe.io/) 網站上的 API Playground 中看到。此標題在提交客戶服務問題以進行故障排除時非常有用。

* 身為使用者，零管道的管道卡為我提供了適當的指引。

* 新活動頁面現已可用，其中可以查看管道和程式碼執行等活動及其關聯的詳細資訊。長期下來，此頁面所列活動範圍會擴展，並提供詳細資訊。

* 新管道現在可以使用懸浮「狀態跨距」(status popover) 來輕鬆查看詳細資訊摘要。可以查看管道執行及其相關詳細資訊。

* 編輯管道 API 現在支援變更部署階段中使用的環境。

* 已針對大型套件引入了 OakPal 掃描流程中的最佳化。

* 品質問題 CSV 檔案現在包含每個品質問題的時間戳。

### 錯誤修正 {#bug-fixes-nov}

* 某些非正統的組建設定會將不必要的檔案儲存在管道的 Maven 成品快取中，導致在啟動和停止組建容器時形成無關的網路 I/O。

* 如果部署階段不存在，管道 PATCH API 將失敗。

* `ClientlibProxyResourceCheck`當存在具有通用基本路徑的用戶端庫時，品質規則會產生誤判問題。

* 達到最大存放庫數時的錯誤訊息未指定錯誤原因。

* 在極少數情況下，由於對某些回應程式碼的重試處理不當，管道會失敗。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的發行日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測和報告所使用的ACS Commons版本。
* 能夠偵測並報告群組中的使用者和子群組數量。
* 能夠偵測並報告MongoDB中超過16MB的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 已改善對Foundation元件的偵測，以減少誤判。
* 針對AEM Forms客戶，已修正AEM as a Cloud Service上無法使用`EMAIL_PDF_SUBMIT_ACTION`的BPA訊息。
