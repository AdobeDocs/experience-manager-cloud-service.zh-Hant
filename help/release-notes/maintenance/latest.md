---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 30b5d5838087a35a457939cdbaa13c5735df144e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 49%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 19823 {#19823}

以下摘要說明維護版本19823數的持續改善，該版本於2025年3月4日公開發佈。 前一個維護版本是版本 19687。

啟用 2025.3.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-19823}

* Assets-46491：用於資產處理狀態變更的OSGI事件處理常式。
* Assets-45613：刪除或移動資產時傳送取消發佈事件。
* Assets-45131： Content Hub中的自訂標籤屬性支援。

### 已修正的問題 {#fixed-issues-19823}

* Assets-20433：受密碼保護的PDF出現Dynamic Media擷取問題。
* Assets-24675：僅色票影像設定檔未顯示影像處理選項。
* Assets-41257：資產版本比較會顯示不正確的外觀比例。 資產版本在時間軸中以不正確的順序顯示。
* Assets-44894： Assets檢視書籤可能無法點選。
* Assets-45015：如果找不到智慧型裁切資產控制點，智慧型裁切寬度和高度會設為零。
* Assets-45192：減少脈衝要求頻率。
* Assets-45724：如果未指派上傳工作，請確保DM上傳已重試。
* Assets-46425： Adobe Stock整合搜尋問題。
* Assets-27400：資料夾預覽產生器可能會嘗試開啟原始檔案。
* CQ-4358722：在Java 11和Java 17中處理不同的地區設定代碼。
* SITES-29369：資產啟用/停用時觸發的頁面發佈/取消發佈事件。
* SITES-24074：修正Unified Shell下的鍵盤協助工具。
* SITES-28058：Assets資料夾標題未轉存至即時副本。

### 已知問題 {#known-issues-19823}

無。

### 已過時的功能和 API {#deprecated-19823}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-19823}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 6 個已確認的漏洞，從而強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-19823}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
