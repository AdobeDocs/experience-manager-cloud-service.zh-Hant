---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 25%

---

# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.4.0是2021年5月6日。
以下版本(2021.5.0)將於2021年5月27日發佈。

## AEMas a Cloud Service{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流模型和步驟在發佈深層內容層次結構時提供了更高的效能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* GraphQL終結點 — 現在可以為各個AEM Sites配置啟AEM用GraphQL API，並使用新的GraphQL控制台UI為這些配置建立自定義GraphQL終結點。 UI還允許管理GraphQL端點。

* 內容模型，增強的日期和時間資料類型 — 現在可以將日期和時間日期類型配置為僅允許創作日期、僅時間或日期和時間資訊。

* 內容模型、增強的標籤資料類型 — 現在可以配置標籤資料類型以允許創作單個或多個標籤。

* 「內容模型」、新的「制表符佔位符」資料類型 — 新的「制表符佔位符」資料類型允許將資料類型分組到內容片段編輯器中頁籤下將呈現的部分中。

### [!DNL Sites]中的錯誤修正 {#bug-fixes-sites}

* 內容片段 — 移動內容片段或資料夾現在會更新片段內的嵌套引用(CQ-4320815)

* GraphQL — 永續查詢現在支援特定於AEM Sites配置的用戶定義終結點(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* [!DNL Experience Manager] 不存檔下載原始檔案的單個資產下載。 此增強功能可加快下載速度。

* 通過連結共用選項下載資產時，您現在可以選擇下載或不下載格式副本。 以前，已下載所有資產格式副本。

* 管理員可以配置 [!DNL Experience Manager] 執行批量資產提取後刪除資產源。 請參閱 [批量資產消耗](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 當執行運行狀況檢查以批量導入資產時，Experience Manager現在提供了失敗的更多資訊原因。 請參閱 [批量資產消耗](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 使用批量導入工具導入資產時，管理員現在可以選擇在導入成功後刪除源檔案。 請參閱 [批量資產消耗](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 在編輯元資料架構時，新的根路徑選擇器欄位允許管理員快速而輕鬆地進行選擇，從而減少配置時間。

* 在編輯元資料模式時，會添加在元資料編輯器中提供自由格式文本區域的資料類型。 用戶可以使用此文本區域輸入自由格式文本作為資產的元資料。 請參閱 [元資料架構編輯器](/help/assets/metadata-schemas.md)。

* 許多資產的元資料可以使用CSV檔案批量導入，並可以導出到CSV檔案。 預設日期格式現在為 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 用戶可以通過更新列標題來利用不同的格式。 例如，添加 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` 作為CSV檔案中的列標題，而不是 `Date`。

* 在「列」視圖中瀏覽資產時，可視指示器會顯示每個資產的已批准或已拒絕狀態。

* 在「列」視圖中瀏覽資產時，將顯示過期資產的可視指示器。

### [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 嘗試移動多個資產或資料夾時，控制台中會記錄錯誤，移動操作未完成。 如果無法更新標題，則移動操作將失敗。 (CQ-4322080)

* 元資料欄位可以基於規則被隱藏，使得當滿足預定義條件時元資料不是必需的。 但是，此類隱藏的元資料欄位會顯示為必填欄位。 (CQ-4321285)

* 由於日期格式不正確，批量元資料導入失敗。 (CQ-4319014)

* 當在「屬性」頁中選擇更新元資料時，當架構提供了許多選項時，介面響應速度較慢。 (CQ-4318538)

* 在單行文本欄位中更新和保存元資料值時，即使在下拉菜單中禁用了編輯，下拉菜單中的值也會被刪除。 (CQ-4317077)

* 可以使用省略號作為注釋來查看資產。 使用小橢圓時，該橢圓與打印版本中注釋的數量重疊。 (CQ-4316792)

* 在搜索後從搜索結果中選擇資產時，不顯示快速發佈選項。 (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

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

* 為便於識別內容，服務現在會為XDP、動態PDF和架構檔案生成即時縮略圖。
* 添加將PDF檔案移動到AEM FormsUI上的資料夾的功能。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援類別UID — 此操作可解除鎖定使用字串進行類別ID的系統的第三方商務整合

* 擴展AEMPWA Studio，包括 示例整合

* 擴展WCM導航核心元件的新CIF導航核心元件

* 庫面中暫存目錄資料的可視指AEM示器

* 現在可通過Cloud Manager UI配置Commerce終結點

### 錯誤修正 {#bug-fixes-commerce}

* 根類別欄位未顯示在類別頁的頁面屬性中的commerce頁籤下

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.4.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-date-cm-april}

Cloud Manager在as a Cloud Service中的發AEM布日期為2021年4月8日。
下一版計畫於2021年5月6日發行。

### 新增功能 {#what-is-new-april}

* UI更新「添加和編輯程式」工作流，使其更直觀。

* 具有必要權限的用戶現在可以通過UI提交商業終點。

* 現在，環境變數可以限定到特定服務的範圍，即作者或發佈。 需要版AEM本 `2021.03.5104.20210328T185548Z` 或更高。

* 的 **管理Git** 即使尚未配置管線，也會在管線卡上顯示。

* Cloud Manager使用的AEM項目原型版本已更新為版本27。

* Cloud Manager建立的Adobe I/O開發人員控制台中的項目不能再被無意地編輯或刪除。

* 當用戶添加新環境時，他們將被告知，一旦建立了一個環境，就不能將其移動到其他區域。

* 現在，環境變數可以限定到特定服務的範圍，即作者或發佈。 需要AEM2021.03.5104.20210328T185548Z或更高版本。

* 已澄清刪除環境時啟動管道時的錯誤消息。

* Eclipse項目提供的OSGi捆綁包現在已從規則中排除 `CQBP-84--dependencies`。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的「體驗」審計頁時，輸入路徑以斜槓開頭 `( / )` 將不再導致該步驟處於掛起狀態。

* 建立新生產管道時，如果用戶未添加內容審核覆蓋，則未審核預設首頁。

* 針對 `CloudServiceIncompatibleWorkflowProcess` 可下載問題CSV檔案中的嚴重性不正確。

* 的 `Runmode` 檢查在非資料夾節點上產生誤報。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.12版的發佈日期為2021年4月12日。

### 錯誤修正 {#bug-fixes-bpa-april}

* 報告的BPA中出現重複行。 這個已經修復了。
* 6.4.2版中的BPA AEM UI引發了禁用「生成報告」按鈕的JS錯誤。 已修復
