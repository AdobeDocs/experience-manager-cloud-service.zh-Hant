---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.3.0版發行說明。」'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: 71647239fc5e740faa25524a01a8ef21ed2d7a3b
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 4%

---

# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>您可從此處導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

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

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 若要建立數位表單，請將表單連線至現有的資料來源，將表單與Adobe Sign整合以將電子簽名新增至表單，產生記錄檔(DoR)以將提交的表單封存為PDF檔案。 此服務也可將您現有的PDF forms轉換為數位表單。 除了標準AEM Forms功能外，此服務還提供數種雲端原生功能，例如自動調整規模、為升級停機時間零，以及雲端原生開發環境。 閱讀 [此部落格貼文](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) 了解AEM Forms as a Cloud Service的功能與特色。

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

AEM 2021.3.0中的Cloud Manageras a Cloud Service日期為2021年3月11日。
下一版預計於2021年4月8日發行。

### 新增功能 {#what-is-new-march}

* 環境中具有預先存在之自訂網域名稱設定的客戶 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) 和 [自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 會看到其先前現有設定的相關訊息，且將能透過UI自助服務。

* 擁有必要權限的使用者現在可以編輯方案，讓他們能以自助方式執行下列作業：

   * 使用資產將Sites解決方案新增至現有計畫，反之亦然。
   * 從同時具有Sites和Assets的現有程式中移除Sites或Assets。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式添加。

* **AEM推播更新** 標籤現在會針對 *管道執行* 和 *活動* 螢幕。

* 如果環境休眠，但也有AEM更新可用，則 **休眠** 狀態優先於 **可用更新**.

* 使用者現在可以在導覽至統一殼層的「使用者設定檔」圖示（右上）後，選取「檢視Cloud Manager角色」選項，查看其Cloud Manager角色。

* 標籤 **申請批准** 已重新標籤為 **生產核准** 更清晰。

* 此 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行畫面中。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為： **立即取消** 和 **立即核准**.

* 類別和方法取代清單已根據版本更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID服務。

* Cloud Manager生產管道現在將包含 [自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 錯誤修正 {#bug-fixes-cm-march}

* 在AEM推送升級期間，在某些情況下會略過套件版本設定。

* 將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能與現有程式名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面進行導覽，雖然實際上會開始執行，但會顯示錯誤訊息，指出動作失敗。

* 當客戶建置導致無效的套件時，建置步驟會不必要地重新啟動。

* 有時，即使未部署該設定，使用者仍可能會在IP允許清單旁看到綠色的「作用中」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

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

## Best Practices Analyzer {#best-practices-analyzer}

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
