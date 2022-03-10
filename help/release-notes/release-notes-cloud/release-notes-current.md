---
title: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e4d7d3d7fb4430c2027d4d2f3c34d77890c28ad8
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 10%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 當前版本(2022.1.0)為2022年2月3日。
以下版本(2022.3.0)為2022年3月31日。

## 發佈視頻 {#release-video}

看看 [2022年1月發佈概述](https://video.tv.adobe.com/v/340120) 視頻，瞭解2022.1.0版中添加的功能摘要。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* 的 **[啟用前端管線](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** 按鈕 **站點** 對使用頁核心元件v2的站點的站點控制台進行連結。 此按鈕將站點配置為載入與現有客戶端庫上的前端管道一起部署的主題。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media]  — 現在，您可以使AEM用Dynamic Media介面配置常規設定和發佈設定，而不必通過Dynamic Media Classic案頭應用程式。

* [!DNL Dynamic Media] 現在支援MXF視頻的接收、預覽、播放和發佈。 尚不支援MXF視頻的注釋和可購物視頻。

* 在配置遠程DAM和站點部署之間的連接後，遠程DAM上的資產可在站點部署中使用。 您現在可以執行 [更新、刪除、更名和移動操作](/help/assets/use-assets-across-connected-assets-instances.md) 資料夾。 這些更新在站點部署中自動可用，但有一些延遲。

### 中的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] 現在提供了靈活性 [配置一個別名帳戶](../../assets/dynamic-media/dm-alias-account.md) 在用戶介面中，從而確保更新出廠設定的Dynamic MediaURL和Viewer Embed代碼。 這對SEO產生了積極影響，以反映對您的業務環境所做的更新，如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 用戶介面：

   * 配置儲存庫中重複資產的檢測。

   * 配置向影像添加數字水印。

* 管理員現在可以配置電子郵件服務以進行大下載。 它允許用戶 [啟用大量下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 。 用戶在完成下載過程後接收包含存檔的zip資料夾的下載連結的電子郵件通知。


* 的 [管理發布](/help/assets/manage-publication.md) 利用改進的用戶介面增強特徵。 用戶可以將內容發佈或取消發佈到選定目標， [添加內容](/help/assets/manage-publication.md#add-content) 從DAM儲存庫到發佈清單， [包括資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 發佈所選資料夾的內容並應用篩選器， [計畫發佈](/help/assets/manage-publication.md#publish-assets-later) 到更晚的日期或時間。

### 錯誤修正 {#bug-fixes}

* 將沒有原始格式副本的未處理資產發送到Asset compute進行處理，同時將資產從本AEM地遷移到雲服務。

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 使用 XML 資料填寫範本檔案來產生文件。
   * 以各種格式生成表單，包括非互動式PDF打印流。
   * 從 XFA 表單 PDF 產生列印 PDF。
   * 通過將多組資料與源模板合併，批量生成PDF、PostScript、PCL和ZPL文檔。

* **記錄文檔的自定義字型和使用Communications API建立的PDF文檔**:現在，您可以在使用Communications API生成的PDF文檔中使用品牌批准的字型，以符合您的組織要求。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **[匯編程式API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**:匯編器API，用於組合、重新排列、增大和獲取有關PDF文檔的資訊。


## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 增強的myAccount元件
* 產品建議元件支援其他頁面類型（首頁、購物車、訂單確認）
* **希望清單**
   * 已登錄的訪問者可以將產品添加到願望清單
   * 通過myAccount修改願望清單及其產品
   * 可以通過策略在元件級別上啟用/禁用「添加到願望清單」按鈕（例如，產品預告、產品詳細資訊）
   * 可作為核心元件在Venia StorefrontAEM中使用

![希望清單](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager在as a Cloud Service2022.01.0中的發AEM布日期為2022年1月20日。 下一版計畫於2022年2月10日發行。

### 新增功能 {#what-is-new-cm}

* 雲管理器將 [在檢測到使用了相同的git提交時避免重建代碼庫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 在多個全棧流水線執行中。
* 現在訪AEM問環境日誌需要 **部署管理器** 產品配置檔案。 沒有此配置檔案的用戶將在用戶介面中看到禁用按鈕。
* UI將不允許為未將站點作為解決方案啟用的程式配置前端管道。
* 在生成Git密碼時，將顯示過期日期。

### 錯誤修正 {#bug-fixes-cm}

* 已更正某些前端管道部署遇到的空指針異常。
* 現在，當環境運行的是的過期版本時，可以添加、更新和刪AEM除環境變數。
* 對於在某些罕見情況下使用計畫步驟的管線，生成映像步驟將不再標籤為ERROR。
* 對於只有一個儲存庫的程式，管道執行螢幕現在將顯示儲存庫名稱。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.8.6的發佈日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 用戶能夠可靠地確定內容傳輸工具提取的所有內容是否已成功地被引入目標實例。 要使用此功能，您需要在 `System Console` 來源環AEM境。 請參閱 [驗證內容傳輸 — 入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 的子菜單。

### 錯誤修正 {#bug-fixes-ctt}

* 某些用戶未映射，因為用戶映射區分大小寫。 這個已經修復了。 用戶映射不再區分大小寫。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.24版的發佈日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測和報告具有和不具有智慧標籤的資產數。
* 能夠檢測和報告所使用的核心元件版本。
* 能夠檢測並報告執行BPA的源層（作者或發佈）的類型。

### 錯誤修正 {#bug-fixes-bpa}

* BPA規模邏輯的製作更快、更高效。
* 在某些情況下，BPA在運行時未增加分析計數。 這個已經修復了。
