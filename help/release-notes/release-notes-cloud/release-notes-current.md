---
title: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 344a42f31444d30e9304b3a2198b1a4df17aa9c0
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作為Cloud Service的最新發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.5.0的發行日期為2021年5月27日。
下列版本(2021.6.0)將於2021年6月24日發行。

## 發行影片 {#release-video}

查看2021年5月[發行概述](https://video.tv.adobe.com/v/333602)影片，以取得新增功能的摘要。

## AEM as a Cloud Service基礎 {#foundation}

### AEM as a A A Experience Foundation的新功能 {#what-is-new-foundation}

* [發行前管道](/help/release-notes/prerelease.md):在即將推出的功能投入生產前，預覽一整個月！

* [取代API](/help/release-notes/deprecated-apis.md):提供AEM as aCloud Service最新淘汰的API清單。

* [AEM as aCloud ServiceSDK組建Analyzer Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):將您的Maven專案更新至最新版本，其中包括已棄用的Java API檢查和其他改進。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]中的新增功能 {#what-is-new-sites}

* 您很快就能驗證新[預覽層級](/help/sites-cloud/authoring/fundamentals/previewing-content.md)上的內容，以模擬最終體驗的外觀和感覺，就像您在發佈層級上一樣。 這是由AEM Sites托管出版物精靈啟用，現在可讓您在「發佈」或「預覽」之間選擇發佈目的地。 接著，您就可以透過專用的URL存取預覽體驗。 在預覽上進行驗證之後，內容可照常從「作者」發佈至「發佈」。 在AEM as aCloud Service環境中啟用預覽服務將於未來幾週逐步推出。

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### 發行前管道提供的新功能 {#what-is-new-assets-prerelease}

* 中繼資料結構可直接套用至資料夾屬性。

   ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

* 「資產大量內嵌」工具可讓您在大量內嵌期間新增中繼資料。

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若資料夾中超過1000個資產， [!DNL Assets]會顯示1000+。

   ![介面上會顯示資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets]中修正的錯誤 {#assets-bugs-fixed}

* 上傳超大型檔案會導致[!DNL Experience Manager desktop app]當機。 (CQ-4320942)
* 從資料夾內選取相同集合，以及從搜尋結果選取集合時，工具列選項會不同。 (CQ-4321406)

#### [!DNL Dynamic Media]中的新增功能 {#what-is-new-dm}

* 智慧型影像設備像素比(DPR)和網路頻寬優化使您能夠在具有高解析度顯示器且網路頻寬受限的設備上高效地提供最佳質量影像。 請參閱[智慧影像常見問題集](/help/assets/dynamic-media/imaging-faq.md)。

* 在[!DNL Dynamic Media]傳送（`fmt` URL修飾元）中，引入對新一代影像格式AVIF的支援。 有關更多詳細資訊和時間軸，請參閱[影像提供和呈現API fmt](https://experienceleague.corp.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)。

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]中的新增功能 {#what-is-new-forms}

* **內容說明**:新增適用性表單編輯器、範本編輯器和主題編輯器的內容說明，協助作者更清楚了解編輯器的各種功能。
* **屬性瀏覽器中的錯誤訊息**:已針對適用性Forms屬性瀏覽器中的每個屬性新增錯誤訊息。這些訊息有助於了解欄位的允許值。

### [!DNL Forms]即將推出的測試版功能 {#what-is-new-forms-prerelease}

輸出雲端服務：輸出服務可協助您結合XDP範本和XML資料，以產生各種格式的列印檔案。 此服務可讓您以同步和非同步批次模式產生檔案。 通過輸出服務，您可以建立應用程式，以便您：

* 使用XML資料填入範本檔案，以產生最終表單檔案。
* 以各種格式產生輸出表單，包括非互動式PDF列印資料流。
* 從XFA表單PDF產生列印PDF。

您可以寫信到formscsbeta@adobe.com註冊測試版計畫。

### [!DNL Forms]中修正的錯誤 {#forms-bugs-fixed}

* 在AEM Forms工作流程的「指派任務」步驟中，當您以珊瑚圖示取代動作按鈕的預設圖示時，工作流程會停止運作並記錄例外狀況。 使用預設圖示時，工作流程會如預期般執行。
* 在版面層中，當您變更欄數時，請開啟編輯層，並拖曳面板中的某些元件，適用性表單編輯器的內容區域會開始出現方形藍色方塊，而編輯器會停止回應。
* 與提供適用性或外部資產的URL相關的規則編輯器選項的錯誤訊息太長，且不方便使用。

## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.6.0和2021.5.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date-june-cm}

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


### 發行日期 {#release-date-cm-may}

AEM as aCloud Service中的Cloud Manager 2021.5.0的發行日期為2021年5月6日。

### 新增功能 {#what-is-new-may}

* PackageOverlaps質量規則現在會檢測在同一部署的包集中多次部署相同包的情況，即在多個嵌入位置中。

* 公用API中的存放庫端點現在包含Git URL。

* Cloud Manager使用者下載的部署記錄將更有洞察力，現在會包含有關失敗和成功案例的詳細資訊。

* 現在已解決將程式碼推送至AdobeGit時發生的間歇性故障。

* 現在，在編輯方案工作流程期間，商務附加元件可套用至沙箱方案。

* 已重新整理「編輯程式」體驗。

* 「環境詳細資料」頁面中的「網域名稱」表格會透過分頁顯示最多250個網域名稱。

* 即使方案只有一個可用解決方案，新增方案和編輯方案工作流程中的解決方案標籤仍會顯示解決方案。

* 當組建未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes-cm-may}

* 有時，即使未部署該設定，使用者仍可能在IP允許清單旁看到綠色的「作用中」狀態。

* 管道變數API不會移除「已刪除」變數，而只會以狀態&#x200B;**DELETED**&#x200B;來標籤它們。

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性等級。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當午夜至凌晨1:00之間開始執行管道時，Cloud Manager產生的工件版本不一定會大於前一天建立的版本。

* 在沙箱方案設定期間，成功建立包含范常式式碼的專案後，「管理Git」會顯示為「概述」頁面中主圖卡的連結。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.4.6版的發行日期為2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果用戶對Java執行檔沒有執行權限，則Quickstart的錯誤日誌中將添加新的日誌記錄語句。

* 當使用者從CTT UI中刪除移轉集時（執行解壓縮），與該移轉集相關聯的`tmp`資料夾將會刪除以節省空間。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 刪除移轉集時，CTT UI偶爾會出現無益的錯誤訊息。 此問題已修正。

* 執行使用者對應時，如果目標和主機上有相同的電子郵件地址，但使用者名稱不同，則整個擷取會失敗。 此問題已修正。 在這種衝突的情況下，會跳過用戶/組，並在日誌檔案中記錄為衝突。

### 發行日期 {#release-date-ctt-may}

內容轉移工具1.4.0版的發行日期為2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的「內容轉移工具」會針對要移轉至Cloud Service的資產建立文字轉譯。 需要文字轉譯才能支援對擷取資產進行全文搜尋。
* 使用者可建立的「內容轉移工具」移轉集數上限已從4個增加至10個。

### 錯誤修正 {#bug-fixes-ctt-may}

* 修正與「內容轉移工具」UI中的自動重新整理功能相關的多項錯誤。
* 包含`wipe=true`的內容轉移工具導致目標上的計數器索引不正確。 此問題已修正。

## 商務附加元件 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-commerce}

* 產品屬性的「資產」索引標籤中未顯示資產縮圖

* 階層連結會重設產品主控台中的預覽資料
