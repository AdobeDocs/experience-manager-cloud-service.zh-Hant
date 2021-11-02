---
title: AEMas a Cloud Service版2021.10.0中移轉工具發行說明
description: AEMas a Cloud Service版2021.10.0中的Cloud Manager發行說明
feature: Release Information
exl-id: null
source-git-commit: 0058cfda65ec8f59dbe3ea1bbcc43c08c5e5fe3e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 6%

---


# AEMas a Cloud Service版2021.10.0中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2021.10.0中移轉工具的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant).

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager現在可讓使用者在趨勢線報表中檢視歷史BPA報表。 透過此報表，使用者可以輕鬆使用圖形表示來檢視其所取得的進展。 請參閱 [使用檢視趨勢線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) 以取得更多詳細資訊。

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager現在讓使用者能以可列印的預覽方式檢視BPA報表，輕鬆列印或列印至PDF，以方便共用。 請參閱 [使用最佳實務分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.6.0版的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 透過簡化的使用者體驗改善使用者對應工具，包括下列功能。 如需詳細資訊，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * 在執行使用者對應之前，測試與使用者管理API的連線
   * 適度略過錯誤，並繼續進行「使用者對應」活動
   * 若 **存取權杖** 24小時後過期。 可以從上次停止的位置重新運行用戶映射。

* 若要提高「內容轉移工具」的健全性，一次可將內容擷取至「製作」例項或「發佈」例項。 請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 以取得更多詳細資訊。

* 包含版本時，路徑 `/var/audit` 會自動納入，以移轉稽核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 偵測及報告節點名稱長度的功能。

* 能夠偵測並報告總索引大小。

* 能夠偵測遺失原始轉譯的資產並製作報表。