---
title: 快取與效能
description: 瞭解各種可用設定，以啟用GraphQL和內容快取，將您的Commerce實作效能最佳化。
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 快取與效能 {#caching}

## 元件和GraphQL回應快取 {#graphql}

AEM CIF核心元件已內建對快取個別元件的GraphQL回應的支援。 此功能可用來大幅減少GraphQL後端呼叫的數量。 尤其對於重複查詢，例如擷取導覽元件的類別樹狀結構，或擷取產品搜尋和類別頁面上顯示的所有可用彙總/多面向值，可以實現有效的快取。

對於AEM CIF核心元件，快取是根據元件來設定，因此能夠控制是否對每個元件快取GraphQL請求/回應（以及快取的時長）。 您也可以使用GraphQL使用者端定義OSGi服務的快取行為。

### 設定 {#configuration}

針對指定元件進行設定後，快取會開始儲存由每個快取設定專案定義的GraphQL查詢和回應。 快取的大小和每個專案的快取持續時間是根據專案來定義，例如，根據下列專案而定：

* 目錄資料可能變更的頻率。
* 元件必須一律顯示最新資料，以此類推。

沒有任何快取失效，因此在設定快取期間時請小心。

設定元件的快取時，快取名稱必須是 **proxy** 您在專案中定義的元件。

使用者端傳送GraphQL要求之前，會先檢查是否該 **精確** 已快取相同的GraphQL請求，並且可能會傳回快取的回應。 為了比對，GraphQL請求 _必須_ 完全相符。 也就是查詢、作業名稱（如果有的話）、變數（如果有的話） _必須_ 都等於快取的請求。 此外，所有可能設定的自訂HTTP標頭 _必須_ 也應該是相同的。 例如Adobe Commerce `Store` 頁首 _必須_ 相符。

### 範例 {#examples}

Adobe建議您為search服務設定一些快取，以便擷取product search和category頁面上顯示的所有可用彙總/多面向值。 例如，只有在將新屬性新增至產品時，這些值才會變更。 因此，如果產品屬性集合不經常變更，則此快取專案的持續時間可能會「很大」。 雖然此專案是專案專用的，但Adobe建議在專案開發階段使用幾分鐘的值，並在穩定生產系統上使用幾小時。

此設定通常使用下列快取專案進行設定：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

另一個建議使用GraphQl快取功能的範例情況是導覽元件。 原因是它會在所有頁面上傳送相同的GraphQL查詢。 在這種情況下，快取專案通常會設為：

```
venia/components/structure/navigation:true:10:600
```

考量到 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) 已使用。 請注意元件代理名稱的使用 `venia/components/structure/navigation`、和 **非** CIF導覽元件的名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應根據專案來定義，通常與在Dispatcher層級設定的快取協調。 請記住，這些快取沒有任何作用中的失效機制，因此應謹慎設定快取持續時間。 沒有任何「適合所有」的值會符合所有可能的專案和使用案例。 請務必在專案層級定義最符合專案需求的快取策略。

## Dispatcher快取 {#dispatcher}

在中快取AEM頁面或片段 [AEM傳送器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是任何AEM專案的最佳實務。 通常，它仰賴失效技術，以確保在AEM中變更的任何內容在Dispatcher中正確更新。 此功能是AEM Dispatcher快取策略的核心。

除了純AEM管理的內容CIF之外，頁面通常也可以顯示透過GraphQL從Adobe Commerce動態擷取的商務資料。 雖然頁面結構本身可能不會變更，但商務內容可能會變更。 例如，如果產品資料（例如名稱和價格）在Adobe Commerce中變更。

為了確保CIF頁面在AEM Dispatcher中的有限時間內皆會快取，Adobe建議使用 [以時間為基礎的快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) （也稱為TTL型快取）在AEM Dispatcher中快取CIF頁面時。 此功能可在AEM中使用「 」額外的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 封裝。

使用TTL型快取時，開發人員通常會為選取的AEM頁面定義一或多個快取持續時間。 此持續時間可確保在AEM Dispatcher中僅快取CIF頁面，直到設定的持續時間為止，並且內容會經常更新。

>[!NOTE]
>
>雖然AEM Dispatcher可能會快取伺服器端資料，但部分CIF元件(例如 `product`， `productlist`、和 `searchresults` 載入頁面時，元件通常會一律在使用者端瀏覽器請求中重新擷取產品價格。 這麼做可確保頁面載入時一定能擷取重要的動態內容。

## 其他資源 {#additional}

* [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL快取設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM傳送器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
