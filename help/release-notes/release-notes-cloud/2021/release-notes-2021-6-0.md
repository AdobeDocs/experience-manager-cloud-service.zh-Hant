---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 21%

---

# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.6.0是2021年6月28日。
以下版本(2021.7.0)將於2021年7月29日發佈。

## 發佈視頻 {#release-video}

看看 [2021年6月發佈概述](https://video.tv.adobe.com/v/334296) 視頻，瞭解添加的功能的摘要。

## 作為雲服AEM務的XML文檔 {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* as a Cloud Service的XML文AEM檔現在正式啟動。
* 這將使現有的AEM Cloud Service客戶能夠購買XML文檔附加，以便跨多個渠道（包括站點）導入、建立、管理和提供技AEM術內容

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service和中的Cloud ManagerAEM的2021.6.0行說2021.5.0。

### 發行日期 {#release-date-june-cm}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年6月10日。
下一版計畫於2021年7月15日發行。

### 新增功能 {#what-is-new-junecm}

* 預覽服務將以滾動方式部署到所有程式。 客戶在為其預覽服務啟用計畫時將收到產品通知。 請參閱 [訪問預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 的子菜單。

* 現在，在生成步驟期間下載的Maven Dependencies將在管道執行之間快取。 此功能將在未來幾週內為客戶啟用。

* 現在，可以通過編輯程式對話框編輯程式的名稱。

* 在項目建立期間和通過管理Git工作流在預設推送命令中使用的預設分支名稱已更改為 `main`。

* 已刷新UI中的編輯程式體驗。

* 質量規則 `ImmutableMutableMixCheck` 已更新以分類 `/oak:index` 節點是不可變的。

* 質量規則 `CQBP-84` 和 `CQBP-84--dependencies` 被整合為一條規則。 作為此整合的一部分，對依賴項的掃描可以更準確地確定正在部署到運行時的第三方依賴項中AEM的問題。

* 為避免混淆，「環境詳細AEM資訊」頁上的「發佈」和「發佈調度程式」段行已合併。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 新代碼質量規則已添加以驗證 `damAssetLucene` 索引。 請參閱 [自定義DAM資產Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 的子菜單。

* 「環境詳細資訊」頁面現在將顯示發佈和預覽服務的多個域名（如果適用）。 請參閱 [環境詳細資訊](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 的雙曲餘切值。

### 錯誤修正 {#bug-fixes-junecm}

* 未正確分析根元素名稱后包含換行符的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為計畫步驟提供了無效值時，顯示錯誤錯誤消息。

* 有時，用戶可能看到綠色 *活動* 即使未部署該配置，「IP允許清單」旁邊的狀態也仍然存在。

* 某些程式編輯序列可能導致無法建立或編輯生產管線。

* 某些程式編輯序列可能導致 **概述** 顯示誤導性消息以重新執行程式設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#ga-features-assets}

* 內容自動化功能允許 [!DNL Experience Manager Assets] 利用 [!DNL Adobe Creative Cloud] API，可實現資產生產的自動化。 它通過顯著減少建立相同資產變體所需的時間和迭代來提高內容速度。 該功能不需要任何代碼，並可從DAM中運行。
* [!DNL Adobe Asset Link] v3.0 [!DNL Adobe Photoshop]。 [!DNL Adobe Illustrator], [!DNL Adobe InDesign] 和 [!DNL Adobe Asset Link] v2.0 [!DNL Adobe XD] 的子菜單。 它提供：

   * 支援 [!DNL Assets Essentials]。
   * 能夠自動連接到 [!DNL Experience Manager] 作為 [!DNL Cloud Service] 或 [!DNL Assets Essentials]。

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### 中提供的新功能 [!DNL Assets] 預釋放通道 {#beta-features-assets}

* 視圖設定將得到增強，以便用戶選擇預設視圖和預設排序參數。
* Linkshare下載功能使用提高下載速度的非同步下載。
* 用戶可以根據屬性謂詞搜索和篩選資料夾。
* [!DNL Experience Manager Assets] 嵌入了PDF查看器 [!DNL Adobe Document Cloud] 預覽支援的文檔。 此功能允許用戶預覽PDF和其他多頁檔案，而無需任何複雜處理。 這改進了功能奇偶校驗 [!DNL Experience Manager] 6.5

### 修正在[!DNL Assets]中的錯誤 {#bugs-fixed-assets}

* 將所有者添加到子資料夾時， [!DNL Assets] 還會添加與父資料夾所有者相同的用戶。 (CQ-4323737)
* 在將資產添加到收集時，如果用戶對「收集」搜索應用篩選器，則用戶無法查看「清單中的收集」視圖。 (CQ-4323181)
* 搜索檔案和資料夾時，如果用戶應用篩選器並選擇 [!UICONTROL 檔案和資料夾]，只顯示檔案，而不顯示資料夾。 (CQ-4319543)

## [!DNL Experience Manager Sites] 作為 [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#ga-features-sites}

* 「發佈到預覽層」現在在「站點管理UI」中顯示為頁面狀態
* 現在，發佈到預覽層將在操作結束時呈現預覽URL，並將URL保留在頁面屬性中以供以後參考

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* 新增篩選 AEM 收件匣中自訂欄的功能
* 新增使用最適化表單的主題編輯器和樣式圖層的功能，以設定驗證碼元件的樣式。
* 改善自動偵測來源 PDF 表單中邏輯區段並將這些區段轉換成對應的最適化表單面板的速度和準確性。
* 新增將 PDF 或 XDP 檔案從一個資料夾移至另一個資料夾的移動動作。

### [!DNL Forms]的 Beta 版功能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：通訊 API 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生最終表單文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表單 PDF 和 Adobe Acrobat 表單 (AcroForm) 產生列印 PDF。

* **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

### 修正在[!DNL Forms]中的錯誤 {#forms-bugs-fixed}

* 當欄位在透過表單資料模型 (FDM) 提交資料到後端服務前驗證時，雖然會成功驗證，但表單資料模型無法叫用發佈驗證。
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。這是AppleiOS的一個已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] 作為 [!DNL Cloud Service] {#screens}

本節概述AEM Screensas a Cloud Service的發行說明。

### 發行日期 {#release-date-june-screens}

AEM Screensas a Cloud Service發佈日期為2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>請參閱 [AEM Screensas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) 有關成功安裝、配置和運行螢幕as a Cloud Service所需的基礎知識的指南，並連結到詳細概念技術文檔。

* 批量設備註冊管理意味著提供大量播放器設備更快、更高效。

* 改進了設備、顯示和渠道清單視圖的搜索和篩選選項。

* 設備運行狀況快照通過提供關鍵狀態即可節省時間。

* 「對象詳細資訊」頁面提供了項目中每個對象最相關資訊的摘要。

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 內容片段的新CIF產品和類別引用資料類型(包括 產品/類別選取器UI支援)
* 新商務內容片段核心元件
* 後端支援全文商務搜AEM索
* Commerce核心元件支援Adobe CommerceSenseiRecs資料收集
* 類別頁的SEO友好型URL的改進
* 支援每個站點/配置的自定義HTTP標頭

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容傳輸工具v1.5.4的發佈日期為2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支援可選 [預拷貝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 添加到CTT中。 當源實例配置為使用AmazonS3或Azure Blob儲存資料儲存時，預拷貝步驟可用於顯著加快內容傳輸活動的提取和接收階段AEM。

* Guardrail已添加到CTT中，以防止用戶在資料在接收階段到達臨界點時停止接收並可能損壞資料。

* 提取日誌的描述性更強，有助於進行故障排除。

* 在UI中添加了更多描述性接收狀態消息。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 在停止Author實例上的攝取時，UI將先前在Publish實例上完成的攝取改寫為 `STOPPED` 從 `FINISHED`。 這個已經修復了。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.16版的發佈日期為2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能夠檢測並報告資料夾中缺少的子節點 `/content/dam`。

* 能夠檢測並報告所使用的最佳做法分析器版本。

### 錯誤修正 {#bug-fixes-bpa-latest}

* 與已修復的不受支援的儲存庫結構(URS)相關的日誌記錄錯誤。
