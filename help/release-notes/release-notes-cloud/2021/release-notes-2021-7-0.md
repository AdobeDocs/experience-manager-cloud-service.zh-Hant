---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.7.0 版發行說明。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 21%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本期(2021.7.0)是2021年7月29日。
以下版本(2021.8.0)是2021年8月26日。

## 發佈視頻 {#release-video}

看看 [2021年7月發佈概述](https://video.tv.adobe.com/v/335580) 視頻，瞭解添加的功能的摘要。

## Experience Manager基金會as a Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更靈活的調度程式配置：項目可以更容易地組織。 例如，現在可以包括多個反映站點結構的重寫規則檔案。 [瞭解](/help/implementing/dispatcher/disp-overview.md#validation-debug) 此靈活模式，包括如何構建調度程式配置以利用它。
* 應將複製代理的「分發」頁籤下的樹複製UI視為已棄用，並計畫在9月30日後刪除。 [瞭解](/help/operations/replication.md#tree-activation) 替代複製策略。
* 捆綁 `org.apache.sling.datasource-1.0.4.jar` 已刪除Sling資料源支援，因為它具有過時的功能且客戶未使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 內容自動化功能允許 [!DNL Experience Manager Assets] 利用 [!DNL Adobe Creative Cloud] API，可實現資產生產的自動化。 它通過顯著減少建立同一資產變體所花費的時間和所需的迭代來提高內容速度。 該功能不需要任何寫程式，可在DAM內工作。 請參閱 [使用Creative Cloud整合生成資產變動](/help/assets/cc-api-integration.md)。

* [!DNL Experience Manager Assets] 包括 [!DNL Document Cloud] PDF查看器以本機方式預覽PDF文檔。 此功能允許用戶預覽多頁PDF檔案，而不需要任何檔案處理或轉換。 此功能改進了奇偶校驗 [!DNL Experience Manager] 6.5查看器中可用的控制項包括縮放、導航到頁面、取消停靠控制項和全屏查看。 用戶案例還預覽並跳轉到頁面和書籤。 支援對檔案本身的注釋，在將來的發行版中將添加對PDF檔案內內容的注釋和注釋。

   ![預覽PDF檔案 [!DNL Experience Manager] 使用PDF查看器](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下載功能使用非同步下載來提高下載速度。 請參閱 [下載使用連結共用共用的資產](/help/assets/download-assets-from-aem.md#link-share-download)。

   ![下載收件箱](/help/assets/assets/download-inbox.png)

* 視圖設定將得到增強，以便用戶選擇預設視圖和預設排序參數。

   ![在中設定預設視圖 [!UICONTROL 查看設定]](/help/assets/assets/view-settings-for-defaults.png)

* 用戶可以根據屬性謂詞搜索和篩選資料夾。

   ![使用搜索謂詞篩選搜索資料夾](/help/assets/assets/search-folders-via-predicates.png)

### 中提供的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 當您將數字資產作為連結共用時，用戶可以將URL複製到剪貼簿。 增強功能使您能夠以更快、更方便的方式共用資產。

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` 在中不可用 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 (CQ-4326322)

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* 您現在可以使用 Automated Forms Conversion 服務[將法文、德文和西班牙文 PDF Forms 轉換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)成最適化表單。
* 範本編輯器新增個別面板，以顯示與最適化表單元件相關的錯誤。它有助於在同一處整合所有最適化表單錯誤，並縮短解決時間。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 該服務允許您以同步模式生成文檔。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

* **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

* **Acroform-based Document of Record**：您也可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心元件v2
   * PDP/PLP URL和SEO的簡化和改進配置
   * 在創作模式下用於分段產品資料的可視指示器，以更好地查看即將進行的更改
   * 用於內容和商業頁面的新站點地圖元件

* 支援 [Adobe CommerceSensei產品推薦，由Adobe Sensei提供支援](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM店面中使用預定義或即時建立的建議

## [!DNL Experience Manager Screens] 作為 [!DNL Cloud Service] {#screens}

### 錯誤修正 {#bug-fixes-screens}

* 現在，內容提供程式設定將在建立或更新期間驗證。

* 所有顯示視圖都包含資料夾列。

* 可以展開「螢幕內容結構」。

* `bulk-offline-update-service` 缺少某些環境的所有權限。

* 已更新幫助連結以匹配新螢幕雲文檔。

* 取消分配播放清單，並禁止刪除分配了播放器的播放清單，現在可以。

* 播放器現在在清除「全部」快取時重新下載資產。

* 如果 *結束時間* 已設定為以後的日。

* `Back&Forward` 現在在螢幕as a Cloud ServiceUI中工作。

* 無法以前建立名稱相同但命名空間不同的標籤。

## XML DocumentationExperience Manageras a Cloud Service {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

XML Documentation的Experience Manageras a Cloud Service一般可以獲得。 它允許Experience Manageras a Cloud Service客戶購買XML Documentation的附件，以跨多個渠道(包括Experience Manager Sites)導入、建立、管理和交付技術內容。

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.7.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-cm-july}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年7月15日。
下一版計畫於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客戶現在能夠將Azul 8和11 JDK用於其Cloud Manager生成過程，並可以選擇將其中一個JDK用於與工具鏈相容的Maven插件 *或* 整個Maven進程的執行。

* 出站出口IP現在將記錄在生成步驟日誌檔案中。

* 運行舊版本的階段和生產環AEM境現在將報告 **可用更新**。

* 支援的最大SSL證書已增加到每個程式20個。

* 可配置的最大域數已增加到每個環境的500個。

* 的 **管理Git** 按鈕已重新命名為 **訪問Git資訊** 對話框已直觀刷新。

* Cloud Manager使用的AEMProject Archetype版本已更新為版本28。

### 錯誤修正 {#bug-fixes-cm-july}

* 在某些情況下，將IP允許清單綁定到環境時，「預覽」不可用。

* 手動導航到非現有執行的執行詳細資訊頁面未顯示錯誤，只顯示無休止的載入螢幕。

* 達到最大SSL證書數時顯示的錯誤消息無用。

* 在某些情況下，在上面的管道卡中顯示的版本版本可能不一致 **概述** 的子菜單。

* 添加程式嚮導錯誤地指出建立後無法更改名稱。

### 已知問題 {#known-issues-cm-july}

切換使用阿祖爾JDK的客戶應該知道，並非所有現有應用程式都會在阿祖爾JDK上進行編譯，而且不會出錯。 強烈建議在切換前在本地test。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-july-cam}

Cloud Acceleration Manager的發佈日期為2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager是基於雲的應用程式，旨在指導您的IT團隊從規劃到Cloud Service生活的整個過渡過程。 通過Adobe建議的最佳實踐、提示、文檔和工具，為成功遷移建立團隊，以便在遷移過程的每個階段都提供AEMCloud Service幫助。 瞭解更多資訊 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en)。

>[!NOTE]
>
> 檢查此 [Cloud Acceleration Manager演示視頻](https://video.tv.adobe.com/v/335547)。
