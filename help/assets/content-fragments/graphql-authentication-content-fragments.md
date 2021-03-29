---
title: 內容片段的AEM遠程GraphQL查詢驗證
description: 瞭解遠程GraphQL查詢AEM的驗證，以確保無頭內容發送的安全。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 對內容片AEM段{#authentication-for-remote-aem-graphql-queries-on-content-fragments}的遠程GraphQL查詢的驗證

[作為Cloud Service(AEM)GraphQL API（用於內容片段傳送）的](/help/assets/content-fragments/graphql-api-content-fragments.md)Adobe Experience Manager的主要使用案例是接受來自第三方應用程式或服務的遠程查詢。 這些遠端查詢可能需要經過驗證的API存取，以確保無頭內容傳送的安全。

>[!NOTE]
>
>對於測試和開發，您還可以使AEM用[GraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)介面直接訪問GraphQL API。

為了驗證，第三方服務需要使用[存取Token](#access-token)，然後該[可用於GraphQL請求](#use-access-token-in-graphql-request)。

## 檢索訪問Token {#retrieving-access-token}

如需完整詳細資訊，請參閱[產生伺服器端API的存取權杖。](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)

## 在GraphQL請求{#use-access-token-in-graphql-request}中使用訪問Token

對於要與實例連接的第AEM三方服務，它需要&#x200B;*訪問Token*。 然後，服務必須將此Token新增至POST請求的`Authorization`標題。

例如，GraphQL授權標題：

```xml
Authorization: Bearer <access_token>
```

## 權限要求{#permission-requirements}

使用存取Token提出的所有請求實際上將由產生Token *的使用者帳戶發出*。

這表示您需要檢查帳戶是否具有運行GraphQL查詢所需的權限。

可以通過在本地實例上使用GraphiQL來檢查此問題。
