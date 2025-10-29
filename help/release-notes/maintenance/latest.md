---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d081b468e42306c56238bee6117d92c6afd48d4
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 23%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 23122 版 {#23122}

以下摘要說明維護版本23122數的持續改善，該版本於2025年10月29日公開發佈。 前一個維護版本是 22943 版。

啟用 2025.11.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-23122}

* Forms-21594：為內容作者啟用互動式通訊範本內容與版面配置鎖定功能。
* Forms-20385：支援在互動式通訊編輯器中進行XDP編輯。
* Forms-10883：支援JSON搭配DoR產生中的XHTML名稱空間標籤，以確保準確轉譯透過API提交的RTF資料。
* Forms-21751：畫布功能 — 文字溢位，分頁的UI。
* Forms-22049：互動式通訊編輯器 — 移轉至Spectrum 2。
* Forms-22050：支援互動式通訊編輯器中的動態頁面編號。
* Forms-21606：互動式通訊的公用OSGi轉譯SPI。
* Forms-21613：轉譯器互動式通訊SPI的交易報表和效能記錄。
* SITES-35092：內容片段 — 語意搜尋的新mixin和升級程式。
* SITES-32319：傳送OpenAPI — 支援頁面參考。
* SITES-20123： GraphQL：支援JSON回應中的上標元素。
* SITES-34744：內容片段回應中新的「卡片」屬性，包含可用於呈現縮圖的資料。
* SITES-34571：允許列舉欄位為空。
* SITES-34812：新增使用值為「none」的「references」引數，擷取不含參考的內容片段的功能。
* SITES-35176：透過Touch UI簽出內容片段現在會防止其他使用者在新編輯器中編輯內容片段。
* SITES-30371：新增對uuid型參考欄位的支援。
* SITES-19309：開啟移動頁面精靈時，最多可擷取150個參考。
* SITES-32515：使用通用編輯器的Edge Delivery — 新增對多欄位和複合多欄位的支援（搶先存取）。
* SITES-33784：使用通用編輯器的Edge Delivery — 在頁面中繼資料中新增ld-json支援。
* SITES-34832：使用通用編輯器的Edge Delivery — 將頁面的公開路徑新增至頁面資訊servlet回應。
* SITES-25893：使用通用編輯器的Edge Delivery — 新增對強式字型的支援，並強調以區塊呈現文字。
* SITES-26158：使用通用編輯器的Edge Delivery — 新增對區塊和欄中表格標籤的支援（搶先存取）。
* SITES-27949：使用通用編輯器的Edge Delivery — 將路徑對應設為選用。

### 已修正的問題 {#fixed-issues-23122}

* CQ-4361144：修正翻譯工作中略過內容片段的問題。
* CQ-4355446：修正取消翻譯工作對話方塊中翻譯專案未本地化的字串。
* SITES-34555： GraphQL — 部署後出現QueryValidationError。
* SITES-35077：內容片段 — 由於錯誤的URL編碼，對帶有括弧的片段取消發佈失敗。
* SITES-35374：內容片段 — 已編輯的內容片段在導覽回到後面後會消失。
* SITES-36130： `EditorRestrictionsStatusImpl`中的NPE。
* SITES-35810： Launches中的NullPointerException區塊publishEdgeDeliverySubscriber佇列。
* SITES-34368： AEM CIF產生12個GraphQL別名，超過Magento 2.4.6-P12的10個限制。
* SITES-36193：CCS聯結器修正。
* SITES-35169：已解決當搜尋傳回無效的片段資源時，會導致錯誤分頁的問題。
* SITES-34574：修正內容片段搜尋API在某些情況下不會傳迴游標的問題。
* SITES-35520：修正嘗試發佈內容時，造成ClassCastException或逾時的問題。
* SITES-35210：修正嘗試使用空白參考篩選條件發佈中斷片段時會發生的NullPointerException。
* SITES-35933：修正會在內容片段發佈後觸發空白「啟用請求」工作流程的錯誤。
* SITES-35925：修正與修補內容片段模型相關的錯誤，這將從模型刪除「translatable」和「showThumbnail」屬性。
* SITES-35409：修正移動頁面時無法重新發佈已調整片段的錯誤。
* SITES-15757：修正無法在移動頁面時重新發佈已調整頁面的錯誤。
* SITES-34638：修正建立新版本時，不會納入祖父頁面屬性的錯誤。
* SITES-35071：當Omnisearch使用引號中的短語時，CSV匯出會傳回未篩選的結果。
* SITES-32182：使用通用編輯器的Edge Delivery — 修正包含已編碼請求引數的URL的編碼問題。
* SITES-34324：使用通用編輯器的Edge Delivery — 修正使用tel：通訊協定轉譯連結的問題。
* SITES-35333：使用通用編輯器的Edge Delivery — 修正頁面中繼資料中影像的資產轉譯選擇。
* SITES-35549：使用通用編輯器的Edge Delivery — 修正頁面中繼資料中的雙重編碼html實體。

### 已知問題 {#known-issues-23122}

無。

### 已過時的功能和 API {#deprecated-23122}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-23122}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 18 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-23122}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.2 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
