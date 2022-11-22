---
title: AEM as a Cloud Service 版本 2022.02.0 中 Cloud Manager 的發行說明
description: 以下是 AEM as a Cloud Service 版本 2022.02.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2022.02.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2022.02.0 中 Cloud Manager 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2022.02.0 中 Cloud Manager 的發行日期為 2022 年 2 月 10 日。下一個版本計畫於 2022 年 3 月 10 日發行。

## 新增功能 {#what-is-new}

* 新的加速 [Web 層設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)已引入，專門部署 HTTPD/Dispatcher 設定。
   * 您必須使用 AEM 版本 `2021.12.6151.20211217T120950Z` 或較新版本，並且[選擇使用 Dispatcher 工具的彈性模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)才能使用此功能。
   * 此功能將在 2022.02.0 版發行後的兩週內分階段推出。
* Cloud Manager 登陸頁面體驗已更新，改進導覽功能、可在網格/圖磚視圖之間輕鬆切換，還有快顯視窗以提供快速計劃摘要。
* 已將新的失敗臨界值 (`< D`) 新增到[可靠性評分量度。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 存在嚴重影響系統穩定性的品質問題 (主要與無效索引和工作流程相關) 的客戶，在這些問題得到解決之前無法部署。
* `BannedPath` [品質規則](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)的嚴重程度已從阻斷因素變更為嚴重。
* 管道精靈會在需要更新 AEM 環境時通知使用者，然後再設定與其關聯的[網頁層級設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。

## 錯誤修正 {#bug-fixes}

* 舊的 Git 存放庫密碼現在都一定會在新密碼產生時失效。
* 在極少數情況下，透過 API 更新環境變數不再干擾管道執行。
