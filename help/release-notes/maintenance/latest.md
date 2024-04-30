---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 71%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15977 版本 {#release-15977}

下面是 15977 維護版本持續改善內容的摘要；該版本於 2024 年 4 月 19 日公開發行。上一個維護版本是版本 15939。

2024.4.0 功能啟用可提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-15977}

* GRANITE-51335：最佳化 AEM 健康情況檢查以提高執行個體穩定性。

### 已修正的問題 {#fixed-issues-15977}

* CQ-4357226：已修正 IMS 設定對 OAuth 憑證的支援迴歸問題。
* GRANITE-51335：速率限制升級到 5.0.4 已修正 Felix 健康情況檢查註冊。

### 已知問題 {#known-issues-15977}

* **(僅適用於 AEM Forms)** 安裝 AEM Cloud Foundation 維護版本 15977 後，最適化表單欄位在表單製作期間和已發佈表單以錯誤順序呈現。如果您使用AEM Forms，Adobe建議您等到在即將推出的維護版本中解決問題後，再升級至15977版本。 這麼做可協助您避免任何不便。

### 已過時的功能和 API {#deprecated-15977}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 自2024年5月1日起，Adobe Dynamic Media將停止支援下列專案：

   * SSL （安全通訊端層） 2.0
   * SSL 3.0
   * TLS （傳輸層安全性） 1.0和1.1
   * TLS 1.2中的下列弱加密：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


若要瞭解AEMas a Cloud Service已棄用或移除的內容，請參閱 [過時和移除的功能和API](/help/release-notes/deprecated-removed-features.md).

### 內嵌技術 {#embedded-tech-15977}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.6 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
