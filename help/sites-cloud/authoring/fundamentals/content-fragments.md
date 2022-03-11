---
title: 內容片段
description: Adobe Experience Manager as a Cloud Service內容片段允許您設計、建立、建立和使用與頁面無關的內容
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 5%

---

# 內容片段 {#content-fragments}

Adobe Experience Manager(AEM)as a Cloud Service中的內容片段 [建立並管理為獨立於頁面的資產](/help/assets/content-fragments/content-fragments.md)。

它們允許您建立通道中性內容以及（可能特定於通道）變體。 然後，在創作內容頁面時，可以使用這些片段及其變體。

與更新的JSON導出器一起，結構化內容片段還可用於通過Content Services將AEM內容傳送到頁面以外的AEM渠道。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** 是內部的不同功AEM能：
>
>* **內容片段** 是編輯內容，主要是文本和相關影像。 它們是純內容，沒有設計和佈局。
>* **體驗片段** 內容以及網頁的片段。
>
>體驗片段可以包含內容片段的形式，但不能以相反的方式。

>[!CAUTION]
>
>此頁必須與 [使用內容片段](/help/assets/content-fragments/content-fragments.md) （及相關頁面），並介紹基本術語和概念，以及建立和管理片段。

內容片段啟用：

* **營銷和營銷策略**
   * 通過集中管理的內容片段審閱內容。
* **創意專業**
   * 通過與內容片段關聯的集合跟蹤創意資產。
* **複製編寫器**
   * 在內容片AEM段編輯器中寫入。
   * 可以建立內容變體。
   * 可以將相關內容與內容片段相關聯。
   * 可以使用版本控制/工作流。
   * 可以共用內容片段。
   * 可以集中管理翻譯。
* **製片人和旅程經理**
   * 從中的預定義片段和創作變體中選AEM擇。
   * 可以依賴片段和相關內容始終是最新的，因為拷貝編寫者和創意人員在集中管理的片段和資產中進行更新。
   * 可以依靠正在建立的關聯媒體內容進行關聯。
   * 可以即時建立臨時內容變體，同時仍確保這些變體在片段中保持集中管理。

## 將內容片段添加到頁面 {#adding-a-content-fragment-to-your-page}

1. 開啟頁面進行編輯。
2. 添加 **內容片段** 元件；從 **元件** 瀏覽器或 **插入新元件**。
3. 您可以:
   * 開啟 **資產** 瀏覽器和過濾器 **內容片段** （預設為Images）。 然後將所需片段拖到元件實例上。
   * 選擇內容片段元件，然後 **配置** 的子菜單。 在對話框中，可以開啟選擇對話框以瀏覽並選擇所需的 **內容片段**。

   >[!NOTE]
   >
   >另一種方法是將特定內容片段直接拖到頁面上。 這將自動建立關聯的元件（內容片段）。

4. 最初， **主** 元素和 **母版** （變體）。 你可以 [選擇其他元素和/或變體](#selecting-the-element-or-variation) 按需要。

   ![資產瀏覽器中的內容片段](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >有關進一步編輯功能的詳細資訊，另請參閱：
   >
   >* [回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [編輯頁面內容](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### 選擇元素或變體 {#selecting-the-element-or-variation}

開啟碎片 **配置** 對話框，以配置要在當前頁上使用的片段。 該對話框可以取決於使用的元件。

>[!NOTE]
>
>另請參閱 [核心元件，內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

在相應的配置對話框中，可以選擇可用參數，包括：

* **內容片段**
   * 指定要使用的片段。
* **顯示模式**:
   * **單文字元素**
   * **多文字元素**
* **元素**
   * 根據所使用的模型，將提供選取內容。

   >[!NOTE]
   >
   >可用元素取決於所使用的模型。

* **變異**
   * 預設主 **版** (Master)將始終可用。
   * 如果為片段建立了變體，則選擇將可用。

* **ID**

   * **要套用至元件的 HTML ID 屬性。**

### 快速連接到片段編輯器 {#quick-connection-to-fragment-editor}

可以使用 **編輯** 表徵圖。 這將允許您 [編輯和管理內容片段](/help/assets/content-fragments/content-fragments.md)。

>[!CAUTION]
>
>一如既往，編輯片段源將影響引用該內容片段的所有頁面。

### 在內容之間添加 {#adding-in-between-content}

將特定內容片段添加到頁面時， **將元件拖動到此處** 片段的每個HTML段落（以及頂部/底部）之間的佔位符。

這允許您添加額外內容 [內部（即內容之間）](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) 片段內容（在任何可用點處），無需更改根片段。

對於中間內容，您可以：

* 從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
* 從 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。
* 使用 [關聯內容](#using-associated-content) 作為中間內容的源。

>[!CAUTION]
>
>中間內容是頁面內容。 它未儲存在內容片段中。

![插入元件](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>您也可以 [將視覺資產（影像）插入片段本身](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
>
>插入片段本身的視覺資產附在片段的前段。 這意味著您不能在可視資產和前段之間放置內容。 如果需要此級別的連接，可以將影像添加到片段(作為 [混合媒體片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets))。

>[!CAUTION]
>
>在您將內容添加到頁面上的內容片段中後，更改基礎內容片段的結構（即在內容片段編輯器中）可能會導致錯誤/意外結果。
>
>當發生這種情況時，中間內容將保持原樣：
>
>* 在片段流中的元件序列內具有絕對位置。 即使片段中段落的內容發生更改，此位置也不會改變。
>
>  這可以使其看起來好像相對位置已更改，因為段落之間與它們位於旁邊的（片段）段落沒有上下文關係。
>* 除非兩款構成衝突；在這種情況下，不顯示中間內容（儘管它仍在內部存在）。


### 使用關聯內容 {#using-associated-content}

如果您有 [與內容片段](/help/assets/content-fragments/content-fragments-assoc-content.md)[相關的內容](/help/assets/content-fragments/content-fragments.md) ，這些資產將可從側面板使用 (在您將片段放在內容頁面後)。關聯內容實際上是用於 [內容](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)。

>[!NOTE]
>
>有多種方法可添加 [視覺資產（例如影像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 到片段和/或頁面。

>[!NOTE]
>
>如果在一個頁面上有多個內容片段， **關聯內容** 頁籤將顯示適合所有片段的資產。

在將包含關聯內容的片段添加到頁面後，您就會添加一個新頁籤(**關聯內容**)。

在此處，您可以將資產拖動到所需位置（可將資產拖至現有元件或將建立相應元件的所需位置）:

![插入影像](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### 插入片段中的資產 {#assets-inserted-into-the-fragment}

如果資產（如影像）已插入片段本身(如 [混合介質片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets))，則頁面編輯器中編輯這些資產的選項受到限制。

例如，對於影像，

* 裁剪、旋轉或翻轉影像。
* 添加標題或替代文本。
* 指定大小。
* 您還可以配置佈局。

必須在片段編輯器中進行其他更改，如移動、複製和刪除。

### 發佈 {#publishing}

片段需要發佈，以便可在已發佈的網頁上使用：

* 可在 [在Assets控制台中建立片段](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment)。
* 如果 *未發佈的片段* 在正在發佈的頁面上使用，此時也可以發佈該片段。
