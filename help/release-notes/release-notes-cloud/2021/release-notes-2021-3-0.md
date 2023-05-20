---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.3.0發行說明。」'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: acd80887d71a528604d37fa2787bca3c3a48d7c4
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 38%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.3.0是2021年3月25日。
以下版本(2021.4.0)將於2021年4月29日發佈。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [站點的漸進式Web應用(PWA)版本](/help/sites-cloud/authoring/features/enable-pwa.md) 現在可以通過簡單的配置在項目級別啟用。
* 內容片段模型擴展 — 現在可以將多行文本資料類型定義為多欄位清單。
* 內容片段編輯器UX增強 — 現在在breadcrumb中顯示的嵌套子片段，以及發佈、保存和保存和退出操作的改進視圖

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 擴展了Connected Assets功能，支援使用 [!DNL Dynamic Media] 支援的核心元件中的影像。 請參閱 [使用連接的資產](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理員可以在特定日期或時間安排批量資產接收。 此外，管理員還可以根據日期和時間計畫定期接收。 請參閱 [批量資產消耗](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 嘗試下載多個版權管理資產時，不顯示版權頁。 (CQ-4314403)
* 選擇編輯INDD檔案時，解析度會意外更改。 (CQ-4317376)
* 「InDesign模板」的最後一頁僅位於PDF格式副本中。 (CQ-4317305)
* 當選取器是複雜元資料架構的一部分時，標籤選取器需要很長時間才能開啟。 (CQ-4316426)
* 上載與現有檔案名相同的資產時，不會顯示名稱衝突對話框以提示用戶建立版本。 (CQ-4315424)
* 可以從資料夾的「屬性」頁的彈出式菜單中設定並保存資料夾元資料屬性。 選擇內容保存在儲存庫中時，在再次開啟資料夾元資料屬性時不顯示。 (CQ-4314429)
* 使用瀏覽器上載檔案名包含空格或特殊字元的資產。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms多年來幫助許多組織提供了出色的寄宿和註冊體驗。 這些經驗幫助組織將銷售線索轉換為銷售線索，處理捕獲的客戶資料，根據受眾概況提供快速響應的體驗，等等。 現在，AEM Forms可以作為雲服務提供。

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 要建立數字表單，將表單連接到現有資料源，與Adobe Sign整合表單以向表單添加電子簽名，生成記錄文檔(DoR)以將提交的表單作為PDF檔案存檔。 該服務還可以將您現有的PDF forms轉換為數字表單。 除了標準的AEM Forms功能外，該服務還提供了多種雲本地功能，如自動擴展、升級零停機和雲本地開發環境。

您可以聯繫Adobe代表進行演示或註冊該服務。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支援Adobe Commerce2.4.2

* 現在可以在任何內容頁面上使用和配置產品詳細資訊元件

* 已發佈CIF Venia參考站點 — 2021.03.25，包括最新的CIF核心元件版本v1.9.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) 的子菜單。

* 已發佈CIF核心元件v1.9.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) 的子菜單。


## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service2021.3.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 發行日期是 2021 年 3 月 11 日。下一版本計劃於 2021 年 4 月 08 日發行。

### 新增功能 {#what-is-new-march}

* 如果客戶的環境中已有 [IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂網域名稱設定，將看到有關其先前現有設定的訊息，也可透過 UI 進行自助服務。

* 擁有必要權限的使用者現在可以編輯方案，好讓他們以自助方式執行以下作業：

   * 使用 Assets 將 Sites 解決方案新增現有計畫中，反之亦然。
   * 從包含 Sites 和 Assets 的現有方案中移除 Sites 或 Assets。
   * 在現有方案中新增第二個未使用的解決方案權利，或當做新的方案。

* **推AEM送更新** 標籤現在將顯示 *管道執行* 和 *活動* 螢幕。

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

內容傳輸工具v1.3.4的發佈日期為2021年3月19日。

### 錯誤修正 {#bug-fixes-ctt}

* CTT正在跳過具有相同名稱但名稱中帶連字元的資料夾中的內容。 這個已經修復了。

### 發行日期 {#release-date-ctt-march}

內容傳輸工具v1.3.0的發佈日期為2021年3月4日。

### 內容傳輸工具中的新增功能 {#what-is-new-ctt-march}

* CTT現在安裝到 `/apps` 而不是 `/libs` 某些頁面的瀏覽器書籤可能不再有效。
* 安裝CTT後，用戶將必須導航其他級別才能進入「內容傳輸」頁。 請參閱 [使用內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) 的子菜單。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑遷移內容時， CTT會引入不相關的資源。 已修復

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.8版的發佈日期為2021年3月22日。

### 最佳做法分析器中的新增功能 {#what-is-new-bpa}

* 能夠從UI中的BPA報告以及導出為CSV檔案的報告中篩選出ACS公域查找結果。

## 程式碼重構工具 {#code-refactoring-tools}

### 代碼重構工具中的新增功能 {#what-is-new-crt}

* Repository Modernizer的新功能和增強功能。 請參閱 [GitHub資源：儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 的下界。
   * 將OSGi配置（除RepoInit配置外）規範化為首選.cfg.json格式。
   * 將OSGi配置資料夾更名為指定格式。
   * 生成ui.apps.structure項目。
   * 建立分析模組。

* Dispatcher Converter的新功能和增強功能。 請參閱 [GitHub資源：調度器轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同的inclusion建立單獨的檔案，而不是在內容的內襯中。
   * 能夠處理vhosts的資料夾路徑和vhost檔案的路徑。
   * 生成具有600個以上大型客戶配置的場檔案。
