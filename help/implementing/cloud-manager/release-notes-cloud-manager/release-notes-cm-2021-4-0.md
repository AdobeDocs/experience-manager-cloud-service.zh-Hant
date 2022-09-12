---
title: AEM as a Cloud Service2021.4.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.4.0版中Cloud Manager發行說明
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2021.4.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.4.0as a Cloud Service版中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM 2021.4.0中的Cloud Manageras a Cloud Service日期為2021年4月8日。
下一版預計於2021年5月6日發行。

### 新增功能 {#what-is-new-april}

* 新增和編輯方案工作流程的UI更新，讓工作流程更直覺。

* 擁有必要權限的使用者現在可以透過UI提交商務端點。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM版本 `2021.03.5104.20210328T185548Z` 或更高版本。

* 此 **管理Git** 按鈕會顯示在「管道」卡上，即使尚未配置管道亦然。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 由Cloud Manager建立的「Adobe I/O開發人員控制台」中的專案，不能再無意中編輯或刪除。

* 當使用者新增新環境時，系統會通知他們，一旦建立環境，就無法將其移至其他區域。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM 2021.03.5104.20210328T185548Z或更高版本。

* 已釐清刪除環境時啟動管道時的錯誤訊息。

* Eclipse專案提供的OSGi套件組合現已從規則中排除 `CQBP-84--dependencies`.

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的「體驗」稽核頁面時，輸入路徑會以斜線開頭 `( / )` 不會再導致步驟停滯於擱置狀態。

* 建立新生產管道時，如果使用者未新增任何內容稽核覆寫，則不會稽核預設首頁。

* 適用於 `CloudServiceIncompatibleWorkflowProcess` 可下載的問題CSV檔案的嚴重性不正確。

* 此 `Runmode` 檢查對非資料夾節點產生誤判。
