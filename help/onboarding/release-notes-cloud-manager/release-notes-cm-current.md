---
title: Cloud Manager的發行說明，AEM作為Cloud Service版本2021.4.0
description: Cloud Manager的發行說明，AEM作為Cloud Service版本2021.4.0
feature: 發行資訊
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
translation-type: tm+mt
source-git-commit: 69694f2067c53667803d38bbf7bc752f3b3afac6
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2021.4.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2021.4.0。

## 發行日期 {#release-date}

Cloud Manager作為2021.4.0Cloud ServiceAEM的發行日期為2021年4月08日。
下一版預計於2021年5月06日推出。

### 新功能 {#what-is-new-april}

* UI更新至「新增及編輯程式」工作流程，使其更直覺。

* 具備必要權限的使用者現在可以透過UI提交商務端點。

* 環境變數現在可以限定到特定服務的範圍，可以是作者或發佈。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管線，「管理Git」（管理Git）按鈕也會顯示在「管線」卡上。****

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 由Cloud Manager建立的Adobe I/O開發人員主控台中的專案，不會再無意間被編輯或刪除。

* 當用戶添加新環境時，他們將被告知，一旦建立了環境，就不能將其移動到其他區域。

* 環境變數現在可以限定到特定服務的範圍，可以是作者或發佈。 需AEM要2021.03.5104.20210328T185548Z或更高版本。

* 刪除環境時啟動管線時的錯誤消息已被澄清。

* Eclipse專案提供的OSGi組合現在已排除在規則`CQBP-84--dependencies`之外。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管線的「體驗」稽核頁面時，以斜線`( / )`開頭的輸入路徑不會再導致步驟卡在擱置狀態。

* 當建立新的生產管道時，如果使用者未新增內容審核覆寫，則不會審核預設首頁。

* `CloudServiceIncompatibleWorkflowProcess`的問題在可下載的問題CSV檔案中嚴重性不正確。

* `Runmode`檢查對非資料夾節點產生誤報。