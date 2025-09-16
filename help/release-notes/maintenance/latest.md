---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 23%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 發行說22450 {#22450}

以下摘要說明維護版本22450數的持續改善，該版本於2025年9月16日公開發佈。 前一個維護版本是版本 22171。

啟用 2025.9.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能 {#new-features-22450}

* SITES-32595：現在可以識別已完成且已略過或拒絕片段的工作流程。 工作流程API回應中提供新屬性，列出因無效或參考無效而被排除的片段。
* SITES-33642：現在會產生新的API事件，並用於修改的內容片段。
* SITES-33320：現在可以透過搜尋API使用其`technicalName`來搜尋內容片段模型。

### 增強功能 {#enhancements-22450}

* SITES-34023：已將`technicalName`欄位新增至內容片段模型端點的回應，以便更好地識別。
* SITES-32766：內容片段模型中的內容資產參考現在支援較廣泛的二進位檔案型別。
* SITES-33974：改進OpenAPI說明檔案，使其更精確且更方便使用。
* SITES-9173：快取`ContentPolicyStatus`。
* SITES-9290：改善`TouchEditContext`的快取。
* SITES-33355：在工作流程主控台的「檢視裝載」上開啟新的CF編輯器。
* SITES-33356：在建立CF上開啟新的CF編輯器→在觸控式UI管理UI中開啟。
* SITES-32952：使用傳送API時，CFM欄位的預設值處理不一致。
* SITES-31539：使用通用編輯器的Edge Delivery：在`head.html`中新增對通用編輯器設定中繼標籤的支援。
* SITES-20672：使用通用編輯器的Edge Delivery：新增對製作中其他大量中繼資料試算表的支援。
* SITES-32963：使用Universal Editor的Edge Delivery：為最佳化目標、自動分配和自我學習新增實驗中繼資料。
* SITES-30847：核心元件 2.30.0 版。
* SITES-29617： referencedBy端點已更新為使用ReferenceSearch類別，改善其效能和可靠性。
* SITES-19308：透過最佳化參考驗證步驟來增強頁面刪除流程的效能。
* SITES-34293：對樣板化資源實作延遲載入，以改善效能。
* SITES-33892：新增功能切換，以略過偽頁面的參照檢查，藉此改善效能。

### 已修正的問題 {#fixed-issues-22450}

* CQ-4360550：修正AEM雲端服務中回覆頁面移動後語言副本意外消失的問題。
* SITES-25232：設定日期和退出時間扭曲連結沒有可見的焦點指標。
* SITES-25258：焦點不是透過刪除註解模型對話方塊來管理。
* SITES-25305：「人口統計」工具列不會以邏輯順序接收焦點。
* SITES-25366：熒幕助讀程式不會宣佈Teaser強制回應視窗的載入狀態。
* SITES-34276：使用通用編輯器的Edge Delivery：修正未套用至發佈層的自動建立CORS原則。
* SITES-34811：使用通用編輯器的Edge Delivery：修正hlx選擇器未新增到製作時試算表連結的問題。
* SITES-31669：工具>網站>啟動中的未當地語系化字串「此頁面重新導向至」。
* SITES-30879： 「網站>頁面編輯器>搜尋元件」中的未當地語系化字串。
* SITES-30959：頁面編輯器>影像元件中未本地化的字串。
* SITES-21743：未當地語系化「請選取要顯示的檔案」。 「頁面編輯器> PDF檢視器」中的字串
* SITES-19785：字串在核心元件網站>索引標籤中未本地化。
* SITES-22059：核心元件網站> PDF檢視器中的未當地語系化「檔案預覽無法使用」字串。
* SITES-33360：作業期間發生未當地語系化的「錯誤」。 提供的路徑不是「啟動>編輯」中的「啟動」字串。
* SITES-32975： 「Headless UI >啟動>比較啟動與Source」中的未本地化日期格式。
* SITES-32973：Headless UI > Launches > Rebase中的硬式編碼字串。
* SITES-13540：「啟動>促銷活動」中未本地化的字串。
* SITES-13085： 「網站>啟動項建立頁面」中的未當地語系化錯誤字串。
* SITES-21499：未本地化的字串是「網站>啟動>編輯」。
* SITES-14961：在「網站>屬性> Blueprint >轉出」對話方塊中截斷日期欄位。
* SITES-33764：啟動篩選器(Source路徑/工作流程建立的啟動)無法運作。
* SITES-33884：「提升目前頁面和子頁面」會無意中提升超出範圍的頁面。
* SITES-33611：即時副本概覽不適用於高流量市場。
* SITES-34331：載入非管理員使用者的轉出覆蓋時逾時503。
* SITES-34403：關機期間`NullPointerException`中的`GraphqlClientImpl deactivate()`。
* SITES-33817：解決UI結構描述和JCR模型之間的同步問題以確保一致性。
* SITES-31141：路徑未代表的內容參考現在會在API回應中正確傳回。
* SITES-34080：內容片段建立程式現在更健全，如果沒有欄位提供給請求，也不會失敗。
* SITES-30773：使用「尋找和取代」尋找字詞的規則運算式已改善，以正確比對UTF-8字元。
* SITES-33742：解決使用工作流程API時無法成功移動內容片段的錯誤。

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
