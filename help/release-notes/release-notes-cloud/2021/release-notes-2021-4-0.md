---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: a2c844d6f72c22ed085690ff98572a52e97de40d
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 46%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Adobe Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>您可以在此處瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.4.0是2021年5月6日。
下列版本(2021.5.0)將於2021年5月27日發行。

## AEMas a Cloud Service基礎{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流程模型和步驟可在發佈深層內容時提高效能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* GraphQL端點 — 現在可以為個別AEM Sites設定啟用AEM GraphQL API，並使用新的GraphQL Console UI為這些設定建立自訂GraphQL端點。 UI也可讓您管理GraphQL端點。

* 內容模型、增強型日期和時間資料型別 — 現在可以設定日期和時間資料型別，以允許撰寫僅限日期、僅限時間或是日期和時間的資訊。

* 內容模型、增強型標籤資料型別 — 現在可以設定標籤資料型別，以允許撰寫單一或多個標籤。

* 內容模型、新索引標籤預留位置資料型別 — 新索引標籤預留位置資料型別允許將資料型別分組到多個區段中，這些區段將會在內容片段編輯器中的索引標籤底下呈現。

### [!DNL Sites]中的錯誤修正 {#bug-fixes-sites}

* 內容片段 — 移動內容片段或資料夾現在會更新片段內的巢狀參考(CQ-4320815)

