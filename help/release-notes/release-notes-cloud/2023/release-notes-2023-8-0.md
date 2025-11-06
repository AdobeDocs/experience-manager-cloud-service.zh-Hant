---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0 版發行說明。'
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.8.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.8.0 版的功能發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.8.0) 的發行日期為 2023 年 8 月 31 日。下一個功能版本 (2023.9.0) 預計於 2023 年 9 月 28 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 8 月發行概觀影片，了解 2023.8.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* [內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hant)現在可讓使用者檢視標記，並依據作為中繼資料套用於內容片段的標記進行搜尋。使用者即不必再為了此功能而切換到資產 UI，減少了內容切換並提高了效率。

  ![在內容片段主控台中進行標記](/help/assets/content-fragments-console-tags.png)
* 新的內容片段編輯器現已在 AEM as a Cloud Service 上提供。此編輯器可簡化內容作者的製作工作，並減少他們編輯內容時在不同應用程式之間切換的需要，進而讓內容作者能夠提高工作效率。
  ![最新內容片段編輯器](/help/release-notes/assets/newCFEditor.png)

最新內容片段編輯器可提供原來編輯器所沒有的以下優點：

* 可自動儲存並提高製作效率，以及防止編輯內容意外遺失。
* 內容片段及其引用的階層式檢視，可使用樹狀結構在深度結構化片段中快速導航。
  ![內容片段編輯器內的樹狀結構](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 以內容參考進行內聯上傳資產，無需先將其上傳到資產 DAM
* 內容片段提供的呈現體驗臨時預覽，可幫助作者在前端應用程式上以視覺方式查看內容的外觀
* 一鍵發佈和取消發佈編輯器中內容片段
* 在編輯內容片段時查看並導覽至語言副本
  ![內容片段編輯器中的語言副本](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* 查看版本有助追蹤內容片段的時間表

  ![內容片段編輯器中的版本](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 查看父參考內容有助作者了解他們編輯內容的影響

  ![內容片段編輯器中的父參考內容](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **大量匯入資料來源的資料**：管理員現在具備[能力可將大量資產](/help/assets/bulk-import-assets-view.md) 從資料來源匯入 AEM Assets。管理員不再需要將個別資產或資料夾上傳到 AEM Assets。支援大量匯入的資料來源包括 Azure、AWS、Google 雲端和 Dropbox。

  ![從資料來源大量匯入資產](/help/release-notes/assets/bulk-import.png)

* **由 Adobe Express 提供技術支援的影像編輯工具**：簡單直覺的[影像編輯工具是由 Adobe Express 提供技術支援，](/help/assets/edit-images-assets-view.md)可直接在 AEM Assets 中使用，以增加內容重複使用性並加快內容流通速度。

  ![使用 Adobe Express 進行影像編輯](/help/release-notes/assets/edit-adobe-express.png)

* **為「我的工作區」的「快速存取」釘選項目時的靈活性**：能夠為您和您的組織或群組清單選擇和釘選項目，讓這些項目能夠根據您的選擇顯示在[「我的工作區」的「快速存取」區段](/help/assets/my-workspace-assets-view.md)中。

  ![為群組釘選項目](/help/release-notes/assets/pin-items-for-groups.png)

### 管理員檢視中的新功能 {#admin-view-features}

**搜尋加強功能**

* 管理員現在可在您執行搜尋時[設定顯示資產的批次大小](/help/assets/search-assets.md#configure-asset-batch-size)。當您進一步向下捲動以載入結果時，資產搜尋結果將以設定的批次大小數字的倍數顯示。您可以從 200、500 和 1000 個資產的可用批次大小中進行選擇。將批次大小設定為較低數字時，會使搜尋回應時間更快。

  ![資產批次大小的設定](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets 現在包含全新第 9 版本 `damAssetLucene` 指數。`damAssetLucene-9` 將 Oak Query 面向計數的行為變更為[不再評估對基本搜尋指數傳回的面向計數存取控制](/help/assets/search-assets.md)，這會使搜尋回應時間更快。

### [!DNL Experience Manager Assets] 中可用的搶鮮版功能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media 中的影片現有多語言字幕和多語言音訊支援](/help/assets/dynamic-media/video.md#about-msma) - 您現在可以輕鬆地將多語字幕和多語言音訊新增至主要影片中。此功能表示全球觀眾都可以存取您的影片。您可以著手自訂一部已發佈的主要影片，以多種語言提供給全球觀眾，並遵守不同地理區域的無障礙指南。此外，作者還可以在使用者介面的單一標籤管理字幕和音軌。

  ![所選影片資產「屬性」頁面上的「字幕和音訊」標籤。](/help/release-notes/assets/msma-aem-cs.png)*所選影片資產「屬性」頁面上的「字幕和音訊」標籤。*

* **資產**：能夠選取在 Experience Manager 中管理的 ZIP 存檔，並可[將檔案直接擷取至 Experience Manager 中的檔案](/help/assets/manage-digital-assets.md#extract-zip-archives)無需下載。

  ![為群組釘選項目](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-forms-channel}

* [**Google reCAPTCHA 企業支援**](/help/forms/captcha-adaptive-forms.md)：以最適化表單使用 Google reCAPTCHA 企業版，以針對詐欺活動和垃圾郵件提供增強的保護，進而提供更安全的使用者體驗。透過進階的風險分析和緊密整合，真實的使用者可輕鬆地提交表單，同時有效地封鎖機器人。


### [!DNL Forms] 中可用的搶鮮版功能 {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics 與表單的 Experience Cloud Setup Automation**：您現在只需輕按幾個按鈕，即可啟用 Adobe Analytics 和 Experience Cloud Setup Automation。這能讓您將 AEM Forms as a Cloud Service 與 Experience Platform 標籤和 Adobe Analytics 連接，以擷取和追蹤已發佈表單的效能指標。

* **適用於最適化表單的 Adobe Analytics 報告範本**：Forms as a Cloud Service 現在提供 Adobe Analytics 報告 OOTB。這可幫助您輕鬆了解表單的效能。表單層級的量度可讓您深入了解表單在多個關鍵績效指標 (KPI) 上的表現，例如呈現、訪客、提交、平均填寫時間。透過追蹤使用者行為和意見回饋，您可以識別表單中造成混亂的部份，並指引表單設計和功能的改善。

  ![最適化表單使用者參與 Adobe Analytics 報告](/help/forms/assets/forms-analytics-report.png)

* **[以核心元件為主的最適化表單中的表單片段](/help/forms/adaptive-form-fragments-core-components.md)**：告別重複的資料、最佳化您的數位庫存，並可改善協作，同時還可使用表單片段提升表單建構體驗。這些可重複使用的元件無縫整合至到多種表單中，簡化了一致且具有專業外觀的表單建立。表單片段透過「一次變更，處處反映」功能確保可重複性、標準化和品牌一致性。由於在一處進行的更新會自動傳播到使用這些片段的所有表單，因此可體驗更高的可維護性和效率。

* **[更佳的 Adobe Sign 工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign 工作流程步驟經過改善，其中包括：
   * **Adobe Sign 以政府核發 ID 為主的驗證**：Adobe Acrobat Sign 以政府核發 ID 為主的驗證允許使用者使用政府核發的 ID (駕駛執照、國民身份證、護照) 驗證其身份，進而提供更多的驗證防護層。此增強功能利用受信任的身分識別文件為簽名過程額外增加一層可信度，使其成為需要增強安全性、合規性和使用者驗證等情境的理想選擇。

   * **Adobe Sign 文件的稽核軌跡**：使用稽核軌跡功能詳細了解 Adobe Sign 文件的生命週期。透過稽核軌跡，您現在可以保留與文件相關的所有動作和互動的全面記錄。其中包括查看、編輯或簽署文件等人員的詳細資訊，以及每個事件的時間戳記。此加強功能對於維持合規性、解決爭議和確保數位協議的完整性至關重要。

   * **協議收件者的新角色不僅僅是簽署人**：Adobe Acrobat Sign 可以選擇將協議收件人的角色擴展到簽署人之外，這樣更可符合其工作流程要求。啟用後，每位協議收件人有其可設定的個別角色，且以簽署人為預設。

* **[使用文件保證 API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：文件保證 API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

* **通訊 API 中的頁數支援**：現在，除了透過通訊 API 擷取文件之外，您還可以接收有關文件內所含頁數的重要資訊。

* **[使用規則編輯器中的自訂錯誤處理常式發生錯誤處理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：您現在可以呼叫自訂函數來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。


### Headless 最適化表單早期採用者方案 {#forms-early-adopter}

使用 [Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=zh-Hant)讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者方案。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### CDN 記錄 {#cdn-logs}

從 Cloud Manager 下載 CDN 記錄，這對於快取命中率最佳化和提高內容傳遞流程的可見性非常有用。[了解關於](/help/implementing/developing/introduction/logging.md#cdn-log) CDN 記錄格式。此功能將於 9 月初逐步向客戶推出。

### CDN 和 WAF 規則早期採用者方案 {#waf-early-adopter}

在 CDN 篩選流量的根據：

* 要求的標頭和屬性 (例如 IP 位址)
* 已知和惡意流量相關的流量模式

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 **aemcs-waf-adopter@adobe.com**，深入了解有關早期採用者方案的資訊。名額有限。

若要深入了解該功能，請點選[這裡](/help/security/traffic-filter-rules-including-waf.md)參閱文章。


## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
