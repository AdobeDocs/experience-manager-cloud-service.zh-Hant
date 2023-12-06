---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 2677e8fbdf6b21ce2d1d848000401c826bc5f289
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 37%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 14538 版 {#release-14538}

以下摘要說明維護版本14538數的持續改善，該版本於2023年12月6日公開發佈。 此維護版本是先前 14227 維護版本的更新。

2023.12.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-14538}

* GRANITE-46723：使用者同步 — SAML從預設同步移轉至IDP型同步。
* OAK-10311：複製 — 最佳化Blob比較，以縮短AEM中大量資產的複製時間。
* OAK-10511：復寫 — 減少網路來回次數，以縮短AEM中大型資產的復寫時間。
* GRANITE-48334： Publishers - RUM缺少集合指令碼。

### 已修正的問題 {#fixed-issues-14538}

* CQ-4354867： ToggleCondition參考參考InstanceActionServlet中不存在的欄位。
* CQ-4349948：在「工具」→「安全性→使用者」下的「編輯使用者設定」中，將「設定檔屬性」字串本地化。
* GRANITE-44541：在「工具」>「安全性」>「使用者」底下，將「編輯使用者」>「金鑰存放區」的「私密金鑰檔案」畫面新增→錯誤對話方塊本地化→
* GRANITE-45341：在「工具」→「安全性→使用者」底下，本地化「啟用/停用使用者」動作的成功/失敗字串。
* GRANITE-46650：錯誤訊息「使用者ID/密碼不符」的本地化。 「工具→安全性」→「使用者建立」對話方塊下的字串。
* GRANITE-47764：更新至Sling模型API 1.5.0：插入至Sling模型中的靜態變數將會導致編譯錯誤(SLING-11507)。
* GRANITE-48452：傳送狀態碼為200的空白clientlibs。
* GRANITE-48410： ResourceResolver未關閉。
* ASSETS-31297：防止從Dynamic Media刪除複製的資產。
* ASSETS-30811：區塊標籤服務繫結的參考更新。
* GRANITE-46418：更新AEM中的Sling事件： GaugeSupport在registerWithSuffix中有無限遞回(SLING-11918)。

### 已知問題 {#known-issues-14538}

無。

### 內嵌技術 {#embedded-tech-14538}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.58-T20231123092841-619e1bd | [Oak API 1.58.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
