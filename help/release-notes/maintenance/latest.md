---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 46%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 20476 {#20476}

以下摘要說明維護版本20476數的持續改善，該版本於2025年4月15日公開發佈。 前一個維護版本是版本 20133。

啟用 2025.4.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-20476}

* CNTBF-411：新增刪除sling作業的可能性，以防JCR捨棄該作業。
* CQ-4359813： AEM翻譯套件：3月20日。
* CQ-4359811：Granite翻譯套件：3月20日。
* GRANITE-57863：更新 Filevault 至 3.8.4 版。
* GRANITE-56154：在oak-segment-azure中設定指數重試。
* GRANITE-55999：改善UserPropertiesService的效能。
* GRANITE-55781：避免重複重新設定使用者成員資格。
* GRANITE-53956：將Azure SDK V8升級為V12，以使用oak-segment-azure。
* GRANITE-50654：在主參與者許可權索引標籤上，移除預設在前端載入的「所有人」。
* SKYOPS-103444：更新至 Sling ResourceResolver 1.12.6。
* SKYOPS-101147：更新Caconfig實作。
* SKYOPS-97124：為過期版本的SPIFly套件組合新增分析器警告。
* SKYOPS-95826：將執行階段Java版本更新為11.0.26和21.0.6。
* SKYOPS-53671：在(RDE) AEM重新啟動時，使用功能模型中的客戶安裝成品。

### 已修正的問題 {#fixed-issues-20476}

* Assets-49027： [回歸] AemRequestEventFilter中斷對OSGI Web主控台的POST要求。
* Assets-44956：無法選取任何Dynamic Media轉譯 — 指令碼標籤應載入頂層元件。
* CNTBF-410： ContentCopy套件組合中的CheckJob getId null指標。
* CNTBF-341： ContentCopy匯出索引超出界限。
* CQ-4355411：工具提示仍顯示在「使用者偏好設定」對話方塊中。
* GRANITE-57265：未選取下拉式清單選擇值。
* GRANITE-57067 - UI上缺少有效原則。
* SITES-30727：在 AEM 編輯器內，子元件拖放可能會失敗。
* SKYOPS-90607：Sling作業會在非使用中部署/可變內容中執行。
* SKYOPS-95722：從AEM-SDK中的快速入門標幟中移除`MaxPermSize`大小。
* SKYOPS-103569：某些影像無法以Java 21載入： `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`。

### 已知問題 {#known-issues-20476}

無。

### 已過時的功能和 API {#deprecated-20476}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-20476}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 5 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-20476}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.28.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
