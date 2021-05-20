---
title: 內容片段的遠端AEM GraphQL查詢驗證
description: 了解遠端AEM GraphQL查詢所需的驗證，以保護無周邊內容的傳送安全。
feature: 內容片段，GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: dab4c9393c26f5c3473e96fa96bf7ec51e81c6c5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 對內容片段{#authentication-for-remote-aem-graphql-queries-on-content-fragments}進行遠端AEM GraphQL查詢的驗證

[Adobe Experience Manager as aCloud Service(AEM)內容片段傳送](/help/assets/content-fragments/graphql-api-content-fragments.md)的主要使用案例是接受來自第三方應用程式或服務的遠端查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護無頭式內容傳送的安全。

>[!NOTE]
>
>對於測試和開發，您還可以直接使用[GraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)介面訪問AEM GraphQL API。

驗證時，第三方服務需要[檢索訪問令牌](#retrieving-access-token)，該令牌隨後可以[用於GraphQL請求](#use-access-token-in-graphql-request)。

## 檢索訪問令牌{#retrieving-access-token}

如需完整詳細資訊，請參閱[產生伺服器端API的存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 。

## 在GraphQL請求{#use-access-token-in-graphql-request}中使用存取權杖

第三方服務若要與AEM執行個體連線，其必須有&#x200B;*存取Token*。 然後，服務必須將此Token新增至POST請求的`Authorization`標題。

例如， GraphQL授權標題：

```xml
Authorization: Bearer <access_token>
```

## 權限要求{#permission-requirements}

使用存取權杖提出的所有請求實際上會由產生權杖&#x200B;*的使用者帳戶提出*。

這表示您需要檢查帳戶是否具備執行GraphQL查詢所需的權限。

您可以在本機執行個體上使用GraphiQL來檢查此問題。
