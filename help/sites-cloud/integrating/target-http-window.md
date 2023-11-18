---
title: AdobeAEM Target HTTP視窗
description: AdobeAEM Target HTTP視窗
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 4%

---


# 簡介 {#introduction}

此頁面說明AdobeAEM Target HTTP視窗中顯示的可設定引數。

## 參數 {#parameters}

![目標HTTP視窗](assets/httpwindow.png "目標HTTP視窗")

此視窗包含下列可設定的引數：

| 參數 | 說明 |
|---|---|
| ADOBE TARGET API URL | Adobe Target API URL。 |
| 啟用絕對URL | 決定是否要使用URL的主機部分或完整URL。 如果您想要使用完整的（未刪節的） URL，請啟用核取方塊。 預設會停用核取方塊。 |
| 連線逾時 | 建立連線前的逾時時間（毫秒）。 預設值為60000毫秒。 0值會解譯為無限逾時。 |
| 通訊端逾時 | 等待資料的逾時時間，或兩個連續資料封包之間的最長閒置時間（毫秒）。 預設值為30000毫秒。 |
| Adobe Target Recommendations URL取代規則運算式權杖 | 控制Adobe Target端點URL中必須取代以指向Target Recommandations API URL的權杖。 |
| Adobe Target Recommendations URL取代為Token | 以上引數中描述的規則運算式取代，因此產生的URL會指向Target Recommandations API。 |
