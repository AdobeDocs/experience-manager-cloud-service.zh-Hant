---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a 2020.11.0的Cloud Service發行說明。'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2020.11.0的發行日期為2020年12月2日。
下列版本(2020.12.0)將於2020年12月17日發行

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* **[啟動階層管](/help/sites-cloud/authoring/launches/managing-pages.md) 理與 [未來時間扭曲](/help/sites-cloud/authoring/launches/preview.md)**:新的UI可在啟動中新增/移除頁面，而具有時間扭曲的瀏覽網站會顯示啟動的未來狀態。

* **[延伸內容片段模型與編輯器](/help/assets/content-fragments/content-fragments-models.md)**:針對各種資料類型提供輸入驗證的新選項、具有新表單視覺效果的改良列舉資料類型，以及內容片段模型名稱可在資產UI中顯示並搜尋。

* **排序可轉出的即時副本頁面**:新選項，可使用名稱 [!UICONTROL 、上次修改]日期 [!UICONTROL 和上次轉出日期屬性來排序可轉]出的  Live Copy頁面。頁面的[!UICONTROL 上次轉出日期]為引進的新屬性。

## [!DNL Adobe Experience Manager Assets] 作為Cloud Service {#assets}

### [!DNL Assets]和[!DNL Dynamic Media] {#what-is-new-assets}中的新增功能

