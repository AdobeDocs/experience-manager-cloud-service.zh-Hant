---
title: 建立經檢測適用 Universal Editor 的區塊
description: 瞭解如何建立在WYSIWYG製作中與Edge Delivery Services專案結合使用並搭配通用編輯器的區塊。
exl-id: 65a5600a-8d16-4943-b3cd-fe2eee1b4abf
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: a7b48559e5bf60c86fecd73a8bcef6c9aaa03b80
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 54%

---


# 建立經檢測適用 Universal Editor 的區塊 {#create-block}

瞭解如何建立在WYSIWYG製作中與Edge Delivery Services專案結合使用並搭配通用編輯器的區塊。

## 先決條件 {#prerequisites}

本指南提供逐步指示，說明如何透過Edge Delivery Services專案在WYSIWYG製作中建立針對通用編輯器檢測的區塊。 內容包括新增元件、載入 Universal Editor 中的元件定義、發佈頁面、實施區塊裝飾和樣式、將變更引入生產以及進行變更驗證。完成本指南後，您可以為自己的專案建立和部署新區塊。

本指南需要與Edge Delivery Services專案及通用編輯器搭配使用的WYSIWYG編寫的現有知識。 在開始執行本指南之前，您應該有 Edge Delivery Services 存取權並熟悉基本使用需知，包括：

