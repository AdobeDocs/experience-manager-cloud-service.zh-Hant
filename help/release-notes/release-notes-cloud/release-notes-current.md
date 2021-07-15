---
title: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 96f2c99caebd446288720adaf4ac929bbc41950f
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager]作為Cloud Service的最新發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.6.0的發行日期為2021年6月28日。
下列版本(2021.7.0)將於2021年7月29日發行。

## 發行影片 {#release-video}

查看2021年6月[發行概述](https://video.tv.adobe.com/v/334296)影片，以取得新增功能的摘要。

## AEM as a Cloud Service的XML檔案 {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* AEM as aCloud Service的XML檔案現已正式發行。
* 這可讓現有AEMCloud Service客戶購買XML檔案新增功能，以匯入、建立、管理和傳送跨多個管道(包括AEM網站)的技術內容

## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.7.0和2021.6.0Cloud Service中Cloud Manager的發行說明。

### 發行日期 {#release-cm-july}

AEM as aCloud Service2021.7.0中的Cloud Manager發行日期為2021年7月15日。
下一版預計於2021年8月12日發行。

### 新增功能 {#what-is-new-cm-july}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建進程，並且可以選擇將其中一個JDK用於與工具鏈相容的Maven插件&#x200B;*或*&#x200B;整個Maven進程執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* 執行舊版AEM的預備和生產環境現在會回報&#x200B;**可用更新**&#x200B;狀態。

* 支援的SSL憑證上限已提高至每個程式20個。

* 每個環境可配置的域數上限已增加到500個。

* **管理Git**&#x200B;按鈕已重新命名為&#x200B;**存取Git資訊**，對話方塊也已視覺化重新整理。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

### 錯誤修正 {#bug-fixes-cm-july}

* 在某些情況下，將IP允許清單系結至環境時，「預覽」不是可用選項。

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 達到最大SSL憑證數時顯示的錯誤訊息並無幫助。

* 在某些情況下，**概述**&#x200B;頁面上的管道卡片所顯示的發行版本可能會不一致。

* 添加程式嚮導未正確說明建立後無法更改名稱。

### 已知問題 {#known-issues-cm-july}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。

### 發行日期 {#release-date-june-cm}

AEM as aCloud Service2021.6.0中的Cloud Manager發行日期為2021年6月10日。
下一版預計於2021年7月15日發行。

### 新增功能 {#what-is-new-junecm}

* 預覽服務將以滾動方式部署到所有程式。 當客戶的計畫啟用預覽服務時，將在產品中收到通知。 如需詳細資訊，請參閱[存取預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 。

* 現在，系統會在管道執行之間快取建置步驟期間下載的Maven相依性。 此功能將在未來數週內為客戶啟用。

* 現在可以通過編輯程式對話框編輯程式的名稱。

* 專案建立期間和透過管理Git工作流程的預設推送命令中使用的預設分支名稱已變更為`main`。

* 重新整理UI中的編輯方案體驗。

* 品質規則`ImmutableMutableMixCheck`已更新，將`/oak:index`節點分類為不可變。

* 品質規則`CQBP-84`和`CQBP-84--dependencies`已整合為單一規則。 作為此整合的一部分，對依賴項的掃描可以更準確地識別部署到AEM運行時的第三方依賴項中的問題。

* 為避免混淆，「環境詳細資料」頁面上的「發佈AEM」和「發佈Dispatcher」區段列已整合。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 已新增新的程式碼品質規則，以驗證`damAssetLucene`索引的結構。 如需詳細資訊，請參閱[自訂DAM資產Lucene Oak Indexes](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 。

* 環境詳細資訊頁面現在會顯示「發佈」和「預覽」服務的多個網域名稱（如適用）。 如需詳細資訊，請參閱[環境詳細資料](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 。

### 錯誤修正 {#bug-fixes-junecm}

* 未正確剖析根元素名稱后包含新行的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為排程步驟提供無效值時，顯示錯誤錯誤訊息。

* 有時，即使未部署該配置，使用者仍可能在IP允許清單旁看到綠色的&#x200B;*active*&#x200B;狀態。

* 某些程式編輯序列可能導致無法建立或編輯生產管道。

* 某些程式編輯序列可能導致在&#x200B;**概述**&#x200B;頁中顯示一條誤導性消息以重新執行程式設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]中的新功能 {#ga-features-assets}

* 「內容自動化」功能可讓[!DNL Experience Manager Assets]運用[!DNL Adobe Creative Cloud] API大規模自動化資產生產。 它可大幅減少建立相同資產變異所需的時間和迭代次數，借此改善內容速度。 此功能不需要任何程式設計，也可在DAM內運作。 請參閱[使用Creative Cloud整合產生資產變異](/help/assets/cc-api-integration.md)。

* [[!DNL Adobe Asset Link] v3.0](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) (適 [!DNL Adobe Photoshop]用) [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign] v2. [[!DNL Adobe Asset Link] 0](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link-for-xd.html) (適 [!DNL Adobe XD] 用)。它提供：

   * 支援[!DNL Assets Essentials]。
   * 能以[!DNL Cloud Service]或[!DNL Assets Essentials]形式自動連接到[!DNL Experience Manager]。

* [資產大量擷取工具](/help/assets/add-assets.md#asset-bulk-ingestor)可讓您在大量擷取期間新增中繼資料。

### [!DNL Assets]發行前通道中提供的新功能 {#beta-features-assets}

* 已增強檢視設定，讓使用者選擇預設檢視和預設排序參數。

   ![在「視圖設定」中設定預設視圖](/help/assets/assets/view-settings-for-defaults.png)

* Linkshare下載功能使用非同步下載，可大幅提升下載速度。 請參閱[下載使用連結共用的共用資產](/help/assets/download-assets-from-aem.md#link-share-download)。

   ![下載收件匣](/help/assets/assets/download-inbox.png)

* 使用者可以根據屬性述詞來搜尋和篩選資料夾。

   ![使用搜索謂詞篩選搜索資料夾](/help/assets/assets/search-folders-via-predicates.png)

* [!DNL Experience Manager Assets] 嵌入PDF查看器以預覽支援的文檔格式。它由[!DNL Adobe Document Cloud]提供。 此功能可讓使用者預覽PDF和其他多頁檔案，而不需進行任何複雜的處理。 這改進了[!DNL Experience Manager] 6.5的同等功能。預覽中可用的控制項是縮放、導覽至頁面、取消固定控制項，以及全螢幕檢視。 整合的PDF檢視器支援AI、DOCX、INDD、PDF和PSD檔案格式。 您可以對資產本身加上註解，但不支援在PDF檔案中加上註解和註解。

   ![使用PDF查看器 [!DNL Experience Manager] 預覽PDF檔案](/help/assets/assets/preview-pdf-file-viewer.png)

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若資料夾中超過1000個資產， [!DNL Assets]會顯示1000+。

   ![介面上會顯示資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

* 您可以將中繼資料結構直接套用至其[!UICONTROL Properties]中的資料夾。

   ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

### [!DNL Assets]中修正的錯誤 {#bugs-fixed-assets}

* 將所有者添加到子資料夾時， [!DNL Assets]還會添加與父資料夾所有者相同的用戶。 (CQ-4323737)
* 將資產新增至集合時，如果使用者對「集合」搜尋套用篩選，則使用者無法在「清單」檢視中檢視集合。 (CQ-4323181)
* 在搜索檔案和資料夾時，如果用戶應用篩選器並選擇[!UICONTROL 檔案和資料夾]，則只顯示檔案，而不顯示資料夾。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a  [!DNL Cloud Service] {#sites}

### [!DNL Sites]中的新功能 {#ga-features-sites}

* 發佈至預覽層級現在在Sites Admin UI中顯示為頁面狀態
* 發佈到預覽層現在會在動作結束時呈現預覽URL，並將URL保留在頁面屬性中以供稍後參考

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]中的新功能 {#what-is-new-forms}

* Forms管理員可以篩選AEM收件匣中的自訂欄。
* Forms開發人員可使用最適化表單編輯器的主題編輯器和樣式層，為驗證碼元件設定樣式。
* 已改善自動偵測來源表單中邏輯區段並將這些區段轉換為相應最適化表單面板的準確度。
* 新增移動動作，協助將PDF或XDP檔案從一個資料夾移至另一個資料夾。
* 縮短載入時間，並改善最適化表單編輯器和主題編輯器的效能。

### [!DNL Forms]的Beta功能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:通訊API可協助您結合XDP範本和XML資料，以產生各種格式的列印檔案。此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   * 使用XML資料填入範本檔案，以產生檔案。
   * 以各種格式產生輸出表單，包括非互動式PDF列印資料流。
   * 從XFA表單產生列印PDF PDF和Adobe Acrobat表單(AcroForm)。

您可以寫入[!DNL formscsbeta@adobe.com]以註冊測試版程式。

### [!DNL Forms]中修正的錯誤 {#forms-bugs-fixed}

* 在透過表單資料模型(FDM)將資料提交至後端服務之前驗證欄位時，驗證會成功，但表單資料模型服務無法叫用後期驗證。
* 當您從Apple iOS裝置提交包含標準HTML上傳欄位的表單時，有時不會傳送檔案內容，而會在另一端收到0位元組檔案。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Adobe Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

本節概述AEM Screens as aCloud Service的發行說明。

### 發行日期 {#release-date-june-screens}

AEM Screens as aCloud Service的發行日期為2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>請參閱[AEM Screens as a Cloud Service指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) ，了解成功安裝、設定和執行Screens as aCloud Service所需的基礎知識，並連結至詳細概念技術檔案。

* 批量設備註冊管理意味著提供大量播放器設備更快、更高效。

* 改善裝置、顯示和管道詳細目錄檢視的搜尋和篩選選項。

* 設備健康快照通過提供關鍵狀態如一覽而節省時間。

* 「對象詳細資訊」頁為項目中的每個對象提供了最相關資訊的摘要。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 內容片段的新CIF產品和類別參考資料類型(包括 產品/類別選擇器UI支援)
* 新商務內容片段核心元件
* AEM後端支援的全文商務搜尋
* 商務核心元件支援Adobe商務Sensei Recs資料收集
* 改善類別頁面的SEO易記URL
* 支援每個網站/設定的自訂HTTP標題

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.5.4版的發行日期為2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支援選用的[pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)步驟，以便與CTT搭配使用。 當來源AEM例項設定為使用Amazon S3或Azure Blob儲存資料存放區時，預先複製步驟可用來大幅加快內容傳輸活動的擷取和擷取階段。

* CTT新增了防護性功能，以防止使用者在擷取階段期間達到關鍵點時停止擷取，並可能損毀資料。

* 提取記錄檔的描述性更強，有助於疑難排解。

* 在UI中新增了較清楚描述的擷取狀態訊息。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 在製作例項上停止擷取時，UI會從`FINISHED`覆寫發佈例項上先前完成的擷取至`STOPPED`。 此問題已修正。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的發行日期為2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能夠檢測並報告`/content/dam`下資料夾中缺少的子節點。

* 能夠偵測並報告所使用的最佳實務分析器版本。

### 錯誤修正 {#bug-fixes-bpa-latest}

* 修正了與不支援的存放庫結構(URS)相關的記錄錯誤。


