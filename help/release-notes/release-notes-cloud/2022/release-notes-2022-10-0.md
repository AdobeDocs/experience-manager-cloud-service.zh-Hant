---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0 版發行說明。'
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 80%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.10.0 版發行說明 {#release-notes}

以下區段會概述2022.10.0版的 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前每月發行 (2022.10.0) 的發行日期是 2022 年 11 月 10 日。 下一個每月發行 (2023.1.0) 計畫於 2023 年 9 月 2 日推出。

## 發行影片 {#release-video}

請觀看 2022 年 10 月發行概觀影片，了解 2022.10.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### [!DNL Sites] 中的新功能 {#sites-features}

* 此 [體驗片段的個人化標籤](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 允許體驗片段編輯器的分段規格功能和建立巢狀體驗片段的靈活性，從而可以為多個片段建立各種不同的頁首和頁尾。 在此功能推出之前，AEM 提供的個人化僅適用於網站頁面，不適用於體驗片段

* [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)現在可讓使用者有效地管理翻譯的內容片段。另外提供一鍵式存取，以便檢視所有語言版本。 使用者也可以依照他們感興趣的地區設定來篩選表格檢視。

![內容片段語言](/help/release-notes/assets/cfconsole-languages.png)

* 透過最佳化範本中的影像大小設訂，進一步縮短訪客的頁面載入時間。在[核心 WCM 元件](https://github.com/adobe/aem-core-wcm-components)尋找影像元件的詳細資訊

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* Experience Manager Assets現在可讓您上傳其他受支援格式型別和[使用隨附的Document Cloud檢視器預覽](/help/assets/manage-pdf-documents.md). 支援的格式類型包括 TXT、RTF、DOC、DOCX、PPT、PPTX、XLS 和 XLSX。

  ![其他格式的 PDF 轉譯](/help/release-notes/assets/multi-page-other-formats.png)


### [!DNL Assets] 發行前版本的新功能 {#prerelease-features-assets}

* Experience Manager Assets 現在為影像智慧標記使用改良的人工智慧框架。 此內容智慧可提高智慧標記的相關性和準確性，在擷取時可用於所有影像資產。此外，`cq:tags` 中會填入方向資訊，而能夠使用方向篩選器獲得更好的搜尋結果。

  如果您有興趣參與 Beta 版測試，請在 11 月 14 日前[填寫本表單](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u)。

* 除了在連接到 Azure Blob 儲存體資料來源以使用大量匯入工具擷取資產時支援用於驗證的存取金鑰之外，Experience Manager Assets 現在還[支援 SAS 權杖](/help/assets/add-assets.md#asset-bulk-ingestor)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中可用的新功能 發行前通道 {#prerelease-features-forms}

* **最適化Forms範本編輯器**：範本編輯器讓您為組織預先定義最適化Forms的基本結構和外觀。 此版本引進了下列對範本編輯器的改良：
   * **[範本編輯器中的表單資料模型](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**：您可以在範本編輯器中將表單資料模型結構描述關聯到調適型表單範本。它有助於縮短建立調適型表單所需的時間。該選項也以新增至調適型表單編輯器中，讓使用者能夠選取或變更現有表單的表單資料模型。
   * **[範本編輯器中的文件記錄](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**：您現在可以將為使用範本建立的所有表單產生文件記錄的過程標準化。這有助於提高組織要求的合規性和標準化。

* **[從 AEM Sites 頁面啟動調適型表單精靈](/help/forms/embed-adaptive-form-aem-sites.md)**：AEM Sites 頁面已延伸對調適型表單的支援。您現在可以建立新的調適型表單或內嵌現有的調適型表單，同時保留在 AEM Sites 頁面上。
* **[變更 DoR 中核取方塊和選項按鈕的顯示對齊方式](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**：您現在可以為文件記錄上的核取方塊和選項按鈕設定所要的對齊方式 (水平、垂直、與調適型表單相同)。此選項決定了文件記錄中核取方塊和選項按鈕選項的位置。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用體驗片段以動態的方式豐富產品清單 (例如：在產品列表之間放置橫幅)。
* 清單元件現在支援相關聯產品/類別頁面以動態顯示相關頁面。
* 已新增 Peregrine 12.5 元件的支援。
* 已新增對產品預告和輪播中用戶端價格載入的支援。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* AEM as a Cloud Service (作者服務) 現在與 Unified Shell 整合，以改進使用者體驗，並將其與所有其他 Experience Cloud 應用程式統一。 請參閱AEM as a [在Unified Shell上Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以取得更多詳細資料。

* 如先前在發行說明中所述，使用復寫代理程式管理畫面或復寫API來分發大於10 MB的內容套件（具有屬性的節點，不包括二進位檔案）現在已棄用和強制執行。 另請參閱 [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow) 瞭解復寫這些大型內容套件的建議方法。

* Dispatcher 設定現在會參照一個列出常見行銷活動查詢參數的檔案。客戶可以選擇取消註釋與其相關的參數，從而促進快取。另請參閱 [行銷活動引數](/help/implementing/dispatcher/caching.md#marketing-parameters) 以取得更多詳細資料。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
