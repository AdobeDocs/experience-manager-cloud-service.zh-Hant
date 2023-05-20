---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.5.0是2021年5月27日。
以下版本(2021.6.0)將於2021年6月28日發佈。

## AEMas a Cloud Service {#foundation}

### as a Cloud Service基金會的AEM新增功能 {#what-is-new-foundation}

* [預發行渠道](/help/release-notes/prerelease.md):在即將推出的功能投入生產前，預覽一個月！

* [API棄用](/help/release-notes/deprecated-apis.md):有一個最新的不建議使用的AEMas a Cloud ServiceAPI清單。

* [AEMas a Cloud ServiceSDK生成Analyzer Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):將您的主項目更新為最新版本，其中包括已過時的Java API檢查和其他改進。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 您很快將能夠驗證新內容 [預覽層](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 模擬最終體驗的外觀和感覺，就像您在「發佈」層時一樣。 這由「AEM Sites托管發佈」嚮導啟用，該嚮導現在允許您在「發佈」或「預覽」之間選擇發佈目標。 然後，可以通過專用URL訪問「預覽」體驗。 在「預覽」上驗證後，內容可以像往常一樣從「作者」發佈到「發佈」。 在as a Cloud Service環境AEM中啟用預覽服務將在未來幾週內逐步推出。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 可以使用連結共用功能下載共用的資產。 現在，此下載使用非同步服務，即使下載量非常大，也可提供更快、不間斷的下載。 請參閱 [下載資產](/help/assets/download-assets-from-aem.md#link-share-download)。

   ![下載收件箱](/help/assets/assets/download-inbox.png)

### 預發行渠道中提供的新功能 {#what-is-new-assets-prerelease}

* 元資料架構可以直接應用於資料夾屬性。

   ![從資料夾屬性添加元資料架構](/help/assets/assets/metadata-schema-folder-properties.png)

* 資產批量接收工具允許您在批量接收期間添加元資料。

* 用戶體驗增強顯示資料夾中的資產數量。 對於資料夾中的1000多個資產， [!DNL Assets] 顯示1000+。

   ![資料夾中的資產數顯示在介面上](/help/assets/assets/browse-folder-number-of-assets.png)

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

* 上載非常大的檔案會崩潰 [!DNL Experience Manager desktop app]。 (CQ-4320942)
* 當從資料夾中選擇同一個集合時以及從搜索結果中選擇該集合時，工具欄選項會有所不同。 (CQ-4321406)

#### Dynamic Media有什麼新聞嗎 {#what-is-new-dm}

* 智慧成像DPR（設備像素率）和網路頻寬優化使您能夠在具有高解析度顯示和有限網路頻寬的設備上高效地提供最佳質量的影像。 有關詳細資訊，請參見 [智慧映像常見問題](/help/assets/dynamic-media/imaging-faq.md) 和 [採用WebP和AVIF格式的下一代影像優化。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* 介紹了對Dynamic Media傳送（fmt URL修飾符）下一代影像格式AVIF的支援。

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

本節概述了as a Cloud Service2021.5.0中Cloud Manager的發行說明AEM。

### 發行日期 {#release-date-cm-may}

AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 發行日期是 2021 年 5 月 06 日。下一版本計劃於 2021 年 6 月 03 日發行。

### 新增功能 {#what-is-new-may}

* PackageOverlaps 品質規則現在會偵測多次部署了相同套件的情況；也就是在同一個部署的套件組中的多個嵌入式位置。

* 公用 API 中的存放庫端點現在包含 Git URL。

* Cloud Manager 使用者下載的部署記錄有更深刻的見解，而且現在包含有關失敗和成功情境的細節。

* 將計劃碼推送到 Adobe Git 時所發生的間歇性失敗狀況現在已經解決了。

* Commerce 附加元件現在可以在編輯計劃工作流程中套用到沙箱計劃。

* 編輯計劃體驗已更新。

* 「環境詳細資訊」頁面中的「網域名稱」表格可透過分頁顯示多達 250 個網域名稱。

* 即使只有一個解決方案可用於「程式」，「添加程式」和「編輯程式」工作流中的「解決方案」頁籤也會顯示該解決方案。

* 當建置未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes-cm-may}

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 管道變數 API 不會移除「已刪除」的變數，而是只會用狀態將其標記為&#x200B;**已刪除**。

* 部分計劃碼異味類型的品質問題錯誤地影響了可靠性評等。

* 由於不支援萬用字元網域，UI 將不允許使用者提交萬用字元網域。

* 在 UTC 午夜和凌晨 1 點之間開始執行管道時，不能保證 Cloud Manager 產生的成品版本大於前一天建立的版本。

* 在沙箱計畫設定過程中，成功建立包含範例計劃碼的專案後，管理 Git 將顯示為總覽頁面中英雄卡的連結。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容傳輸工具v1.4.6的發佈日期為2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果用戶對Java執行檔沒有執行權限，則新日誌記錄語句已添加到快速啟動的錯誤日誌中。

* 當用戶從執行抽取的CTT UI中刪除遷移集時， `tmp` 將刪除與該遷移集關聯的資料夾以節省空間。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 刪除遷移集時，偶爾會在CTT UI中出現無益的錯誤消息。 這個已經修復了。

* 運行用戶映射時，如果用戶在目標和主機上具有相同的電子郵件地址，但用戶名不同，則整個接收將失敗。 這個已經修復了。 在這種衝突的情形中，將跳過用戶/組，並將其記錄為日誌檔案中的衝突。

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.4.0的發佈日期為2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的內容傳輸工具為要遷移到Cloud Service的資產建立文本格式副本。 需要文本格式副本來支援對所接收資產的全文搜索。
* 用戶可以建立的「內容傳輸工具」遷移集的最大數量已從4個增加到10個。

### 錯誤修正 {#bug-fixes-ctt-may}

* 與內容傳輸工具UI中的自動刷新功能相關的多個錯誤修復程式。
* 內容傳輸工具 `wipe=true` 導致目標上的計數器索引不正確。 這個已經修復了。

## 商業附加模組 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品控制台屬性中關聯內容的分頁支援

### 錯誤修正 {#bug-fixes-commerce}

* 未在產品屬性的「資產」頁籤中顯示資產縮略圖

* Breadcrumb重置產品控制台中的預覽資料
