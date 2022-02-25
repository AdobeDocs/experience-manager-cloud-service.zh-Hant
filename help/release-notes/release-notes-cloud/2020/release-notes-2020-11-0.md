---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.11.0發行說明。」'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.11.0是2020年12月2日。
以下版本(2020.12.0)將於2020年12月17日發佈

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* **[啟動層次結構管理](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [未來時間曲線](/help/sites-cloud/authoring/launches/preview.md)**:在啟動中添加/刪除頁面的新UI，並使用Timewarp瀏覽網站顯示「啟動」中的未來狀態。

* **[擴展內容片段模型和編輯器](/help/assets/content-fragments/content-fragments-models.md)**:用於對各種資料類型進行輸入驗證的新選項、具有新表單可視化的改進的枚舉資料類型，以及內容片段模型名稱在資產UI中顯示和可搜索。

* **對可用於部署的Live Copy頁面進行排序**:新選項：使用 [!UICONTROL 名稱]。 [!UICONTROL 上次修改日期], [!UICONTROL 上次推廣日期] 屬性。 的 [!UICONTROL 上次推廣日期] 對於頁面是引入的新屬性。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### 中的新增功能 [!DNL Assets] 和 [!DNL Dynamic Media] {#what-is-new-assets}

* **批量資產接收**:為客戶提供可擴展的雲本地接收服務，該服務利用 [!DNL Experience Manager] as a Cloud Service架構，包括資產微服務。 關鍵使用案例包括通過監控、報告和計畫進行大規模接收，同時允許使用通用雲上傳工具將資產初始傳輸到雲資料儲存。 請參閱 [資產批量導入工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

   此工具適用於系統管理員、顧問或實施合作夥伴角色。 該功能允許大規模攝入，在初始攝入或偶爾大攝入期間理想地使用。 對於較小的攝取作業，請使用 [[!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) 或 [使用資產用戶介面上載](/help/assets/add-assets.md#upload-assets)。

   ![批量導入程式的配置](/help/assets/assets/bulk-import-config-low-res.png)

* 用戶現在可以在「卡」和「列」視圖中對數字資產進行排序。

   ![排序資產](/help/assets/assets/asset-sort-options.png)

* 對中的輔助功能執行了以下增強 [!DNL Experience Manager Assets] 在本版。 有關詳細資訊，請參見 [輔助功能 [!DNL Assets]](/help/assets/accessibility.md)。

   * 使用鍵盤導航時間軸時，Esc鍵可折疊「顯示全部」選項，而不會丟失焦點。
   * 使用鍵盤標籤鍵導航時，在從添加的標籤中刪除最後一個標籤後，標籤欄位將保留焦點。
   * [!DNL Experience Manager] 元件現在包含供螢幕閱讀器使用的名稱、角色和值的適當資訊。
   * 刪除「類型/大小」組合框、「連結」組合框、「語言」組合框或「文本編輯」框後，鍵盤焦點將返回下一個或上一個用戶介面元素或更相關的用戶介面元素。
   * 將指針懸停在選項上時，將顯示「選擇」和「下載」等提示。 使用螢幕放大鏡的用戶可能看不到檔案縮略圖，因為這些提示。 現在，在使用 `Escape` 按鈕
   * 從頁面中存在的網格中選擇網格單元格後，焦點將移到螢幕上顯示的操作欄。
   * 可視用戶可以區分普通文本和連結，因為顯示視覺線索（下划線和雪佛龍表徵圖），以便連結到中的所有解決方案 [!DNL Experience Manager] 的子菜單。

* **批集預設在Dynamic Media**:現在，您可以在將資產檔案單獨或使用批量攝取上載到資料夾時，自動建立和組織映像集或旋轉集中的多個資產。

   請參閱 [關於批集預設](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* 以下輔助功能增強功能現已在 [!DNL Dynamic Media]:

   * 螢幕閱讀器（JAWS、講述人）在「嵌入大小」菜單選項中描述菜單項的名稱、角色和狀態。
   * 用戶可以使用 `Tab` 按鈕
   * 建立視頻編碼配置檔案的工作流程更方便用戶，因為螢幕閱讀器增強了用戶的功能。
   * 導航時使用 `Tab` 鍵，焦點將移到工作流中相應的用戶介面元素以建立互動式視頻。
   * 「發佈」頁、「編輯資產」頁、「編輯智慧作物」頁和「影像集編輯器」頁將得到改進，以符合Web標準。 輔助技術(AT)用戶現在可以輕鬆瀏覽這些頁面並採取諸如裁剪影像之類的操作。
   * 改進觀看者，使用戶使用鍵盤導航。
   * 鍵盤和螢幕閱讀器用戶可以使用裁剪功能。
   * 鍵盤用戶可以更好地管理熱點。

   請參閱 [中的輔助功能 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF Venia參考站點 — 2020.11.05，包括最新的CIF核心元件版本v1.5.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) 的子菜單。

* 已發佈CIF核心元件v1.5.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) 的子菜單。

### 錯誤修正 {#bug-fixes-commerce}

* 當配置未直接在Sling CA配置中指定，而在父配置中指定時，GraphQL客戶端配置未正確讀取。 這個已經修復了。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager在as a Cloud Service中的發AEM布日期為2020年11月12日。

### [!DNL Cloud Manager]的新增功能 {#what-is-new-cm}

* 新菜單選項 **本地登錄** 現在可供用戶從 **環境** 卡和 **環境** 摘要頁面。
請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 的子菜單。

* 的 **學習** 已使用UI中的新映像刷新Cloud Manager中的頁籤。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在生成執行之前完成的依賴項的載入需要下載Maven插件。
* 從Cloud Manager頁腳中選擇語言的連結現在將導航到正確的位置。
* 有時，在代碼掃描期間，SonarQube進程不會啟動。 現在將自動檢測並嘗試重新啟動。
* 使用「體驗審核」步驟將自動啟用所有現有生產管道。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已添加支援，用於根據工作流標題、工作流模型、狀態、啟動器、負載路徑和開始日期搜索工作流實例。 請參閱 [搜索工作流實例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 發佈層用戶資料同步 {#user-sync}

* 用戶資料（包括配置檔案屬性和組成員）可以保留在發佈層上。 在中瞭解有關此功能的詳細資訊 [註冊、登錄和用戶配置檔案文檔](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)。

### SDK生成分析器 {#analyzers}

as a Cloud ServiceAEMSDK生成分析器Maven插件可檢測給定項目中的問題，包括缺少依賴項。 它為開發人員提供了在本地開發過程中發現問題的機會，而且遠在使用Cloud Manager部署到雲環境之前。 有關詳細資訊，請參閱文檔 [這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) 和 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新建 [&quot;httpd -t&quot;語法](/help/implementing/dispatcher/disp-overview.md#local-validation) 檢查在Cloud Manager生成期間執行的apache和dispatcher配置，也可以使用AEMas a Cloud ServiceSDK的Dispatcher Tools運行該配置。

## 內容轉移工具 {#content-transfer-tool}

請按照本部分瞭解新增內容和更新 [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改進了日誌的用戶體驗。 已添加到提取和接收日誌的時間戳。 添加的消息指示日誌是否為空。

### 錯誤修正 {#ctt-bug-fixes}

* 如果遷移集包含具有部分相似檔案名的路徑，則內容傳輸工具正在跳過內容檔案。 這個已經修復了。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器的發佈日期為2020年11月13日。

### [!DNL Best Practices Analyzer]的新增功能 {#what-is-new-bpa}

* 雲就緒性分析程式現在是最佳做法分析程式(BPA)。 BPA提供對您當前實施情況的AEM最佳實踐評估，並幫助評估從現有實例遷移到AEMas a Cloud Service的AEM準備情況。

* 增加了新的探測器以檢測 `java.io.InputStream`，如果在AEMas a Cloud Service中使用，則可能導致問題。

### 錯誤修正 {#bpa-bug-fixes}

* 導致與 *文本欄位基礎* 元件已修復。
