---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版發行說明。'
description: "[!DNL Adobe Experience Manager]個2020.11.0as a Cloud Service發行說明。"
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager]as a Cloud Service的發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]as a Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.11.0版的發行日期為2020年12月2日。
下列版本(2020.12.0)將於2020年12月17日發行

## [!DNL Adobe Experience Manager Sites]個as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[啟動階層管理](/help/sites-cloud/authoring/launches/managing-pages.md)與[未來時間扭曲](/help/sites-cloud/authoring/launches/preview.md)**：新的UI可在啟動項中新增/移除頁面，而且使用Timewarp瀏覽網站會顯示啟動項的未來狀態。

* **[擴充的內容片段模型與編輯器](/help/assets/content-fragments/content-fragments-models.md)**：針對各種資料型別的輸入驗證新增選項、透過新表單視覺效果改善的列舉資料型別，以及可在Assets UI中顯示及搜尋內容片段模型名稱。

* **排序可用於轉出的即時副本頁面**：使用[!UICONTROL 名稱]、[!UICONTROL 上次修改日期]和[!UICONTROL 上次轉出日期]屬性來排序可用於轉出的即時副本頁面的新選項。 頁面的[!UICONTROL 上次轉出日期]是引入的新屬性。

## [!DNL Adobe Experience Manager Assets]個as a Cloud Service {#assets}

### [!DNL Assets]和[!DNL Dynamic Media]的新增功能 {#what-is-new-assets}

