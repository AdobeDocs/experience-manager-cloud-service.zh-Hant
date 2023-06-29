---
title: 針對 AEM 開發 SPA
description: 本文介紹當與前端開發人員合作開發適用於AEM的SPA時，應考量的一些重要問題。 此外也提供有關SPA的AEM架構概觀，以供在AEM上部署已開發的SPA時牢記。
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 11%

---

# 針對 AEM 開發 SPA {#developing-spas-for-aem}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用 SPA 框架建立網站，而作者則想在 AEM 中為使用這類框架建立網站，順暢地編輯內容。

本文介紹當請前端開發人員開發SPA for AEM時需要考慮的重要問題，並提供AEM有關在AEM上部署SPA的架構概覽。

## AEM的SPA開發原則 {#spa-development-principles-for-aem}

在 AEM 開發單頁應用程式是假設前端開發人員在建立 SPA 時有遵守標準最佳做法。如果您身為前端開發人員，遵循這些一般最佳實務和一些AEM特定原則，您的SPA可透過以下方式運作： [AEM及其內容製作功能](introduction.md#content-editing-experience-with-spa).

* **[可攜性](#portability)** - 如同任何元件， 元件應盡可能建置為具可攜性。SPA 應該使用可攜帶和可重複使用的元件建置。
* **[AEM磁碟機網站結構](#aem-drives-site-structure)**  — 前端開發人員建立元件並擁有其內部結構，但仰賴AEM定義網站的內容結構。
* **[動態呈現](#dynamic-rendering)** - 所有呈現都應該是動態的。
* **[動態路由](#dynamic-routing)** - SPA 負責路由，AEM 會偵聽並據此進行擷取。任何路由也應該是動態的。

如果您在開發SPA時牢記這些原則，在啟用所有支援的AEM編寫功能時，它會儘可能地靈活且經得起未來考驗。

如果您不需要支援AEM編寫功能，請考慮其他功能 [SPA設計模型](#spa-design-models).

### 可攜性 {#portability}

如同開發任何元件一樣，元件的設計應儘可能提高可攜性。 應避免任何影響元件可移植性或可重複使用的模式，以確保未來相容性、彈性和可維護性。

產生的SPA應使用可攜性強且可重複使用的元件建置。

### AEM磁碟機網站結構 {#aem-drives-site-structure}

前端開發人員必須自行負責建立用於建置應用程式的SPA元件資料庫。 前端開發人員可完全控制元件的內部結構。 [不過，AEM一律擁有網站結構](editor-overview.md).

此控制表示前端開發人員可以在元件的進入點之前或之後新增客戶內容，並也可以在元件內進行協力廠商呼叫。 不過，前端開發人員無法完全控制元件的巢狀內嵌方式等。

### 動態演算 {#dynamic-rendering}

SPA應該僅依賴內容的動態呈現。 此預期為AEM擷取並轉譯內容結構之所有子項的預設值。

任何指向特定內容的明確呈現都會視為靜態呈現，而且雖然受到支援，仍與AEM內容製作功能相容。 這也違背了以下原則 [可攜性](#portability).

### 動態路由 {#dynamic-routing}

如同演算一樣，所有路由也應該是動態的。 在AEM中， [SPA應一律擁有路由](routing.md) 和AEM會監聽它，並根據它擷取內容。

任何靜態路由都適用於 [可攜性原則](#portability) 和會因為與AEM的內容製作功能不相容而限製作者。 例如，使用靜態路由，如果內容作者想要變更路由或變更頁面，他們必須要求前端開發人員執行此操作。

## AEM 專案原型 {#aem-project-archetype}

任何AEM專案都應該使用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，支援使用React或Angular的SPA專案，並使用SPA SDK。

## SPA設計模型 {#spa-design-models}

如果 [在AEM中開發SPA的原則](#spa-development-principles-for-aem) ，則您的SPA可透過所有支援的AEM內容製作功能運作。

不過，在某些情況下，此功能並非完全必要。 下表概述各種設計模型、其優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <td>AEM用作Headless CMS，而不使用 <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA Editor SDK架構。</a></td>
   <td>前端開發人員可完全控制應用程式。</td>
   <td><p>內容作者無法使用AEM內容製作體驗。</p> <p>如果程式碼包含靜態參考或路由，則無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPA Editor SDK架構，但只對內容作者開啟部分割槽域。</td>
   <td>開發人員只會在應用程式的受限制區域中啟用撰寫，就能保持對應用程式的控制。</td>
   <td><p>內容作者受限於有限的AEM內容製作體驗。</p> <p>如果程式碼包含靜態參考或路由，就有可能無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>專案完全使用SPA編輯器SDK，前端元件會開發為程式庫，而應用程式的內容結構會委派給AEM。</td>
   <td><p>應用程式可重複使用且可移植。</p> <p>內容作者可使用AEM內容製作體驗來編輯應用程式。<br /> </p> <p>SPA與範本編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構和委派給AEM的內容部分。</p> <p>開發人員仍可保留應用程式的區域，以供不應使用AEM編寫的內容使用。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>雖然AEM支援所有模型，但只要實作第三種(並遵循建議的 [SPA開發原則](#spa-development-principles-for-aem))是能夠在AEM中與SPA內容互動及編輯其內容的內容作者。

## 將現有SPA移轉至AEM {#migrating-existing-spas-to-aem}

一般而言，如果您的SPA遵循 [AEM的SPA開發原則](#spa-development-principles-for-aem)，則您的SPA可在AEM中運作，並可使用AEM SPA編輯器進行編輯。

請依照下列步驟操作，讓現有的SPA準備好與AEM搭配使用。

1. **將您的JS元件模組化。**  — 可讓您以任何順序、位置和大小呈現這些影像。
1. **使用SDK提供的容器將您的元件放置在畫面上。** - AEM提供頁面和段落系統元件供您使用。
1. **為每個JS元件建立AEM元件。** - AEM元件會定義對話方塊和JSON輸出。

## 面向前端開發人員的說明 {#instructions-for-front-end-developers}

讓前端開發人員建立AEM適用的SPA的主要工作是就元件及其JSON模型達成共識。

以下概述前端開發人員在開發適用於AEM的SPA時必須執行的步驟。

1. **同意元件及其JSON模型**

   前端開發人員和後端AEM開發人員必須就所需的元件和模型達成一致，以便從SPA元件到後端元件進行一對一比對。

   AEM元件仍然主要用於提供編輯對話方塊和匯出元件模型。

1. **在React元件中，透過以下方式存取模型`this.props.cqModel`**

   在同意元件及JSON模型就緒後，前端開發人員即可自由開發SPA，並可透過以下方式存取JSON模型 `this.props.cqModel`.

1. **實作元件的 `render()` 方法**

   前端開發人員實作 `render()` 方法以適合的方式呈現，而且可以使用 `cqModel` 屬性。 此方法會輸出插入頁面中的DOM和HTML片段。 此方法也是在React中建立應用程式的標準方式。

1. **透過以下方式將元件對應到AEM資源型別`MapTo()`**

   對應會儲存元件類別，並由提供的在內部使用 `Container` 根據指定的資源型別擷取及動態例項化元件的元件。

   此地圖可當作前端與後端之間的「粘合劑」，讓編輯器知道react元件對應到哪些元件。

   此 `Page` 和 `ResponsiveGrid` 是延伸基底類別的良好範例 `Container`.

1. **定義元件的 `EditConfig` 作為引數`MapTo()`**

   只要尚未轉譯或沒有可轉譯的內容，此引數是告訴編輯器元件應如何命名所必需的。

1. **擴充提供的 `Container` 頁面和容器的類別**

   頁面和段落系統應該擴充此類別，好讓委派給內部元件的功能如預期般運作。

1. **實作路由解決方案，該解決方案使用HTML5 `History` API。**

   當 `ModelRouter` 已啟用，呼叫 `pushState` 和 `replaceState` 函式觸發要求 `PageModelManager` 以擷取模型的遺失片段。

   目前版本的 `ModelRouter` 僅支援使用指向Sling模型進入點的實際資源路徑的URL。 不支援使用虛名URL或別名。

   此 `ModelRouter` 可停用或設定為忽略規則運算式清單。

## 與AEM無關 {#aem-agnostic}

這些程式碼區塊說明您的React和Angular元件如何不需要特定於Adobe或AEM的元件。

* JavaScript元件內的所有內容都與AEM無關。
* 不過，AEM的專屬之處在於，JS元件必須透過MapTo協助程式對應至AEM元件。

![與AEM無關的方法](assets/aem-agnostic.png)

此 `MapTo` helper是「粘合劑」，可讓後端和前端元件搭配使用：

* 它會告訴JS容器（或JS段落系統）哪個JS元件負責轉譯JSON中存在的每個元件。
* 它會將HTML資料屬性新增至JS元件轉譯的HTML，以便SPA編輯器知道在編輯元件時向作者顯示的對話方塊。

如需關於使用的詳細資訊 `MapTo` 以及建置SPA for AEM的一般資訊，請參閱所選架構的快速入門手冊。

* [開始在 AEM 中使用 React 建立 SPA](getting-started-react.md)
* [開始在 AEM 中使用 Angular 建立 SPA](getting-started-angular.md)

## AEM架構與SPA {#aem-architecture-and-spas}

AEM的一般架構，包括開發、製作和發佈環境，在使用SPA時不會變更。 不過，瞭解SPA開發如何適應此架構很有幫助。

![AEM架構與SPA](assets/aem-architecture.png)

* **組建環境**

  此環境是出庫SPA應用程式和元件來源的位置。

   * NPM clientlib產生器會從SPA專案建立使用者端程式庫。
   * 該程式庫由Maven取得，並由Maven Build外掛程式與元件部署到AEM作者。

* **AEM 作者**

  內容是在AEM作者上建立的，包括編寫SPA。

  在製作環境中使用SPA編輯器編輯SPA時：

   1. SPA要求外部HTML。
   1. CSS已載入。
   1. SPA應用程式的JavaScript已載入。
   1. 執行SPA應用程式時，系統會要求JSON，讓應用程式建立頁面的DOM，包括 `cq-data` 屬性。
   1. 此 `cq-data` 屬性可讓編輯器載入其他頁面資訊，以便知道哪些編輯設定可供元件使用。

* **AEM 發佈**

  其中發佈編寫的內容和編譯的程式庫(包括SPA應用程式成品、使用者端程式庫和元件)以供公眾使用。

* **Dispatcher / CDN**

  Dispatcher是網站訪客的AEM快取階層。
   * 請求的處理方式與它們在AEM作者上的處理方式類似。 不過，不會要求頁面資訊，因為只有編輯器需要它。
   * 快取JavaScript、CSS、JSON和HTML，最佳化頁面以快速傳送。

>[!NOTE]
>
>在AEM內部，不需要執行JavaScript建置機制或執行JavaScript本身。 AEM僅代管來自SPA應用程式的編譯成品。

## 後續步驟 {#next-steps}

* [開始在 AEM 中使用 React 建立 SPA](getting-started-react.md)展示如何在 AEM 中使用 React 建立基本 SPA 以與 SPA 編輯器搭配運作.
* [開始在 AEM 中使用 Angular 建立 SPA](getting-started-angular.md)展示如何在 AEM 中使用 Angular 建立基本 SPA 以與 SPA 編輯器搭配運作.
* [SPA 編輯器概述](editor-overview.md)更深入地介紹 AEM 和 SPA 之間的通訊模型。
* [WKND SPA專案](wknd-tutorial.md) 是逐步教學課程，在AEM中實作簡單的SPA專案。
* [SPA的動態模型到元件對應](model-to-component-mapping.md) 說明動態模型到元件的對應，以及它如何在AEM的SPA中運作。
* [SPA Blueprint](blueprint.md) 讓您深入瞭解SPA SDK for AEM的運作方式，以防您想要在AEM中針對React或Angular以外的架構實作SPA。 或者，您只想要更深入的瞭解。
