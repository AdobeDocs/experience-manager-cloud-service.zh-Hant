---
title: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: f542d9423450086fcc4c0ba62f0e6f178df462e3
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2021.10.0)是2021年11月4日。
下列版本(2021.11.0)將於2021年12月2日發行。

## 發行影片 {#release-video}

查看 [2021年10月發行概述](https://video.tv.adobe.com/v/338253) 視訊，以取得新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容片段模型發佈後，現在會自動設為唯讀狀態，以避免重新發佈已編輯的模型後，無意中中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] 現在支援使用內建連接器，從支援的音訊和視訊資產自動產生文字記錄 [!DNL Azure Media Services]. 此 [支援的檔案類型](/help/assets/file-format-support.md#audio-video-transcription-formats) 會自動轉錄，且文字會以WebVTT格式儲存。 WebVTT字幕用於更有效的搜索、字幕或翻譯。 此外，此功能還可改善資產的協助工具、可探索性和本地化。

### 中的新功能 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

* [!DNL Dynamic Media] 影像智慧型裁切和色票現在由最新的Sensei服務提供技術支援，可產生改良的裁切和色票。 此外，已推出增強功能，以產生不同的裁切內容，針對相同外觀比例，但跨不同解析度。 此外，如果影像描述檔中的寬度和高度沒有變更，則任何手動編輯都會保留在重新處理時。

* 智慧標籤會使用資產微服務（而非智慧內容服務）自動套用至資產。 更新基礎模型，以改善標籤結果並減少偏誤。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 新增功能 [!DNL Forms] {#what-is-new-forms-oct-2021}

* **適用性Forms**:您現在可以透過Adobe Analytics for Adaptive Forms，擷取及追蹤登入與非登入（匿名）的行為，以收集一般使用者分析。 它有助於根據資料做出明智的決策，以改善一般使用者體驗。

### 中提供的新功能 [!DNL Forms] 預發行管道 {#prerelease-features-forms-oct-2021}

* **將AEM工作流程資料外部化，以安全處理**:您可以將包含敏感個人資料(SPD)元素的處理中AEM工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中，以進行安全處理。 資料元素和工作流程變數不會儲存在AEM存放庫中，並會在處理工作流程時，從客戶管理的存放庫隨選擷取。

### 測試版功能 [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 幫助您結合模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步和批次模式產生檔案。 API可讓您建立應用程式，以便您：

   * 使用XML資料填入範本檔案(PDF和XDP)，以產生檔案。
   * 以各種格式生成輸出表單，包括非互動式PDF打印流。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加元件支援最新的Commerce v2.4.3，並提供新的GraphQL API和結構

* 作者可使用RTF編輯器(RTE)，在文字欄位中新增產品和目錄頁面的連結。 RTE工具列中已新增CIF圖示，可開啟選擇器以快速搜尋並選取產品或類別，而不需離開內容。

* 現有的快顯購物車和結帳已取代為專用的AEM購物車和結帳頁面。 這些頁面上的元件是使用Magento的可擴充Peregrine元件所建置

* 商家可使用商務後端，在導覽中隱藏特定產品目錄類別。 CIF導覽核心元件會依照商務後端設定「包含在功能表中」，顯示/隱藏導覽中的類別

* AEM Storefront Venia在找不到類別或產品頁面時傳回HTTP 404錯誤

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service的2021.10.0版發行說明。

### 發行日期 {#release-date-cm-nov}

AEMas a Cloud Service的Cloud Manager發行日期2021.11.0為2021年11月4日。
下一版預計於2021年12月9日發行。

### 新增功能 {#what-is-new-cm-nov}

* 使用者現在可以運用新的前端管道，以加速方式專門部署前端程式碼。 請參閱 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 了解更多。

   >[!IMPORTANT]
   >您必須使用AEM版本 `2021.10.5933.20211012T154732Z` 以利用新的前端管道。

* 以更有效的方式執行程式碼分析，而不需要建立整個AEM影像，可大幅縮短程式碼品質管道持續時間。 此變更將在發行後的數週內逐步推出。

* Git提交ID現在會顯示在管道執行詳細資訊中，以便更輕鬆追蹤已建置的程式碼。

* 現在可透過公開的API建立方案。

* 現在可透過公開的API建立環境。

* 此 `x-request-id` 回應標題現在會顯示在 [www.adobe.io](https://www.adobe.io/). 提交客戶服務問題以進行疑難排解時，此標題相當實用。

* 身為使用者，我看到管道為零的管道卡為我提供適當的指引。

* 現在提供新的「活動頁面」，供檢視活動（例如管道和程式碼執行）及其相關詳細資訊之用。 隨著時間推移，此頁面所列的活動將會擴展範圍以及提供的詳細資料。

* 提供新的管道頁面，可在暫留時顯示狀態彈出視窗，方便您檢視詳細資訊摘要。 可檢視管道執行及其相關聯的詳細資訊。

* 「編輯管道API」現在支援變更部署階段所使用的環境。

* 已針對大型封裝導入OakPal掃描程式的最佳化。

* 品質問題CSV檔案現在會包含每個品質問題的時間戳記。

### 錯誤修正 {#bug-fixes-nov}

* 某些非正統的組建設定會導致管道的Maven工件快取中儲存不必要的檔案，導致在啟動和停止組建容器時產生多餘的網路I/O。

* 如果部署階段不存在，管道PATCHAPI就會失敗。

* 此 `ClientlibProxyResourceCheck` 當有具有共同基本路徑的用戶端程式庫時，品質規則會產生誤判問題。

* 達到最大儲存庫數時，錯誤訊息未指定錯誤的原因。

* 在少數情況下，管道由於某些回應代碼的重試處理不當而失敗。


## 發行日期 {#release-date-cm-oct}

AEMas a Cloud Service的Cloud Manager發行日期為2021.10.0年10月14日。

### 新增功能 {#what-is-new-cm-oct}

* 為準備日後的一些變更，現在會在使用者介面中參照現有的部署管道，並將其標示為 **完整堆棧** 管道。

* 管道卡已重新整理，現在會顯示顯示生產管道和非生產管道的單一整合面板，且使用者可從與每個管道相關聯的動作功能表中直接選取「執行/暫停/繼續」。

* 部署管理員角色中的使用者現在可以透過UI以自助方式刪除生產管道。

* 新增和編輯管道體驗已重新整理，現在可使用熟悉的現代模組。

* Cloud Manager的使用者現在可以透過 **意見反應** 按鈕。

* 每年的SLA圖表現在可以從Cloud Manager的使用者介面下載。

* 程式碼品質和非生產管道執行現在會在建置步驟期間使用更有效率的淺層復製程式，為擁有特別大型Git存放庫的客戶提供更快的建置時間。

* 「新增IP允許清單」精靈現在會通知使用者已達到允許的IP允許清單數目上限。

* Cloud Manager API檔案現在包含互動式操作場，可讓登入的使用者透過瀏覽器試驗API。 請參閱 [Cloud Manager API遊樂場](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以取得更多詳細資訊。

* 如果禁用「導航到」下的選擇選項，則「程式」卡上的工具提示將更具描述性。 現在會顯示「生產環境不存在」。

### 錯誤修正 {#bug-fixes-cm-oct}

* 在極少數情況下，當Adobe員工恢復客戶的環境時，在環境完全運行之前，會將恢復視為已完成。

* 環境建立期間提出的某些內部請求未重試。

* 如果在域名驗證後發生部署失敗錯誤，則錯誤消息已更正，以請客戶聯繫其Adobe代表。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 偵測及報告節點名稱長度的功能。

* 能夠偵測並報告總索引大小。

* 能夠偵測遺失原始轉譯的資產並製作報表。
