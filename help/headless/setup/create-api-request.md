---
title: 建立 API 要求 - Headless 設定
description: 了解如何使用 GraphQL API 無周邊傳遞內容片段，以及如何使用 AEM Assets REST API 管理內容片段。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 98%

---

# 建立 API 要求 - Headless 設定 {#accessing-delivering-content-fragments}

了解如何使用 GraphQL API 無周邊傳遞內容片段，以及如何使用 AEM Assets REST API 管理內容片段。

## 什麼是 GraphQL 和 Assets REST API？ {#what-are-the-apis}

[現在您已經建立一些內容片段，](create-content-fragment.md)您可以使用 AEM 的 API 無周邊傳遞內容片段。

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) 允許您建立存取和傳遞內容片段的要求。這個 API 提供了一組最強大的功能來查詢和取用內容片段內容。
   * 若要使用，[需要在 AEM 中定義和啟用端點](/help/headless/graphql-api/graphql-endpoint.md)，如果需要，[安裝 GraphiQL 介面](/help/headless/graphql-api/graphiql-ide.md)。
* [Assets REST API](/help/assets/content-fragments/assets-api-content-fragments.md) 允許您建立及修改內容片段 (和其他資產)。

本指南的其餘部分著重在 GraphQL 存取和內容片段傳遞。

## 啟用 GraphQL 端點 {#enable-graphql-endpoint}

必須建立 GraphQL 端點，才能使用 GraphQL API。

1. 導覽至&#x200B;**工具**、**一般**，然後選取 **GraphQL**。
1. 選擇 **建立**。
1. **建立新的 GraphQL 端點**&#x200B;對話框隨即開啟。您可以在這裡指定：
   * **名稱**：端點名稱，您可以輸入任何文字。
   * **使用以下方式提供的 GraphQL 結構描述**：使用下拉選單選取所需的設定。
1. 使用&#x200B;**建立**&#x200B;確認。
1. 主控台現在將根據之前建立的設定顯示&#x200B;**路徑**。這是用於執行 GraphQL 查詢的路徑。

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

更多有關啟用 [GraphQL 端點的詳細資訊位於此處](/help/headless/graphql-api/graphql-endpoint.md)。

## 使用 GraphQL 和 GraphiQL 查詢內容

資訊架構師需要為其通道端點設計查詢來傳遞內容。 通常只需要為每個模型的每個端點考慮一次這些查詢。出於本快速入門指南的目的，我們只需要建立一個。

GraphiQL 是包含在您 AEM 環境中的 IDE，在[設定您的端點](#enable-graphql-endpoint)後，即可存取/看見它。

1. 登入 AEM as a Cloud Service 並存取 GraphiQL 介面：

   您可以從以下任一方式存取查詢編輯器：

   * **工具** -> **一般** -> **GraphQL 查詢編輯器**
   * 直接；例如 `http://localhost:4502/aem/graphiql.html`

1. GraphiQL IDE 是 GraphQL 的瀏覽器內查詢編輯器。您可以用來建立查詢以擷取內容片段，以將其作為 JSON 以無周邊方式傳遞。
   * 右上角的下拉選單允許您選取端點。
   * 最左側的面板列出持續性查詢 (如果可用)
   * 中間偏左的面板允許您建立查詢。
   * 中間偏右面板顯示結果。
   * 查詢編輯器具有程式碼完成和快速鍵功能，可輕鬆執行查詢。

   ![GraphiQL 編輯器](../assets/graphiql.png)

1. 假設我們建立的模型名為 `person`，其中包含欄位 `firstName`、`lastName` 和 `position`，我們可以建立一個簡單的查詢來擷取內容片段的內容。

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
   ![GraphiQL 查詢](../assets/graphiql-query.png)

1. 按一下&#x200B;**執行查詢**&#x200B;按鈕或使用 `Ctrl-Enter` 快速鍵，右側面板將以 JSON 格式顯示結果。
   ![GraphiQL 結果](../assets/graphiql-results.png)

1. 按一下頁面右上角的&#x200B;**文件**連結可顯示內文中文件，協助您建立適合您自己模型的查詢。
   ![GraphiQL 文件](../assets/graphiql-documentation.png)

GraphQL 支援結構化查詢，這些查詢不僅可以針對特定資料集或個別資料物件，還可以傳遞物件的特定元素、巢狀結果、支援查詢變數等等。

GraphQL 可以避免反覆 API 要求以及過度傳遞，而是允許大量傳遞呈現作業所需的內容，作為對單一 API 查詢的回應。產生的 JSON 可用於將資料傳遞到其他網站或應用程式。

## 後續步驟 {#next-steps}

就是這樣！您現在對 AEM 無周邊內容管理有基本的了解。當然，還有更多資源可供您深入研究以全面了解可用的功能。

* **[內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)** - 詳細說明如何建立和管理內容片段
* **[AEM Assets HTTP API 支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md)** - 詳細說明如何運用 CRUD 操作 (建立、讀取、更新、刪除) 透過 HTTP API 直接存取 AEM 內容。
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - 詳細說明如何以無周邊方式傳遞內容片段
