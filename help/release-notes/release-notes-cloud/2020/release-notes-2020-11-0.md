---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 作為2020.11.0的雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: c0db892d58f762bd5659596371ece86950e9cdd7
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]做為雲端服務的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為雲服務2020.11.0的發行日期為2020年12月2日。
下列版本(2020.12.0)將於2020年12月17日發行

## [!DNL Adobe Experience Manager Sites] 雲端服務  {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* **[啟動階層管理](/help/sites-cloud/authoring/launches/managing-pages.md) 與未 [來時間彎曲](/help/sites-cloud/authoring/launches/preview.md)**:新的UI可在啟動中新增／移除頁面，而具有「時間彎曲」的瀏覽網站則會顯示啟動的未來狀態。

* **[延伸內容片段模型與編輯器](/help/assets/content-fragments/content-fragments-models.md)**:針對各種資料類型提供新的輸入驗證選項、改良的列舉資料類型及新的表單視覺化，以及「資產」使用者介面中顯示和可搜尋的內容片段模型名稱。

* **排序可開始使用的即時副本頁面**:新選項，可使用「名稱」、「上次修改日期」和「上次轉出日期屬性 [!UICONTROL 」來排序可]轉出的「即時復   制」頁面。頁面的[!UICONTROL 上次推出日期]是引入的新屬性。

## [!DNL Adobe Experience Manager Assets] 雲端服務  {#assets}

### [!DNL Assets]和[!DNL Dynamic Media] {#what-is-new-assets}的新增功能

* **大量資產擷取**:為客戶提供可擴充的雲端原生擷取服務，此服務可運 [!DNL Experience Manager] 用為雲端服務架構，包括資產微服務。主要使用案例包括透過監控、報告和排程大規模擷取，同時允許使用通用雲端上傳工具將資產初始傳輸至雲端資料存放區。 請參閱[資產大量內嵌工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

   此工具適用於系統管理員、顧問或實施合作夥伴角色。 此功能可進行大規模攝取，最理想地用於初始攝取或偶爾大量攝取。 對於較小的擷取工作，請使用「資產」使用者介面](/help/assets/add-assets.md#upload-assets)使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en)或[上傳。

   ![批量匯入程式的設定](/help/assets/assets/bulk-import-config-low-res.png)

* 使用者現在可以在「卡片」和「欄」檢視中排序數位資產。

   ![排序資產](/help/assets/assets/asset-sort-options.png)

* 本版次針對[!DNL Experience Manager Assets]的協助功能進行下列增強功能。 如需詳細資訊，請參閱 [!DNL Assets]](/help/assets/accessibility.md)中的[協助功能。

   * 使用鍵盤導覽時間軸時，Esc鍵可以收合「全部顯示」選項，而不會失去焦點。
   * 使用鍵盤標籤鍵導覽時，從新增的標籤中移除最後一個標籤後，標籤欄位會保留焦點。
   * [!DNL Experience Manager] 元件現在包含螢幕閱讀程式使用之名稱、角色和值的適當資訊。
   * 刪除「類型／大小」組合框、「連結」組合框、「語言」組合框或「文本」編輯框後，鍵盤焦點將返回下一個或上一個用戶介面元素或更相關的用戶介面元素。
   * 當將指標暫留在選項上時，會顯示「選取」和「下載」等提示。 使用螢幕放大鏡的使用者可能看不到檔案縮圖，因為這些提示。 現在，在使用`Escape`鍵移除選項後，可以保留焦點。
   * 從頁面中顯示的格線選取格線儲存格後，焦點會移至螢幕上顯示的動作列。
   * 視覺使用者可區分一般文字和連結，因為在[!DNL Experience Manager]首頁中會顯示所有解決方案的連結視覺線索（底線和雪佛龍圖示）。

* **動態媒體中的批次集預設集**:現在，您可以在個別或使用大量擷取將資產檔案上傳至檔案夾時，自動建立和組織影像集或回轉集中的多個資產。

   請參閱[關於批集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]現在提供下列協助工具增強功能：

   * 螢幕閱讀程式（JAWS，旁白）會在「內嵌大小」功能表選項中，為功能表項目的名稱、角色和狀態加上旁白。
   * 使用者可使用`Tab`鍵來導覽「電子郵件連結」對話方塊。
   * 由於螢幕閱讀程式增強功能，建立視訊編碼設定檔的工作流程更易於使用。
   * 使用`Tab`鍵導覽時，焦點會移至工作流程中適當的使用者介面元素，以建立互動式視訊。
   * 「發佈」頁、「編輯資產」頁、「編輯智慧裁切」頁和「影像集編輯器」頁已經過改良，以符合Web標準。 協助技術(AT)使用者現在可以輕鬆導覽這些頁面，並採取像是裁切影像等動作。
   * 檢視器已改良，可讓使用者使用鍵盤進行導覽。
   * 鍵盤和螢幕閱讀程式使用者可使用裁切功能。
   * 鍵盤用戶可以更好地管理熱點。

   請參閱 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)中的[輔助功能。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 發佈的CIF Venia參考網站- 2020.11.05，其中包含最新的CIF核心元件v1.5.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* 已發佈CIF核心元件v1.5.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)。

