---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.1.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.1.0 版發行說明。'
exl-id: 1c40ab67-8fd7-4f29-b8c9-dd98b6d5b490
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 30%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0 版發行說明 {#release-notes}

以下章節概述2022.1.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2022.1.0)為2022年2月3日。
以下版本(2022.3.0)將於2022年3月31日發行。

## 發行影片 {#release-video}

請檢視 [2022年1月版本總覽](https://video.tv.adobe.com/v/340120) 2022.1.0版新增功能摘要影片。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* 此 **[啟用前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** 按鈕可在 **網站** 使用v2頁面核心元件的網站的Sites主控台邊欄。 此按鈕會將網站設定為載入使用前端管道部署在現有使用者端資料庫之上的主題。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [!DNL Dynamic Media]  — 您現在可以使用AEM Dynamic Media介面進行設定，包括一般設定和發佈設定，而不必透過Dynamic Media Classic案頭應用程式來進行。

* [!DNL Dynamic Media] 現在支援MXF影片的擷取、預覽、播放和發佈。 尚不支援MXF影片的附註和可訂購影片。

* 在設定遠端DAM與Sites部署之間的連線後，遠端DAM上的資產便可在Sites部署中使用。 您現在可以執行 [更新、刪除、重新命名和移動作業](/help/assets/use-assets-across-connected-assets-instances.md) 位於遠端DAM資產或資料夾上。 這些更新會在Sites部署中自動提供，但會有一些延遲。

### 中的新功能 [!DNL Assets] 發行前通道 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] 現在提供下列作業的彈性： [設定一個別名帳戶](/help/assets/dynamic-media/dm-alias-account.md) ，以確保更新開箱即用的Dynamic Media URL和檢視器內嵌程式碼。 這會對SEO產生正面影響，以反映對企業內容所做的更新，例如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 使用者介面至：

   * 設定存放庫中重複資產的偵測。

   * 設定新增數位浮水印至影像。

* 管理員現在可以設定電子郵件服務以進行大量下載。 它可讓使用者 [啟用大型下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 介面。 下載程式完成後，使用者會收到電子郵件通知，其中包含封存zip資料夾的下載連結。


* 此 [管理發布](/help/assets/manage-publication.md) 功能已透過改良的使用者介面來增強。 使用者可以將內容發佈或取消發佈到所選目的地，或從所選目的地取消發佈內容， [新增內容](/help/assets/manage-publication.md#add-content) 至整個DAM存放庫的發佈清單， [包含資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 以發佈所選資料夾的內容並套用篩選器，以及 [排程發佈](/help/assets/manage-publication.md#publish-assets-later) 到更晚的日期或時間。

### 錯誤修正 {#bug-fixes}

* 將資產從AEM內部部署移轉至雲端服務時，沒有原始轉譯的未處理資產會傳送至Asset compute進行處理。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生各種格式的表單，包括非互動式PDF列印資料流。
   * 從 XFA 表單 PDF 產生列印 PDF。
   * 將多組資料與來源範本合併，以大量產生PDF、PostScript、PCL和ZPL檔案。

* **使用Communications API建立的記錄檔案和PDF檔案的自訂字型**：您現在可以在使用Communications API產生的PDF檔案中使用品牌核准的字型，以符合您的組織要求。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **[組合器API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**：組合器API用於組合、重新排列、擴充和取得有關PDF檔案的資訊。


## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 增強的myAccount元件
* 產品推薦元件支援其他頁面型別（首頁、購物車、訂單確認）
* **希望清單**
   * 登入的訪客可將產品新增至願望清單
   * 您可以透過myAccount管理願望清單及其產品
   * 可以透過原則（例如產品Teaser、產品詳細資訊）在元件層級上啟用/停用「新增到願望清單」按鈕
   * 可作為核心元件提供給AEM Venia Storefront

![希望清單](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEMas a Cloud Service2022.01.0中的Cloud Manager發行日期是2022年1月20日。 下一版計劃於 2022 年 2 月 10 日發行。

### 新增功能 {#what-is-new-cm}

* Cloud Manager [在偵測到多個全堆疊管道執行中使用了相同的 Git 認可時，將避免重建計劃碼基底](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* 現在存取 AEM 環境記錄檔需要 **Deployment Manager** 產品設定檔。沒有此設定檔的使用者將在使用者介面中看到停用按鈕。
* UI 不允許針對未啟用 Sites 解決方案的計畫設定前端管道。
* 在產生Git密碼時，會顯示到期日。

### 錯誤修正 {#bug-fixes-cm}

* 已修正部署部分前端管道時發生的空指針異常。
* 現在可以在環境執行過時版本的 AEM 時新增、更新和刪除環境變數。
* 對於在某些極少數情況下使用計畫步驟的管道，建置影像步驟將不再標記為錯誤。
* 對於僅有一個存放庫的計畫，管道執行畫面現在將顯示存放庫名稱。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.8.6的發行日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 使用者能夠可靠地判斷「內容轉移工具」擷取的所有內容是否已成功內嵌至目標例項。 若要使用此功能，您需要在 `System Console` 來源AEM環境的。 請參閱 [驗證內容轉移 — 快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以取得更多詳細資料。

### 錯誤修正 {#bug-fixes-ctt}

* 部分使用者未對應，因為使用者對應區分大小寫。 此問題已修正。 使用者對應不再區分大小寫。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的發行日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測及報告使用和不使用智慧標籤的資產數量。
* 能夠偵測並報告所使用的核心元件版本。
* 能夠偵測並報告BPA執行所在的來源層級型別（製作或發佈）。

### 錯誤修正 {#bug-fixes-bpa}

* BPA大小調整邏輯變得更快速、更有效率。
* 在某些情況下，BPA在執行時不會增加分析的計數。 此問題已修正。
