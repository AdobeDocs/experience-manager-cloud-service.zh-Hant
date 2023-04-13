---
title: 使用JavaScript擷取JSON內容
description: 探索使用CodePen應用程式和AEM Headless Client for JavaScript從試用環境擷取JSON內容。
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用JavaScript擷取JSON內容 {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="使用JavaScript擷取JSON內容"
>abstract="探索使用CodePen應用程式和AEM Headless Client for JavaScript從試用環境擷取JSON內容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="啟動CodePen應用程式範例"
>abstract="我們已整合最簡單的CodePen應用程式，導入使用GraphQL持續查詢從試用環境擷取JSON資料的功能。<br><br>按一下下方啟動CodePen範例，然後依照本指南了解詳細資訊。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在本模組中，您已了解如何使用AEM Headless Client for JavaScript，使用GraphQL持續查詢從試用環境擷取JSON資料。<br><br>現在，您已了解如何使用此用戶端來使用您自己Web應用程式中的資料。"
>abstract=""

## 簡介 {#intro}

您從CodePen應用程式開始，此應用程式只是使用擷取JSON資料的簡單範例， [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). 範例應用程式的設計目的，是要轉譯任何傳回的JSON內容，無論基礎內容片段模型的結構為何。 CodePen應用程式會嘗試詳細列出所遇到的任何錯誤，因此您可能會看到下列錯誤訊息列印至應用程式的底部窗格：

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

此錯誤是預期會出現的情況，因為應用程式尚未設定為使用您儲存並發佈於先前模組中的持續查詢。 您將透過下列步驟，設定應用程式以從您的特定查詢擷取資料。

## CodePen逐步說明 {#code-walkthrough}

CodePen上的JS(Javascript)窗格包含範例應用程式的大腦。 從第2行開始，我們會從Skypack CDN匯入AEM Headless Client for JavaScript。 Skypack可用來促進開發而不需進行建置步驟，但您也可以在自己的專案中使用AEM Headless Client搭配NPM或Hayr。 查看 [讀我檔案](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) 以了解更多詳情。

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第6行，我們會從 `publishHost` 查詢參數。 這是AEM無頭用戶端將從中擷取資料的主機。 這通常會編碼到您的應用程式中，但我們使用查詢參數，讓CodePen應用程式可更輕鬆地搭配不同環境運作。

我們在第12行設定AEM無頭式用戶端，以使用代理AdobeIO執行階段功能，以避免CORS問題。 這對於您自己的專案並非必要操作，但是CodePen應用程式使用您的試用環境是必要操作。 代理函式配置為使用 `publishHost` 查詢參數中提供的值。

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最後，函式 `fetchJsonFromGraphQL()` 用於使用AEM無頭用戶端執行擷取請求。 每次變更程式碼時都會呼叫，或透過按「重新擷取」連結來觸發。 實際 `aemHeadlessClient.runPersistedQuery(..)` 34線上發生呼叫。 稍後，我們會變更此JSON資料的呈現方式，但目前我們只會將它列印至 `#output` div使用 `resultToPreTag(queryResult)` 函式。

## 從持續查詢擷取資料 {#use-persisted-query}

在第25行中，我們會指出應用程式應從中擷取資料的持續存在的GraphQL查詢。 持續的查詢名稱是專案名稱（即）的組合。 `your-project`)，後面接著正斜線，然後是查詢的名稱。

更新 `persistedQueryName` 變數，以使用您在上一個模組中建立的持續查詢。 如果您確實遵循命名建議，則會建立一個持續存在的查詢，命名為 `adventures` 在 `your-project` 專案，然後您 `persistedQueryName` 變數 `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

進行此變更後，應用程式應會自動重新整理，並將原始JSON回應從您保存的查詢列印至 `#output` div. 如果您看到錯誤訊息，請查看主控台以取得其他詳細資訊。

此JSON是否包含您的應用程式需要的確切屬性？ 否則，請返回您的AEM製作環境、工具、GraphQL查詢編輯器(或導覽至 `/aem/graphiql.html` 路徑)，並對持續存在的查詢進行變更。 完成後，別忘了儲存並發佈查詢。

## 變更JSON呈現 {#change-rendering}

目前，JSON會依原樣呈現至 `pre` 標籤，這不太有創意。 我們可以切換CodePen，使用 `resultToDom()` 函式來說明如何反覆運算JSON回應，以建立更有趣的結果。

要進行此更改，請注釋第37行，並從第40行中刪除注釋：

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

此函式也會將JSON回應中包含的任何影像轉譯為 `img` 標籤。 如果您建立的「冒險」內容片段不包含任何影像，您可以嘗試切換以使用 `aem-demo-assets/adventures-all` 修改第25行以保存查詢：

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

此查詢會產生包含影像的JSON回應，以及 `resultToDom()` 函式會將它們內嵌。

![歷險結果 — all查詢和resultToDom轉譯函式](assets/do-not-localize/adventures-all-query-result.png)
