---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0 版發行說明。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 43%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.5.0為2021年5月27日。
下列版本(2021.6.0)將於2021年6月28日發行。

## AEMas a Cloud Service基礎 {#foundation}

### AEMas a Cloud Service基礎的新增功能 {#what-is-new-foundation}

* [發行前通道](/help/release-notes/prerelease.md)：在即將上線的功能投入生產之前，先預覽整整一個月！

* [API淘汰](/help/release-notes/deprecated-removed-features.md)：提供適用於AEMas a Cloud Service的最新已棄用API清單。

* [AEMas a Cloud ServiceSDK建置分析器Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)：將您的Maven專案更新至最新版本，其中包括已淘汰的Java API檢查和其他改善。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 您很快就會能夠驗證新版本的內容 [預覽層](/help/sites-cloud/authoring/sites-console/previewing-content.md) 以模擬最終的體驗外觀，如同您在發佈層級上一樣。 這可透過AEM Sites Managed Publication精靈啟用，現在可讓您在發佈或預覽之間選擇發佈目的地。 接著，您就可以透過專用URL存取「預覽」上的體驗。 在「預覽」上進行驗證後，內容可以如常從「作者」發佈至「發佈」。 在AEMas a Cloud Service環境中啟用預覽服務將在未來幾週逐步推出。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 您可以使用「連結共用」功能下載共用的資產。 此下載專案現在使用非同步服務，提供更快速且無中斷的下載專案，即使是大型下載專案亦然。 另請參閱 [下載資產](/help/assets/download-assets-from-aem.md#link-share-download).

  ![下載收件匣](/help/assets/assets/download-inbox.png)

### 發行前管道中可用的新功能 {#what-is-new-assets-prerelease}

* 中繼資料結構描述可直接套用至資料夾屬性。

  ![從資料夾屬性新增中繼資料結構](/help/assets/assets/metadata-schema-folder-properties.png)

* 資產大量擷取工具可讓您在大量擷取期間新增中繼資料。

* 使用者體驗增強功能會顯示存在於資料夾中的資產數量。 若資料夾中有超過1000個資產， [!DNL Assets] 顯示1000+。

  ![介面上會顯示資料夾中的資產數量](/help/assets/assets/browse-folder-number-of-assets.png)

### 修正在 [!DNL Assets] 中的錯誤 {#assets-bugs-fixed}

* 上傳超大型檔案會當機 [!DNL Experience Manager desktop app]. (CQ-4320942)
* 當從資料夾中選取相同的集合，以及從搜尋結果中選取集合時，工具列選項會不同。 (CQ-4321406)

#### Dynamic Media的新增功能 {#what-is-new-dm}

* 智慧型影像DPR （裝置畫素比）和網路頻寬最佳化可讓您在具有高解析度顯示器且網路頻寬受限的裝置上，有效率地提供最佳品質影像。 如需詳細資訊，請參閱 [智慧型影像常見問題集](/help/assets/dynamic-media/imaging-faq.md) 和 [使用新一代影像格式WebP和AVIF進行影像最佳化。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* 在Dynamic Media傳送中推出對新一代影像格式AVIF的支援（fmt URL修飾元）。

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **關聯式說明**：新增最適化表單編輯器、範本編輯器和主題編輯器的關聯式說明，以協助作者更能了解編輯器的各種功能。
* **屬性瀏覽器中的錯誤訊息**：新增最適化表單屬性瀏覽器中每種屬性的錯誤訊息。這些訊息有助於了解欄位允許的值。

### [!DNL Forms] 即將推出的 Beta 版功能 {#what-is-new-forms-prerelease}

Output as a Cloud service：Output 服務可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和非同步的批次模式產生文件。 Output 服務可讓您建立以下用途的應用程式：

* 使用 XML 資料填寫範本檔案來產生最終表單文件。
* 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
* 從 XFA 表單 PDF 產生列印 PDF。

您可以寫信寄到 formscsbeta@adobe.com 來註冊 beta 版計劃。

### 修正在[!DNL Forms]中的錯誤 {#forms-bugs-fixed}

* 在 AEM Forms 工作流程的指派任務步驟中，當您以珊瑚圖示取代將動作按鈕的預設圖示時，工作流程會停止運作並記錄例外狀況。使用預設圖示時工作流程則會如預期執行。
* 在版面圖層，當您變更欄數、開啟編輯圖層，以及在面板中拖曳某些元件時，藍色正方形方塊會開始在最適化表單編輯器的內容區域中出現，且編輯器開始沒有回應。
* 與提供最適化或外部資產的 URL 關聯的規則編輯器的錯誤訊息過長或不人性化。


## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.5.0中Cloud Manager的發行說明

### 發行日期 {#release-date-cm-may}

AEMas a Cloud Service2021.5.0中Cloud Manager的發行日期為2021年5月06日。
下一個版本計畫於2021年6月3日發行。

### 新增功能 {#what-is-new-may}

* PackageOverlaps 品質規則現在會偵測多次部署了相同套件的情況，也就是在同一個部署的套件組中的多個嵌入式位置。

* 公用 API 中的存放庫端點現在包含 Git URL。

* Cloud Manager使用者下載的部署記錄有更深刻的見解，並包含有關失敗和成功情境的細節。

* 將程式碼推送到 Adobe Git 時所發生的間歇性失敗狀況現在已經解決了。

* Commerce 附加元件現在可以在編輯計畫工作流程中套用到沙箱計畫。

* 編輯計畫體驗已更新。

* 「環境詳細資訊」頁面中的「網域名稱」表格可透過分頁顯示多達 250 個網域名稱。

* 「新增計畫」和「編輯計畫」工作流程中的「解決方案」索引標籤會顯示解決方案，即便該計畫只有一個解決方案可用。

* 當建置未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes-cm-may}

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 管道變數 API 不會移除「已刪除」的變數，而是只會用狀態將其標記為&#x200B;**已刪除**。

* 部分程式碼異味類型的品質問題錯誤地影響了可靠性評等。

* 由於不支援萬用字元網域，UI 將不允許使用者提交萬用字元網域。

* 在 UTC 午夜和凌晨 1 點之間開始執行管道時，不能保證 Cloud Manager 產生的成品版本大於前一天建立的版本。

* 在沙箱計畫設定過程中，成功建立包含範例程式碼的專案後，管理 Git 將顯示為概觀頁面中英雄卡的連結。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具v1.4.6的發行日期為2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果使用者沒有Java可執行檔的執行許可權，則會將新的記錄陳述式新增至快速入門的錯誤記錄檔。

* 當使用者從CTT使用者介面（已執行擷取）刪除移轉集時， `tmp` 會刪除與該移轉集相關聯的資料夾以節省空間。

### 錯誤修正 {#bug-fixes-ctt-latest}

* 刪除移轉集時，CTT UI中偶爾會顯示一則無用的錯誤訊息。 此問題已修正。

* 執行使用者對應時，如果使用者在目標與主機上擁有相同的電子郵件地址，但使用者名稱不同，則整個內嵌都會失敗。 此問題已修正。 在此衝突情況下，使用者/群組會被略過，並記錄為記錄檔案中的衝突。

### 發行日期 {#release-date-ctt}

內容轉移工具v1.4.0的發行日期為2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的「內容轉移工具」會針對正移轉至Cloud Service的資產建立文字轉譯。 需要文字轉譯才能支援對所擷取的資產進行全文搜尋。
* 使用者可建立的內容轉移工具移轉集數量上限已從4個增加到10個。

### 錯誤修正 {#bug-fixes-ctt-may}

* 和內容轉移工具UI中的自動重新整理功能相關的多項錯誤修正。
* 內容轉移工具，搭配 `wipe=true` 導致目標上的計數器索引不正確。 此問題已修正。

## Commerce附加元件 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品主控台屬性中的相關內容支援分頁

### 錯誤修正 {#bug-fixes-commerce}

* 資產縮圖未顯示在產品屬性的「資產」標籤中

* 階層連結在產品主控台中重設預覽資料