* 您已完成 [Edge Delivery Service 教學課程。](/help/edge/developer/tutorial.md)
* 您有權存取 [AEM Cloud Service 沙箱。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* 您已[在同一沙箱環境中啟用 Universal Editor。](/help/implementing/universal-editor/getting-started.md)
* 您已完成使用Edge Delivery Services進行WYSIWYG製作的[開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)。

本指南以[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)中完成的工作為基礎。

## 為您的專案新增區塊 {#add-block}

在本指南中，您將建立一個區塊並在頁面上呈現令人難忘的引述。

為了簡化此範例，所有變更均針對專案儲存庫的 `main` 分支進行。當然，進行實際專案時[應該遵照開發最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)進行，在不同的分支上進行開發，並在合併到`main`之前透過提取請求檢查所有變更。

Adobe 建議您採用三階段方法來開發區塊：

1. 建立區塊的定義和模式、審查區塊，然後將區塊投入生產。
1. 使用新區塊建立內容。
1. 實施新區塊的裝飾和風格。

以下引述區塊範例即遵照此方法進行。

### 建立區塊定義和模式 {#create-block-model}

1&amp;amp；period；在本機複製您在[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)中建立的GitHub專案，並在您選擇的編輯器中開啟。

* 此處使用 Microsoft 程式碼是為了說明目的。

![複製專案。](assets/create-block/clone.png)

2&amp;amp；句點；編輯專案根目錄中的`component-definition.json`檔案，並為您的新報價區塊新增下列定義並儲存檔案。

>[!BEGINTABS]

>[!TAB JSON範例]

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

>[!TAB 熒幕擷圖]

![編輯 component-definitions.json 檔案以定義引述區塊](assets/create-block/component-definitions.png)

>[!ENDTABS]

3&amp;amp；句點；編輯專案根目錄中的`component-models.json`檔案，並為您的新報價區塊新增下列[模型定義](/help/implementing/universal-editor/field-types.md#model-structure)並儲存檔案。

* 請參閱檔案[使用Edge Delivery Services專案進行WYSIWYG製作的內容模型](/help/edge/wysiwyg-authoring/content-modeling.md)，以取得建立內容模型時務必要考量的詳細資訊。

>[!BEGINTABS]

>[!TAB JSON範例]

```json
{
  "id": "quote",
  "fields": [
     {
       "component": "richtext",
       "name": "quote",
       "value": "",
       "label": "Quote",
       "valueType": "string"
     },
     {
       "component": "text",
       "valueType": "string",
       "name": "author",
       "label": "Author",
       "value": ""
     }
   ]
}
```

>[!TAB 熒幕擷圖]

![編輯 component-models.json 檔案以定義引述區塊的模式](assets/create-block/component-models.png)

>[!ENDTABS]

4&amp;amp；句點；編輯專案根目錄中的`component-filters.json`檔案，並將引號區塊新增至[篩選定義](/help/implementing/universal-editor/customizing.md#filtering-components)，以允許將區塊新增至任何區段並儲存檔案。

>[!BEGINTABS]

>[!TAB JSON範例]

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

>[!TAB 熒幕擷圖]

![編輯 component-filters.json 檔案以定義引述區塊的篩選器](assets/create-block/component-filters.png)

>[!ENDTABS]

5&amp;amp；句點；使用Git，將這些變更提交至您的`main`分支。

* 提交至`main`僅是為了說明目的。[遵照最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)，並在實際專案工作中使用提取請求。

### 使用區塊建立內容。 {#create-content}

現在您的基本引述區塊已定義並提交給範例專案，您可以將引述區塊新增至現有頁面。

1. 在瀏覽器中，登入 AEM as a Cloud Service。[使用Sites主控台，](/help/sites-cloud/authoring/basic-handling.md)導覽至您在[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)指南中建立的網站，並選取頁面。

   * 在本案例中，`index`是用於說明目的。

   ![在 Sites 控制台中選取索引頁面](assets/create-block/sites-console.png)

1. 點選或按一下控制台工具列中的「**編輯**」，Universal Editor 將會開啟。

   * 為了載入該頁面，您可能需要點選或按一下「**使用 Adob&#x200B;&#x200B;e 登入**」，並在 Universal Editor 中對 AEM 進行驗證。

1. 在 Universal Editor 中，選取一個區段。在屬性面板中，點選或按一下「**新增**」圖示，然後從功能表中選取新的&#x200B;**Quote**&#x200B;區塊。

   *  **新增**&#x200B;圖示是一個加號。
   * 如果所選物件的藍色外框有一個標為「**區段**」的標記，表示您已選取了一個區段。
   * 在此範例中，在「**Lorem Ipsum**」標題上方輕輕點選或按一下，即可選取包含標題和 lorem ipsum 文字的區段。

   ![在 Universal Editor 中選取一個區段](assets/create-block/add-quote-block.png)

1. 頁面重新加載，且引述區塊將新增至所選區段的底部，以及成為 `component-definitions.json` 檔案中指定的預設內容。

   * 引號區塊可以像任何其他區塊一樣就地或在「屬性」面板中選取和編輯。
   * 樣式將在下一步中套用。

   ![所選區段中包含新引述區塊的頁面](assets/create-block/quote-added.png)

1. 當您對引述內容感到滿意時，可以在 Universal Editor 工具列中點選或按一下「**發佈**」按鈕。

1. 導覽至已發佈的頁面，驗證內容是否已發佈。該連結類似 `https://<branch>--<repo>--<owner>.hlx.page`

   ![發佈的引述](assets/create-block/quote-published.png)

### 區塊的樣式 {#style-block}

現在您已經有了一個可用的引述區塊，您可以對區塊套用樣式。

1&amp;amp；句號；返回專案的編輯器。

2&amp;amp；句點；在`blocks`資料夾下建立`quote`資料夾。

![建立引述檔案夾](assets/create-block/new-folder.png)

3&amp;amp；句點；在新的`quote`資料夾中，新增`quote.js`檔案以新增下列JavaScript並儲存檔案來實施區塊裝飾。

>[!BEGINTABS]

>[!TAB JavaScript範例]

```javascript
export default function decorate(block) {
  const [quoteWrapper] = block.children;
 
  const blockquote = document.createElement('blockquote');
  blockquote.textContent = quoteWrapper.textContent.trim();
  quoteWrapper.replaceChildren(blockquote);
}
```

>[!TAB 熒幕擷圖]

![新增 JavaScript 以裝飾區塊](assets/create-block/quote-js.png)

>[!ENDTABS]

4&amp;amp；period；在`quote`資料夾中，新增一個`quote.css`檔案，藉由新增下列CSS程式碼來定義區塊的樣式並儲存檔案。

>[!BEGINTABS]

>[!TAB CSS範例]

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

>[!TAB 熒幕擷圖]

![新增 CSS 以定義區塊樣式](assets/create-block/quote-css.png)

>[!ENDTABS]

5&amp;amp；句點；使用Git，將這些變更提交至您的`main`分支。

* 提交至`main`僅是為了說明目的。[遵照最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)，並在實際專案工作中使用提取請求。

6&amp;amp；句號；返回至Universal Editor的瀏覽器索引標籤（您編輯專案的頁面），並重新載入頁面以檢視您設定樣式的區塊。

7&amp;amp；句點；請參閱頁面上目前樣式的引號區塊。

![Universal Editor 中附有樣式的引述區塊](assets/create-block/quote-styled.png)

8&amp;amp；period；導覽至發佈的頁面，確認變更已推送至生產環境。 該連結類似 `https://<branch>--<repo>--<owner>.hlx.page`

![已發布且附樣式的引述區塊](assets/create-block/quote-styled-published.png)

恭喜！您現在擁有一個完全可使用且附樣式的引述區塊。您可以此範例為基礎，用來設計您自己專案的特定區塊。

### 區塊選項 {#block-options}

如果您需要區塊的外觀或行為因特定情況而略有不同，但差異不足以成為新的區塊，您可以讓作者從[區塊選項中進行選擇。](content-modeling.md#type-inference)

將`classes`屬性新增至區塊後，該屬性會呈現在簡單區塊的表格標頭中，或呈現為容器區塊中專案的值清單。

```json
{
  "id": "simpleMarquee",
  "fields": [
    {
      "component": "text",
      "valueType": "string",
      "name": "marqueeText",
      "value": "",
      "label": "Marquee text",
      "description": "The text you want shown in your marquee"
    },
    {
      "component": "select",
      "name": "classes",
      "value": "",
      "label": "Background Color",
      "description": "The marquee background color",
      "valueType": "string",
      "options": [
        {
          "name": "Red",
          "value": "bg-red"
        },
        {
          "name": "Green",
          "value": "bg-green"
        },
        {
          "name": "Blue",
          "value": "bg-blue"
        }
      ]
    }
  ]
}
```

## 使用其他工作分支 {#other-branches}

為了簡單起見，本指南會讓您直接使用`main`分支。對於範例存放庫中的實驗，這通常不是問題。進行實際專案工作時[應該遵照開發最佳實務](https://www.aem.live/docs/dev-collab-and-good-practices)進行，在不同的分支上進行開發，並在合併到`main`之前透過提取請求檢查所有變更。

當你是在`main`分支上開發時，您可以在 Universal Editor 位置列中附加 `?ref=<branch>`，以便從您的分支載入頁面。`<branch>` 是分支名稱，因為此分支會用於專案的預覽或即時 URL，例如 `https://<branch>--<repo>--<owner>.hlx.page`。

只有模式合併到`main`分支時，才支援發佈內容及新模式。

## 重複使用您的區塊以進行檔案式編寫 {#reusing-blocks}

如果您遵循相同的內容模型，可以使用透過通用編輯器為WYSIWYG編寫建立的區塊，以進行檔案式編寫。

如需詳細資訊，請參閱檔案[WYSIWYG和檔案式編寫的區塊](/help/edge/wysiwyg-authoring/wysiwyg-doc-blocks.md)。

## 後續步驟 {#next-steps}

既然您已經知道如何建立區塊，那麼了解如何以語義方式建立內容模式並實現精益開發人員體驗就很重要。

請參閱檔案[使用Edge Delivery Services專案進行WYSIWYG製作的內容模型](/help/edge/wysiwyg-authoring/content-modeling.md)，瞭解內容模型如何用於使用Edge Delivery Services專案進行WYSIWYG製作。

>[!TIP]
>
>如需使用AEM as a Cloud Service作為內容來源來建立啟用WYSIWYG撰寫的新Edge Delivery Services專案的端對端逐步解說，請檢視[此AEM GEM網路研討會。](https://experienceleague.adobe.com/en/docs/events/experience-manager-gems-recordings/gems2024/aem-authoring-and-edge-delivery)

