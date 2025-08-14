---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 版發行說明。'
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
feature: Release Information
role: Admin
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 95%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 2023.9.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.9.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2023.2.0) 的發行日期是 2023 年 9 月 28 日。 下一個功能版本 (2023.10.0) 計畫於 2023 年 10 月 26 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2023 年 9 月發行概觀影片，了解 2023.9.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEM Edge Delivery Services {#edge-delivery}

Edge Delivery 是一組可組合的新服務，著重在最大限度地發揮內容的影響，以便與客戶互動時能推動可衡量的業務成果。

了解更多關於 Edge Delivery Services 的文章：[這裡](/help/edge/overview.md)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

**將中繼資料表單指派至資料夾**

現在您可以將中繼資料表單指派到部署中的特定資料夾。然後，資料夾中的所有資產 (包括子資料夾中的資產) 將顯示被指派中繼資料表單中定義的屬性。

![將中繼資料表單指派至資料夾](/help/release-notes/assets/assign-to-folder.png)

### 管理員檢視中的新功能 {#admin-view-features}

* **將AEM Assets as a Cloud Service與Edge Delivery Services的檔案式製作整合**：將AEM Assets與Edge Delivery Services的檔案式製作整合，讓網站作者在Microsoft Word或Google Docs中製作檔案時，可以[使用AEM Assets存放庫中可用的影像](/help/edge/overview.md)。

* **擷取 ZIP 封存**：能夠選取在 Experience Manager 中管理的 ZIP 存檔，並可[將檔案直接擷取至 Experience Manager 中的檔案](/help/assets/manage-digital-assets.md#extract-zip-archives)無需下載。

  ![為群組釘選項目](/help/release-notes/assets/extract-archive.png)

### [!DNL Experience Manager Assets] 中可用的搶鮮版功能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media 中的影片現有多語言字幕和多語言音訊支援](/help/assets/dynamic-media/video.md#about-msma) - 您現在可以輕鬆地將多語字幕和多語言音訊新增至主要影片中。此功能表示全球觀眾都可以存取您的影片。您可以著手自訂一部已發佈的主要影片，以多種語言提供給全球觀眾，並遵守不同地理區域的無障礙指南。此外，作者還可以在使用者介面的單一標籤管理字幕和音軌。

  ![所選影片資產「屬性」頁面上的「字幕和音訊」標籤。](/help/release-notes/assets/msma-aem-cs.png)*所選影片資產「屬性」頁面上的「字幕和音訊」標籤。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* [**Google reCAPTCHA 企業支援**](/help/forms/captcha-adaptive-forms-core-components.md)：以最適化表單使用 Google reCAPTCHA 企業版，以針對詐欺活動和垃圾郵件提供增強的保護，進而提供更安全的使用者體驗。透過進階的風險分析和緊密整合，真實的使用者可輕鬆地提交表單，同時有效地封鎖機器人。

* [**Adobe Analytics 與表單的 Experience Cloud Setup Automation**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)：您現在只需輕按幾個按鈕，即可啟用 Adobe Analytics 和 Experience Cloud Setup Automation。這能讓您將 AEM Forms as a Cloud Service 與 Experience Platform 標籤和 Adobe Analytics 連接，以擷取和追蹤已發佈表單的效能指標。

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**適用於最適化表單的 Adobe Analytics 報告範本**](/help/forms/view-understand-aem-forms-analytics-reports.md)：Forms as a Cloud Service 現在提供 Adobe Analytics 報告 OOTB。這可幫助您輕鬆了解表單的效能。表單層級的量度可讓您深入了解表單在多個關鍵績效指標 (KPI) 上的表現，例如呈現、訪客、提交、平均填寫時間。透過追蹤使用者行為和意見回饋，您可以識別表單中造成混亂的部份，並指引表單設計和功能的改善。

  ![最適化表單使用者參與 Adobe Analytics 報告](/help/forms/assets/forms-analytics-report.png)

* **[以核心元件為主的最適化表單中的表單片段](/help/forms/adaptive-form-fragments-core-components.md)**：告別重複的資料、最佳化您的數位庫存，並可改善協作，同時還可使用表單片段提升表單建構體驗。這些可重複使用的元件無縫整合至到多種表單中，簡化了一致且具有專業外觀的表單建立。表單片段透過「一次變更，處處反映」功能確保可重複性、標準化和品牌一致性。由於在一處進行的更新會自動傳播到使用這些片段的所有表單，因此可體驗更高的可維護性和效率。

* **[更佳的 Adobe Sign 工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign 工作流程步驟經過改善，其中包括：
   * **Adobe Sign 以政府核發 ID 為主的驗證**：Adobe Acrobat Sign 以政府核發 ID 為主的驗證允許使用者使用政府核發的 ID (駕駛執照、國民身份證、護照) 驗證其身份，進而提供更多的驗證防護層。此增強功能利用受信任的身分識別文件為簽名過程額外增加一層可信度，使其成為需要增強安全性、合規性和使用者驗證等情境的理想選擇。

   * **Adobe Sign 文件的稽核軌跡**：使用稽核軌跡功能詳細了解 Adobe Sign 文件的生命週期。透過稽核軌跡，您現在可以保留與文件相關的所有動作和互動的全面記錄。其中包括查看、編輯或簽署文件等人員的詳細資訊，以及每個事件的時間戳記。此加強功能對於維持合規性、解決爭議和確保數位協議的完整性至關重要。

   * **協議收件者的新角色不僅僅是簽署人**：Adobe Acrobat Sign 可以選擇將協議收件人的角色擴展到簽署人之外，這樣更可符合其工作流程要求。啟用後，每位協議收件人有其可設定的個別角色，且以簽署人為預設。

* **通訊 API 中的頁數支援**：現在，除了透過通訊 API 擷取文件之外，您還可以接收有關文件內所含頁數的重要資訊。

* **[使用規則編輯器中的自訂錯誤處理常式發生錯誤處理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：您現在可以呼叫自訂函數來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。

* **[AEM Forms Designer 64 位元版本](/help/forms/installing-configuring-designer.md)**：AEM Forms Designer 64 位元版本在效能、可擴充性和記憶體管理方面更為提升，以增強您的表單建立體驗。透過 64 位元架構，您可以輕鬆處理更大、更複雜的專案，確保設計工作流程流暢和最佳效率。透過這最先進的版本，提升您的表單設計能力並擁抱 AEM Forms Designer 的未來。

### 早期採用計劃 {#forms-early-adopter}

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

* **[Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=zh-Hant)**：使用 Headless 最適化表單讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

   * 使用您選擇的程式語言建置高品質的多管道表單
   * 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
   * 在表單應用程式中重複使用您的專屬 UI 元件
   * 使用 Adobe Experience Manager Forms 的強大功能

  使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者方案。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 行銷活動相關 URL 參數的新 CDN 快取行為 {#cache-url-params}

針對新環境，CDN預設會移除行銷相關查詢引數，以提高行銷活動效能和快取命中率。 既有環境不受影響。[了解更多](/help/implementing/dispatcher/caching.md#marketing-parameters)。

### 流量篩選規則 (包括 WAF 規則) 早期採用者計劃 {#waf-early-adopter}

在 CDN 篩選流量的根據：

* 要求的標頭和屬性 (例如 IP 位址)
* 已知和惡意流量相關的流量模式

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 **aemcs-waf-adopter@adobe.com**，深入了解有關早期採用者方案的資訊。名額有限。

若要深入了解該功能，請點選[這裡](/help/security/traffic-filter-rules-including-waf.md)參閱文章。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
