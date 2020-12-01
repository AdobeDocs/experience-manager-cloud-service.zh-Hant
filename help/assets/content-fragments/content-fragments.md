---
title: 使用內容片段
description: 瞭解Adobe Experience Manager(AEM)中的內容片段如何讓您設計、建立、組織和使用不受頁面影響的內容。
translation-type: tm+mt
source-git-commit: 468d6f6a87c9a4794d5187146f7d879433cafa6f
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 3%

---


# 使用內容片段{#working-with-content-fragments}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

>[!CAUTION]
>
>AEM GraphQL API（針對內容片段傳送）將於2021年初發行。
>
>相關檔案已可供預覽使用。

以Adobe Experience Manager(AEM)為雲端服務，內容片段可讓您設計、建立、組織及[發佈不受頁面影響的內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。 它們可讓您準備內容，以便在多個位置／多個通道中使用。

內容片段包含結構化內容：

* 它們以[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)為基礎，該模型預先定義了產生片段的結構。
* 結構可以介於：
   * 基本
      * 例如，單行、多行文字欄位。
      * 可用來準備直接的內容，以便用於頁面製作。
   * 複雜
      * 多種不同資料類型的欄位組合，包括文字、數字、布林值、資料和時間等。
      * 可用於準備更多結構化內容以製作頁面，或傳送至您的應用程式。

<!--
  * Nested
    * The reference data types available allow you to nest your content.
    * Tends to be used for delivery to your application.
-->

內容片段也可以使用AEM核心元件的Sling Model(JSON)匯出功能，以JSON格式傳送。 這種交付形式：

* 可讓您使用元件來管理要傳送的片段元素
* 允許大量傳送，方法是在用於API傳送的頁面上新增多個內容片段核心元件

本頁及下列各頁涵蓋建立、設定、維護和使用您的內容片段的工作：

* [為您的例項啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) -啟用、建立和定義模型
* [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md) -建立您的內容片段；然後編輯、發佈和參考
* [變數——製作片段內容](/help/assets/content-fragments/content-fragments-variations.md) -製作片段內容並建立主版的變數
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)  —— 使用Markdown語法建立片段
* [使用關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) -添加關聯內容
* [中繼資料——片段屬性](/help/assets/content-fragments/content-fragments-metadata.md) -檢視和編輯片段屬性
* 使用[內容片段和GraphQL來傳送內容](/help/assets/content-fragments/content-fragments-graphql.md)以用於您的應用程式。 若要提供協助，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

