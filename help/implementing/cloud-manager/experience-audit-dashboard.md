---
title: 體驗稽核控制面板
description: 瞭解體驗稽核如何驗證您的部署流程，並透過清晰、資訊豐富的儀表板介面，幫助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。
source-git-commit: 7a8e6c3d226b02c65943629d0df196252218aa3c
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 22%

---


# 體驗稽核控制面板 {#experience-audit-dashboard}


瞭解體驗稽核如何驗證您的部署流程，並透過清晰、資訊豐富的儀表板介面，幫助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。

>[!NOTE]
>
>此功能僅適用於 [早期採用者計畫。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>如需AEMas a Cloud Service現有體驗稽核功能的詳細資訊，請參閱此檔案 [體驗稽核測試。](/help/implementing/cloud-manager/experience-audit-testing.md)

## 概觀 {#overview}

體驗稽核是 Cloud Manager Sites 生產管道中提供的功能，可驗證部署過程並幫助確保已部署變更：

1. 符合效能、協助工具、最佳實務、SEO (搜尋引擎最佳化) 和 PWA (漸進式 Web 應用程式) 的基準標準。

1. 不要引入迴歸。

Cloud Manager 中的體驗稽核可確保一般使用者的網站體驗達到最高標準。

稽核結果會提供資訊，可讓部署管理員查看目前和先前分數之間的分數和變更。此深入分析對於判斷是否有會於目前部署引入的迴歸十分有用。

體驗稽核由提供技術支援 [Google燈塔，](https://developer.chrome.com/docs/lighthouse/overview/) Google中的開放原始碼工具，並在所有Cloud Manager生產管道中啟用。

>[!TIP]
>
>當您[設定您的管道時，您可以設定要將哪些頁面包含在體驗稽核中。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)

## 體驗稽核控制面板 {#dashboard}

體驗稽核的結果會顯示在中 **中繼測試** 透過的生產管道階段 [生產管道執行頁面。](/help/implementing/cloud-manager/deploy-code.md)

![管道中的儀表板](assets/dashboard.png)

體驗稽核提供彙總和詳細的頁面層級測試結果，這些結果會歸納在四個索引標籤上：

* **[Insights](#insights)** 提供改善網站效能的可行建議簡短說明。
* **[Lighthouse分數](#lighthouse)** 是此管道執行中部署的程式碼的Lighthouse分數摘要。
* **[頁面](#pages)** 是特別設定以供分析之頁面的效能摘要。
* **[問題](#issues)** 總結在此管道執行的程式碼中偵測到的任何效能問題。

### Insights {#insights}

此 **Insights** 索引標籤簡要說明改善網站效能的可行建議。

![Insights](assets/insights.png)

點選或按一下 **顯示更多** 按鈕以開啟完整儀表板。

在 **深入分析和建議** 區段，您會找到可操作建議的詳細清單，這些建議具有繫結至預期績效的清晰值指標，以及受影響的頁面百分比。 這可讓您輕鬆為團隊排定這些建議的優先順序。

![深入分析和建議](assets/insights-recommendations.png)

若要導覽回生產管道執行頁面，只需選取瀏覽器上的上一頁箭頭。

### Lighthouse分數 {#lighthouse}

此 **Lighthouse分數** 索引標籤是此管道執行中部署的程式碼的Lighthouse分數摘要。

![Lighthouse分數](assets/lighthouse.png)

點選或按一下 **顯示更多** 按鈕以開啟完整儀表板。

在 **Lighthouse分數** 區段，您會找到各種分數的趨勢檢視。 選取 **效能**， **協助工具**， **PWA**，或 **SEO** 檢視這些值的每月趨勢檢視。

![Lighthouse分數圖表](assets/lighthouse-scores.png)

請注意，圖表上的每一點都是發生當月所有部署的平均值。

若要導覽回生產管道執行頁面，只需選取瀏覽器上的上一頁箭頭。

### 頁面 {#pages}

此 **頁面** 索引標籤是特別設定為要分析的頁面效能摘要。

![頁面索引標籤](assets/pages.png)

點選或按一下 **顯示更多** 按鈕以開啟完整儀表板。

此 **頁面** 區段提供已測試的頁面清單，及其最新的Lighthouse效能分數和劃分。

![頁面檢視](assets/pages-view.png)

當您[設定您的管道時，您可以設定要將哪些頁面包含在體驗稽核中。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)

若要導覽回生產管道執行頁面，只需選取瀏覽器上的上一頁箭頭。

### 問題 {#issues}

此 **問題** 索引標籤會總結在此管道執行的程式碼中偵測到的任何效能問題。

![問題索引標籤](assets/issues.png)

點選或按一下 **顯示更多** 按鈕以開啟完整儀表板。

在 **深入分析和建議** 區段，您會找到可操作建議的更詳細清單，這些建議具有繫結至預期績效增益的清晰值指標，以及受影響的頁面百分比。 這可讓您輕鬆為團隊排定這些建議的優先順序。

![深入分析和建議](assets/insights-recommendations.png)

若要導覽回生產管道執行頁面，只需選取瀏覽器上的上一頁箭頭。

### 頁面詳細資料 {#page-detail}

如果您在的標籤上點選或按一下頁面的連結， **體驗稽核** 管道執行頁面索引標籤或中的區段 **頁面** 體驗稽核控制面板的區段，您可以檢視特定頁面的詳細資訊。

![頁面資料](assets/page-data.png)

您可以查看各個頁面在特定測試中的得分情況以及與上一次測試執行相比的變化。

按一下任何單個頁面的詳細資訊，可獲得已評估頁面元素的相關資訊，以及在偵測到改善機會時修正問題的指引。

若要導覽回生產管道執行頁面，只需選取瀏覽器上的上一頁箭頭。
