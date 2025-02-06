---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f7aa50d8a2fa80489c56571caa9a75bc50715368
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 20%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 19352 {#19352}

以下摘要說明維護版本19352數的持續改善，該版本於2025年2月5日公開發佈。 前一個維護版本是版本 19149。

2025.2.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-19352}

* Forms-13998：新增摺疊式功能表元件。
* Forms-17913：新增無線電群組的卡片變體。
* Forms-17333：在AEM表單提交中啟用HTML電子郵件範本。
* Forms-17702：啟用將Output Sync API中產生的PDF上傳至Azure Blob儲存體。
* SITES-28282：使用通用編輯器的Edge Delivery：提供基本路徑、網站名稱和組織，作為任何頁面的頁面資訊。
* SITES-27055：使用通用編輯器的Edge Delivery：支援反向Proxy servlet中的查詢引數。
* SITES-26796：使用通用編輯器的Edge Delivery：支援分類試算表的自訂欄。
* SITES-26087：使用通用編輯器的Edge Delivery：支援試算表的CSV匯出。
* SITES-26265：使用通用編輯器的Edge Delivery：顯示要在設定UI中與Edge Delivery整合的TA帳戶。
* SITES-20372：使用通用編輯器的Edge Delivery：啟用試算表的基本MSM使用案例。
* SITES-26681：使用通用編輯器的Edge Delivery：支援作者上分類試算表的？sheet=引數。
* SITES-26479： [結構描述]內容片段模型排程發佈狀態端點。
* SITES-25944： [即時副本概觀]新增狀態「即時副本為最新且繼承受限」。
* SITES-28713： [V2]新增結構化資料支援至內容刮刀。
* SITES-27896：在通知時自動開啟CommentsTab。
* SITES-26720：不應允許使用者從資產選擇器中選擇整個集合。
* SITES-27875：預設可移動容器內的任何可編輯專案。
* SITES-28340：Dark Alley通用編輯器服務外掛程式。
* SITES-26098：在發佈Content-Fragment時避免發佈參考頁面的可能性。
* SITES-27789：在DOM中支援資料屬性data-aue-component。
* SITES-25997：增強變數以支援修改日期。
* SITES-28023：遠端資產參考的GraphQL輸出（存放庫+資產ID）。
* SITES-26058：內容片段模型已排程發佈狀態端點。
* SITES-25108：UUID參考的模型移轉。
* SITES-26630：多個內容片段的內容片段已排程發佈狀態端點。
* SITES-23432：改善刪除參考功能。
* SITES-25797：支援外部資產參考 — GraphQL。
* SITES-17514：刪除端點增強功能以取消發佈Content-Fragment。
* SITES-14633：安裝前驗證內容片段模型建立裝載 — 試執行。

### 已修正的問題 {#fixed-issues-19352}

* SITES-28415：使用通用編輯器的Edge Delivery：修正試算表的「開啟屬性」按鈕。
* SITES-26669：使用通用編輯器的Edge Delivery：修正以試算表BOM上傳以UTF-8編碼的CSV檔案時的問題。
* SITES-26543：使用通用編輯器的Edge Delivery：修正沒有模型呈現錯誤標籤的空白區塊。
* SITES-26857：使用通用編輯器的Edge Delivery：針對檔案型設定，修正UI中顯示的網站驗證權杖。
* SITES-26662：使用通用編輯器的Edge Delivery：修正區分大小寫的大量中繼資料的問題。
* SITES-28133： Publish若設為「預覽」，導致內容可用於生產環境。
* SITES-27187：排程的頁面/資產啟用，包括參考（實驗）未命中發佈參考。
* SITES-27264： 2個與Content-Fragment-LiveCopy-Creation相關的Selenium測試在主版上一致失敗。
* SITES-26559：將內容片段模型的查詢釘選到cqPageLucene索引。
* SITES-24469：無法透過鍵盤存取互動式元素。
* SITES-24518：「父參照」表格中的「名稱」和「模型」按鈕無法使用鍵盤。
* SITES-27937：更新模型後，UISchema限制會設定為null。
* SITES-27852：模型UISchema缺少分類。
* SITES-27904：完整投影的清單/搜尋內容片段模型中缺少MetadataSchema。
* SITES-26827：列出片段最後會進入無限回圈。
* SITES-27678： [效能]防止不必要擷取_references。
* SITES-27589：具有多個內容/片段參考欄位的內容片段模型的UUID升級失敗。
* SITES-26679：取消發佈內容片段模型應僅驗證已發佈的引用。
* SITES-26666：referencesTree和參照端點傳回不同的結果。
* SITES-26499：標籤欄位值在GET片段中的順序錯誤，且PATCH會隨機排列順序。
* SITES-26585：修正結構描述中的小型說明錯誤。
* SITES-26647：非管理員使用者的刪除端點和UnpublishFragments參考驗證可能會失敗。
* SITES-26458： [搜尋內容片段模型]依復寫狀態修正篩選。
* SITES-23513： [Content-Fragment Model Editor] 「Fragment Reference」 — 「Allowed Content Fragment Model」屬性的驗證失敗。
* SITES-26575：從預覽中取消發佈片段應該會更新previewStatus。
* SITES-26571：啟用FT_SITES-12435時無法儲存頁面參考。
* SITES-26660：當@ContentType為「字串」型別時，內容片段版本比較可能會中斷。
* SITES-26626：數字和布林值欄位上缺少customErrorMessage。
* SITES-26268：如果在建立片段時參考無效，則會傳回錯誤的狀態代碼。
* Forms-18098、FORMS-17954：最適化Forms無法在Microsoft Edge瀏覽器的Internet Explorer模式中載入。
* Forms-17162：發佈資產會導致執行OOTB查詢，進而降低發佈效能。

### 已知問題 {#known-issues-19352}

無。

### 已過時的功能和 API {#deprecated-19352}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-19352}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 36 個已確認的漏洞，從而強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-19352}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
