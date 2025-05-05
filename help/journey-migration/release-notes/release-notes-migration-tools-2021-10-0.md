---
title: AEM as a Cloud Service 2021.10.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2021.11.0版中移轉工具的發行說明
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 7%

---

# AEM as a Cloud Service 2021.10.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2021.10.0中移轉工具的發行說明。

>[!NOTE]
>
>如需最新發行說明，請參閱[Adobe Experience Manager as a Cloud Service最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager現在可讓使用者在趨勢線報告中檢視歷史BPA報告。 使用此報表，使用者便能以易於使用的圖形表示來檢視他們正在取得的進度。 如需詳細資訊，請參閱[使用檢視趨勢線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=zh-Hant#trendline-view-cam)。

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager現在可讓使用者在可列印的預覽中檢視BPA報告，以便進行簡易列印或列印PDF以便輕鬆共用。 請參閱[使用最佳做法分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=zh-Hant#best-practices-analysis)中的步驟6和步驟7。


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具v1.6.0的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 透過簡化的使用者體驗改進使用者對應工具，包括以下列出的功能。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=zh-Hant)。
   * 在執行使用者對應之前測試與使用者管理API的連線
   * 正常略過錯誤，並繼續使用者對應活動
   * 如果&#x200B;**存取權杖**&#x200B;在24小時後過期，則使用者對應不再失敗。 可以從上次停止的位置重新執行使用者對應。

* 為了提高「內容轉移工具」的健全度，內容可以一次擷取到作者例項或Publish例項。 如需詳細資訊，請參閱[內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant)。

* 包含版本時，會自動包含路徑`/var/audit`以移轉稽核事件。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能夠偵測並報告節點名稱長度。

* 能夠偵測及報告索引總大小。

* 能夠偵測並報告缺少原始轉譯的資產。
