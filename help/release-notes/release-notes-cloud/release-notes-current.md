---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
mini-toc-levels: 1
source-git-commit: ffc3ba84630fe85d2b7e5a1f55aa71a2d978991c
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 19%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述目前（最新）版本的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2021、2022 等版本。
>
>查看 [Experience Manager發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant) 若要了解 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前的功能版本(2023.1.0)為2023年2月9日。 下一個功能版本(2023.2.0)預計於2023年3月30日推出。

## 發行影片 {#release-video}

請觀看2023年1月版本概述影片，以取得2023.1.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 預發行 {#prerelease-features-sites}

* AEM GraphQL內容傳送API現在支援GraphQL [分頁](/help/headless/graphql-api/content-fragments.md#paging) 和 [排序](/help/headless/graphql-api/content-fragments.md#sorting)，讓擷取和轉譯大型內容集更有效率。 GraphQL分頁可透過在子集中傳回結果，而非一次傳回所有結果，來改善查詢回應時間。 GraphQL排序可讓用戶端應用程式以所需順序排列內容集，更輕鬆處理內容。  AEM GraphQL引擎中的混合篩選可進一步改善查詢回應時間。 現在會從JCR讀取與查詢篩選器對應之較小集的內容。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 「資產報表」現在包含管理員 [產生資產下載報表](/help/assets/asset-reports.md) 從Experience Manager Assetsas a Cloud Service部署。 此資料可讓管理員從關鍵成功量度中獲得深入分析，以衡量企業內和客戶對資產的採用程度。

   ![其他格式的 PDF 轉譯](/help/release-notes/assets/choose_report.png)

* 除了在連接到 Azure Blob 儲存體資料來源以使用大量匯入工具擷取資產時支援用於驗證的存取金鑰之外，Experience Manager Assets 現在還[支援 SAS 權杖](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 改善Asset compute中CMYK影像的管理，讓您為CMYK影像產生智慧型裁切和智慧標籤。

### [!DNL Assets] 發行前版本的新功能 {#prerelease-features-assets}

* Experience Manager Assets現在支援 [從Google雲端平台大規模擷取資產](/help/assets/add-assets.md#asset-bulk-ingestor) 使用「批量導入」工具。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[生成非互動式PDF文檔和可打印輸出的工作流步驟](/help/forms/aem-forms-workflow-step-reference.md)**:使用AEM Workflow步驟，自動建立非互動式PDF文檔並輸出可打印的業務流程，從而簡化文檔生成流程並節省時間。
* **[使用腳注在適用性Forms中提供引證或額外資訊](/help/forms/footnotes-richtextsupport.md)**:在最適化表單中使用腳注，以顯示如何完成或使用表單的資訊。 您也可以用它來提供括弧資訊、版權權限和其他實用資訊。

### [!DNL Forms] 發行前版本的新功能 {#prerelease-features-forms}

* **[使用資料擷取核心元件來建立最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [使用適用性Forms編輯器](/help/forms/creating-adaptive-form-core-components.md) 根據標準化資料擷取元件（核心元件）建立表單。 這些元件可提供自訂功能、縮短開發時間，並降低數位註冊體驗的維護成本。
* **[基於樣式核心元件的前端管道支援自適應Forms](/help/forms/using-themes-in-core-components.md)**:透過前端部署管道部署核心元件的適用性Forms，運用可輕鬆自訂的BEM型主題，增強表單的外觀和風格。
* **[產生核心元件適用性Forms的記錄檔案](/help/forms/generate-document-of-record-core-components.md)**:在提交以供長期存檔、打印或文檔格式使用時，為核心元件建立基於最適化表單的記錄。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[將適用性Forms提交至Microsoft SharePoint和Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**:透過直接將適用性表單資料傳送至Microsoft SharePoint和Microsoft OneDrive的功能，簡化資料提交作業。 您可以提交結構型和無結構型資料。 這些提交操作除了現有的提交操作之外。
* **[以「儲存最適化表單為範本」功能有效建立表單](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:將最適化表單儲存為範本，並重複使用下一個最適化表單的範本，以簡化您的表單建立流程。
* **[將AEM Forms連接到JDBC支援的資料庫](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:輕鬆將您的AEM Forms資料模型連接到支援JDBC的資料庫，讓您能夠無縫地讀寫資料。
* **[使用Open API 3.0與REST端點整合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:將AEM Formsas a Cloud Service表單資料模型連線至支援Open API規格3.0版的REST端點，讓您輕鬆傳送和接收資料。
* **[共用最適化表單以供審核](/help/forms/create-reviews-forms.md)**:使用適用性Forms審核機制，允許一或多位審核者審核表單。


## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用體驗片段以動態的方式豐富產品清單 (例如：在產品列表之間放置橫幅)。
* 清單元件現在支援相關聯產品/類別頁面以動態顯示相關頁面。
* 已新增 Peregrine 12.5 元件的支援。
* 已新增對產品預告和輪播中用戶端價格載入的支援。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE可讓開發人員快速疑難排解問題，並在AEM as a Cloud Service上部署新功能。

   快速開發環境是新類型的雲端環境，旨在以快速、一致且可擴充的方式驗證本機運作的程式碼，且可在雲端中正常運作。 使用命令列工具，快速將內容套件、套件組合、內容檔案、OSGI設定或Dispatcher設定「同步」至RDE。 請觀看以下影片中的動作：

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   在RDE中成功驗證程式碼後，建議您先部署至雲端開發環境以執行Cloud Manager品質閘門，再透過生產管道部署至預備和生產環境。

   每個程式都包括一個RDE，並可選擇地許可更多。

   >[!NOTE]
   >
   >RDE將在未來幾週逐步推出；您可以發送電子郵件至aemcs-rde-support@adobe.com以跳到最前面。

* [延伸支援伺服器端API存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)  — 您現在可以產生多個憑證，這對API具有不同特性的情況非常有用。 現在也可以以自助方式撤銷證書。

## 維護髮行說明 {#maintenance}

您可以找到最新的維護髮行說明 [此處](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [這裡。](/help/implementing/cloud-manager/release-notes/current.md)

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
