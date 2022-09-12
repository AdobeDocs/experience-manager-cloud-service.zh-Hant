---
title: AdobeAEM Target HTTP視窗
description: AdobeAEM Target HTTP視窗
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# 簡介 {#introduction}

本頁面說明AdobeAEM Target HTTP視窗中顯示的可設定參數。

## 參數 {#parameters}

![目標HTTP窗口](assets/httpwindow.png "目標HTTP窗口")

該窗口包含以下可配置參數：

| 參數 | 說明 |
|---|---|
| Adobe Target API URL | Adobe Target API的URL。 |
| 啟用絕對URL | 判斷是否使用URL的主機部分或完整URL。 如果要使用完整（未刪除的）URL，請啟用此複選框。 依預設，核取方塊會停用。 |
| 連線逾時 | 建立連線前的逾時（毫秒）。 預設值為60000毫秒。 0值會解譯為無限逾時。 |
| 通訊端逾時 | 等待資料或兩個連續資料包之間最長閒置時間的超時（毫秒）。 預設值為30000毫秒。 |
| Adobe Target Recommendations URL取代Regex代號 | 控制需要取代的Adobe Target端點URL中的Token，以指向Target Recommandations API URL。 |
| Adobe Target Recommendations URL取代為Token | 取代上述參數中所述的規則運算式，因此產生的URL會指向Target Recommandations API。 |
