---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a091dd6b1b69d77f9eeb50065e8946af0133f4f9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 39%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 19149 {#19149}

以下摘要說明維護版本19149數的持續改善，該版本於2025年1月21日公開發佈。 前一個維護版本是版本 18751。

2025.1.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-19149}

* Assets-45286：顯示下載封存非同步工作的精細進度。
* Assets-46296：資產選擇器支援Dynamic Media範本。
* Assets-44796：為DAM非同步資產作業引發Assets事件。

### 已修正的問題 {#fixed-issues-19149}

* GRANITE-55074：確保在錯誤回應上設定CORS回應標題。
* Assets-43755：改善大量資產的相關擴充性。
* Assets-45399：建立資產即時副本後，重新導向至Assets主控台。
* Assets-45462：自訂資料夾縮圖出現瀏覽器快取問題。
* Assets-46398：隱藏DM範本的下載和重新處理動作。
* Assets-44484：重新儲存連線Assets設定時發生問題。
* Assets-44122：非同步複製資產作業在複製到目前資料夾時不會重新命名目的地資料夾。
* Assets-44463：成功匯出中繼資料時，「下載CSV」按鈕不可見。
* Assets-45134：以目的地標題移動工作會覆寫所有資料夾標題。
* Assets-45137：與透過Assets檢視的大量上傳衝突。
* Assets-45758：資產關係在新增關係後獲得無窮多的忙碌/載入動畫。
* Assets-44148： AEM中的NODE_MOVED事件可能會導致記錄中出現假的NPE。
* Assets-28607：設定自訂視訊縮圖時出現JS錯誤。
* GRANITE-55781：改善Adobe Developer Console與AEM之間的群組同步。 [使用者群組和產品設定檔同步處理中的變更](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)中有更多詳細資料。
* GRANITE-55754：確保SDK啟動指令碼支援Java 21。
* GRANITE-54248：無法捲動大型資產資料夾中的所有專案。
* SCRNS-4597：搜尋結果清單檢視改進。


### 已知問題 {#known-issues-19149}

無。

### 已過時的功能和 API {#deprecated-19149}

使用Adobe Admin Console進行許可權管理時，下列群組不得使用，因為系統將不再將它們與AEM同步：
* 以_GROUP_NAME_SUFFIX結尾的AEM群組。
* 來自其他環境、計畫或產品的產品設定檔。

如需詳細資訊，請檢查使用者群組與產品設定檔同步中的[變更](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)。


[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-19149}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 4 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-19149}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
