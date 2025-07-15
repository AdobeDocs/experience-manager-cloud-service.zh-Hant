---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5d00bed4008c70e81f3a70d219ddc411ec8bdc59
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 94%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21484 {#21484}

以下摘要說明維護版本 21484 的持續改善內容；此版本已於 2025 年 7 月 10 日公開發佈。前一個維護版本為版本 21331。

啟用 2025.7.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21484}

無。

### 已修正的問題 {#fixed-issues-21484}

無。

#### AEM Guides {#guides-21484}

* GUIDES-29781：在來源檢視中的元素內新增 XML 註解時，該註解前後的空格會在切換檢視畫面時遺失。
* GUIDES-29078：瀏覽器重新整理後，在「作者」檢視中開啟主題時，不會保留「檔案屬性」面板中先前套用的標籤，且新增標籤時會覆寫現有標籤，尤其是有大量標籤可供選取時。
* GUIDES-28214：因為未建立檢閱節點，嘗試透過 AEM 工作流程建立檢閱任務持續失敗。
* GUIDES-28104：發佈具有 `chunk=to-content` 屬性的 DITA 對應時，會在新的 AEM Sites 輸出中建立重複的 JCR 節點，導致 AEM Sites 中有多餘的內容結構。
* GUIDES-29065、GUIDES-28793：處理大型集合時，觀察到載入時間較長和間歇性逾時等效能問題。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-21484}

* 軟體發佈入口網站中提供之SDK在本機執行時發生問題。 請繼續使用先前的SDK進行本機測試。

### 已過時的功能和 API {#deprecated-21484}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21484}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 5 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21484}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
