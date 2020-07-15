---
title: Adobe AEM Target HTTP視窗
description: 'Adobe AEM Target HTTP視窗 '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# 簡介 {#introduction}

本頁說明Adobe AEM Target HTTP視窗中顯示的可設定參數。

## 參數 {#parameters}

![目標HTTP窗](assets/httpwindow.png "口目標HTTP窗口")

該窗口包含以下可配置參數：

| 參數 | 說明 |
|---|---|
| Adobe Target API URL | Adobe Target API的URL。 |
| 啟用絕對URL | 判斷是否使用URL的主機部分或完整URL。 如果您要使用完整（未刪除的）URL，請啟用核取方塊。 預設情況下，複選框處於禁用狀態。 |
| 連線逾時 | 建立連線之前的逾時（以毫秒為單位）。 預設值為60000毫秒。 值0被解釋為無限超時。 |
| 通訊端逾時 | 等待資料或兩個連續資料包之間最長閒置時間的超時（毫秒）。 預設值為30000毫秒。 |
| Adobe Target Recommendations URL取代規則運算式Token | 控制Adobe Target端點URL中需要取代的Token，以指向Target Recommandations API URL。 |
| Adobe Target Recommendations URL取代為Token | 取代上述參數中所述的regex，因此產生的URL將指向Target Recommandations API。 |
