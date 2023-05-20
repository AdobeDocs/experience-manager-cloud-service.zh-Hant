---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 69%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本期(2021.10.0)是2021年11月4日。
以下版本(2021.11.0)是2021年12月2日。

## 發行影片 {#release-video}

看看 [2021年10月發佈概述](https://video.tv.adobe.com/v/338253) 視頻，瞭解添加的功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容片段模型在發佈後將自動設定為只讀狀態，以避免在重新發佈編輯的模型後無意中中斷即時API查詢。 嘗試編輯已發佈模型時，系統會提示用戶出現警告。 接受警告後可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [!DNL Experience Manager] 現在支援使用內置連接器從支援的音頻和視頻資產自動生成文本記錄 [!DNL Azure Media Services]。 的 [支援的檔案類型](/help/assets/file-format-support.md#audio-video-transcription-formats) 文本以WebVTT格式儲存。 WebVTT字幕用於更有效的搜索、字幕或翻譯。 此外，該功能還改進了資產的可訪問性、可發現性和本地化。

### 中的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop and Swatch現在由最新的Sensei服務提供支援，該服務可生成改良的作物和色板。 此外，已啟動增強，以生成不同的作物內容，對於相同的長寬比，但跨不同的解析度。 此外，如果「影像配置檔案」中的寬度和高度沒有變化，則在重新處理時將保留任何手動編輯。

* 智慧標籤將自動應用於使用資產微服務（而不是Smart Content Services）的資產。 更新基礎模型以改進標籤結果並減少偏差。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤已登入和未登入 (匿名) 的行為，以收集一般用戶的深入解析。它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-oct-2021}

* **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms]的 Beta 版功能 {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加模組支援最新的Commerce v2.4.3和新的GraphQLAPI和架構

* 作者可以使用富格文本編輯器(RTE)在文本欄位中添加到產品和目錄頁面的連結。 CIF表徵圖已添加到RTE工具欄，該工具欄將開啟選擇者以快速搜索和選擇產品或類別而不離開上下文。

* 現有的彈出式購物車和結帳已替換為專用的購AEM物車和結帳頁。 這些頁面上的元件是使用Adobe Commerce的可擴展Peregrine元件構建的

* 商家可以使用Commerce後端在導航中隱藏某些產品目錄類別。 CIF導航核心元件尊重商業後端配置「包括在菜單中」以顯示/隱藏導航中的類別

* 如AEM果找不到類別或產品頁，Storefront Venia將返回HTTP 404錯誤

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.10.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 發行日期是 2021 年 11 月 04 日。下一個版本計畫於 2021 年 12 月 09 日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以善用新的前端管道以加速的方式專門部署前端計劃碼。 請參閱 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)來了解更多資訊。

   >[!IMPORTANT]
   >您必須使用 AEM 版本 `2021.10.5933.20211012T154732Z` 才可使用最新的前端管道。

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


## 發行日期 {#release-date-cm-oct}

AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 發行日期是 2021 年 10 月 14 日。

### 新增功能 {#what-is-new-cm-oct}

* 為了準備一些即將發生的變化，現有的部署管道現在將在使用者界面中被引用和標記為&#x200B;**完整堆疊**&#x200B;管道。

* 管道卡已刷新，現在顯示一個整合的面，顯示生產和非生產管道，使用者可以直接從與每個管道關聯的操作選單中選擇執行/暫停/恢復。

* Deployment Manager 角色的使用者現在可以透過 UI 以自助方式刪除生產管道。

* 新增和編輯管道體驗已更新，現在可以使用熟悉的現代模式。

* Cloud Manager 的使用者現在可以透過使用者界面直接提交意見反饋&#x200B;**意見反饋**&#x200B;著陸頁右上角的按鈕。

* 現在可以從 Cloud Manager 的使用者界面下載年度 SLA 圖表。

* 計劃碼品質和非生產管道執行現在將在構建步驟中使用更有效的淺層克隆過程，從而為擁有特別大的 git 存放庫的客戶帶來更快的構建時間。

* 新增 IP 允許清單嚮導現在將通知使用者是否已達到 IP 允許清單的最大允許數量。

* Cloud Manager API 文件現在包括一個交互式遊樂場，允許登入使用者從他們的瀏覽器中試驗 API。查看 [Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 的更多細節。

* 如果停用「瀏覽至」下的選擇選項，則程序卡上的工具提示將更具描述性。現在會顯示「生產環境不存在。」

### 錯誤修正 {#bug-fixes-cm-oct}

* 在極少數情況下，當 Adobe 工作人員恢復客戶的環境時，在環境完全執行之前，恢復就被認為已完成。

* 在環境建立期間發出的某些內部請求沒有被重試。

* 如果在網域名稱驗證後出現部署失敗錯誤，則已更正錯誤消息以請求客戶聯繫其 Adobe 代表。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

最佳做法分析器2.1.20版的發佈日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 能夠檢測並報告節點名稱長度。

* 能夠檢測並報告總索引大小。

* 能夠檢測並報告丟失原始格式副本的資產。
