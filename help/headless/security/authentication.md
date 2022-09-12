---
title: 內容片段的遠端AEM GraphQL查詢驗證
description: 了解遠端AEM GraphQL查詢所需的驗證，以保護無周邊內容的傳送安全。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 內容片段的遠端AEM GraphQL查詢驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

主要使用案例 [Adobe Experience Manager as a Cloud Service(AEM)用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md) 接受來自第三方應用程式或服務的遠程查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護無頭式內容傳送的安全。

>[!NOTE]
>
>若要進行測試和開發，您也可以直接使用 [GraphiQL介面](/help/headless/graphql-api/graphiql-ide.md) 介面。

針對驗證，第三方服務需要 [擷取存取權杖](#retrieving-access-token)，則 [用於GraphQL請求](#use-access-token-in-graphql-request).

## 擷取存取權杖 {#retrieving-access-token}

請參閱 [產生伺服器端API的存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 以取得完整詳細資訊。

## 在GraphQL請求中使用存取權杖 {#use-access-token-in-graphql-request}

若要讓協力廠商服務連線至AEM執行個體，它必須具備 *存取權杖*. 然後，服務必須將此Token新增至 `Authorization` 標題。

例如， GraphQL授權標題：

```xml
Authorization: Bearer <access_token>
```

## 權限需求 {#permission-requirements}

使用存取權杖提出的所有請求實際上都會執行 *由產生代號的使用者帳戶*.

這表示您需要檢查帳戶是否具備執行GraphQL查詢所需的權限。

您可以在本機執行個體上使用GraphiQL來檢查此問題。 有關的更多詳細資訊 [可在此處找到權限](/help/headless/security/permissions.md).
