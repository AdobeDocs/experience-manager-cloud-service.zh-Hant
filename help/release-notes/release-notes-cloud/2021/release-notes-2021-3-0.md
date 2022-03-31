---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.3.0發行說明。」'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: 71647239fc5e740faa25524a01a8ef21ed2d7a3b
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 4%

---

# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

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

## [!DNL Adobe Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

AEM Forms多年來幫助許多組織提供了出色的寄宿和註冊體驗。 這些經驗幫助組織將銷售線索轉換為銷售線索，處理捕獲的客戶資料，根據受眾概況提供快速響應的體驗，等等。 現在，AEM Forms可以作為雲服務提供。

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 要建立數字表單，將表單連接到現有資料源，與Adobe Sign整合表單以向表單添加電子簽名，生成記錄文檔(DoR)以將提交的表單作為PDF檔案存檔。 該服務還可以將您現有的PDF forms轉換為數字表單。 除了標準的AEM Forms功能外，該服務還提供了多種雲本地功能，如自動擴展、升級零停機和雲本地開發環境。 閱讀 [此部落格帖子](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) 瞭解AEM Formsas a Cloud Service的功能和特性。

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

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年3月11日。
下一版計畫於2021年4月08日發行。

### 新增功能 {#what-is-new-march}

* 具有預先存在的自定義域名配置的環境的客戶 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)。 [SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) 和 [自定義域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 將看到有關其先前現有配置的消息，並能夠通過UI自助服務。

* 具有必要權限的用戶現在可以編輯程式，允許他們以自助方式執行以下操作：

   * 將「站點」解決方案添加到具有「資產」的現有程式，反之亦然。
   * 從具有站點和資產的現有程式中刪除站點或資產。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式。

* **推AEM送更新** 標籤現在將顯示 *管道執行* 和 *活動* 螢幕。

* 如果某個環境已休眠，但還有可AEM用的更新， **冬眠** 狀態將優先於 **更新可用**。

* 現在，用戶可以在導航到Unified Shell的「用戶配置檔案」表徵圖（右上）後選擇「查看雲管理器角色」選項來查看其雲管理器角色。

* 標籤 **申請審批** 被重新安排 **生產審批** 更清晰。

* 的 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行螢幕中。

* 當重要度量不滿足定義的閾值時定義行為的標籤已重新標籤，以反映其真實行為： **立即取消** 和 **立即批准**。

* 類和方法棄用清單已根據版本進行更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service軟體開發工具包。

* Cloud Manager生產管道現在將包括 [自定義UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 錯誤修正 {#bug-fixes-cm-march}

* 在某些情況下，在推送升級期間跳過了包AEM版本控制。

* 當將包嵌入到其他包中時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能是現有程式名稱的副本。

* 有時，如果用戶在啟動管道後立即從管道執行頁面導航出去，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行會開始。

* 當客戶生成導致無效包時，生成步驟不必要地重新啟動。

* 有時，即使未部署IP允許清單，用戶也可能看到該配置旁邊的綠色「活動」狀態。

* 使用「體驗審核」步驟將自動啟用所有現有生產管道。

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

## 最佳做法分析器 {#best-practices-analyzer}

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
