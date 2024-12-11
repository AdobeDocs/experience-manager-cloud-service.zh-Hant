---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 33%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18751 {#18751}

以下摘要說明維護版本18751數的持續改善，該版本於2024年12月11日公開發佈。 前一個維護版本是版本 18598。

2025.1.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18751}

* SKYOPS-88509：AEM SDK的Java 21支援。

### 已修正的問題 {#fixed-issues-18751}

* Assets-42802： MFE上的「上一步」按鈕永遠無法運作，且會顯示額外的對話方塊。
* Assets-44148：修正AEM中的NODE_MOVED事件可能導致NPE。
* Assets-44418：未在Skyline上設定修正的環境。
* Assets-44821：修正更新事件篩選器，針對上傳事件納入表單URL編碼資料。
* CNTBF-298：固定內容複製因UUID衝突而失敗。
* CNTBF-331： [content-copy-bundle]版本2.0.14。
* Forms-16572：移除Java 21 SDK組建的工作流程測試失敗。
* GRANITE-36205：QS內部Oak版本的自動更新。
* GRANITE-53704：重新評估存放庫服務上的Sling探索。
* GRANITE-54300：更新 Oak 至最新的公開版本 (1.70.0)。
* GRANITE-54416：更新 Filevault 至 3.8.2 版。
* GRANITE-54462：設定SubscriberAgents以使用「systemready」的hc.tags。
* GRANITE-54542：將commons-io相依性更新為2.17.0。
* GRANITE-54658：在QS中為fullGC新增delayFactor和批次大小OSGi設定。
* GRANITE-54696：加寬Jackrabbit API的匯入範圍。
* GRANITE-54803：當imsauth作用中時，在AEM中停用ClusterAtExchange。
* GRANITE-55095：更新 Oak 至最新的公開版本 (1.72.0)。
* GUIDES-20006：在儲存新版本之前，標籤為「完成」的檔案狀態會回復到「草稿」，導致「完成」狀態不會持續在任何檔案版本中。
* GUIDES-21840：在原生PDF輸出中，目錄中有章節標題遺失，導致階層不正確。
* GUIDES-19558：如果基線具有大量主題或地圖，請在1分鐘後編輯並在雲端設定上儲存基線，如此將會逾時。
* GUIDES-19733：使用基準線的對映轉譯會變慢，最終無法載入所有關聯主題和對映檔案的清單。
* SITES-26798：「啟動自動促銷」未更新「促銷狀態（促銷日期）」。
* SITES-27137：從MSM核心移除Sling Commons量度相依性。
* SKYOPS-75446：修正AEM有時會傳回404或遺失內容的頁面。
* SKYOPS-76366：AEM發行說15977和更新版本中沒有Jetty Threadpool量度。
* SKYOPS-82371： java.io.IOException： classFile.delete()失敗。
* SKYOPS-83369：如果轉換工作執行未產生組合，AEM部署將無法啟動。
* SKYOPS-83910：修正SKYOPS-82371中發現的並行問題。
* SKYOPS-84821：將Sling主要Servlet的sling.include.checkcontenttype設定設為true。
* SKYOPS-85798：固定轉換作業會產生空的索引定義。
* SKYOPS-86251：升級至AEM Analyzer核心1.5.6，並在轉換工作中啟用產品套件匯入分析器。
* SKYOPS-86710：移除Java 21 sdk組建的最小測試失敗。
* SKYOPS-86745：Sling ResourceResolver 1.12.2的更新。
* SKYOPS-89616：修正無法在Adobe Developer Console中建立技術帳戶的問題。
* SKYOPS-89691：修正用於ASM警告的不正確成品ID。
* SKYOPS-89699：遺漏內嵌在Groovy主控台「orbinson」風格中的舊Groovy版本警告。
* SKYOPS-88664：記錄並保護已下載地圖檔案行超過1024限制的情況。
* SKYOPS-89734：發行Dispatcher image 2.0.235。

如需更多有關 Experience Manager Guides 中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 版本藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-18751}

無。

### 已過時的功能和 API {#deprecated-18751}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-18751}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 3 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18751}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
