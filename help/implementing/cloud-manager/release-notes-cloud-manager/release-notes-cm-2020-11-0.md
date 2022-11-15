---
title: AEM as a Cloud Service 版本 2020.11.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2020.11.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.11.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2020.11.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2020.11.0 中的 Cloud Manager 發行日期是 2020 年 11 月 12 日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 一個新的選單選項&#x200B;**本機登入**現在，使用者可以從環境卡和環境摘要頁面上的環境選單選項中使用。
如需詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* **學習** Cloud Manager 中的索引標籤已在 UI 中使用新圖像進行了刷新。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在構建執行之前完成的依賴項加載需要下載 Maven 插件。
* Cloud Manager 頁腳中用於選擇語言的鏈接現在將瀏覽到正確的位置。
* 有時在計劃碼掃描過程中，SonarQube 進程不會啟動。現在將自動檢測到這並嘗試重新啟動。
* 所有現有的生產管道都將透過體驗稽核步驟自動啟用。
