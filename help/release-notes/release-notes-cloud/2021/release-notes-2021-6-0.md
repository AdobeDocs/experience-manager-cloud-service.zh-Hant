---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版發行說明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 21%

---

# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service的2021.6.0是2021年6月28日。
下列版本(2021.7.0)將於2021年7月29日發行。

## 發行影片 {#release-video}

查看 [2021年6月發行概述](https://video.tv.adobe.com/v/334296) 視訊，以取得新增功能的摘要。

## XML Documentation for AEM as a cloud service {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* XML Documentation for AEMas a Cloud Service現已正式發行。
* 這可讓現有AEM Cloud Service客戶購買XML Documentation addon，以便跨多個管道(包括AEM網站)匯入、建立、管理和傳遞技術內容

## Cloud Manager {#cloud-manager}

本節概述AEM 2021.6.0和2021.5.0中Cloud Manageras a Cloud Service的發行說明。

### 發行日期 {#release-date-june-cm}

AEM 2021.6.0中的Cloud Manageras a Cloud Service日期為2021年6月10日。
下一版預計於2021年7月15日發行。

### 新增功能 {#what-is-new-junecm}

* 預覽服務將以滾動方式部署到所有程式。 當客戶的計畫啟用預覽服務時，將在產品中收到通知。 請參閱 [存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 以取得更多詳細資訊。

* 現在，系統會在管道執行之間快取建置步驟期間下載的Maven相依性。 此功能將在未來數週內為客戶啟用。

* 現在可以通過編輯程式對話框編輯程式的名稱。

* 在專案建立期間和透過管理Git工作流程的預設推送命令中使用的預設分支名稱，已變更為 `main`.

* 重新整理UI中的編輯方案體驗。

* 品質規則 `ImmutableMutableMixCheck` 已更新為可分類 `/oak:index` 節點不可修改。

* 品質規則 `CQBP-84` 和 `CQBP-84--dependencies` 已整合為單一規則。 作為此整合的一部分，對依賴項的掃描可以更準確地識別部署到AEM運行時的第三方依賴項中的問題。

* 為避免混淆，「環境詳細資料」頁面上的「發佈AEM」和「發佈Dispatcher」區段列已整合。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 已新增新的程式碼品質規則，以驗證 `damAssetLucene` 索引。 請參閱 [自訂DAM資產Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 以取得更多詳細資訊。

* 環境詳細資訊頁面現在會顯示「發佈」和「預覽」服務的多個網域名稱（如適用）。 請參閱 [環境詳細資訊](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes-junecm}

* 未正確剖析根元素名稱后包含新行的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為排程步驟提供無效值時，顯示錯誤錯誤訊息。

* 有時，使用者可能會看到綠色 *活動* 狀態（即使未部署該配置）。

* 某些程式編輯序列可能導致無法建立或編輯生產管道。

* 某些程式編輯序列可能會導致 **概述** 顯示誤導性消息的頁面，以重新執行程式設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#ga-features-assets}

* 內容自動化功能可讓 [!DNL Experience Manager Assets] 善用 [!DNL Adobe Creative Cloud] API可大規模自動化資產生產。 它可大幅減少建立相同資產變異所需的時間和迭代次數，進而改善內容速度。 功能不需要任何程式碼，且可在DAM內運作。
* [!DNL Adobe Asset Link] v3.0 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]，和 [!DNL Adobe InDesign] 和 [!DNL Adobe Asset Link] v2.0 [!DNL Adobe XD] 已發行。 它提供：

   * 支援 [!DNL Assets Essentials].
   * 自動連線至 [!DNL Experience Manager] as a [!DNL Cloud Service] 或 [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### 此 [!DNL Assets] 預發行管道 {#beta-features-assets}

* 已增強檢視設定，讓使用者選擇預設檢視和預設排序參數。
* Linkshare下載功能使用非同步下載，可大幅提升下載速度。
* 使用者可以根據屬性述詞來搜尋和篩選資料夾。
* [!DNL Experience Manager Assets] 內嵌PDF檢視器，由 [!DNL Adobe Document Cloud] 預覽支援的文檔。 此功能可讓使用者預覽PDF和其他多頁檔案，而不需進行任何複雜的處理。 這可改善與 [!DNL Experience Manager] 6.5。

### 修正在[!DNL Assets]中的錯誤 {#bugs-fixed-assets}

* 將所有者添加到子資料夾時， [!DNL Assets] 也會新增與父資料夾擁有者相同的使用者。 (CQ-4323737)
* 將資產新增至集合時，如果使用者對「集合」搜尋套用篩選，則使用者無法在「清單」檢視中檢視集合。 (CQ-4323181)
* 搜索檔案和資料夾時，如果用戶應用了篩選器並選擇 [!UICONTROL 檔案和資料夾]，只會顯示檔案，不會顯示資料夾。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#ga-features-sites}

* 發佈至預覽層級現在在Sites Admin UI中顯示為頁面狀態
* 發佈到預覽層現在會在動作結束時呈現預覽URL，並將URL保留在頁面屬性中以供稍後參考

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

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
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。這是Apple iOS的已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

本節概述AEM Screens as a Cloud Service的發行說明。

### 發行日期 {#release-date-june-screens}

AEM Screensas a Cloud Service的發行日期為2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>請參閱 [AEM Screensas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) 成功安裝、設定和執行Screensas a Cloud Service所需基礎知識的指南，以及詳細概念技術檔案的連結。

* 批量設備註冊管理意味著提供大量播放器設備更快、更高效。

* 改善裝置、顯示和管道詳細目錄檢視的搜尋和篩選選項。

* 設備健康快照通過提供關鍵狀態如一覽而節省時間。

* 「對象詳細資訊」頁為項目中的每個對象提供了最相關資訊的摘要。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 內容片段的新CIF產品和類別參考資料類型(包括 產品/類別選擇器UI支援)
* 新商務內容片段核心元件
* AEM後端支援的全文商務搜尋
* 商務核心元件支援Adobe Commerce Sensei Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標題

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.5.4版的發行日期為2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支援選用 [預復](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 與CTT搭配使用的步驟。 當來源AEM例項設定為使用Amazon S3或Azure Blob儲存資料存放區時，預先複製步驟可用來大幅加快內容傳輸活動的擷取和擷取階段。

* CTT新增了防護性功能，以防止使用者在擷取階段期間達到關鍵點時停止擷取，並可能損毀資料。

* 提取記錄檔的描述性更強，有助於疑難排解。

* 在UI中新增了較清楚描述的擷取狀態訊息。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 在製作例項上停止擷取時，UI會將先前完成的擷取覆寫至 `STOPPED` 從 `FINISHED`. 此問題已修正。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的發行日期為2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能夠偵測資料夾中遺失的子節點並製作報表 `/content/dam`.

* 能夠偵測並報告所使用的最佳實務分析器版本。

### 錯誤修正 {#bug-fixes-bpa-latest}

* 修正了與不支援的存放庫結構(URS)相關的記錄錯誤。
