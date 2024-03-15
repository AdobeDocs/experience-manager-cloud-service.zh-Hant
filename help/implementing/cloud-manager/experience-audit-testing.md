---
title: 體驗稽核測試
description: 了解體驗稽核如何驗證您的部署過程，並幫助確保部署的變更符合效能、協助工具、最佳實務和 SEO 的基準標準。
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 58%

---


# 體驗稽核測試 {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="體驗稽核測試"
>abstract="了解體驗稽核如何驗證您的部署過程，並幫助確保部署的變更符合效能、協助工具、最佳實務和 SEO 的基準標準。"

了解體驗稽核如何驗證您的部署過程，並幫助確保部署的變更符合效能、協助工具、最佳實務和 SEO 的基準標準。

## 概觀 {#overview}

體驗稽核是 Cloud Manager Sites 生產管道中提供的功能，可驗證部署過程並幫助確保已部署變更：

1. 符合效能、協助工具、最佳實務、SEO (搜尋引擎最佳化) 和 PWA (漸進式 Web 應用程式) 的基線標準。

1. 不要引入迴歸。

Cloud Manager中的體驗稽核可確保使用者在網站上的體驗達到最高標準。

稽核結果會提供資訊，可讓部署管理員查看目前和先前分數之間的分數和變更。此深入分析對於判斷是否有會於目前部署引入的迴歸十分有用。

體驗稽核由Google的開放原始碼工具Google Lighthouse提供技術支援。

>[!INFO]
>
>自 2023 年 8 月 31 日起，體驗稽核將轉變為展示行動平台的特定結果。行動效能量度通常註冊的比桌上型電腦低，因此您應預期在此變更後，報告的效能會有所轉變。

## 可用性 {#availability}

體驗稽核適用於Cloud Manager：

* 網站生產管道，預設為。
* 可選擇前端開發管道。

請參閱 [設定區段](#configuration) 有關如何為選用環境設定稽核的詳細資訊。

## 設定 {#configuration}

生產管道預設會提供體驗稽核。 您可以選擇為前端開發管道啟用它。 在所有情況下，您需要定義在管道執行期間評估哪些內容路徑。

您可以設定在設定管道時，哪些頁面包含在體驗稽核中。

1. 根據您要設定的管線型別，請遵循以下指示：

   * 新增 [生產管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 如果要定義稽核要評估的路徑。
   * 新增 [非生產管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 如果您想要在前端或開發完整棧疊管道上啟用稽核。
   * 或者，您可以 [編輯現有管道，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) 並更新現有選項。

1. 如果您要新增或編輯要使用體驗稽核的非生產管道，則必須選取 **體驗稽核** 上的核取方塊 **原始碼** 標籤。

   ![啟用體驗稽核](assets/experience-audit-enable.jpg)

   * 這僅對非生產管道是必要的。
   * 此 **體驗稽核** 核取方塊選取時，標籤隨即顯示。

1. 對於生產和非生產管道，您可以定義應包含在上的體驗稽核中的路徑 **體驗稽核** 標籤。

   * 頁面路徑的開頭必須是 `/` 和是相對於您的網站。
   * 例如，若您的網站為 `wknd.site` 並且想要包含 `https://wknd.site/us/en/about-us.html` 在體驗稽核中，輸入路徑 `/us/en/about-us.html`.

   ![定義體驗稽核的路徑](assets/experience-audit-add-page.png)

1. 點選或按一下 **新增頁面** 路徑會使用您環境的地址自動完成，並新增至路徑表中。

   ![儲存表格的路徑](assets/experience-audit-page-added.png)

1. 重複前兩個步驟根據需要繼續新增路徑。

   * 您最多可以新增 25 個路徑。
   * 如果您未定義任何路徑，則預設情況下該網站的首頁會包含在體驗稽核中。

1. 按一下&#x200B;**儲存**，即可儲存您的管道。

## 了解體驗稽核結果 {#understanding-experience-audit-results}

體驗稽核透過[生產管道執行頁面](/help/implementing/cloud-manager/deploy-code.md)。

* 彙總量度會測量經過稽核、效能、協助工具、最佳實務、SEO (搜尋引擎最佳化) 之頁面的平均分數。
* 個別頁面層級分數也可透過深入研究取得。
* 分數的詳細資訊可用於查看各個測試的結果以及如何修復已發現的任何問題的指南。
* 測試結果的歷史記錄會保留在 Cloud Manager 中，以判斷管道中引入的變更是否包括上一次執行的任何迴歸。

### 彙總分數 {#aggregate-scores}

彙總層級分數採用執行中包含之頁面的平均分數。彙總層級的變更代表目前執行中頁面的平均分數，與上次執行的平均分數相比，即使設定為包含的頁面集合在執行之間已變更，仍然如此。

每種測試類型 (例如效能、協助工具、SEO 和最佳實務) 都有彙總層級分數。

變更量度可以有下列其中一個值。

* **正值**  — 自上次生產管道執行以來，頁面在選取的測試上已有所改善。

* **負值**  — 自上次生產管道執行以來，頁面已在選取的測試上回覆。

* **無變更**  — 頁面的分數與上次生產管道執行時的分數相同。

* **不適用** - 沒有可用於比較的先前分數。

![體驗稽核結果](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### 頁面層級分數 {#page-level-scores}

透過深入研究任何測試，可以獲得更詳細的頁面層級分數。您可以查看各個頁面在特定測試中的得分情況以及與上一次測試執行相比的變化。

按一下任何單個頁面的詳細資訊，可獲得已評估頁面元素的相關資訊，以及在偵測到改善機會時修正問題的指引。

![頁面層級分數](/help/implementing/cloud-manager/assets/exp-audit-2.png)
