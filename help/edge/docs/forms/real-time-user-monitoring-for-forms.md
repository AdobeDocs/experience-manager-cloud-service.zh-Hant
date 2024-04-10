---
title: FormsEdge Delivery Services的即時使用者監控
description: Forms的Edge Delivery Services即時使用者監控涉及持續追蹤和分析使用者與表單的互動。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# FormsEdge Delivery Services的即時使用者監控

Adobe Experience Manager使用Real User Monitoring (RUM)來瞭解訪客與Adobe Experience Manager導向網站的互動。 它有助於診斷效能挑戰，並評估實驗效率。 Real User Monitoring使用取樣技術來維護訪客的隱私權，確保您造訪的網站不會收集任何個人資訊。 不允許將個人資料新增到RUM資料收集。 Adobe Experience Manager中的「即時使用者監控」可保留訪客隱私權，並將資料收集降至最低。

## 對Edge Delivery Services Forms使用即時使用者監控的優勢 {#advantages}

AEM會針對下列專案使用即時使用者監控：

* 找出並修正網站上的效能瓶頸。
* 若要預估客戶網站的頁面檢視次數，請執行下列步驟：
* 若要瞭解Adobe Experience Manager與相同頁面上的分析、目標定位或外部程式庫的互動，可增強相容性。

## 必要條件 

您可以存取以下URL來檢視Edge Delivery Services Forms的即時使用者監視儀表板： https://data.aem.live/?ext=forms

![Edge Delivery Services Forms的RUM登入畫面 ](/help/edge/assets/rum-login-screen.png)

若要登入FormsEdge Delivery Services的即時使用者監視儀表板，請輸入下列內容：
* **URL**：此URL專屬於使用者網站或網域。 使用者可以選擇篩選網站或網域，以根據其需求檢視控制面板。
* **網域金鑰**：使用者手動產生網域金鑰。 如需協助或查詢，請參閱 [產生RUM網域金鑰](https://aemcs-workspace.adobe.com/rum/generate-domain-key) 檔案。

### Edge Delivery Services Forms的即時使用者監視儀表板

在登入畫面中輸入URL和網域金鑰後，您就可以存取Edge Delivery Services Forms的即時使用者監視儀表板。

下圖示範Edge Delivery ServicesForms的RUM控制面板：

![RUM Forms控制面板](/help/edge/assets/rum-forms-dashboard.png)

### Forms的RUM控制面板的不同關鍵量度 {#different-metrics-rum-dashboard-forms}

您可以使用以下關鍵量度來評估訪客與Adobe Experience Manager導向網站的互動：

* **表單檢視**：這是指定日期範圍內針對URL呈現的表單總數。
* **表單提交**：指定日期範圍內針對URL提交的表單總數。
* **最大內容油漆**：它顯示URL載入的速度，代表從使用者要求URL的那一刻起，轉譯檢視區中最大的內容元素所花的時間。 此最大內容元素可能是影像、影片或實質性的區塊層級文字元素。 URL載入速度的效能評等分類如下：
   * **好**：若載入時間為2.5秒或更短。
   * **確定**：如果載入時間超過2.5秒但4秒或更短。
   * **不良**：如果載入時間超過4秒

* **累計版面配置位移**：此量度會針對整個頁面生命週期中發生的每個非預期版面位移，測量所有個別版面位移分數的總和。 它在識別頁面效能方面扮演了至關重要的角色，因為當使用者嘗試與頁面元素互動時頁面元素發生變更，會導致使用者體驗不佳。 此分數從零到任何正數的範圍：零表示無位移，數字越高表示頁面上的版面位移越大。 用來評估版面配置班次分數的績效量度分類如下：

   * **好**：如果版面配置位移分數為0.1或更低。
   * **確定**：如果版面配置位移分數大於0.1但小於或等於0.25。
   * **不良**：如果版面配置位移分數超過0.25。

* **與下一個繪畫的互動**：它會評估頁面對使用者互動的回應速度，考量頁面在使用者造訪頁面期間回應點選、點選和鍵盤輸入所花費的時間。 最終值是觀察到的最長互動，不考慮任何異常。 「互動至下一個繪圖」的效能度量分類如下：
   * **好**：如果使用者動作之間的持續時間為200毫秒(ms)或更少。
   * **確定**：如果持續時間超過200毫秒但500毫秒或更短。
   * **不良**：如果持續時間超過500毫秒。

