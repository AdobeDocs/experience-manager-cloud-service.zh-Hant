---
title: Cloud Manager在as a Cloud Service版AEM2020.11.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2020.11.0中的發行說明
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2020.11.0 {#release-notes}

本頁概述了as a Cloud Service2020.11.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的發AEM布日期為2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 新菜單選項 **本地登錄** 現在，用戶可以從「環境」卡和「環境摘要」頁上的「環境」菜單選項獲得。
請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 的子菜單。

* 的 **學習** 已使用UI中的新映像刷新Cloud Manager中的頁籤。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在生成執行之前完成的依賴項的載入需要下載Maven插件。
* 從Cloud Manager頁腳中選擇語言的連結現在將導航到正確的位置。
* 有時，在代碼掃描期間，SonarQube進程不會啟動。 現在將自動檢測並嘗試重新啟動。
* 使用「體驗審核」步驟將自動啟用所有現有生產管道。
