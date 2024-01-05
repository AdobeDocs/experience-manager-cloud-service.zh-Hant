---
title: 使用內容片段（資產 — 內容片段）
description: 瞭解Adobe Experience Manager (AEM) as a Cloud Service中的內容片段如何讓您設計、建立、策劃和使用不受頁面影響的內容，適用於頁面製作和headless傳送。 以及它們如何與MSM搭配使用。
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: 62ede258711d0cb8d0b72479559c37221509e23f
workflow-type: tm+mt
source-wordcount: '2222'
ht-degree: 4%

---

# 使用內容片段 {#working-with-content-fragments}

透過Adobe Experience Manager (AEM)as a Cloud Service，內容片段可讓您設計、建立、組織和 [發佈獨立於頁面的內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md). 它們可讓您準備內容以用於多個位置/多個管道，非常適合Headless傳送。 它們也可以搭配 [多網站管理可讓您重複使用內容](#reusing-content-fragments-with-msm-assets).

內容片段包含結構化內容：

* 它們是根據 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)，會預先定義產生片段的結構。
* 此結構的範圍介於：
   * 基本
      * 例如，單一多行文字欄位。
      * 它可用來準備直接的內容以用於頁面編寫。
   * 複雜
      * 多種資料型別的欄位組合，包括文字、數字、布林值、資料和時間等。
      * 它可用來準備更多結構化內容以進行頁面編寫，或傳送給您的應用程式。
   * 巢狀
      * 可用的參考資料型別可讓您巢狀內嵌內容。
      * 通常用於傳遞至您的應用程式。

使用AEM核心元件的Sling模型(JSON)匯出功能，內容片段也可以以JSON格式傳送。 此傳遞形式：

* 可讓您使用元件來管理要傳送片段的哪些元素
* 允許在用於API傳送的頁面上新增多個內容片段核心元件，以大量傳送

