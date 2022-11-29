---
title: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 218dd65d1969f92317ae1d9877e2e37bb201ea6a
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---


# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

>[!CAUTION]
>
>**計畫維護排除期**
>
> 下列時間範圍內(從午夜開始到結束，CET為(00:00))不會執行自動AEMaCS維護：
>
>* 11月21日星期一至12月12日星期一
>* 12月19日星期一至1月3日星期二


## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前的每月發行(2022.10.0)為2022年11月10日。 下一個月發行(2023.1.0)預計於2023年1月26日推出。

## 發行影片 {#release-video}

請觀看2022年10月版本概觀影片，以取得2022.10.0版中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### 中的新功能 [!DNL Sites] {#sites-features}

* 此 [體驗片段的個人化標籤](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 可讓體驗片段編輯器取得區段規格功能，並可彈性建立巢狀體驗片段，以便為多個區段建立頁首和頁尾變數。 在啟動此功能之前，AEM提供的個人化僅適用於網站頁面，不適用於體驗片段

* 此 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 現在可讓使用者有效管理翻譯的內容片段。 提供一鍵式存取，也可檢視所有語言副本。 使用者也可以依所感興趣的地區來篩選表格檢視。

![內容片段語言](/help/release-notes/assets/cfconsole-languages.png)

* 透過最佳化範本中的影像大小設定，進一步縮短訪客的頁面載入時間。 如需影像元件的詳細資訊，請前往 [核心WCM元件](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* Experience Manager Assets現在可讓您上傳其他支援格式類型的檔案，以及[ 使用隨附的Document Cloud檢視器預覽](/help/assets/manage-pdf-documents.md). 支援的格式類型包括TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。

   ![其他格式的PDF轉譯](/help/release-notes/assets/multi-page-other-formats.png)


### 中的新功能 [!DNL Assets] 預發行 {#prerelease-features-assets}

* Experience Manager Assets現在對影像智慧標籤使用改良的人工智慧架構。 此內容智慧可讓擷取時所有影像資產都能使用的智慧標籤，具有更佳的關聯性和精確度。 此外，方向資訊會填入 `cq:tags`，可使用方向篩選器來啟用更好的搜尋結果。

   如果您有興趣參與測試版， [填寫表格](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) 到11月14日。

* 現在Experience Manager Assets [支援SAS令牌](/help/assets/add-assets.md#asset-bulk-ingestor) 除了用於驗證的存取金鑰外，還連接到Azure Blob儲存資料來源，以使用大量匯入工具擷取資產。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 中提供的新功能 [!DNL Forms] {#new-features-available-in-channel}


* [適用性Forms精靈](/help/forms/creating-adaptive-form.md):AEM Forms提供商務使用者易記精靈，可快速撰寫最適化Forms。 精靈提供快速的索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。 此版本對精靈進行下列改良：

   * 選擇或取消選擇欄位：精靈可讓您根據JSON和表單資料模型結構建立最適化表單。 您現在可以選取結構內要納入適用性表單的欄位子集。 選取的欄位會轉換為對應的最適化表單資料擷取元件，以快速建立所需的最適化表單。

   * 使用靜態範本：如果客戶現有投資於舊版靜態範本，則可在精靈中使用靜態範本來撰寫最適化表單，以繼續雲端採用歷程。 這可讓客戶將舊靜態範本移轉至現代可編輯的範本，以提供額外的時間。

* [在伺服器端處理時，從記錄檔案(DoR)中移除隱藏欄位](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md):您可以為最終用戶生成記錄PDF文檔，該文檔僅包含在資料捕獲體驗期間對他們可見的欄位。 提交表單時，伺服器會根據提交的資料驗證向最終用戶隱藏的欄位，並從記錄中排除以保持一致。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **適用性Forms範本編輯器**:範本編輯器可讓您預先定義組織的適用性Forms的基本結構和外觀。 此版本對範本編輯器進行下列改良：
   * **[範本編輯器中的表單資料模型](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**:您可以在範本編輯器中將表單資料模型架構與適用性表單範本建立關聯。 有助於縮短建立最適化表單的時間。 此選項也新增至適用性Forms編輯器，讓使用者為現有表單選取或變更表單資料模型。
   * **[模板編輯器中的記錄文檔](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**:您現在可以針對使用範本建立的所有表單，標準化記錄檔的產生。 這有助於增強組織需求的合規性和標準化。

* **[從AEM Sites頁面啟動適用性表單精靈](/help/forms/embed-adaptive-form-aem-sites.md)**:AEM Sites頁面已延伸支援適用性Forms。 您現在可以建立新的適用性表單，或在保留在AEM Sites頁面時內嵌現有的適用性表單。
* **[更改DoR中複選框和單選按鈕的顯示對齊方式](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**:您現在可以為「記錄檔」上的核取方塊和選項按鈕設定所需的對齊方式(水準、垂直、與適用性Forms相同)。 此選項確定記錄文檔中複選框和單選按鈕選項的位置。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用體驗片段來動態豐富產品清單(範例：在產品清單之間放置橫幅)。
* 清單元件現在支援關聯的產品/類別頁面，以動態顯示相關頁面。
* 新增對Peregrine 12.5元件的支援。
* 新增了產品預告和轉盤中用戶端價格載入的支援。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* AEMas a Cloud Service（作者服務）現已與Unified Shell整合，以改善使用者體驗，並與所有其他Experience Cloud應用程式統一。 請參閱AEM as a [Cloud Service統一殼層](/help/overview/aem-cloud-service-on-unified-shell.md) 以取得更多詳細資訊。

* 如發行說明中先前所述，使用復寫代理管理螢幕或復寫API來分送大於10 MB的內容套件（含屬性的節點，不包括二進位檔）已遭取代，並將於未來數天內強制執行。 請參閱 [管理出版物](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) 針對複製這些大型內容套件的建議方法。

* Dispatcher設定現在會參考列出常見行銷活動查詢參數的檔案。 客戶可以選擇取消註解與他們相關的參數，進而改善快取。 請參閱 [行銷活動參數](/help/implementing/dispatcher/caching.md#marketing-parameters) 以取得更多詳細資訊。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
