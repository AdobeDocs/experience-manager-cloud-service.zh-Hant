---
title: 體驗稽核測試
description: 了解Experience Audit如何驗證您的部署程式，並協助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 1a7a9ee78d09a9360922a63dfa315ef9d106209e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# 體驗稽核測試 {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="體驗稽核測試"
>abstract="了解Experience Audit如何驗證您的部署程式，並協助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。"

了解Experience Audit如何驗證您的部署程式，並協助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。

## 總覽 {#overview}

Experience Audit是Cloud Manager Sites生產管道中提供的功能，可驗證部署程式，並協助確保已部署變更：

1. 符合效能、協助工具、最佳實務、SEO（搜尋引擎最佳化）和PWA（漸進式網頁應用程式）的基準標準。

1. 不要引入回歸。

Cloud Manager中的體驗稽核可確保一般使用者的網站體驗達到最高標準。

稽核結果提供資訊，可讓部署管理員查看目前和先前分數之間的分數和變更。 此深入分析對於判斷是否有將於目前部署引入的回歸十分有用。

Experience Audit由Google Lighthouse提供技術支援，Lighthouse是Google的開放原始碼工具，可在所有Cloud Manager生產管道中啟用。

## 了解體驗稽核結果 {#understanding-experience-audit-results}

體驗稽核透過 [生產管道執行頁面。](/help/implementing/cloud-manager/deploy-code.md)

* 匯總量度會測量經過稽核、效能、協助工具、最佳實務、SEO（搜尋引擎最佳化）之頁面的平均分數。
* 個別頁面層級分數也可透過向下切入取得。
* 可以查看各個測試的結果以及如何糾正已發現的任何問題的指導，分數的詳細資訊。
* 測試結果的歷史記錄會保存在Cloud Manager中，以判斷管道中引入的變更是否包含先前執行的任何回歸。

### 匯總分數 {#aggregate-scores}

匯總層級分數會採用執行中包含之頁面的平均分數。 匯總層級的變更代表目前執行中頁面的平均分數，與上次執行的平均分數相比，即使設定為包含的頁面集合在執行之間已變更，仍然如此。

每種測試類型（例如效能、協助工具、SEO和最佳實務）都有匯總層級分數。

變更量度可以有下列其中一個值。

* **正值**  — 自上次生產管道執行以來，頁面在選取的測試上已有所改善。

* **負值**  — 自上次生產管道執行以來，頁面已在選取的測試上回復。

* **無更改**  — 頁面的分數與上次生產管道執行時的分數相同。

* **不適用**  — 沒有可用於比較的先前分數。

![體驗稽核結果](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 頁面層級分數 {#page-level-scores}

借由切入任何測試，可提供更詳細的頁面層級分數。 您可以查看個別頁面在特定測試的分數，以及上次測試執行的變更。

按一下任何個別頁面的詳細資訊，可提供已評估之頁面元素的相關資訊，以及在偵測到改善機會時修正問題的指引。

![頁面層級分數](/help/implementing/cloud-manager/assets/exp-audit-2.png)
