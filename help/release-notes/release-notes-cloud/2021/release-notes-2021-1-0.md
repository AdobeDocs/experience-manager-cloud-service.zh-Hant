---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a 2021.1.0的Cloud Service發行說明。'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.1.0的發行日期為2021年2月3日。
下列版本(2021.2.0)將於2021年2月25日發行。

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增/更新及刪除內容片段變體的功能。

* **[用於內容片段傳送的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:可使用GraphQL語法查詢內容片段，以及根據內容片段模型的結構，以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:可使用伺服器端API的存取權杖，驗證GraphQL API請求。

* 從GraphQL API增強JSON輸出，包括以JSON格式和地區設定輸出RTF。

* 支援巢狀內容片段模型，以允許透過專用的內容片段參考資料類型或內嵌在多行文字欄位中的內容片段參考，建立巢狀內容片段結構。

* 內容片段模型資料類型中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 可標籤內容片段模型，以及允許在資料夾中建立內容片段，並依標籤或路徑使用原則。

* 內容片段編輯器中的可用性增強功能，包括發佈動作和片段所依據之模型的顯示。

* 可在內容片段編輯器中直接預覽JSON輸出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] 延伸智 [!DNL Cloud Service] 慧標籤功能，以支援文字資產中關鍵字和實體的識別。文字經識別、索引，並可作為中繼資料使用，以改善搜尋體驗，而無需任何設定。 請參閱[智慧標籤](/help/assets/smart-tags.md)。

* 現已支援MXF檔案格式。 請參閱[支援的檔案格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：針對資產和體驗片段新增「商務」屬性標籤。 此索引標籤可讓您將產品/類別連結至資產和體驗片段。 索引標籤也會顯示連結產品/類別的即時資料，以及可在產品主控台中顯示詳細資料的連結。

* CIF Venia Reference Site - 2021.02.02版已發行，其中包含最新CIF核心元件1.7.0版。如需詳細資訊，請參閱[CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* CIF核心元件v1.7.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) 。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as aCloud Service2021.1.0中的Cloud Manager發行日期為2021年1月14日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* Assets生產例項有時會將&#x200B;**Environments**&#x200B;詳細資料頁面上的Brand Portal狀態顯示為&#x200B;*Pending*，而不允許使用者採取任何動作。

* 從Cloud Manager觸發解除休眠時，即使成功啟動解除休眠，有時也會顯示失敗訊息。

* 已解決在環境建立或刪除中遇到的罕見失敗案例。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}中的新增功能

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本修正了AEM Dispatcher Converter和Repository Modernizer的錯誤，也支援新的公用程式Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以深入了解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為AEM，作為相容Cloud Service的OAK索引定義。 有關詳細資訊，請參閱[Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，可建立獨立的套件`ui.config`以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* AEM Dispatcher轉換工具和Repository Modernizer工具上已完成數項錯誤修正。 請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

## AEM as a Cloud Service基礎{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器對伺服器已驗證的API呼叫 — 產生適當的存取權杖，以在外部應用程式與AEM(作為Cloud Service環境)之間進行已驗證的伺服器對伺服器API呼叫。 閱讀[檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或參閱[教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)以深入了解。

### SDK建置分析器{#sdk-build-analyzers}

AEM as a MavenCloud ServiceSDK Build Analyzer Maven Plugin可偵測Maven專案中的問題，包括缺少相依性。 這可讓開發人員在本機開發期間，即可在使用Cloud Manager部署至雲端環境之前，先行探索問題。

已針對此版本新增兩個分析器：

* 重點分析器
* bundle-nativecode

如需詳細資訊，請參閱[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)的檔案。

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容轉移工具1.2.2版的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}中的新增功能

* 內容轉移工具 — 使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID，作為內容移轉活動的一部分。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 。
* 「內容轉移工具」現在會移轉移集中參考的所有群組和使用者，包括子項。
* 建立移轉集時，允許使用者在`/etc`下選取特定路徑。
