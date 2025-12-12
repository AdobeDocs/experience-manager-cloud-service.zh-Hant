---
title: 使用內容片段的概念和最佳實務概觀
description: 瞭解Adobe Experience Manager (AEM) as a Cloud Service中的內容片段如何讓您建立和使用結構化內容；非常適合於Headless傳送和頁面編寫。
feature: Content Fragments
role: User, Developer
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 2449bc380268ed42b6c8d23ae4a4fecaf1736889
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 3%

---

# 使用內容片段 — 概念與最佳實務 {#working-with-content-fragments-concepts-and-best-practices}

透過Adobe Experience Manager (AEM) as a Cloud Service，內容片段可讓您設計、建立、管理和發佈獨立於頁面的內容。 它們可讓您準備內容以用於多個位置及多個管道，非常適合[Headless傳遞](/help/headless/what-is-headless.md)及[頁面製作](/help/sites-cloud/authoring/fragments/content-fragments.md)。

>[!IMPORTANT]
>
>本節中說明的許多功能&#x200B;*僅*&#x200B;可在[Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md)中使用；因此&#x200B;*線上* Adobe Experience Manager (AEM) as a Cloud Service，而不是本機執行個體。

>[!IMPORTANT]
>
>可以從兩個主控台存取內容片段： **內容片段**&#x200B;和&#x200B;**Assets**。
>
>編寫內容片段時也有兩個編輯器；雖然基本功能相同，但有一些差異。 兩個編輯器都可從兩個主控台存取。
>
>本節處理&#x200B;**內容片段**&#x200B;主控台和&#x200B;*新*&#x200B;內容片段編輯器。 這些是針對Headless內容傳送開發的（儘管可用於所有情境）
>
>如需進一步詳細資訊，請參閱：
>
>* 使用&#x200B;**Assets**&#x200B;主控台進行[管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用&#x200B;[*原始*&#x200B;內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)，
>* 使用[內容片段進行頁面編寫](/help/sites-cloud/authoring/fragments/content-fragments.md)。


內容片段包含結構化內容：

* 每個片段都以[內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)為基礎。
   * [內容片段模型定義了結果片段的結構](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)。
