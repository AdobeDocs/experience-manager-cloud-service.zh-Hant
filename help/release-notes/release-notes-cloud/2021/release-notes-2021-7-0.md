---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽到舊版的發行說明；例如，2020年和2021年的版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]目前版本(2021.7.0)的發行日期為2021年7月29日。
下列版本(2021.8.0)將於2021年8月26日發行。

## 發行影片 {#release-video}

請觀看[2021年7月版本總覽](https://video.tv.adobe.com/v/335580)影片，以瞭解新增功能的摘要。

## Experience Manager基礎as a Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更靈活的Dispatcher設定：更輕鬆地組織專案。 例如，您現在可以包含反映網站結構的多個重寫規則檔案。 [瞭解](/help/implementing/dispatcher/disp-overview.md#validation-debug)此彈性模式，包括如何建構您的Dispatcher設定，以便您加以運用。
* 在復寫代理程式的「散發」標籤下方的樹狀復寫UI應視為不建議使用，並在2021年9月30日之後移除。 [瞭解](/help/operations/replication.md#tree-activation)替代復寫策略。
* Sling資料來源支援的套件`org.apache.sling.datasource-1.0.4.jar`已移除，因為其功能已過時且未由客戶使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 內容自動化功能可讓[!DNL Experience Manager Assets]使用[!DNL Adobe Creative Cloud] API來大規模自動化資產的製作。 它大幅減少了建立相同資產的變體所需的時間和反複工作，進而加快提供內容的速度。 此功能不需要從DAM中進行任何程式設計和工作。 請參閱[使用Creative Cloud整合](/help/assets/cc-api-integration.md)產生資產的變體。

* [!DNL Experience Manager Assets]包含[!DNL Document Cloud]個PDF檢視器以原生預覽PDF檔案。 此功能可讓使用者預覽多頁PDF檔案，而不需進行任何檔案處理或轉換。 此功能改善與[!DNL Experience Manager] 6.5的同等性。檢視器中可用的控制項包括縮放、瀏覽至頁面、取消固定控制項，以及全熒幕檢視。 使用者也可以預覽並跳至頁面和書籤。 支援檔案本身的註解。 對PDF檔案中的內容發表評論和註解計畫於未來版本推出。

  使用PDF檢視器在[!DNL Experience Manager]中預覽PDF檔案![&#128279;](/help/assets/assets/preview-pdf-file-viewer.png)

* 連結共用下載功能使用可提高下載速度的非同步下載。 如需詳細資訊，請參閱[下載使用連結共用的資產](/help/assets/download-assets-from-aem.md#link-share-download)。

  ![下載收件匣](/help/assets/assets/download-inbox.png)

* 已增強檢視設定，讓使用者可選擇預設檢視和預設排序引數。

  ![在[!UICONTROL 檢視設定]](/help/assets/assets/view-settings-for-defaults.png)中設定預設檢視

* 使用者可以根據屬性述詞搜尋及篩選檔案夾。

  ![使用搜尋述詞篩選搜尋資料夾](/help/assets/assets/search-folders-via-predicates.png)

### [!DNL Assets]發行前通道中可用的新功能 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 當您以連結形式共用數位資產時，使用者可以將URL複製到剪貼簿。 此增強功能可讓您以更快、更方便的方式共用資產。

### 修正在 [!DNL Assets] 中的錯誤 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection`在[!DNL Experience Manager]中無法當作[!DNL Cloud Service]使用。 (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 您現在可以使用Automated forms conversion服務[將法文、德文和西班牙文PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=zh-Hant&#language-specific-meta-model)轉換為最適化表單。
* 範本編輯器新增個別面板，以顯示與最適化表單元件相關的錯誤。 它有助於在同一處整合所有最適化表單錯誤，並縮短解決時間。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hant) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

* **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

* **Acroform-based Document of Record**：您也可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=zh-Hant) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft® Azure資料存放區聯結器**：您現在可以[將表單資料模型連線至Microsoft® Azure儲存體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=zh-Hant)。 它可讓您擷取最適化表單資料，並將該資料作為BLOB儲存於Microsoft® Azure儲存體。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心元件v2
   * 簡化並改善PDP/PLP URL和SEO的設定
   * 在製作模式下分階段產品資料的視覺指示器，可更清楚顯示即將發生的變更
   * 內容和商務頁面的新Sitemap元件

* 支援[Adobe Commerce Sensei產品建議，由AEM Storefront中的Adobe Sensei](https://business.adobe.com/tw/products/magento/product-recommendations.html)提供技術支援，使用預先定義或即時建立的建議

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 錯誤修正 {#bug-fixes-screens}

* 內容提供者設定現在會在建立或更新期間驗證。

* 所有顯示檢視都有資料夾欄。

* 您可以展開Screens內容結構。

* `bulk-offline-update-service`缺少某些環境的所有許可權。

* 更新說明連結以符合新的screens cloud檔案。

* 現在可以解除指派播放清單，並禁止移除已指派播放器的播放清單。

* 清除「全部」快取時，播放器現在會重新下載Assets。

* 如果將&#x200B;*結束時間*&#x200B;設定為隔天，則重複排程現在有效。

* `Back&Forward`現在可在Screensas a Cloud ServiceUI中使用。

* 之前無法建立具有相同名稱但不同名稱空間的標籤。

## 適用於Experience Manageras a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

適用於Experience Manageras a Cloud Service的XML Documentation現已正式推出。 它可讓Experience Manager as a Cloud Service的客戶取得XML Documentation附加元件，以跨多個管道(包括Experience Manager Sites)匯入、建立、管理和傳遞技術內容。

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.7.0中Cloud Manager的發行說明

### 發行日期 {#release-cm-july}

AEM as a Cloud Service 2021.7.0中的Cloud Manager發行日期是2021年7月15日。
下一版本計畫於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客戶現在可以將 Azul 8 和 11 JDK 用於其 Cloud Manager 建置流程，也可以選擇將這些 JDK 之一用於與工具鏈相容的 Maven 外掛計劃&#x200B;*或*&#x200B;整個 Maven 流程執行。

* 輸出 IP 現在記錄於建置步驟記錄檔。

* 執行舊版AEM的階段和生產環境現在會回報&#x200B;**有可用的更新**&#x200B;的狀態。

* 支援的 SSL 憑證數量上限已增加到每個計劃 20 個。

* 可以設定的網域數量上限已增加到每個環境 500 個。

* 「**管理 Git**」按鈕已重新命名為「**存取 Git 資訊**」並更新此對話方塊。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 28。

### 錯誤修正 {#bug-fixes-cm-july}

* 在某些情況下，將 IP 允許清單繫結到環境時，預覽選項無法使用。

* 手動瀏覽到不存在執行的執行詳細資訊頁面不會顯示錯誤，只會不斷載入畫面。

* 當達到SSL憑證的最大數量時顯示的錯誤訊息沒有幫助。

* 在某些情況下，在&#x200B;**總覽**&#x200B;頁面中管道卡上顯示的發行版本可能存在差異。

* 新增計畫精靈誤指建立後無法變更名稱。

### 已知問題 {#known-issues-cm-july}

改用 Azul JDK 的客戶應了解，並非所有現有應用計劃都能在 Azul JDK 上順利編譯。Adobe建議您在切換前先在本機測試。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-july-cam}

Cloud Acceleration Manager的發行日期為2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager是雲端型應用程式，專為引導您的IT團隊進行從規劃到Cloud Service上線的轉換歷程所設計。 透過Adobe建議的最佳實務、秘訣、檔案和工具，協助進行AEM as aCloud Service歷程的每個階段，讓您的團隊成功進行移轉。 在[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=zh-Hant)瞭解更多資訊。

>[!NOTE]
>
> 檢視此[Cloud Acceleration Manager示範影片](https://video.tv.adobe.com/v/335547)。
