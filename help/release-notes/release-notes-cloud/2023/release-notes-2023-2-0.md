---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.2.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.2.0 版發行說明。'
exl-id: 671056e6-84cc-4c2c-bca3-fde68d5cc835
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: ht
source-wordcount: '731'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.2.0 版發行說明 {#release-notes}

以下章節會概述 [!DNL Experience Manager] as a Cloud Service 2023.2.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2021、2022 等版本。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2023.2.0) 的發行日期是 2023 年 4 月 12 日。下一個功能版本 (2023.4.0) 預計於 2023 年 6 月 7 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 2 月發行概觀影片，了解 2023.2.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 預先發佈的新功能 {#prerelease-sites}

* 將 AEM as a Cloud Service 中的內容片段匯出到 Adobe Target 作為 JSON 選件。
* 支援 GraphQL 分頁和排序，以及內部快取增強功能，現在可協助提升分離的用戶端應用程式在使用複雜 GraphQL 查詢和篩選器從 AEM 擷取大型內容集時的工作效能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 為 Dynamic Media 影片傳遞 (啟用 CMAF) 中的自適應串流推出的新通訊協定 (DASH - 基於 HTTP 的動態自適應串流) 支援：
   * 自適應串流 (DASH/HLS) 可確保使用者擁有更好的觀看影片體驗。
   * DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用
   * 在 NA 可使用，透過支援票證啟用，即將在 APAC、EMEA 推出

* 已新增對 WebP 影像的支援以自動擷取中繼資料、產生縮圖和自訂轉譯。這些檔案現在也支援智慧型標記和智慧型裁切功能。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[使用資料擷取核心元件以建置最適化表單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)**：[使用最適化表單編輯器](/help/forms/creating-adaptive-form-core-components.md)根據標準化的資料擷取元件 (核心元件) 建立表單。這些元件為您的數位註冊體驗提供自訂功能、縮短的開發時間並降低維護成本。

* **[前端管道支援設計以核心元件為基礎之最適化表單的樣式](/help/forms/using-themes-in-core-components.md)**：通過使用前端部署管道部署，為以核心元件為基礎之最適化表單使用標準化的 BEM 型主題，以增強表單的外觀和風格並符合您組織認可的品牌設計方針。

* **[為以核心元件為基礎的最適化表單產生記錄文件](/help/forms/generate-document-of-record-core-components.md)**：為使用核心元件建置的最適化表單，建立包含提交之資料的記錄文件，供一般使用者封存或參考，採列印或文件格式。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[使用儲存最適化表單做為範本功能高效建置表單](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：透過將現有的品牌認可表單儲存為表單範本以快速重複使用，促進和標準化表單開發工作。

* **[將 AEM Forms 連接至支援 JDBC 的資料庫](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：使用 JDBC 通訊協定直接從 AEM Cloud 服務連接至企業資料庫，而不需透過 REST API 公開它們。

* **[使用 Open API 3.0 整合 REST 端點](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：順暢地整合到支援 Open API 3.0 的記錄系統，以使用表單資料模型擷取資料。

* **[共用最適化表單以供審閱](/help/forms/create-reviews-forms.md)**：使用最適化表單審閱機制讓一個或多個審核者審閱表單。


### [!DNL Forms] 發行前版本的功能 {#prerelease-features-forms}

* **[將最適化表單提交至 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：提高商業使用者的敏捷性，可快速啟動新表單並將提交的資料儲存在他們日常使用的工具中，例如 Microsoft SharePoint 網站或 OneDrive 資料夾。

![將最適化表單提交至 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Headless 最適化表單早期採用者方案 {#forms-early-adopter}

使用 Headless 最適化表單讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 aem-forms-headless@adobe.com，即可加入早期採用者方案。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
