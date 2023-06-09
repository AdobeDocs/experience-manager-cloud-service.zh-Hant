---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: d9c5934c03b9c5aa91bafa09569d441fc7868937
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 39%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2021、2022 等版本。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2023.4.0)為2023年6月7日。 下一個功能版本 (2023.6.0) 計畫預計於 2023 年 6 月 29 日發行。

## 發行影片 {#release-video}

請觀看2023年4月版本概觀影片，瞭解2023.4.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 將 AEM as a Cloud Service 中的內容片段匯出到 Adobe Target 作為 JSON 選件。
* 支援 GraphQL 分頁和排序，以及內部快取增強功能，現在可協助提升分離的用戶端應用程式在使用複雜 GraphQL 查詢和篩選器從 AEM 擷取大型內容集時的工作效能。

### 中的新功能 [!DNL Experience Manager Sites] 預約 {#prerelease-sites}

* 內容片段及其參考現已可發佈至 [AEM預覽服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) 使用 [內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en)，可讓使用者在離線的預覽應用程式上線前預覽最終體驗。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 已新增對 WebP 影像的支援以自動擷取中繼資料、產生縮圖和自訂轉譯。這些檔案現在也支援智慧標籤功能。 WebP不支援Dynamic Media功能作為輸入格式。

* [搜尋體驗增強功能](/help/assets/search-assets.md#aftersearch)  — 您現在可以對搜尋結果中顯示的資產快速執行下列操作：

   * 建立工作流程
   * 建立新版本
   * 建立資產關聯或取消關聯

     您不需要導覽至資產位置並檢視其屬性，即可執行這些作業。

* 色彩搜尋Facet可用性改善 — 現在可編輯色彩值的輸入欄位，且搜尋結果僅會在您退出檢色器時更新。

* 為 Dynamic Media 影片傳遞 (啟用 CMAF) 中的自適應串流推出的新通訊協定 (DASH - 基於 HTTP 的動態自適應串流) 支援：
   * 自適應串流 (DASH/HLS) 可確保更好的一般使用者觀看影片體驗
   * DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用
   * 可在所有區域使用，透過支援票證啟用

* Dynamic Media _快照_  — 實驗測試影像或Dynamic Media URL，以檢視不同影像修飾元的輸出，以及針對檔案大小（使用WebP和AVIF傳送）、網路頻寬和裝置畫素比的智慧型影像最佳化。 另請參閱 [Dynamic Media快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[將最適化表單提交至 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：提高商業使用者的敏捷性，可快速啟動新表單並將提交的資料儲存在他們日常使用的工具中，例如 Microsoft SharePoint 網站或 OneDrive 資料夾。

### [!DNL Forms] 發行前版本的功能 {#prerelease-features-forms}

* [增強的Adobe Acrobat Sign整合與合規性](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms現在與適用於政府的Adobe Acrobat Sign整合，針對政府相關帳戶（政府部門及機構）提交的最適化表格內容，提供電子簽章高階的合規與安全性。

  與適用於政府的Adobe Acrobat Sign整合可讓我們的合作夥伴和政府客戶在Adaptive Forms中使用電子簽章，處理某些最關鍵和敏感的業務線。 此額外的安全層可確保所有電子簽章完全符合FedRAMP Moderate合規性，讓我們的政府客戶高枕無憂。

* [AEM頁面編輯器中的最適化Forms](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您現在可以使用AEM頁面編輯器快速建立多個表單並新增至您的網站頁面。 此功能可讓內容作者運用最適化表單元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面內建立順暢的資料擷取體驗。 您可以：

   * 建立最適化表單，方法是拖放表單元件至AEM Sites編輯器或體驗片段中的最適化Forms容器元件。
   * 在AEM Sites編輯器中使用最適化Forms精靈來建立獨立於任何Sites頁面的表單，為您提供在多個頁面中重複使用這類表單的自由。
   * 新增多個表單至Sites頁面，精簡使用者體驗並提供更大的彈性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* 增強規則編輯器中自訂錯誤處理常式的錯誤處理功能：您現在可以叫用自訂函式（使用使用者端程式庫）來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應，或針對服務傳回的錯誤採取特定動作。 例如，您可以在後端叫用自訂工作流程來取得特定錯誤代碼，或通知客戶服務已關閉。

  這有助於改善整體錯誤處理能力，因為引進了標準化的錯誤回應，可回溯相容於OOTB錯誤處理常式，並擁有更大的彈性和控制能力。

### Headless 最適化表單早期採用者計劃 {#forms-early-adopter}

使用 Headless 最適化表單讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 利用 Adobe Experience Manager Forms 的強大功能

您可以傳送電子郵件至 `aem-forms-headless@adobe.com` 從您的正式電子郵件ID加入早期採用者計畫。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 其他發佈區域：除了主要區域外，客戶最多可授權三個發佈區域。 流量會路由至其他發佈陣列，以降低特定請求的延遲，並增強抵禦區域中斷的能力。 如需授權的相關資訊，請聯絡您的Adobe客戶經理 [其他發佈區域](/help/operations/additional-publish-regions.md) 您的程式。

## 維護版本發行說明 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
