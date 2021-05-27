---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager] as aCloud Service{#release-notes}的最新發行說明

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>您可從此處導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.4.0的發行日期為2021年5月6日。
下列版本(2021.5.0)將於2021年5月27日發行。

## AEM as a Cloud Service基礎{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [發佈內容樹狀結構工作流程](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流程模型和步驟可在發佈內容的深層階層時提供更高的效能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* GraphQL端點 — 現在可以為個別AEM Sites設定啟用AEM GraphQL API，並可使用新的GraphQL主控台UI為這些設定建立自訂GraphQL端點。 UI也允許管理GraphQL端點。

* 內容模型，增強的日期與時間資料類型 — 現在可以設定日期與時間日期類型，僅允許編寫日期、時間或日期和時間資訊。

* 內容模型、增強標籤資料類型 — 現在可以設定標籤資料類型，以允許編寫單一或多個標籤。

* 內容模型、新的標籤佔位符資料類型 — 新的標籤佔位符資料類型允許將資料類型分組到內容片段編輯器中標籤下呈現的部分。

### [!DNL Sites] {#bug-fixes-sites}中的錯誤修正

* 內容片段 — 移動內容片段或資料夾現在會更新片段內的巢狀參考(CQ-4320815)

* GraphQL — 持續查詢現在支援專用於AEM Sites設定的使用者定義端點(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

* [!DNL Experience Manager] 不會封存下載原始檔案的單一資產下載。此增強功能可加快下載速度。

* 透過linkshare選項下載資產時，您現在可以選擇下載或不下載轉譯。 之前，會下載所有資產轉譯。

* 管理員可以設定[!DNL Experience Manager]在執行大量資產擷取後刪除資產來源。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 執行健全狀態檢查以大量匯入資產時，Experience Manager現在會提供失敗的詳細資訊原因。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 使用大量匯入工具匯入資產時，管理員現在可以選擇在匯入成功後刪除來源檔案。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 編輯中繼資料結構時，新的根路徑選擇器欄位可讓管理員快速輕鬆地進行選擇，從而縮短配置時間。

* 許多資產的中繼資料可使用CSV檔案大量匯入，也可匯出為CSV檔案。 預設日期格式現在為`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 使用者可更新欄標題，以運用不同格式。 例如，將`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`新增為CSV檔案中的欄標題，而非字詞`Date`。

* 在「欄」檢視中瀏覽資產時，視覺指標會顯示每個資產的已核准或已拒絕狀態。

* 在欄檢視中瀏覽資產時，會顯示過期資產的視覺指標。

### [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 嘗試移動多個資產或資料夾時，主控台中會記錄錯誤，且移動作業未完成。 如果無法更新標題，移動操作就會失敗。 (CQ-4322080)

* 元資料欄位可以根據規則來隱藏，以便當符合預先定義的條件時，元資料不是強制性的。 不過，這類隱藏的中繼資料欄位會顯示為必要欄位。 (CQ-4321285)

* 由於日期格式錯誤，大量中繼資料匯入失敗。 (CQ-4319014)

* 在「屬性」頁面中選取要更新中繼資料時，當結構提供許多選項時，介面回應速度緩慢。 (CQ-4318538)

* 在單行文字欄位中更新和儲存中繼資料值時，下拉式選單中的值會遭到刪除，即使下拉式選單中已停用編輯亦然。 (CQ-4317077)

* 您可以使用刪節號作為註解來檢閱資產。 使用小橢圓時，橢圓與打印版本中的注釋數重疊。 (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] {#what-is-new-forms}中的新增功能

* **在啟用Adobe Sign的適用性Forms中使用政府ID身分驗證方法**

   Adobe Sign的政府ID程式採用進階的機器學習演算法，讓全球公司能夠確保收件者身分的高品質驗證。 現在，您可以在啟用Adobe Sign的適用性Forms中使用政府ID身分驗證方法。

   政府ID是一種高級身份驗證方法，指示接收者[上傳政府頒發的身份證（駕照、國家ID、護照）](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)的影像，然後評估該檔案以確保其真實性。

* **支援非同步最適化表單提交使用表單內簽署體驗**

   您現在可以使用表單內簽署體驗，以非同步最適化表單提交。 您也可以在[!DNL Experience Manager Sites]頁面中嵌入最適化表單，並使用表單內簽署體驗來提交最適化表單。

* **支援在為「指派任務」步驟預填適用性表單時使用變數指定附件**

   為「指派任務」步驟預填適用性表單時，您現在可以使用檔案類型變數來為適用性表單選取輸入附件。

* **支援使用常值選項來設定JSON類型變數的值**

   您可以在AEM工作流程的設定變數步驟中使用文字選項來設定JSON類型變數的值。 文字選項可讓您以字串的形式指定JSON。

* **使用本地開發環境建立記錄文檔(DoR)**

   您可以在Cloud Service例項上使用XDP作為記錄檔案範本，並在AEM Forms作為Cloud ServiceSDK（本機開發環境）。 過去，支援僅限於Cloud Service例項。

### [!DNL Forms] {#bug-fixes-forms}中的錯誤修正

* 將配置為不生成記錄文檔的適用性表單提交到配置為生成記錄文檔的AEM工作流時，不會顯示錯誤消息，且任務無法提交。

### 其他更新{#misc-2021-04-0-forms}

* 為了更輕鬆辨識內容，服務現在會為XDP、動態PDF和結構檔案產生即時縮圖。
* 新增將PDF檔案移至AEM Forms UI中放置之資料夾的功能。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援類別UID — 如此可為使用字串作為類別ID的系統解除鎖定第三方商務整合

* AEM的PWA Studio擴充功能，包括 範例整合

* 擴展WCM導覽核心元件的全新CIF導覽核心元件

* AEM店面中分段目錄資料的視覺指示器

* 現在可透過Cloud Manager UI設定Commerce端點

### 錯誤修正 {#bug-fixes-commerce}

* 根類別欄位沒有顯示在類別頁面的頁面屬性中的商務標籤下

## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.4.0Cloud Service中Cloud Manager的發行說明。

### 發行日期 {#release-date-cm-april}

AEM as aCloud Service2021.4.0中的Cloud Manager發行日期為2021年4月8日。
下一版預計於2021年5月6日發行。

### 新功能 {#what-is-new-april}

* 新增和編輯方案工作流程的UI更新，讓工作流程更直覺。

* 擁有必要權限的使用者現在可以透過UI提交商務端點。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管道，「管道」卡上也會顯示&#x200B;**管理Git**&#x200B;按鈕。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 由Cloud Manager建立的「Adobe I/O開發人員控制台」中的專案，不能再無意中編輯或刪除。

* 當使用者新增新環境時，系統會通知他們，一旦建立環境，就無法將其移至其他區域。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM 2021.03.5104.20210328T185548Z或更高版本。

* 已釐清刪除環境時啟動管道時的錯誤訊息。

* Eclipse專案提供的OSGi套件組合現已從規則`CQBP-84--dependencies`中排除。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的「體驗」稽核頁面時，以斜線`( / )`開頭的輸入路徑不會再導致步驟卡在擱置狀態。

* 建立新生產管道時，如果使用者未新增任何內容稽核覆寫，則不會稽核預設首頁。

* `CloudServiceIncompatibleWorkflowProcess`的問題在可下載的問題CSV檔案中嚴重性不正確。

* `Runmode`檢查對非資料夾節點產生誤判。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的發行日期為2021年4月12日。

### 錯誤修正 {#bug-fixes-bpa-april}

* 報告的BPA中出現重複行。 此問題已修正。
* AEM 6.4.2版上的BPA UI會擲回停用「產生報表」按鈕的JS錯誤。 此問題已修正

