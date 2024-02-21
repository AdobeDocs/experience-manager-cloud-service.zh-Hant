---
title: 建立經檢測適用 Universal Editor 的區塊
description: 了解如何在使用 Edge Delivery Services 專案進行的 AEM 製作環境中，建立經檢測適用 Universal Editor 的區塊。
source-git-commit: 40e404c743102f1de8b3d959597836f04f0c0fef
workflow-type: ht
source-wordcount: '1205'
ht-degree: 100%

---


# 建立經檢測適用 Universal Editor 的區塊 {#create-block}

了解如何在使用 Edge Delivery Services 專案進行的 AEM 製作環境中，建立經檢測適用 Universal Editor 的區塊。

{{aem-authoring-edge-early-access}}

## 先決條件 {#prerequisites}

本指南提供逐步說明，讓您了解如何在使用 Edge Delivery Services 專案進行的 AEM 製作環境中建立經檢測適用 Universal Editor 的區塊。內容包括新增元件、載入 Universal Editor 中的元件定義、發佈頁面、實施區塊裝飾和樣式、將變更引入生產以及進行變更驗證。完成本指南後，您可以為自己的專案建立和部署新區塊。

本指南需要具備使用 Edge Delivery Services 專案進行 AEM 製作及 Universal Editor 的知識。在開始執行本指南之前，您應該有 Edge Delivery Services 存取權並熟悉基本使用需知，包括：

