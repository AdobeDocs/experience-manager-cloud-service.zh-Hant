---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 29%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 16145 版本 {#release-16145}

以下摘要說明維護版本16145數的持續改善，該版本於2024年5月1日公開發佈。 上一個維護版本是版本 15977。

2024.5.0 功能啟用可提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16145}

* ASSETS-23489：儲存庫深入分析增強功能。
* ASSETS-26926： Dynamic Media上傳輪詢改善。
* ASSETS-30351：「下載」對話方塊應以非同步方式載入Dynamic Media轉譯大小。
* ASSETS-30379：改善下載中DRM授權解析度。
* ASSETS-31058：在轉譯索引標籤的AEM Assets UI中顯示智慧型裁切轉譯，並在使用者按一下這些轉譯時產生智慧型裁切影像。
* ASSETS-31218：在資產傳送api中新增對已命名smartcrop的支援。
* ASSETS-31979：在非同步資產操作期間新增視覺指示器並停用UI函式。
* ASSETS-32735：改善資產中繼資料更新事件。
* ASSETS-34661：適用於DM預覽和/或來自AEMaaCS Publish的傳送URL的API。
* ASSETS-37259：XMP剖析改善。
* ASSETS-37263：允許取消失敗的資產非同步作業。
* CNTBF-114：改善內容回流。
* CNTBF-148：改善內容回流。
* CQ-4356992：最新的AEM和Granite翻譯。
* SITES-19326：更新 Assets UI 中的連結，以便在新的 CF 編輯器中開啟 CF。
* SITES-20686： GraphQL — 透過_dmS7Url公開Dynamic Media URL （適用於非影像資產）。
* SKYOPS-68091：更新至Java 11.0.20。

### 已修正的問題 {#fixed-issues-16145}

* ASSETS-32321：如果上級資料夾缺少「jcr：content」子節點，後處理工作流程解析會失敗。
* ASSETS-33856：JPEG影像預設集會以TXT格式下載檔案。
* ASSETS-34096：修正非同步下載報表的觸控式UI檢視。
* ASSETS-34493：啟用多公司功能切換後，載入下載對話方塊失敗。
* ASSETS-34824：DM停用資料夾的複製URL會顯示為空白。
* ASSETS-35226：如果在DAM根上指定，則後處理工作流程未解析。
* ASSETS-35559：將DM批次上傳失敗記錄檔減少為WARN。
* ASSETS-35860：AEM Assets 欄視圖中的時區轉換不正確。
* ASSETS-35935：關閉裝載檢閱後檔案夾導覽不正確。
* ASSETS-35961：在影像設定檔下新增裁切按鈕無法運作。
* ASSETS-36227：停用發佈上的FolderPreviewUpdaterImpl服務。
* ASSETS-36943：當CF和其他非CF專案出現在清單檢視的資料夾中時，遺漏對齊的欄。
* ASSETS-36990：匯出的中繼資料作業失敗/速度變慢，並出現大量屬性。
* ASSETS-37113：如果查詢只傳回CF結果，則重新處理資產作業會立即終止。
* ASSETS-37260：AEM中的中繼資料匯出可能會產生無效的CSV。
* ASSETS-37261：AEM Assets上的PPTx和PDF附註問題。
* ASSETS-37282：開啟大型資料夾的請求速度可能變慢。
* ASSETS-37330：從OneDrive大量匯入會建立不正確的AEM資料夾結構。
* ASSETS-37609：移除舊版scene7 conf查閱。
* ASSETS-38016：事件中未正確追蹤部分中繼資料更新。
* CQ-4357161： AEM收件匣裝載畫面傳回404訊息。
* GRANITE-50041：當下拉式清單選項中只有「新增轉譯」選項時，如果解析度大於1440px寬度，則新增轉譯無法運作。
* GRANITE-50279：Coral日期選取器元件中的周名稱無序。
* SCRNS-3949： Screens頻道擷取要求時間太長。
* SCRNS-3981： [順序頻道] 當元素載入/解除安裝事件的順序扭曲時，會產生黑色熒幕。
* SCRNS-4180： [順序頻道] 當頻道從遞補縮圖復原時，畫面會以空白畫面停止顯示持續時間–1的影片。
* SCRNS-4245： [順序頻道] 載入和從遞補縮圖切換視訊時，有限的「空白熒幕」持續時間。
* SITES-16055：修正各個屬性頁面中的即時副本和即時副本來源連結。
* SCRNS-4243：非管理員使用者的內容提供者中缺少按鈕。

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
