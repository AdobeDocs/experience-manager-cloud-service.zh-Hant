---
title: 《 2021.10.0版中遷移工具AEM發行說明》
description: 《 2021.11.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 6%

---

# 《 2021.10.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2021.10.0中遷移工具的AEM發行說明。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 雲加速管理器 {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發佈日期為2021年10月25日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager現在允許用戶在趨勢線報告中查看歷史BPA報告。 使用此報告，用戶可以輕鬆使用圖形表示方式來查看他們正在取得的進展。 請參閱 [使用查看趨勢線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) 的子菜單。

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發佈日期為2021年10月4日。

### 新增功能 {#what-is-new-cam-oct}

Cloud Acceleration Manager現在允許用戶在可打印預覽中查看BPA報告，從而允許簡單打印或打印到PDF，以便於共用。 請參閱中的步驟6和7 [使用最佳做法分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis)。


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt-latest}

內容傳輸工具v1.6.0的發佈日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt-oct}

* 使用簡化的用戶體驗改進了用戶映射工具，包括下面列出的以下功能。 有關詳細資訊，請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html)。
   * Test到用戶管理API的連接，然後運行用戶映射
   * 順利跳過錯誤並繼續「用戶映射」活動
   * 如果 **訪問令牌** 24小時後過期。 可以從上次停止的位置重新運行用戶映射。

* 要增強內容傳輸工具的健壯性，可以一次將內容攝取到Author實例或Publish實例。 請參閱 [內容傳輸工具入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 的子菜單。

* 包含版本時，路徑 `/var/audit` 自動包含以遷移審核事件。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

最佳做法分析器2.1.20版的發佈日期為2021年10月5日。

### 新增功能 {#what-is-new-bpa-oct}

* 能夠檢測並報告節點名稱長度。

* 能夠檢測並報告總索引大小。

* 能夠檢測並報告丟失原始格式副本的資產。
