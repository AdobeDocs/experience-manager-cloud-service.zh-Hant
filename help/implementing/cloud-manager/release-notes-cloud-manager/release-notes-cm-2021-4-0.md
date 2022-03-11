---
title: Cloud Manager在as a Cloud Service版AEM2021.4.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.4.0中的發行說明
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.4.0 {#release-notes}

本頁概述了as a Cloud Service2021.4.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的發AEM布日期為2021年4月8日。
下一版計畫於2021年5月6日發行。

### 新增功能 {#what-is-new-april}

* UI更新「添加和編輯程式」工作流，使其更直觀。

* 具有必要權限的用戶現在可以通過UI提交商業終點。

* 現在，環境變數可以限定到特定服務的範圍，即作者或發佈。 需要版AEM本 `2021.03.5104.20210328T185548Z` 或更高。

* 的 **管理Git** 即使尚未配置管線，也會在管線卡上顯示。

* Cloud Manager使用的AEM項目原型版本已更新為版本27。

* Cloud Manager建立的Adobe I/O開發人員控制台中的項目不能再被無意地編輯或刪除。

* 當用戶添加新環境時，他們將被告知，一旦建立了一個環境，就不能將其移動到其他區域。

* 現在，環境變數可以限定到特定服務的範圍，即作者或發佈。 需要AEM2021.03.5104.20210328T185548Z或更高版本。

* 已澄清刪除環境時啟動管道時的錯誤消息。

* Eclipse項目提供的OSGi捆綁包現在已從規則中排除 `CQBP-84--dependencies`。

### 錯誤修正 {#bug-fixes-cm-april}

* 編輯管道的「體驗」審計頁時，輸入路徑以斜槓開頭 `( / )` 將不再導致該步驟處於掛起狀態。

* 建立新生產管道時，如果用戶未添加內容審核覆蓋，則未審核預設首頁。

* 針對 `CloudServiceIncompatibleWorkflowProcess` 可下載問題CSV檔案中的嚴重性不正確。

* 的 `Runmode` 檢查在非資料夾節點上產生誤報。
