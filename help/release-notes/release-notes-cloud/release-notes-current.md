---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 555873b15e3a748c95893a371925d3ab6e87ae67
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 25%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

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

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2023.8.0)為2023年8月31日。 下一個功能版本(2023.9.0)計畫於2023年9月28日發行。

## 發行影片 {#release-video}

請觀看2023年8月版本概觀影片，瞭解2023.8.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

* [內容片段主控台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hant)現在可讓使用者檢視標記，並依據作為中繼資料套用於內容片段的標記進行搜尋。使用者即不必再為了此功能而切換到資產 UI，減少了內容切換並提高了效率。

  ![在內容片段主控台中進行標記](/help/assets/content-fragments-console-tags.png)
* 新的內容片段編輯器現在可在AEMas a Cloud Service上使用。 透過簡化其撰寫工作，並減少在編輯內容時在不同應用程式之間切換的需求，讓內容作者提高生產力。
  ![新的內容片段編輯器](/help/release-notes/assets/newCFEditor.png)

新的內容片段編輯器提供原始編輯器中未提供的下列優點：
* 自動儲存可提升撰寫效率，並防止意外遺失編輯內容。
* 使用結構樹在深度結構化片段中快速導覽內容片段及其參考的階層式檢視。
  ![內容片段編輯器中的結構樹](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 無需先將資產上傳至資產DAM，即可將資產內傳作為內容參考
* 內容片段所傳送呈現體驗的臨時預覽，協助作者將前端應用程式上內容的外觀與感覺視覺化
* 按一下「 」即可從編輯器發佈和取消發佈內容片段
* 在編輯內容片段時檢視和導覽至語言副本
  ![內容片段編輯器中的語言副本](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* 檢視版本以協助追蹤內容片段的時間軸

  ![內容片段編輯器中的版本](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 檢視上層參考資料以協助作者瞭解編輯的影響

  ![內容片段編輯器中的父參照](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **從資料來源大量匯入資產**：管理員現在擁有 [匯入大量資產的能力](/help/assets/bulk-import-assets-view.md) 從資料來源移至AEM Assets。 管理員不再需要將個別資產或資料夾上傳到 AEM Assets。 支援大量匯入的資料來源包括 Azure、AWS、Google 雲端和 Dropbox。

  ![從資料來源大量匯入資產](/help/release-notes/assets/bulk-import.png)

* **由 Adobe Express 提供支援的影像編輯工具**：簡單又直觀 [Adobe Express支援的影像編輯工具](/help/assets/edit-images-assets-view.md) 可直接在AEM Assets中使用，以提高內容重複使用率並加快內容速度。

  ![使用 Adobe Express 進行影像編輯](/help/release-notes/assets/edit-adobe-express.png)

* **為「我的工作區快速存取」釘選項目時具備靈活性**：可選取並釘選您、整個組織或群組清單的專案，以便這些專案顯示在 [我的工作區的快速存取區段](/help/assets/my-workspace-assets-view.md) 根據您的選取。

  ![為群組釘選項目](/help/release-notes/assets/pin-items-for-groups.png)

### Admin檢視中的新功能 {#admin-view-features}

**搜尋增強功能**

* 管理員現在可以 [設定資產的批次大小](/help/assets/search-assets.md#configure-asset-batch-size) 執行搜尋時顯示的專案。 當您進一步向下捲動以載入結果時，資產搜尋結果會以設定批次大小數字的倍數顯示。 您可以從可用的批次大小中選取200、500和1000個資產。 設定較小的批次大小數字會加快搜尋回應時間。

  ![資產批次大小設定](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets現在包含新版本9 `damAssetLucene` 索引。 `damAssetLucene-9` 將Oak查詢Facet計數行為變更為 [不再評估Facet計數的存取控制](/help/assets/search-assets.md) 由基礎搜尋索引傳回，這會加快搜尋回應時間。

### [!DNL Experience Manager Assets] 中可用的搶鮮版功能 {#prerelease-features-assets}

* **Dynamic Media**： [Dynamic Media中的影片支援多字幕與多音訊曲目](/help/assets/dynamic-media/video.md#about-msma) — 您現在可以輕鬆地將多個字幕和多個音軌新增到主要視訊中。 此功能表示您的視訊可在全球對象中存取。 您可以透過多種語言，為全球觀眾自訂單一已發佈的主要影片，並遵守不同地理區域的協助工具准則。 作者也可以從使用者介面的單一標籤管理字幕和音軌。

  ![所選視訊資產屬性頁面上的字幕和音訊曲目索引標籤。](/help/release-notes/assets/msma-aem-cs.png)*所選視訊資產屬性頁面上的字幕和音訊曲目索引標籤。*

* **資產**：可選取在Experience Manager中管理的ZIP封存，並 [將檔案直接解壓縮到Experience Manager中](/help/assets/manage-digital-assets.md#extract-zip-archives) 而不下載。

  ![為群組釘選項目](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的搶鮮版功能 {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA 企業支援**](/help/forms/captcha-adaptive-forms-core-components.md)：以最適化表單使用 Google reCAPTCHA 企業版，以針對詐欺活動和垃圾郵件提供增強的保護，進而提供更安全的使用者體驗。透過進階的風險分析和緊密整合，真實的使用者可輕鬆地提交表單，同時有效地封鎖機器人。

* **Adobe Analytics與Forms的Experience Cloud設定自動化**：您現在可以啟用具有Experience Cloud設定自動化的Adobe Analytics ，只需扳動幾個按鈕。 它可讓您連結AEM Formsas a Cloud Service與Experience Platform標籤和Adobe Analytics，以擷取及追蹤您已發佈表單的效能度量。

* **最適化Forms的Adobe Analytics報表範本**：Formsas a Cloud Service現在提供Adobe Analytics報表OOTB。 它可協助您輕鬆瞭解表單的效能。 表單層級量度可讓您深入瞭解表單在多重關鍵績效指標(KPI) （例如，轉譯、訪客、提交、平均填滿時間）上的執行情形。 透過追蹤使用者行為和意見回饋，您可以識別表單中造成混淆的區域，並指引表單的設計和功能改善。

  ![最適化表單使用者參與adobe analytics報告](/help/forms/assets/forms-analytics-report.png)

* **[根據核心元件的最適化Forms中的表單片段](/help/forms/adaptive-form-fragments-core-components.md)**：與複製再見、最佳化您的數位庫存，並在您使用表單片段提升您的表單建立體驗時改善共同作業。 這些可重複使用的元件可順暢地整合為多種表單，簡化建立一致且具備專業外觀的表單。 表單片段透過「一次變更並隨處反映」功能，確保可重複使用、標準化和品牌一致性。 由於在一個位置進行的更新會自動傳播到使用這些片段的所有表單，因此體驗更好的可維護性和效率。

* **[增強的Adobe Sign工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign工作流程步驟已增強，現在包括下列專案：
   * **Adobe Sign的政府機關身分證件型驗證**：Adobe Acrobat Sign的政府機關身分證件可讓使用者使用政府核發的ID （駕照、國民身分證、護照）驗證身分，進一步提升身分驗證層次。 運用信任的身分識別檔案，這項增強功能為簽署程式增添了額外的信賴度，非常適合需要增強安全性、法規遵循及使用者驗證的案例。

   * **Adobe Sign檔案的稽核軌跡**：使用稽核軌跡功能，取得Adobe Sign檔案生命週期的詳細深入分析。 使用「稽核軌跡」，您現在可以維護與檔案相關的所有動作與互動的完整記錄。 其中包括檢視、編輯或簽署檔案者的詳細資訊，以及每個事件的時間戳記。 此增強功能對於維護合規性、解決爭議及確保數位合約的完整性至關重要。

   * **除了簽署者之外，協定收件者的新角色**：Adobe Acrobat Sign可選擇擴充協定收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 啟用後，協定中的每個收件者皆可個別設定其角色，預設值為「簽署者」。

* **[使用檔案保證API （通訊API的一部分）Protect您的檔案](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：檔案保證API可讓您透過簽署和加密檔案來保護敏感資訊。 透過加密，檔案的內容會轉換為無法讀取的格式，確保只有授權的使用者才能取得存取權。 這種強化的保護層不僅能夠保護寶貴的資料，避免未經授權的眼睛，而且讓您完全安心。 簽名API可讓您的組織保護其發佈和接收Adobe PDF檔案的安全性和隱私權。 此服務使用數位簽名和憑證，以確保只有預期的收件者才能變更檔案。

* **通訊API中的頁數支援**：現在，透過通訊API擷取您的檔案時，您還可以收到檔案中包含頁數的重要資訊。

* **[在規則編輯器中使用自訂錯誤處理常式來處理錯誤](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：您現在可以叫用自訂函式來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。 例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。

* **[64位元版AEM Forms Designer](/help/forms/installing-configuring-designer.md)**： 64位元版本的AEM Forms Designer提供更優異的效能、擴充能力及記憶體管理，讓您更輕鬆地建立表單。 有了64位元架構，您可以輕鬆處理更大型且更複雜的專案，確保順暢的設計工作流程及最佳化效率。 透過此尖端的發行版本，提升您的外型設計功能，並擁抱AEM Forms Designer的未來。


### 早期採用者計畫 {#forms-early-adopter}

* **[使用DocAssurance API （通訊API的一部分）Protect您的檔案](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API可讓您簽署及加密檔案，以保護敏感資訊。 透過加密，檔案的內容會轉換為無法讀取的格式，確保只有授權的使用者才能取得存取權。 這種強化的保護層不僅能夠保護寶貴的資料，避免未經授權的眼睛，而且讓您完全安心。 簽名API可讓您的組織保護其發佈和接收Adobe PDF檔案的安全性和隱私權。 此服務使用數位簽名和憑證，以確保只有預期的收件者才能變更檔案。

      您可以從官方電子郵件ID寫信到「aem-forms-early-adopter-program@adobe.com」，以加入率先採用者計畫並請求存取功能。
  
* **[Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)**：使用Headless最適化Forms，讓開發人員建立、發佈和管理可透過API （而非透過傳統圖形使用者介面）存取和互動的互動式表單。 Headless 最適化表單可協助您：

   * 使用您選擇的程式語言建置高品質的多管道表單
   * 以原生方式將表單整合到您的桌面和行動應用程式、網站和聊天應用程式
   * 在表單應用程式中重複使用您的專屬 UI 元件
   * 使用 Adobe Experience Manager Forms 的強大功能

  使用您的官方電子郵件 ID 寄送電子郵件至 `aem-forms-headless@adobe.com`，即可加入早期採用者計畫。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### CDN 紀錄 {#cdn-logs}

從Cloud Manager下載CDN記錄，這對於快取命中率最佳化以及內容傳送流程的可見度非常有用。 [瞭解](/help/implementing/developing/introduction/logging.md#cdn-log) CDN記錄格式。 此功能將於9月初逐步向客戶推出。

### CDN 和 WAF 規則早期採用者計劃 {#waf-early-adopter}

在 CDN 篩選流量的根據：
* 要求的標頭和屬性 (例如，IP 位址)
* 已知和惡意流量相關的流量模式

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 **aemcs-waf-adopter@adobe.com**，深入了解有關早期採用者計劃的資訊。名額有限。

若要深入了解該功能，請點選[這裡](/help/security/cdn-and-waf-rules.md)參閱文章。


## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
