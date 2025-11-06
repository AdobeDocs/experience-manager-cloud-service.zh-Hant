---
title: AEM Forms as a Cloud Service 之 Edge Delivery Services 的操作遙測
description: AEM Forms as a Cloud Service 之 Edge Delivery Services 的操作遙測包含持續追蹤和分析使用者與表單的互動情形。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 100%

---

# AEM Forms as a Cloud Service 之 Edge Delivery Services 的操作遙測

操作遙測讓您可以獲得關於現實中訪客與 Adobe Experience Manager (AEM) 網站互動方式的見解。這項內建工具提供重要的資料，協助了解使用者行為、診斷效能問題，以及測量網站實驗的效益。操作遙測能擷取實際使用的互動情形，超越綜合測試，更準確地了解您的網站效能情況。

不過，操作遙測會優先考慮訪客的隱私。其利用抽樣技巧從具有代表性的使用者子集收集資料，確保不會擷取任何個人識別資訊 (PII)。此外，操作遙測的設計將資料最小化納入考量，僅收集效能分析所需的基本量度。您可以利用這個方法將 AEM 網站最佳化，同時維持使用者信任。


## 必要條件

您可以存取以下 URL，檢視 Edge Delivery Services for AEM Forms as a Cloud Service 的監視儀表板：

https://data.aem.live/?ext=forms

![Edge Delivery Services for Forms 的操作遙測登入畫面](/help/edge/assets/rum-login-screen.png)

若要登入 Edge Delivery Services for AEM Forms as a Cloud Service 的監視儀表板，請輸入以下內容：

- **URL**：該 URL 是針對使用者網站或網域。使用者可以選擇篩選網站或網域，根據自己的要求來查看儀表板。

- **網域金鑰**：使用者可手動產生網域金鑰。若要取得表單的網域金鑰，請聯絡您的 Adobe 代表。

### Edge Delivery Services for AEM Forms as a Cloud Service 的監視儀表板

在登入畫面中輸入 URL 和網域金鑰後，您便可以存取 Edge Delivery Services for AEM Forms as a Cloud Service 的監視儀表板。

下圖示範 Edge Delivery Services for AEM Forms as a Cloud Service 的儀表板：

![操作遙測表單儀表板](/help/edge/assets/rum-forms-dashboard.png)

### 表單儀表板的不同關鍵量度 {#different-metrics-operational-telemetry-dashboard-forms}

此儀表板提供有關訪客如何與 Adobe Experience Manager (AEM) 網站上表單互動的分析。透過監視這些量度，您可以確認需要改善的地方，並將表單最佳化以利改善使用者體驗和轉換率：

- **表單檢視次數**：追蹤表單顯示的總次數
- **表單提交**：追蹤已完成提交的總數

- **最大的內容繪製**：這會顯示 URL 載入的速度，表示從使用者請求 URL 的那一刻起呈現檢視區中可見最大內容元素所花的時間。此最大內容元素可以是圖像、影片或大量的區塊級文字元素。URL 載入速度的效能評級分類如下：
   - **很好**：如果載入時間為 2.5 秒或更短。
   - **還好**：如果載入時間超過 2.5 秒但在 4 秒以下。
   - **不好**：如果載入時間超過 4 秒

- **累積的版面移動**：這會測量在整個頁面有效期所發生每個意外版面移動的所有個別版面移動分數的總和。此功能對於確定頁面效能有很關鍵的作用，因為當使用者嘗試與頁面元素互動時頁面元素會發生變化，此功能會造成不良的使用者體驗。此分數的範圍為零到任何正數：零表示沒有移動，較高數字表示頁面上的版面移動較多。用來評估版面移動分數的效能指標分類如下：

   - **很好**：如果版面移動分數為 0.1 或更小。
   - **還好**：如果佈局移動分數大於 0.1 但 比 0.25 或更小。
   - **不好**：如果版面移動分數超過 0.25。

- **至下次繪製的互動**：此功能可評估頁面對使用者互動的反應速度，考慮使用者造訪頁面期間頁面回應按選、點選和鍵盤輸入所需的時間。最終值是觀察到的最久互動，且忽略任何異常。「至下次繪製的互動」的效能指標分類如下：
   - **很好**：如果使用者兩個動作之間的持續時間為 200 毫秒 或更短。
   - **還好**：如果持續時間超過 200 毫秒但小於等於 500 毫秒。
   - **不好**：如果持續時間超過 500 毫秒。

## 可操作分析

透過分析這些量度，您可以發現以下機會：

- 簡化表單並減少欄位數量。
- 透過清晰的指示和標籤讓表單內容更加明確。
- 最佳化表單版面以提高行動裝置的回應能力。
- 解決表單載入速度緩慢的技術問題。

透過關注這些方面，您可以建立更易於使用的表單，並鼓勵訪客填寫表單，最終實現更高的轉換率。


