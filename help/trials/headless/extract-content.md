---
title: 通過 GraphQL API 擷取內容
description: 了解如何將內容片段和 GraphQL API 用作 Headless 內容管理系統。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 44%

---


# 通過 GraphQL API 擷取內容 {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="使用 GraphQL API 擷取內容"
>abstract="在本模組中，您將了解如何使用內容片段和GraphQL API作為無頭式內容管理系統。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="啟動 GraphQL Explorer"
>abstract="GraphQL 提供查詢式的 API，允許外部客戶端應用程式使用單一 API 呼叫，以便查詢 AEM 所需的內容。請依照此模組，了解如何執行兩種不同的查詢類型。 接著，了解如何從您在上一個模組中建立的內容片段擷取內容。<br><br>按一下下方的，在新索引標籤中啟動此模組。"
>additional-url="https://video.tv.adobe.com/v/328618" text="擷取內容簡介影片"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="幹得好！ 您已經了解關於兩種基本類型的查詢以及如何查詢您自己的內容。 您現在已了解如何使用AEM GraphQL API，以應用程式預期的格式來建立傳送內容的有效查詢。"
>abstract=""

## 查詢範例內容清單 {#list-query}

按一下 **啟動GraphQL Explorer** 按鈕會在新標籤中開啟GraphQL Explorer。

![GraphQL 查詢編輯器](assets/extract-content/query-editor.png)

使用GraphQL Explorer時，您可以先針對無頭式內容建立和驗證查詢，再使用無頭式內容來支援應用程式或網站中的內容。 讓我們看看是怎麼做的！

1. 您的AEM無頭試用版隨附預先載入內容片段的端點，您可從中擷取內容，以用於測試用途。 選取 **AEM示範資產** 從 **端點** 編輯器右上角的下拉式功能表。

   ![選取端點](assets/extract-content/select-endpoint.png)

1. 為預先載入的清單查詢複製下列程式碼片段 **AEM示範資產** 端點。 清單查詢會傳回使用特定內容片段模型的所有內容清單。 詳細目錄和類別頁面通常使用這種查詢格式。

   ```text
   {
       adventureList {
         items {
            _path
            adventureTitle
            adventurePrice
            adventureTripLength
            adventurePrimaryImage {
              ... on ImageRef {
               _path
               mimeType
               width
               height
             }
           }
         }
      }
    }
   ```

1. 貼上複製的程式碼，取代查詢編輯器中的現有內容。

   ![清單查詢](assets/extract-content/list-query.png)

1. 貼上後，在查詢編輯器左上方按一下「**播放**」按鈕以執行查詢。

1. 結果會顯示在查詢編輯器旁的右側面板中。 如果查詢不正確，右側面板中會出現錯誤。

   ![列出查詢結果](assets/extract-content/list-query-results.png)

您剛剛驗證了清單查詢以取得所有內容片段的完整清單。 此過程有助於確保查詢的回應符合您應用程式的預期，且結果會說明您的應用程式和網站將如何擷取在 AEM 建立的內容。

## 查詢特定範例內容 {#bypath-query}

執行byPath查詢可讓您擷取特定內容片段的內容。 產品詳細資訊頁面，以及著重在通常需要這類查詢的一組特定內容頁面。讓我們看看它如何運作！

1. 為預先載入的byPath查詢複製下列程式碼片段 **AEM示範資產** 端點。

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         adventureTitle
         adventureDescription {
           json
         }
         adventurePrimaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. 貼上複製的程式碼，取代查詢編輯器中的現有內容。

   ![byPath 查詢](assets/extract-content/bypath-query.png)

1. 貼上後，在查詢編輯器左上方按一下「**播放**」按鈕以執行查詢。

1. 結果會顯示在查詢編輯器旁的右側面板中。 如果查詢不正確，右側面板中會出現錯誤。

   ![byPath 查詢結果](assets/extract-content/bypath-query-results.png)

您剛剛驗證了byPath查詢，以擷取該片段路徑所識別的特定內容片段。

## 查詢您自己的內容 {#own-queries}

現在您已執行兩種主要查詢類型，您可以查詢自己的內容了！

1. 若要針對您自己的內容片段進行查詢，請將端點從「**AEM 示範資產**」資料夾變更為「**您的專案**」資料夾。

   ![選取您自己的端點](assets/extract-content/select-endpoint.png)

1. 刪除查詢編輯器中的所有現有內容。 然後鍵入開括弧 `{` 和按Ctrl+空格鍵或Option+空格鍵以自動完成端點中定義的模型清單。 選取您建立的結尾於 `List` 中。

   ![在查詢編輯器中自動完成模式](assets/extract-content/auto-complete-models.png)

1. 為您選取的內容片段模型定義查詢應包含的項目。 再次輸入左方括號 `{`，然後按 Ctrl+Space 或 Option+Space 以獲得自動完成清單。選擇 `items` 中。

   ![在查詢編輯器中自動完成項目](assets/extract-content/auto-complete-items.png)

1. 為您選取的內容片段模式定義查詢應包含的欄位。 再鍵入開括弧 `{`，然後按Ctrl+空格鍵或Option+空格鍵以自動完成「內容片段」模型中可用欄位的清單。 從清單中選取您希望從模式中選取的欄位。

   ![在查詢編輯器中自動完成欄位](assets/extract-content/auto-complete-fields.png)

1. 用逗號 (`,`) 或空格分隔多個欄位，然後再次按 Ctrl+Space 或 Option+Space 以選擇其他欄位。

1. 在工作時，您可以點選或按一下「**修飾**」按鈕，自動格式化您的程式碼以便更易於閱讀。

   ![修飾](assets/extract-content/prettify.png)

1. 完成後，在查詢編輯器左上方點選或按一下「**播放**」按鈕以進行查詢。

   ![您自己的查詢結果](assets/extract-content/custom-query-results.png)

1. 結果會顯示在查詢編輯器旁的右側面板中。

這就是將您的內容傳送至全頻道數位體驗的方式。
