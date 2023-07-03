---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 目前發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 45004db44af48301f0a9cbd9f574ac34c360275e
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 32%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.6.0) 的發行日期為 2023 年 6 月 29 日。下一個功能版本(2023.7.0)計畫於2023年7月27日發行。

## 發行影片 {#release-video}

請觀看2023年6月版本概觀影片，瞭解2023.6.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 內容片段及其參考資料現在可以發佈到 [AEM 預覽服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hant#access-preview-service) (使用[內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hant))，讓使用者在上線前可在分離的預覽應用程式上先預覽最終體驗。
* 現在可以使用AEM GraphQL在Headless案例中針對Web傳送動態最佳化影像。 [查詢變數](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) 可在GraphQL查詢中定義，以允許分離的使用者端應用程式從AEM請求對應的最佳化影像。
* 上的標籤 [內容片段變數](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) 現在可以使用AEM GraphQL內容傳送API輸出到JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

**新資產檢視的可用性**

此 [新資產檢視](/help/assets/assets-view-introduction.md) 現在可在Experience Manager Assets中使用。 Assets View提供簡化的使用者介面，讓您輕鬆管理、探索和分發數位資產。 體驗的目標是創意人員、唯讀資產消費者和重量較輕的DAM使用者。

![標籤管理](/help/assets/assets/my-workspace.png)

**搜尋體驗增強功能**

Experience Manager Assets現在可讓您從搜尋結果使用者介面執行更多作業：您現在可以：

* [在目前的存放庫位置中執行搜尋](/help/assets/search-assets.md) 依預設，不會在整個存放庫中搜尋關鍵字。

* [導覽至資料夾位置](/help/assets/search-assets.md#aftersearch) 適用於顯示在搜尋結果中的資產。

**3D資產的縮圖預覽**

[!DNL Experience Manager Assets] 現在產生 [常見3D檔案格式的縮圖預覽](/help/assets/file-format-support.md) 包括gLB、USDz、FBX、3DS、OBJ和SBSAR。 上傳這些檔案時，預設會自動產生縮圖。

**連結共用設定**

改善的新使用者體驗 [建立連結共用](/help/assets/share-assets.md) 以及一套全新的設定，讓管理員可以為您的使用者自訂此功能的預設行為。

![標籤管理](/help/assets/assets/config-email-service.png)

**Dynamic Media：更新影像設定檔中與智慧型裁切相關的欄位**

影像設定檔中某些智慧型裁切相關欄位的使用者介面現已更新，以反映定義智慧型裁切的目前准則。 請參閱[裁切選項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=zh-Hant#crop-options)。

### 「資產」檢視中的新功能 {#assets-view-features}

**資產的階層式標籤，提供更快速的搜尋體驗**

控管辭彙的平面清單會隨著時間而變得無法管理。 資產檢視現在支援 [階層式標籤結構](/help/assets/tagging-management-assets-view.md)，可協助套用相關中繼資料、分類資產、支援搜尋、重複使用標籤、改善可發現性等。

![標籤管理](/help/assets/assets/tags-hierarchy.png)

**釘選檔案、資料夾和集合以快速存取**

您現在可以 [釘選檔案、資料夾和集合，以加快存取速度](/help/assets/my-workspace-assets-view.md) 之後需要這些專案時使用這些專案。 釘選專案會顯示在 **快速存取** 區段。 您可以使用「我的工作區」來存取這些物件，而不必導覽至儲存於存放庫中的儲存位置。

![Workspace 中的任務](/help/assets/assets/quick-access.png)

**篩選垃圾桶資料夾中的資產**

資產檢視現在可讓您 [篩選垃圾桶資料夾中可用的資產](/help/assets/navigate-assets-view.md). 您可以套用標準或自訂篩選器，在垃圾桶資料夾中搜尋適當的資產，以還原或永久刪除它們。

**3D資產的縮圖預覽**

Assets檢視現在會產生常見3D檔案格式的縮圖預覽，包括gLB、USDz、FBX、3DS、OBJ和SBSAR。 將這些檔案上傳至「資產」檢視時，系統會依預設自動產生縮圖。

![Workspace 中的任務](/help/assets/assets/3d-preview.png)

**檢視熱門搜尋字詞**

資產檢視現在支援 [檢視部署中搜尋最多的辭彙](/help/assets/my-workspace-assets-view.md) 使用 **深入分析** 區段。 您也可以導覽至詳細分析，檢視過去30天或12個月的熱門搜尋。

![Workspace 中的任務](/help/assets/assets/insights-top-searches.png)

**中繼資料表單增強功能**

資產檢視現在可讓您 [新增多值文字和下拉式清單屬性元件](/help/assets/metadata-assets-view.md#property-components) 至中繼資料表單。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* [AEM頁面編輯器和體驗片段中的最適化Forms](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您現在可以使用AEM頁面編輯器和體驗片段來快速建立多個表單並新增到您的AEM Sites頁面。 此功能可讓內容作者運用Adaptive Forms元件的強大功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面中建立順暢的資料擷取體驗。

  >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [透過AEM Forms使用政府用Adobe Acrobat Sign Solutions （HIPPA投訴）](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms現在與適用於政府的Adobe Acrobat Sign Solutions整合。 這種整合能夠讓政府相關帳戶 (政府部門和機構) 在提交最適化表單時，享有等級更高的電子簽名合規性和安全性。

  與適用於政府的Adobe Acrobat Sign Solutions整合可讓Adobe的合作夥伴和政府客戶在Adaptive Forms中使用電子簽章，處理某些最關鍵和敏感的業務線。 這額外一層的安全性可確保所有電子簽名完全符合 FedRAMP 中等合規性，讓 Adobe 的政府客戶安心使用。

* [增強規則編輯器中自訂錯誤處理常式的錯誤處理功能](/help/forms/add-custom-error-handler-adaptive-forms.md)：您現在可以叫用自訂函式（使用使用者端資料庫）來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。 或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。

  此功能有助於引進標準型錯誤回應來提高整體的錯誤處理能力；這些回應向後相容於 OOTB 錯誤處理常式，且具有更大的彈性和控制性。

* [表單資料模型的增強驗證方法](/help/forms/configure-data-sources.md)：使用者端憑證式驗證能將AEM Forms （表單資料模型）與相容的資料來源連線，讓您體驗更強的安全性。 此增強功能免除模擬或使用者登入的需要，進而加強資料的保護。

* [使用可重複區段建立最適化Forms](/help/forms/create-forms-repeatable-sections.md)：您現在可以製作 [收合式選單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)， [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、和 [水準標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) 元件在核心元件型最適化表單中建立可重複區段。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  這些可重複區段可讓您提供不限數量的專案，而不含固定欄位計數。 當所需的資料例項事先未知時，這個變數很有用。 Forms使用者可輕鬆新增或移除區段，讓表單能適應不同的資料輸入情境，並簡化相同資料多次出現次數的收集工作。

* **[將最適化Forms提交至Microsoft®SharePoint和Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：您現在可以將最適化Forms資料提交至Microsoft®SharePoint Site或Microsoft® OneDrive等日常工具。

### Headless 最適化表單早期採用者計劃 {#forms-early-adopter}

使用 [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 可讓您的開發人員建立、發佈和管理互動式表單，這些表單可透過API （而非透過傳統的圖形使用者介面）存取及互動。 Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者計劃。


## 維護版本發行說明 {#maintenance}

您可以在[此處](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
