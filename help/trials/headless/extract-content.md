---
title: 通過 GraphQL API 擷取內容
description: 了解如何將內容片段和 GraphQL API 用作 Headless 內容管理系統。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: 2f4e38ba9bb2e0aab4dc126719a922fc983f8711
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 72%

---


# 通過 GraphQL API 擷取內容 {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="使用 GraphQL API 擷取內容"
>abstract="在此單元中，您將瞭解如何使用內容片段和 GraphQL API 當作 Headless 內容管理系統。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="啟動 GraphQL Explorer"
>abstract="GraphQL 提供查詢式的 API，允許外部客戶端應用程式使用單一 API 呼叫，以便查詢 AEM 所需的內容。按照本單元學習如何執行兩種不同類型的查詢。然後，您將瞭解如何從您在上一個單元中建立的內容片段擷取內容。 <br><br>點選下方，在新標籤中啟動該單元。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="幹得好！您已經瞭解關於兩種基本類型的查詢，以及如何查詢您自己的內容。 您現在瞭解如何使用 AEM GraphQL API 建立有效率的查詢，以您應用程式預期的格式提供內容。"
>abstract=""

## 查詢範例內容清單 {#list-query}

您先從新分頁中的 GraphQL Explorer 開始。 您可以針對 Headless 內容建置和驗證查詢，再使用它們為您的應用程式或網站中的內容提供支援。

1. 您的 AEM Headless 試用版附有一個預先載入了內容片段的端點，您可以從中擷取內容以進行測試。 記得選取「**AEM 示範資產**」端點 (從編輯器右上方的「**端點**」下拉式清單中選取)。

1. 為預先載入的 **AEM 示範資產**&#x200B;端點的清單查詢複製以下程式碼片段。清單查詢將傳回使用特定內容片段模式的所有內容清單。 詳細目錄和類別頁面通常使用這種查詢格式。

   ```text
   {
    adventureList {
     items {
       _path
       title
       price
       tripLength
       primaryImage {
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

1. 貼上複製的程式碼，以取代查詢編輯器中的現有內容。

1. 貼上後，在查詢編輯器左上方按一下「**播放**」按鈕以執行查詢。

1. 結果將顯示在右側面板中 (在查詢編輯器旁邊)。 如果查詢不正確，右側面板中會出現錯誤。

   ![清單查詢](assets/do-not-localize/list-query-1-3-4-5.png)

您剛剛驗證了所有內容片段完整清單的清單查詢。 此過程有助於確保查詢的回應符合您應用程式的預期，且結果會說明您的應用程式和網站將如何擷取在 AEM 建立的內容。

>[!NOTE]
>
>如果您無法選取 **AEM示範資產** 從下拉式清單中的端點，請聯絡Adobe客戶服務，或前往 [AEM試用Slack管道。](https://adobe-dx-support.slack.com/)

## 查詢範例內容指定片段 {#bypath-query}

執行 byPath 查詢可讓您擷取特定內容片段的內容。 產品詳細資訊頁面，以及著重在通常需要這類查詢的一組特定內容頁面。

1. 為預先載入的 **AEM 示範資產**&#x200B;端點的 byPath 查詢複製以下程式碼片段。

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
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

1. 貼上複製的程式碼，以取代查詢編輯器中的現有內容。

1. 貼上後，在查詢編輯器左上方按一下「**播放**」按鈕以執行查詢。

1. 結果將顯示在右側面板中 (在查詢編輯器旁邊)。 如果查詢不正確，右側面板中會出現錯誤。

   ![byPath 查詢結果](assets/do-not-localize/bypath-query-2-3-4.png)

您剛剛驗證了 byPath 查詢，以擷取由該片段的路徑標識的特定內容片段。

## 查詢自己的內容 {#own-queries}

您現在已經進行了兩種主要類型的查詢，您可以準備查詢自己的內容了。

1. 若要針對您自己的內容片段進行查詢，請將端點從「**AEM 示範資產**」資料夾變更為「**您的專案**」資料夾。

1. 刪除查詢編輯器中的所有現有內容。然後，輸入左方括號 `{` 並按 Ctrl+Space 或 Option+Space，可獲得端點中定義的模式自動完成清單。 從選項中選取您建立且以 `List` 結尾的模式。

   ![開始自訂查詢](assets/do-not-localize/custom-query-1-2.png)

1. 為您選取的內容片段模式定義查詢應包含的項目。 再次輸入左方括號 `{`，然後按 Ctrl+Space 或 Option+Space 以獲得自動完成清單。從選項中選取 `items`。

1. 在工作時，您可以點選或按一下「**修飾**」按鈕，自動格式化您的程式碼以便更易於閱讀。

1. 完成後，在查詢編輯器左上方點選或按一下「**播放**」按鈕以進行查詢。編輯器會自動完成`items`並執行查詢。

1. 結果將顯示在右側面板中 (在查詢編輯器旁邊)。

   ![執行自訂查詢](assets/do-not-localize/custom-query-3-4-5-6.png)

這就是將您的內容傳送至全管道數位體驗的方式。

## 持續查詢 {#persisted-queries}

持續查詢是將GraphQL API公開給用戶端應用程式的偏好機制。 保存查詢後，可使用GET請求進行請求，並快取以便快速檢索。

您將建立一個持續查詢，其中包含您要從用戶端應用程式使用的資料。

1. 您將使用先前建立為內容片段的資料，因此請確定 **您的專案** 在中選取端點 **端點** 編輯器右上角的下拉式功能表。

1. 複製下列程式碼片段。

   ```text
      {
      adventureList {
       items {
         title
         description {
           plaintext
         }
         title
         price
         image {
           ... on ImageRef {
             _publishUrl
             mimeType
           }
         }
       }
     }
   }
   ```

1. 貼上複製的程式碼，以取代查詢編輯器中的現有內容。

   >[!NOTE]
   >
   >如果您使用的欄位說明與先前模組中所述的不同，則需要更新此查詢中的欄位名稱。
   >
   >如先前所述，使用GraphQL自動完成（Ctrl+空格鍵或Option+空格鍵）功能，以協助識別可用屬性。

1. 貼上後，在查詢編輯器左上方按一下「**播放**」按鈕以執行查詢。

1. 結果將顯示在右側面板中 (在查詢編輯器旁邊)。 如果查詢不正確，右側面板中會出現錯誤。

   ![建立自己的查詢](assets/do-not-localize/own-query.png)

1. 對您的查詢滿意後，按一下 **另存新檔** 按鈕，以保留查詢。

1. 在 **查詢名稱** 快顯視窗，將查詢命名為 `adventure-list`.

1. 點選或按一下 **另存新檔**.

   ![保留查詢](assets/do-not-localize/persist-query.png)

1. 查詢會持續保存，如畫面底部的橫幅訊息所確認。 查詢現在也會顯示在視窗中持續存在的查詢的左側面板中。

1. 為了讓持續存在的查詢可以公開使用，它需要發佈，很像需要發佈內容片段的方式。 按一下 **發佈** 按鈕，以發佈查詢。

1. 橫幅通知會確認發佈。

您現在有新的持續查詢，其將僅包含您定義的特定屬性和格式。