* 您已完成 [Edge Delivery Service 教學課程。](/help/edge/developer/tutorial.md)
* 您有權存取 [AEM Cloud Service 沙箱。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* 您已[在同一沙箱環境中啟用 Universal Editor。](/help/implementing/universal-editor/getting-started.md)
* 您已完成「[使用 Edge Delivery Services 進行 AEM 製作的開發人員快速入門指南](/help/edge/edge-dev-getting-started.md)」指南。

本指南是以在「[使用 Edge Delivery Services 進行 AEM 製作的開發人員快速入門指南](/help/edge/edge-dev-getting-started.md)」指南中完成的工作為基礎。

## 為您的專案新增區塊 {#add-block}

在本指南中，您將建立一個區塊並在頁面上呈現令人難忘的引述。

為了簡化此範例，所有變更均針對專案儲存庫的 `main` 分支進行。當然，進行實際專案時[應該遵照開發最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)進行，在不同的分支上進行開發，並在合併到`main`之前透過提取請求檢查所有變更。

Adobe 建議您採用三階段方法來開發區塊：

1. 建立區塊的定義和模式、審查區塊，然後將區塊投入生產。
1. 使用新區塊建立內容。
1. 實施新區塊的裝飾和風格。

以下引述區塊範例即遵照此方法進行。

### 建立區塊定義和模式 {#create-block-model}

1. 將您在「[使用 Edge Delivery Services 進行 AEM 製作的開發人員快速入門指南](/help/edge/edge-dev-getting-started.md)」指南中建立的 GitHub 專案複製到本機，並在您選擇的編輯器中將其打開。

   * 此處使用 Microsoft 程式碼是為了說明目的。

   ![複製專案。](assets/create-block/clone.png)

1. 編輯專案根目錄下的 `component-definition.json` 檔案，為新引述區塊新增以下定義並儲存檔案。

   ```json
   {
     "title": "Quote",
     "id": "quote",
     "plugins": {
       "xwalk": {
         "page": {
           "resourceType": "core/franklin/components/block/v1/block",
           "template": {
             "name": "Quote",
             "model": "quote",
             "quote": "<p>Think, McFly! Think!</p>",
             "author": "Biff Tannen"
           }
         }
       }
     }
   }
   ```

   ![編輯 component-definitions.json 檔案以定義引述區塊](assets/create-block/component-definitions.png)

1. 編輯專案根目錄下的 `component-models.json` 檔案，為新引述區塊新增以下[模式定義](/help/implementing/universal-editor/field-types.md#model-structure)並儲存檔案。

   * 請參閱文件「[使用 Edge Delivery Services 專案進行 AEM 製作的內容模式](/help/edge/content-modeling.md)」，了解有關建立內容模式時需要考慮的重要事項詳細資訊。

   ```json
   {
     "id": "quote",
     "fields": [
        {
          "component": "text-area",
          "name": "quote",
          "value": "",
          "label": "Quote",
          "valueType": "string"
        },
        {
          "component": "text-input",
          "valueType": "string",
          "name": "author",
          "label": "Author",
          "value": ""
        }
      ]
   }
   ```

   ![編輯 component-models.json 檔案以定義引述區塊的模式](assets/create-block/component-models.png)

1. 編輯專案根目錄下的 `component-filters.json` 檔案，並將引述區塊新增至[篩選器定義](/help/implementing/universal-editor/customizing.md#filtering-components)中，以允許將該區塊新增至任何區段並且儲存檔案。

   ```json
   {
     "id": "section",
     "components": [
       "text",
       "image",
       "button",
       "title",
       "hero",
       "cards",
       "columns",
       "quote"
      ]
   }
   ```

   ![編輯 component-filters.json 檔案以定義引述區塊的篩選器](assets/create-block/component-filters.png)

1. 使用 git，將這些變更提交到您的 `main` 分支。

   * 提交至`main`僅是為了說明目的。[遵照最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)，並在實際專案工作中使用提取請求。

### 使用區塊建立內容。 {#create-content}

現在您的基本引述區塊已定義並提交給範例專案，您可以將引述區塊新增至現有頁面。

1. 在瀏覽器中，登入 AEM as a Cloud Service。[使用 Sites 控制台，](/help/sites-cloud/authoring/getting-started/basic-handling.md) 導覽至您在「[使用 Edge Delivery Services 進行 AEM 製作的開發人員快速入門指南](/help/edge/edge-dev-getting-started.md)」指南中建立的網站，然後選擇一個頁面。

   * 在本案例中，`index`是用於說明目的。

   ![在 Sites 控制台中選取索引頁面](assets/create-block/sites-console.png)

1. 點選或按一下控制台工具列中的「**編輯**」，Universal Editor 將會開啟。

   * 為了載入該頁面，您可能需要點選或按一下「**使用 Adob&#x200B;&#x200B;e 登入**」，並在 Universal Editor 中對 AEM 進行驗證。

1. 在 Universal Editor 中，選取一個區段。在屬性邊欄中，點選或按一下「**新增**」圖示，然後從選單中選取新的&#x200B;**引述** 區塊。

   *  **新增**&#x200B;圖示是一個加號。
   * 如果所選物件的藍色外框有一個標為「**區段**」的標記，表示您已選取了一個區段。
   * 在此範例中，在「**Lorem Ipsum**」標題上方輕輕點選或按一下，即可選取包含標題和 lorem ipsum 文字的區段。

   ![在 Universal Editor 中選取一個區段](assets/create-block/add-quote-block.png)

1. 頁面重新加載，且引述區塊將新增至所選區段的底部，以及成為 `component-definitions.json` 檔案中指定的預設內容。

   * 與任何其他區塊一樣，引述區塊可在原處或屬性邊欄中供選取和編輯。
   * 樣式將在下一步中套用。

   ![所選區段中包含新引述區塊的頁面](assets/create-block/quote-added.png)

1. 當您對引述內容感到滿意時，可以在 Universal Editor 工具列中點選或按一下「**發佈**」按鈕。

1. 導覽至已發佈的頁面，驗證內容是否已發佈。該連結類似 `https://<branch>--<repo>--<owner>.hlx.page`

   ![發佈的引述](assets/create-block/quote-published.png)

### 區塊的樣式 {#style-block}

現在您已經有了一個可用的引述區塊，您可以對區塊套用樣式。

1. 返回您的專案編輯器。

1. 在`blocks`檔案夾中，建立一個`quote`檔案夾。

   ![建立引述檔案夾](assets/create-block/new-folder.png)

1. 在新的`quote`檔案夾中，透過新增以下 JavaScript，新增一個 `quote.js` 檔案以實施區塊裝飾，然後儲存檔案。

   ```javascript
   export default function decorate(block) {
     const [quoteWrapper] = block.children;
   
     const blockquote = document.createElement('blockquote');
     blockquote.textContent = quoteWrapper.textContent.trim();
     quoteWrapper.replaceChildren(blockquote);
   }
   ```

   ![新增 JavaScript 以裝飾區塊](assets/create-block/quote-js.png)


1. 在`quote`檔案夾中，透過新增以下 CSS 程式碼，新增一個 `quote.css` 檔案以定義區塊樣式，然後儲存檔案。

   ```css
   .block.quote {
       background-color: #ccc;
       padding: 0 0 24px;
       display: flex;
       flex-direction: column;
       margin: 1rem 0;
   }
   
   .block.quote blockquote {
       margin: 16px;
       text-indent: 0;
   }
   
   .block.quote > div:last-child > div {
       margin: 0 16px;
       font-size: small;
       font-style: italic;
       position: relative;
   }
   
   .block.quote > div:last-child > div::after {
       content: "";
       display: block;
       position: absolute;
       left: 0;
       bottom: -8px;
       height: 5px;
       width: 30px;
       background-color: darkgray;
   }
   ```

   ![新增 CSS 以定義區塊樣式](assets/create-block/quote-css.png)

1. 使用 git，將這些變更提交到您的 `main` 分支。

   * 提交至`main`僅是為了說明目的。[遵照最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)，並在實際專案工作中使用提取請求。

1. 返回 Universal Editor 的瀏覽器標記，您可在此編輯專案頁面，並重新載入頁面以查看附有樣式的區塊。

1. 請參閱頁面上現在附有樣式的引述區塊。

   ![Universal Editor 中附有樣式的引述區塊](assets/create-block/quote-styled.png)

1. 導覽至已發佈的頁面，驗證變更是否已推至生產。該連結類似 `https://<branch>--<repo>--<owner>.hlx.page`

   ![已發布且附樣式的引述區塊](assets/create-block/quote-styled-published.png)

恭喜！您現在擁有一個完全可使用且附樣式的引述區塊。您可以此範例為基礎，用來設計您自己專案的特定區塊。

## 使用其他工作分支 {#other-branches}

為了簡單起見，本指南會讓您直接使用`main`分支。對於範例存放庫中的實驗，這通常不是問題。進行實際專案工作時[應該遵照開發最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)進行，在不同的分支上進行開發，並在合併到`main`之前透過提取請求檢查所有變更。

當你是在`main`分支上開發時，您可以在 Universal Editor 位置列中附加 `?ref=<branch>`，以便從您的分支載入頁面。`<branch>` 是分支名稱，因為此分支會用於專案的預覽或即時 URL，例如 `https://<branch>--<repo>--<owner>.hlx.page`。

只有模式合併到`main`分支時，才支援發佈內容及新模式。
