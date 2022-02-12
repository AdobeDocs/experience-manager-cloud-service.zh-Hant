---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service2021.1.0發行說明。'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: 44b24a68e2b9a9abd2a9d609c3a28f6b90e492fa
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.1.0是2021年2月3日。
以下版本(2021.2.0)將於2021年2月25日發佈。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加/更新和刪除內容片段變體的功能。

* **[用於內容片段傳遞的GraphQL API](/help/headless/graphql-api/content-fragments.md)**:能夠使用GraphQL語法和基於內容片段模型的架構查詢內容片段，以便以JSON格式輸出。

* **[GraphQL API請求的身份驗證支援](/help/headless/security/authentication.md)**:能夠使用伺服器端API的訪問令牌驗證GraphQL API請求。

* GraphQL API的增強JSON輸出，包括以JSON格式和區域設定輸出富格文本的能力。

* 支援嵌套內容片段模型，以允許通過多行文本欄位中的專用內容片段引用資料類型或內容片段引用內聯建立嵌套的內容片段結構。

* 內容片段模型資料類型中提供的其他驗證規則，包括「唯一」、「必需」和「可翻譯」。

* 功能標籤內容片段模型，並允許在資料夾中按標籤或路徑建立包含策略的內容片段。

* 內容片段編輯器中的可用性增強功能，包括發佈操作和片段所基於模型的顯示。

* 能夠直接在內容片段編輯器中預覽JSON輸出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] 作為 [!DNL Cloud Service] 擴展了智慧標籤功能，以支援基於文本的資產中的關鍵字和實體的標識。 文本被識別、索引，並被作為元資料提供，以改進搜索體驗，而不需要任何配置。 請參閱 [智慧標籤](/help/assets/smart-tags.md)。

* 現在支援MXF檔案格式。 請參閱 [支援的檔案格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：「資產」和「體驗片段」的新「商業」屬性頁籤。 此頁籤使您能夠將產品/類別連結到資產和體驗片段。 該頁籤還顯示連結產品/類別的即時資料，以及在產品控制台中顯示詳細資訊的連結。

* 已發佈CIF Venia參考站點 — 2021.02.02，包括最新的CIF核心元件版本v1.7.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) 的子菜單。

* 已發佈CIF核心元件v1.7.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) 的子菜單。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年1月14日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 資產生產實例可能會在以下日期顯示Brand Portal狀態： **環境** 詳細資訊頁面 *待定* 不允許用戶採取任何操作。

* 從雲管理器觸發去休眠時，即使成功啟動去休眠時，有時也會顯示失敗消息。

* 已解決在建立或刪除環境時遇到的極少數故障。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 已發佈新版本的AIO-CLI插件。 此插件的最新版本包括Dispatcher Converter和Repository Modernizer的AEM錯誤修復程式，並且還支援新的實用程式 — 索引轉換器。 請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 瞭解有關此插件的詳細資訊。

* 索引轉換器是一種實用程式，可用於將客戶的自定義OAK索引定義轉換為AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 的子菜單。

* 添加到的新功能 [儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 建立單獨的包 `ui.config` 包含所有OSGi配置。

### 錯誤修正 {#crt-bug-fixes}

* 在Dispatcher Converter和Repository Modernizer工具上執AEM行了幾個錯誤修復。 請參閱 [調度AEM器轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

## AEMas a Cloud Service {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器到伺服器已驗證的API調用 — 生成適當的訪問令牌，以便在外部應用程式和as a Cloud Service環境之間進行經驗證的伺服器到伺服器APIAEM調用。 通過閱讀瞭解更多資訊 [文檔](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 或者通過咨詢 [教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)。

### SDK生成分析器 {#sdk-build-analyzers}

as a Cloud ServiceAEMSDK生成分析器Maven插件可檢測給定項目中的問題，包括缺少依賴項。 它為開發人員提供了在本地開發過程中發現問題的機會，而且遠在使用Cloud Manager部署到雲環境之前。

已為此版本添加了兩個新分析器：

* 重點分析儀
* 束 — nativecode

有關詳細資訊，請參閱文檔 [這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.2的發佈日期為2021年2月1日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 新功能和UI已添加到內容傳輸工具 — 用戶映射工具。 此功能會自動將現有用戶和組映射到其AdobeIdentity Management系統ID，作為內容遷移活動的一部分。 請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 的子菜單。
* 內容傳輸工具現在可以遷移遷移集中引用的所有組和用戶，包括子代。
* 允許用戶在 `/etc` 建立遷移集時。
