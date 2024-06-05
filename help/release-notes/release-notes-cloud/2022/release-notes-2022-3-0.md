---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 版發行說明 {#release-notes}

以下章節概述2022.3.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2022.3.0)為2022年3月31日。
下一個版本(2022.4.0)計畫於2022年5月5日發行。

## 發行影片 {#release-video}

請檢視 [2022年3月版本總覽](https://video.tv.adobe.com/v/341465) 2022.3.0版新增功能摘要影片。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 發行前通道中可用的新功能 {#prerelease-features-sites}

* 現在可以使用內容模型編輯器中的簡單核取方塊，將內容模型資料型別定義為可翻譯。 此外，AEM翻譯規則和設定也會自動更新。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [!DNL AEM Dynamic Media] 現在提供下列彈性： [設定一個別名帳戶](/help/assets/dynamic-media/dm-alias-account.md) ，以確保更新開箱即用的Dynamic Media URL和檢視器內嵌程式碼。 這會對SEO產生正面影響，反映對企業內容所做的更新，例如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 使用者介面至：

   * 設定 [偵測重複資產](/help/assets/detect-duplicate-assets.md) 存放庫中。

   * 設定 [新增數位浮水印](/help/assets/watermark-assets.md) 至影像。

* 管理員現在可以設定電子郵件服務以進行大量下載。 它可讓使用者 [啟用大量下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 介面。 使用者在完成下載後會收到電子郵件通知，其中包含封存zip資料夾的下載連結。

* 此 [管理發布](/help/assets/manage-publication.md) 功能有改進的使用者介面。 使用者可以將內容發佈或取消發佈到所選目的地，或從所選目的地取消發佈內容， [新增內容](/help/assets/manage-publication.md#add-content) 從整個DAM存放庫發佈清單， [包含資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 若要發佈所選資料夾的內容並套用篩選器，以及 [排程發佈](/help/assets/manage-publication.md#publish-assets-later) 至之後的日期或時間。

### [!DNL Assets] 發行前通道中可用的新功能 {#prerelease-features-assets}

* 您現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 在標籤選擇器視窗中，根據標簽名稱、建立日期或修改日期的升序或降序順序。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**： [Document Generation API](/help/forms/aem-forms-cloud-service-communications.md) 協助組合、重新排列和驗證PDF檔案。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 組合PDF檔案。
   * 拆解PDF檔案。
   * 轉換為並驗證符合PDF/A標準的檔案。

* **自動將超過15頁的PDF forms轉換為最適化表單**：您現在可以使用automated forms conversion服務，將最多40頁的PDF forms轉換為最適化表單。 此服務現在提供將超過15頁的表單部分轉換為最適化表單片段的選項。 它有助於提高轉換表單的渲染速度，並使在自適應表單編輯器中載入大型表單變得更容易。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **使用自訂XCI產生記錄檔案**：您現在可以使用自訂XCI檔案來設定記錄檔案的各種屬性。 它會以自訂變更覆寫主XCI。

* **在最適化表單中使用隱藏的驗證碼**：只有在可疑活動的情況下，您才能使用隱藏的驗證碼來顯示驗證碼質詢。 如果未發現可疑活動，則不顯示驗證碼質詢。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 改進多儲存場景的SEO：現在可以透過CIF雲端設定屬性在儲存層級上設定PDP/PLP的URL格式
* 產品選取器透過UI中的新篩選器選項支援分階段產品。  這可讓內容從業人員為即將推出的產品準備產品內容管理
* 使用CIF Cloud Config名稱（而不是config proxy url）簡化CIF設定管理和錯誤處理
* 產品清單和轉盤元件的手動類別選擇。 這可讓內容從業人員在目錄體驗之外的內容頁面上使用這些元件

### CIF發行前管道中可用的新功能 {#prerelease-features-cif}

* AEM CIF搜尋核心元件支援Commerce LiveSearch

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 為了更有效率並有效地疑難排解雲端環境中的自訂功能，我們發佈了一款新的開發人員工具 —  [存放庫瀏覽器](/help/implementing/developing/tools/repository-browser.md). 它是一個輕量、只讀、HTML的瀏覽器，您可以從開發人員控制檯啟動。 瞭解發佈者、作者和預覽層以及所有環境（包括生產、暫存和開發）中的內容存放庫。 瀏覽內容結構、檢視屬性，以及預覽和下載二進位檔案。

  ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* 現在，用於驗證伺服器到伺服器API呼叫(例如，GraphQL API請求)的憑據可以在開發人員控制檯以自助服務方式過期之前刷新。 請參閱 [檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 以取得更多資訊。

* 版本清除和稽核記錄清除維護任務（以前未啟用）現在已為新環境啟用。 請參閱以下檔案中的相關值： [維護任務](/help/operations/maintenance.md) 文章。

* AEMas a Cloud ServiceSDK Dispatcher工具現在支援配備M1晶片的Mac電腦

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

「內容轉移工具v1.9.0」的發行日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 內容轉移工具檢查大小功能有助於減少失敗的內容轉移。  使用「檢查大小」功能，使用者可以1)判斷是否有足夠的磁碟空間 `crx-quickstart` 擷取前的子目錄，以及2)估計移轉集大小並驗證其是否受支援。 如果違反了其中一項或兩項檢查，使用者會在CTT UI中看到警告。 有了這道護欄，您可以避免內容轉移失敗，並主動與Adobe客戶服務討論移轉選項。 另請參閱 [正在決定移轉集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#migration-set-size) 以取得更多詳細資料。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的發行日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 可偵測未處理的資產。 如果偵測到未處理的資產，則需要將這些資產設定為已處理，或在內容轉移期間從移轉集將其移除，以避免在內容擷取期間遇到問題。
* 能夠偵測內容是否超過1000個虛名URL。 使用大量虛名URL不是最佳做法，因為它會讓Dispatcher和Publish伺服器承受負載。
* 能夠識別Oak索引定義相關問題並偵測與AEMas a Cloud Service的不相容性。
* 能夠偵測和報告外部器設定的使用情況。 在AEM中，as a Cloud Service的外部化工具設定是由Cloud Manager設定，因此，需要重構現有的外部化工具設定以保持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法執行，因為FormsSelectiveFeaturesAnalysis擲回宣告錯誤。 此問題已修正。
* BPA將與WRK模式相關的發現回報為MAJOR而非CRITICAL。 此問題已修正。
* BPA錯誤地將ui.apps中與OAK索引定義相關的發現回報為CRITICAL。 此問題已修正
