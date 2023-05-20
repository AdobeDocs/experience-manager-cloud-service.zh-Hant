---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0 版發行說明。'
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.1.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.1.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2021、2022 等版本。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 2023.1.0 功能版本的發行日期是 2023 年 2 月 9 日。下一個功能版本 (2023.2.0) 已計劃於 2023 年 4 月 12 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 1 月發行概觀影片，了解 2023.1.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 預先發佈 {#prerelease-features-sites}

* AEM GraphQL 內容傳遞 API 現在支援 GraphQL [分頁](/help/headless/graphql-api/content-fragments.md#paging)和[排序](/help/headless/graphql-api/content-fragments.md#sorting)，以提高擷取和呈現大型內容集的效率。GraphQL 分頁允許以子集傳回結果而非一次全部傳回來縮短查詢回應時間。GraphQL 排序允許按所需順序放置內容集，進而讓使用戶端應用程式更容易處理內容。AEM GraphQL 引擎中的混合篩選可進一步改進查詢回應時間。現在以與查詢篩選器相對應的較小集合的形式從 JCR 讀取內容。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 資產報告現在可讓管理員從 Experience Manager Assets as a Cloud Service 部署[產生資產下載報告](/help/assets/asset-reports.md)。此資料可進一步讓管理員從關鍵成功量度取得深入見解，以衡量企業內和客戶對資產的採用程度。

   ![其他格式的 PDF 轉譯](/help/release-notes/assets/choose_report.png)

* 除了在連接到 Azure Blob 儲存體資料來源以使用大量匯入工具擷取資產時支援用於驗證的存取金鑰之外，Experience Manager Assets 現在還[支援 SAS 權杖](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 改進 Asset Compute 中 CMYK 影像的管理，可讓您為 CMYK 影像產生智慧型裁切和智慧型標記。

### [!DNL Assets] 發行前版本的新功能 {#prerelease-features-assets}

* Experience Manager 資產現在支援使用大量匯入工具[從 Google Cloud Platform 大規模擷取資產](/help/assets/add-assets.md#asset-bulk-ingestor)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[可產生非互動式 PDF 文件和可列印輸出的工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md)**：使用 AEM 工作流程步驟，將業務流程的非互動式 PDF 文件和可列印輸出建立工作自動化，簡化您文件產生程序並節省時間。
* **[使用腳註在最適化表單中提供引述或額外資訊](/help/forms/footnotes-richtextsupport.md)**：在最適化表單中使用腳註來顯示有關如何完成或使用表單的資訊。您還可以使用它來提供附加資訊、版權許可和其他有用的資訊。

### [!DNL Forms] 發行前版本的新功能 {#prerelease-features-forms}

* **[使用資料擷取核心元件以建置最適化表單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)**：[使用最適化表單編輯器](/help/forms/creating-adaptive-form-core-components.md)根據標準化的資料擷取元件 (核心元件) 建立表單。這些元件為您的數位註冊體驗提供自訂功能、縮短的開發時間並降低維護成本。
* **[前端管道支援設計以核心元件為基礎之最適化表單的樣式](/help/forms/using-themes-in-core-components.md)**：通過使用前端部署管道部署，為以核心元件為基礎之最適化表單使用易於自訂的 BEM 型主題，以增強表單的外觀和風格。
* **[為以核心元件為基礎之最適化表單產產生記錄文件](/help/forms/generate-document-of-record-core-components.md)**：為以核心元件為基礎之最適化表單建立記錄，以提交供長期封存，採列印或文件格式。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[將最適化表單提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：簡化資料提交作業，能夠將最適化表單直接傳送到 Microsoft SharePoint 和 Microsoft OneDrive。您可以提交具結構描述的資料和無結構描述的資料。這些提交動作是對已經可用的提交動作的補充。
* **[使用將最適化表單另存為模板功能來提升表單建置效率](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：將最適化表單另存為模板，並在建置下一個最適化表單時重複使用模板，藉此簡化表單建置程序。
* **[連接 AEM Forms 到支援 JDBC 的資料庫](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：輕鬆將 AEM Forms 資料模式連接到支援 JDBC 的資料庫，讓您順暢讀寫資料。
* **[使用 Open API 3.0 與 REST 端點相整合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：將 AEM Forms as a Cloud Service 表單資料模式連接到支援 Open API 規格版格 3.0 的 REST 端點，讓您輕鬆傳送和接收資料。
* **[共用最適化表單以供審閱](/help/forms/create-reviews-forms.md)**：使用最適化表單審閱機制讓一個或多個審核者審閱表單。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE 可讓開發人員可以快速解決問題並在 AEM as a Cloud Service 部署新功能。

   快速開發環境是一種新型雲端環境，用於以快速、一致和可擴展的方式來驗證在本機運作的程式碼在雲端是否也能正常運作。使用命令列工具，可以快速將內容套件、套件組合、內容檔案、OSGI 設定或 Dispatcher 設定同步到 RDE。在下面的視訊中看到這個動作：

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   在 RDE 中成功驗證代碼後，鼓勵部署到雲端開發環境以執行 Cloud Manager 品質關卡，然後再透過生產管道部署到階段和生產環境。

   每個程序包括一個 RDE，並且可以選擇授權更多。

   >[!NOTE]
   >
   >RDE 將在接下來幾週內逐步推出；您可以發送電子郵件至 aemcs-rde-support@adobe.com 以跳到該行的前面。

* [擴展對伺服器端 API 存取代號的支援](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) – 您現在可以產生多個憑證，這有助於 API 具有不同特性的使用案例。現在也能以自助式方式撤銷憑證。

## 維護發行說明 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護發行說明。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
