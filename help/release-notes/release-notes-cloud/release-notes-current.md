---
title: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: 8ca3fe045aba4ec9e546fee0700d1bec08e337fb
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作為{#release-notes}Cloud Service的當前發行說明

以下章節概述[!DNL Experience Manager]目前（最新）版本的一般發行說明，做為Cloud Service。

>[!NOTE]
>您可從此處瀏覽至舊版的發行說明；例如2020年、2021年等。

>[!NOTE]
>
>如需與發行版本無直接關聯的檔案更新詳細資訊，請參閱[最新檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.4.0的發行日期為2021年5月6日。
下列版本(2021.5.0)將於2021年5月27日發行。

## 作AEM為Cloud Service基金會{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) -新的工作流程模型和步驟可在發佈內容的深層階層時，提供更高的效能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* GraphQL端點——現在可以為各個AEM SitesAEM配置啟用GraphQL API，並通過使用新的GraphQL控制台UI為這些配置建立自定義GraphQL端點。 UI還允許管理GraphQL端點。

* 內容模型、增強的日期與時間資料類型——現在可以設定日期與時間日期類型，讓您只能編寫日期、時間或日期和時間資訊。

* 內容模型、增強的標籤資料類型——現在可以設定標籤資料類型，以允許製作單一或多個標籤。

* 內容模型、新的標籤預留位置資料類型——新的標籤預留位置資料類型可將資料類型分組到內容片段編輯器中標籤下方的區段中。

### [!DNL Sites] {#bug-fixes-sites}中的錯誤修正

* 內容片段——移動內容片段或資料夾現在會更新片段內的巢狀參照(CQ-4320815)

* GraphQL —— 持久查詢現在支援特定於AEM Sites配置的用戶定義端點(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

* [!DNL Experience Manager] 不會封存下載原始檔案的單一資產下載。此增強功能可讓下載更快速。

* 透過linkshare選項下載資產時，您現在可以選擇下載或不下載轉譯。 以前，會下載所有資產轉譯。

* 管理員可以設定[!DNL Experience Manager]，在執行大量資產擷取後刪除資產來源。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 當執行健康檢查以大量匯入資產時，Experience Manager現在會提供失敗的更多資訊原因。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 使用大量匯入工具匯入資產時，管理員現在可以選擇在匯入成功後刪除來源檔案。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 編輯中繼資料結構時，新的根路徑選擇器欄位可讓管理員快速輕鬆地進行選擇，進而縮短設定時間。

* 許多資產的中繼資料可使用CSV檔案大量匯入，並可匯出至CSV檔案。 預設日期格式現在為`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 使用者可以透過更新欄標題來運用不同的格式。 例如，在CSV檔案中新增`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`作為欄標題，而非字詞`Date`。

* 在「欄」檢視中瀏覽資產時，視覺指標會顯示每個資產的已核准或已拒絕狀態。

* 在「欄」檢視中瀏覽資產時，會顯示過期資產的視覺指標。

### [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 嘗試移動多個資產或檔案夾時，主控台中會記錄錯誤，且移動作業尚未完成。 如果無法更新標題，移動操作將失敗。 (CQ-4322080)

* 元資料欄位可以基於規則進行隱藏，以便當滿足預定條件時，元資料不是強制的。 不過，這類隱藏的中繼資料欄位會顯示為必要欄位。 (CQ-4321285)

* 大量中繼資料匯入因日期格式不正確而失敗。 (CQ-4319014)

* 當在「屬性」頁面中選擇更新中繼資料時，當架構提供許多選項時，介面的回應速度會變慢。 (CQ-4318538)

* 在單行文字欄位中更新和儲存中繼資料值時，即使在下拉式功能表中停用編輯，下拉式功能表中的值也會被刪除。 (CQ-4317077)

* 您可以使用省略號做為註解來檢閱資產。 使用小橢圓時，橢圓與打印版本中的注釋數重疊。 (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] {#what-is-new-forms}的新增功能

您可以使用[AEM FormsCloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)來建立數位表單、將表單連接至現有資料來源、將表單與Adobe Sign整合以新增電子簽名至表單、產生記錄檔案(DoR)以將提交的表單封存為PDF檔案。 此服務也可將您現有的PDF forms轉換為數位表單。 除了標準的AEM Forms功能外，該服務還提供數種雲端原生功能，例如自動縮放、升級零停機和雲端原生開發環境。 閱讀[此部落格文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)，瞭解AEM Forms作為Cloud Service的功能與功能。

* **在啟用Adobe Sign的自適應Forms中使用政府ID身份驗證方法**

   在進階機器學習演算法的支援下，Adobe Sign的政府ID程式可讓全球各地的公司確保接受者身分的高品質驗證。 現在，您可以在啟用Adobe Sign的最適化Forms中使用政府ID身分驗證方法。

   政府ID是高階身分驗證方法，可指示收件者[上傳政府核發的身分檔案（駕照、國家ID、護照）](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)的影像，然後評估該檔案以確保其真實性。

* **支援使用表單內簽署體驗進行非同步的調適性表單提交**

   您現在可以針對非同步自適應表單提交使用表單內簽署體驗。 您也可以在[!DNL Experience Manager Sites]頁面中內嵌最適化表單，並使用表單中的簽署體驗來提交最適化表單。

* **支援在為「分配任務」步驟預填充「最適化表單」時使用變數指定附件**

   在為分配任務步驟預填充最適化表單時，您現在可以使用文檔類型變數為最適化表單選擇輸入附件。

* **支援使用常值選項來設定JSON類型變數的值**

   您可以使用常值選項，在「工作流程」的設定變數步驟中設定JSON類型變AEM數的值。 常值選項可讓您以字串的形式指定JSON。

* **使用本機開發環境來建立記錄檔案(DoR)**

   您可以在Cloud Service實例上使用XDP作為記錄文檔模板，而AEM Forms作為Cloud ServiceSDK（本地開發環境）。 以前，支援僅限Cloud Service例項。

### [!DNL Forms] {#bug-fixes-forms}中的錯誤修正

* 將配置為不生成記錄文檔的最適化表單提交到配置為生成記錄文檔的AEM工作流時，不顯示錯誤消息，並且任務無法提交。

### 其他更新{#misc-2021-04-0-forms}

* 為了更容易辨識內容，服務現在會針對XDP、動態PDF和架構檔案產生即時縮圖。
* 新增將PDF檔案移至AEM FormsUI中資料夾的功能。

## Adobe Experience Manager商務Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援類別UID —— 這可為使用類別ID字串的系統解除協力廠商商務整合鎖定

* AEM擴充PWA Studio 範例整合

* 擴充WCM導覽核心元件的全新CIF導覽核心元件

* 店面中分段型錄資料的可視指AEM示器

* 商務端點現在可透過Cloud Manager UI進行設定

### 錯誤修正 {#bug-fixes-commerce}

* 類別頁面的頁面屬性中，根類別欄位未顯示在商務標籤下方


## Cloud Manager {#cloud-manager}

本節將以Cloud Service2021.5.0和AEM2021.4.0概述Cloud Manager的發行說明。

### 發行日期 {#release-date-cm-may}

Cloud Manager作為2021.5.0版Cloud ServiceAEM的發行日期為2021年5月6日。
下一版預計於2021年6月03日推出。

### 新功能 {#what-is-new-may}

* PackageOverlaps品質規則現在會偵測在相同部署的套件集中，同一套件已部署多次（即在多個內嵌位置）的情況。

* Public API中的儲存庫端點現在包含Git URL。

* 由Cloud Manager用戶下載的部署日誌將更加深入，現在將包含有關失敗和成功案例的詳細資訊。

* 現在已解決將程式碼推送至AdobeGit時間不斷發生的故障。

* 商務附加元件現在可在編輯程式工作流程中套用至沙盒程式。

* 編輯程式體驗已重新整理。

* 「環境詳細資訊」(Environment Details)頁中的「域名」(Domain Names)表將通過分頁顯示多達250個域名。

* 「新增方案」和「編輯方案」工作流程中的「解決方案」索引標籤會顯示解決方案，即使方案只提供一個解決方案。

* 當組建未產生任何已部署的內容封裝時，不清楚組建步驟記錄中的錯誤訊息。

### 錯誤修正 {#bug-fixes-cm-may}

* 有時，即使未部署IP允許清單，使用者仍可能在該設定旁看到綠色的「作用中」狀態。

* 管線變數API不會移除&#39;deleted&#39;變數，而只會以狀態&#x200B;**DELETED**&#x200B;來標籤它們。

* 某些「程式碼氣味」類型的品質問題錯誤地影響「可靠性評等」。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當管道執行在午夜到凌晨1點之間啟動時，Cloud Manager生成的對象版本不保證大於前一天建立的版本。

* 在沙盒程式設定期間，當已成功建立包含范常式式碼的專案後，「管理Git」就會在「概述」頁面中顯示為英雄卡的連結。

### 發行日期 {#release-date-cm-april}

Cloud Manager作為2021.4.0Cloud ServiceAEM的發行日期為2021年4月08日。

### 新功能 {#what-is-new-april}

* UI更新至「新增及編輯程式」工作流程，使其更直覺。

* 具備必要權限的使用者現在可以透過UI提交商務端點。

* 環境變數現在可以限定到特定服務的範圍，可以是作者或發佈。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管線，「管理Git」（管理Git）按鈕也會顯示在「管線」卡上。****

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 由Cloud Manager建立的Adobe I/O開發人員主控台中的專案，不會再無意間被編輯或刪除。

* 當用戶添加新環境時，他們將被告知，一旦建立了環境，就不能將其移動到其他區域。

* 環境變數現在可以限定到特定服務的範圍，可以是作者或發佈。 需AEM要2021.03.5104.20210328T185548Z或更高版本。

* 刪除環境時啟動管線時的錯誤消息已被澄清。

* Eclipse專案提供的OSGi組合現在已排除在規則`CQBP-84--dependencies`之外。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管線的「體驗」稽核頁面時，以斜線`( / )`開頭的輸入路徑不會再導致步驟卡在擱置狀態。

* 當建立新的生產管道時，如果使用者未新增內容審核覆寫，則不會審核預設首頁。

* `CloudServiceIncompatibleWorkflowProcess`的問題在可下載的問題CSV檔案中嚴重性不正確。

* `Runmode`檢查對非資料夾節點產生誤報。

## 最佳做法分析器{#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的發行日期為2021年4月12日。

### 錯誤修正 {#bug-fixes-bpa-april}

* 報告的BPA中出現重複行。 這個問題已經修正。
* 6.4.2版AEM的BPA UI會造成JS錯誤，此錯誤會停用「產生報表」按鈕。 此問題已修正

