---
title: 使用 API 整合建立 Salesforce Lead 物件
description: 了解如何使用 API 整合來建立 Salesforce Lead 物件。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: 在規則編輯器中整合 API、叫用服務增強功能
exl-id: 55835ffe-1b77-449b-b76d-16c0a343cf5c
hide: true
hidefromtoc: true
index: false
source-git-commit: 3a09a3fa9b8fb3dacef4c900979c4cc256551941
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 100%

---

# 使用 API 整合建立 Salesforce Lead 物件

此使用案例會逐步說明如何在 Salesforce 中使用 API 整合來建立 Lead。完成此流程後，您可以：

設定 ](https://help.salesforce.com/s/articleView?id=platform.ev_relay_create_connected_app.htm&type=5)Salesforce 中已連線的應用程式[來啟用安全的 API 存取權。

設定 CORS (跨來源資源共用) 來允許在網頁瀏覽器中執行的程式碼 (例如 JavaScript) 從特定來源與 Salesforce 進行通訊，將此來源新增至允許清單，如下所示：

![CORS](assets/salesforce-cors.png)

## 已連線應用程式設定

以下設定用於已連線的應用程式中。您可以根據自身需求指派 OAuth 範圍。
![connected-app-settings](assets/salesforce-connected-app-settings.png)

## 建立 API 整合

| 名稱 | 值 |
|--------------------------------|------------------|
| API URL | https://`<your-domain>`d.my.salesforce.com/services/data/v32.0/sobjects/Lead |
| 用戶端 ID | 專屬於您已連線的應用程式 |
| 用戶端密碼 | 專屬於您已連線的應用程式 |
| OAuth URL | https://login.salesforce.com/services/oauth2/authorize |
| 存取權杖 URL | https://`<your-domain>`/services/oauth2/token |
| 重新整理權杖 URL | https://`<your-domain>`/services/oauth2/token |
| 授權範圍 | api chatter_api full id openid refresh_token visualforce web |
| 授權標頭 | 授權持有人 |

![api-integration](assets/salesforce-api-integration-create-lead.png)

## 輸入和輸出參數

定義 API 呼叫的輸入參數，並使用以下 json 對應輸出參數

```json
{
    "id": "00QKY000001LyJR2A0",
    "success": true
}
```

![input-output](assets/create-lead-api-integration-input-output.png)

## 建立表單

使用通用編輯器建立簡易的自適應表單，來擷取 Lead 物件的詳細資訊，如下所示 
![lead-object-form](assets/create-lead.png)

使用規則編輯器處理「建立 Lead」核取方塊上的點按事件。將輸入參數對應至適當表單物件的值，如下所示。在 `leadid` 文字欄位物件中顯示新建立的 Lead 物件 ID
![rule-editor](assets/create-leade-rule-editor.png)

## 測試整合

- 預覽此表單

- 輸入一些有意義的值
- 選取「`Create Lead`」核取方塊來觸發 API 呼叫
- 新建立 Lead 物件的 Lead ID 已顯示於 `Lead ID` 文字欄位中。
