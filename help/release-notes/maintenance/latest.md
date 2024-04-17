---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 5e216e45a1400299efcc418007ddbe93f0c571a1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 35%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15939 版本 {#release-15939}

以下摘要說明維護版本15939數的持續改善，該版本於2024年4月17日公開發佈。 上一個維護版本是版本 15860。

2024.4.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)。

### 增強功能 {#enhancements-15939}

* GRANITE-39892：更新佇列大小限制的分佈並準備發佈。
* GRANITE-48777：將QS更新為com.adobe.granite.security.user-0.4.84完成。
* GRANITE-49421：已新增區段服務主體的屬性。
* GRANITE-49855：編寫功能模型分析器，在使用新commons.json的情況下，使Quickstart組建失敗。
* GRANITE-47995：允許切換cq：isDelivered的寫入。
* GRANITE-36205：將內部Oak發行版本更新至最新版本。
* GRANITE-50156為通用編輯器將AEMCS相似性繫結至IMS使用者ID。
* GRANITE-50556：將交叉通路套件組合升級至v0.1.18。
* GRANITE-50728：將FileVault更新至3.7.3-T20240308111857-81fa88f1。
* GRANITE-50957：將QS更新為com.adobe.granite.repository至1.8.114。
* GRANITE-50158：在YAML載入器中新增OAuth伺服器的伺服器認證流程支援。
* GRANITE-51327：將Oak更新至最新公開版本(1.62.0)。
* SKYOPS-68091將Java 11執行階段影像更新至3.0.0版。
* SKYOPS-70421：升級org.apache.sling.servlet-helpers套件組合
* SKYOPS-73483：允許在AEM上記錄Token。

### 已修正的問題 {#fixed-issues-15939}

* GRANITE-46901：將量度新增至訊息使用者端。
* GRANITE-48793：將QS更新為com.adobe.granite.crx-explorer-1.1.28。
* GRANITE-48937： Omniseaarch無法在aem/start.html頁面上運作。
* GRANITE-49638：修正RUM轉換器工廠的錯誤內容型別設定。
* GRANITE-50141： IMSProviderImpl正在傳送記錄檔。
* SITES-20949： Youtube新增referrerpolicy=&quot;strict-origin-when-cross-origin&quot;後，ComponentsIT.testEmbed失敗。
* SITES-21233：核心元件更新 — 升級至15860後，修正GS1US的Accordion。
* SKYOPS-74819： Apache Commons中重複金鑰的向後相容性中斷。
* SKYOPS-67087：Clientlib彙總在某些情況下無法運作。
* CQ-4355415： AEM通知連結在6.5 SP18中無法運作。

### 已知問題 {#known-issues-15939}

無。

### 已過時的功能和 API {#deprecated-15939}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」，了解 AEM as a Cloud Service 中已過時或已移除的功能。

### 內嵌技術 {#embedded-tech-15939}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20 - 1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.6 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
