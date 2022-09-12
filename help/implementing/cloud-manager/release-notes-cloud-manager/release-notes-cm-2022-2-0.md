---
title: AEMas a Cloud Service版2022.02.0中的Cloud Manager發行說明
description: 以下是AEM 2022.02.0版as a Cloud Service版本中Cloud Manager的發行說明。
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service 2022.02.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEMas a Cloud Service版2022.02.0中Cloud Manager的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期為2022.02.0年2月10日。 下一版預計於2022年3月10日發行。

## 新增功能 {#what-is-new}

* 新加速 [Web層配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 已導入專門部署HTTPD/dispatcher設定。
   * 您必須使用AEM版本 `2021.12.6151.20211217T120950Z` 或更新版本 [選擇加入dispatcher工具的彈性模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 來使用此功能。
   * 此功能將在2022.02.0版後的兩週內分階段推出。
* Cloud Manager登錄頁面體驗已重新整理，可提供改善的導覽、在格線/圖磚檢視之間輕鬆切換，以及快速取得方案摘要的快顯畫面。
* 新的失敗臨界值(`< D`)已新增至 [可靠性評等量度。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 如果客戶遇到嚴重影響系統穩定性的嚴重質量問題（主要與無效索引和工作流進程相關），則要等到這些問題得到解決後，才能進行部署。
* 嚴重性 `BannedPath` [品質規則](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) 已從封鎖程式變更為嚴重。
* 在設定 [Web層配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 關聯。

## 錯誤修正 {#bug-fixes}

* 產生新密碼時，舊的Git存放庫密碼一律失效。
* 在罕見情況下，透過API更新環境變數不再會干擾管道執行。
