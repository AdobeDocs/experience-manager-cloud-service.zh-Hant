---
title: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
translation-type: tm+mt
source-git-commit: 3aff98256eb26176bca52a49286bf2853290b5ef
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 2%

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

AEM中Cloud Manager作為Cloud Service 2020.12.0的發行日期為2020年12月10日。

### [!DNL Cloud Manager] {#what-is-new-cm}的新增功能

* [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)的自助服務管理。

* [IP允許清單的自助管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 更新的&#x200B;**環境**&#x200B;詳細資訊頁面現在允許用戶管理其環境中的自定義域名和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在代碼掃描階段發生的某些故障，但未提供解決結果。

* 環境卡未一致顯示&#x200B;**Add**&#x200B;按鈕。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已新增支援根據「工作流程標題」、「工作流程模型」、「狀態」、「啟動器」、「裝載路徑」和「開始日期」來搜尋工作流程例項。 請參閱[搜尋工作流程例項](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 發佈層用戶資料同步{#user-sync}

* 使用者資料（包括描述檔屬性和群組成員資格）可保存在發佈層。 在[註冊、登入和使用者設定檔檔案](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中進一步瞭解此功能。

### SDK Build Analyzers {#analyzers}

AEM as a Cloud Service SDK Build Analyzer Maven Plugin會偵測主要專案中的問題，包括缺少相依性。 它為開發人員提供了在本機開發期間發現問題的機會，而遠在使用Cloud Manager部署至雲端環境之前。 如需詳細資訊，請參閱說明檔案[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)和[這裡](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新的[&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation)檢查Cloud Manager建置期間執行的apache和dispatcher組態，此組態也可以使用AEM作為Cloud Service SDK的Dispatcher Tools來執行。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}的新增功能

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本包含AEM Dispatcher Converter和Repository Modernizer的錯誤修正，也支援新的公用程式- Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以進一步瞭解此外掛程式。

* Index Converter是一個公用程式，可用來將客戶的自訂OAK索引定義轉換為AEM，做為CLoud Service相容的OAK索引定義。
有關詳細資訊，請參閱[索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，可建立個別的套件`ui.config`以包含所有OSGi組態。

### 錯誤修正 {#crt-bug-fixes}

* 在AEM Dispatcher Converter和Repository Modernizer工具上完成數個錯誤修正。
請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。