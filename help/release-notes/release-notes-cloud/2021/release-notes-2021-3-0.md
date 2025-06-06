---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: "[!DNL Adobe Experience Manager]個2021.3.0版as a Cloud Service發行說明。"
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 32%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>您可以從此導覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2021.3.0的發行日期為2021年3月25日。
下列版本(2021.4.0)將於2021年4月29日發行。

## [!DNL Adobe Experience Manager Sites]個as a Cloud Service {#sites}

* [網站的漸進式網頁應用程式(PWA)版本](/help/sites-cloud/authoring/sites-console/enable-pwa.md)現在可透過簡易設定在專案層級啟用。
* 內容片段模型延伸功能 — 現在可將多行文字資料型別定義為多欄位清單。
* 內容片段編輯器UX增強功能 — 巢狀子系片段現在顯示在階層連結中，並改善發佈、儲存和儲存並結束動作的檢視

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager]延伸連線Assets功能，以支援在支援的核心元件中使用[!DNL Dynamic Media]影像。 請參閱[使用連線的Assets](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理員可以在特定日期或時間排程大量資產擷取。 此外，管理員可以根據日期和時間排程週期性內嵌。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 嘗試下載多個版權管理的資產時，版權頁面未顯示。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度會意外變更。 (CQ-4317376)
* 只有InDesign範本的最後一頁存在於PDF轉譯中。 (CQ-4317305)
* 當選取器是複雜中繼資料結構的一部分時，標籤選取器需要很長時間才能開啟。 (CQ-4316426)
* 上傳與現有資產檔名相同的資產時，不會顯示名稱衝突對話方塊以提示使用者建立版本。 (CQ-4315424)
* 資料夾中繼資料屬性可從資料夾的「屬性」頁面中的彈出式選單設定及儲存。 當選取專案儲存在存放庫時，再次開啟資料夾中繼資料屬性時不會顯示該選取專案。 (CQ-4314429)
* 檔案名稱包含空格或特殊字元的Assets會使用瀏覽器上傳。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms在多年來已幫助許多組織提供絕佳的上線和註冊體驗。 這些體驗已幫助組織將銷售線索轉換為銷售、處理擷取的客戶資料、根據受眾個人資料提供回應靈敏的體驗等等。 現在，AEM Forms以Cloud Service的形式提供。

您可以使用[AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html?lang=zh-Hant)來建立數位表格、將表格連結到現有的資料來源、將表格與Adobe Sign整合以將電子簽章新增至表格、產生記錄檔案(DoR)以將提交的表格封存為PDF檔案。 此服務也可以將您現有的PDF forms轉換為數位表格。 除了標準AEM Forms功能外，此服務也提供幾個雲端原生功能，像是自動縮放、升級時的零停機時間，以及雲端原生開發環境。

您可以聯絡您的Adobe代表來要求示範或註冊此服務。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Adobe Commerce 2.4.2

* 產品詳細資料元件現在可以在任何內容頁面上使用和設定

* 已發行CIF Venia參考網站 — 2021.03.25，其中包含最新CIF核心元件1.9.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)。

* 已發行CIF Core Components v1.9.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)。


## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.3.0中Cloud Manager的發行說明

## 發行日期 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0中Cloud Manager的發行日期為2021年3月11日。
下一版本計畫於2021年4月8日發行。

### 新增功能 {#what-is-new-march}

* 如果客戶的環境中已有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂網域名稱設定，可檢視有關其先前現有設定的訊息，並可透過使用者介面進行自助服務。

* 擁有必要權限的使用者現在可以編輯方案，好讓他們以自助方式執行以下作業：

   * 將網站解決方案新增到有資產的現有方案中，反之亦然。
   * 從包含 Sites 和 Assets 的現有計畫中移除 Sites 或 Assets。
   * 在現有計畫中新增第二個未使用的解決方案權利，或當做新的計畫。

* **AEM推播更新**&#x200B;標籤現在會同時顯示在&#x200B;*管線執行*&#x200B;和&#x200B;*活動*&#x200B;畫面中。

* 如果環境處於休眠狀態，但同時有 AEM 更新可用，則&#x200B;**已休眠**&#x200B;狀態會優先於&#x200B;**有可用的更新**。

* 使用者現在可以在瀏覽至 Unified Shell 的使用者個人資料圖示 (右上方) 後選取「檢視 Cloud Manager 角色」選項，以查看其 Cloud Manager 角色。

* **申請核准**&#x200B;標籤現在已重新標記為&#x200B;**生產核准**，好讓人更容易了解。

* **版本**&#x200B;標籤現已在生產管線執行畫面中重新標記為 **Git Tag**。

* 定義重要度量不符合定義之臨界值時的行為模式的標籤已重新標記，以反映其真正的行為：**立即取消**&#x200B;和&#x200B;**立即核准**。

* 已根據 AEM Cloud Service SDK 的版本 `2021.3.4997.20210303T022849Z-210225` 更新了類別和方法淘汰清單。

* Cloud Manager 生產管線現在包含[自訂 UI 測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正 {#bug-fixes-cm-march}

* 在 AEM 推送升級期間，某些情況下會跳過套件版本控制。

* 當套件嵌入到其他套件中時，部分品質問題沒有被發現。

* 在不明確的情況下，打開「新增計畫」對話框時生成的預設計畫名稱可能與現有計畫名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面，則會顯示一則錯誤消息，指出操作失敗，儘管執行實際上已開始。

* 當客戶構建導致無效包時，構建步驟不必要地重新啟動。

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.3.4的發行日期為2021年3月19日。

### 錯誤修正 {#bug-fixes-ctt}

* CTT已略過名稱相同但名稱中包含連字型大小的資料夾內容。 此問題已修正。

### 發行日期 {#release-date-ctt-march}

內容轉移工具v1.3.0的發行日期為2021年3月4日。

### 內容轉移工具的新增功能 {#what-is-new-ctt-march}

* CTT現在安裝至`/apps`，而非`/libs`。特定頁面的瀏覽器書籤可能已失效。
* 安裝CTT時，使用者必須瀏覽其他層級，才能前往「內容轉移」頁面。 如需詳細資訊，請參閱[使用內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=zh-Hant)。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此問題已修正

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8的發行日期為2021年3月22日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠篩選掉使用者介面中BPA報告以及匯出為CSV檔案的報告中的ACS Commons發現。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具的新增功能 {#what-is-new-crt}

* Repository Modernizer的新功能和增強功能。 如需最新版本，請參閱[GitHub資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 將OSGi設定（RepoInit設定除外）標準化為慣用的.cfg.json格式。
   * 將OSGi設定資料夾重新命名為指定格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher Converter的新功能和增強功能。 請參閱[GitHub資源： Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同的包含專案建立個別檔案，而不是在內容中排行。
   * 能夠處理vhosts的資料夾路徑和vhost檔案的路徑。
   * 產生具有範圍在600及更多的大型客戶設定的伺服器陣列檔案。
