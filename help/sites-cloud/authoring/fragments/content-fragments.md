---
title: 內容片段
description: Adobe Experience Manager as a Cloud Service內容片段允許您設計、建立、組織和使用獨立於頁面的內容
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 2%

---

# 內容片段 {#content-fragments}

Adobe Experience Manager (AEM)as a Cloud Service中的內容片段包括 [已建立並管理為不受頁面影響的資產](/help/sites-cloud/administering/content-fragments/overview.md).

它們可讓您建立頻道中性內容，以及各種（頻道特定的）變化。 接著，您就可以在編寫內容頁面時，使用這些片段及其變數。

結構化內容片段與更新的JSON匯出工具搭配使用，也可用來透過Content Services將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>內容片段為 **網站** 功能，但儲存為 **資產**.
>
>他們現在主要透過 **[內容片段](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** 主控台，但仍可從 **[資產](/help/assets/content-fragments/content-fragments-managing.md)** 主控台。
>
>編寫內容片段有兩個編輯器：
>
>* 的新編輯器 [內容片段 — 製作](/help/sites-cloud/administering/content-fragments/authoring.md)，主要從存取 **內容片段** 主控台。
>* 此 [原始編輯器](/help/assets/content-fragments/content-fragments-variations.md) 主要從「 」存取 **資產** 主控台。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-cloud/authoring/fragments/content-fragments.md)** 是AEM中的不同功能：
>* **內容片段** 是可編輯內容，具備定義與結構，但無其他視覺化設計及/或版面配置。 它們可用於存取結構化資料，包括文字、數字和日期等。
>* **體驗片段** 是完全佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。
>
>如需詳細資訊，請參閱 [瞭解AEM中的內容片段和體驗片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

>[!CAUTION]
>
>此頁面必須結合閱讀 [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md) （及相關頁面），其中介紹基本術語和概念，以及建立和管理片段。

內容片段會啟用：

* **行銷和行銷活動策略**
   * 透過集中管理的內容片段稽核內容。
* **Creative Pro**
   * 透過與內容片段相關聯的集合追蹤創意資產。
* **複製寫入者**
   * 在AEM內容片段編輯器中寫入。
   * 可以建立內容變數。
   * 可以關聯相關內容與內容片段。
   * 可以使用版本設定/工作流程。
   * 可共用內容片段。
   * 可集中管理翻譯。
* **製作者和歷程管理員**
   * 從預先定義的片段和AEM中編寫的變數中選取。
   * 當復本作者和創意人員以集中管理的片段和資產進行更新時，可依賴片段和相關內容始終保持最新。
   * 可以依賴因關聯性而管理的相關媒體內容。
   * 可以立即建立隨選內容變數，同時仍然確保這些變數在片段中受到集中管理。

## 新增內容片段至您的頁面 {#adding-a-content-fragment-to-your-page}

1. 開啟您的頁面以進行編輯。
2. 新增 **內容片段** 元件；從 **元件** 瀏覽器或 **插入新元件**.
3. 您可以執行下列兩個動作中的一個:
   * 開啟 **資產** 瀏覽器和篩選器 **內容片段** （預設值為「影像」）。 然後將所需的片段拖曳到元件例項上。
   * 選取內容片段元件，然後 **設定** 工具列中的。 在對話方塊中，您可以開啟選取對話方塊以瀏覽並選取所需的專案 **內容片段**.

   >[!NOTE]
   >
   >另一種方法是將特定的內容片段直接拖曳到頁面上。 這會自動建立關聯的元件（內容片段）。

4. 最初，內容來自 **主要** 元素和 **主版** （變數）會顯示。 您可以 [選取其他元素和/或變數](#selecting-the-element-or-variation) 視需要。

   ![資產瀏覽器中的內容片段](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >如需進一步編輯功能的詳細資訊，另請參閱：
   >
   >* [回應式版面](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [編輯頁面內容](/help/sites-cloud/authoring/page-editor/edit-content.md)

### 選取元素或變數 {#selecting-the-element-or-variation}

開啟片段的 **設定** 對話方塊，以設定片段用於目前頁面。 此對話方塊取決於所使用的元件。

>[!NOTE]
>
>另請參閱 [核心元件內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

在適當的組態對話方塊中，您可以選取可用的引數，包括：

* **內容片段**
   * 指定要使用的片段。
* **顯示模式**：
   * **單一文字元素**
   * **多個元素**
* **元素**
   * 可用的選取範圍取決於所使用的模型。

  >[!NOTE]
  >
  >可用的元素取決於所使用的模型。

* **變異**
   * 預設 **主版** 隨時可用。
   * 如果變數是為片段而建立，則可供選取。

* **ID**

   * **HTMLID** 要套用至元件的屬性。

### 快速連線到片段編輯器 {#quick-connection-to-fragment-editor}

您可以使用開啟片段來源以進行編輯（資產） **編輯** 圖示來切換元件。 這可讓您 [編輯和管理內容片段](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>一如既往，編輯片段來源將會影響參照該內容片段的所有頁面。

### 新增中間內容 {#adding-in-between-content}

將特定內容片段新增到頁面時， **將元件拖曳到這裡** 片段中每個HTML段落（和上/下）之間的預留位置。

這可讓您新增額外內容 [中間（即中間內容）](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) 片段內容（在任何可用點），不必變更根片段。

針對中間內容，您可以：

* 從新增元件 [元件瀏覽器。](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
* 從新增資產 [資產瀏覽器。](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)
* 使用 [關聯內容](#using-associated-content) 作為中間內容的來源。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

![插入元件](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>您也可以 [將視覺資產（影像）插入片段本身](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>插入片段本身的視覺資產會附加至片段中前面的段落。 這表示您無法在視覺資產與前一段落之間放置中間內容。 如果您需要這種連線等級，可以將影像新增到片段(以 [混合媒體片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets))。

>[!CAUTION]
>
>將中間內容新增至頁面上的內容片段後，變更基礎內容片段的結構（即在內容片段編輯器中）可能會導致錯誤/未預期的結果。
>
>發生此情況時，中間內容會維持不變：
>
>* 中間元件在片段流程中的元件順序內有絕對位置。 此位置不會變更，即使片段中段落的內容變更亦然。
>
>  這可能使其看起來像是相對位置已變更，因為中間段落與它們旁邊的（片段）段落沒有上下文關係。
>* 除非兩個段落結構衝突；在這種情況下，不會顯示中間內容（儘管它仍然存在於內部）。

### 使用關聯內容 {#using-associated-content}

如果您有 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 使用 [內容片段](/help/assets/content-fragments/content-fragments.md) 這些資產可從側面板使用（在您將片段放在內容頁面後）。 關聯內容實際上是的特殊內容來源 [中間內容](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>有多種方法可新增 [視覺資產（例如影像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 至片段和/或頁面。

>[!NOTE]
>
>如果您在一個頁面上有多個內容片段，請 **關聯內容** 索引標籤會顯示適用於所有片段的資產。

將具有關聯內容的片段新增到頁面後，就會顯示新索引標籤(**關聯內容**)即會在側面板中開啟。

從這裡，您可以將資產拖曳至所需位置（可拖曳至現有元件，或拖曳至建立適當元件的所需位置）：

![插入影像](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### 插入到片段中的資產 {#assets-inserted-into-the-fragment}

如果資產（例如影像）已插入片段本身(如 [混合媒體片段](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets))，則頁面編輯器中用於編輯這些資產的選項會受到限制。

例如，您可以對影像執行

* 裁切、旋轉或翻轉影像。
* 新增標題或替代文字。
* 指定大小。
* 您也可以配置配置。

您必須在片段編輯器中執行其他變更，例如移動、複製、刪除。

### 發佈 {#publishing}

片段必須發佈，才能用於您已發佈的網頁：

* 片段可以在以下時間後發佈： [在內容片段控制檯中建立片段](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* 如果 *未發佈的片段* 用於正在發佈的頁面，目前也可以發佈片段。

## 匯出內容片段 {#exporting-content-fragments}

若要匯出至Adobe Target，可使用JSON來傳送片段。 請參閱：

* [整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [將內容片段匯出到 Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
