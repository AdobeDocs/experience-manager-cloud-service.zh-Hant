---
title: 內容審核測試——雲端服務
description: 內容審核測試——雲端服務
translation-type: tm+mt
source-git-commit: ce25ec1472dc349937fdbd5f7265d4295fe111e8
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# 內容審核測試 {#content-audit-testing}

「內容審核」是Cloud Manager Sites Production管道中的一項功能，由Google的開放原始碼工具Lighthouse提供支援。 所有Cloud Manager生產管道都啟用了此功能。

它可驗證部署程式，並協助確保已部署變更：

1. 符合效能、協助工具、最佳實務、搜尋引擎最佳化(SEO)和PWA（漸進式網頁應用程式）的基準標準。

1. 不要在這些維度中加入回歸。

Cloud Manager中的內容審核可確保網站上的使用者數位體驗維持在最高標準。 這些結果是提供資訊的，讓使用者可以查看目前和先前的分數之間的分數和變更。 此見解對於判斷目前部署中是否會引入回歸，十分有用。

## 瞭解內容審核結果 {#understanding-content-audit-results}

「內容審核」透過「生產管道」執行頁面提供匯總和詳細的頁面層級測試結果。

* 匯總層級量度會測量已稽核之頁面的平均分數。
* 您也可以透過向下切入來取得個別頁面層級的分數。
* 您可以取得分數的詳細資訊，以查看個別測試的結果，以及如何修正內容審核期間發現的任何問題的指引。
* 測試結果的歷史記錄保存在Cloud Manager中，因此客戶可以查看在管道運行中引入的更改是否包含先前運行的任何回歸。

### 匯總分數 {#aggregate-scores}

每個測試類型（效能、協助工具、SEO、最佳實務和PWA）都有匯總的等級分數。

匯總層級分數會取得執行中所包含之頁面的平均分數。 匯總層級的變更代表目前執行中頁面的平均分數，與前次執行的平均分數相比，即使設定為包含的頁面集合在執行之間已變更亦然。

「變更」量度的值可能是下列其中一項：

* **正值** -自上次生產管線執行以來，所選測試的頁面已改善

* **負值** -自上次生產管線執行以來，頁面在所選測試上已退縮

* **無更改** -自上次生產管道運行以來，頁面的分數相同

* **N/A** —— 沒有舊分數可供比較

   ![](/help/implementing/developing/introduction/assets/content-audit-test1.png)

### 頁面層級分數 {#page-level-scores}

透過鑽取任何測試，可檢視更詳細的頁面等級計分。 使用者將能夠查看個別頁面在特定測試中的分數，以及與上次測試執行時的變更。

按一下任何個別頁面的詳細資訊，將會提供已評估頁面元素的資訊，並指引您在偵測到改善機會時修正問題。 Google Lighthouse提供測試的詳細資訊和相關指引。

![](/help/implementing/developing/introduction/assets/page-level-scores.png)

