---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 21%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2021.7.0)為2021年7月29日。
下列版本(2021.8.0)將於2021年8月26日發行。

## 發行影片 {#release-video}

查看 [2021年7月發行概述](https://video.tv.adobe.com/v/335580) 視訊，以取得新增功能的摘要。

## Experience Manager基礎as a Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更有彈性的Dispatcher設定：可更輕鬆地組織專案。 例如，您現在可以包含反映您網站結構的多個重寫規則檔案。 [了解](/help/implementing/dispatcher/disp-overview.md#validation-debug) 此彈性模式，包括如何建構您的dispatcher設定，以便充分運用。
* 應將復寫代理的「分發」標籤下的樹狀復寫UI視為已過時，並計畫在9月30日後移除。 [了解](/help/operations/replication.md#tree-activation) 替代複製策略。
* 捆綁 `org.apache.sling.datasource-1.0.4.jar` for Sling資料來源支援已移除，因為其功能已過時，且客戶未使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 內容自動化功能可讓 [!DNL Experience Manager Assets] 善用 [!DNL Adobe Creative Cloud] API可大規模自動化資產生產。 它可大幅減少建立相同資產變異所需的時間和迭代次數，借此改善內容速度。 此功能不需要任何程式設計，也可在DAM內運作。 請參閱 [使用Creative Cloud整合產生資產變異](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] 包括 [!DNL Document Cloud] PDF查看器以原生方式預覽PDF文檔。 此功能可讓使用者預覽多頁PDF檔案，而不需進行任何檔案處理或轉換。 此功能可改善奇偶校驗 [!DNL Experience Manager] 6.5.檢視器中可用的控制項包括縮放、導覽至頁面、取消固定控制項，以及以全螢幕檢視。 使用者案例也可預覽並跳至頁面和書籤。 支援對檔案本身的註解，且未來版本將新增對PDF檔案內容的註解和註解。

   ![在中預覽PDF檔案 [!DNL Experience Manager] 使用PDF檢視器](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下載功能使用非同步下載來提升下載速度。 請參閱 [下載使用連結共用共用的資產](/help/assets/download-assets-from-aem.md#link-share-download).

   ![下載收件匣](/help/assets/assets/download-inbox.png)

* 已增強檢視設定，讓使用者選擇預設檢視和預設排序參數。

   ![在中設定預設檢視 [!UICONTROL 檢視設定]](/help/assets/assets/view-settings-for-defaults.png)

* 使用者可以根據屬性述詞來搜尋和篩選資料夾。

   ![使用搜索謂詞篩選搜索資料夾](/help/assets/assets/search-folders-via-predicates.png)

### 此 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 當您以連結形式共用數位資產時，使用者可以將URL複製到剪貼簿。 增強功能可讓您以更快速且更方便的方式共用資產。

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` 在中無法使用 [!DNL Experience Manager] as a [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* 您現在可以使用 Automated Forms Conversion 服務[將法文、德文和西班牙文 PDF Forms 轉換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)成最適化表單。
* 範本編輯器新增個別面板，以顯示與最適化表單元件相關的錯誤。它有助於在同一處整合所有最適化表單錯誤，並縮短解決時間。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生檔案。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

* **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

* **Acroform-based Document of Record**：您也可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心元件v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 以製作模式呈現階段產品資料的視覺指標，可更清楚掌握即將進行的變更
   * 適用於內容與商務頁面的新Sitemap元件

* 支援 [Adobe Commerce Sensei產品建議，由Adobe Sensei提供技術支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用預先定義或即時建立的建議

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 錯誤修正 {#bug-fixes-screens}

* 內容提供者設定現在會在建立或更新期間驗證。

* 所有顯示的視圖都有資料夾列。

* 您可以展開「螢幕」內容結構。

* `bulk-offline-update-service` 缺少某些環境的所有權限。

* 更新說明連結，以符合新的screens雲端檔案。

* 取消指派播放清單，以及不允許移除已指派播放器的播放清單，現在已可運作。

* 清除「全部」快取時，播放器現在會重新下載資產。

* 重複排程現在可行，如果 *結束時間* 設定為後一天。

* `Back&Forward` 現在可在Screensas a Cloud ServiceUI中運作。

* 無法先建立名稱相同但命名空間不同的標籤。

## XML Documentation for Experience Manageras a Cloud Service {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

XML Documentation forExperience Manageras a Cloud Service已推出。 它可讓Experience Manageras a Cloud Service客戶購買XML Documentation廣告，以跨多個管道(包括Experience Manager Sites)匯入、建立、管理及傳送技術內容。

## Cloud Manager {#cloud-manager}

本節概述AEM 2021.7.0中Cloud Manageras a Cloud Service的發行說明。

### 發行日期 {#release-cm-july}

AEM 2021.7.0中的Cloud Manageras a Cloud Service日期為2021年7月15日。
下一版預計於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建過程，並且可以選擇使用其中一個JDK用於與工具鏈相容的Maven插件 *或* 整個Maven程式執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* 執行舊版AEM的預備和生產環境現在會回報 **可用更新**.

* 支援的SSL憑證上限已提高至每個程式20個。

* 每個環境可配置的域數上限已增加到500個。

* 此 **管理Git** 按鈕已重新命名為 **存取Git資訊** 對話框已刷新。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

### 錯誤修正 {#bug-fixes-cm-july}

* 在某些情況下，將IP允許清單系結至環境時，「預覽」不是可用選項。

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 達到最大SSL憑證數時顯示的錯誤訊息並無幫助。

* 在某些情況下，在上的管道卡片中顯示的發行版本可能會不一致 **概述** 頁面。

* 添加程式嚮導未正確說明建立後無法更改名稱。

### 已知問題 {#known-issues-cm-july}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-july-cam}

Cloud Acceleration Manager的發行日期為2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager是雲端型應用程式，旨在引導您的IT團隊完成從規劃到上線的整個轉換過程。Cloud Service 透過Adobe建議的最佳實務、提示、檔案和工具，為您的團隊設定成功的移轉作業，以協助您在前往AEM作為Cloud Service的歷程的每個階段。 深入了解 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> 檢查 [Cloud Acceleration Manager示範影片](https://video.tv.adobe.com/v/335547).
