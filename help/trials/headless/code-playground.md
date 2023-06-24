---
title: 在簡單的應用程式中轉譯您的內容
description: 探索使用 CodePen 範例應用程式和適用於 JavaScript 的 AEM Headless 用戶端，從您的試用環境擷取 JSON 內容。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 57%

---


# 在簡單的應用程式中轉譯您的內容 {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="在簡單的應用程式中轉譯您的內容"
>abstract="探索使用 CodePen 範例應用程式和適用於 JavaScript 的 AEM Headless 用戶端，從您的試用環境擷取 JSON 內容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="啟動範例 CodePen 應用程式"
>abstract="本指南將逐步解說如何查詢試用環境的 JSON 資料並放入基本的 JavaScript 網頁應用程式中。您會使用在先前的學習模組中建立模型的內容片段。 如有必要，請先瀏覽這些指南，然後再跳至本指南。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在本單元中，您會了解如何使用適用於 JavaScript 的 AEM Headless 用戶端，透過 GraphQL 持續性查詢從您的試用環境擷取 JSON 資料。<br><br>現在您已了解如何使用此用戶端在您自己的 Web 應用程式中的取用資料。"
>abstract=""

## CodePen {#codepen}

CodePen 是用於前端 Web 開發的線上程式碼編輯器和遊樂場。它可讓您在瀏覽器中撰寫HTML、CSS和JavaScript程式碼，並幾乎立即看到您的工作結果。 您也可以儲存您的工作並與他人分享。Adobe已在CodePen中建立應用程式，您可使用它從試用環境中擷取JSON資料 [適用於JavaScript的AEM Headless使用者端](https://github.com/adobe/aem-headless-client-js). 您可以按原樣使用此應用程式，或者建立您自己的 CodePen 帳戶以進一步自訂。

按一下 **啟動範常式式碼筆應用程式** 試用版中的按鈕會帶您前往CodePen中的應用程式。 該應用程式是使用 JavaScript 擷取 JSON 資料的最精簡範例。此範例應用程式旨在轉譯傳回的任何 JSON 內容，不論基礎內容片段模型的結構為何。開箱即用的應用程式會從 `aem-demo-assets` 包含在試用環境中的持續查詢。 您應該會看到類似於以下內容的 JSON 回應：

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

如果您看到錯誤，請查看瀏覽器主控台以取得更多詳細資料，或[在 Slack](https://adobe-dx-support.slack.com) 尋求協助。

現在您對 CodePen 有了一些了解，接下來您將設定應用程式以從您在前面單元建立的持續性查詢擷取資料。

## JavaScript 程式碼逐步解說 {#code-walkthrough}

此 **JS** CodePen右側的窗格包含範例應用程式的JavaScript。 從第2行開始，您會從Skypack CDN匯入適用於JavaScript的AEM Headless使用者端。 Skypack 用於在沒有建置步驟的情況下方便開發，但您也可以在自己的專案中將 AEM Headless 用戶端搭配 NPM 或 Yarn 使用。如需更多詳細資訊，請參閱 [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) 中的使用說明。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第6行，您的發佈主機詳細資訊已從以下網址讀取： `publishHost` 查詢引數。 此引數是AEM Headless使用者端擷取資料的主機。 此功能通常會編碼至您的應用程式中，但您使用查詢引數，讓CodePen應用程式更容易搭配不同環境使用。

您可在第12行設定AEM Headless使用者端：

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>此 **serviceURL** 設為使用Proxy Adobe I/O Runtime函式，以避免CORS問題。 您自己的專案不需要此Proxy，但CodePen應用程式需要此Proxy才能與您的試用環境搭配使用。 Proxy 函數設定為使用查詢參數中提供的 **publishHost** 值。

最後，函數 `fetchJsonFromGraphQL()` 用於使用 AEM Headless 用戶端執行擷取要求。每次變更程式碼時都會呼叫它，或者可以透過按一下「**重新擷取**」連結來觸發。實際的 `aemHeadlessClient.runPersistedQuery(..)` 呼叫在第 34 行發生。稍後，您會變更此JSON資料的呈現方式，但現在可將其列印至 `#output` div使用 `resultToPreTag(queryResult)` 函式。

## 從持續性查詢擷取資料 {#use-persisted-query}

在第25行中，您可以指出應用程式應從哪個GraphQL持續查詢擷取資料。 持久查詢名稱是端點名稱的組合(即， `your-project` 或 `aem-demo-assets`)，後面接著正斜線，然後是查詢名稱。 如果您完全按照之前的模組指示進行，則您建立的持久查詢位在 `your-project` 端點。

1. 更新 `persistedQueryName` 變數，以使用您在上一個模組中建立的持續查詢。 如果您按照命名建議，您將在 `adventure-list` 端點中建立名稱為 `your-project` 的持續性查詢，並且將 `persistedQueryName` 變數設定為 `your-project/adventure-list`：

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. 完成此變更後，此應用程式將自動重新整理，並將來自持續性查詢的原始 JSON 回應列印到 `#output` div。如果出現錯誤訊息，請查看主控台以取得更多詳細資訊。如果您在此步驟中仍有問題，請[在 Slack](https://adobe-dx-support.slack.com) 尋求協助。

1. 此 JSON 是否包含應用程式所需的確切屬性？如果沒有，請回到[使用 GraphQL API 擷取內容](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql)學習指南進行變更。完成後不要忘記儲存並發佈您的查詢。

## 變更 JSON 轉譯 {#change-rendering}

JSON會依原樣轉譯為 `pre` 標籤中，沒有太多創意。 您可以切換CodePen來使用 `resultToDom()` 函式取代，以說明如何迭代JSON回應以建立更有趣的結果。

1. 若要進行此改變，請註解掉第 37 行並刪除第 40 行的註解：

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. 此函式將JSON回應中包含的任何影像轉譯為 `img` 標籤之間。 如果您建立的「**冒險**」內容片段不包含任何影像，您可以嘗試透過修改第 25 行來改用 `aem-demo-assets/adventures-all` 持續性查詢：

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

此查詢會產生JSON回應，其中包含影像，以及 `resultToDom()` 函式會將其內嵌轉譯。

![adventures-all 查詢的結果和 resultToDom 轉譯函數](assets/do-not-localize/adventures-all-query-result.png)

現在您已經完成了建置模型和查詢的工作，您的內容團隊可以輕鬆接手。在下一個模組中，您會顯示內容作者流程。
