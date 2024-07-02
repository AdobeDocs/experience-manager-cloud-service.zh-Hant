---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3a4dd9f1d769a9c9da12fdd8febfef481112d18c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 79%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16799 {#release-16799}

以下摘要說明 16799 維護版本的持續改善內容，該版本於 2024 年 6 月 18 日公開發佈。上一個維護版本是版本 16544。

2024.6.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16799}

* ASSETS-31977：增強型資產移動、複製和刪除作業。
* ASSETS-33618：Dynamic Media 中影片的自動轉錄和翻譯功能。
* ASSETS-35185：ContentHub 和 DM 的核准動作，並將屬性新增至 damAssetLucene 屬性。
* ASSETS-35533：將 DRM 和 CAI 屬性新增至 damAssetLucene 索引。
* ASSETS-37280：當來源字幕 (vtt) 仍在處理時，按照作業順序處理翻譯。
* ASSETS-37559：改善了資產刪除事件。
* ASSETS-37723：實施資產發佈事件。
* ASSETS-37724：實施資產未發佈事件。
* ASSETS-38614：共用連結 UI 增強。
* ASSETS-39601：自動將驗證規則運算式套用至資產 Livecopy 名稱。
* ASSETS-39454：在快速入門中升級到檢視器 2024.5.0。
* CNTBF-184：支援內容回流中 `/conf` 下方的路徑。

### 已修正的問題 {#fixed-issues-16799}

* ASSETS-37335：在篩選器中編輯搜尋面板會取消選取所有方塊。
* ASSETS-38069：時間軸篩選器選項的 AEM DAM PDF 預覽問題。
* ASSETS-38215：企業訂閱的 AEM as a Cloud Service 中，Adobe Stock 授權按鈕呈現灰色。
* ASSETS-38578：資產連結共用報告中的超連結不正確。
* ASSETS-38678：集合詳細資料中的檢視設定損壞。
* ASSETS-39071：如果原始呈現 MIME 類型為 Null，Web 最佳化傳遞可能會引發例外狀況。
* ASSETS-39316：集合中無法使用依照名稱排序功能。
* ASSETS-39377：從遠端 API 接收背壓時，從 OneDrive 大量匯入可能會失敗。
* ASSETS-39428：版權管理 UI 中的轉譯問題。
* CQ-4357150：cq-content-sync 套裝中的 Guava。
* GRANITE-52573：包含雙斜線 `//` 的要求遭到拒絕，狀態代碼為 400。
* SCRNS-4194：移除對 Google Guava API 的相依性。
* SCRNS-4360：頻道內容提供者中的非管理員使用者缺少管理發佈和快速發佈按鈕。
* SCRNS-4323：隱藏/停用 Screens.html 中的啟動。

#### 表單

* Forms-14844：即使失敗reCAPTCHA驗證，最適化Forms仍允許表單提交。
* Forms-14984：如果提交的資料中沒有「submitMetaData」，則使用驗證碼略過驗證的Forms。
* Forms-14477：規則編輯器中的「晚於」和「早於」選項在日期選擇器驗證中無法正常運作。
* Forms-14019：規則編輯器的「叫用服務」功能在通用編輯器中無法運作。
* Forms-14336：未選取任何表單欄位時，編輯器應會開啟，並聚焦於整個表單元素。
* Forms-15061：在規則編輯器中使用叫用服務選項時，載入器循環會無限期持續存在。

### 已知問題 {#known-issues-16799}

>[!NOTE]
> AEM Engineering 發現「啟動」功能已迴歸，從 16461 版開始的目前 AEM 版本會受到影響。由於這種迴歸，包含非深層頁面的新啟動 (套用新版本後建立) 將由於缺少設定而無法正確升級。
> 如果您的環境受到影響，可以透過客戶支援取得用於識別和更新缺失設定的 shell 指令碼 (內部參考 SITES-22457)。
> 將提供長期修正，以確保使用所有正確的設定建立新的啟動。在此之前，還可視需要提供內部修補版本。

#### 表單

* 當您安裝AEM SDK並新增 `AEM Forms add-on v2024.05.04.00-240400`，Docker服務無法啟動。 需要Docker服務才能在本機開發環境中生成記錄檔案。 若要修正問題：
   1. 下載 [hotfix](/help/forms/assets/sdk_hotfix.zip). 下載Hotfix時， `.zip` 資料夾已下載。
   1. 將下載的Hotfix解壓縮至資料夾。
   1. 取代舊的 `sdk.sh` 和 `sdk.bat` 在步驟2中擷取的資料夾中有較新檔案的檔案。

### 變更通知 {#change-notice-16799}

* 此版本包含以下新產品索引版本：
   * **damAssetLucene-11**
   * **fragments-11**

  先前索引版本的自訂版本將自動與新產品索引版本合併。請對合併版本套用進一步的自訂更新。

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-16799}

若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16799}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
