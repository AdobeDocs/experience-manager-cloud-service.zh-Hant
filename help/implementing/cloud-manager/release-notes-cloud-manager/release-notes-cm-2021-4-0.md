---
title: AEM as a Cloud Service 版本 2021.4.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.4.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.4.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.4.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.4.0 中 Cloud Manager 的發行日期為 2021 年 4 月 08 日。下一個版本計劃於 2021 年 05 月 06 日發行。

### 新增功能 {#what-is-new-april}

* UI 更新成新增和編輯計劃工作流程，讓使用者介面更直覺。

* 具有必要權限的使用者現在可以透過 UI 提交商務端點。

* 環境變數現在可以將範圍限定至特定服務，即作者或發佈。需要 AEM 版本 `2021.03.5104.20210328T185548Z` 或更高版本

* **「管理 Git」** 按鈕於管線卡中顯示，即使尚未設定任何管線。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 27。

* 在 Adobe I/O Developer Console 中由 Cloud Manager 建立的專案不再可無意編輯或刪除。

* 使用者新增環境時，便會告知使用者，在建立環境後，即無法將環境移至不同區域。

* 環境變數現在可以將範圍限定至特定服務，即作者或發佈。需要 AEM 版本 2021.03.5104.20210328T185548Z 或更高版本

* 已釐清啟動管線時或刪除環境時的錯誤訊息。

* Eclipse 專案提供的 OSGi 產品組合現在已從規則 `CQBP-84--dependencies` 排除。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的體驗稽核頁面時，以斜杠開頭的輸入路徑`( / )`將不再導致步驟卡在掛起狀態。

* 建立新的生產管道時，如果使用者未新增任何內容稽核覆蓋，則預設主頁未經過稽核。

* 的問題`CloudServiceIncompatibleWorkflowProcess`可下載的問題 CSV 文件中的嚴重性不正確。

* `Runmode` 可檢查在非文件夾節點上產生誤報。
