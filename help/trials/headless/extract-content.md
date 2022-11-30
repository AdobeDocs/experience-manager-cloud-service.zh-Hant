---
title: 透過GraphQL API擷取內容
description: 了解如何將內容片段和GraphQL API作為無周邊的內容管理系統。
hidefromtoc: true
index: false
source-git-commit: a832ed1d81866a6470b47d8e30f5c242b10d1422
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---


# 透過GraphQL API擷取內容 {#extract-content}

到目前為止，在AEM Trials中， [建立您自己的內容片段模型](content-structure.md) 建立您自己的無頭內容 [內容片段。](create-content.md) 現在，您可以了解如何使用內容片段和GraphQL API，作為無周邊位置的內容管理系統，來傳遞您的內容。

GraphQL提供以查詢為基礎的API，讓外部用戶端應用程式只能透過單一API呼叫，查詢AEM所需的內容。

首先，您將學習如何執行兩種不同類型的查詢： **清單** 和 **byPath** 查詢。 接著，您將學習如何從您先前建立的內容片段擷取內容。 本檔案是互動式導覽的補充，涵蓋相同步驟，並視需要連結至其他資源。

>[!TIP]
>
>如果您想要進一步了解GraphQL API，請參閱 [「其他資源」部分](#additional-resources) 在本模組的結尾，請參閱GraphQL API指南。

## GraphQL Explorer {#graphql-explorer}

您可以在GraphQL資源管理器上啟動。 您可以在此針對無頭式內容建立和執行查詢。

![GraphQL查詢編輯器](assets/extract-content/query-editor.png)

如果您想在應用程式內指引之外自行導覽至GraphQL Explorer，請使用頁面左上角的Adobe圖示找到。 這會開啟AEM的全域導覽。 從這裡，您選擇 **工具** 標籤，然後 **一般** -> **GraphQL查詢編輯器**.

>[!TIP]
>
>如果您想進一步了解AEM中的導覽，請參閱 [「其他資源」部分](#additional-resources) ，以取得AEM基本處理的詳細資訊。

AEM試用版隨附預先載入內容的端點，您可從中擷取內容以用於測試用途。

![選擇端點](assets/extract-content/select-endpoint.png)

選取 **AEM示範資產** 從 **端點** 編輯器右上角的下拉式功能表（如果尚未執行）。

## 複製並運行清單查詢 {#list-query}

從簡單的清單查詢開始，了解如何運用AEM as a Cloud Service的GraphQL API運作方式。 此清單查詢範例將傳回使用特定內容片段模型的所有內容清單。 庫存和類別頁面通常使用此查詢格式。

1. 複製下列程式碼片段。

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

1. 然後，借由貼上複製的程式碼，取代查詢編輯器中的現有內容。

   ![清單查詢](assets/extract-content/list-query.png)

1. 貼上後，按一下 **播放** 按鈕，執行查詢。

1. 查詢成功執行後，結果會顯示在查詢編輯器旁的右側面板中。 如果查詢不正確，右側面板中會顯示錯誤。

   ![列出查詢結果](assets/extract-content/list-query-results.png)

您剛剛驗證了清單查詢以取得所有內容片段的完整清單。 此程式可協助確保回應符合應用程式的預期，結果可說明應用程式和網站如何擷取在AEM中建立的內容。

您的內容需要顯示的不同管道和平台現在可以使用此查詢或類似內容來擷取無頭內容。

## 複製並運行byPath查詢 {#bypath-query}

執行byPath查詢可讓您擷取特定內容片段的資產。 專注於特定內容集的產品詳細資料頁面和頁面通常需要此類型的查詢。

1. 複製下列程式碼片段。

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

1. 然後，借由貼上複製的程式碼，取代查詢編輯器中的現有內容。

   ![byPath查詢](assets/extract-content/bypath-query.png)

1. 貼上後，按一下 **播放** 按鈕，執行查詢。

1. 查詢成功執行後，結果會顯示在查詢編輯器旁的右側面板中。 如果查詢不正確，右側面板中會顯示錯誤。

1. 查詢成功執行後，結果會顯示在查詢編輯器旁的右側面板中。 如果查詢不正確，右側面板中會顯示錯誤。

   ![byPath查詢結果](assets/extract-content/bypath-query-results.png)

您剛剛驗證了清單查詢以取得所有內容片段的完整清單。 此程式可協助確保回應符合應用程式的預期，結果可說明應用程式和網站如何擷取在AEM中建立的內容。

您的內容需要顯示的不同管道和平台現在可以使用此查詢或類似內容來擷取無頭內容。

## 對您自己的內容執行查詢 {#own-queries}

現在您已經運行了兩種主要類型的查詢，您就可以針對自己建立的內容設定並運行查詢。

1. 若要對您自己的內容片段執行查詢，請變更 **AEM示範資產** 檔案夾 **您的專案** 檔案夾。

   ![選取您自己的端點](assets/extract-content/select-endpoint.png)

1. 首先，在查詢編輯器中選取並刪除所有現有內容。 然後鍵入開括弧 `{` 和按Ctrl+空格鍵或Option+空格鍵可自動完成內容片段模型中定義的模型清單。 選取您建立的結尾於 `List` 從清單中。

   ![在查詢編輯器中自動完成模型](assets/extract-content/auto-complete-models.png)

1. 為您選取的內容片段模型定義查詢應包含的項目。 同樣，鍵入開括弧 `{`，然後按Ctrl+空格鍵或Option+空格鍵以自動完成清單。 選擇 `items` 從清單中。

   ![在查詢編輯器中自動完成項目](assets/extract-content/auto-complete-items.png)

1. 為您選取的內容片段模型定義查詢應包含的欄位。 同樣，鍵入開括弧 `{`，然後按Ctrl+空格鍵或Option+空格鍵以自動完成「內容片段」模型中可用欄位的清單。 從清單中選取您希望的模型欄位。

   ![查詢編輯器中的自動完成欄位](assets/extract-content/auto-complete-fields.png)

1. 請使用逗號分隔多個欄位(`,`)或空格鍵，然後按Ctrl+空格鍵或Option+空格鍵以選取其他欄位。

1. 在您工作時，您可以點選或按一下 **美化** 按鈕以自動格式化程式碼，以便更輕鬆閱讀。

   ![美化](assets/extract-content/prettify.png)

1. 完成後，點選或按一下 **播放** 按鈕，以運行查詢。

   ![您自己的查詢結果](assets/extract-content/custom-query-results.png)

這是將內容傳遞至全通路數位體驗的方式。 請參閱 [「其他資源」部分](#additional-resources) 如需其他範例查詢，並了解GraphQL API的功能。

## 您已學會如何查詢內容！ {#conclusion}

幹得好！ 您已了解兩種基本的查詢類型以及如何查詢您自己的內容。 請務必查看 [「其他資源」部分](#additional-resources) 如需其他範例查詢，並了解GraphQL API的功能。

如果您想要了解擷取的內容之後如何用於自訂React應用程式，請務必檢閱模組 [自訂範例React應用程式中的內容。](customize-app.md)

您可以按一下，返回試用主螢幕 **解決方案** 按鈕，然後選擇 **Experience Manager**.

![導覽首頁](assets/extract-content/home.png)

## 其他資源 {#additional-resources}

如需內容片段和AEM的詳細資訊，請考慮檢閱此額外檔案。

* [GraphQL API指南](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/explore-graphql-api.html)
* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如何為新使用者導覽和使用AEM的檔案
* [學習如何搭配AEM使用GraphQL — 範例內容與查詢](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/sample-queries.html)
