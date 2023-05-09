---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.3.0版發行說明。」'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: acd80887d71a528604d37fa2787bca3c3a48d7c4
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 38%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>您可從此處導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.3.0為2021年3月25日。
下列版本(2021.4.0)將於2021年4月29日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [網站的漸進式網頁應用程式(PWA)版本](/help/sites-cloud/authoring/features/enable-pwa.md) 現在可透過簡單的設定，在專案層級啟用。
* 內容片段模型擴充功能 — 現在可將多行文字資料類型定義為多欄位清單。
* 內容片段編輯器UX增強功能 — 巢狀子片段現在顯示在階層連結中，並改善發佈、儲存和儲存&amp;退出動作的檢視

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 延伸「連線資產」功能，以支援使用 [!DNL Dynamic Media] 支援核心元件中的影像。 請參閱 [使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md).
* Experience Manager管理員可以在特定日期或時間排程大量資產擷取。 此外，管理員也可以根據日期和時間排程週期性擷取。 請參閱 [大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor).

### [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 嘗試下載多個權限管理資產時，不會顯示版權頁面。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度意外更改。 (CQ-4317376)
* 「InDesign轉譯」中只有PDF範本的最後一頁。 (CQ-4317305)
* 當選擇器是複雜中繼資料結構的一部分時，標籤選擇器需要很長的時間才能開啟。 (CQ-4316426)
* 上傳的資產檔案名稱與現有資產相同時，不會顯示名稱衝突對話方塊以提示使用者建立版本。 (CQ-4315424)
* 可以從資料夾的「屬性」頁面的彈出菜單設定並保存資料夾元資料屬性。 選擇項保存在儲存庫中，但在重新開啟「資料夾元資料屬性」時不顯示。 (CQ-4314429)
* 檔案名稱包含空格或特殊字元的資產會透過瀏覽器上傳。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms多年來協助許多組織提供絕佳的入門和註冊體驗。 這些體驗可協助組織將銷售機會轉換為銷售機會、處理擷取的客戶資料、根據受眾設定檔提供回應式體驗，以及執行其他更多功能。 現在，AEM Forms能以雲端服務形式提供使用。

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 若要建立數位表單，請將表單連線至現有的資料來源，將表單與Adobe Sign整合以將電子簽名新增至表單，產生記錄檔(DoR)以將提交的表單封存為PDF檔案。 此服務也可將您現有的PDF forms轉換為數位表單。 除了標準AEM Forms功能外，此服務還提供數種雲端原生功能，例如自動調整規模、為升級停機時間零，以及雲端原生開發環境。

您可以聯絡Adobe代表以觀看示範或註冊服務。

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Adobe Commerce 2.4.2

* 您現在可以在任何內容頁面上使用和設定產品詳細資料元件

* CIF Venia Reference Site - 2021.03.25已發行，其中包含最新CIF核心元件1.9.0版。請參閱 [CIF Venia參考站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) 以取得更多詳細資訊。

* CIF核心元件1.9.0版已發行。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) 以取得更多詳細資訊。


## Cloud Manager {#cloud-manager}

本節概述AEM 2021.3.0中Cloud Manageras a Cloud Service的發行說明。

## 發行日期 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 發行日期是 2021 年 3 月 11 日。下一版本計劃於 2021 年 4 月 08 日發行。

### 新增功能 {#what-is-new-march}

* 如果客戶的環境中已有 [IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂網域名稱設定，將看到有關其先前現有設定的訊息，也可透過 UI 進行自助服務。

* 擁有必要權限的使用者現在可以編輯方案，好讓他們以自助方式執行以下作業：

   * 使用 Assets 將 Sites 解決方案新增現有計畫中，反之亦然。
   * 從包含 Sites 和 Assets 的現有方案中移除 Sites 或 Assets。
   * 在現有方案中新增第二個未使用的解決方案權利，或當做新的方案。

* **AEM推播更新** 標籤現在會針對 *管道執行* 和 *活動* 螢幕。

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

* 在不明確的情況下，打開「新增計畫」對話框時生成的預設程序名稱可能與現有程序名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面，則會顯示一則錯誤消息，指出操作失敗，儘管執行實際上已開始。

* 當客戶構建導致無效包時，構建步驟不必要地重新啟動。

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 所有現有的生產管道都將透過體驗稽核步驟自動啟用。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容轉移工具1.3.4版的發行日期為2021年3月19日。

### 錯誤修正 {#bug-fixes-ctt}

* CTT正在跳過同名資料夾中的內容，但名稱中帶有連字型大小。 此問題已修正。

### 發行日期 {#release-date-ctt-march}

內容轉移工具1.3.0版的發行日期為2021年3月4日。

### 「內容轉移工具」的新功能 {#what-is-new-ctt-march}

* CTT現在安裝至 `/apps` 而非 `/libs` 瀏覽器書籤至特定頁面可能已無效。
* 安裝CTT時，使用者必須導覽其他層級才能前往「內容轉移」頁面。 請參閱 [使用內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此問題已修正

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8的發行日期為2021年3月22日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠從UI中的BPA報表以及匯出為CSV檔案的報表中篩除ACS公域結果。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具的新功能 {#what-is-new-crt}

* Repository Modernizer的新功能和增強功能。 請參閱 [GitHub資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) ，以取得最新版本。
   * 將OSGi設定（RepoInit設定除外）標準化為偏好的.cfg.json格式。
   * 將OSGi配置資料夾更名為指定的格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher轉換工具的新功能和增強功能。 請參閱 [GitHub資源：Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同包含建立不同的檔案，而不是在內容內襯中。
   * 能夠處理vhost的資料夾路徑和vhost檔案的路徑。
   * 以600個或更多的範圍內的大型客戶配置生成伺服器陣列檔案。
