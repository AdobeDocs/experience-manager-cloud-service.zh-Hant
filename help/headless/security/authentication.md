---
title: 針對內容片段之遠端 AEM GraphQL 查詢的驗證
description: 了解必須對遠程 Adobe Experience Manager GraphQL 查詢執行的驗證，以確保 Headless 內容傳遞的安全。
feature: Headless, Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 96%

---

# 針對內容片段之遠端 AEM GraphQL 查詢的驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[用於內容片段傳遞的 Adobe Experience Manager as a Cloud Service (AEM) GraphQL API](/help/headless/graphql-api/content-fragments.md) 的主要使用案例是接受協力廠商應用程式或服務的遠端查詢。這些遠端查詢可能需要經驗證的 API 存取權，以確保 Headless 內容傳遞的安全。

>[!NOTE]
>
>對於測試和開發，您還可以使用 [GraphiQL 介面](/help/headless/graphql-api/graphiql-ide.md)直接存取 AEM GraphQL API。

為進行驗證，協力廠商服務必須[擷取存取權杖](#retrieving-access-token)，然後可[用於 GraphQL 要求](#use-access-token-in-graphql-request)。

## 擷取存取權杖 {#retrieving-access-token}

如需完整詳細資訊，請參閱[產生伺服器端 API 的存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

## 在 GraphQL 要求中使用存取權杖 {#use-access-token-in-graphql-request}

協力廠商服務若要連接 AEM 執行個體，則必須有&#x200B;*存取權杖*。然後，服務必須將此權杖加入到 POST 要求的 `Authorization` 標頭中。

例如，GraphQL 授權標頭：

```xml
Authorization: Bearer <access_token>
```

## 權限要求 {#permission-requirements}

所有使用存取權杖的要求是&#x200B;*由產生權杖的使用者帳戶發出*。

此使用者帳戶表示您必須檢查該帳戶是否具有執行 GraphQL 查詢所需的權限。

您可以在本機執行個體上使用 GraphiQL 來檢查這些權限。如需更多詳細資料，請參閱[Headless內容的許可權考量事項](/help/headless/security/permissions.md)。
