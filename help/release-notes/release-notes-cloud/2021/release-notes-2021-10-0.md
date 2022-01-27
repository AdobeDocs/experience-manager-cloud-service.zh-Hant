---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.10.0 版發行說明。'
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 16%

---



# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本期(2021.10.0)是2021年11月4日。
以下版本(2021.11.0)是2021年12月2日。

## 發佈視頻 {#release-video}

看看 [2021年10月發佈概述](https://video.tv.adobe.com/v/338253) 視頻，瞭解添加的功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容片段模型在發佈後將自動設定為只讀狀態，以避免在重新發佈編輯的模型後無意中中斷即時API查詢。 嘗試編輯已發佈模型時，系統會提示用戶出現警告。 接受警告後可進行編輯。

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] 現在支援使用內置連接器從支援的音頻和視頻資產自動生成文本記錄 [!DNL Azure Media Services]。 的 [支援的檔案類型](/help/assets/file-format-support.md#audio-video-transcription-formats) 文本以WebVTT格式儲存。 WebVTT字幕用於更有效的搜索、字幕或翻譯。 此外，該功能還改進了資產的可訪問性、可發現性和本地化。

### 中的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop and Swatch現在由最新的Sensei服務提供支援，該服務可生成改良的作物和色板。 此外，已啟動增強，以生成不同的作物內容，對於相同的長寬比，但跨不同的解析度。 此外，如果「影像配置檔案」中的寬度和高度沒有變化，則在重新處理時將保留任何手動編輯。

* 智慧標籤將自動應用於使用資產微服務（而不是Smart Content Services）的資產。 更新基礎模型以改進標籤結果並減少偏差。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤已登入和未登入 (匿名) 的行為，以收集一般用戶的深入解析。它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-oct-2021}

* **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms]的 Beta 版功能 {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加模組支援最新的Commerce v2.4.3和新的GraphQL API和架構

* 作者可以使用富格文本編輯器(RTE)在文本欄位中添加到產品和目錄頁面的連結。 CIF表徵圖已添加到RTE工具欄，該工具欄將開啟選擇者以快速搜索和選擇產品或類別而不離開上下文。

* 現有的彈出式購物車和結帳已替換為專用的購AEM物車和結帳頁。 這些頁面上的元件是使用Adobe Commerce的可擴展Peregrine元件構建的

* 商家可以使用Commerce後端在導航中隱藏某些產品目錄類別。 CIF導航核心元件尊重商業後端配置「包括在菜單中」以顯示/隱藏導航中的類別

* 如AEM果找不到類別或產品頁，Storefront Venia將返回HTTP 404錯誤

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.10.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-date-cm-nov}

Cloud Manager在as a Cloud Service中的發AEM布日期為2021年11月4日。
下一版計畫於2021年12月9日發行。

### 新增功能 {#what-is-new-cm-nov}

* 用戶現在可以利用新的前端管道以加速的方式專門部署前端代碼。 請參閱 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 來瞭解更多資訊。

   >[!IMPORTANT]
   >您必須處於版AEM本 `2021.10.5933.20211012T154732Z` 利用新的前端管道。

* 通過以更有效的方式執行代碼分析而不需要構建整個影像，代碼質量流水線持續時間顯著AEM縮短。 此更改將在發佈後的幾週內逐步展開。

* Git提交ID現在將顯示在管道執行詳細資訊中，使跟蹤生成的代碼更容易。

* 現在可通過公開的API建立程式。

* 現在可通過公開的API建立環境。

* 的 `x-request-id` 響應標頭現在可在上的API Ploagn中看到 [www.adobe.io](https://www.adobe.io/)。 此標題在提交客戶關心問題以進行故障排除時非常有用。

* 作為用戶，我看到零管線的管線卡為我提供了適當的指導。

* 現在可以使用新的「活動」頁，其中可以查看諸如管道和代碼執行等活動及其關聯的詳細資訊。 隨著時間的推移，此頁中列出的活動將擴展範圍以及提供的詳細資訊。

* 現在可以使用一個新的「管線」(Pipelines)頁面，該頁面具有懸停時的狀態跨距，以便輕鬆查看詳細資訊摘要。 可以查看管道執行及其關聯的詳細資訊。

* 「編輯管道API」現在支援更改部署階段中使用的環境。

* 介紹了OakPal掃描過程中對大包裝的優化。

* 質量問題CSV檔案現在將包含每個質量問題的時間戳。

### 錯誤修正 {#bug-fixes-nov}

* 某些非常規的生成配置導致不必要的檔案儲存在管道的Maven項目快取中，這導致在啟動和停止生成容器時產生額外的網路I/O。

* 如果部署階段不存在，管道PATCHAPI將失敗。

* 的 `ClientlibProxyResourceCheck` 當存在具有共同基本路徑的客戶端庫時，質量規則會產生誤報問題。

* 達到最大資料庫數時的錯誤消息未指定錯誤原因。

* 在少數情況下，管道由於某些響應代碼的重試處理不當而失敗。


## 發行日期 {#release-date-cm-oct}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年10月14日。

### 新增功能 {#what-is-new-cm-oct}

* 為準備即將進行的一些更改，現在將在用戶介面中引用現有部署管道並將其標籤為 **完整堆棧** 管線。

* 管道卡已刷新，現在將顯示一個顯示生產管線和非生產管線的單個整合面，用戶可以直接從與每個管線關聯的操作菜單中選擇「運行/暫停/恢復」。

* 部署管理器角色中的用戶現在可以通過UI以自助方式刪除生產管道。

* 添加和編輯管道體驗已刷新，現在可使用熟悉的現代模型。

* Cloud Manager的用戶現在可以通過以下方式直接從用戶介面提交反饋： **反饋** 按鈕。

* 現在，可以從Cloud Manager的用戶介面下載年度SLA圖表。

* 代碼質量和非生產流水線執行現在將在生成步驟期間使用一個更高效的淺層克隆過程，從而為具有特別大的Git儲存庫的客戶帶來更快的生成時間。

* 「添加IP允許清單」嚮導現在將通知用戶是否已達到允許的IP允許清單的最大數量。

* Cloud Manager API文檔現在包括一個互動式操場，允許登錄用戶從其瀏覽器中試用API。 請參閱 [Cloud Manager API遊樂場](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 的子菜單。

* 如果禁用「導航至」下的選擇選項，則程式卡上的工具提示將更具說明性。 現在顯示「生產環境不存在」。

### 錯誤修正 {#bug-fixes-cm-oct}

* 在極少數情況下，當Adobe員工恢復客戶的環境時，在環境完全正常運行之前，會認為恢復已完成。

* 未重試在建立環境期間發出的某些內部請求。

* 如果在域名驗證後出現部署失敗錯誤，則已更正錯誤消息以請求客戶聯繫其Adobe代表。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

最佳做法分析器2.1.20版的發佈日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 能夠檢測並報告節點名稱長度。

* 能夠檢測並報告總索引大小。

* 能夠檢測並報告丟失原始格式副本的資產。
