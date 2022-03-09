---
title: 體驗審計測試
description: 瞭解體驗審核如何驗證您的部署流程並幫助確保部署的更改符合效能、可訪問性、最佳實踐和SEO的基準標準。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# 體驗審計測試 {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="體驗審計測試"
>abstract="瞭解體驗審核如何驗證您的部署流程並幫助確保部署的更改符合效能、可訪問性、最佳實踐和SEO的基準標準。"

瞭解體驗審核如何驗證您的部署流程並幫助確保部署的更改符合效能、可訪問性、最佳實踐和SEO的基準標準。

## 概覽 {#overview}

體驗審計是Cloud Manager站點生產管道中提供的一項功能，可驗證部署過程並幫助確保部署的更改：

1. 滿足效能、可訪問性、最佳實踐、SEO（搜索引擎優化）和PWA(Progressive Web App)的基準標準。

1. 不要帶回回歸。

Cloud Manager中的體驗審核可確保最終用戶在站點上的體驗符合最高標準。

審計結果是資訊性的，使部署管理器能夠查看當前和以前的分數之間的分數和變化。 這一洞見對於確定當前部署中是否將引入回歸非常重要。

體驗審計由Google燈塔提供支援，後者是谷歌的開源工具，在所有Cloud Manager生產管道中都啟用。

## 瞭解經驗審計結果 {#understanding-experience-audit-results}

體驗審核通過以下方式提供聚合和詳細的頁面級test結果： [生產管道執行頁。](/help/implementing/cloud-manager/deploy-code.md)

* 聚合度量度量在已審核的頁面中的平均分數，這些頁面針對效能、可訪問性、最佳實踐、SEO（搜索引擎優化）。
* 單個頁面級別分數也可通過向下鑽取獲得。
* 可以查看各個test結果的詳細資訊以及有關如何修正已識別的任何問題的指導。
* Cloud Manager中保留test結果的歷史記錄，以確定管道中引入的更改是否包含上一運行中的任何回歸。

### 聚合分數 {#aggregate-scores}

聚合級別分數採用運行中包括的頁面的平均分數。 聚合級別的更改表示當前運行中頁面的平均分數與前一次運行中得分的平均值相比，即使配置為包含的頁面集合在兩次運行之間已更改。

每個test類型（如效能、可訪問性、SEO和最佳實踐）都有聚合級別分數。

更改度量可以具有以下值之一。

* **正值**  — 自上次生產管道運行以來，所選test上的頁面已得到改善。

* **負值**  — 自上次生產管道運行以來，頁面在所選test上已退縮。

* **無更改**  — 自上次生產管道運行以來，頁面的得分相同。

* **不適用**  — 以前沒有可供比較的分數。

![經驗審計結果](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### 頁級分數 {#page-level-scores}

通過鑽取任何test，可獲得更詳細的頁級評分。 您可以看到各個頁面對特定test的評分方式，以及上次test運行的更改。

按一下任何單個頁面的詳細資訊提供有關已評估頁面元素的資訊，以及在檢測到改進機會時解決問題的指導。

![頁級分數](/help/implementing/cloud-manager/assets/exp-audit-2.png)
