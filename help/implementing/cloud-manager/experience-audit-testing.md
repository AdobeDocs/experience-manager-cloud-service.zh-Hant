---
title: 體驗稽核測試 — Cloud Services
description: 體驗稽核測試 — Cloud Services
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 體驗稽核測試{#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="體驗稽核測試"
>abstract="Experience Audit是Cloud Manager Sites生產管道中提供的功能，由Google Lighthouse（Google的開放原始碼工具）提供技術支援。 所有Cloud Manager生產管道都會啟用此功能。"

Experience Audit是Cloud Manager Sites生產管道中提供的功能，由Google Lighthouse（Google的開放原始碼工具）提供技術支援。 所有Cloud Manager生產管道都會啟用此功能。

它會驗證部署程式，並協助確保已部署變更：

1. 符合效能、協助工具、最佳實務、SEO（搜尋引擎最佳化）和PWA（漸進式網頁應用程式）的基準標準。

1. 請勿在這些維度中包含回歸。

Cloud Manager中的體驗稽核可確保網站上的使用者數位體驗可維持在最高標準。 結果提供資訊，讓使用者可查看目前和先前分數之間的分數和變更。 此深入分析對於判斷是否有將於目前部署引入的回歸十分有用。

## 了解體驗稽核結果{#understanding-experience-audit-results}

體驗稽核透過生產管道執行頁面提供匯總和詳細的頁面層級測試結果。

* 匯總層級量度會測量經過稽核、效能、協助工具、最佳實務、SEO（搜尋引擎最佳化）之頁面的平均分數。
   >[!NOTE]
   >摘要分數中不包含漸進式網頁應用程式(PWA)分數，且只會顯示在頁面層級的報表詳細資料畫面中。
* 個別頁面層級分數也可透過向下切入取得。
* 分數的詳細資訊可供查看個別測試的結果，以及如何修正在體驗稽核期間所識別的任何問題的指引。
* 測試結果的歷史記錄會保存在Cloud Manager中，讓客戶可以查看管道執行中引入的變更是否包含先前執行的任何回歸。

### 匯總分數{#aggregate-scores}

每種測試類型（例如效能、協助工具、SEO和最佳實務）都有匯總層級分數。
>[!NOTE]
>摘要分數中不包含漸進式網頁應用程式(PWA)分數，且只會顯示在頁面層級的報表詳細資料畫面中。

匯總層級分數會採用執行中包含之頁面的平均分數。 匯總層級的變更代表目前執行中頁面的平均分數，與上次執行的平均分數相比，即使設定為包含的頁面集合在執行之間已變更，仍然如此。

「變更」量度的值可能是下列其中一項：

* **正值**  — 自上次生產管道執行以來，頁面在選取的測試上已有所改善

* **負值**  — 自上次生產管道執行以來，頁面已在選取的測試上回復

* **無變更**  — 自上次生產管道執行以來，頁面的分數相同

* **不適用**  — 沒有先前的分數可供比較

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 頁面層級分數{#page-level-scores}

借由切入任何測試，可看到更詳細的頁面層級計分。 使用者將能查看個別頁面針對特定測試的評分情形，以及執行上次測試時的變更。

按一下任何個別頁面的詳細資訊，即可提供已評估頁面元素的資訊，並在偵測到改善機會時提供修正問題的指引。 測試的詳細資訊和相關指引由Google Lighthouse提供。

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
