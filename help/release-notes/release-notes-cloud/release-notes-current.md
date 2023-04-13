---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前版本注意事項。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前版本注意事項。'
mini-toc-levels: 1
source-git-commit: 34313a984b8ddb76211ed97dd11c437cbefa90c2
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 33%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 目前版本注意事項 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能版本注意事項。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的版本注意事項；例如，2021、2022 等版本。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前的功能版本(2023.2.0)為2023年4月12日。 下一個功能版本(2023.4.0)預計於2023年5月4日發行。

## 發行影片 {#release-video}

請觀看2023年2月版本概述影片，以取得2023.2.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 預租 {#prerelease-sites}

* 從AEM as a cloud service匯出內容片段，以JSON選件Adobe目標。
* 支援GraphQL分頁和排序，以及內部快取增強功能，現在可協助您使用複雜的GraphQL查詢和篩選器從AEM擷取大型內容集時，改善去耦用戶端應用程式的效能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 針對Dynamic Media視訊傳送中的最適化串流（已啟用CMAF）推出全新通訊協定（DASH — 透過HTTP動態最適化串流）支援：
   * 最適化串流(DASH/HLS)可確保提供更佳的視訊使用者檢視體驗
   * DASH是自適應視頻流的國際標準協定，在業界得到廣泛採用
   * 適用於NA，即將在EMEA的APAC中推出支援票證，支援票證將予啟用

* 新增WebP影像支援，以自動擷取中繼資料、產生縮圖及自訂轉譯。 這些檔案現在也支援智慧標籤和智慧裁切功能。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[使用資料擷取核心元件以建置調適型表單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)**：[使用調適型表單編輯器](/help/forms/creating-adaptive-form-core-components.md)根據標準化的資料擷取元件 (核心元件) 建立表單。這些元件為您的數位註冊體驗提供自訂功能、縮短的開發時間並降低維護成本。

* **[基於樣式核心元件的前端管道支援自適應Forms](/help/forms/using-themes-in-core-components.md)**:透過前端部署管道部署核心元件適用性Forms，運用標準化的BEM型主題，增強表單的外觀和風格，並符合貴組織品牌認可的設計准則。

* **[產生核心元件適用性Forms的記錄檔案](/help/forms/generate-document-of-record-core-components.md)**:建立記錄檔案，其中包含使用核心元件建立的適用性Forms的已提交資料，以供封存或參考給使用者、列印或檔案格式。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[以「儲存最適化表單為範本」功能有效建立表單](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:將現有品牌認可的表單儲存為表單範本，以便快速重複使用，借此加快表單開發並標準化。

* **[將AEM Forms連接到JDBC支援的資料庫](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:使用JDBC通訊協定，直接從AEM雲端服務連線至企業資料庫，而無須透過REST API公開。

* **[使用Open API 3.0與REST端點整合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:無縫整合至支援Open API 3.0的記錄系統，以使用表單資料模型儲存和擷取資料。

* **[共用調適型表單以供審閱](/help/forms/create-reviews-forms.md)**：使用調適型表單審閱機制讓一個或多個審核者審閱表單。


### 中的功能 [!DNL Forms] 預發行 {#prerelease-features-forms}

* **[將適用性Forms提交至Microsoft SharePoint和Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**:提高商務使用者的靈活性，以快速啟動新表單，並將提交的資料儲存在他們使用的日常工具中，如Microsoft SharePoint網站或OneDrive資料夾。

![將適用性Forms提交至Microsoft SharePoint和Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## 無頭式適應性Forms早期採用者計畫 {#forms-early-adopter}

使用無頭式適用性Forms，讓開發人員可建立、發佈及管理可透過API存取及互動的互動式表單，而非透過傳統的圖形使用者介面。 無頭式最適化表單可協助您：

* 以您所選擇的程式設計語言建立高品質的多管道表單
* 將表單與您的案頭和行動應用程式、網站和聊天應用程式進行原生整合
* 在表單應用程式中重複使用專有的UI元件
* 運用Adobe Experience Manager Forms的力量

您可以從官方電子郵件ID發送電子郵件至aem-forms-headless@adobe.com，以加入早期採用者計畫。

## 維護版本注意事項 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護版本注意事項。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
