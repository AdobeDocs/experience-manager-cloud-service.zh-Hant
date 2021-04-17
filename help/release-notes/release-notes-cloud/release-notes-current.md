---
title: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: affe1f0be3f3448e15787cdd831474e0a9d5de6b
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager]作為{#release-notes}Cloud Service的當前發行說明

以下章節概述[!DNL Experience Manager]目前（最新）版本的一般發行說明，做為Cloud Service。

>[!NOTE]
>您可從此處瀏覽至舊版的發行說明；例如2020年、2021年等。

>[!NOTE]
>
>如需與發行版本無直接關聯的檔案更新詳細資訊，請參閱[最新檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.3.0的發行日期為2021年3月25日。
下列版本(2021.4.0)將於2021年4月29日發行。

## [!DNL Adobe Experience Manager Sites] Cloud Service  {#sites}

* [現在，可透過簡單的設定，在專](/help/sites-cloud/authoring/features/enable-pwa.md) 案層級啟用網站的漸進式網頁應用程式(PWA)版本。
* 內容片段模型擴充功能——現在可將多行文字資料類型定義為多欄位清單。
* 內容片段編輯器UX增強功能——巢狀子片段現在顯示在階層連結中，並改善發佈、儲存和儲存與退出動作的檢視

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 擴充Connected Assets功能，以支援在支 [!DNL Dynamic Media] 援的核心元件中使用影像。請參閱[使用連接的資產](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理員可以在特定日期或時間排程大量資產收錄。 此外，管理員也可以根據日期和時間排程週期性收錄。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 嘗試下載多個版權管理的資產時，不會顯示版權頁面。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度意外更改。 (CQ-4317376)
* 「PDF轉譯」中只有「InDesign範本」的最後一頁。 (CQ-4317305)
* 當選擇器是複雜中繼資料結構的一部分時，開啟標籤選擇器需要很長的時間。 (CQ-4316426)
* 上傳與現有檔案名稱相同的資產時，不會顯示名稱衝突對話方塊，提示使用者建立版本。 (CQ-4315424)
* 可以在資料夾的「屬性」頁面的彈出菜單中設定和保存資料夾元資料屬性。 選擇保存在儲存庫中時，當再次開啟資料夾元資料屬性時不顯示。 (CQ-4314429)
* 檔案名稱包含空格或特殊字元的資產會使用瀏覽器上傳。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

AEM Forms多年來協助許多組織提供絕佳的入門和註冊體驗。 這些體驗可協助組織將潛在客戶轉化為銷售、處理擷取的客戶資料、根據受眾個人檔案提供互動式體驗等。 現在，AEM Forms提供雲端服務。

您可以使用[AEM FormsCloud Service](https://experienceleague.corp.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)來建立數位表單、將表單連接至現有資料來源、將表單與Adobe Sign整合以新增電子簽名至表單、產生記錄檔案(DoR)以將提交的表單封存為PDF檔案。 此服務也可將您現有的PDF forms轉換為數位表單。 除了標準的AEM Forms功能外，該服務還提供數種雲端原生功能，例如自動縮放、升級零停機和雲端原生開發環境。 閱讀[此部落格文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)，瞭解AEM Forms作為Cloud Service的功能與功能。

您可以聯絡Adobe代表以取得示範或註冊服務。

## Adobe Experience Manager商務Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Magento2.4.2

* 產品詳細資訊元件現在可在任何內容頁面上使用和設定

* 發佈的CIF Venia參考網站- 2021.03.25，其中包含最新的CIF核心元件1.9.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)。

* 已發佈CIF核心元件v1.9.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)。


## Cloud Manager {#cloud-manager}

本節將以Cloud Service2021.4.0和AEM2021.3.0概述Cloud Manager的發行說明。

### 發行日期 {#release-date-cm-april}

Cloud Manager作為2021.4.0Cloud ServiceAEM的發行日期為2021年4月08日。
下一版預計於2021年5月06日推出。

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


### 發行日期 {#release-date-cm-march}

Cloud Manager作為2021.3.0Cloud ServiceAEM的發行日期為2021年3月11日。

### 新功能 {#what-is-new-march}

* 具有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自訂域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂域名配置的環境的客戶將看到有關其先前現有配置的消息，並能夠通過UI自助服務。

* 具備必要權限的使用者現在可以編輯程式，讓他們以自助方式進行下列作業：

   * 將Sites解決方案新增至包含資產的現有計畫，反之亦然。
   * 將網站或資產從既有的計畫中移除，同時包含網站和資產。
   * 將第二個未使用的解決方案權益新增至現有的方案，或新增為新的方案。

* **現AEM在，「Pipeline  Execution」（管線執行）和「Activity」（活動）畫面都會** 顯 *示推播更新*  ** 標籤。

* 如果環境已休眠，但也有可用的更AEM新，則&#x200B;**已休眠**&#x200B;狀態將優先於&#x200B;**可用更新**。

* 現在，在導覽至Unified Shell的「使用者設定檔」圖示（右上角）後，使用者可以選取「檢視雲端管理員角色」選項，以查看其Cloud Manager角色。

* **申請批准**&#x200B;標籤已重新標籤至&#x200B;**生產批准**，以更清楚明瞭。

* **版本**&#x200B;標籤已重新標籤至「生產管線」執行畫面中的&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標籤，以反映其真實行為：**取消立即**&#x200B;和&#x200B;**批准立即**。

* 類別和方法取代清單已根據Cloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版AEM本更新。

* Cloud Manager生產管道現在將包含[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正 {#bug-fixes-cm-march}

* 在推播升級期間，在某些情況下會略過套AEM件版本。

* 在將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能是現有程式名稱的副本。

* 有時，如果用戶在啟動管線後立即導航離開管線執行頁面，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行開始。

* 當客戶建置導致無效包時，不必要地重新啟動建置步驟。

* 有時，即使未部署IP允許清單，用戶也會看到該配置旁邊的綠色「活動」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.3.4的發行日期為2021年3月19日。

### 錯誤修正 {#bug-fixes-ctt}

* CTT正在跳過同名但名稱中帶有連字型大小的資料夾中的內容。 這個問題已經修正。

### 發行日期 {#release-date-ctt-march}

內容傳輸工具v1.3.0的發行日期為2021年3月04日。

### 內容傳輸工具{#what-is-new-ctt-march}的新增功能

* CTT現在會安裝至`/apps`，而非`/libs`特定頁面的瀏覽器書籤可能不再有效。
* 當安裝CTT時，使用者將必須導覽其他層級，才能進入「內容傳輸」頁面。 如需詳細資訊，請參閱[使用內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此問題已修正

## 最佳做法分析器{#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的發行日期為2021年4月12日。

### 錯誤修正 {#bug-fixes-bpa-april}

* 報告的BPA中出現重複行。 這個問題已經修正。
* 6.4.2版AEM的BPA UI會造成JS錯誤，此錯誤會停用「產生報表」按鈕。 此問題已修正


## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具{#what-is-new-crt}的新增功能

* Repository Modernizer的新功能和增強功能。 請參閱[GitHub資源：最新版本的Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 將OSGi組態標準化為偏好的。cfg.json格式（RepoInit組態除外）。
   * 將OSGi配置資料夾更名為指定格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher Converter的新功能和增強功能。 請參閱[GitHub資源：Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同內含項目建立個別檔案，而非內容內嵌。
   * 能夠同時處理vhosts的資料夾路徑和vhost檔案的路徑。
   * 以超過600種客戶配置生成群檔案。
