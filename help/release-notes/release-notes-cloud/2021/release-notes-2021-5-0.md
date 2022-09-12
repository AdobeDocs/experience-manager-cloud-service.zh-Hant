---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 23%

---

# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.5.0為2021年5月27日。
下列版本(2021.6.0)將於2021年6月28日發行。

## AEMas a Cloud Service基礎 {#foundation}

### AEM Foundation的新增功能 {#what-is-new-foundation}

* [發行前管道](/help/release-notes/prerelease.md):在即將推出的功能投入生產前，預覽一整個月！

* [取代API](/help/release-notes/deprecated-apis.md):提供AEMas a Cloud Service最新淘汰的API清單。

* [AEMas a Cloud ServiceSDK建置Analyzer Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):將您的Maven專案更新至最新版本，其中包括已棄用的Java API檢查和其他改進。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 您很快就能驗證新 [預覽層](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 來模擬最終體驗的外觀和感覺，就像您在發佈層級上一樣。 這是由AEM Sites托管出版物精靈啟用，現在可讓您在「發佈」或「預覽」之間選擇發佈目的地。 接著，您就可以透過專用的URL存取預覽體驗。 在預覽上進行驗證之後，內容可照常從「作者」發佈至「發佈」。 在AEMas a Cloud Service環境中啟用預覽服務將於未來幾週逐步推出。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 您可以下載使用「連結共用」功能共用的資產。 此下載現在使用非同步服務，即使下載量非常大，也能提供更快速且不間斷的下載。 請參閱 [下載資產](/help/assets/download-assets-from-aem.md#link-share-download).

   ![下載收件匣](/help/assets/assets/download-inbox.png)

### 發行前管道提供的新功能 {#what-is-new-assets-prerelease}

* 中繼資料結構可直接套用至資料夾屬性。

   ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

* 「資產大量內嵌」工具可讓您在大量內嵌期間新增中繼資料。

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若是資料夾中超過1000個資產， [!DNL Assets] 顯示1000+。

   ![介面上會顯示資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

* 上傳超大型檔案會導致 [!DNL Experience Manager desktop app]. (CQ-4320942)
* 從資料夾內選取相同集合，以及從搜尋結果選取集合時，工具列選項會不同。 (CQ-4321406)

#### Dynamic Media的新增功能 {#what-is-new-dm}

* 智慧影像處理DPR（設備像素比率）和網路頻寬優化使您能夠在具有高解析度顯示器且網路頻寬受限的設備上高效地提供最佳質量影像。 如需詳細資訊，請參閱 [智慧型影像處理常見問題集](/help/assets/dynamic-media/imaging-faq.md) 和 [使用新一代影像格式WebP和AVIF進行影像優化。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* 推出在Dynamic Media傳送（fmt URL修飾元）中支援新一代影像格式AVIF。

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **關聯式說明**：新增最適化表單編輯器、範本編輯器和主題編輯器的關聯式說明，以協助作者更能了解編輯器的各種功能。
* **屬性瀏覽器中的錯誤訊息**：新增最適化表單屬性瀏覽器中每種屬性的錯誤訊息。這些訊息有助於了解欄位允許的值。

### [!DNL Forms]即將推出的 Beta 版功能 {#what-is-new-forms-prerelease}

Output as a Cloud service：Output 服務可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和非同步批次模式產生文件。 Output 服務可讓您建立以下用途的應用程式：

* 使用 XML 資料填寫範本檔案來產生最終表單文件。
* 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
* 從 XFA 表單 PDF 產生列印 PDF。

您可以寫信寄到 formscsbeta@adobe.com 來註冊 beta 版計劃。

### 修正在[!DNL Forms]中的錯誤 {#forms-bugs-fixed}

* 在 AEM Forms 工作流程的指派任務步驟中，當您以珊瑚圖示取代將動作按鈕的預設圖示時，工作流程會停止運作並記錄例外狀況。使用預設圖示時工作流程則會如預期執行。
* 在版面圖層，當您變更欄數、開啟編輯圖層，以及在面板中拖曳某些元件時，藍色正方形方塊會開始在最適化表單編輯器的內容區域中出現，且編輯器開始沒有回應。
* 與提供最適化或外部資產的 URL 關聯的規則編輯器的錯誤訊息過長或不人性化。


## Cloud Manager {#cloud-manager}

本節概述AEM 2021.5.0中Cloud Manageras a Cloud Service的發行說明。

### 發行日期 {#release-date-cm-may}

AEM 2021.5.0中的Cloud Manageras a Cloud Service日期為2021年5月6日。
下一版預計於2021年6月3日發行。

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

* 管道變數API不會移除「已刪除」的變數，而只會將其標示為狀態 **已刪除**.

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性等級。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當午夜至凌晨1:00之間開始執行管道時，Cloud Manager產生的工件版本不一定會大於前一天建立的版本。

* 在沙箱方案設定期間，成功建立包含范常式式碼的專案後，「管理Git」會顯示為「概述」頁面中主圖卡的連結。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.4.6版的發行日期為2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果用戶對Java執行檔沒有執行權限，則Quickstart的錯誤日誌中將添加新的日誌記錄語句。

* 當使用者從執行提取的CTT UI中刪除移轉集時， `tmp` 將刪除與該遷移集關聯的資料夾以節省空間。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 刪除移轉集時，CTT UI偶爾會出現無益的錯誤訊息。 此問題已修正。

* 執行使用者對應時，如果目標和主機上有相同的電子郵件地址，但使用者名稱不同，則整個擷取會失敗。 此問題已修正。 在這種衝突的情況下，會跳過用戶/組，並在日誌檔案中記錄為衝突。

### 發行日期 {#release-date-ctt}

內容轉移工具1.4.0版的發行日期為2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的「內容轉移工具」會針對要移轉至Cloud Service的資產建立文字轉譯。 需要文字轉譯才能支援對擷取資產進行全文搜尋。
* 使用者可建立的「內容轉移工具」移轉集數上限已從4個增加至10個。

### 錯誤修正 {#bug-fixes-ctt-may}

* 修正與「內容轉移工具」UI中的自動重新整理功能相關的多項錯誤。
* 內容轉移工具，搭配 `wipe=true` 導致目標上的計數器索引不正確。 此問題已修正。

## 商務附加元件 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-commerce}

* 產品屬性的「資產」索引標籤中未顯示資產縮圖

* 階層連結會重設產品主控台中的預覽資料
