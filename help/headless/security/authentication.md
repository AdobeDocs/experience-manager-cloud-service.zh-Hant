---
title: 內容片段AEM上遠程GraphQL查詢的驗證
description: 瞭解遠程GraphQL查詢所需AEM的身份驗證，以確保無頭內容交付的安全。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 內容片段AEM上遠程GraphQL查詢的驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

C.S.的主要使用案例 [Adobe Experience Manager as a Cloud Service(AEM)用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md) 接受來自第三方應用程式或服務的遠程查詢。 這些遠程查詢可能需要經過驗證的API訪問，以確保無頭內容傳送的安全。

>[!NOTE]
>
>為進行測試和開發，您還可以AEM使用 [GraphiQL介面](/help/headless/graphql-api/graphiql-ide.md) 。

為驗證第三方服務需要 [檢索訪問令牌](#retrieving-access-token)，然後 [在GraphQL請求中使用](#use-access-token-in-graphql-request)。

## 檢索訪問令牌 {#retrieving-access-token}

請參閱 [為伺服器端API生成訪問令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 的雙曲餘切值。

## 在GraphQL請求中使用訪問令牌 {#use-access-token-in-graphql-request}

對於與實例連接的第AEM三方服務，它需要 *訪問令牌*。 然後，服務必須將此令牌添加到 `Authorization` POST請求的標題。

例如，GraphQL授權標頭：

```xml
Authorization: Bearer <access_token>
```

## 權限要求 {#permission-requirements}

使用訪問令牌發出的所有請求將實際發出 *生成令牌的用戶帳戶*。

這意味著您需要檢查帳戶是否具有運行GraphQL查詢所需的權限。

可以通過在本地實例上使用GraphiQL來檢查此項。 有關 [在此處可找到權限](/help/headless/security/permissions.md)。
