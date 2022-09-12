---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.1.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.1.0 版發行說明。'
exl-id: 1c40ab67-8fd7-4f29-b8c9-dd98b6d5b490
source-git-commit: b591b0fd24267ae0036b26f137927d5588a28316
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 11%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.1.0)為2022年2月3日。
下列版本(2022.3.0)將於2022年3月31日發行。

## 發行影片 {#release-video}

查看 [2022年1月發行概述](https://video.tv.adobe.com/v/340120) 影片，以取得2022.1.0版中新增功能的摘要。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* 此 **[啟用前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** 按鈕 **網站** 使用頁面核心元件v2之網站的Sites主控台邊欄。 此按鈕可配置站點以載入與現有客戶端庫頂端前端管道一起部署的主題。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media]  — 您現在可以使用AEM Dynamic Media介面來設定「一般設定」和「發佈設定」，而不需要透過Dynamic Media Classic案頭應用程式。

* [!DNL Dynamic Media] 現在支援MXF影片的擷取、預覽、播放和發佈。 尚不支援MXF視訊的註解和可購買視訊。

* 在遠端DAM和Sites部署之間設定連線後，即可在Sites部署中使用遠端DAM上的資產。 您現在可以執行 [更新、刪除、更名和移動操作](/help/assets/use-assets-across-connected-assets-instances.md) 在遠端DAM資產或資料夾上。 Sites部署會自動提供延遲的更新。

### 中的新功能 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] 現在可靈活地 [配置一個別名帳戶](/help/assets/dynamic-media/dm-alias-account.md) ，進而確保更新現成可用的Dynamic Media URL和檢視器內嵌程式碼。 這對SEO有正面影響，可反映對您的業務內容所做的更新，例如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 用戶介面：

   * 設定在存放庫中偵測重複資產的方式。

   * 配置向影像中添加數字水印。

* 管理員現在可以設定電子郵件服務以進行大量下載。 可讓使用者 [啟用大量下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 介面。 使用者在下載程式完成時，會收到包含已封存Zip資料夾的下載連結的電子郵件通知。


* 此 [管理出版物](/help/assets/manage-publication.md) 透過改善的使用者介面來增強功能。 使用者可以從選取的目的地，發佈或取消發佈內容， [新增內容](/help/assets/manage-publication.md#add-content) 從DAM存放庫的發佈清單， [包含資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 發佈所選資料夾的內容並應用篩選器，以及 [排程發佈](/help/assets/manage-publication.md#publish-assets-later) 到以後的日期或時間。

### 錯誤修正 {#bug-fixes}

* 將資產從AEM內部部署移轉至雲端服務時，沒有原始轉譯的未處理資產會傳送至Asset compute以進行處理。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案來產生文件。
   * 以各種格式產生表單，包括非互動式PDF列印資料流。
   * 從 XFA 表單 PDF 產生列印 PDF。
   * 將多組資料與源模板合併，以批量生成PDF、PostScript、PCL和ZPL文檔。

* **記錄檔的自訂字型和使用通訊API建立的PDF檔案**:您現在可以在使用通訊API產生的PDF檔案中使用品牌核准字型，以符合您的組織需求。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **[組合器API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**:組合器API，用於組合、重新排列、擴展和獲取有關PDF文檔的資訊。


## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 增強的myAccount元件
* 產品建議元件支援其他頁面類型（首頁、購物車、訂單確認）
* **希望清單**
   * 登入的訪客可將產品新增至願望清單
   * 可通過myAccount管理願望清單及其產品
   * 可以通過策略（例如產品預告、產品詳細資訊）在元件級別上啟用/禁用「添加到願望清單」按鈕
   * 以核心元件形式提供，並可在AEM Venia Storefront中使用

![希望清單](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEMas a Cloud Service的Cloud Manager 2022.01.0的發行日期為2022年1月20日。 下一版預計於2022年2月10日發行。

### 新增功能 {#what-is-new-cm}

* Cloud Manager將 [偵測到使用相同的git提交時，請避免重建程式碼基底](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 在多個完整堆棧管道執行中。
* 現在存取AEM環境記錄時，需要 **部署管理員** 產品設定檔。 沒有此設定檔的使用者會在使用者介面中看到「已停用」按鈕。
* 若程式未啟用Sites作為解決方案，UI將不允許進行前端管道設定。
* 產生Git密碼時，會顯示到期日。

### 錯誤修正 {#bug-fixes-cm}

* 某些前端管道部署遇到的Null指標例外狀況已修正。
* 現在當環境執行過時的AEM版本時，可以新增、更新及刪除環境變數。
* 在某些罕見情況下，使用排程步驟的管道將不再將建置影像步驟標示為「錯誤」。
* 對於只有一個存放庫的程式，管道執行畫面現在會顯示存放庫名稱。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具1.8.6版的發行日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 使用者能可靠判斷內容轉移工具擷取的所有內容是否皆成功內嵌至目標例項。 若要使用此功能，您必須在 `System Console` 來源AEM環境。 請參閱 [驗證內容傳輸 — 快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes-ctt}

* 有些使用者未對應，因為「使用者對應」須區分大小寫。 此問題已修正。 使用者對應不再區分大小寫。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的發行日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測有智慧標籤和沒有智慧標籤的資產數量並製作報表。
* 偵測並報告所使用核心元件的版本。
* 能夠偵測並報告執行BPA的來源層級（製作或發佈）類型。

### 錯誤修正 {#bug-fixes-bpa}

* BPA調整邏輯的製作速度更快、效率更高。
* 在某些情況下，BPA在執行時沒有增加分析計數。 此問題已修正。
