---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.1.0版發行說明。」'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下章節概述的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service的2021.1.0是2021年2月3日。
下列版本(2021.2.0)將於2021年2月25日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增/更新及刪除內容片段變體的功能。

* **[用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md)**:可使用GraphQL語法查詢內容片段，以及根據內容片段模型的結構，以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/headless/security/authentication.md)**:可使用伺服器端API的存取權杖，驗證GraphQL API請求。

* 從GraphQL API增強JSON輸出，包括以JSON格式和地區設定輸出RTF。

* 支援巢狀內容片段模型，以允許透過專用的內容片段參考資料類型或內嵌在多行文字欄位中的內容片段參考，建立巢狀內容片段結構。

* 內容片段模型資料類型中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 可標籤內容片段模型，以及允許在資料夾中建立內容片段，並依標籤或路徑使用原則。

* 內容片段編輯器中的可用性增強功能，包括發佈動作和片段所依據之模型的顯示。

* 可在內容片段編輯器中直接預覽JSON輸出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a [!DNL Cloud Service] 延伸「智慧標籤」功能，以支援文字資產中關鍵字和實體的識別。 文字經識別、索引，並可作為中繼資料使用，以改善搜尋體驗，而無需任何設定。 請參閱 [智慧標籤](/help/assets/smart-tags.md).

* 現已支援MXF檔案格式。 請參閱 [支援的檔案格式](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：針對資產和體驗片段新增「商務」屬性標籤。 此索引標籤可讓您將產品/類別連結至資產和體驗片段。 索引標籤也會顯示連結產品/類別的即時資料，以及可在產品主控台中顯示詳細資料的連結。

* CIF Venia Reference Site - 2021.02.02已發佈，其中包含最新CIF核心元件1.7.0版。請參閱 [CIF Venia參考站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) 以取得更多詳細資訊。

* CIF核心元件1.7.0版已發行。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) 以取得更多詳細資訊。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM 2021.1.0中的Cloud Manageras a Cloud Service日期為2021年1月14日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* Assets生產例項有時可能會在 **環境** 詳細頁面 *待定* 而不允許使用者採取任何動作。

* 從Cloud Manager觸發解除休眠時，即使成功啟動解除休眠，有時也會顯示失敗訊息。

* 已解決在環境建立或刪除中遇到的罕見失敗案例。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本修正了AEM Dispatcher Converter和Repository Modernizer的錯誤，也支援新的公用程式Index Converter。 請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以深入了解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以取得更多詳細資訊。

* 新增功能至 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 建立獨立包 `ui.config` 以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* AEM Dispatcher轉換工具和Repository Modernizer工具上已完成數項錯誤修正。 請參閱 [AEM Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEMas a Cloud Service基礎 {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器對伺服器已驗證的API呼叫 — 產生適當的存取權杖，以在外部應用程式與AEMas a Cloud Service環境之間進行已驗證的伺服器對伺服器API呼叫。 閱讀以了解更多 [檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 或諮詢 [教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK建置分析器 {#sdk-build-analyzers}

AEMas a Cloud ServiceSDK建置Analyzer Maven外掛程式會偵測Maven專案中的問題，包括缺少相依性。 這可讓開發人員在本機開發期間，即可在使用Cloud Manager部署至雲端環境之前，先行探索問題。

已針對此版本新增兩個分析器：

* 重點分析器
* bundle-nativecode

如需詳細資訊，請參閱本檔案 [此處](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容轉移工具1.2.2版的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 內容轉移工具 — 使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID，作為內容移轉活動的一部分。 請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 以取得更多詳細資訊。
* 「內容轉移工具」現在會移轉移集中參考的所有群組和使用者，包括子項。
* 使用者可在下選取特定路徑 `/etc` 建立移轉集時。