* GraphQL — 持續查詢現在支援特定於AEM Sites設定的使用者定義端點(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* [!DNL Experience Manager] 不會封存下載原始檔案的單一資產下載。 此增強功能可加快下載速度。

* 透過linkshare選項下載資產時，您現在可以選擇下載或不下載轉譯。 之前則會下載所有資產轉譯。

* 管理員可以設定 [!DNL Experience Manager] 若要在執行大量資產擷取後刪除資產來源，請執行下列動作。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 在執行狀況檢查以大量匯入資產時，Experience Manager現在會提供失敗原因的更多資訊。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 使用大量匯入工具匯入資產時，管理員現在可以選擇在匯入成功後刪除來源檔案。 另請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 編輯中繼資料結構描述時，新的根路徑選擇器欄位可讓管理員快速輕鬆地做出選擇，進而縮短設定時間。

* 編輯中繼資料結構描述時，會新增一個資料型別，在中繼資料編輯器中提供自由格式的文字區域。 使用者可以使用此文字區域輸入自由格式文字作為資產的中繼資料。 另請參閱 [中繼資料結構編輯器](/help/assets/metadata-schemas.md).

* 許多資產的中繼資料可以使用CSV檔案大量匯入，也可以匯出到CSV檔案。 預設日期格式現在為 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. 使用者可以更新欄標題來運用不同的格式。 例如，新增 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` 做為CSV檔案中的欄標題，而不是單字 `Date`.

* 在「欄」檢視中瀏覽資產時，視覺指示器會顯示每個資產的已核准或已拒絕狀態。

* 在「欄」檢視中瀏覽資產時，視覺指示器會顯示已到期的資產。

### [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 嘗試移動多個資產或資料夾時，控制檯中會記錄錯誤，且移動作業未完成。 如果無法更新標題，移動作業會失敗。 (CQ-4322080)

* 中繼資料欄位可以根據規則隱藏，以便在滿足預先定義的條件時，中繼資料不是強制性的。 不過，此類隱藏的中繼資料欄位會顯示為必填欄位。 (CQ-4321285)

* 大量中繼資料匯入失敗，因為日期格式不正確。 (CQ-4319014)

* 在「屬性」頁面中選取要更新中繼資料時，如果結構描述提供了許多選項，介面的回應會很緩慢。 (CQ-4318538)

* 在單行文字欄位中更新和儲存中繼資料值時，即使下拉式選單上的編輯功能已停用，下拉式選單中的值也會被刪除。 (CQ-4317077)

* 您可以使用省略符號作為註解來檢閱資產。 使用小橢圓時，橢圓與列印版本中的註釋編號重疊。 (CQ-4316792)

* 在搜尋資產後，若從搜尋結果中選取資產，快速發佈選項不會顯示。 (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **在啟用 Adobe Sign 的最適化表格中使用政府機關身分證件驗證方法**

   在先進的機器學習演算法的支援下，Adobe Sign 的政府機關身分證件流程讓全球的公司能夠確保對其接收者身分進行高品質的驗證。 現在，您可以在啟用 Adobe Sign 的最適化表格中使用政府機關身分證件驗證方法。

   政府機關身分證件是優質的身分驗證方法，會指示接收者[上傳政府機構簽發的身分證件 (駕照、國民身分證、護照) 的影像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然後評估該證件以確保其真實性。

* **支援使用表格中的簽名體驗來提交非同步的最適化表格**

   您現在可以使用表格中的簽名體驗來提交非同步的最適化表格。 您也可以將最適化表格內嵌到 [!DNL Experience Manager Sites] 頁面上，並使用表格中的簽名體驗來提交最適化表格。

* **為指派工作步驟預先填寫最適化表格時，支援使用變數來指定附件**

   為指派工作步驟預先填寫最適化表格時，您現在可以使用文件類型變數為最適化表格選取輸入附件。

* **支援使用常值選項來設定 JSON 類型變數的值**

   您可以在 AEM 工作流程的設定變數步驟中，使用常值選項來設定 JSON 類型變數的值。 此常值選項可讓您使用字串形式來指定 JSON。

* **使用本機開發環境來建立記錄文件 (DoR)**

   您可以在雲端服務實例及 AEM Forms as a Cloud Service SDK (本機開發環境) 中使用 XDP 當做記錄文件範本。 在過去，支援僅限於雲端服務實例。

### [!DNL Forms]中的錯誤修正 {#bug-fixes-forms}

* 當將設為不產生記錄文件的最適化表單提交給設為產生記錄文件的 AEM 工作流程，則會顯示無錯誤訊息，且任務無法提交。

### 其他更新 {#misc-2021-04-0-forms}

* 為了更方便識別內容，該服務現在會為XDP、動態PDF和結構描述檔案產生即時縮圖。
* 新增將PDF檔案移動到放置在AEM Forms UI上的資料夾的功能。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 類別UID的支援 — 針對使用字串作為類別ID的系統，這可解除鎖定第三方商業整合

* PWA Studio的AEM擴充功能，包括 整合範例

* 可擴充WCM導覽核心元件的新CIF導覽核心元件

* AEM店面中暫存目錄資料的視覺指示器

* 現在可透過Cloud Manager UI設定商務端點

### 錯誤修正 {#bug-fixes-commerce}

* 根類別欄位未顯示在類別頁面的頁面屬性中的商務索引標籤下

## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.4.0中Cloud Manager的發行說明

### 發行日期 {#release-date-cm-april}

AEM as a Cloud Service 2021.4.0 中 Cloud Manager 的發行日期為 2021 年 4 月 08 日。下一個版本計劃於 2021 年 05 月 06 日發行。

### 新增功能 {#what-is-new-april}

* UI 更新成新增和編輯計劃工作流程，讓使用者介面更直覺。

* 具有必要權限的使用者現在可以透過 UI 提交商務端點。

* 環境變數現在可以將範圍限定至特定服務，即作者或發佈。需要 AEM 版本 `2021.03.5104.20210328T185548Z` 或更高版本

* **「管理 Git」** 按鈕於管線卡中顯示，即使尚未設定任何管線。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 27。

* 在 Adobe I/O Developer Console 中由 Cloud Manager 建立的專案不再可無意編輯或刪除。

* 使用者新增環境時，便會告知使用者，在建立環境後，即無法將環境移至不同區域。

* 環境變數現在可以將範圍限定至特定服務，即作者或發佈。需要 AEM 版本 2021.03.5104.20210328T185548Z 或更高版本

* 已釐清啟動管線時或刪除環境時的錯誤訊息。

* Eclipse 專案提供的 OSGi 產品組合現在已從規則 `CQBP-84--dependencies` 排除。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的體驗稽核頁面時，以斜杠開頭的輸入路徑`( / )`將不再導致步驟卡在掛起狀態。

* 建立新的生產管道時，如果使用者未新增任何內容稽核覆蓋，則預設主頁未經過稽核。

* 的問題`CloudServiceIncompatibleWorkflowProcess`可下載的問題 CSV 文件中的嚴重性不正確。

* `Runmode` 可檢查在非文件夾節點上產生誤報。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的發行日期為2021年4月12日。

### 錯誤修正 {#bug-fixes-bpa-april}

* 在報告的BPA中看到重複列。 此問題已修正。
* AEM 6.4.2版上的BPA UI擲回停用產生報告按鈕的JS錯誤。 此問題已修正
