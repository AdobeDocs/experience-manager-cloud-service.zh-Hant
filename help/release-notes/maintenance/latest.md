---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82b3b4bdcd09aa86974518f4f62e73c9f377c83f
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 30%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 發行說25821 {#release-25821}

以下摘要說明維護版本25821數的持續改善，該版本於2026年5月5日公開發佈。 先前的維護發行版本為發行說25520。

2026.5.0功能啟動將提供此維護版本的完整功能集。 如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-25821}

* CQ-4362304：建立指引前端並更新LLM設定UI。
* GRANITE-39546：將Apache Tika升級至3.x。
* GRANITE-53957：將適用於oak-blob-azure的Azure SDK V8升級至V12。
* GRANITE-61245：移除commons-lang的所有用法（取代為commons-lang3）。
* GRANITE-64748：凹凸OIDC驗證處理常式。
* GRANITE-64764：將Apache Commons文字更新為1.15.0。
* GRANITE-64963：將Filevault更新為4.2.0。
* GRANITE-66197：為M365租使用者新增Microsoft Graph API電子郵件支援。
* GRANITE-66449：針對Java 17 API支援更新Maven外掛程式。
* GRANITE-66473：將咖啡因快取程式庫新增至base-granite。
* GRANITE-66836：將Quickstart更新至Oak 2.0.0。
* SKYOPS-129301：將APIs jar Javadoc規範等級設定為Java 17。
* SKYOPS-129351：針對MCP SDK相容性更新反應流和反應核心。
* SKYOPS-131412：將Apache Commons Exec更新至最新版本。
* SKYOPS-131432：將Felix SCR更新至2.2.14。
* SKYOPS-131907：將Sling API區域更新至1.1.10。
* SKYOPS-131938：將GSON更新至最新版本。
* SKYOPS-132173：將Apache Commons轉碼器更新至最新版本。
* SKYOPS-132182：更新Sling租使用者套件組合。
* SKYOPS-132267：更新`org.osgi.service.component`註解。
* SKYOPS-132272：更新Sling功能模型套件。
* SKYOPS-132525：新增Quickstart分析器以防止新API移除。
* SKYOPS-134408：將`com.adobe.granite.asset.core`更新為2.2.82。
* SKYOPS-137750：將`com.adobe.granite.comments`更新為1.0.40。
* SKYOPS-137759：將`com.adobe.granite.jobs.async.ui.commons`更新為3.2.4。
* SKYOPS-138356：將`com.adobe.granite.oauth.server`更新為1.1.36。
* SKYOPS-138739：將SnakeYAML更新至2.6。

### 已修正的問題 {#fixed-issues-25821}

* Assets-59546：移除已棄用commons-lang程式庫的相依性。
* Assets-64831： AssetProcessorProcess重設處理嘗試計數導致資產停滯。
* Assets-66683：uploadBlob失敗導致的核准回圈。
* CNTBF-613：登入節點型別時修正存取遭拒(JCR-101)。
* GRANITE-44537：「國家/地區」中的字串未在AEM中本地化。
* GRANITE-61760：修正無法啟動AdminUserInitializer的問題。
* GRANITE-64543：許可權限制回應不遵循API結構。
* GRANITE-66692：內部類別載入器對封裝重新整理不敏感。
* GRANITE-66732：使用啟動器，而不是啟動層級1套裝的服務元件。
* GRANITE-66846： AEM許可權API未顯示`rep:ntNames`限制。
* SITES-39267：還原關係鏈結專案中的pagePath。
* SITES-43715：許可權驗證無法讀取資源狀態。

#### AEM Guides {#guides-25821}

* GUIDES-45110：使用&#x200B;**選取檔案**&#x200B;對話方塊在編輯器中選取影像時，只會顯示點陣格式（例如JPG、PNG和GIF）。 向量檔案（例如`.ai`和`.eps`）未顯示且無法選取。
* GUIDES-41938：在名稱中包含空格的資料夾中建立主題時，會錯誤地建立一個重複的資料夾，其中空格會被連字型大小取代，且主題會儲存在那裡而不是原始資料夾。
* GUIDES-38377：將資料夾設定檔中輸出預設集的變更套用至現有地圖時，已為AEM Sites預設集儲存的&#x200B;**發佈內容**&#x200B;會重設。
* GUIDES-43547：開啟大型主題或地圖時，作者執行個體會停止回應，在某些情況下需要重新啟動。
* GUIDES-32520：在元素上使用Backspace時，無論游標位置為何，編輯器都會捲動到主題的頂端（編輯器2.0）。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-25821}

無。

### 已過時的功能和 API {#deprecated-25821}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-25821}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。 此維護發行版本解決19個已識別的弱點，強化我們提供強大系統保護的承諾。

### 嵌入技術 {#embedded-tech-25821}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 2.0.0 | [Oak 2.0.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
