---
title: 存取及傳遞內容片段無頭快速入門手冊
description: 了解如何使用AEM Assets REST API管理內容片段，以及GraphQL API，以無周邊方式傳送內容片段內容。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# 存取和傳送內容片段無頭快速入門手冊{#accessing-delivering-content-fragments}

了解如何使用AEM Assets REST API管理內容片段，以及GraphQL API，以無周邊方式傳送內容片段內容。

## 什麼是GraphQL和Assets REST API?{#what-are-the-apis}

[現在您已建立一些內容片段，](create-content-fragment.md) 您可以使用AEM API無端傳送。

* [GraphQL API可](/help/assets/content-fragments/graphql-api-content-fragments.md) 讓您建立存取和傳送內容片段的請求。
* [Assets REST API可](/help/assets/content-fragments/assets-api-content-fragments.md) 讓您建立及修改內容片段（和其他資產）。

本指南的其餘部分將重點介紹GraphQL訪問和內容片段交付。

## 如何使用GraphQL {#how-to-deliver-a-content-fragment}傳送內容片段

資訊架構師需要為其管道端點設計查詢，才能傳送內容。 通常，每個模型的每個端點只需考慮這些查詢一次。 為了此快速入門手冊的目的，我們只需建立指南。

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. 以Cloud Service身分登入AEM並存取GraphiQL介面：
   * 例如：`https://<host>:<port>/content/graphiql.html`。

1. GraphiQL是GraphQL的瀏覽器內查詢編輯器。 您可以使用它建立查詢來擷取內容片段，以便以JSON形式直接傳送。
   * 左側面板可讓您建立查詢。
   * 右側面板顯示結果。
   * 查詢編輯器具有代碼完成功能和可輕鬆執行查詢的快捷鍵。
      ![GraphiQL編輯器](../assets/graphiql.png)

1. 假設我們建立的模型名為`person`，且欄位為`firstName`、`lastName`和`position`，我們可以建立簡單查詢來擷取內容片段的內容。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 在左側面板中輸入查詢。
   ![GraphiQL查詢](../assets/graphiql-query.png)

1. 按一下&#x200B;**執行查詢**&#x200B;按鈕或使用`Ctrl-Enter`快捷鍵，結果將顯示為右側面板中的JSON。
   ![GraphiQL結果](../assets/graphiql-results.png)

1. 按一下頁面右上角的&#x200B;**Docs**連結，顯示內容內檔案，協助您建立可適應您自己模型的查詢。
   ![GraphiQL檔案](../assets/graphiql-documentation.png)

GraphQL啟用結構化查詢，這些查詢不僅可以定位特定的資料集或單個資料對象，還可以提供對象的特定元素、嵌套結果、對查詢變數的支援等。

GraphQL可避免迭代API要求以及過度傳送，而可大量傳送要求，以回應單一API查詢，即可呈現所需的內容。 產生的JSON可用來傳送資料至其他網站或應用程式。

## 後續步驟{#next-steps}

就這樣！ 您現在對AEM中無頭式內容管理有了基本的了解。 當然，您還可以透過更多資源更進一步深入了解可用功能。

* **設定瀏覽器**  — 如需AEM設定瀏覽器的詳細資訊
* **[內容片段](/help/assets/content-fragments/content-fragments.md)**  — 如需建立和管理內容片段的詳細資訊
* **[AEM Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)**  — 如需透過CRUD操作（建立、讀取、更新、刪除）直接透過HTTP API存取AEM內容的詳細資訊
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  — 了解如何無條件傳送內容片段的詳細資訊
