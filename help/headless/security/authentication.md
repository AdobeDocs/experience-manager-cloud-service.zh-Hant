---
title: 針對內容片段之遠端 AEM GraphQL 查詢的驗證
description: 瞭解遠端Adobe Experience Manager GraphQL查詢所需的驗證，以確保Headless內容傳送的安全。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 26%

---

# 針對內容片段之遠端 AEM GraphQL 查詢的驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

的主要使用案例 [用於內容片段傳送的Adobe Experience Manager as a Cloud Service (AEM) GraphQL API](/help/headless/graphql-api/content-fragments.md) 是接受來自協力廠商應用程式或服務的遠端查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護Headless內容傳送。

>[!NOTE]
>
>若要進行測試和開發，您也可以使用直接存取AEM GraphQL API [GraphiQL介面](/help/headless/graphql-api/graphiql-ide.md).

針對驗證，協力廠商服務必須 [擷取存取Token](#retrieving-access-token) 然後可以 [用於GraphQL請求](#use-access-token-in-graphql-request).

## 擷取存取權杖 {#retrieving-access-token}

另請參閱 [為伺服器端API產生存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 以取得完整詳細資訊。

## 在 GraphQL 要求中使用存取權杖 {#use-access-token-in-graphql-request}

協力廠商服務若要連線至AEM執行個體，必須具備 *存取Token*. 然後，服務必須將此權杖加入到 POST 要求的 `Authorization` 標頭中。

例如，GraphQL 授權標頭：

```xml
Authorization: Bearer <access_token>
```

## 權限要求 {#permission-requirements}

使用存取權杖提出的所有請求都會發出 *由產生Token的使用者帳戶設定*.

此使用者帳戶表示您必須檢查該帳戶是否擁有執行GraphQL查詢所需的許可權。

您可以在本機執行個體上使用GraphiQL來檢查這些許可權。 您可以在[這裡](/help/headless/security/permissions.md)找到更多有關權限的詳細資訊。
