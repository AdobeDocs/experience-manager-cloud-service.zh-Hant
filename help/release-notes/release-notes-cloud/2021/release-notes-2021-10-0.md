---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 66%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]目前版本(2021.10.0)的發行日期為2021年11月4日。
下列版本(2021.11.0)將於2021年12月2日發行。

## 發行影片 {#release-video}

請觀看[2021年10月版本總覽](https://video.tv.adobe.com/v/338253)影片，以瞭解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]中的新功能 {#sites-features}

* 內容片段模型現在會在發佈後自動設為唯讀狀態，以避免重新發佈已編輯的模型後，無意中中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [!DNL Experience Manager]現在支援使用[!DNL Azure Media Services]的內建聯結器，從支援的音訊和視訊資產自動產生文字記錄。 [支援的檔案型別](/help/assets/file-format-support.md#audio-video-transcription-formats)會自動轉譯，文字會以WebVTT格式儲存。 WebVTT註解可用於更有效的搜尋、註解或翻譯。 此外，功能可改善資產的協助工具、可發現性和本地化。

### [!DNL Assets]發行前管道中的新功能 {#assets-prerelease-features}

* [!DNL Dynamic Media]影像智慧型裁切和色票現在由最新的AI服務提供支援，可製作出更佳裁切和色票成果。 此外，已啟動增強功能以產生相同縱橫比但跨不同解析度的不同裁切內容。 此外，如果「影像設定檔」中的寬度和高度沒有變化，則在重新處理時會保留任何手動編輯。

* 智慧標籤會自動套用至使用資產微服務的資產，而非智慧內容服務。 基礎模型已更新，以改善標籤結果並減少偏差。<!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤已登入和未登入（匿名）的行為，以收集使用者的深入解析。 這可幫助您根據資料來進行明智的決策，以改善使用者體驗。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-oct-2021}

* **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms] 的 Beta 版功能  {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加元件支援具有新Commerce API和結構描述的最新GraphQL v2.4.3

* 作者可使用RTF編輯器(RTE)，在文字欄位中新增產品與目錄頁面的連結。 RTE工具列已新增CIF圖示，可開啟選擇器，以快速搜尋並選取產品或類別，而不需離開內容。

* 現有的彈出式購物車和結帳頁面已替換為專用的AEM購物車和結帳頁面。 這些頁面上的元件是使用Adobe Commerce的可擴充Peregrine元件所建置

* 商家可使用Commerce後端，在導覽中隱藏特定產品目錄類別。 CIF導覽核心元件遵守Commerce後端設定「包含在功能表中」以在導覽中顯示/隱藏類別

* 如果找不到類別或產品頁面，AEM Storefront Venia會傳回HTTP 404錯誤

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.10.0中Cloud Manager的發行說明

### 發行日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0中Cloud Manager的發行日期為2021年11月4日。
下一版本計畫於2021年12月9日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以使用新的前端管道以加速的方式專門部署前端代碼。請參閱 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)來了解更多資訊。

  >[!IMPORTANT]
  >您必須使用 AEM 版本 `2021.10.5933.20211012T154732Z` 才可使用最新的前端管道。

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


## 發行日期 {#release-date-cm-oct}

AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 發行日期是 2021 年 10 月 14 日。

### 新增功能 {#what-is-new-cm-oct}

* 為了準備一些即將發生的變化，現有的部署管道現在將在使用者界面中被引用和被其標籤為&#x200B;**完整堆疊**&#x200B;管道。

* 管道卡已刷新，現在顯示一個整合的面，顯示生產和非生產管道，使用者可以直接從與每個管道關聯的操作選單中選擇執行/暫停/恢復。

* Deployment Manager 角色的使用者現在可以透過 UI 以自助方式刪除生產管道。

* 新增和編輯管道體驗已更新，現在可以使用熟悉的現代模式。

* Cloud Manager 的使用者現在可以透過使用者界面直接提交意見反饋&#x200B;**意見反饋**&#x200B;著陸頁右上角的按鈕。

* 現在可以從 Cloud Manager 的使用者界面下載年度 SLA 圖表。

* 程式碼品質和非生產管道執行現在將在構建步驟中使用更有效的淺層克隆過程，從而為擁有特別大的 git 存放庫的客戶帶來更快的構建時間。

* 新增 IP 允許清單精靈現在將通知使用者是否已達到 IP 允許清單的最大允許數量。

* Cloud Manager API 文件現在包括一個交互式遊樂場，允許登入使用者從他們的瀏覽器中試驗 API。查看 [Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 的更多細節。

* 如果停用「瀏覽至」下的選擇選項，則程序卡上的工具提示將更具描述性。現在會顯示「生產環境不存在。」

### 錯誤修正 {#bug-fixes-cm-oct}

* 在極少數情況下，當 Adobe 工作人員恢復客戶的環境時，在環境完全執行之前，恢復就被認為已完成。

* 在環境建立期間發出的某些內部請求沒有被重試。

* 如果在網域名稱驗證後出現部署失敗錯誤，則已更正錯誤消息以請求客戶聯繫其 Adobe 代表。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 能夠偵測並報告節點名稱長度。

* 能夠偵測及報告索引總大小。

* 能夠偵測並報告缺少原始轉譯的資產。
