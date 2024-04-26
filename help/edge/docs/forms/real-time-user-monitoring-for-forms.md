---
title: Edge Delivery Services 表單的即時使用者監控
description: Edge Delivery Services 表單的即時使用者監控是對使用者與表單互動的持續追蹤和分析。
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: ht
source-wordcount: '701'
ht-degree: 100%

---


# Edge Delivery Services 表單的即時使用者監控

Adobe Experience Manager 使用即時使用者監控 (RUM) 來了解訪客與由 Adob&#x200B;&#x200B;e Experience Manager 驅動網站的互動。此功能可協助診斷效能挑戰並衡量實驗有效性。即時使用者監控可透過使用抽樣技術來維護訪客的隱私權，確保您正在造訪的網站不會收集任何個人資訊。此功能不允許將個人資料新增至 RUM 資料集合。Adobe Experience Manager 中的即時使用者監控旨在保護訪客隱私權並限制至最少的資料收集。

## 為 Edge Delivery Services 表單使用即時使用者監控的優點 {#advantages}

AEM 會使用即時使用者監控來達到以下目的：

* 識別並修正網站上的效能瓶頸。
* 估計客戶網站的頁面瀏覽量
* 了解 Adob&#x200B;&#x200B;e Experience Manager 在相同頁面上與分析、目標市場或外部資料庫的互動，以便增強相容性。

## 必要條件 

您可以造訪以下 URL 來查看 Edge Delivery Services 表單的即時使用者監控儀表板：
https://data.aem.live/?ext=forms

![Edge Delivery Services 表單的 RUM 登入畫面 ](/help/edge/assets/rum-login-screen.png)

若要登入 Edge Delivery Services 表單的即時使用者監控儀表板，請輸入以下內容：
* **URL**：該 URL 是針對使用者網站或網域。使用者可以選擇篩選網站或網域，根據自己的要求來查看儀表板。
* **網域金鑰**：使用者可手動產生網域金鑰。如需協助或查詢，請參閱「[產生 RUM 網域金鑰](https://aemcs-workspace.adobe.com/rum/generate-domain-key)」文件。

### Edge Delivery Services 表單的即時使用者監控儀表板

在登入畫面中輸入 URL 和網域金鑰後，您可以取得 Edge Delivery Services 表單的即時使用者監控儀表板存取權。

下圖示範了 Edge Delivery Services 表單的 RUM 儀表板：

![RUM 表單儀表板](/help/edge/assets/rum-forms-dashboard.png)

### RUM 表單儀表板的不同關鍵量度 {#different-metrics-rum-dashboard-forms}

您可以使用以下關鍵量度評估訪客與 Adob&#x200B;&#x200B;e Experience Manager 驅動網站的互動：

* **表單視圖**：這是在指定日期範圍內為 URL 呈現的表單總數。
* **表單提交**：這是在指定日期範圍內為 URL 提交的表單總數。
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
