---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90e92cfb15a6dfe5a8a474996f52c8a0c689f5e6
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 36%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21994 {#21994}

以下摘要說明維護版本21994數的持續改善，該版本於2025年8月19日公開發佈。 前一個維護版本是版本 21772。

啟用 2025.8.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能  {#new-features-21994}

無。

### 增強功能 {#enhancements-21994}

* GRANITE-53488：改善deleteconf.json端點錯誤處理。
* GRANITE-59968：允許設定REPLICATION_FORCE_READY_MILLIES。
* GRANITE-60183： Apache Commons-fileupload 1.6.0。
* GRANITE-60306：Apache Commons-lang至3.18.0。
* GRANITE-60637：Apache Commons-codec至1.19.0。
* GRANITE-60645： Apache Commons-ui 2.20.0。
* GRANITE-60663： Apache Commons-text 1.14.0。
* GRANITE-60714：Mongo Java驅動程式5.2。
* GRANITE-60778： Filevault 4.0.0。
* GRANITE-60823： Jackrabbit 2.22.2。
* GRANITE-60967：建立用於追蹤clientlib編譯時間的量度。
* SKYOPS-105469：在autofix api中新增對acsredirectMgr的支援。
* SKYOPS-113929：新增復寫就緒檢查的量度。
* SKYOPS-84821：Sling引擎2.16.6。
* SKYOPS-114322：將層級的關閉編譯器語言提升至`ECMASCRIPT_2018`。

### 已修正的問題 {#fixed-issues-21994}

* GRANITE-60167： Skyline中的非同步索引更新不支援CSV資料。
* GRANITE-60532：不選取值切換的修改。
* SITES-34277：修正頁面翻譯工作流程中的封鎖錯誤。
* SKYOPS-105471：支援aso autofix的dambaseredirect修正。
* SKYOPS-109532：新增功能已移除的連結作為切換後的註解。

#### AEM Guides {#guides-21994}

* GUIDES-26688：原生PDF範本中的CSS和頁面配置檔案表現出不一致的檔案鎖定行為，即使檔案被鎖定仍允許編輯。
* GUIDES-30900：從Assets UI複製具有大量資產的資料夾會導致API逾時。 操作會在後端繼續執行，並在一段時間後完成，但UI中未顯示成功或失敗訊息，或通知。
* GUIDES-29090：在原生PDF輸出中，索引清單(LOI)會以非字母順序顯示，且巢狀索引詞未正確分組，導致索引難以導覽。
* GUIDES-11227：從Assets UI複製DITA map時，也會將其附加的基線複製到新對應。
* GUIDES-31506：當「最近使用的檔案」小工具中列出的其中一個檔案是根據其來源範本不包含縮圖的範本時，首頁會變成空白。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-21994}

* Apache HTTPD版本2.4.65引入的變更可能會影響某些設定，因為作為安全性修正的一部分實作的新限制。 這些修正解決漏洞的方法是確保用於修改Content-Type標頭的`RequestHeader set`、`edit`和`edit_r`等指令現在正確限製為請求標頭。 此變更可防止回應標頭發生意外修改，尤其是靜態內容。

### 已過時的功能和 API {#deprecated-21994}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21994}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 2 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21994}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
