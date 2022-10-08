---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 7%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.3.0)為2022年3月31日。
下一版(2022.4.0)預計於2022年5月5日推出。

## 發行影片 {#release-video}

查看 [2022年3月發行概述](https://video.tv.adobe.com/v/341465) 影片，以取得2022.3.0版中新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 搶鮮版頻道中可用的新功能 {#prerelease-features-sites}

* 內容模型資料類型現在可使用內容模型編輯器中的簡單核取方塊定義為可翻譯。 此外，也會自動更新AEM翻譯規則和設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] 現在可靈活地 [配置一個別名帳戶](/help/assets/dynamic-media/dm-alias-account.md) ，進而確保更新現成可用的Dynamic Media URL和檢視器內嵌程式碼。 這對SEO有正面影響，可反映對您的業務內容所做的更新，例如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 用戶介面：

   * 設定 [偵測重複資產](/help/assets/manage-digital-assets.md#detect-duplicate-assets) 儲存庫。

   * 設定 [添加數字水印](/help/assets/watermark-assets.md) 到影像。

* 管理員現在可以設定電子郵件服務以進行大量下載。 可讓使用者 [啟用大量下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 介面。 使用者在下載程式完成時，會收到包含已封存Zip資料夾的下載連結的電子郵件通知。

* 此 [管理出版物](/help/assets/manage-publication.md) 透過改善的使用者介面來增強功能。 使用者可以從選取的目的地，發佈或取消發佈內容， [新增內容](/help/assets/manage-publication.md#add-content) 從DAM存放庫的發佈清單， [包含資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 發佈所選資料夾的內容並應用篩選器，以及 [排程發佈](/help/assets/manage-publication.md#publish-assets-later) 到以後的日期或時間。

### [!DNL Assets] 搶鮮版頻道中可用的新功能 {#prerelease-features-assets}

* 您現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 依據標籤名稱、建立日期或修改日期，以遞增或遞減順序在標籤選取器視窗中顯示。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [檔案產生API](/help/forms/aem-forms-cloud-service-communications.md) 幫助組合、重新排列和驗證PDF文檔。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 組合PDF文檔。
   * 拆解PDF文檔。
   * 轉換為並驗證PDF/A相容的文檔。

* **自動將大於15頁的PDF forms轉換為最適化表單**:您現在可以使用automated forms conversion服務，將最多40頁的PDF forms轉換為最適化表單。 此服務現在提供將超過15頁的表單區段轉換為最適化表單片段的選項。 有助於改善轉換表單的轉譯速度，並讓您在最適化表單編輯器中輕鬆載入大型表單。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **使用自訂XCI產生記錄檔案**:您現在可以使用自訂XCI檔案來設定記錄檔案的各種屬性。 會以自訂變更覆寫主XCI。

* **在最適化表單中使用不可見的驗證碼**:只有在可疑活動時，才可使用隱形驗證碼來顯示驗證碼挑戰。 如果未發現任何可疑活動，則不顯示驗證碼質詢。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 改善多商店案例的SEO:現在可透過CIF雲端設定屬性，在商店層級設定PDP/PLP的URL格式
* 產品選擇器透過UI中的新篩選器選項支援分段產品。  這可讓內容從業人員為即將推出的產品做準備產品內容管理
* 使用CIF雲端設定名稱（而非設定代理url）簡化CIF設定管理和錯誤處理
* 手動選擇產品清單和輪播元件的類別。 這可讓內容從業人員在目錄體驗之外的內容頁面上使用這些元件

### CIF發行前管道提供的新功能 {#prerelease-features-cif}

* AEM CIF搜尋核心元件支援Commerce LiveSearch

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 為了更有效率且有效地疑難排解雲端環境中的自訂功能，我們發行了新的開發人員工具 —  [儲存庫瀏覽器](/help/implementing/developing/tools/repository-browser.md). 這是輕量型、唯讀、HTML的瀏覽器，您可以從開發人員控制台啟動。 在發佈商、製作和預覽層級，以及在所有環境（包括生產、預備和開發）中，洞察內容存放庫。 瀏覽內容結構、檢視屬性，以及預覽和下載二進位檔。

   ![repbrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* 現在，用於驗證伺服器對伺服器API呼叫的憑證（例如，用於GraphQL API請求）可從開發人員控制台以自助式方式在到期前重新整理。 請參閱 [檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 以取得詳細資訊。

* 版本清除和審核日誌清除維護任務（以前未啟用）將啟用新環境。 請參閱 [維護任務](/help/operations/maintenance.md) 文章。

* AEMas a Cloud ServiceSDK Dispatcher工具現在支援採用M1晶片的Mac電腦

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具1.9.0版的發行日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 「內容轉移工具檢查大小」功能有助於減少失敗的內容轉移。  使用「檢查大小」功能，用戶可以1)確定他們在 `crx-quickstart` 子目錄，提取前，和2)預估移轉集大小並確認是否支援。 如果違反上述一項或兩項檢查，使用者在CTT UI中會看到警告。 透過此護欄，您可以避免內容傳輸失敗，並主動與Adobe客戶服務討論移轉選項。 請參閱 [確定遷移集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 以取得更多詳細資訊。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的發行日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 偵測未處理資產的功能。 如果偵測到未處理的資產，這些資產需要設為已處理，或需在內容轉移期間從移轉集中移除，以避免在內容擷取期間遇到問題。
* 偵測內容是否超過1000個虛名URL的功能。 使用大量虛名URL並非最佳作法，因為這會對Dispatcher和Publish伺服器造成負載。
* 能識別Oak索引定義相關問題，並偵測與AEMas a Cloud Service不相容。
* 能夠檢測並報告外部化程式配置的使用情況。 在AEMas a Cloud Service外部化程式設定中，由Cloud Manager設定，因此需重構現有外部化程式設定以維持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法運行，因為FormsSelectiveFeaturesAnalysis擲回斷言錯誤。 此問題已修正。
* BPA將與工作模式有關的結果報告為MAJOR，而非CRITICAL。 此問題已修正。
* BPA在ui.apps中以CRITICAL形式錯誤報告與OAK索引定義相關的發現。 此問題已修正
