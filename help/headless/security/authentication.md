---
title: 針對內容片段之遠端 AEM GraphQL 查詢的驗證
description: 瞭解遠端AEM GraphQL查詢所需的驗證，以確保Headless內容傳送的安全。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 88%

---

# 針對內容片段之遠端 AEM GraphQL 查詢的驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[用於內容片段傳遞的 Adobe Experience Manager as a Cloud Service (AEM) GraphQL API](/help/headless/graphql-api/content-fragments.md) 的主要使用案例是接受協力廠商應用程式或服務的遠端查詢。這些遠端查詢可能需要經過驗證的API存取，以保護Headless內容傳送。

>[!NOTE]
>
>對於測試和開發，您還可以使用 [GraphiQL 介面](/help/headless/graphql-api/graphiql-ide.md)直接存取 AEM GraphQL API。

為進行驗證，協力廠商服務需要[擷取存取權杖](#retrieving-access-token)，然後可[用於 GraphQL 要求](#use-access-token-in-graphql-request)。

## 擷取存取權杖 {#retrieving-access-token}

如需完整詳細資訊，請參閱[產生伺服器端 API 的存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

## 在 GraphQL 要求中使用存取權杖 {#use-access-token-in-graphql-request}

協力廠商服務若要連接 AEM 執行個體，則需要有&#x200B;*存取權杖*。然後，服務必須將此權杖加入到 POST 要求的 `Authorization` 標頭中。

例如，GraphQL 授權標頭：

```xml
Authorization: Bearer <access_token>
```

## 權限要求 {#permission-requirements}

所有使用存取權杖的要求實際上將&#x200B;*由產生權杖的使用者帳戶發出*。

這表示您需要檢查該帳戶是否具有執行 GraphQL 查詢所需的權限。

您可以在本機執行個體上使用 GraphiQL 來檢查這一點。您可以在[這裡](/help/headless/security/permissions.md)找到更多有關權限的詳細資訊。
