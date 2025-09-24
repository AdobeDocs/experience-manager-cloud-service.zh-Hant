---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: ht
source-wordcount: '902'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 22450 版 {#22450}

以下摘要說明 22450 維護版本的持續改善內容，該版本於 2025 年 9 月 16 日公開發佈。前一個維護版本是 22171 版。

啟用 2025.9.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能 {#new-features-22450}

* SITES-32595：現在可以識別工作流程完成時曾略過或拒絕的片段。工作流程 API 回應中提供新屬性，列出因無效或具有無效參照而被排除的片段。
* SITES-33642：現在會產生新的 API 事件，並用於修改的內容片段。
* SITES-33320：現在可透過搜尋 API，使用 `technicalName` 來搜尋內容片段模型。

### 增強功能 {#enhancements-22450}

* SITES-34023：已將 `technicalName` 欄位新增至內容片段模型端點的回應，以便更有效識別。
* SITES-32766：內容片段模型中的內容資產參照現已支援較廣泛的二進位檔案類型。
* SITES-33974：改進 OpenAPI 檔案，使其更精確且更方便使用。
* SITES-9173：快取 `ContentPolicyStatus`。
* SITES-9290：改善 `TouchEditContext` 的快取。
* SITES-33355：在工作流程主控台的「檢視承載」上開啟新的 CF 編輯器。
* SITES-33356：在建立 CF 上開啟新的 CF 編輯器 → 在觸控式 UI 管理員 UI 中開啟。
* SITES-32952：使用傳送 API 時，CFM 欄位的預設值處理不一致。
* SITES-31539：使用通用編輯器的 Edge Delivery：在 `head.html` 新增對通用編輯器設定中繼標記的支援。
* SITES-20672：使用通用編輯器的 Edge Delivery：新增對製作中其他大量後設資料試算表的支援。
* SITES-32963：使用通用編輯器的 Edge Delivery：為最佳化目標、自動分配和自我學習，新增實驗用後設資料。
* SITES-30847：核心元件 2.30.0 版。
* SITES-29617：referencedBy 端點已更新為使用 ReferenceSearch 類別，改善其效能和可靠性。
* SITES-19308：透過最佳化參照驗證步驟來增強頁面刪除流程的效能。
* SITES-34293：對範本化資源實施延遲載入以改善效能。
* SITES-33892：新增功能切換，以略過偽頁面的參照檢查，藉此改善效能。

### 已修正的問題 {#fixed-issues-22450}

* CQ-4360550：修正 AEM Cloud Service 中恢復頁面移動後語言副本意外消失的問題。
* SITES-25232：設定日期和退出時間扭曲連結沒有可見的焦點指標。
* SITES-25258：焦點不是透過刪除註解模態對話框來管理。
* SITES-25305：人口統計工具列不會以邏輯順序接收焦點。
* SITES-25366：螢幕閱讀器未宣佈 Teaser 模態的載入狀態。
* SITES-34276：使用通用編輯器的 Edge Delivery：修正未套用至發佈階層的自動建立 CORS 原則。
* SITES-34811：使用通用編輯器的 Edge Delivery：修正製作時 hlx 選擇器未新增到試算表連結的問題。
* SITES-31669：工具 > Sites > 啟動中的字串「此頁面重新導向至」未本地化。
* SITES-30879：Sites > 頁面編輯器 > 搜尋元件中的字串未本地化。
* SITES-30959：頁面編輯器 > 影像元件中的字串未本地化。
* SITES-21743：頁面編輯器 > PDF 檢視器中的「請選取要顯示的文件。」字串未本地化
* SITES-19785：核心元件網站 > 索引標籤中的字串未本地化。
* SITES-22059：核心元件網站 > PDF 檢視器中的「檔案預覽無法使用」字串未本地化。
* SITES-33360：啟動 > 編輯中「作業期間發生錯誤。提供的路徑不是啟動。」字串未本地化。
* SITES-32975：Headless UI > 啟動 > 比較啟動與來源中的日期格式未本地化。
* SITES-32973：Headless UI > 啟動 > 重定基底中的字串使用硬式編碼。
* SITES-13540：啟動 > 促銷活動中的字串未本地化。
* SITES-13085：Sites > 啟動建立頁面中的錯誤字串未本地化。
* SITES-21499：Sites > 啟動 > 編輯中的字串未本地化。
* SITES-14961：Sites > 屬性 > Blueprint > 轉出對話框中的日期欄位截斷。
* SITES-33764：啟動篩選器 (來源路徑/工作流程建立的啟動) 無法運作。
* SITES-33884：「行銷目前頁面和子頁面」會無意中行銷超出範圍的頁面。
* SITES-33611：Live Copy 概觀不適用於高流量市場。
* SITES-34331：載入非管理員使用者的轉出覆蓋時出現 503 逾時。
* SITES-34403：關機期間 `GraphqlClientImpl deactivate()` 中的 `NullPointerException`。
* SITES-33817：解決 UI 結構描述和 JCR 模型之間的同步問題以確保一致性。
* SITES-31141：路徑未代表的內容參照現在會在 API 回應中正確傳回。
* SITES-34080：內容片段建立流程現在更健全，且如果沒有欄位提供給請求，也不會失敗。
* SITES-30773：使用「尋找和取代」尋找字詞的規則運算式已改善，以正確符合 UTF-8 字元。
* SITES-33742：解決使用工作流程 API 時無法成功移動內容片段的錯誤。

### 已知問題 {#known-issues-22450}

無。

### 已過時的功能和 API {#deprecated-22450}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-22450}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 18 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-22450}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