>[!NOTE]
>
>內容片段是 Sites 的一項功能，但儲存為&#x200B;**資產**。
>
>他們現在主要透過 **[內容片段](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** 主控台，但仍可從 **資產** 主控台。 本節涵蓋以下專案的管理： **資產** 主控台。
>
>編寫內容片段有兩個編輯器。 本節介紹原始編輯器，主要透過以下網址存取： **資產** 主控台。 請參閱網站檔案， [內容片段 — 製作](/help/sites-cloud/administering/content-fragments/authoring.md)，以取得新編輯器的詳細資訊(主要透過以下網址存取： **內容片段** 主控台)。 兩個編輯器在頂部工具欄中都有一個切換開關，用於提供對另一個編輯器的快速存取。

此和下列頁面涵蓋建立、設定、維護及使用內容片段的任務：

* [為您的執行個體啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 啟用、建立和定義您的模型
* [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 建立您的內容片段；然後編輯、發佈和參考
* [變化 — 編寫片段內容](/help/assets/content-fragments/content-fragments-variations.md)  — 編寫片段內容並建立主控
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)  — 使用片段的Markdown語法
* [使用關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md)  — 新增關聯內容
* [中繼資料 — 片段屬性](/help/assets/content-fragments/content-fragments-metadata.md)  — 檢視和編輯片段屬性
* 使用 [內容片段，連同GraphQL，讓您能傳送內容](/help/assets/content-fragments/content-fragments-graphql.md) 以便在您的應用程式中使用。 若要協助處理此專案，您可以預覽 [JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md).
* [使用MSM對資產重複使用內容片段](#reusing-content-fragments-with-msm-assets)

>[!NOTE]
>
>您可以透過以下方式讀取這些頁面：
>
>* [使用內容片段編寫頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [自訂和擴充內容片段](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [轉譯專用內容片段設定元件](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [與內容片段搭配使用的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)

通訊管道的數量每年都在增加。 通常，管道是指傳遞機制，例如：

* 實體管道；例如，桌上型電腦、行動裝置。
* 實體管道中的傳遞形式；例如，「產品詳細資料頁面」、「產品類別頁面」（適用於案頭）或「行動網頁」（適用於行動應用程式）。

不過，您（可能）不想在所有管道上使用相同的內容 — 您必須根據特定管道將內容最佳化。

內容片段允許您：

* 考慮如何跨頻道有效率地觸及目標對象。
* 建立並管理頻道中性的編輯內容。
* 為一系列管道建立內容集區。
* 為特定管道設計內容變體。
* 透過插入資產（混合媒體片段）將影像新增至文字。
* 建立巢狀內容，讓您可以反映資料的複雜性。

接著，您就可以組合這些內容片段，透過各種管道提供體驗。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** 是AEM中的不同功能：
>* **內容片段** 是可編輯內容，具備定義與結構，但無其他視覺化設計及/或版面配置。 它們可用於存取結構化資料，包括文字、數字和日期等。
>* **體驗片段** 是完全佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。
>
>如需詳細資訊，另請參閱 [瞭解AEM中的內容片段和體驗片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## 內容片段與內容服務 {#content-fragments-and-content-services}

AEM Content Services的設計目的，是要概括AEM內/外部內容的說明和傳遞，而不只是關注網頁。

它們使用可供任何使用者端使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。 這些管道可能包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他管道和接觸點

使用JSON匯出工具以JSON格式進行傳遞。

AEM內容片段可用於說明和管理結構化內容。 結構化內容在可包含各種內容型別（包括文字、數值資料、布林值、日期和時間等）的模型中定義。

此結構化內容與AEM核心元件的JSON匯出功能搭配使用，可用於將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>另請參閱 [Headless和AEM](/help/headless/introduction.md) 介紹AEM Sites的Headless開發as a Cloud Service。

>[!NOTE]
>
>AEM也支援翻譯片段內容。 另請參閱 [翻譯資產](/help/assets/translate-assets.md) 以取得進一步資訊。

## 透過MSM為資產重複使用內容片段 {#reusing-content-fragments-with-msm-assets}

當透過存取時 **資產** 主控台，您可以使用MSM和為您的片段建立即時副本。

如需詳細資訊，請參閱 [使用MSM對資產重複使用內容片段](/help/assets/reuse-assets-using-msm.md). 如此可啟用 [繼承](/help/assets/content-fragments/content-fragments-variations.md#inheritance) 變數和片段的個別欄位。

>[!CAUTION]
>
>如果您想使用MSM （這會建立內容片段的復本），則任何 **獨特** 應從個別專案中使用的任何資料型別中移除限制 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md).

## 內容類型 {#content-type}

內容片段包括：

* 儲存為 **資產**：

   * 內容片段（及其變數）可以透過以下網址建立及維護： **資產** 主控台。
   * 在內容片段編輯器中撰寫和編輯。

* 用於 [依內容片段元件的頁面編輯器](/help/sites-cloud/authoring/fundamentals/content-fragments.md) （參照元件）：

   * 此 **內容片段** 元件可供頁面作者使用。 它可讓他們以HTML或JSON格式參考及傳送所需的內容片段。

* 可使用以下專案存取： [AEM GRAPHQL API](/help/headless/graphql-api/content-fragments.md).

內容片段是內容結構，具備以下功能：

* 沒有版面或設計（RTF模式中可能會使用某些文字格式）。
* 包含一或多個 [組成部分](#constituent-parts-of-a-content-fragment).
* [包含或可連線至影像](#fragments-with-visual-assets).
* 已使用 [中間內容](#in-between-content-when-page-authoring-with-content-fragments) 在頁面上參考時。
* 這些區段與傳送機制（即頁面、頻道）無關。

### 具有視覺資產的片段 {#fragments-with-visual-assets}

為了讓作者更能掌控其內容，可以將影像新增至內容片段及/或與內容片段整合。

資產可以透過數個方式與內容片段一起使用；各有其優點：

* **插入資產** 放入片段（混合媒體片段）

   * 它們是片段的一部分(請參閱 [內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 定義資產位置。
   * 另請參閱 [將資產插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) 在片段編輯器中以取得詳細資訊。

  >[!NOTE]
  >
  >插入內容片段本身的視覺資產附加於前面的段落。 將片段新增到頁面時，在新增中間內容時，這些資產會相對於該段落移動。

* **相關聯的內容**

   * 連線到片段；但不是片段的固定部分(請參閱 [內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 具有一定的定位彈性。
   * 在頁面上使用片段時，可輕鬆使用（當作中間內容）。

  另請參閱 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 以取得詳細資訊。

* 頁面編輯器的「 **資產** 」瀏覽器可用的資產

   * 允許選擇資產的完整靈活性。
   * 具有一定的定位彈性。
   * 不提供為特定片段核准的概念。

  另請參閱 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) 以取得詳細資訊。

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分（直接或間接）組成：

* **片段元素**

   * 元素會與儲存內容的資料欄位建立關聯。
   * 您使用內容模型來建立內容片段。 模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是各種資料型別。

* **片段段落**

   * 文字區塊，通常是以個別實體分隔的多行。

   * 在富 [文本](/help/assets/content-fragments/content-fragments-variations.md#rich-text)[](/help/assets/content-fragments/content-fragments-variations.md#markdown) 和標籤下拉模式中，段落可以格式化為標題，在這種情況下，它和以下段落作為一個單位一起組成。

   * 在頁面製作期間啟用內容控制。

* **插入到片段中的資產（混合媒體片段）**

   * 插入到實際片段中並用作片段內部內容的資產（影像）。
   * 內嵌在片段的段落系統中。
   * 可以在下列情況下格式化： [在頁面上使用/參考片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * 只能使用片段編輯器在片段中新增、刪除或移動。 無法在頁面編輯器中執行這些動作。
   * 只能使用在片段中新增、刪除或移動片段 [片段編輯器中的RTF格式](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * 只能新增到多行文字元素（任何片段型別）。
   * 附於前文（段落）。

     >[!CAUTION]
     >
     >切換為純文字格式，可以（無意中）從片段中移除資產。

     >[!NOTE]
     >
     >在頁面上使用片段時，資產也可以新增為其他（中間）內容；使用 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 或資產（從「資產」瀏覽器）。

* **相關聯的內容**

   * 這是片段外部的內容，但與編輯相關。 通常是影像、影片或其他片段。
   * 將集合中的個別資產新增至頁面時，即可在頁面編輯器中與片段搭配使用。 這表示它們是選用專案，視特定通道的需求而定。
   * 資產為 [透過集合關聯到片段](/help/assets/content-fragments/content-fragments-assoc-content.md)；關聯的集合可讓作者決定在編寫頁面時要使用的資產。

      * 收藏集可以作為預設內容與片段相關聯，也可以由作者在片段製作期間相關聯。
      * [資產(DAM)集合](/help/assets/manage-collections.md) 是片段關聯內容的基礎。
   * 或者，您也可以將片段本身新增至集合，以輔助追蹤。

* **片段中繼資料**

   * 使用 [資產中繼資料結構](/help/assets/metadata-schemas.md).
   * 標籤可在以下情況下建立：

      * 建立和編寫片段
      * 或更新版本：

         * 透過檢視/編輯片段 **屬性** 從主控台
         * 透過編輯 **中繼資料** 在片段編輯器中時

  >[!CAUTION]
  >
  >中繼資料處理設定檔不適用於內容片段。

* **主版**

   * 片段的一部分

      * 每個內容片段都有一個Master例項。
      * 無法刪除主版。

   * 主版可在下的片段編輯器中存取 **[變數](/help/assets/content-fragments/content-fragments-variations.md)**.
   * 主版本身不是變數，而是所有變數的基礎。

* **變數**

   * 特定編輯目的的片段文字轉譯；可能與頻道相關，但並非強制，也可用於臨時本機修改。
   * 建立為的復本 **主版**，但隨後可視需要進行編輯。 變數本身之間存在內容重疊。
   * 可以在片段製作期間定義。
   * 儲存在片段中，有助於避免內容副本的散佈。
   * 變數可以是 [已同步](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) 如果主要內容已更新，則使用Master。
   * 可以是 [摘要](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) 以快速將文字截斷成預先定義的長度。
   * 可在下取得 [變數](/help/assets/content-fragments/content-fragments-variations.md) 標籤進行標籤。

### 使用內容片段編寫頁面時的中間內容 {#in-between-content-when-page-authoring-with-content-fragments}

中間內容：

* 可用於處理內容片段時的頁面編輯器。
* [在片段流程中新增的其他內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) 在頁面上使用或參照之後。
* 可用於以下專案： [使用內容片段時的頁面編輯器](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* 中間內容可以新增到任何片段中，其中只有一個元素可見。
* 關聯內容以及適當瀏覽器的資產和/或元件皆可使用。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

### 片段必填 {#required-by-fragments}

若要建立內容片段，您需要：

* **內容模型**

   * 為 [使用設定瀏覽器啟用](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * 為 [使用工具建立](/help/assets/content-fragments/content-fragments-models.md).
   * 必填 [建立片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容模型定義需要一個標題和一個資料元素；其他內容都是選用的。
   * 模型可定義預設內容（如果適用）。
   * 作者在製作片段內容時無法變更已定義的結構。
   * 建立相依內容片段後對模型所做的變更可能會影響這些內容片段。

若要使用您的內容片段進行頁面製作，您還需要：

* **內容片段元件**

   * 有助於以HTML格式或JSON格式（或兩者）傳送片段。
   * 必填 [在頁面上參考片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * 負責片段的佈局和傳送；即管道。
   * 片段需要一或多個專用元件來定義版面並傳遞部分或全部元素/變數和相關內容。
   * 在製作中將片段拖曳到頁面上會自動建立所需元件的關聯。

## 使用範例 {#example-usage}

片段及其元素和變數可用於為多個管道建立一致的內容。 在設計片段時，請考慮使用的內容及其使用位置。

### WKND範例 {#wknd-sample}

此 [WKND網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 提供範例來協助您瞭解AEMas a Cloud Service。

WKND專案包括：

* 內容片段模型可在以下位置取用：
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 內容片段 (和其他內容) 可在以下位置取用：
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
