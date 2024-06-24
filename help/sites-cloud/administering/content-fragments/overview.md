---
title: 使用內容片段的概觀
description: 瞭解AEMas a Cloud Service中的內容片段如何讓您建立和使用內容；適合Headless傳送和頁面編寫。
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 4%

---

# 使用內容片段的概觀 {#overview-working-with-content-fragments}

透過Adobe Experience Manager (AEM)as a Cloud Service，內容片段可讓您設計、建立、組織和 [發佈獨立於頁面的內容](/help/sites-cloud/authoring/fragments/content-fragments.md). 它們可讓您準備內容以用於多個位置和多個管道，非常適合Headless傳送和頁面製作。

>[!IMPORTANT]
>
>可以從兩個主控台存取內容片段： **內容片段** 和 **資產**.
>
>此外，還有兩個編輯器可用於內容片段。 （兩個編輯器都可從兩個主控台存取。）
>
>本節將說明 **內容片段** 主控台與 *新* 內容片段編輯器。 這些是針對Headless內容傳送開發的（儘管可用於所有情境）
>
>如需進一步詳細資訊，請參閱：
>
>* 使用 **資產** 主控台 [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用 [*原始* 內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)，
>* 使用 [用於頁面編寫的內容片段](/help/sites-cloud/authoring/fragments/content-fragments.md).


內容片段包含結構化內容：

* 每個片段都根據 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * 內容片段模式會定義產生片段的結構。
* 每個片段都包含：
   * **[主要](#main-and-variations)**  — 包含核心內容的片段整體部分；永遠存在，無法刪除
   * **[變數](#main-and-variations)**  — 內容的一個或多個排列，由作者建立
* 此結構的範圍介於：
   * 基本
      * 例如，單一多行文字欄位。
      * 可用來準備直接的內容以用於頁面製作。
      * 也可用於向您的應用程式傳送Headless。
   * 複雜
      * 多種資料型別的欄位組合，包括文字、數字、布林值、日期與時間等。
      * 可用於為頁面編寫準備更多結構化內容，或用於向您的應用程式傳送headless。
   * 巢狀
      * 可用的參考資料型別可讓您巢狀內嵌內容。
      * 通常用於向您的應用程式進行Headless傳送。

使用AEM核心元件的Sling模型(JSON)匯出功能，內容片段也可以以JSON格式傳送。 此傳遞形式：

* 可讓您使用元件來管理要傳送片段的哪些元素
* 允許大量傳送；透過新增多個 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 在用於API傳送的頁面上

通訊管道的數量每年都在增加。 通常，管道是指傳遞機制，例如：

* 實體管道；例如，桌上型電腦、行動裝置。
* 實體管道中的傳遞形式；例如，「產品詳細資料頁面」、「產品類別頁面」（適用於案頭）或「行動網頁」（適用於行動應用程式）。

不過，您（可能）不想要使用 *精確* 所有頻道使用相同內容 — 您需要根據特定頻道最佳化內容。

內容片段允許您：

* 考慮如何跨頻道有效率地觸及目標對象。
* 建立並管理頻道中性的編輯內容。
* 為一系列管道建立內容集區。
* 為特定管道設計內容變體。
* 透過插入資產將影像新增至文字。
* 建立巢狀內容以反映資料的複雜性。

接著，您就可以組合這些內容片段，透過各種管道提供體驗。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-cloud/authoring/fragments/content-fragments.md)** 是AEM中的不同功能：
>* **內容片段** 是可編輯內容，具備定義與結構，但無其他視覺化設計及/或版面配置。 它們可用於存取結構化資料，包括文字、數字和日期等。
>* **體驗片段** 是完全佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。
>
>如需詳細資訊，請參閱 [瞭解AEM中的內容片段和體驗片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

本頁和下列頁面涵蓋建立、設定、維護及使用內容片段的任務：

* [為您的執行個體啟用內容片段功能](/help/sites-cloud/administering/content-fragments/setup.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)  — 啟用、建立和定義您的模型
* [建立您的內容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) （使用內容片段控制檯）

建立片段後，您可以：

* [使用內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md)  — 存取、發佈（預覽或生產）和參考您的片段
* [使用內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)  — 編輯、發佈（預覽或生產）和參考您的片段
* [分析](/help/sites-cloud/administering/content-fragments/analysis.md)  使用編輯器的內容片段結構
* [使用GraphQL存取您的片段，以將Headless傳送至您的應用程式](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [或使用您的片段進行頁面製作](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>這些頁面可搭配下列專案一起閱讀：
>
>* [自訂和擴充內容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [轉譯專用內容片段設定元件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [與內容片段搭配使用的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [使用內容片段編寫頁面](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* 也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。


## 主要和變數 {#main-and-variations}

變數是AEM內容片段的一項重要功能。 它們可讓您建立並編輯 **主要** 用於特定頻道和情境的內容，讓headless內容傳送和頁面製作更加靈活。

* **主要**

   * **主要** 本身不是變數，而是所有變數的基礎。
   * 片段的一個組成部分

      * 每個內容片段都有一個例項 **主要**.
      * **主要** 無法刪除。

   * **主要** 可在下的片段編輯器中存取 **[變數](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >在可從取得的編輯器中 **資產** 主控台， **主要** 標籤為 **主版**.

* **變數**

   * 片段文字的轉譯是編輯目的所特有的；可能與頻道相關，但不是強制性的，也可以用於臨機本機修改。
   * 建立為的復本 **主要**，但接著可視需求進行編輯；變數本身之間通常會有內容重疊。
   * 可以在片段製作期間定義；從左側面板。
   * 儲存在片段中，有助於避免內容副本的散佈。
   * 變數可以是 [已比較和同步](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) 替換為 **主要**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## 內容片段與內容服務 {#content-fragments-and-content-services}

AEM Content Services的設計目的，是要概括AEM內/外部內容的說明和傳遞，而不只是關注網頁。

它們使用可供任何使用者端使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。 這些管道可能包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他管道和接觸點

使用JSON匯出工具以JSON格式進行傳遞。

AEM內容片段可用於說明和管理結構化內容。 結構化內容在可包含各種內容型別的模型中定義；包括文字、數值資料、布林值、日期和時間等。

此結構化內容與AEM核心元件的JSON匯出功能搭配使用，可用於將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>另請參閱 [Headless和AEM](/help/headless/introduction.md) 介紹AEM Sites的Headless開發as a Cloud Service。

>[!NOTE]
>
>AEM也支援翻譯片段內容。 另請參閱 [翻譯資產](/help/assets/translate-assets.md) 以取得進一步資訊。

## 內容類型 {#content-type}

內容片段包括：

* A **網站** 功能。

* 儲存為 **資產**：

   * 內容片段（及其變數）可以透過以下網址建立及維護： [內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * 在中製作和編輯 [內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md).

* 可使用進行內容傳送 [AEM GRAPHQL API](/help/headless/graphql-api/content-fragments.md).

* 可在 [使用內容片段元件的頁面編輯器](/help/sites-cloud/authoring/fragments/content-fragments.md) （參照元件）：

   * 此 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 可供頁面作者使用。 它可讓他們以HTML或JSON格式參考及傳送所需的內容片段。

內容片段是內容結構，具備以下功能：

* 沒有版面配置或設計（文字欄位可設定文字格式）。
* 獨立於傳遞機制（例如頁面或頻道）。
* 包含一或多個， [組成部分](#constituent-parts-of-a-content-fragment).
* 可以 [包含或連線到影像](#fragments-with-visual-assets).

### 具有視覺資產的片段 {#fragments-with-visual-assets}

為了讓作者更能掌控其內容，可以將影像新增至內容片段及/或與內容片段整合。

資產可以透過數個方式與內容片段一起使用；各有其優點：

* as a **內容參考**
* 在 **多行文字** 欄位

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分（直接或間接）組成：

* **片段元素**

   * 元素會與儲存內容的資料欄位建立關聯。
   * 您使用 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) 以建立內容片段。 模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是各種資料型別。

* **片段段落**

   * 以個別實體分隔的文字區塊，通常為多行。

   * 在頁面製作期間啟用內容控制。

* **片段中繼資料**

   * 使用 [資產中繼資料結構](/help/assets/metadata-schemas.md).
   * 標籤可在以下情況下建立：

      * 建立和編寫片段
      * 或以後，當您 [檢視或編輯屬性](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) 在片段編輯器中時

  >[!CAUTION]
  >
  >中繼資料處理設定檔不適用於內容片段。

  >[!CAUTION]
  >
  >內容片段模型通常可以定義資料欄位，名為 **標題** 和 **說明**. 如果這兩個欄位存在，則為使用者定義的欄位，並可在編輯器的內容區域中更新。
  >
  >內容片段及其變數也有稱為的中繼資料（屬性）欄位 **標題** 和 **說明**. 這兩個中繼資料欄位是任何內容片段和變數的組成部分，最初在建立片段時定義。 您可以在編輯器的屬性/中繼資料區域中更新它們。

* **[主要](#main-and-variations)**
* **[變數](#main-and-variations)**

### 片段必填 {#required-by-fragments}

若要建立內容片段，您需要：

* **內容模型**

   * 為 [使用設定瀏覽器啟用](/help/sites-cloud/administering/content-fragments/setup.md).
   * 為 [使用工具建立](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * 必填 [建立片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容片段模型定義需要標題和一個資料元素，其他內容都是選用的。
   * 模型可定義預設內容（如果適用）。
   * 作者在製作片段內容時無法變更已定義的結構；雖然他們可以從片段編輯器開啟模式編輯器。
   * 建立相依內容片段後對模型所做的變更可能會影響這些內容片段。

若要將您的內容片段用於Headless內容傳送，您還需要：

* a [GraphQL查詢](/help/headless/graphql-api/content-fragments.md) 以要求必要的內容
* 然後，此內容可用於開發您自己的SPA for AEM；如需詳細資訊，請檢閱下列檔案：

   * [SPA WKND 教學課程](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [使用 React 快速入門](/help/implementing/developing/hybrid/getting-started-react.md)
   * [使用 Angular 快速入門](/help/implementing/developing/hybrid/getting-started-angular.md)

若要使用您的內容片段進行頁面製作，您還需要：

* A **內容片段元件**

   * 有助於以HTML和/或JSON格式傳送片段。
   * 必填 [在頁面上參考片段](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * 負責片段的佈局和傳遞；例如管道。
   * 片段需要一或多個專用元件來定義版面並傳遞部分或全部元素/變數和關聯內容。
   * 在製作中將片段拖曳到頁面上會自動建立所需元件的關聯。
   * 請參閱 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html).

## 使用範例 {#example-usage}

片段及其元素和變數可用於為多個管道建立一致的內容。 在設計片段時，您需要考慮將使用的內容以及位置。

### WKND範例 {#wknd-sample}

此 [WKND網站和WKND共用](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 提供範例來協助您瞭解AEMas a Cloud Service。

<!-- CHECK: which links can/should be used these days? -->

WKND專案包括：

* 內容片段模型可在以下位置取用：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 內容片段 (和其他內容) 可在以下位置取用：

   * `.../assets.html/content/dam/wknd/en`
