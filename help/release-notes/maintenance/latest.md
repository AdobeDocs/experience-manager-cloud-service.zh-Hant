---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 20476 {#20476}

下面是 20476 維護版本持續改善內容的摘要；該版本於 2025 年 4 月 15 日公開發行。前一個維護版本是版本 20133。

啟用 2025.4.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-20476}

* CNTBF-411：在 JCR 捨棄 Sling 作業的情況下，新增刪除該作業的可能性。
* CQ-4359813：AEM 翻譯套件：3 月 20 日。
* CQ-4359811：Granite 翻譯套件：3 月 20 日。
* GRANITE-57863：更新 Filevault 至 3.8.4 版。
* GRANITE-56154：在 oak-segment-azure 中設定指數型重試。
* GRANITE-55999：提升 UserPropertiesService 的效能。
* GRANITE-55781：避免對使用者會籍進行冗餘重新設定。
* GRANITE-53956：將 oak-segment-azure 的 Azure SDK V8 升級至 V12。
* GRANITE-50654：在主體權限標籤上，預設刪除前端的「所有人」負載。
* SKYOPS-103444：更新至 Sling ResourceResolver 1.12.6。
* SKYOPS-101147：更新 caconfig 實作。
* SKYOPS-97124：針對 SPIFly 套件的過時版本新增分析器警告。
* SKYOPS-95826：將執行階段 Java 版本更新至 11.0.26 和 21.0.6。
* SKYOPS-53671：在 (RDE) AEM 重新啟動時使用客戶安裝的功能模型成品。

### 已修正的問題 {#fixed-issues-20476}

* ASSETS-49027：[迴歸] AemRequestEventFilter 會中斷對 OSGI 網頁主控台的 POST 要求。
* ASSETS-44956：無法選取任何 Dynamic Media 轉譯 - 指令碼標籤應載入到頂層元件。
* CNTBF-410：ContentCopy 套件中的 CheckJob getId 空指標。
* CNTBF-341：ContentCopy 匯出索引超出範圍。
* CQ-4355411：工具提示仍顯示在「使用者偏好設定」對話框中。
* GRANITE-57265：下拉選單中的值未選取。
* GRANITE-57067 - UI 中缺少有效的原則。
* SITES-30727：在 AEM 編輯器內，子元件拖放可能會失敗。
* SKYOPS-90607：Sling 作業在非使用中部署/可變內容中執行。
* SKYOPS-95722：移除 AEM-SDK 中 quickstart 標幟的 `MaxPermSize` 大小。
* SKYOPS-103569：某些影像無法使用 Java 21 載入：`javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`。

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
