---
title: 在簡單應用程式中呈現內容
description: 探索使用CodePen範例應用程式和AEM Headless Client for JavaScript從試用環境擷取JSON內容。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 3b64b909996674bcbe36f746bcfd15e1422a8a4b
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 42%

---


# 在簡單應用程式中呈現內容 {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="在簡單應用程式中呈現內容"
>abstract="探索使用CodePen範例應用程式和AEM Headless Client for JavaScript從試用環境擷取JSON內容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="啟動範例 CodePen 應用程式"
>abstract="本指南會逐步說明如何從試用環境中查詢JSON資料至基本的JavaScript網頁應用程式。 我們將使用您在先前的學習模組中建立和模型的內容片段，因此，請先閱讀這些指南，再跳到這個指南中。<br><br>為了示範如何從JavaScript網頁應用程式查詢內容，我們已設定CodePen，您可以依原樣使用，或取用您自己的帳戶以進一步自訂。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在本單元中，您會了解如何使用適用於 JavaScript 的 AEM Headless 用戶端，透過 GraphQL 持續性查詢從您的試用環境擷取 JSON 資料。<br><br>現在您已了解如何使用此用戶端在您自己的 Web 應用程式中的取用資料。"
>abstract=""

## CodePen {#codepen}

CodePen是用於前端Web開發的線上代碼編輯器和操場。 它可讓您在瀏覽器中撰寫HTML、CSS和JavaScript程式碼，並幾乎立即查看工作結果。 您也可以儲存您的工作並與他人共用。 我們已在CodePen中建立應用程式，您可使用，從試用環境擷取JSON資料 [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). 您可以照原樣使用此應用程式，或將其複製到您自己的CodePen帳戶，以進一步自訂。

按一下 **啟動CodePen應用程式範例** 按鈕，將帶您進入CodePen中的應用。 此應用程式只是使用JavaScript擷取JSON資料的簡單範例。 範例應用程式的設計目的，是要轉譯任何傳回的JSON內容，無論基礎內容片段模型的結構為何。 應用程式會立即從 `aem-demo-assets` 包含在試用環境中的持續查詢。 您應該會看到類似下列的JSON回應：

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

如果您反之看到錯誤，請查看瀏覽器主控台以取得詳細資訊或聯絡 [Slack](https://adobe-dx-support.slack.com).

現在您對CodePen有了一些了解，接下來您將設定應用程式，以從您在先前模組中建立的持續查詢中擷取資料。

## JavaScript程式碼逐步說明 {#code-walkthrough}

此 **JS** CodePen右側的窗格包含範例應用程式的Javascript。 從第 2 行開始，我們從 Skypack CDN 匯入適用於 JavaScript 的 AEM Headless 用戶端。Skypack 用於在沒有建置步驟的情況下方便開發，但您也可以在自己的專案中將 AEM Headless 用戶端搭配 NPM 或 Yarn 使用。如需更多詳細資訊，請參閱 [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) 中的使用說明。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第 6 行，我們從 `publishHost` 查詢參數讀取您的發佈主機詳細資料。這是 AEM Headless 用戶端將從中擷取資料的主機。這通常會編碼到您的應用程式中，但我們使用查詢參數來使 CodePen 應用程式輕鬆搭配不同環境運作。

我們在第 12 行將 AEM Headless 用戶端設定為使用 Proxy Adobe IO 執行階段函數來避免 CORS 問題。您自己的專案不需要這麼做，但 CodePen 應用程式需要才能搭配您的試用環境運作。Proxy 函數設定為使用查詢參數中提供的 `publishHost` 值。

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最後，函數 `fetchJsonFromGraphQL()` 用於使用 AEM Headless 用戶端執行擷取要求。每次變更程式碼時都會呼叫，或按一下 **重新擷取** 連結。 實際的 `aemHeadlessClient.runPersistedQuery(..)` 呼叫在第 34 行發生。稍後我們將變更此 JSON 資料的轉譯方式，但現在我們只需使用 `resultToPreTag(queryResult)` 函數將其列印到 `#output` div。

## 從持續查詢擷取資料 {#use-persisted-query}

在第 25 行，我們指示應用程式應從哪個 GraphQL 持續性查詢中擷取資料。持續的查詢名稱是端點名稱（即）的組合。 `your-project` 或 `aem-demo-assets`)，後面接著正斜線，然後是查詢的名稱。 如果您確實遵循先前的模組指示，則您建立的持續查詢將位於 `your-project` 端點。

1. 更新 `persistedQueryName` 變數以使用您在前一個單元建立的持續性查詢。如果您遵循命名建議，則會建立一個名為 `adventure-list` 在 `your-project` 端點，然後設定 `persistedQueryName` 變數 `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. 完成此變更後，此應用程式將自動重新整理，並將來自持續性查詢的原始 JSON 回應列印到 `#output` div。如果出現錯誤訊息，請查看主控台以取得更多詳細資訊。伸手 [Slack](https://adobe-dx-support.slack.com) 如果您仍對此步驟有問題。

1. 此 JSON 是否包含應用程式所需的確切屬性？否則返回 [使用GraphQL API擷取內容](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) 學習指南進行變更。 完成後，別忘了儲存並發佈查詢。

## 變更JSON轉譯 {#change-rendering}

JSON會依原樣呈現至 `pre` 標籤，這不太有創意。 可以改變我們的 CodePen 來改用 `resultToDom()` 函數，以說明如何疊代 JSON 回應以產生更有趣的結果。

1. 若要進行此改變，請註解掉第 37 行並刪除第 40 行的註解：

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. 此函數也會轉譯包含在 JSON 回應中的任何影像作為 `img` 標籤。若 **冒險** 您建立的內容片段不包含任何影像，您可以嘗試切換以使用 `aem-demo-assets/adventures-all` 修改第25行以保存查詢：

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

此查詢將產生一個包含影像的 JSON 回應，`resultToDom()` 函數將使它們內嵌轉譯。

![adventures-all 查詢的結果和 resultToDom 轉譯函數](assets/do-not-localize/adventures-all-query-result.png)

現在您已完成建立模型和查詢的工作，您的內容團隊便可輕鬆接管。 我們將在下一個模組中顯示內容製作流程。
