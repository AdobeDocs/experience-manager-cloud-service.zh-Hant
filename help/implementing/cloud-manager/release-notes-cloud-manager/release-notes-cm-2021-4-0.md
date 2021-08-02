---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.4.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.4.0版
feature: 發行資訊
exl-id: 456f945a-0320-4334-a407-ee2fcb1dbc0f
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Adobe Experience Manager as aCloud Service2021.4.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM as a 2021.4.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM as aCloud Service2021.4.0中的Cloud Manager發行日期為2021年4月8日。
下一版預計於2021年5月6日發行。

### 新增功能 {#what-is-new-april}

* 新增和編輯方案工作流程的UI更新，讓工作流程更直覺。

* 擁有必要權限的使用者現在可以透過UI提交商務端點。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管道，「管道」卡上也會顯示&#x200B;**管理Git**&#x200B;按鈕。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 由Cloud Manager建立的「Adobe I/O開發人員控制台」中的專案，不能再無意中編輯或刪除。

* 當使用者新增新環境時，系統會通知他們，一旦建立環境，就無法將其移至其他區域。

* 環境變數現在可限定在特定服務的範圍，可以是製作或發佈。 需要AEM 2021.03.5104.20210328T185548Z或更高版本。

* 已釐清刪除環境時啟動管道時的錯誤訊息。

* Eclipse專案提供的OSGi套件組合現已從規則`CQBP-84--dependencies`中排除。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的「體驗」稽核頁面時，以斜線`( / )`開頭的輸入路徑不會再導致步驟卡在擱置狀態。

* 建立新生產管道時，如果使用者未新增任何內容稽核覆寫，則不會稽核預設首頁。

* `CloudServiceIncompatibleWorkflowProcess`的問題在可下載的問題CSV檔案中嚴重性不正確。

* `Runmode`檢查對非資料夾節點產生誤判。
