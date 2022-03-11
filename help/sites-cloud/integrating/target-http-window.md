---
title: AdobeAEM目標HTTP窗口
description: 'AdobeAEM目標HTTP窗口 '
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# 簡介 {#introduction}

本頁介紹Adobe目標HTTP窗口中AEM的可配置參數。

## 參數 {#parameters}

![目標HTTP窗口](assets/httpwindow.png "目標HTTP窗口")

該窗口包含以下可配置參數：

| 參數 | 說明 |
|---|---|
| Adobe TargetAPI URL | Adobe TargetAPI的URL。 |
| 啟用絕對URL | 確定是使用URL的主機部分還是使用完整URL。 如果要使用完整（未刪除）URL，請啟用複選框。 預設情況下，複選框處於禁用狀態。 |
| 連線逾時 | 建立連接之前的超時（毫秒）。 預設值為60000毫秒。 值0被解釋為無限超時。 |
| 通訊端逾時 | 等待資料或兩個連續資料包之間最大非活動時間的超時（毫秒）。 預設值為30000毫秒。 |
| Adobe TargetRecommendationsURL替換規則運算式令牌 | 控制需要替換以指向目標重定向API URL的Adobe Target終結點URL中的令牌。 |
| Adobe TargetRecommendationsURL替換為令牌 | 替換上述參數中描述的規則運算式，因此生成的URL將指向「目標重構API」。 |
