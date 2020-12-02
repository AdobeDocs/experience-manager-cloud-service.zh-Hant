---
title: 快取與效能
description: 瞭解啟用GraphQL和內容快取以最佳化商務實作效能的不同組態。
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# 快取與效能{#caching}

## 元件和圖形QL響應快取{#graphql}

AEM CIF核心元件已內建支援個別元件的快取GraphQL回應。 此功能可用來減少GraphQL後端呼叫數量。 特別對於重複查詢，例如檢索導航元件的類別樹或提取產品搜索和類別頁面上顯示的所有可用聚合／刻面值，可以實現有效的快取。

對於AEM CIF核心元件，快取是以元件為基礎來設定，因此可以控制是否（以及多長時間）快取每個元件的GraphQL請求／回應。 也可以使用GraphQL客戶端定義OSGi服務的快取行為。

### 設定

為給定元件配置後，快取開始儲存由每個快取配置條目定義的GraphQL查詢和響應。 快取大小和每個項目的快取持續時間將根據專案來定義，例如，目錄資料變更的頻率、元件永遠顯示最新可能資料的重要性等。 請注意，沒有任何快取失效，因此在設定快取期間時請務必小心。

為元件配置快取時，快取名稱必須是您在項目中定義的&#x200B;**proxy**&#x200B;元件的名稱。

在客戶端發送GraphQL請求之前，它將檢查是否已快取&#x200B;**exact**&#x200B;同一GraphQL請求，並可能返回快取的響應。 要匹配，GraphQL請求必須完全匹配，即查詢、操作名稱（如果有）、變數（如果有）均必須等於快取請求，並且所有可設定的自定義HTTP標頭也必須相同。 例如，Magento `Store`標題必須匹配。

### 範例

我們建議您為擷取產品搜尋和類別頁面上所有可用匯總／刻面值的搜尋服務設定一些快取。 這些值通常只會在例如將新屬性新增至產品時變更，因此，如果產品屬性集不經常變更，此快取項目的持續時間可能會「大」。 雖然這是專案特定的，但我們建議在專案開發階段使用幾分鐘的值，在穩定的生產系統上使用數小時。

這通常配置有以下快取條目：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建議使用GraphQl快取功能的另一個範例是導覽元件，因為它會在所有頁面上傳送相同的GraphQL查詢。 在這種情況下，快取條目通常設定為：

```
venia/components/structure/navigation:true:10:600
```

當考慮使用[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)時。 請注意，使用元件代理名`venia/components/structure/navigation`和&#x200B;**not**&#x200B;來表示CIF導航元件的名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應根據專案來定義，通常與Dispatcher層級設定的快取相協調。 請記住，這些快取並沒有任何作用中的失效，因此應謹慎設定快取持續時間。 沒有任何「一刀切」的值能符合所有可能的專案和使用案例。 請確定您在專案層級定義最符合專案需求的快取策略。

## Dispatcher caching {#dispatcher}

在[AEM Dispatcher](https://docs.adobe.com/content/help/zh-Hant/experience-manager-dispatcher/using/dispatcher.html)中快取AEM頁面或片段是任何AEM專案的最佳實務。 通常，它依賴失效技術來確保在Dispatcher中正確更新AEM中變更的任何內容。 這是AEM Dispatcher快取策略的核心功能。

除了純AEM管理的內容CIF外，頁面通常還可顯示透過GraphQL從Magento動態擷取的商務資料。 雖然頁面結構本身可能永遠不會變更，但商務內容可能會變更，例如，如果Magento中有些產品資料（名稱、價格等）變更。

為了確保CIF頁面可在AEM Dispatcher中快取有限的時間，因此建議在AEM Dispatcher中快取CIF頁面時使用[ Time Based Cache Invalidation](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl)（也稱為TTL架構快取）。 此功能可在AEM中使用額外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)套件進行設定。

使用TTL快取功能，開發人員通常會為選取的AEM頁面定義一或多個快取期間。 這可確保CIF頁面只會快取到設定的持續時間，而且內容會經常更新。

>[!NOTE]
>
>雖然伺服器端資料可由AEM分派程式快取，但有些CIF元件（例如`product`、`productlist`和`searchresults`元件）通常會在載入頁面時重新擷取用戶端瀏覽器要求中的產品價格。 如此可確保在載入頁面時一律擷取重要的動態內容。

## 其他資源

- [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL快取配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)