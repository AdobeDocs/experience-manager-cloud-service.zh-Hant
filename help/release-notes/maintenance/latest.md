---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 53b692b9f668387c889c28498bb20c67149e36be
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 28%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16799 {#release-16799}

以下摘要說明維護版本16799數的持續改善，該版本於2024年6月18日公開發佈。 上一個維護版本是版本 16544。

2024.6.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/tw/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16799}

* ASSETS-31977：增強資產移動、複製和刪除作業。
* ASSETS-33618： Dynamic Media中視訊的自動轉寫和翻譯功能。
* ASSETS-35185：ContentHub和DM的核准動作，並新增屬性至damAssetLucene屬性。
* ASSETS-35533：將DRM和CAI屬性新增至damAssetLucene索引。
* ASSETS-37280：當來源子標題(vtt)仍在處理時，翻譯的循序工作處理。
* ASSETS-37559：改善資產已刪除事件。
* ASSETS-37723：實作資產已發佈事件。
* ASSETS-37724：實作資產未發佈事件。
* ASSETS-38614：共用連結UI增強功能。
* ASSETS-39601：自動套用驗證Regex至Asset Livecopy名稱。
* ASSETS-39454：在Quickstart升級至2024.5.0版檢視器。
* CNTBF-184：下方支援路徑 `/conf` 於內容回流。

### 已修正的問題 {#fixed-issues-16799}

* ASSETS-37335：在篩選器中編輯搜尋面板會取消勾選所有方塊。
* ASSETS-38069：時間軸篩選器選擇中的AEM DAMPDF預覽問題。
* ASSETS-38215：適用於企業訂閱的AEMas a Cloud Service中，Adobe Stock授權按鈕顯示為灰色。
* ASSETS-38578：資產連結共用報表中的超連結不正確。
* ASSETS-38678：檢視在集合詳細資料中破壞的設定。
* ASSETS-39071：如果原始轉譯mimetype為null，Web最佳化傳送可能會擲回例外狀況。
* ASSETS-39316：按名稱排序在集合中無法運作。
* ASSETS-39377：從遠端API接收背壓時，從OneDrive大量匯入可能會失敗。
* ASSETS-39428：版權管理UI中的轉譯問題。
* CQ-4357150：cq-content-sync套裝中的Guava。
* GRANITE-52573：包含雙斜線的請求 `//` 已拒絕，狀態碼為400。
* SCRNS-4194：移除對Google Guava API的相依性。
* SCRNS-4360：頻道內容提供者中的非管理員使用者缺少管理出版物和快速發佈按鈕。
* SCRNS-4323：隱藏/停用screens.html中的啟動。

### 已知問題 {#known-issues-16799}

>[!NOTE]
> AEM工程部門已針對Launches功能找出回歸，而這會影響目前從16461開始的AEM版本。 由於此回歸，包含非深層頁面的新啟動（在套用新版本後建立）由於遺失設定，將無法正常提升。
> 如果您的環境受到影響，可透過客戶支援使用殼層指令碼來識別和更新缺少的設定(內部參考SITES-22457)。
> 我們將提供更長期的修正，以確保使用所有正確的設定來建立新的啟動。 在此之前，您也可依需求使用內部修補程式版本。

#### 表單

1. 如果使用者下載最新的AEM Forms SDK (`AEM Forms add-on v2024.05.04.00-240400`)，批次檔案無法啟動Docker服務。 若要解決此問題：
   1. 下載 [資料夾](/help/forms/assets/sdk_hotfix.zip).
   1. 從下載的資料夾中解壓縮內容，並複製 `sdk.sh` 和 `sdk.bat` 檔案。
   1. 取代現有的 `sdk.sh` 和 `sdk.bat` AEM Forms SDK中包含新檔案的檔案。

### 變更通知 {#change-notice-16799}

* 此發行版本包含下列新產品索引版本：
   * **damAssetLucene-11**
   * **片段–11**

  舊版索引的自訂版本會自動與新產品索引版本合併。 請進一步套用自訂更新至合併的版本。

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
