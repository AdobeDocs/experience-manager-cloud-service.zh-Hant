---
title: Cloud Manager在as a Cloud Service版AEM2022.02.0中的發行說明
description: 以下是as a Cloud Service版本2022.02.0中Cloud Manager的AEM發行說明。
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2022.02.0 {#release-notes}

本頁概述了as a Cloud Service2022.02.0中Cloud ManagerAEM的發行說明。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud ServiceAEM2022.02.0中的發佈日期為2022年2月10日。 下一版計畫於2022年3月10日發行。

## 新增功能 {#what-is-new}

* 新加速 [Web層配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 已引入專門部署HTTPD/dispatcher配置。
   * 您必須處於版AEM本 `2021.12.6151.20211217T120950Z` 或更新 [選擇調度工具的靈活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 功能。
   * 此功能將在發佈後的兩週內分階段2022.02.0出。
* Cloud Manager登錄頁體驗已刷新，可提供改進的導航、網格/平鋪視圖之間的輕鬆切換，以及彈出窗口，以快速獲得程式摘要。
* 新的失敗閾值(`< D`)已添加到 [可靠性評級指標。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 如果客戶遇到嚴重質量問題，影響系統穩定性，主要與無效索引和工作流進程有關，則在這些問題得到解決之前，他們將無法進行部署。
* 嚴重性 `BannedPath` [質量規則](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) 已從阻止程式更改為關鍵。
* 管道嚮導將在配置環境之前AEM通知用戶何時需要環境更新 [Web層配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 關聯。

## 錯誤修正 {#bug-fixes}

* 當生成新密碼時，舊Git儲存庫密碼始終無效。
* 通過API更新環境變數不再會在極少數情況下干擾管道執行。