* 每個片段都包含：
   * **[Main](#main-and-variations)** — 包含核心內容的片段整體部分；永遠存在，無法刪除
   * **[變數](#main-and-variations)** — 作者建立的一或多個內容排列
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
* 允許大量傳送；方法是在用於API傳送的頁面上新增多個[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)

通訊管道的數量每年都在增加。 通常，管道是指傳遞機制，例如：

* 實體管道；例如，桌上型電腦、行動裝置。
* 實體管道中的傳遞形式；例如，「產品詳細資料頁面」、「產品類別頁面」（適用於案頭）或「行動網頁」（適用於行動應用程式）。

不過，您（可能）不想對所有頻道使用&#x200B;*完全*&#x200B;相同的內容 — 您需要根據特定頻道最佳化您的內容。

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
>**內容片段**&#x200B;和&#x200B;**[體驗片段](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;是AEM中的不同功能：
>
>* **內容片段**&#x200B;是可編輯內容，具有定義和結構，但沒有額外的視覺設計和/或版面配置。 它們可用於存取結構化資料，包括文字、數字和日期等。
>* **體驗片段**&#x200B;是完整佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。
>
>如需進一步資訊，請參閱[瞭解AEM中的內容片段和體驗片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments)。

本頁和下列頁面涵蓋建立、設定、維護及使用內容片段的任務：

* [為您的執行個體啟用內容片段功能](/help/sites-cloud/administering/content-fragments/setup.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) — 啟用、建立和[定義您的模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [建立您的內容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) （使用內容片段主控台）

建立片段後，您可以：

* [使用內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md) -：
   * 存取、發佈（以預覽或生產）和參考您的片段
* [使用內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md) -：
   * 編輯、發佈（以預覽或生產）和參考您的片段
   * 使用評論與其他作者共同作業
* [使用編輯器分析](/help/sites-cloud/administering/content-fragments/analysis.md)內容片段的結構
* [使用GraphQL存取您的片段，以將Headless傳遞至您的應用程式](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)。
* [在Adobe Journey Optimizer中整合併使用您的內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-with-journey-optimizer.md)
* 建立及管理內容片段的[啟動](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)
* [或使用您的片段進行頁面製作](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>這些頁面可搭配下列專案一起閱讀：
>
>* [自訂和擴充內容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [轉譯專用內容片段設定元件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [與內容片段搭配使用的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* 使用內容片段[編寫頁面](/help/sites-cloud/authoring/fragments/content-fragments.md)。
>* 也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。


## 主要和變數 {#main-and-variations}

變數是AEM內容片段的一項重要功能。 它們可讓您建立並編輯&#x200B;**主要**&#x200B;內容的復本，以用於特定管道和情境，使Headless內容傳送和頁面製作更加靈活。

* **主要**

   * **主要**&#x200B;本身不是變數，而是所有變數的基礎。
   * 片段的一個組成部分

      * 每個內容片段都有一個&#x200B;**主要**&#x200B;的執行個體。
      * 無法刪除&#x200B;**主要**。

   * **Main**&#x200B;可在&#x200B;**[變數](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**&#x200B;下的片段編輯器中存取。

  >[!NOTE]
  >
  >在&#x200B;**Assets**&#x200B;主控台可用的編輯器中，**Main**&#x200B;標示為&#x200B;**Master**。

* **變數**

   * 片段文字的轉譯是編輯目的所特有的；可能與頻道相關，但不是強制性的，也可以用於臨機本機修改。
   * 建立為&#x200B;**主要**&#x200B;的復本，但之後可視需要加以編輯；變數本身之間通常會有內容重疊。
   * 可以在片段製作期間定義；從左側面板。
   * 儲存在片段中，有助於避免內容副本的散佈。
   * 變數可以是[與](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text)主要&#x200B;**比較和同步化**。
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## 內容片段與內容服務 {#content-fragments-and-content-services}

AEM Content Services的設計目的，是要概括AEM內/外部內容的說明和傳遞，而不只是關注網頁。

這些頻道使用任何使用者端都能使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。 這些管道可能包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他管道和接觸點

使用JSON匯出工具以JSON格式進行傳遞。

AEM內容片段可用於說明和管理結構化內容。 結構化內容在可包含各種內容型別的模型中定義；包括文字、數值資料、布林值、日期和時間等。

此結構化內容與AEM核心元件的JSON匯出功能搭配使用，可用於將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>請參閱[Headless與AEM](/help/headless/introduction.md)，瞭解AEM Sites as a Cloud Service的Headless開發簡介。

>[!NOTE]
>
>AEM也支援翻譯片段內容。 如需進一步資訊，請參閱[翻譯Assets](/help/assets/translate-assets.md)。

## 內容類型 {#content-type}

內容片段包括：

* **網站**&#x200B;功能。

* 儲存為&#x200B;**Assets**：

   * 內容片段（及其變數）可以從[內容片段主控台](#content-fragments-console)建立及維護。
   * 在[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中編寫與編輯。

* 可使用[AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)進行內容傳送。

* 使用內容片段元件[&#x200B; （參考元件）可在](/help/sites-cloud/authoring/fragments/content-fragments.md)頁面編輯器中取得：

   * [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)可供頁面作者使用。 它可讓他們以HTML或JSON格式參考及傳送所需的內容片段。

內容片段是內容結構，具備以下功能：

* 沒有版面配置或設計（文字欄位可設定文字格式）。
* 獨立於傳遞機制（例如頁面或頻道）。
* 包含一或多個[組成部份](#constituent-parts-of-a-content-fragment)。
* 可以[包含或連線到影像](#fragments-with-visual-assets)。

### 具有視覺Assets的片段 {#fragments-with-visual-assets}

為了讓作者更能掌控其內容，可以將影像新增至內容片段及/或與內容片段整合。

Assets可以透過數個方式與內容片段搭配使用；各有其優點：

* 作為&#x200B;**內容參考**
* 在&#x200B;**多行文字**&#x200B;欄位內

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分（直接或間接）組成：

* **片段元素**

   * 元素會與儲存內容的資料欄位建立關聯。
   * 您使用[內容片段模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)來建立內容片段。 模型中指定的元素（欄位） [定義片段](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)的結構。 這些元素（欄位）可以是各種資料型別。

* **片段段落**

   * 以個別實體分隔的文字區塊，通常為多行。

   * 在頁面製作期間啟用內容控制。

* **片段中繼資料**

   * 使用[Assets中繼資料結構](/help/assets/metadata-schemas.md)。
   * 標籤可在以下情況下建立：

      * 建立和編寫片段
      * 稍後當您在片段編輯器中[檢視或編輯屬性](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags)時

  >[!CAUTION]
  >
  >中繼資料處理設定檔不適用於內容片段。

  >[!CAUTION]
  >
  >內容片段模型通常可以定義名為&#x200B;**Title**&#x200B;和&#x200B;**Description**&#x200B;的資料欄位。 如果這兩個欄位存在，則為使用者定義的欄位，並可在編輯器的內容區域中更新。
  >
  >內容片段及其變數也有稱為&#x200B;**Title**&#x200B;和&#x200B;**Description**&#x200B;的中繼資料（屬性）欄位。 這兩個中繼資料欄位是任何內容片段和變數的組成部分，最初在建立片段時定義。 您可以在編輯器的屬性/中繼資料區域中更新它們。

* **[主要](#main-and-variations)**
* **[變數](#main-and-variations)**

### 片段必填 {#required-by-fragments}

若要建立內容片段，您需要：

* **內容模型**

   * 是否使用組態瀏覽器[啟用](/help/sites-cloud/administering/content-fragments/setup.md)。
   * 是使用內容片段主控台[建立的](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model)。
   * 需要[建立片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments)。
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容片段模型定義需要標題和一個資料元素，其他內容都是選用的。
   * 模型可定義預設內容（如果適用）。
   * 作者在製作片段內容時無法變更已定義的結構；雖然他們可以從片段編輯器開啟模式編輯器。
   * 建立相依內容片段後對模型所做的變更可能會影響這些內容片段。

若要將您的內容片段用於Headless內容傳送，您還需要：

* [GraphQL查詢](/help/headless/graphql-api/content-fragments.md)以請求必要的內容
* 接著，您就可以將此內容用於為AEM開發自己的SPA；如需詳細資訊，請參閱下列檔案：

   * [SPA WKND 教學課程](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [使用 React 快速入門](/help/implementing/developing/hybrid/getting-started-react.md)
   * [使用 Angular 快速入門](/help/implementing/developing/hybrid/getting-started-angular.md)

若要使用您的內容片段進行頁面製作，您還需要：

* **內容片段元件**

   * 有助於以HTML和/或JSON格式傳送片段。
   * 需要[參考頁面](/help/sites-cloud/authoring/fragments/content-fragments.md)上的片段。
   * 負責片段的佈局和傳遞；例如管道。
   * 片段需要一或多個專用元件來定義版面並傳遞部分或全部元素/變數和關聯內容。
   * 在製作中將片段拖曳到頁面上會自動建立所需元件的關聯。
   * 檢視[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)。

## 內容片段主控台 {#content-fragments-console}

內容片段主控台專用於管理、搜尋和建立[內容片段](/help/sites-cloud/administering/content-fragments/managing.md)、[內容片段模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)和[Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)。 它已針對在Headless內容中使用進行了最佳化，但在建立用於頁面編寫的內容片段和內容片段模型時也會使用。

主控台可直接從全域導覽的頂層存取。

![全域導覽 — 內容片段主控台](assets/cf-managing-global-navigation.png)

您可以使用最左側的面板來選取要檢視、瀏覽及管理的資源型別：

![內容片段主控台 — 導覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-navigation.png)

如需詳細資訊，請參閱：

* [內容片段](/help/sites-cloud/administering/content-fragments/managing.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

* 您可以在此主控台中使用一組[鍵盤快速鍵](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md)

>[!CAUTION]
>
>此主控台&#x200B;*僅*&#x200B;可線上上Adobe Experience Manager (AEM) as a Cloud Service中使用。

>[!NOTE]
>
>您的專案團隊可視需要自訂主控台和編輯器。 如需詳細資訊，請參閱[自訂內容片段主控台和編輯器](/help/implementing/developing/extending/content-fragments-console-and-editor.md)。

## 使用範例 {#example-usage}

片段及其元素和變數可用於為多個管道建立一致的內容。 在設計片段時，您需要考慮將使用的內容以及位置。

### WKND範例 {#wknd-sample}

提供[WKND Site和WKND Shared](/help/implementing/developing/introduction/develop-wknd-tutorial.md)範例，協助您瞭解AEM as a Cloud Service。

<!-- CHECK: which links can/should be used these days? -->

WKND專案包括：

* 內容片段模型可在以下位置取用：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 內容片段 (和其他內容) 可在以下位置取用：

   * `.../assets.html/content/dam/wknd/en`

## 最佳做法 {#best-practices}

內容片段可用於形成複雜結構。 Adobe提供在定義及使用模型與片段時最佳實務的建議。

### 保持簡單 {#keep-it-simple}

在AEM中建立結構化內容模型時，請儘可能簡化內容結構，以確保強大的系統效能和簡化的控管。

### 模型數量 {#number-of-models}

視需要建立儘可能多的內容模型，但不用再建立。

太多模型會使控管複雜化，並可能會減慢GraphQL查詢的速度。 一小部分模型（最多數十個）通常就足夠了。 如果您接近數十或更高的數值，請重新考慮您的模型策略。

### 巢狀模型和片段（非常重要） {#nesting-models-and-fragments}

使用內容片段參考避免內容片段巢狀過多或過深，此參考允許片段參考其他片段，有時會跨多個層級。

大量使用內容片段參考資料可能會顯著影響系統效能、UI回應速度和GraphQL查詢執行。 旨在將巢狀結構保持不超過10個層級。

### 每個模型的資料欄位和型別數目 {#number-of-data-fields-and-types-per-model}

僅包含模型真正需要的資料欄位和型別。

過於複雜的模型會導致過於複雜的片段，這會使編寫變得困難並降低編輯器效能。

### RTF欄位 {#rich-text-fields}

考慮使用RTF欄位（**多行文字**&#x200B;資料型別）。

限制每個模型的RTF文字欄位數。 還有每個片段中儲存的文字量，以及HTML格式化的數量。 非常大的RTF內容可能會對系統效能產生負面影響。

### 變化版本數量 {#number-of-variations}

視需要建立儘可能多的片段變數，但僅此而已。

變數會為內容片段增加處理時間、在製作環境中和傳送時。 建議您將變異數維持在可控的最低限度。

最佳實務是每個內容片段不超過十個變數。

### 生產前測試 {#test-before-production}

如有疑問，請先原型設計您預期的內容結構，然後再將其推出至生產環境。 及早的概念證明，加上充分的技術和使用者接受度測試，有助於避免日後生產面臨截止日期時的問題。