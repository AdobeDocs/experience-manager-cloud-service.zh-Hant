---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18311 {#18311}

下面是 18311 維護版本持續改善的內容，該版本於 2024 年 10 月 22 日公開發佈。前一個維護版本是版本 18175。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18311}

* ASSETS-41820：用於處理監控程式的索引功能改進。
* ASSETS-43720：用於處理監控程式的功能改進。
* ASSETS-42554：大型資料夾的效能改進。
* SKYOPS-77603：業務使用者的重新導向管理。

### 已修正的問題 {#fixed-issues-18311}

* ASSETS-37534：變更搜尋以不公開用於核准目標的屬性。
* ASSETS-38322：移除發佈條件提供者設定移除發佈事件功能。
* ASSETS-40482：Scene7 視訊播放器中播放/暫停和靜音/取消靜音按鈕的輔助功能問題。
* ASSETS-40593：按一下「資產 > 檔案」中的「屬性」按鈕後出現錯誤頁面。
* ASSETS-40598：將未同步的資產移至啟用同步的資料夾時同步智慧裁切。
* ASSETS-40743：當檔案名稱中存在某些字元時，觸發「取代資產」對話框時出現問題。
* ASSETS-40825：編輯搜尋表單後資產搜尋面向消失。
* ASSETS-41007：AEM 上的刪除有時會在傳遞時留下孤立資產。
* ASSETS-41172：Dynamic Media 範本名稱中不允許使用特殊字元。
* ASSETS-41896：資料夾上的 cq:discarded 屬性中所提及的資產不應發佈到 Brand Portal。
* ASSETS-42067：Dynamic Media 範本 - 下載出現錯誤。
* ASSETS-42070：Dynamic Media 範本 - 非管理員使用者應具有範本建立/編輯存取權限。
* ASSETS-42344：連接的資產同步已中斷 - 重新連接並為客戶提供建議。
* ASSETS-42620：資產版本的預覽選項發生問題 - 當我們開啟資產時顯示空白預覽。
* ASSETS-42701：Web 最佳化的影像傳遞和裁切問題。
* ASSETS-42966：如果多個工作共用相同路徑，非同步防護柵欄可能會錯誤地解除鎖定。
* ASSETS-43072：Dynamic Media 範本 - 參考無效時，範本參考查詢會中斷。
* ASSETS-43212：後設資料結構編輯器的國際化問題。
* ASSETS-43202：修正從時間軸選取要列印的註解的問題。
* ASSETS-43502：AEM CS 現有影像預設名稱未顯示在編輯頁面上。
* ASSETS-43538：非同步複製資產工作使用了錯誤的來源路徑屬性。
* ASSETS-43798：在複製資產之前，先檢查目標路徑。
* ASSETS-43945：將非同步資產工作佇列的重試延遲增加到 20 分鐘。
* ASSETS-44025：選取單一資產時，非同步刪除資產工作會失敗。
* SITES-26128：CreateLiveCopyStep 中發生類別轉換例外狀況。
* SCRNS-4551：[SG Pools Screens] 頻道中包含視訊元件時，瀏覽器預覽和播放器顯示「一般頁面錯誤」。

### 已知問題 {#known-issues-18311}

* FORMS-15818：元件描述項條目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。

### 已過時的功能和 API {#deprecated-18311}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-18311}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 3 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18311}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
