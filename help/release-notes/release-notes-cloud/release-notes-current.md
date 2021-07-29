---
title: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9ef41bc9f60f16a2fdf1900466db8bad99e619e9
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作為Cloud Service的最新發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前版本(2021.7.0)的發行日期為2021年7月29日。
下列版本(2021.8.0)將於2021年8月26日發行。

## 發行影片 {#release-video}

查看2021年7月[發行概述](https://video.tv.adobe.com/v/335580)影片，以取得新增功能的摘要。

## Experience ManagerFoundation作為Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更有彈性的Dispatcher設定：可更輕鬆地組織專案。 例如，您現在可以包含反映您網站結構的多個重寫規則檔案。 [了](/help/implementing/dispatcher/disp-overview.md#validation-debug) 解此彈性模式，包括如何建構您的Dispatcher設定，以便充分運用。
* 應將復寫代理的「分發」標籤下的樹狀復寫UI視為已過時，並計畫在9月30日後移除。 [了解](/help/operations/replication.md#tree-activation) 替代的復寫策略。
* Sling資料來源支援的套件組合`org.apache.sling.datasource-1.0.4.jar`已移除，因為其功能已過時，且客戶未使用。

## Experience Manager為Cloud Service的XML文檔 {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

Experience Manager作為Cloud Service的XML檔案正式提供。 它可讓Experience ManagerCloud Service客戶採購XML檔案，以便跨多個管道(包括Experience Manager網站)匯入、建立、管理和傳送技術內容。

## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.7.0Cloud Service中Cloud Manager的發行說明。

### 發行日期 {#release-cm-july}

AEM as aCloud Service2021.7.0中的Cloud Manager發行日期為2021年7月15日。
下一版預計於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建進程，並且可以選擇將其中一個JDK用於與工具鏈相容的Maven插件&#x200B;*或*&#x200B;整個Maven進程執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* 執行舊版AEM的預備和生產環境現在會回報&#x200B;**可用更新**&#x200B;狀態。

* 支援的SSL憑證上限已提高至每個程式20個。

* 每個環境可配置的域數上限已增加到500個。

* **管理Git**&#x200B;按鈕已重新命名為&#x200B;**存取Git資訊**，對話方塊也已視覺化重新整理。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

### 錯誤修正 {#bug-fixes-cm-july}

* 在某些情況下，將IP允許清單系結至環境時，「預覽」不是可用選項。

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 達到最大SSL憑證數時顯示的錯誤訊息並無幫助。

* 在某些情況下，**概述**&#x200B;頁面上的管道卡片所顯示的發行版本可能會不一致。

* 添加程式嚮導未正確說明建立後無法更改名稱。

### 已知問題 {#known-issues-cm-july}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]中的新功能 {#assets-features}

* 「內容自動化」功能可讓[!DNL Experience Manager Assets]運用[!DNL Adobe Creative Cloud] API大規模自動化資產生產。 它可大幅減少建立相同資產變異所需的時間和迭代次數，借此改善內容速度。 此功能不需要任何程式設計，也可在DAM內運作。 請參閱[使用Creative Cloud整合產生資產變異](/help/assets/cc-api-integration.md)。

* [!DNL Experience Manager Assets] 包含PDF [!DNL Document Cloud] 查看器以原生方式預覽PDF文檔。此功能可讓使用者預覽多頁PDF檔案，而不需進行任何檔案處理或轉換。 此功能改進了[!DNL Experience Manager] 6.5的奇偶校驗。查看器中可用的控制項包括縮放、導航到頁面、取消固定控制項以及全螢幕查看。 使用者案例也可預覽並跳至頁面和書籤。 支援對檔案本身的註解，且未來版本將新增對PDF檔案內容的註解和註解。

   ![使用PDF查看器 [!DNL Experience Manager] 預覽PDF檔案](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下載功能使用非同步下載來提升下載速度。 請參閱[下載使用連結共用的共用資產](/help/assets/download-assets-from-aem.md#link-share-download)。

   ![下載收件匣](/help/assets/assets/download-inbox.png)

* 已增強檢視設定，讓使用者選擇預設檢視和預設排序參數。

   ![在「視圖設定」中設定 [!UICONTROL 預設視圖]](/help/assets/assets/view-settings-for-defaults.png)

* 使用者可以根據屬性述詞來搜尋和篩選資料夾。

   ![使用搜索謂詞篩選搜索資料夾](/help/assets/assets/search-folders-via-predicates.png)

### [!DNL Assets]發行前通道中提供的新功能 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 當您以連結形式共用數位資產時，使用者可以將URL複製到剪貼簿。 增強功能可讓您以更快速且更方便的方式共用資產。

### [!DNL Assets]中修正的錯誤 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection`在[!DNL Experience Manager]中不作為[!DNL Cloud Service]使用。 (CQ-4326322)

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 錯誤修正 {#bug-fixes-screens}

* 內容提供者設定現在會在建立或更新期間驗證。

* 所有顯示的視圖都有資料夾列。

* 您可以展開「螢幕」內容結構。

* `bulk-offline-update-service` 缺少某些環境的所有權限。

* 更新說明連結，以符合新的screens雲端檔案。

* 取消指派播放清單，以及不允許移除已指派播放器的播放清單，現在已可運作。

* 清除「全部」快取時，播放器現在會重新下載資產。

* 如果為後一天設定了&#x200B;*結束時間*，則重複計畫現在可以運作。

* `Back&Forward` 現在可在Screens中以Cloud ServiceUI的形式運作。

* 無法先建立名稱相同但命名空間不同的標籤。

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]中的新增功能 {#what-is-new-forms}

* 您現在可以使用Automated forms conversion服務，將法文、德文和西班牙文的PDF forms轉換為最適化表單。
* 新增個別面板至範本編輯器，以顯示與最適化表單元件相關的錯誤。 它有助於在單一位置整合所有最適化表單錯誤，並縮短解析時間。

### [!DNL Forms]發行前通道中提供的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:通訊API可協助您結合XDP範本和XML資料，以產生各種格式的列印檔案。此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   * 使用XML資料填入範本檔案，以產生檔案。
   * 以各種格式產生輸出表單，包括非互動式PDF列印資料流。
   * 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

* **變數資料外部化程式**:您可以將AEM工作流程變數的資料儲存在您的組織所管理的外部儲存系統上。

* **基於Acroform的記錄文檔**:除了XFA型表單範本外，您也可以使用Adobe Acrobat表單PDF(Acroform PDF)作為記錄檔案的範本。

* **Microsoft Azure資料儲存連接器**:您現在可以將表單資料模型連接到Microsoft Azure Storage。它可讓您將最適化表單資料儲存及擷取至Microsoft Azure Storage，作為BLOB。


## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-july-cam}

Cloud Acceleration Manager的發行日期為2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager是雲端型應用程式，旨在引導您的IT團隊完成從規劃到上線的整個轉換過程。Cloud Service 透過Adobe建議的最佳實務、提示、檔案和工具，為您的團隊設定成功的移轉作業，以協助您在前往AEM作為Cloud Service的歷程的每個階段。 了解更多[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en)。

>[!NOTE]
>
> 查看此[Cloud Acceleration Manager示範影片](https://video.tv.adobe.com/v/335547)。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心元件v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 以製作模式呈現階段產品資料的視覺指標，可更清楚掌握即將進行的變更
   * 適用於內容與商務頁面的新Sitemap元件

* 支援AEM Storefront的[Adobe商務Sensei產品建議(由Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)提供技術支援，使用預先定義或即時建立的建議)