>[!NOTE]
>
>這些頁面可與以下內容一起閱讀：
>
>* [使用內容片段製作頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
>* [自訂和擴充內容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [轉譯專用內容片段設定元件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API，用於內容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)


通訊頻道的數量逐年增加。 通常渠道是指傳送機制，例如：

* 物理通道；例如桌上型電腦、行動裝置。
* 實體渠道的交付形式；例如，「產品詳細資訊頁面」、「產品類別頁面」（適用於桌上型電腦）或「行動網頁」（適用於行動裝置）、「行動應用程式」（適用於行動裝置）。

不過，您（可能）不想針對所有通道使用完全相同的內容——您需要根據特定通道最佳化您的內容。

內容片段可讓您：

* 考慮如何跨通道有效觸及目標受眾。
* 建立並管理不受頻道影響的編輯內容。
* 建立適用於各種通道的內容池。
* 針對特定通道設計內容變化。
* 插入資產（混合媒體片段），將影像新增至文字。

<!--
* Create nested content to reflect the complexity of your data.
-->

然後，這些內容片段可以組合起來，以透過多種通道提供體驗。

>[!NOTE]
>
>**內容** 片段和 **[體驗](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** 片段是AEM中的不同功能：
>* **內容** 片段是編輯內容，可用來存取結構化資料，包括文字、數字和日期等。它們是純內容，具有定義和結構，但不需額外的視覺設計和／或版面。
>* **體驗** 片段內容已完整排版；網頁的片段。

>
>
「體驗片段」可以包含內容片段的形式，但不能以相反的方式包含。
>
>如需詳細資訊，請參閱[瞭解AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments)中的內容片段和體驗片段。

## 內容片段和內容服務{#content-fragments-and-content-services}

AEM Content Services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。

它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。 這些渠道可以包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他通道和觸點

使用JSON匯出器以JSON格式進行傳送。

AEM內容片段可用來描述和管理結構化內容。 結構化內容定義在可包含多種內容類型的模型中；包括文字、數值資料、布林值、日期和時間等。

此結構化內容可搭配AEM核心元件的JSON匯出功能，用來將AEM內容傳送至AEM頁面以外的通道。

>[!NOTE]
>
>如需AEM Sites的雲端服務無頭開發簡介，請參閱[無頭和AEM](/help/implementing/developing/headless/introduction.md)。

>[!NOTE]
>
>AEM也支援片段內容的轉譯。

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## 內容類型 {#content-type}

內容片段包括：

* 儲存為&#x200B;**Assets**:

   * 內容片段（及其變化）可從&#x200B;**Assets**&#x200B;主控台建立和維護。
   * 在「內容片段編輯器」中撰寫和編輯。

* 在[頁面編輯器中，借助內容片段元件](/help/sites-cloud/authoring/fundamentals/content-fragments.md)（引用元件）使用：

   * **內容片段**&#x200B;元件可供頁面作者使用。 它可讓使用者參考並傳送HTML或JSON格式的必要內容片段。

* 使用[AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)存取。

內容片段是一種內容結構，可：

* 沒有版面或設計（在Rich Text模式中可能有某些文字格式）。
* 包含一個或多個[組成部分](#constituent-parts-of-a-content-fragment)。
* 可以[包含或連接到images](#fragments-with-visual-assets)。
* 在頁面上參考時，可使用[in-between內容](#in-between-content-when-page-authoring-with-content-fragments)。

* 獨立於傳送機制（即頁面、頻道）。

### 具有視覺資產{#fragments-with-visual-assets}的片段

為了讓作者更能控制其內容，可將影像新增至內容片段及／或與內容片段整合。

資產可以幾種方式與內容片段搭配使用；各自各有優勢：

* **插入** Assento片段（混合媒體片段）

   * 是片段的一個完整部分（請參閱[內容片段的組成部分](#constituent-parts-of-a-content-fragment)）。
   * 定義資產的位置。
   * 如需詳細資訊，請參閱片段編輯器中的[將資產插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。

   >[!NOTE]
   >
   >插入到內容片段本身的視覺資產附加在前段。 將片段新增至頁面時，這些資產會在新增中間內容時相對於該段落移動。

* **相關聯的內容**

   * 連接到碎片；但不是片段的固定部分（請參閱內容片段的[組成部分](#constituent-parts-of-a-content-fragment)）。
   * 提供一定的定位彈性。
   * 在頁面上使用片段時，可輕鬆使用（當成中間內容）。
   * 如需詳細資訊，請參閱[關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md)。

* 頁面編輯器的「 **資產** 」瀏覽器可用的資產

   * 允許完全彈性地選擇資產。
   * 提供一定的定位彈性。
   * 不提供特定片段的核准概念。
   * 如需詳細資訊，請參閱[資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。

### 內容片段的組成部分{#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分（直接或間接）組成：

* **片段元素**

   * 元素會關聯至包含內容的資料欄位。
   * 您使用內容模型來建立內容片段。 在模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是多種資料類型。

* **片段段落**

   * 以個別實體分隔的文字區塊，通常為多行。

   * 在富 [文本](/help/assets/content-fragments/content-fragments-variations.md#rich-text)[](/help/assets/content-fragments/content-fragments-variations.md#markdown) 和標籤下拉模式中，段落可以格式化為標題，在這種情況下，它和以下段落作為一個單位一起組成。

   * 在製作頁面時啟用內容控制。

* **插入片段的資產（混合媒體片段）**

   * 插入實際片段並用作片段內部內容的資產（影像）。
   * 嵌入片段的段落系統中。
   * 可在頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)上使用／參考[片段時格式化。
   * 只能使用片段編輯器將片段添加到片段、從中刪除或在其中移動。 這些動作無法在頁面編輯器中執行。
   * 只能在片段編輯器](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)中使用[Rich Text格式將片段添加到片段、從中刪除或移動到片段中。
   * 只能新增至多行文字元素（任何片段類型）。
   * 附於前文（段）。

      >[!CAUTION]
      >
      >資產可以（不慎）切換為純文字格式，從片段中移除。

      >[!NOTE]
      >
      >當在頁面上使用片段時，也可將資產新增為[其他（介於）內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content);使用「資產」瀏覽器中的「關聯內容」或「資產」。

* **相關聯的內容**

   * 這是片段外部的內容，但與編輯相關。 通常是影像、視訊或其他片段。
   * 當系列中的個別資產新增至頁面時，可與頁面編輯器中的片段搭配使用。 這表示它們是可選的，具體取決於特定渠道的要求。
   * 這些資產透過系列[與片段相關聯；關聯的系列可讓作者決定在編寫頁面時要使用哪些資產。](/help/assets/content-fragments/content-fragments-assoc-content.md)

      * 系列可以與片段相關聯，做為預設內容，或由作者在編寫片段時建立。
      * [資產(DAM)收](/help/assets/manage-collections.md) 集是片段相關內容的基礎。
   * （可選）您也可以將片段本身新增至系列，以協助追蹤。

* **片段中繼資料**

   * 使用[Assets中繼資料結構](/help/assets/metadata-schemas.md)。
   * 標籤可在下列情況下建立：

      * 建立並編寫片段
      * 或更新版本：

         * 通過從控制台檢視／編輯片段&#x200B;**屬性**
         * 在片段編輯器中編輯&#x200B;**中繼資料**

   >[!CAUTION]
   >
   >中繼資料處理設定檔不適用於內容片段。

* **主版**

   * 碎片的一個整體

      * 每個內容片段都有一個主體實例。
      * 無法刪除主版。
   * 主版可在&#x200B;**[Valuations](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;下的片段編輯器中存取。
   * 主變數不是變數，而是所有變數的基礎。


* **變數**

   * 轉譯特定於編輯目的的片段文字；可以與頻道相關，但非強制性，也可以是臨機本機修改。
   * 建立為&#x200B;**Master**&#x200B;的副本，但隨後可根據需要進行編輯；這些變化本身之間通常有內容重疊。
   * 可在編寫片段時定義。
   * 儲存在片段中，以協助避免內容復本散布。
   * 如果主版內容已更新，則變化可以與主版[synchronized](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)一起使用。
   * 可以是[Agmurated](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)，以快速將文字截斷為預先定義的長度。
   * 可在片段編輯器的[Valuations](/help/assets/content-fragments/content-fragments-variations.md)標籤下使用。

### 使用內容片段製作頁面時的內容介於{#in-between-content-when-page-authoring-with-content-fragments}

中間內容：

* 在使用內容片段時，可在頁面編輯器中使用。
* 在頁面上使用／參考片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content)後，會在片段的流程中加入[其他內容。
* 在使用內容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md)時，可在[頁面編輯器中使用。
* 您可以將中間內容新增至任何片段，其中只有一個元素可見。
* 可使用相關的內容，也可使用適當瀏覽器的資產和／或元件。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

### 片段{#required-by-fragments}所需

若要建立內容片段，您需要：

* **內容模型**

   * 使用配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)啟用[。
   * 是使用Tools](/help/assets/content-fragments/content-fragments-models.md)建立的[。
   * 建立片段[所需。](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容模型定義需要一個標題和一個資料元素；其他一切都是可選的。
   * 模型可以定義預設內容（如果適用）。
   * 製作片段內容時，作者無法變更已定義的結構。
   * 在建立相依內容片段後對模型所做的變更可能會影響這些內容片段。

若要將內容片段用於頁面製作，您還需要：

* **內容片段元件**

   * 有助於以HTML和／或JSON格式傳送片段。
   * [參考頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)上的片段時需要。
   * 負責片段的排版和傳送；即頻道。
   * 片段需要一個或多個專用元件來定義版面，並傳送部分或所有元素／變化和相關內容。
   * 將片段拖曳至編寫時的頁面，將會自動關聯所需的元件。

## 使用範例{#example-usage}

片段及其元素和變化可用於為多個通道建立相干內容。 在設計片段時，您需要考慮將使用哪些內容。

### WKND示例{#wknd-sample}

提供[WKND網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md)範例，協助您瞭解AEM為雲端服務。 其中包含範例片段，您可在以下網址查看：

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