* **大量資產擷取**:為客戶提供可擴充的雲端原生擷取服務，其可運 [!DNL Experience Manager] 用為Cloud Service架構，包括資產微服務。主要使用案例包括透過監控、報告和排程大規模擷取，同時允許使用通用雲端上傳工具將資產初始傳輸至雲端資料存放區。 請參閱[資產大量擷取工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

   此工具適用於系統管理員、顧問或實作合作夥伴角色。 此功能可進行大規模擷取，最理想的作法是在初始擷取或偶爾大型擷取期間使用。 若是較小的擷取工作，請使用Assets使用者介面](/help/assets/add-assets.md#upload-assets)使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en)或[上傳。

   ![大量匯入工具的設定](/help/assets/assets/bulk-import-config-low-res.png)

* 使用者現在可以在「卡片」和「欄」檢視中排序數位資產。

   ![排序資產](/help/assets/assets/asset-sort-options.png)

* 在此版本中，對[!DNL Experience Manager Assets]的協助工具進行了下列增強。 如需詳細資訊，請參閱 [!DNL Assets]](/help/assets/accessibility.md)中的[協助功能。

   * 使用鍵盤導覽時間軸時，Esc鍵可折疊「全部顯示」選項，而不會失去焦點。
   * 使用鍵盤Tab鍵導覽時，從新增的標籤中移除最後一個標籤後，標籤欄位會保留焦點。
   * [!DNL Experience Manager] 元件現在包含螢幕助讀程式所使用之名稱、角色和值的適當資訊。
   * 刪除「類型/大小」組合框、「連結」組合框、「語言」組合框或「文本」編輯框後，鍵盤焦點將返回下一個或上一個用戶介面元素或更相關的用戶介面元素。
   * 將游標移至選項時，會顯示「選取」和「下載」等提示。 使用螢幕放大鏡的用戶可能看不到檔案縮圖，因為這些提示。 現在，使用`Escape`鍵移除選項後，可以保留焦點。
   * 從頁面中顯示的格線選取格線儲存格後，焦點會移至畫面上顯示的動作列。
   * 可視用戶可以區分普通文本和連結，因為在[!DNL Experience Manager]首頁中顯示指向所有解決方案的連結的視覺線索（下划線和>形箭頭表徵圖）。

* **Dynamic Media中的批次集預設集**:現在起，您可以在將資產檔案個別上傳至資料夾或使用大量擷取時，自動建立及組織影像集或回轉集中的多個資產。

   請參閱[關於批集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]現已提供下列協助工具增強功能：

   * 螢幕助讀程式（JAWS、講述人）提供「內嵌大小」功能表選項中功能表項目的名稱、角色和狀態旁白。
   * 使用者可使用`Tab`鍵導覽「電子郵件連結」對話方塊。
   * 由於螢幕助讀程式增強功能，建立視訊編碼設定檔的工作流程更方便使用。
   * 使用`Tab`鍵導覽時，焦點會移至工作流程中適當的使用者介面元素，以建立互動式視訊。
   * 「發佈」頁、「編輯資產」頁、「編輯智慧裁切」頁和「影像集編輯器」頁經過改進，以符合Web標準。 輔助技術(AT)使用者現在可以輕鬆導覽這些頁面，並採取動作，例如裁切影像。
   * 檢視器經過改良，可讓使用者使用鍵盤導覽。
   * 鍵盤和螢幕助讀程式的使用者可使用裁切功能。
   * 鍵盤用戶可以更好地管理熱點。

   請參閱 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)中的[輔助功能。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF Venia Reference Site - 2020.11.05版已發行，其中包含最新CIF核心元件v1.5.0版。如需詳細資訊，請參閱[CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* CIF核心元件v1.5.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) 。

### 錯誤修正 {#bug-fixes-commerce}

* 若未直接在Sling CA設定中指定設定，但在其中一個上層設定中指定，則GraphQL用戶端設定無法正確讀取。 此問題已修正。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as a Cloud Manager 2020.11.0Cloud Service的發行日期為2020年11月12日。

### [!DNL Cloud Manager] {#what-is-new-cm}中的新增功能

* 使用者現在可以從&#x200B;**Environments**&#x200B;卡片和&#x200B;**Environments**&#x200B;摘要頁面上的環境功能表選項，使用新的功能表選項&#x200B;**Local Login**。
如需詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 。

* Cloud Manager中的&#x200B;**Learn**&#x200B;標籤已透過UI中的新影像重新整理。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在建置執行前完成的相依性載入需要下載Maven外掛程式。
* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確位置。
* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 新增了根據「工作流程標題」、「工作流模型」、「狀態」、「發起人」、「裝載路徑」和「開始日期」搜尋工作流程例項的支援。 請參閱[搜尋工作流程例項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 發佈層用戶資料同步{#user-sync}

* 使用者資料（包括設定檔屬性和群組成員）可保存在發佈層級。 在[註冊、登入和使用者設定檔檔案](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中深入了解此功能。

### SDK建置分析器 {#analyzers}

AEM as a MavenCloud ServiceSDK Build Analyzer Maven Plugin可偵測Maven專案中的問題，包括缺少相依性。 這可讓開發人員在本機開發期間，即可在使用Cloud Manager部署至雲端環境之前，先行探索問題。 如需詳細資訊，請參閱以下檔案[,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)和[,](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新的[&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation)檢查在Cloud Manager建置期間執行的Apache和Dispatcher設定，也可以使用AEM作為Cloud ServiceSDK的Dispatcher工具來執行。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，了解[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 記錄檔的使用者體驗已改善。 提取和擷取記錄檔新增時間戳記。 已新增訊息，指出記錄是否空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果移轉集包含的路徑的檔案名稱部分相似，則「內容轉移工具」會略過內容檔案。 此問題已修正。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer的發行日期為2020年11月13日。

### [!DNL Best Practices Analyzer] {#what-is-new-bpa}中的新增功能

* Cloud Readiness Analyzer現在稱為Best Practices Analyzer(BPA)。 BPA會評估您目前AEM實作的最佳實務，並協助您評估從現有AEM例項移至AEM作為Cloud Service的準備程度。

* 已新增偵測器以偵測`java.io.InputStream`的使用，若在AEM中作為Cloud Service使用，可能會造成問題。

### 錯誤修正 {#bpa-bug-fixes}

* 已修正導致&#x200B;*textfield foundation*&#x200B;元件相關的正面錯誤。
