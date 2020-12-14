---
title: 存取和傳送內容片段無頭快速入門手冊
description: Assets REST API允許管理內容片段，而GraphQL API允許簡單無頭地傳送內容片段內容。
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 存取和傳送內容片段無頭快速入門手冊{#accessing-delivering-content-fragments}

Assets REST API允許管理內容片段，而GraphQL API允許簡單無頭地傳送內容片段內容。

## 什麼是GraphQL和Assets REST API?{#what-are-the-apis}

[現在您已建立一些內容片段，](create-content-fragment.md) 您可以使用AEM的API無端傳遞這些片段。

* [GraphQL ](/help/assets/content-fragments/graphql-api-content-fragments.md) API可讓您建立存取和傳送內容片段的請求。
* [「資產REST ](/help/assets/content-fragments/assets-api-content-fragments.md) API」可讓您建立和修改「內容片段」（和其他資產）。

本指南的其餘部分將重點介紹GraphQL訪問和內容片段交付。

## 如何使用GraphQL {#how-to-deliver-a-content-fragment}提供內容片段

資訊架構師將需要針對其通道端點設計查詢，以便傳遞內容。 通常，每個模型的每個端點只需考慮這些查詢一次。 為達到本快速入門手冊的目的，我們只需建立一本指南。

1. 以雲端服務的身分登入AEM，並從主功能表選擇「**工具->資產-> GraphQL**」
   * 或者，直接在`https://<host>:<port>/content/graphiql.html`開啟頁面。

1. GraphiQL是GraphQL的瀏覽器內查詢編輯器。 您可使用它來建立查詢以擷取內容片段，以JSON形式直接傳遞這些片段。
   * 左側面板可讓您建立查詢。
   * 右側面板會顯示結果。
   * 查詢編輯器具有代碼完成和熱鍵功能，以便輕鬆執行查詢。
      ![圖形QL編輯器](../assets/graphiql.png)

1. 假設我們建立的模型名為`person`（欄位`firstName`、`lastName`和`position`），我們可以建立簡單查詢來擷取內容片段的內容。

   ```text
   query {
     persons {
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

1. 按一下「執行查詢」按鈕或使用「**快速鍵」，結果會以JSON顯示在右側面板中。**`Ctrl-Enter`
   ![GraphiQL結果](../assets/graphiql-results.png)

1. 按一下頁面右上方的&#x200B;**Docs**連結，顯示內容相關檔案，協助您建立適合您自己機型的查詢。
   ![GraphiQL文檔](../assets/graphiql-documentation.png)

GraphQL可啟用結構化查詢，不僅可以定位特定的資料集或單個資料對象，還可以提供對象的特定元素、嵌套結果、支援查詢變數等。

GraphQL可避免重複的API要求以及過度傳送，而允許大量傳送呈現為單一API查詢回應所需的內容。 產生的JSON可用來將資料傳送至其他網站或應用程式。

## 後續步驟{#next-steps}

就這樣！ 您現在對AEM中的無頭內容管理有基本的瞭解。 當然，您還有更多資源可讓您更深入地瞭解可用功能。

* **設定瀏覽器** -如需AEM設定瀏覽器的詳細資訊
* **[內容片段](/help/assets/content-fragments/content-fragments.md)** -如需建立和管理內容片段的詳細資訊
* **[AEM Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)** -如需透過HTTP API直接存取AEM內容(透過CRUD作業（建立、讀取、更新、刪除）的詳細資訊
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)** -如需如何無故傳送內容片段的詳細資訊
