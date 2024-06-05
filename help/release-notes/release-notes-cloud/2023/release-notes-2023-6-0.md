---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 版發行說明。'
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.6.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.6.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.6.0) 的發行日期為 2023 年 6 月 29 日。下一個功能版本 (2023.7.0) 預計於 2023 年 7 月 27 日發行。

## 發行影片 {#release-video}

請觀看 2023 年 6 月發行概觀影片，了解 2023.6.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* 內容片段及其參考資料現在可以發佈到 [AEM 預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) (使用[內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console))，讓使用者在上線前可在分離的預覽應用程式上先預覽最終體驗。

![在內容片段主控台中的預覽](/help/assets/content-fragments-console-preview.png)

* 現在可以使用 AEM GraphQL 在 Headless 情境下，動態最佳化影像以進行 Web 傳遞。[查詢變數](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html#query-variables)可以在 GraphQL 查詢中定義，以允許分離的用戶端應用程式相應地要求 AEM 中的最佳化影像。
* 現在可以使用 AEM GraphQL 內容傳遞 API 將[內容片段變化](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html)上的標記輸出至 JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

**新資產檢視的可用性**

Experience Manager Assets 現在提供[新的資產檢視](/help/assets/assets-view-introduction.md)。資產檢視提供簡化的使用者介面，使您可輕鬆管理、探索和分發數位資產。該體驗的目標對象是唯讀創意資產的取用者以及輕量型 DAM 使用者。

![標記管理](/help/assets/assets/my-workspace.png)

**搜尋體驗增強功能**

Experience Manager Assets 現在使您能夠透過搜尋結果使用者介面執行更多操作：您現在可以：

* 預設會[在目前存放庫位置執行搜尋](/help/assets/search-assets.md)，而不是在整個存放庫中搜尋關鍵字。

* [瀏覽到搜尋結果中顯示之資產所在的資料夾。](/help/assets/search-assets.md#aftersearch)

**3D 資產的縮圖預覽**

[!DNL Experience Manager Assets] 現在可以產生[常見 3D 檔案格式的縮圖預覽](/help/assets/file-format-support.md)，包括 gLB、USDz、FBX、3DS、OBJ 和 SBSAR。當這些檔案上傳時，縮圖會依預設自動產生。

**Dynamic Media：更新了影像設定檔中與智慧型裁切相關欄位**

影像設定檔中一些與智慧型裁切相關之欄位的使用者介面現已更新，以反映定義智慧型裁切的最新指引。請參閱[裁切選項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html#crop-options)。

### 資產檢視中的新功能 {#assets-view-features}

**資產的階層式標記可提供更快速的搜尋體驗**

受控詞彙的平面清單會隨著時間推移而變得難以管理。資產檢視現在支援[標記階層結構](/help/assets/tagging-management-assets-view.md)，這有助於套用相關的中繼資料、將資產分類、支援搜尋、重複使用標記、提高易尋性等。

![標記管理](/help/assets/assets/tags-hierarchy.png)

**釘選檔案、資料夾和集合以便快速存取**

現在可以[釘選檔案、資料夾和集合以便快速存取](/help/assets/my-workspace-assets-view.md) (之後需要時)。釘選的項目都顯示在「我的工作區」的&#x200B;**快速存取**&#x200B;部分。您可以使用「我的工作區」進行存取，而不是瀏覽到存放庫中儲存的位置。

![Workspace 中的任務](/help/assets/assets/quick-access.png)

**篩選「垃圾桶」資料夾的資產**

資產檢視現在可讓您[篩選「垃圾桶」資料夾中的資產](/help/assets/navigate-assets-view.md)。您也可以套用標準或自訂篩選條件搜尋「垃圾桶」資料夾中的適當資產，以恢復或永久刪除。

**3D 資產的縮圖預覽**

資產檢視現在可以產生常見 3D 檔案格式的縮圖預覽，包括 gLB、USDz、FBX、3DS、OBJ 和 SBSAR。當這些檔案上傳到資產檢視時，系統會依預設情況自動生成縮圖。

![Workspace 中的任務](/help/assets/assets/3d-preview.png)

**檢視熱門搜尋詞彙**

資產檢視現在支援使用「我的工作區」的 **Insights** 部分，[檢視在部署中的熱門搜尋詞彙](/help/assets/my-workspace-assets-view.md)。您也可以瀏覽到詳細的 Insights 以檢視過去 30 天或 12 個月內的熱門搜尋。

![Workspace 中的任務](/help/assets/assets/insights-top-searches.png)

**中繼資料表單增強功能**

資產檢視現在可讓您在中繼資料表單中[新增多值文字和下拉式清單屬性元件](/help/assets/metadata-assets-view.md#property-components)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 {#new-features-available-in-channel}

* [AEM 頁面編輯器中的最適化表單](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您現在可以使用 AEM 頁面編輯器快速建立多個表單，並將這些表單新增至您的 Sites 頁面。此功能讓內容作者可使用最適化表單元件 (包括動態行為、驗證、資料整合、產生記錄文件和業務流程自動化) 的強大功能，在 Sites 頁面內建立順暢的資料擷取體驗。您可以：

   * 將表單元件拖放到 AEM Sites 編輯器或體驗片段中的最適化表單容器元件，即可建立最適化表單。
   * 使用 AEM Sites 編輯器中的最適化表單精靈，以便建立不屬於任何 Sites 頁面的表單，讓您能夠在多個頁面之間自由地重複使用這些表單。
   * 將多個表單新增到 Sites 頁面，簡化使用者體驗並提供更大的彈性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [適用於政府機關的 Adobe Acrobat Sign Solutions](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms 現在與適用於政府機關的 Adobe Acrobat Sign Solutions 整合。這種整合能夠讓政府相關帳戶 (政府部門和機構) 在提交最適化表單時，享有等級更高的電子簽名合規性和安全性。

  藉由與適用於政府機關的 Adobe Acrobat Sign Solutions 整合，在一些最重要的關鍵任務和敏感業務線，Adobe 的合作夥伴和政府客戶便可以在最適化表單使用電子簽名。這額外一層的安全性可確保所有電子簽名完全符合 FedRAMP 中等合規性，讓 Adobe 的政府客戶安心使用。

* [使用規則編輯器中的自訂錯誤處理常式增強錯誤處理](/help/forms/add-custom-error-handler-adaptive-forms.md)：您現在可以呼叫自訂函數 (使用用戶端資料庫) 來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。

  此功能有助於引進標準型錯誤回應來提高整體的錯誤處理能力；這些回應向後相容於 OOTB 錯誤處理常式，且具有更大的彈性和控制性。

* [表單資料模型的增強型驗證方法](/help/forms/configure-data-sources.md)：導入以用戶端憑證為基礎的驗證機制將 AEM Forms 與相容的資料來源相連接，體驗更高的安全性。使用此增強功能就不需要模擬或使用者登入，從而強化對資料的保護。

* [具有可重複區段的最適化表單](/help/forms/create-forms-repeatable-sections.md)：您現在可在以核心元件為主的最適化表單中製作[折疊式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)、[面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)和[水平索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)，藉此建立可重複區段。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  這些可重複的區段可讓您提供無限數量的項目，欄位數不用固定。當無法事先知道需要多少份的資料時，這就非常有用。Forms 使用者可以輕鬆新增或移除區段，使表單可依不同資料輸入情境進行調整，並簡化同一資料多次出現的收集作業。

* **[將最適化表單提交至 Microsoft® SharePoint 和 Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：改善商業使用者的敏捷性，以便快速啟動新表單並將提交的資料儲存在日常使用的工具中，例如 Microsoft® SharePoint 網站或 OneDrive 資料夾。

### Headless 最適化表單早期採用者方案 {#forms-early-adopter}

使用 [Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)讓您的開發人員能夠建立、發佈和管理可透過 API 存取和互動的互動式表單，而不是透過傳統的圖形使用者介面。Headless 最適化表單可協助您：

* 使用您選擇的程式語言建置高品質的多管道表單
* 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
* 在表單應用程式中重複使用您的專屬 UI 元件
* 使用 Adobe Experience Manager Forms 的強大功能

使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者計畫。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