* **大量資產擷取**：為客戶提供使用[!DNL Experience Manager]as a Cloud Service架構（包括資產微服務）的可擴充、雲端原生擷取服務。 主要使用案例包括大規模內嵌與監控、報告和排程，同時允許使用通用雲端上傳工具將資產初始傳輸到雲端資料存放區。 請參閱[資產大量擷取器工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

  此工具適用於系統管理員、顧問或實作合作夥伴角色。 此功能可進行大規模擷取，最好在初始擷取或偶爾大量擷取期間使用。 對於較小的內嵌工作，請使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)或使用Assets使用者介面[&#128279;](/help/assets/add-assets.md#upload-assets)的上傳。

  ![大量匯入工具的設定](/help/assets/assets/bulk-import-config-low-res.png)

* 使用者現在可以在卡片檢視和欄檢視中排序數位資產。

  ![排序資產](/help/assets/assets/asset-sort-options.png)

* 此版本中的[!DNL Experience Manager Assets]已針對協助工具完成下列增強功能。 如需詳細資訊，請參閱 [!DNL Assets][&#128279;](/help/assets/accessibility.md)中的協助工具功能。

   * 使用鍵盤導覽時間軸時，Esc鍵可以摺疊「全部顯示」選項而不會失去焦點。
   * 使用鍵盤Tab鍵導覽時，從新增的標籤中移除最後一個標籤後，標籤欄位會保持焦點。
   * [!DNL Experience Manager]元件現在包含熒幕朗讀程式使用的名稱、角色和值的適當資訊。
   * 刪除「型別/大小」下拉式方塊、「連結」下拉式方塊、「語言」下拉式方塊或「文字」編輯方塊後，鍵盤焦點會回到下一個或上一個使用者介面元素，或是更相關的使用者介面元素。
   * 將指標暫留在選項上時，會顯示如「選取」和「下載」等提示。 由於這些秘訣，使用熒幕放大鏡的使用者可能無法看到檔案縮圖。 現在，使用`Escape`鍵移除選項後，可以保留焦點。
   * 從頁面中顯示的網格選取網格儲存格時，焦點會移至熒幕上顯示的動作列。
   * 視覺使用者可以區分一般文字和連結，因為[!DNL Experience Manager]首頁會顯示所有解決方案的連結的視覺提示（底線和>形箭號圖示）。

* **Dynamic Media中的批次集預設集**：現在您可以單獨或使用大量擷取將資產檔案上傳至資料夾時，自動建立及組織影像集或迴轉集中的多個資產。

  請參閱[關於批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]現已提供下列協助工具增強功能：

   * 熒幕助讀程式（JAWS、朗讀程式）會在「內嵌大小」選單選項中講述選單專案的名稱、角色和狀態。
   * 使用者可以使用`Tab`鍵瀏覽電子郵件連結對話方塊。
   * 有了熒幕助讀程式的增強功能，建立視訊編碼設定檔的工作流程會更方便使用。
   * 使用`Tab`鍵導覽時，焦點會移至工作流程中的適當使用者介面元素，以建立互動式視訊。
   * Publish頁面、編輯資產頁面、編輯智慧型裁切頁面和影像集編輯器頁面均已改善以符合Web標準。 輔助技術(AT)使用者現在可以輕鬆地導覽這些頁面，並在這些頁面上執行動作，例如裁切影像。
   * 檢視器經過改良，讓使用者能使用鍵盤導覽。
   * 鍵盤和熒幕助讀程式的使用者可以使用裁切功能。
   * 鍵盤使用者可以更妥善地管理熱點。

  檢視 [!DNL Dynamic Media][&#128279;](/help/assets/dynamic-media/accessibility-dm.md)中的協助工具。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia Reference Site - 2020.11.05，其中包含最新CIF核心元件1.5.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* 已發行CIF Core Components v1.5.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)。

### 錯誤修正 {#bug-fixes-commerce}

* 未直接在Sling CA設定中指定（但在其中一個父設定中指定）設定時，GraphQL使用者端設定無法正確讀取。 此問題已修正。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as a Cloud Service 2020.11.0 中的 Cloud Manager 發行日期是 2020 年 11 月 12 日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 使用者現在可以從&#x200B;**環境**&#x200B;卡片和&#x200B;**環境**&#x200B;摘要頁面上的環境功能表選項中使用新的功能表選項&#x200B;**本機登入**。
如需更多詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* **學習** Cloud Manager 中的索引標籤已在 UI 中使用新圖像進行了刷新。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在構建執行之前完成的依賴項加載需要下載 Maven 插件。
* Cloud Manager 頁腳中用於選擇語言的鏈接現在將瀏覽到正確的位置。
* 有時在程式碼掃描過程中，SonarQube 進程不會啟動。現在將自動檢測到這並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已新增根據工作流程標題、工作流程模型、狀態、發起人、裝載路徑和開始日期來搜尋工作流程例項的支援。 請參閱[搜尋工作流程執行個體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### Publish層級使用者資料同步 {#user-sync}

* 使用者資料（包括設定檔屬性和群組成員）可儲存於發佈層級。 在[註冊、登入和使用者個人檔案檔案](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中進一步瞭解此功能。

### SDK建置分析器 {#analyzers}

AEM as a Cloud Service SDK Build Analyzer Maven外掛程式會偵測maven專案中的問題，包括遺漏的相依專案。 它讓開發人員有機會在本機開發期間以及使用Cloud Manager部署到雲端環境之前發現問題。 如需詳細資訊，請參閱檔案[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html#developing)和[這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html#building-for-the-sdk)。

### 其他 {#others-foundation}

針對在Cloud Manager建置期間執行的Apache和Dispatcher設定，新增了[&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation)檢查，這些設定也可以使用AEM as a Cloud Service SDK的Dispatcher工具執行。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，瞭解[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改善記錄的使用者體驗。 擷取和內嵌記錄檔中新增的時間戳記。 已新增訊息，以指出記錄檔是否為空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果移轉集包含具有部分類似檔案名稱的路徑，則內容轉移工具會略過內容檔案。 此問題已修正。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer的發行日期為2020年11月13日。

### [!DNL Best Practices Analyzer] 的新增功能 {#what-is-new-bpa}

* Cloud Readiness Analyzer現在更名為Best Practices Analyzer (BPA)。 BPA會評估您目前AEM實作的最佳實務，並協助您評估從現有AEM例項移至AEM as a Cloud Service的準備程度。

* 已新增偵測器來偵測`java.io.InputStream`的使用，若在AEM as a Cloud Service中使用可能會造成問題。

### 錯誤修正 {#bpa-bug-fixes}

* 已修正造成與&#x200B;*textfield foundation*&#x200B;元件相關之正向的錯誤。
