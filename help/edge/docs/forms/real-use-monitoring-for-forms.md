---
title: AEM Formsas a Cloud ServiceEdge Delivery Services的即時使用監控
description: AEM Formsas a Cloud ServiceEdge Delivery Services的即時使用監控涉及持續追蹤和分析使用者與表單的互動。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 6f78b43e857ca496465c315e8812bb67aff8c627
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 45%

---


# AEM Formsas a Cloud ServiceEdge Delivery Services的「即時使用監控」

「即時監控(RUM)」可讓您在真實世界中深入瞭解訪客如何與您的Adobe Experience Manager (AEM)網站互動。 此內建工具提供寶貴資料，有助於瞭解使用者行為、診斷效能問題，以及評估網站實驗的成效。 RUM不僅透過擷取真實使用互動來進行合成測試，更準確地呈現您網站的效能。

不過，RUM會優先處理訪客隱私權。 其運用取樣技術來收集代表性使用者子集合的資料，確保未擷取任何個人識別資訊(PII)。 此外，RUM的設計也考慮到資料最小化，只收集效能分析所需的必要量度。 此方法可讓您最佳化AEM網站，同時維持使用者信任。


## 必要條件 

您可以存取下列URL，檢視AEM Formsas a Cloud ServiceEdge Delivery Services的監視控制面板：

https://data.aem.live/?ext=forms

![FormsEdge Delivery Services的RUM登入畫面](/help/edge/assets/rum-login-screen.png)

若要登入AEM Formsas a Cloud ServiceEdge Delivery Services的監視控制面板，請輸入下列內容：

* **URL**：該 URL 是針對使用者網站或網域。使用者可以選擇篩選網站或網域，根據自己的要求來查看儀表板。

* **網域金鑰**：使用者可手動產生網域金鑰。若要取得表單的網域金鑰，請聯絡您的Adobe代表。

### AEM Formsas a Cloud ServiceEdge Delivery Services監視儀表板

在登入畫面中輸入URL和網域金鑰後，您就可以存取監控控制面板，以便AEM Forms的as a Cloud ServiceEdge Delivery Services。

下圖示範AEM Formsas a Cloud Service的Edge Delivery Services控制面板：

![RUM 表單儀表板](/help/edge/assets/rum-forms-dashboard.png)

### Forms控制面板的不同關鍵量度 {#different-metrics-rum-dashboard-forms}

此儀表板提供訪客如何與您Adobe Experience Manager (AEM)網站上表單互動的關鍵深入分析。 透過監控這些量度，您可以找出需要改善的領域並最佳化您的表單，以獲得更好的使用者體驗和轉換率：

* **表單檢視**：追蹤表單顯示的總次數
* **表單提交**：追蹤已完成的提交總數

* **最大的內容繪製**：這會顯示 URL 載入的速度，表示從使用者請求 URL 的那一刻起呈現檢視區中可見最大內容元素所花的時間。此最大內容元素可以是圖像、影片或大量的區塊級文字元素。URL 載入速度的效能評級分類如下：
   * **很好**：如果載入時間為 2.5 秒或更短。
   * **還好**：如果載入時間超過 2.5 秒但在 4 秒以下。
   * **不好**：如果載入時間超過 4 秒

* **累積的版面移動**：這會測量在整個頁面有效期所發生每個意外版面移動的所有個別版面移動分數的總和。此功能對於確定頁面效能有很關鍵的作用，因為當使用者嘗試與頁面元素互動時頁面元素會發生變化，此功能會造成不良的使用者體驗。此分數的範圍為零到任何正數：零表示沒有移動，較高數字表示頁面上的版面移動較多。用來評估版面移動分數的效能指標分類如下：

   * **很好**：如果版面移動分數為 0.1 或更小。
   * **還好**：如果佈局移動分數大於 0.1 但 比 0.25 或更小。
   * **不好**：如果版面移動分數超過 0.25。

* **至下次繪製的互動**：此功能可評估頁面對使用者互動的反應速度，考慮使用者造訪頁面期間頁面回應按選、點選和鍵盤輸入所需的時間。最終值是觀察到的最久互動，且忽略任何異常。「至下次繪製的互動」的效能指標分類如下：
   * **很好**：如果使用者兩個動作之間的持續時間為 200 毫秒 或更短。
   * **還好**：如果持續時間超過 200 毫秒但小於等於 500 毫秒。
   * **不好**：如果持續時間超過 500 毫秒。

## 可操作分析

透過分析這些量度，您可以找出機會來：

* 簡化表單並減少欄位數。
* 透過清楚的指示和標籤改善表單清晰度。
* 最佳化表單版面配置以提供行動回應。
* 解決拖慢表單載入速度的技術問題。

透過專注於這些區域，您可以建立更易於使用的表單，並鼓勵訪客完成這些表單，最終導致更高的轉換率。