---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a 2021.3.0的Cloud Service發行說明。'
source-git-commit: 3ff105507f4d42f5858a7e3a4c703d9135b36e5b
workflow-type: tm+mt
source-wordcount: '1318'
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

[!DNL Adobe Experience Manager]作為Cloud Service2021.3.0的發行日期為2021年3月25日。
下列版本(2021.4.0)將於2021年4月29日發行。

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

* [現在，網站的漸進式網頁應用程式(](/help/sites-cloud/authoring/features/enable-pwa.md) PWA)版本可透過簡單的設定，在專案層級啟用。
* 內容片段模型擴充功能 — 現在可將多行文字資料類型定義為多欄位清單。
* 內容片段編輯器UX增強功能 — 巢狀子片段現在顯示在階層連結中，並改善發佈、儲存和儲存&amp;退出動作的檢視

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 延伸「連線資產」功能，以支援支 [!DNL Dynamic Media] 援核心元件中使用影像。請參閱[使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理員可以在特定日期或時間排程大量資產擷取。 此外，管理員也可以根據日期和時間排程週期性擷取。 請參閱[大量資產擷取](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 嘗試下載多個權限管理資產時，不會顯示版權頁面。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度意外更改。 (CQ-4317376)
* PDF轉譯中只有InDesign範本的最後一頁。 (CQ-4317305)
* 當選擇器是複雜中繼資料結構的一部分時，標籤選擇器需要很長的時間才能開啟。 (CQ-4316426)
* 上傳的資產檔案名稱與現有資產相同時，不會顯示名稱衝突對話方塊以提示使用者建立版本。 (CQ-4315424)
* 可以從資料夾的「屬性」頁面的彈出菜單設定並保存資料夾元資料屬性。 選擇項保存在儲存庫中，但在重新開啟「資料夾元資料屬性」時不顯示。 (CQ-4314429)
* 檔案名稱包含空格或特殊字元的資產會透過瀏覽器上傳。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

AEM Forms多年來協助許多組織提供絕佳的入門和註冊體驗。 這些體驗可協助組織將銷售機會轉換為銷售機會、處理擷取的客戶資料、根據受眾設定檔提供回應式體驗，以及執行其他更多功能。 現在，AEM Forms能以雲端服務形式提供使用。

您可以使用[AEM Forms作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)來建立數位表單、將表單連接至現有的資料來源、將表單與Adobe Sign整合以將電子簽名新增至表單、產生記錄檔(DoR)以將提交的表單封存為PDF檔案。 此服務也可將您現有的PDF forms轉換為數位表單。 除了標準AEM Forms功能外，此服務還提供數種雲端原生功能，例如自動調整規模、為升級停機時間零，以及雲端原生開發環境。 請閱讀[此部落格文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)以了解AEM Forms as aCloud Service的功能和特色。

您可以聯絡Adobe代表以觀看示範或註冊服務。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Magento2.4.2

* 您現在可以在任何內容頁面上使用和設定產品詳細資料元件

* CIF Venia Reference Site - 2021.03.25版已發行，其中包含最新CIF核心元件1.9.0版。如需詳細資訊，請參閱[CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)。

* CIF核心元件v1.9.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) 。


## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.3.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date-cm-march}

AEM as aCloud Service2021.3.0中的Cloud Manager發行日期為2021年3月11日。
下一版預計於2021年4月8日發行。

### 新功能 {#what-is-new-march}

* 若客戶的環境中已有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的先前自訂網域名稱設定，則會看到有關其先前現有設定的訊息，且將能透過UI自行服務。

* 擁有必要權限的使用者現在可以編輯方案，讓他們能以自助方式執行下列作業：

   * 使用資產將Sites解決方案新增至現有計畫，反之亦然。
   * 從同時具有Sites和Assets的現有程式中移除Sites或Assets。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式添加。

* **AEM推播** 更新標籤現在會針對Pipeline執行和 *Activity* Screen顯示 ** 。

* 如果環境已休眠，但也有AEM更新可用，則&#x200B;**已休眠**&#x200B;狀態將優先於&#x200B;**可用更新**。

* 使用者現在可以在導覽至統一殼層的「使用者設定檔」圖示（右上）後，選取「檢視Cloud Manager角色」選項，查看其Cloud Manager角色。

* 標籤&#x200B;**申請核准**&#x200B;已重新標示為&#x200B;**生產核准**，以更清楚明瞭。

* 在「生產管道」執行畫面中，**Version**&#x200B;標籤已重新標示為&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為：**取消立即**&#x200B;和&#x200B;**立即批准**。

* 類別和方法取代清單已根據AEMCloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版本更新。

* Cloud Manager生產管道現在將包含[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

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

### 內容轉移工具{#what-is-new-ctt-march}的新增功能

* CTT現在會安裝至`/apps`而非`/libs`瀏覽器書籤至特定頁面可能已無效。
* 安裝CTT時，使用者必須導覽其他層級才能前往「內容轉移」頁面。 如需詳細資訊，請參閱[使用內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) 。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此問題已修正

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8的發行日期為2021年3月22日。

### Best Practices Analyzer {#what-is-new-bpa}的新增功能

* 能夠從UI中的BPA報表以及匯出為CSV檔案的報表中篩除ACS公域結果。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具{#what-is-new-crt}的新增功能

* Repository Modernizer的新功能和增強功能。 請參閱[GitHub資源：最新版本的Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 將OSGi設定（RepoInit設定除外）標準化為偏好的.cfg.json格式。
   * 將OSGi配置資料夾更名為指定的格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher轉換工具的新功能和增強功能。 請參閱[GitHub資源：Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同包含建立不同的檔案，而不是在內容內襯中。
   * 能夠處理vhost的資料夾路徑和vhost檔案的路徑。
   * 以600個或更多的範圍內的大型客戶配置生成伺服器陣列檔案。
