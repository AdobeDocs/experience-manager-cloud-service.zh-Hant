---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: ht
source-wordcount: '632'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21706 {#21706}

以下摘要說明維護版本 21706 的持續改善內容，該版本已於 2025 年 7 月 24 日公開發佈。前一個維護版本為版本 21570。

>[!NOTE]
>
>版本 21644 已設為私人版本，並由版本 21706 取代。

啟用 2025.7.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21706}

* ASSETS-39377：改善資產大量匯入工具的遠端儲存發出之 429 訊息的處理方式。
* ASSETS-46026：可設定後設資料匯出工具的最大深度。
* ASSETS-49172：Dynamic Media 範本資產應繼承資料夾的後設資料。
* ASSETS-50209：DM 範本支援子字串功能。
* ASSETS-52326：AEM Assets 設定頁面可設定 Assets 的標題顯示偏好設定。
* ASSETS-52805：大量作業的工作增加對 CSV 輸出/下載的支援。
* ASSETS-52873：在資料夾屬性中增加新設定，以停用該資料夾的 AI 處理。
* ASSETS-53535：提升 YouTube 影片上傳效能。
* ASSETS-53612：在資產全方位搜尋中提供控制混合式搜尋的功能。
* GRANITE-60183：將 commons-fileupload 相依性更新至 1.6.0。
* GRANITE-60287：將 QS 更新至 Jackrabbit 2.22.1。
* SITES-30452：內容 API 搭配 ASO，提供標題和描述建議。
* SITES-31677：自訂工作區支援 AEM 內容片段匯出至 Target。
* SKYOPS-112741：從 AEM-CS SDK 中刪除 `com.adobe.granite.product.support` 套件。

### 已修正的問題 {#fixed-issues-21706}

* ASSETS-12882：開啟檢視器預設集後出現 UI 對齊問題。
* ASSETS-48958：資產同步導致 Sites 本機 AEM 的已發佈狀態變更的問題。
* ASSETS-50856：在執行 completeUpload 時 `dam:processingAttempts` 未重設。
* ASSETS-51604：連結共用報告 CSV 缺少「共用者」資料。
* ASSETS-51783：如果使用搜尋查詢找不到任何設定，則恢復到 `/conf/global` 下的 DM 設定。
* ASSETS-51857：資產表格項目不可重新排序。
* ASSETS-52169：下載資產時，誤把新的 BAT 機器轉譯包含在內。
* ASSETS-52229：AEM as a Cloud Service 的資產報告缺少收件匣通知。
* ASSETS-52399：com.day.cq.dam.api 中的版本號提升可能會導致客戶程式碼無法運作。
* ASSETS-52780：即使未啟用切換，也可以標記資產以供預覽。
* ASSETS-52866：在停用 DM 同步的情況下，遷移後的 DM 影片在資料夾下仍維持處理中狀態。
* ASSETS-53237：在影像預設編輯器中，顏色設定檔下拉式清單為空白。
* ASSETS-53240：資產報告 - 從 Dynamic Media 取得資產轉譯大小時，無法取得磁碟使用量的資料。
* ASSETS-53446：因為 NPE，導致重新整理 YouTube 驗證權杖時不時發生失敗的情況。
* ASSETS-53827：ACL 驗證導致無法儲存混合媒體集。
* ASSETS-5403：在發佈實例上使用的 Dynamicmedia clientlibs 應該具有 `allowProxy=true`。
* ASSETS-54261：如果檔案下載失敗，後設資料匯入會發生連線資源洩漏的情況且無法繼續執行。
* CQ-4359863：在內容片段編輯器或資產編輯器中，因為關鍵字順序錯誤使得標記搜尋中斷。
* CQ-4359958：使 openapi-support 與 AEM 6.5.22.0 及更高版本相容。
* CQ-4360256：對於透過 `/adobe` servlet 環境處理的 HTTP 要求，在要求路徑中包含 servlet 環境路徑。
* CQ-4360317：新增在建立回應時設定停止支援日期標頭的方法。
* GRANITE-60311：AEM SDK 快速入門 - 執行「OSGi 安裝程式設定印表機」時發生 NPE。
* GS-15285：使用者顯示為已停用。

### 已知問題 {#known-issues-21706}

無。

### 已過時的功能和 API {#deprecated-21706}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21706}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 4 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21706}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