### 錯誤修正 {#bug-fixes-commerce}

* 當Sling CA設定中未直接指定設定，但是父組態中的一個設定時，GraphQL用戶端設定無法正確讀取。 這個問題已經修正。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM中Cloud Manager作為雲端服務2020.11.0的發行日期為2020年11月12日。

### [!DNL Cloud Manager] {#what-is-new-cm}的新增功能

* 現在，用戶可從&#x200B;**Environments**&#x200B;卡和&#x200B;**Environments**&#x200B;摘要頁上的環境菜單選項獲得新的菜單選項&#x200B;**本地登錄**。
有關詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md##login-locally)。

* Cloud Manager中的&#x200B;**Learn**&#x200B;標籤已在UI中以新影像重新整理。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在建立執行前載入的相依性需要下載Maven外掛程式。
* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確的位置。
* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已新增支援根據「工作流程標題」、「工作流程模型」、「狀態」、「啟動器」、「裝載路徑」和「開始日期」來搜尋工作流程例項。 請參閱[搜尋工作流程例項](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 發佈層用戶資料同步{#user-sync}

* 使用者資料（包括描述檔屬性和群組成員資格）可保存在發佈層。 在[註冊、登入和使用者設定檔檔案](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中進一步瞭解此功能。

### SDK Build Analyzers {#analyzers}

AEM as a Cloud Service SDK Build Analyzer Maven Plugin會偵測主要專案中的問題，包括缺少相依性。 它為開發人員提供了在本機開發期間發現問題的機會，而遠在使用Cloud Manager部署至雲端環境之前。 如需詳細資訊，請參閱說明檔案[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)和[這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新的[&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation)檢查Cloud Manager建置期間執行的apache和dispatcher組態，此組態也可以使用AEM作為Cloud Service SDK的Dispatcher Tools來執行。

## 內容轉移工具 {#content-transfer-tool}

請依照本節內容，瞭解[內容傳輸工具](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改善記錄檔的使用者體驗。 已新增時間戳記至擷取和擷取記錄檔。 新增訊息，指出記錄檔是否空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果遷移集包含具有部分相似檔案名的路徑，則內容傳輸工具正在跳過內容檔案。 這個問題已經修正。

## 最佳做法分析器{#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器的發行日期是2020年11月13日。

### [!DNL Best Practices Analyzer] {#what-is-new-bpa}的新增功能

* Cloud Readiness Analyzer現在是最佳做法分析器(BPA)。 BPA提供您目前AEM實作的最佳實務評估，並協助評估從現有AEM例項移至AEM（雲端服務）的準備程度。

* 已新增偵測器來偵測`java.io.InputStream`的使用，若在AEM中當做雲端服務使用，可能會造成問題。

### 錯誤修正 {#bpa-bug-fixes}

* 修正造成&#x200B;*textfield foundation*&#x200B;元件相關的錯誤。
