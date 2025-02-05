---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0 版發行說明。'
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
feature: Release Information
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.4.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.4.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
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

* 將 AEM as a Cloud Service 中的內容片段以 JSON 格式匯出到 Adobe Target，並在 Target 中建立對應的 JSON 產品建議。
* 支援 GraphQL 分頁和排序，以及內部快取增強功能，現在可協助提升分離的用戶端應用程式在使用複雜 GraphQL 查詢和篩選器從 AEM 擷取大型內容集時的工作效能。

### [!DNL Experience Manager Sites] 發行前版本的新功能 {#prerelease-sites}

* 內容片段及其參考資料現在可以發佈到 [AEM 預覽服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html#access-preview-service) (使用[內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html))，讓使用者在上線前可在分離的預覽應用程式上先預覽最終體驗。
* 現在可以使用 AEM GraphQL 在 Headless 情境下，動態最佳化影像以進行 Web 傳遞。[查詢變數](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html#query-variables)可以在 GraphQL 查詢中定義，以允許分離的用戶端應用程式相應地要求 AEM 中的最佳化影像。
* 現在可以使用 AEM GraphQL 內容傳遞 API 將[內容片段變化](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html)上的標記輸出至 JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 已新增對 WebP 影像的支援以自動擷取中繼資料、產生縮圖並自訂轉譯。這些檔案現在也支援智慧型標記功能。WebP 不支援將 Dynamic Media 功能用為輸入格式。

* [搜尋體驗增強功能](/help/assets/search-assets.md#aftersearch) - 您現在可以對搜尋結果中顯示的資產快速執行以下作業：

   * 建立工作流程
   * 建立版本
   * 建立資產關聯或取消關聯

     若要執行這些作業，您並不需要瀏覽至資產位置及檢視其屬性。

* 顏色搜尋面向的可用性改進 - 顏色值的輸入欄位現在為可編輯，搜尋結果只在您退出檢色器時才會更新。

* 為 Dynamic Media 影片傳遞 (啟用 CMAF) 中的自適應串流推出新的通訊協定支援 (DASH - 基於 HTTP 的動態自適應串流)：
   * 自適應串流 (DASH/HLS) 可確保使用者擁有更好的觀看影片體驗。
   * DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用
   * 「在所有區域提供」將透過支援票證啟用

* Dynamic Media _快照_ - 對測試影像或 Dynamic Media URL 進行實驗，以查看不同影像修飾元的輸出，並針對檔案大小 (使用 WebP 和 AVIF 傳遞)、網路頻寬和裝置像素比來評估智慧型影像最佳化。請參閱 [Dynamic Media 快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)。

### [!DNL Assets] 發行前版本的功能 {#prerelease-feature-assets}

* Dynamic Media - 影像設定檔中一些與智慧型裁切相關之欄位的使用者介面現已更新，以反映定義智慧型裁切的最新指引。請參閱[裁切選項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html#crop-options)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* **[將最適化表單提交至 Microsoft® SharePoint 和 Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：改善商業使用者的敏捷性，以便快速啟動新表單並將提交的資料儲存在日常使用的工具中，例如 Microsoft® SharePoint 網站或 OneDrive 資料夾。

### [!DNL Forms] 發行前版本的功能 {#prerelease-features-forms}

* [AEM 頁面編輯器中的最適化表單](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您現在可以使用 AEM 頁面編輯器快速建立多個表單，並將這些表單新增至您的 Sites 頁面。此功能讓內容作者可使用最適化表單元件 (包括動態行為、驗證、資料整合、產生記錄文件和業務流程自動化) 的強大功能，在 Sites 頁面內建立順暢的資料擷取體驗。您可以：

   * 將表單元件拖放到 AEM Sites 編輯器或體驗片段中的最適化表單容器元件，即可建立最適化表單。
   * 使用 AEM Sites 編輯器中的最適化表單精靈，以便建立不屬於任何 Sites 頁面的表單，讓您能夠在多個頁面之間自由地重複使用這些表單。
   * 將多個表單新增到 Sites 頁面，簡化使用者體驗並提供更大的彈性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [適用於政府機關的 Adobe Acrobat Sign Solutions](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms 現在與適用於政府機關的 Adobe Acrobat Sign Solutions 整合。這種整合能夠讓政府相關帳戶 (政府部門和機構) 在提交最適化表單時，享有等級更高的電子簽名合規性和安全性。

  藉由與政府適用之 Adobe Acrobat Sign 整合，在一些最重要的關鍵任務和敏感業務線，Adobe 的合作夥伴和政府客戶便可以在最適化表單使用電子簽名。這額外一層的安全性可確保所有電子簽名完全符合 FedRAMP 中等合規性，讓 Adobe 的政府客戶安心使用。

* 使用規則編輯器中的自訂錯誤處理常式增強錯誤處理：您現在可以呼叫自訂函數 (使用用戶端資料庫) 來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。

  此功能有助於引進標準型錯誤回應來提高整體的錯誤處理能力；這些回應向後相容於 OOTB 錯誤處理常式，且具有更大的彈性和控制性。

### Headless 最適化表單早期採用者方案 {#forms-early-adopter}

使用 Headless 最適化表單讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者方案。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 額外發佈區域：除了主要區域外，Sites 客戶最多可授權三個發佈區域。流量會路由到其他發佈伺服器陣列，因此可降低某些要求的延遲，並增進發生區域性中斷時的復原能力。如需授權您的方案[額外發佈區域](/help/operations/additional-publish-regions.md)的資訊，請和您的 Adobe 客戶經理聯絡。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
