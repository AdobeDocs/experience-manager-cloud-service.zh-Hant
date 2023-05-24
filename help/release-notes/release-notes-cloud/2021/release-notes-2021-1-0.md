---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] 2021.1.0版as a Cloud Service發行說明」。'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 15%

---


# [!DNL Adobe Experience Manager]as a Cloud Service 版發行說明 {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.1.0為2021年2月3日。
下列版本(2021.2.0)將於2021年2月25日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：新增使用HTTP API新增/更新和刪除內容片段變體的功能。

* **[用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md)**：能夠使用GraphQL語法和根據內容片段模型的結構描述查詢內容片段，以產生JSON格式的輸出。

* **[GraphQL API要求的驗證支援](/help/headless/security/authentication.md)**：能夠使用伺服器端API的存取權杖來驗證GraphQL API請求。

* 增強GraphQL API的JSON輸出，包括輸出JSON格式和地區設定的豐富文字的功能。

* 對巢狀內容片段模型的支援，允許透過專用內容片段參考資料型別或內嵌在多行文字欄位中的內容片段參考來建立巢狀內容片段結構。

* 內容片段模式資料型別中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 標籤內容片段模型，以及允許在包含原則（依標籤或路徑）的資料夾中建立內容片段的功能。

* 內容片段編輯器中的可用性增強，包括發佈動作和顯示片段所依據的模型。

* 直接在內容片段編輯器中預覽JSON輸出的功能。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a [!DNL Cloud Service] 擴充智慧標籤功能，以支援文字型資產中的關鍵字和實體識別。 無需任何設定，即可識別文字、編制其索引並使其成為中繼資料，以改善搜尋體驗。 另請參閱 [智慧標籤](/help/assets/smart-tags.md).

* 現在支援MXF檔案格式。 另請參閱 [支援的檔案格式](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：資產和體驗片段的新「商務」屬性。 此索引標籤可讓您將產品/類別連結到資產和體驗片段。 此索引標籤也會顯示連結的產品/類別的即時資料，以及在產品主控台中顯示詳細資訊的連結。

* 已發行CIF Venia Reference Site - 2021.02.02，其中包含最新CIF Core Components v1.7.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) 以取得更多詳細資料。

* 已發行CIF Core Components v1.7.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) 以取得更多詳細資料。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as a Cloud Service 2021.1.0 中的 Cloud Manager 發行日期是 2021 年 1 月 14 日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* Assets Production 實例有時可能會在&#x200B;**環境**&#x200B;詳情頁為&#x200B;*待辦的*&#x200B;不允許使用者採取任何行動。

* 從 Cloud Manager 觸發解除休眠時，即使解除休眠成功啟動，有時也會顯示失敗消息。

* 解決了在環境建立或刪除過程中遇到的罕見失敗案例。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此外掛程式的最新版本包含AEM Dispatcher Converter和Repository Modernizer的錯誤修正，並支援新的公用程式Index Converter。 請參閱 [整合式體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以進一步瞭解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為與AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以取得更多詳細資料。

* 新增功能至 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 會建立個別的封裝 `ui.config` 以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* 對AEM Dispatcher Converter和Repository Modernizer工具進行的多項錯誤修正。 請參閱 [AEM Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEMas a Cloud Service基礎 {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器對伺服器驗證的API呼叫 — 產生適當的存取權杖，以在您的外部應用程式和AEMas a Cloud Service環境之間執行經過驗證的伺服器對伺服器API呼叫。 閱讀以瞭解更多資訊 [說明檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 或透過諮詢 [教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK建置分析器 {#sdk-build-analyzers}

AEMas a Cloud ServiceSDK Build Analyzer Maven外掛程式會偵測Maven專案中的問題，包括遺漏的相依性。 它讓開發人員有機會在本機開發期間以及使用Cloud Manager部署到雲端環境之前發現問題。

已為此版本新增兩個新分析器：

* repoinit分析器
* bundle-nativecode

如需詳細資訊，請參閱檔案 [此處](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.2.2的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 內容轉移工具新增功能和UI — 使用者對應工具。 此功能會在內容移轉活動中，自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID。 請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 以取得更多詳細資料。
* 內容轉移工具現在會移轉在移轉集內參考的所有群組和使用者（包括子項）。
* 允許使用者選取底下的特定路徑 `/etc` 建立移轉集時。
