---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 45%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 19567 {#19567}

以下摘要說明維護版本19567數的持續改善，該版本於2025年2月18日公開發佈。 前一個維護版本是版本 19352。

2025.2.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-19567}

* GRANITE-56650：內容發佈應僅在重試幾次後訊號已封鎖的佇列
* SKYOPS-89616：允許在Adobe Developer Console中建立最多40個技術帳戶

### 已修正的問題 {#fixed-issues-19567}

* CNTBF-232：深層套件nt：file節點，包含強制的jcr：content子項
* CQ-4358930：具有多個欄位的頁面屬性載入期間的效能問題
* GRANITE-55960： AEM as Cloud Service上Coral選取欄位的效能問題
* GRANITE-56197：新的TreeActivation工作流程步驟不會批次處理大型平面資料夾結構中的資產

#### AEM 指南 {#guides}

* GUIDES-23526：從資料夾設定檔更新條件時，所有條件群組都會遺失，條件會平面化。
* GUIDES-22574：如果外部連結包含UUID，它會進行後期處理，並將外部連結轉換為UUID連結，因此在編輯器和發佈網站上都會中斷連結。
* GUIDES-24983：從任何外部產品（例如MS PowerPoint）複製影像並將其貼上到Guides時，即時上傳資產以用於檔案的功能會中斷。
* GUIDES-21772：產生&#x200B;**區塊屬性**&#x200B;設為&#x200B;**to-content**&#x200B;之內容的原生PDF失敗。
* GUIDES-23964：選擇&#x200B;**編輯屬性**&#x200B;時，基準對話方塊不會顯示先前儲存的動態基準條件。
* GUIDES-19067：複製任何資料夾設定檔時，也會從原始資料夾設定檔複製其管理員使用者清單

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-19567}

無。

### 已過時的功能和 API {#deprecated-19567}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-19567}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 21 個已確認的漏洞，從而強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-19567}

| 技術 | 版本 | 連結 |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
