---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 100%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 16145 版本 {#release-16145}

下面是 16145 維護版的持續改善內容，該版本於 2024 年 5 月 1 日公開發佈。上一個維護版本是版本 15977。

2024.5.0 功能啟用可提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16145}

* ASSETS-23489：存放庫深入解析增強。
* ASSETS-26926：Dynamic Media 上傳輪詢改進。
* ASSETS-30351：下載對話方塊應非同步載入 Dynamic Media 呈現大小。
* ASSETS-30379：提高下載的 DRM 授權的解析度。
* ASSETS-31058：在「呈現」標籤的 AEM 資產 UI 中顯示智慧型裁切呈現，並在使用者點擊這些呈現時產生智慧型裁切影像。
* ASSETS-31218：在資產傳遞 API 中新增對名為 smartcrop 的支援。
* ASSETS-31979：在非同步資產操作期間新增視覺指示器並停用 UI 功能。
* ASSETS-32735：資產中繼資料更新事件改進。
* ASSETS-34661：用於 DM 預覽的 API 和/或來自 AEMaaCS Publish 的傳遞 URL。
* ASSETS-37259：XMP 剖析改進。
* ASSETS-37263：允許取消失敗的資產非同步工作。
* CNTBF-114：內容回流改進。
* CNTBF-148：內容回流改進。
* CQ-4356992：最新的 AEM 和 Granite 翻譯。
* SITES-19326：更新 Assets UI 中的連結，以便在新的 CF 編輯器中開啟 CF。
* SITES-20686：GraphQL - 透過 _dmS7Url 公開 Dynamic Media URL (適用於非影像資產)。
* SKYOPS-68091：更新至 Java 11.0.20。

### 已修正的問題 {#fixed-issues-16145}

* ASSETS-32321：如果上階資料夾缺少「jcr:content」子節點，後處理工作流程解析將會失敗。
* ASSETS-33856：JPEG 影像預設將檔案下載為 TXT。
* ASSETS-34096：修正非同步下載報告的觸控式 UI 視圖。
* ASSETS-34493：啟用多公司功能切換後載入下載對話方塊失敗。
* ASSETS-34824：對於 DM 停用資料夾，複製 url 顯示為空。
* ASSETS-35226：如果在 DAM 根目錄上指定，則後處理工作流程無法解析。
* ASSETS-35559：將 DM 批次上傳失敗記錄降為「警告」。
* ASSETS-35860：AEM Assets 欄視圖中的時區轉換不正確。
* ASSETS-35935：關閉承載檢閱後資料夾導覽不正確。
* ASSETS-35961：新增裁切按鈕在影像設定檔中無法運作。
* ASSETS-36227：發佈時停用 FolderPreviewUpdaterImpl 服務。
* ASSETS-36943：當清單視圖中的資料夾中出現 CF 和其他非 CF 項目時，會遺失對齊的欄。
* ASSETS-36990：匯出的中繼資料工作因大量屬性而失敗/緩慢。
* ASSETS-37113：如果查詢僅傳回 CF 結果，重新處理資產工作將立即終止。
* ASSETS-37260：AEM 中的中繼資料匯出可能會產生無效的 CSV。
* ASSETS-37261：AEM Assets 上的 PPTx 和 PDF 註解問題。
* ASSETS-37282：開啟大型資料夾的請求可能會很慢。
* ASSETS-37330：從 OneDrive 大量匯入會建立不正確的 AEM 資料夾結構。
* ASSETS-37609：刪除舊版 scene7 conf 查詢。
* ASSETS-38016：事件中未正確追蹤某些中繼資料更新。
* CQ-4357161：AEM 收件匣承載畫面傳回 404。
* GRANITE-50041：當解析度大於 1440px 寬度且下拉選項中只有「新增呈現」選項時，新增呈現無法運作。
* GRANITE-50279：Coral Datepicker 元件中的周名稱順序錯誤。
* SCRNS-3949：Screens 頻道擷取請求時間太長。
* SCRNS-3981：[序列管道]當元素載入/卸載事件序列被扭曲時會造成螢幕變黑。
* SCRNS-4180：[序列頻道]從備援影片縮圖復原後，影片長度為 -1 的頻道序列會停止並顯示空白畫面。
* SCRNS-4245：[序列頻道]載入影片和從備援影片縮圖切換時，空白畫面持續時間有限。
* SITES-16055：修正對應屬性頁面中的 Live Copy 和 Live Copy 來源連結。
* SCRNS-4243：內容提供者中缺少針對非管理員使用者的按鈕。

### 已知問題 {#known-issues-16145}

無。

### 已過時的功能和 API {#deprecated-16145}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 從 2024 年 5 月 1 日起，Adobe Dynamic Media 將終止對以下項目的支援：

   * SSL (安全通訊端層) 2.0
   * SSL 3.0
   * TLS (傳輸層安全性) 1.0 和 1.1
   * TLS 1.2 中的以下弱密碼：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16145}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.6 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
