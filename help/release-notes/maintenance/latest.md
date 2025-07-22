---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 13124956fcce105ad42767f67b700284c8250012
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 31%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21644 {#21644}

以下摘要說明維護版本21644數的持續改善，該版本於2025年7月22日公開發佈。 前一個維護版本為版本 21570。

啟用 2025.7.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21644}

* Assets-39377：改善對Assets大量匯入工具中遠端儲存體429的處理。
* Assets-46026：可設定的中繼資料匯出工具最大深度。
* Assets-49172：Dynamic Media範本資產應繼承資料夾的中繼資料。
* Assets-50209：支援DM範本中的子字串。
* Assets-52326： AEM Assets設定頁面，可設定Assets的「標題」顯示偏好設定。
* Assets-52805：為大量作業工作新增CSV輸出/下載支援。
* Assets-52873：在資料夾屬性中新增設定，以停用該資料夾的AI處理。
* Assets-53535：改善YouTube視訊上傳效能。
* Assets-53612： Assets Omnisearch中的混合式搜尋控制。
* GRANITE-60183：將commons-fileupload相依性更新為1.6.0。
* GRANITE-60287：將QS更新至Jackrabbit 2.22.1。
* SITES-30452：包含ASO的內容API — 標題和說明建議。
* SITES-31677：自訂工作區支援 AEM 內容片段匯出至 Target。
* SKYOPS-112741：從AEM-CS SDK中移除`com.adobe.granite.product.support`套件組合。

### 已修正的問題 {#fixed-issues-21644}

* Assets-12882：開啟檢視器預設集後，UI對齊出現問題。
* Assets-48958： Asset Sync變更Sites本機AEM中的已發佈狀態的問題。
* Assets-50856： completeUpload未重設`dam:processingAttempts`。
* Assets-51604：連結共用報表CSV缺少「共用對象」資料。
* Assets-51783：如果使用搜尋查詢找不到設定，則遞補為`/conf/global`底下的DM設定。
* Assets-51857：無法重新排序資產表格專案。
* Assets-52169：新的BAT電腦轉譯錯誤包含在資產下載中。
* Assets-52229：遺失AEM as a Cloud Service中資產報告的收件匣通知。
* Assets-52399： com.day.cq.dam.api中的版本增加可能會破壞客戶程式碼。
* Assets-52780：即使未啟用切換，資產仍可標示為預覽。
* Assets-52866：移轉的DM視訊在停用DM同步處理的資料夾下仍維持處理狀態。
* Assets-53237：影像預設集編輯器中的「色彩設定檔」下拉式清單為空白。
* Assets-53240：資產報表 — 從Dynamic Media取得資產轉譯大小時，「磁碟使用情況」會失敗。
* Assets-53446：由於NPE，YouTube驗證權杖重新整理間歇性失敗。
* Assets-53827： ACL驗證封鎖儲存混合媒體集。
* Assets-5403：用於發佈執行個體的Dynamicmedia clientlibs應該有`allowProxy=true`。
* Assets-54261：中繼資料匯入會洩漏連線，並在檔案下載失敗時遭到封鎖。
* CQ-4359863：內容片段編輯器/資產編輯器中關鍵字的標籤搜尋順序出錯。
* CQ-4359958：讓openapi-support與AEM 6.5.22.0和更新版本相容。
* CQ-4360256：在透過`/adobe` servlet內容處理的HTTP要求的要求路徑中包含servlet內容路徑。
* CQ-4360317：新增在建置回應時設定Sunset date標題的方法。
* GRANITE-60311： AEM SDK Quickstart - 「OSGi Installer Configuration Printer」上的NPE。
* GS-15285：使用者顯示為已停用。

### 已知問題 {#known-issues-21644}

無。

### 已過時的功能和 API {#deprecated-21644}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21644}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 4 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21644}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
