---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 060956eee5136924263e4df5bd756670384e8365
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 57%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版（例如2021或2022）的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.4.0) 的發行日期為 2023 年 6 月 7 日。下一個功能版本 (2023.6.0) 預計於 2023 年 6 月 29 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 4 月發行概觀影片，以了解 2023.4.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 以JSON格式將內容片段從AEMas a Cloud Service匯出至Adobe Target，並在Target中建立對應的JSON選件。
* 支援 GraphQL 分頁和排序，以及內部快取增強功能，現在可協助提升分離的用戶端應用程式在使用複雜 GraphQL 查詢和篩選器從 AEM 擷取大型內容集時的工作效能。

### [!DNL Experience Manager Sites] 發行前版本的新功能 {#prerelease-sites}

* 內容片段及其參考資料現在可以發佈到 [AEM 預覽服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hant#access-preview-service) (使用[內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hant))，讓使用者在上線前可在分離的預覽應用程式上先預覽最終體驗。
* 現在可以使用AEM GraphQL在Headless案例中針對Web傳送動態最佳化影像。 [查詢變數](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) 可在GraphQL查詢中定義，以允許分離的使用者端應用程式從AEM請求對應的最佳化影像。
* 上的標籤 [內容片段變數](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) 現在可以使用AEM GraphQL內容傳送API輸出到JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 已新增對 WebP 影像的支援以自動擷取中繼資料、產生縮圖並自訂轉譯。這些檔案現在也支援智慧型標記功能。WebP 不支援將 Dynamic Media 功能用為輸入格式。

* [搜尋體驗增強功能](/help/assets/search-assets.md#aftersearch) - 您現在可以對搜尋結果中顯示的資產快速執行以下作業：

   * 建立工作流程
   * 建立版本
   * 建立資產關聯或取消關聯

     若要執行這些作業，您並不需要瀏覽至資產位置及檢視其屬性。

* 顏色搜尋面向的可用性改進 - 顏色值的輸入欄位現在為可編輯，搜尋結果只在您退出檢色器時才會更新。

* 推出新的通訊協定支援(DASH - Dynamic Adaptive Streaming over HTTP)，適用於Dynamic Media影片傳送中的最適化資料流（已啟用CMAF）：
   * 自適應串流 (DASH/HLS) 可確保更好的一般使用者觀看影片體驗
   * DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用
   * 「在所有區域提供」將透過支援票證啟用

* Dynamic Media _快照_  — 實驗測試影像或Dynamic Media URL，以檢視不同影像修飾元的輸出，並評估檔案大小（使用WebP和AVIF傳送）、網路頻寬和裝置畫素比的智慧型影像最佳化。 請參閱 [Dynamic Media 快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)。

### 中的功能 [!DNL Assets] 發行前 {#prerelease-feature-assets}

* Dynamic Media — 影像設定檔中某些智慧型裁切相關欄位的使用者介面現已更新，以反映定義智慧型裁切的目前准則。 另請參閱 [裁切選項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[將最適化Forms提交至Microsoft®SharePoint和Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：提高企業使用者的靈敏度，以便您快速啟動新表單，並將提交的資料儲存在日常使用的工具中，例如Microsoft®SharePoint網站或OneDrive資料夾。

### [!DNL Forms] 發行前版本的功能 {#prerelease-features-forms}

* [AEM 頁面編輯器中的最適化表單](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您現在可以使用 AEM 頁面編輯器快速建立多個表單，並將這些表單新增至您的 Sites 頁面。 此功能讓內容作者可使用最適化表單元件 (包括動態行為、驗證、資料整合、產生記錄文件和業務流程自動化) 的強大功能，在 Sites 頁面內建立順暢的資料擷取體驗。 您可以：

   * 將表單元件拖放到 AEM Sites 編輯器或體驗片段中的最適化表單容器元件，即可建立最適化表單。
   * 在AEM Sites編輯器中使用最適化Forms精靈，以便您可以建立獨立於任何Sites頁面的表單，讓您自由地在多個頁面中重複使用此類表單。
   * 將多個表單新增到 Sites 頁面，簡化使用者體驗並提供更大的靈活性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [增強的Adobe Acrobat Sign整合與合規性](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms現在與適用於政府的Adobe Acrobat Sign整合。 此整合針對政府相關帳戶（政府部門及機構）提交的最適化表單電子簽章，提供進階層級的法規遵循與安全性。

  與適用於政府的Adobe Acrobat Sign整合可讓Adobe的合作夥伴和政府客戶在Adaptive Forms中使用電子簽章，處理某些最關鍵和敏感的業務線。 此額外的安全層可確保所有電子簽章完全符合FedRAMP Moderate合規性，讓Adobe的政府客戶高枕無憂。

* 增強規則編輯器中自訂錯誤處理常式的錯誤處理功能。 您現在可以叫用自訂函式（使用使用者端資料庫）來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。 或者，您也可以針對服務傳回的錯誤採取特定動作。 例如，您可以在後端叫用自訂工作流程來取得特定錯誤代碼，或通知客戶服務已關閉。

  此功能引進了標準式錯誤回應，可回溯相容於OOTB錯誤處理常式，並擁有更大的彈性和控制能力，有助於改善您的整體錯誤處理能力。

### Headless 最適化表單早期採用者計劃 {#forms-early-adopter}

使用 Headless 最適化表單讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 運用Adobe Experience Manager Forms的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者計劃。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 額外發佈區域：除了主要區域外，Sites 客戶最多可授權三個發佈區域。流量會路由至其他發佈陣列，以降低特定請求的延遲，並增強抵禦區域中斷的能力。 如需授權您的計畫[額外發佈區域](/help/operations/additional-publish-regions.md)的資訊，請和您的 Adob&#x200B;&#x200B;e 客戶經理聯絡。

## 維護版本發行說明 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
