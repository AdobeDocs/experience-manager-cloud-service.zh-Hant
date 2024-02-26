---
title: 組織頁面
description: 瞭解如何使用AEM組織您的網站。
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 3%

---


# 組織頁面 {#creating-and-organizing-pages}

瞭解如何使用AEM組織您的網站。 瞭解如何組織頁面後，您可以 [建立新頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md) 和 [管理現有頁面。](/help/sites-cloud/authoring/sites-console/managing-pages.md)

{{edge-delivery-authoring}}

## 組織您的網站 {#organizing-your-site}

身為作者，您需要在AEM中組織您的網站。 這涉及建立和命名內容頁面，以便：

* 您可以在作者環境中輕鬆找到他們
* 您網站的訪客可在發佈環境中輕鬆瀏覽這些專案

您也可以使用 [資料夾](#creating-a-new-folder) 協助組織您的內容。

網站的結構可視為儲存內容頁面的樹狀結構。 這些內容頁面的名稱會用於組成URL，而標題則會在檢視頁面內容時顯示。

以下範例將來自 [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 網站，其中有一篇關於滑板場(`la-skateparks`)已存取：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

此結構可從下列位置檢視： [**網站** 主控台，](/help/sites-cloud/authoring/sites-console/introduction.md) 您可以在此瀏覽網站的各個頁面，並在頁面上執行動作。

## 頁面命名慣例 {#page-naming-conventions}

建立頁面時，有兩個索引鍵欄位：

* **[標題](#title)**：
   * 主控台會向使用者顯示這項資訊，並在編輯時顯示在頁面內容的頂端。
   * 此欄位為必填。
* **[名稱](#name)**：
   * 這會用來產生URI。
   * 此欄位的使用者輸入為選用。 如果未指定，則會從標題衍生名稱。 請參閱下節 [頁面名稱限制和最佳實務](#page-name-restrictions-and-best-practices) 以取得詳細資訊。

### 頁面名稱限制和最佳實務 {#page-name-restrictions-and-best-practices}

頁面 **標題****和名稱可以單獨建立** ，但是是相關的：

* 建立頁面時，僅 **標題** 欄位為必填。 若否 **名稱** 在建立頁面時提供，AEM會從標題的前64個字元產生名稱（觀察以下列出的驗證）。 僅前64個字元用於支援短頁面名稱的最佳做法。
* 如果作者手動指定頁面名稱，64字元限制不適用，但頁面名稱長度的其他技術限制可能適用。

>[!TIP]
>
>定義頁面名稱時，一個好的經驗法則是保持頁面名稱簡短，但儘可能表達到位且容易記憶，讓讀者容易理解。 請參閱 [W3C風格指南](https://www.w3.org/Provider/Style/TITLE.html) 針對 `title` 元素以取得詳細資訊。
>
>也請記住，某些瀏覽器（例如舊版的IE）只能接受一定長度的URL，因此還有技術原因需縮短頁面名稱。

建立頁面時，AEM [根據慣例驗證頁面名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。

允許的最小字元為：

* `a` 到 `z`
* `A` 到 `Z`
* `0` 到 `9`
* `_` （底線）
* `-` （連字型大小/減號）

所有允許字元的完整詳細資訊可在以下連結中找到： [命名慣例](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>頁面名稱長度上限為150個字元。

### 標題 {#title}

如果您只提供頁面 **標題** 建立頁面時，AEM會衍生頁面 **名稱** 來自此字串和 [根據慣例驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。

A **標題** 接受包含無效字元的欄位，但衍生的名稱會以無效的字元取代。 例如：

| 標題 | 衍生名稱 |
|---|---|
| Schon | `schoen.html` |
| SC%&amp;&#42;c+ | `sc---c-.html` |

### 名稱 {#name}

當您提供頁面時 **名稱** 建立頁面時，AEM [根據慣例驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。 您無法在中提交無效的字元 **名稱** 欄位。 當AEM偵測到無效字元時，此欄位會以說明訊息強調顯示。

![輸入無效頁面名稱的範例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>除非是語言根，否則應避免使用ISO-639-1定義的雙字母代碼作為頁面名稱。
>
>另請參閱 [準備翻譯內容](/help/sites-cloud/administering/translation/preparation.md) 以取得詳細資訊。

## 範本 {#templates}

在AEM中， [範本](/help/sites-cloud/authoring/sites-console/templates.md) 是特殊型別的頁面，用來作為建立任何新頁面的基礎。

範本定義包含縮圖影像和其他屬性的頁面結構。 例如，您可以為產品頁面、Sitemap和聯絡資訊使用不同的範本。 範本包括 [元件](#components).

AEM隨附幾個現成可用的範本。 可用的範本視個別網站而定。 主要欄位包括：

* **標題**  — 產生的網頁上顯示的標題
* **名稱**  — 用於命名頁面
* **範本**  — 產生新頁面時可使用的範本清單

## 元件 {#components}

[元件](/help/implementing/developing/components/overview.md) 是AEM提供的元素，因此您可以新增特定型別的內容。 AEM隨附一系列現成可用的元件，稱為 [核心元件、](/help/implementing/developing/components/overview.md#core-components) 功能齊全。 以下是元件的一些範例：

* 文字
* 影像
* 標題
* 傳送
* 以及更多功能

建立並開啟頁面後，您可以 [使用元件新增內容](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component)，可從取得 [元件瀏覽器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>此 [元件主控台](/help/sites-cloud/authoring/components-console.md) 提供執行個體上元件的概述。
