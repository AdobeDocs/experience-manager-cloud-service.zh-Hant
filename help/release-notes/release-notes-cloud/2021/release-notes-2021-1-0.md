---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 作為2021.1.0的Cloud Service發行說明。'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
translation-type: tm+mt
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節將[!DNL Experience Manager]的一般發行說明概述為Cloud Service。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.1.0的發行日期為2021年2月3日。
下列版本(2021.2.0)將於2021年2月25日發行。

## [!DNL Adobe Experience Manager Sites] Cloud Service  {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增／更新和刪除內容片段變數的能力。

* **[內容片段傳送的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能夠使用GraphQL語法查詢內容片段，並根據內容片段模型來結構，以便以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能夠使用伺服器端API的存取Token來驗證GraphQL API請求。

* 從GraphQL API增強JSON輸出，包括以JSON格式和地區設定輸出豐富型文字的功能。

* 支援巢狀內容片段模型，以允許透過多行文字欄位中的專屬內容片段參考資料類型或內容片段參考，建立巢狀內容片段結構。

* 內容片段模型資料類型中提供的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 可標籤內容片段模型，並允許在資料夾中依標籤或路徑建立內容片段原則。

* 內容片段編輯器中的可用性增強功能，包括發佈動作和片段所依據的模型顯示。

* 可直接在內容片段編輯器中預覽JSON輸出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] 延伸「 [!DNL Cloud Service] 智慧標籤」功能，以支援在文字型資產中識別關鍵字和實體。文字會被識別、建立索引，並可做為中繼資料使用，以改善搜尋體驗，而不需進行任何設定。 請參閱[智慧型標籤](/help/assets/smart-tags.md)。

* 現在支援MXF檔案格式。 請參閱[支援的檔案格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager商務Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：資產和體驗片段的新「商務」屬性標籤。 此標籤可讓您將產品／類別連結至資產和體驗片段。 此標籤也會顯示連結產品／類別的即時資料，以及在產品主控台中顯示詳細資料的連結。

* 發佈的CIF Venia參考網站- 2021.02.02，其中包含最新的CIF核心元件1.7.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* 已發佈CIF核心元件v1.7.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager作為2021.1.0Cloud ServiceAEM的發行日期為2021年1月14日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 資產生產實例有時可能會將&#x200B;**環境**&#x200B;詳細資訊頁面上的品牌入口網站狀態顯示為&#x200B;*待定*，而不允許使用者採取任何動作。

* 從Cloud Manager觸發解除休眠時，有時即使成功啟動解除休眠，仍會顯示失敗訊息。

* 已解決在環境建立或刪除中遇到的罕見故障。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}的新增功能

* 新版AIO-CLI增效模組已發行。 此插件的最新版本包括Dispatcher Converter和Repository Modernizer的錯AEM誤修正，還支援新的實用程式- Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以進一步瞭解此外掛程式。

* Index Converter是一個實用程式，可用於將客戶的自定義OAK索引定義轉換為AEMCloud Service相容的OAK索引定義。 有關詳細資訊，請參閱[索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，可建立個別的套件`ui.config`以包含所有OSGi組態。

### 錯誤修正 {#crt-bug-fixes}

* 在Dispatcher Converter和Repository Modernizer工具AEM上完成的幾個錯誤修正。 請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[ Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

## 作AEM為Cloud Service基金會{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器對伺服器的已驗證API呼叫——產生適當的存取Token，以便在外部應用程式之間以及作為Cloud Service環境進行已驗證的伺服器AEM對伺服器API呼叫。 閱讀[說明檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或參閱[教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)，瞭解更多資訊。

### SDK Build Analyzers {#sdk-build-analyzers}

作為AEMCloud ServiceSDK Build Analyzer Maven Plugin可檢測主項目中的問題，包括缺少依賴項。 它為開發人員提供了在本機開發期間發現問題的機會，而遠在使用Cloud Manager部署至雲端環境之前。

此版本新增了兩個分析器：

* 重點分析器
* bundle-nativecode

如需詳細資訊，請參閱說明檔案[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.2的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}的新增功能

* 內容傳輸工具——使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其Adobe的Identity Management系統ID，做為內容移轉活動的一部分。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容傳輸工具現在會移轉移移集（包括子系）中參考的所有群組和使用者。
* 在建立遷移集時，允許用戶選擇`/etc`下的某些路徑。
