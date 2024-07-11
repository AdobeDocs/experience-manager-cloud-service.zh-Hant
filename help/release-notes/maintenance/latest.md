---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: ht
source-wordcount: '944'
ht-degree: 100%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16971 {#release-16971}

以下摘要說明 16971 維護版本的持續改善內容，該版本於 2024 年 7 月 3 日公開發佈。上一個維護版本是版本 16799。

2024.7.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16971}

* SITES-22948：移除 AEM CS 基礎內容中的商務參考。
* SITES-22141：[內容片段] - OnRC 之後，CFM ModelChangeRepositoryImpl 出現 SegmentNotFoundException。
* SITES-21893：作者實例上的影像裁切問題。
* SITES-21788：[內容片段] - 為模型啟用 uiSchema 時，在 CF 和 CF 模型編輯器中顯示註解。
* SITES-21688：MSM 推出不會更新 Live Copy 頁面上的體驗片段 (XF) 路徑。
* SITES-21659：傳回建立/修改/複製模型資源的使用者全名。
* SITES-21609：OpenAPI 端點將內容片段從一個模型移轉至另一個模型。
* SITES-21598：[Open API] - 建立 CFM - 如果所提供的設定路徑不存在，則傳回錯誤。
* SITES-21491：[Open API] - CF PATCH 端點應遵循欄位層級的即時關係。
* SITES-21434：[Open API] - CF GET 端點應遵循欄位層級的即時關係。
* SITES-21415：CF 編輯器 - 支援 UUID 參考。
* SITES-21326：[Open API] - 為內容片段提供參考是否存在的資訊。
* SITES-21310：[Open API] - 在翻譯 API 回應中加入內容片段的 ID。
* SITES-20859：CF Open API - 依路徑擷取片段時傳回參考。
* SITES-20687：[Open API] - 用於批次處理狀態擷取的端點。
* SITES-20657：[Open API] - 使用 `FindAndReplace` 端點取代字串時提供符合整個單字的選項。
* SITES-20587：[Open API] - 為內容片段建立 `COPY` 端點。
* SITES-20584：[Open API] - 最佳化參考擷取。
* SITES-20308：[Open API] - 在 API 上啟用批次處理。
* SITES-19976：[Open API] - 條件欄位的通用 UI 結構描述。
* SITES-19556：[內容片段] - 更新 uiSchema (如果編輯模型時其存在)。
* SITES-18056：[Open API] - 將內容片段發佈至預覽時，會包含參考。
* SITES-16898：[Schema] OpenAPI 端點將內容片段從一個模型移轉至另一個模型。
* SITES-16609：列出啟動端點。
* SITES-16606：建立啟動端點。
* SITES-21617：[Xwalk] - 使頁面屬性/中繼資料可在 UE 中編輯。
* SITES-19614：[Xwalk] - 試算表編輯器分頁和無限捲動。
* SITES-22163：[Xwalk] - 已改善對 Edge Delivery 網站發佈層所提供內容的支援。
* SITES-22109：[Xwalk] - 已改善對 RTF 標記後處理的處理。
* SITES-22035：[Xwalk] - 已改善對 MSM 和啟動的處理。
* SITES-21839：[Xwalk] - 已改善對 Edge Delivery 未提供之內容的對應和清理。

### 已修正的問題 {#fixed-issues-16971}

* CQ-4356898：[翻譯] - CF 出現 outOfMemory 錯誤，其中包含異常大量的連結。
* CQ-4357055：[翻譯] - 使用 Rest API 無法自動翻譯。
* CQ-4353931：[翻譯] - 在翻譯來源頁面/xf/資產缺少 jcr:uuid 時新增。
* CQ-4357591：[翻譯] - 修改「關聯 JCR:UUID」工作流程以適用於頁面/XF。
* FORMS-14844：儘管 reCAPTCHA 驗證失敗，最適化表單仍允許表單提交。
* FORMS-14984：如果提交的資料中不存在「submitMetaData」，則含 CAPTCHA 的表單會跳過驗證。
* FORMS-14477：規則編輯器中的「Is After」和「Is Before」選項在日期選擇器驗證中失去作用。
* FORMS-14019：規則編輯器的「呼叫服務」功能在通用編輯器中失去作用。
* FORMS-14336：當未選取任何表單欄位時，編輯器應開啟且焦點放在整個表單元素。
* FORMS-15061：在規則編輯器中使用呼叫服務選項後，載入程式循環將無限期地持續存在。
* SITES-22457：升級非深層的啟動不會更新來源內容。
* SITES-22748：[內容片段] - 增強對內容片段更新作業的錯誤處理
* SITES-22349：[內容片段] - 空白多行 cf 元素的 ContentType 無法變更。
* SITES-22343：[內容片段] - 語意類型「列舉」已損壞。
* SITES-22194：設定重新導向後，model.json 不再作用。
* SITES-21953：[Open API] Etag 依照 validationStatus 的順序進行變更。
* SITES-21894：[Open API] - 增強建立 CF 時的父路徑驗證。
* SITES-21887：[Open API] - POST 變化版本端點傳回無效 ETag。
* SITES-21657：[Open API] - 改善對 CF 搜尋路徑屬性的驗證。
* SITES-21949：Search API 無效游標傳回 500。
* SITES-20927：遺失查詢時，Search API 傳回 500。
* SITES-20544：[Open API] - 變更發佈套件的產生以避免 Oak 衝突。
* SITES-19710：CVE-2022-47937 - 從頁面編輯器中刪除 org.apache.sling.commons.json 的所有使用情況。
* SITES-11992：[協助工具] - 註解改良選取器按鈕缺少無障礙名稱。
* SITES-10979：[協助工具] - 標籤不會持續存在。
* SITES-10962：[協助工具] - 按鈕：按鈕沒有角色。
* SITES-10905：[協助工具] - 活動組件的狀態缺乏 3 比 1 的對比比率。
* SITES-2974：[協助工具] - 以 320 像素寬度水平滾動。
* SITES-22026：無法在 AEM 的資料夾之間移動體驗片段
* SITES-22106：新內容片段編輯器發生語言切換功能問題
* SITES-21980：對 UUID 型的參考類型的處理不一致。
* SITES-7257：ThumbnailServlet 中的 NPE。

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
