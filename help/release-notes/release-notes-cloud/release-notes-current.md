---
title: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 40897b9194de56251da73cbea8718845882f98af
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager] as aCloud Service{#release-notes}的最新發行說明

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.5.0的發行日期為2021年5月27日。
下列版本(2021.6.0)將於2021年6月24日發行。

## 發行視頻{#release-video}

查看2021年5月[發行概述](https://video.tv.adobe.com/v/333602)影片，以取得新增功能的摘要。

## AEM as a Cloud Service基礎 {#foundation}

### AEM as a A Porting Foundation的新增功能{#what-is-new-foundation}

* [發行前管道](/help/release-notes/prerelease.md):在即將推出的功能投入生產前，預覽一整個月！

* [取代API](/help/release-notes/deprecated-apis.md):提供AEM as aCloud Service最新淘汰的API清單。

* [AEM as aCloud ServiceSDK組建Analyzer Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):將您的Maven專案更新至最新版本，其中包括已棄用的Java API檢查和其他改進。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* 您很快就能驗證新[預覽層級](/help/sites-cloud/authoring/fundamentals/previewing-content.md)上的內容，以模擬最終體驗的外觀和感覺，就像您在發佈層級上一樣。 這是由AEM Sites托管出版物精靈啟用，現在可讓您在「發佈」或「預覽」之間選擇發佈目的地。 接著，您就可以透過專用的URL存取預覽體驗。 在預覽上進行驗證之後，內容可照常從「作者」發佈至「發佈」。 在AEM as aCloud Service環境中啟用預覽服務將於未來幾週逐步推出。

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### 發行前通道{#what-is-new-assets-prerelease}中提供的新功能

* 中繼資料結構可直接套用至資料夾屬性。

   ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

* 「資產大量內嵌」工具可讓您在大量內嵌期間新增中繼資料。

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若資料夾中超過1000個資產， [!DNL Assets]會顯示1000+。

   ![介面上會顯示資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] {#assets-bugs-fixed}中修正的錯誤

* 上傳超大型檔案會導致[!DNL Experience Manager desktop app]當機。 (CQ-4320942)
* 從資料夾內選取相同集合，以及從搜尋結果選取集合時，工具列選項會不同。 (CQ-4321406)

#### [!DNL Dynamic Media] {#what-is-new-dm}中的新增功能

* 智慧型影像設備像素比(DPR)和網路頻寬優化使您能夠在具有高解析度顯示器且網路頻寬受限的設備上高效地提供最佳質量影像。 請參閱[智慧影像常見問題集](/help/assets/dynamic-media/imaging-faq.md)。

   >[!NOTE]
   >
   >上述智慧型影像處理增強功能的發行時間軸為：
   >
   >* 北美2021年5月24日於納歐州，
      >
      >
   * 歐洲、中東和非洲2021年6月25日，
      >
      >
   * 亞太2021年7月19日。


* 在[!DNL Dynamic Media]傳送（fmt URL修飾符）中引入了對下一代影像格式AVIF的支援。

   >[!NOTE]
   >
   >AVIF支援的發行時間表為：
   >
   >* 北美2021年5月10日，
      >
      >
   * 歐洲、中東和非洲2021年5月24日，
      >
      >
   * 2021年6月24日。


## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.5.0Cloud Service中Cloud Manager的發行說明。

### 發行日期 {#release-date-cm-may}

AEM as aCloud Service中的Cloud Manager 2021.5.0的發行日期為2021年5月6日。
下一版預計於2021年6月10日發行。

### 新功能 {#what-is-new-may}

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

### 新功能 {#what-is-new-ctt-latest}

* 如果用戶對Java執行檔沒有執行權限，則Quickstart的錯誤日誌中將添加新的日誌記錄語句。

* 當使用者從CTT UI中刪除移轉集時（執行解壓縮），與該移轉集相關聯的`tmp`資料夾將會刪除以節省空間。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 刪除移轉集時，CTT UI偶爾會出現無益的錯誤訊息。 此問題已修正。

* 執行使用者對應時，如果目標和主機上有相同的電子郵件地址，但使用者名稱不同，則整個擷取會失敗。 此問題已修正。 在這種衝突的情況下，會跳過用戶/組，並在日誌檔案中記錄為衝突。

### 發行日期 {#release-date-ctt-may}

內容轉移工具1.4.0版的發行日期為2021年5月11日。

### 新功能 {#what-is-new-ctt-may}

* 此版本的「內容轉移工具」會針對要移轉至Cloud Service的資產建立文字轉譯。 需要文字轉譯才能支援對擷取資產進行全文搜尋。
* 使用者可建立的「內容轉移工具」移轉集數上限已從4個增加至10個。

### 錯誤修正 {#bug-fixes-ctt-may}

* 修正與「內容轉移工具」UI中的自動重新整理功能相關的多項錯誤。
* 包含`wipe=true`的內容轉移工具導致目標上的計數器索引不正確。 此問題已修正。

## 商務附加元件{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-commerce}

* 產品屬性的「資產」索引標籤中未顯示資產縮圖

* 階層連結會重設產品主控台中的預覽資料
