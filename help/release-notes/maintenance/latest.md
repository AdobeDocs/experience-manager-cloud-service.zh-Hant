---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 19%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16971 {#release-16971}

以下摘要說明維護版本16971數的持續改善，該版本於2024年7月3日公開發佈。 上一個維護版本是版本 16799。

2024.7.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16971}

* SITES-22948：移除AEM CS基礎內容中的商務參考。
* SITES-22141： [內容片段] OnRC之後CFM ModelChangeRepositoryImpl中的SegmentNotFoundException。
* SITES-21893：作者例項上的影像裁切問題。
* SITES-21788： [內容片段] 為模型啟用uiSchema時，在CF和CF模型編輯器中顯示NOTE。
* SITES-21688： MSM轉出不會更新即時副本頁面上的體驗片段(XF)路徑。
* SITES-21659：傳回建立/修改/復寫模型資源之使用者的全名。
* SITES-21609：將內容片段從一個模型移轉至另一個模型的OpenAPI端點。
* SITES-21598： [開啟API] 建立CFM — 如果指定的設定路徑不存在，則傳回錯誤。
* SITES-21491： [開啟API] CFPATCH端點應遵循欄位層級的即時關係。
* SITES-21434： [開啟API] CFGET端點應遵循欄位層級的即時關係。
* SITES-21415： CF編輯器 — 支援UUID參照。
* SITES-21326： [開啟API] 提供有關是否存在內容片段參考的資訊。
* SITES-21310： [開啟API] 在翻譯API回應中新增內容片段的ID。
* SITES-20859： CF Open API — 依路徑擷取片段時傳回參考。
* SITES-20687： [開啟API] 批次處理狀態擷取的端點。
* SITES-20657： [開啟API] 使用以下專案取代字串時，為match全字提供選項 `FindAndReplace` 端點。
* SITES-20587： [開啟API] 建立 `COPY` 內容片段的端點。
* SITES-20584： [開啟API] 最佳化參考擷取。
* SITES-20308： [開啟API] 啟用API上的批次處理。
* SITES-19976： [開啟API] 條件欄位的通用UI結構描述。
* SITES-19556： [內容片段] 如果編輯模型時存在uiSchema，請更新它。
* SITES-18056： [開啟API] 將內容片段發佈到預覽時，包含參考。
* SITES-16898： [結構描述] OpenAPI端點可將內容片段從一個模型移轉至另一個模型。
* SITES-16609：列出啟動端點。
* sites-16606：建立啟動端點。
* SITES-21617： [Xwalk] 在UE內讓頁面屬性/中繼資料可編輯。
* SITES-19614： [Xwalk] 試算表編輯器分頁和無限捲動。
* SITES-22163： [Xwalk] 改善對Edge Delivery Sites發佈層級所提供內容的支援。
* SITES-22109： [Xwalk] 改善RTF標籤後續處理的處理。
* SITES-22035： [Xwalk] 改善MSM和Launch的處理。
* SITES-21839： [Xwalk] 改善Edge Delivery未提供內容的路徑對應和清理功能。

### 已修正的問題 {#fixed-issues-16971}

* CQ-4356898： [翻譯] 包含異常大量連結的CF出現outOfMemory錯誤。
* CQ-4357055： [翻譯] 使用Rest API時，自動翻譯無法運作。
* CQ-4353931： [翻譯] 在翻譯來源頁面/xf/asset中新增jcr：uuid （若其遺失）。
* CQ-4357591： [翻譯] 修改「關聯JCR：UUID」工作流程以用於「頁面/XF」。
* Forms-14844：即使失敗reCAPTCHA驗證，最適化Forms仍允許表單提交。
* Forms-14984：如果提交的資料中沒有「submitMetaData」，則使用驗證碼略過驗證的Forms。
* Forms-14477：規則編輯器中的「晚於」和「早於」選項在日期選擇器驗證中無法正常運作。
* Forms-14019：規則編輯器的「叫用服務」功能在通用編輯器中無法運作。
* Forms-14336：未選取任何表單欄位時，編輯器應會開啟，並聚焦於整個表單元素。
* Forms-15061：在規則編輯器中使用叫用服務選項時，載入器循環會無限期持續存在。
* SITES-22457：提升非深層啟動不會更新來源內容。
* SITES-22748： [內容片段] 增強內容片段更新工作的錯誤處理
* SITES-22349： [內容片段] 無法變更空白多行cf元素的ContentType。
* SITES-22343： [內容片段] 語意型別「分項清單」已中斷。
* SITES-22194：設定重新導向後，model.json不再運作。
* SITES-21953： [開啟API] 會根據validationStatus的順序變更Etag。
* SITES-21894： [開啟API] 建立CF時增強父路徑驗證。
* SITES-21887： [開啟API] POST變數端點傳回無效的ETag。
* SITES-21657： [開啟API] 改善CF搜尋路徑屬性的驗證。
* SITES-21949：搜尋API無效的游標傳回500。
* SITES-20927：當查詢遺失時，搜尋API會傳回500。
* SITES-20544： [開啟API] 變更發佈套件名稱的產生，以避免Oak衝突。
* SITES-19710： CVE-2022-47937 — 從頁面編輯器中移除org.apache.sling.commons.json的所有使用方式。
* SITES-11992： [協助工具] 附注色票選擇器按鈕遺失可存取的名稱。
* SITES-10979： [協助工具] 標籤不是永久性的。
* SITES-10962： [協助工具] 按鈕：按鈕沒有角色。
* SITES-10905： [協助工具] 作用中元件的狀態缺少3對1的對比率。
* SITES-2974：  [協助工具]  — 以320px寬度水準捲動。
* SITES-22026：無法在AEM中的資料夾之間移動體驗片段
* SITES-22106：新內容片段編輯器中的語言切換功能問題
* SITES-21980：以UUID為基礎的參考型別處理不一致。
* SITES-7257：ThumbnailServlet中的NPE。

### 已知問題 {#known-issues-16971}

無。

### 變更通知 {#change-notice-16971}

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-16971}

若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16971}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
