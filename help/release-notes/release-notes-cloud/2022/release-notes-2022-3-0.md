---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 版發行說明。'
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
source-git-commit: 599f924465552b2ef43827da8e139c239e47baed
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 版發行說明 {#release-notes}

以下部分概述2022.3.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本版本(2022.3.0)為2022年3月31日。
下一版(2022.4.0)計畫於2022年5月5日發行。

## 發行影片 {#release-video}

看看 [2022年3月發佈概述](https://video.tv.adobe.com/v/341465) 視頻，瞭解2022.3.0版中添加的功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 發行前通道中可用的新功能 {#prerelease-features-sites}

* 現在，可以使用內容模型編輯器中的簡單複選框將內容模型資料類型定義為可翻譯。 此外，還AEM會自動更新翻譯規則和配置。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [!DNL AEM Dynamic Media] 現在提供了靈活性 [配置一個別名帳戶](/help/assets/dynamic-media/dm-alias-account.md) 在用戶介面中，從而確保更新出廠設定的Dynamic MediaURL和Viewer Embed代碼。 這對SEO產生了積極影響，以反映對您的業務環境所做的更新，如品牌重塑。

* 您現在可以使用 [!DNL Experience Manager Assets] 用戶介面：

   * 配置 [檢測重複資產](/help/assets/manage-digital-assets.md#detect-duplicate-assets) 的下界。

   * 配置 [添加數字水印](/help/assets/watermark-assets.md) 到影像。

* 管理員現在可以配置電子郵件服務以進行大下載。 它允許用戶 [啟用大量下載的電子郵件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 從 [!DNL Experience Manager Assets] 。 用戶在完成下載過程後接收包含存檔的zip資料夾的下載連結的電子郵件通知。

* 的 [管理發布](/help/assets/manage-publication.md) 利用改進的用戶介面增強特徵。 用戶可以將內容發佈或取消發佈到選定目標， [添加內容](/help/assets/manage-publication.md#add-content) 從DAM儲存庫到發佈清單， [包括資料夾設定](/help/assets/manage-publication.md#include-folder-settings) 發佈所選資料夾的內容並應用篩選器， [計畫發佈](/help/assets/manage-publication.md#publish-assets-later) 到更晚的日期或時間。

### [!DNL Assets] 發行前通道中可用的新功能 {#prerelease-features-assets}

* 你現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 按照標籤名稱、建立日期或修改日期的升序或降序排列。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [文檔生成API](/help/forms/aem-forms-cloud-service-communications.md) 幫助合併、重新排列和驗證PDF文檔。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   * 組合 PDF 文件.
   * 分解 PDF 文件.
   * 轉換為 PDF/A 相容文件並進行驗證.

* **自動將大於15頁的PDF forms轉換為自適應表單**:現在，您可以使用automated forms conversion服務將最多40頁的PDF forms轉換為自適應表單。 該服務現在提供了將超過15頁的表單部分轉換為自適應表單片段的選項。 它有助於提高轉換表單的渲染速度，並使在自適應表單編輯器中載入大型表單更加容易。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **使用自定義XCI生成記錄文檔**:現在，您可以使用自定義XCI檔案來設定記錄文檔的各種屬性。 它用自定義更改覆蓋主XCI。

* **以自適應形式使用不可見的驗證碼**:您只能在可疑活動時使用看不見的驗證碼顯示驗證碼挑戰。 如果未發現可疑活動，則不顯示驗證碼質詢。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 針對多儲存方案改進SEO:現在，可以通過CIF雲配置屬性在儲存級別上配置PDP/PLP的URL格式
* 產品選取器通過UI中的新篩選器選項支援分階段產品。  這使內容從業人員能夠為即將推出的產品準備產品內容管理
* 使用CIF雲配置名稱（而不是配置代理url）簡化CIF配置管理和錯誤處理
* 產品清單和旋轉傳送元件的手動類別選擇。 這允許內容從業人員在目錄體驗之外的內容頁面上使用這些元件

### CIF預發行渠道中提供的新功能 {#prerelease-features-cif}

* CIF搜AEM索核心元件支援Commerce LiveSearch

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 為了更高效、更高效地排除雲環境中的自定義功能，我們發佈了一個新的開發工具 —  [儲存庫瀏覽器](/help/implementing/developing/tools/repository-browser.md)。 它是一個輕量、只讀、HTML瀏覽器，您可以從開發人員控制台啟動。 查看發佈者、作者和預覽層上的內容儲存庫，以及所有環境（包括生產、舞台和開發）中的內容儲存庫。 瀏覽內容結構、查看屬性以及預覽和下載二進位檔案。

   ![repbrowsernel(reprowerser](/help/release-notes/assets/repobrowserrelnotes.png)

* 現在，用於驗證伺服器到伺服器API調用(例如，GraphQLAPI請求)的憑據可以在開發人員控制台以自助服務方式過期之前刷新。 查看 [文檔](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 的子菜單。

* 版本清除和審核日誌清除維護任務（以前未啟用）將啟用新環境。 請參閱 [維護任務](/help/operations/maintenance.md) 文章。

* AEMas a Cloud ServiceSDK Dispatcher Tools（SDK調度工具）現在支援具有M1晶片的Mac電腦

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.9.0的發佈日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 內容傳輸工具檢查大小功能有助於減少失敗的內容傳輸。  使用「檢查大小」功能，用戶可以1)確定他們在 `crx-quickstart` 在提取之前，先為子目錄，然後2)估計遷移集大小並驗證是否支援遷移集大小。 如果違反了其中一項或兩項檢查，用戶將在CTT UI中看到警告。 通過此保證，您可以避免內容傳輸失敗，並主動與Adobe客戶服務部門討論遷移選項。 請參閱 [確定遷移集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 的子菜單。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.26版的發佈日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 檢測未處理資產的能力。 如果檢測到未處理的資產，則這些資產要麼需要設定為已處理，要麼需要在內容傳輸期間從遷移集中刪除，以避免在內容接收期間遇到問題。
* 能夠檢測內容是否具有1000個以上虛擬URL。 使用大量虛擬URL不是最佳做法，因為它給Dispatcher和Publish伺服器載入了負載。
* 能夠識別與Oak索引定義相關的問題並檢測與AEMas a Cloud Service的不相容。
* 能夠檢測並報告外部化器配置的使用情況。 在AEMas a Cloud Service外部化器配置中，由雲管理器設定，因此需要重新構造現有外部化器配置，以保持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法運行，因為FormsSelectiveFeaturesAnalysis引發斷言錯誤。 這個已經修復了。
* 雙酚A以主要而非關鍵的方式報告與工作模式有關的調查結果。 這個已經修復了。
* BPA錯誤地將與ui.apps中的OAK索引定義相關的發現報告為CRITICAL。 已修復
