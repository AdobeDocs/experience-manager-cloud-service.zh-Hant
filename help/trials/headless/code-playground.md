---
title: 使用 JavaScript 擷取 JSON 內容
description: 探索使用 CodePen 應用程式和適用於 JavaScript 的 AEM Headless 用戶端，從您的試用環境擷取 JSON 內容。
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 100%

---


# 使用 JavaScript 擷取 JSON 內容 {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="使用 JavaScript 擷取 JSON 內容"
>abstract="探索使用 CodePen 應用程式和適用於 JavaScript 的 AEM Headless 用戶端，從您的試用環境擷取 JSON 內容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="啟動範例 CodePen 應用程式"
>abstract="我們已經放入一個最小的 CodePen 應用程式來介紹使用 GraphQL 持續性查詢從您的試用環境擷取 JSON 資料。<br><br>點選下方以啟動 CodePen 範例，然後按照本指南操作以進一步了解。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在本單元中，您會了解如何使用適用於 JavaScript 的 AEM Headless 用戶端，透過 GraphQL 持續性查詢從您的試用環境擷取 JSON 資料。<br><br>現在您已了解如何使用此用戶端在您自己的 Web 應用程式中的取用資料。"
>abstract=""

## 簡介 {#intro}

您從 CodePen 應用程式開始，此應用程式是使用[適用於 JavaScript 的 AEM Headless 用戶端](https://github.com/adobe/aem-headless-client-js)擷取 JSON 資料的最精簡範例。此範例應用程式旨在轉譯傳回的任何 JSON 內容，不論基礎內容片段模型的結構為何。CodePen 應用程式會嘗試詳述發生的任何錯誤，因此您可能會在應用程式的底部窗格中看到以下錯誤訊息：

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

這是預期中的錯誤，因為應用程式尚未設定為使用您在前一個單元中儲存和發佈的持續性查詢。在以下步驟中，您將設定此應用程式以從您的特定查詢中擷取資料。

## CodePen 逐步解說 {#code-walkthrough}

CodePen 上的 JS (Javascript) 窗格包含範例應用程式的大腦。從第 2 行開始，我們從 Skypack CDN 匯入適用於 JavaScript 的 AEM Headless 用戶端。Skypack 用於在沒有建置步驟的情況下方便開發，但您也可以在自己的專案中將 AEM Headless 用戶端搭配 NPM 或 Yarn 使用。如需更多詳細資訊，請參閱 [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) 中的使用說明。

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第 6 行，我們從 `publishHost` 查詢參數讀取您的發佈主機詳細資料。這是 AEM Headless 用戶端將從中擷取資料的主機。這通常會編碼到您的應用程式中，但我們使用查詢參數來使 CodePen 應用程式輕鬆搭配不同環境運作。

我們在第 12 行將 AEM Headless 用戶端設定為使用 Proxy Adobe IO 執行階段函數來避免 CORS 問題。您自己的專案不需要這麼做，但 CodePen 應用程式需要才能搭配您的試用環境運作。Proxy 函數設定為使用查詢參數中提供的 `publishHost` 值。

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最後，函數 `fetchJsonFromGraphQL()` 用於使用 AEM Headless 用戶端執行擷取要求。每次變更程式碼時都會呼叫它，或者可以透過按下「重新擷取」連結來觸發。實際的 `aemHeadlessClient.runPersistedQuery(..)` 呼叫在第 34 行發生。稍後我們將變更此 JSON 資料的轉譯方式，但現在我們只需使用 `resultToPreTag(queryResult)` 函數將其列印到 `#output` div。

## 從持續性查詢中擷取資料 {#use-persisted-query}

在第 25 行，我們指示應用程式應從哪個 GraphQL 持續性查詢中擷取資料。持續性查詢名稱是專案名稱的組合 (即 `your-project`)，後面接著正斜線，然後是查詢名稱。

更新 `persistedQueryName` 變數以使用您在前一個單元建立的持續性查詢。如果您完全按照命名建議，您將在 `your-project` 專案中建立名稱為 `adventures` 的持續性查詢，並且將 `persistedQueryName` 變數設定為 `your-project/adventures`：

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

完成此變更後，此應用程式將自動重新整理，並將來自持續性查詢的原始 JSON 回應列印到 `#output` div。如果出現錯誤訊息，請查看主控台以取得更多詳細資訊。

此 JSON 是否包含應用程式所需的確切屬性？如果沒有，請返回您的 AEM Author 環境、工具、GraphQL 查詢編輯器 (或導覽至`/aem/graphiql.html`路徑) 並變更您的持續性查詢。完成後不要忘記儲存並發佈查詢。

## 變更 JSON 轉譯 {#change-rendering}

目前，JSON 按原狀轉譯為 `pre` 標籤，這不是很有創意。可以改變我們的 CodePen 來改用 `resultToDom()` 函數，以說明如何疊代 JSON 回應以產生更有趣的結果。

若要進行此改變，請註解掉第 37 行並刪除第 40 行的註解：

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

此函數也會轉譯包含在 JSON 回應中的任何影像作為 `img` 標籤。如果您建立的「冒險」內容片段不包含任何影像，您可以嘗試透過修改第 25 行來改用 `aem-demo-assets/adventures-all` 持續性查詢：

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

此查詢將產生一個包含影像的 JSON 回應，`resultToDom()` 函數將使它們內嵌轉譯。

![adventures-all 查詢的結果和 resultToDom 轉譯函數](assets/do-not-localize/adventures-all-query-result.png)
