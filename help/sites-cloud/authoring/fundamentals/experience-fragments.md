---
title: 體驗片段
description: 使用Adobe Experience Manager as a Cloud Service體驗片段，讓您的體驗可重複使用且更靈活。
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 3%

---

# 體驗片段 {#experience-fragments}

在Adobe Experience Manager as a Cloud Service中，體驗片段：

* 是一或多個元件的群組
* 包含內容和版面
* 可在頁面中參照
* 可包含任何元件

體驗片段：

* 是體驗（頁面）的一部分。
* 可以跨多個頁面使用。
* 以範本為基礎（僅可編輯）以定義結構和元件。
* 此範本用於建立 *根頁面* 體驗片段的URL。
* 由段落系統中一或多個元件組成，具有版面。
* 可以包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合以形成完整頁面（體驗）。
* 您可以根據根頁面建立一或多個變數。
* 這些變化可能會共用內容和/或元件。
* 可以劃分為可在片段的多個變體中使用的建置區塊。

您可以使用體驗片段：

* 如果作者想要重複使用頁面的部分（體驗的片段）。
如果沒有體驗片段，作者需要複製並貼上該片段。 建立及維護這些複製/貼上體驗非常耗時，而且容易發生使用者錯誤。
體驗片段不需要複製/貼上。
* 支援Headless CMS使用案例。
作者只想將AEM用於製作，而不是用於提供給客戶。 協力廠商系統/接觸點會取用該體驗，然後傳送給使用者。

>[!NOTE]
>
>**[內容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md)** 和 **體驗片段** 是AEM中的不同功能：
>* **內容片段** 是可編輯內容，具備定義與結構，但無其他視覺化設計及/或版面配置。 它們可用於存取結構化資料，包括文字、數字和日期等。
>* **體驗片段** 是完全佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。
>
>如需詳細資訊，請參閱 [瞭解AEM中的內容片段和體驗片段](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

>[!NOTE]
>
>體驗片段的寫入許可權需要在群組中註冊使用者帳戶：
>
>* `experience-fragments-editors`
>
>如果您遇到任何問題，請聯絡您的系統管理員。

## 何時應使用體驗片段？ {#when-should-you-use-experience-fragments}

該使用「體驗片段」的情況：

* 每當您想要重複使用體驗時。
   * 與相同或類似內容重複使用的體驗。
* 當您使用AEM做為協力廠商的內容傳遞平台時。
   * 任何想要使用AEM作為內容傳遞平台的解決方案。
   * 將內容內嵌於第三方接觸點。
* 如果您有具有不同變數或轉譯的體驗。
   * 管道或內容特定變數。
   * 對群組有意義的體驗，例如跨頻道具有不同體驗的行銷活動。
* 當您使用全通路商務時。
   * 讓接觸點成為異動。

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾中設定允許的範本](#configure-allowed-templates-folder).

建立資料夾可讓您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

  >[!NOTE]
  >
  >您不需要將體驗片段的結構與網站的頁面結構對齊。

* [在檔案夾層級配置允許的範本](#configure-allowed-templates-folder)

  >[!NOTE]
  >
  >您可以使用 [範本編輯器](/help/sites-cloud/authoring/features/templates.md) 以建立您自己的範本。

WKND專案會根據以下規則建構一些體驗片段 `Contributors`. 使用的結構也說明了如何使用其他功能，例如「多網站管理」（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-cloud/authoring/assets/xf-folders.png)

## 為您的體驗片段建立和設定資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

若要為體驗片段建立及設定資料夾，建議您：

1. [建立資料夾](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [為該資料夾設定允許的體驗片段範本](#configure-allowed-templates-folder).

>[!NOTE]
>
>您也可以設定 [執行個體允許的範本](#configure-allowed-templates-instance)，但此方法為 **非** 建議使用，因為升級時可覆寫這些值。

### 設定資料夾的允許範本 {#configure-allowed-templates-folder}

>[!NOTE]
>
>建議使用此方式指定 **允許的範本**，因為值在升級時不會被覆寫。

1. 導覽至所需的 **體驗片段** 資料夾。

1. 選取資料夾，然後 **屬性**.

1. 指定規則運算式，以擷取 **允許的範本** 欄位。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性 — 允許的範本](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >另請參閱 [體驗片段的範本](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 以取得更多詳細資料。

1. 選取 **儲存並關閉**.

### 為您的執行個體設定允許的範本 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>不建議變更 **允許的範本** 此方法可在升級時覆寫指定的範本。
>
>使用此對話方塊僅供參考。

1. 導覽至所需的 **體驗片段** 主控台。

1. 選取 **設定選項**：

   ![設定按鈕](/help/sites-cloud/authoring/assets/xf-18.png)

1. 在中指定所需的範本 **設定體驗片段** 對話方塊：

   ![設定體驗片段](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >另請參閱 [體驗片段的範本](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 以取得更多詳細資料。

1. 選取「**儲存**」。

## 建立體驗片段 {#creating-an-experience-fragment}

若要建立體驗片段：

1. 選取 **體驗片段** 從「全域導覽」。

   ![導覽面板中的體驗片段](/help/sites-cloud/authoring/assets/xf-01.png)

1. 導覽至所需的資料夾，然後選取「 」 **建立**：

   ![建立體驗片段的資料夾](/help/sites-cloud/authoring/assets/xf-02.png)

1. 選取 **體驗片段** 以開啟 **建立體驗片段** 精靈。

   依次選擇所需 **的範本**、下 **一步**:

   ![選取體驗片段範本](/help/sites-cloud/authoring/assets/xf-03.png)


1. 輸入 **體驗****片段的屬性**。

   A **標題** 為必填欄位。 如果 **名稱** 保留為空白，其衍生自 **標題**.

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >體驗片段範本中的標籤不會與此體驗片段根頁面上的標籤合併。
   >
   >它們是完全獨立的。

1. 按一下&#x200B;**建立**。

   此時會顯示訊息。 選取：

   * **完成** 以返回主控台
   * **開啟** 以開啟片段編輯器

## 編輯您的體驗片段 {#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
>
>另請參閱 [編輯頁面內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 以取得有關如何使用頁面編輯器的詳細資訊。

下列範例程式說明如何建立產品的Teaser：

1. 將必要的元件從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. 依元件而定：
   * 視需要新增任何內容和/或資產。
   * 視需要設定屬性。

1. 視需要新增更多元件。

例如：`http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![頁面上的體驗片段](/help/sites-cloud/authoring/assets/xf-05.png)

## 建立體驗片段變數 {#creating-an-experience-fragment-variation}

您可以根據自己的需求，建立體驗片段的變數：

1. 開啟您的片段用於 [編輯](#editing-your-experience-fragment).
1. 開啟 **變數** 標籤。

   ![建立體驗片段變數](/help/sites-cloud/authoring/assets/xf-06.png)

1. **建立** 可讓您建立：

   * **變異**
   * **變數為live-copy**.

1. 定義必要的屬性：

   * **範本**
   * **標題**
   * **名稱**  — 如果留空，其衍生自標題
   * **說明**
   * **變數標籤**

   例如：

   ![變數屬性](/help/sites-cloud/authoring/assets/xf-07.png)


1. 確認 **完成**，新的變數會顯示在面板中。

## 使用您的體驗片段 {#using-your-experience-fragment}

您現在可以在編寫頁面時使用您的體驗片段：

1. 開啟任何頁面進行編輯。

1. 在頁面段落系統中建立體驗片段元件的例項：

1. 將實際的體驗片段新增到元件例項；可以：

   * 從資產瀏覽器拖曳所需的片段，並放置到元件上。
   * 選取 **設定** 從元件工具列並指定要使用的片段，確認使用 **完成**.

   >[!NOTE]
   >
   >元件工具列中的「編輯」可作為在片段編輯器中開啟片段的捷徑。

例如：`http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![頁面編輯器中的體驗片段](/help/sites-cloud/authoring/assets/xf-08.png)

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段中回收的建置區塊：

### 建立建置區塊 {#creating-a-building-block}

若要建立建置區塊：

1. 在體驗片段編輯器中，選取您要重複使用的元件：

   ![選取建置區塊的元件](/help/sites-cloud/authoring/assets/xf-09.png)

1. 從元件工具列中，選取 **轉換為建置區塊**：

   ![建置區塊按鈕](/help/sites-cloud/authoring/assets/xf-10.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![為建置區塊命名](/help/sites-cloud/authoring/assets/xf-11.png)

1. 此 **建置區塊** 顯示在左側標籤(**本機**)，並可選取以執行進一步動作：

   ![邊欄中的建置區塊](/help/sites-cloud/authoring/assets/xf-12.png)

#### 管理建置區塊 {#managing-a-building-block}

您的建置區塊會顯示在 **建置區塊** 標籤。 對於每個區塊，都可使用下列動作：

* **移至主版**：在新索引標籤中開啟根頁面變數
* **重新命名**
* **刪除**

![管理建置區塊](/help/sites-cloud/authoring/assets/xf-13.png)

#### 使用建置區塊 {#using-a-building-block}

您可以將建置區塊拖曳至任何片段的段落系統，就像對任何元件一樣。

編輯體驗片段時，可用的建置區塊會顯示在左側標籤中。 您可以根據以下條件進行篩選：

* **本機**  — 目前體驗片段的建置區塊
* **全部**  — 所有片段的建置區塊

![選取建置區塊](/help/sites-cloud/authoring/assets/xf-14.png)

## 您的體驗片段上的個人化 {#personalization-experience-fragment}

您的體驗片段個人化可讓您作為行銷人員，為體驗片段定義一次目標對象，然後在任何頁面中重複使用片段。 此特性：

* 無需在每次使用片段時為每個對象指定所需的變數
* 維持各優惠方案的樣式

您可以建立體驗片段，並將多個元件分組在此單一片段中。 您也可以為每個特定的受眾區段建立片段的變數，然後在所需的管道中重複使用這些體驗片段。

個人化是透過定義 **個人化** 體驗片段或變數或包含片段的資料夾上的屬性；這表示繼承可以覆寫個人化屬性。

設定這些屬性也會啟用 **目標定位** 體驗片段編輯器中的模式

### 為您的體驗片段定義個人化 {#defining-personalization-experience-fragment}

個人化您的片段：

1. 導覽至中的所需位置 **體驗片段** 主控台。

1. 選取資料夾或您的片段，然後 **屬性** 工具列中的。

   >[!NOTE]
   >
   >資料夾上定義的個人化屬性會由子樹狀結構中的所有子資料夾以及該子樹狀結構中的體驗片段（和變數）繼承。 可透過中斷繼承來覆寫它們。

1. 開啟 **個人化** 標籤來定義和儲存您的設定。 例如，在資料夾上：

   ![體驗片段 — 個人化屬性](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >片段內嵌於Sites頁面中時，以及 **個人化** 設定，則在頁面轉譯時只會使用頁面的個人化版本。
   >
   >為了在頁面轉譯時對片段中的元件執行目標定位，以下條件必須符合：
   >
   >此 **ContextHub路徑** 已選取於 **個人化** 索引標籤必須是：
   >
   >* 與為呈現片段的頁面設定的路徑相同
   >
   >  或：
   >
   >* 包含為頁面設定的ContextHub中所定義之存放區子集的路徑
   >
   >此 **區段路徑** 已選取於 **個人化** 索引標籤必須是：
   >
   >* 與為呈現片段的頁面設定的路徑相同
   >
   >  或
   >
   >* 包含為頁面設定的區段子集的路徑

### 為您的體驗片段定義定位 {#defining-targeting-experience-fragment}

設定個人化屬性後，當開啟片段進行編輯時，可以使用目標模式。

![體驗片段編輯器 — 目標定位模式](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

此模式的運作方式與頁面編輯相同。 另請參閱 [頁面編輯器的鎖定目標模式](/help/sites-cloud/authoring/personalization/targeted-content.md) 以取得更多詳細資料。

## 您的體驗片段的詳細資料 {#details-of-your-experience-fragment}

您可以檢視片段的詳細資訊：

1. 導覽至體驗片段的位置（請勿進一步導覽至片段內的變數）。
詳細資訊會顯示在 **體驗片段** 主控台，使用 **清單檢視** 包含詳細資訊 [匯出至Target](/help/sites-cloud/integrating/integrating-adobe-target.md)：

   ![體驗片段詳細資料](/help/sites-cloud/authoring/assets/xf-15.png)

1. 當您開啟 **屬性** 體驗片段的：

   ![「屬性」按鈕](/help/sites-cloud/authoring/assets/xf-16.png)

   屬性位於各種標籤中：

   >[!CAUTION]
   >
   >這些標籤會在您開啟時顯示 **屬性** 體驗片段主控台中的。
   >
   >如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 。

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-17.png)

   * **基本**
      * **標題**  — 必要
      * **說明**
      * **標籤**
      * **變數總數**  — 僅供參考
      * **網路變數的數量**  — 僅供參考
      * **非網路變數的數量**  — 僅供參考
      * **使用此片段的頁數**  — 僅供參考
   * **Cloud Service**
      * **雲端設定**
      * **Cloud Service設定**
      * **facebook頁面ID**
      * **pinterest展示板**
   * **引用**
      * 引用清單
   * **個人化**
      * **ContextHub路徑**
      * **區段路徑**
      * **品牌**

## 純HTML轉譯 {#the-plain-html-rendition}

使用 `.plain.` 選取「 」後，您便可從瀏覽器存取純HTML轉譯。

>[!NOTE]
>
>雖然這可以直接從瀏覽器取得， [主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實施）僅使用URL直接存取體驗片段的內容](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## 發佈體驗片段 {#publishing-experience-fragments}

發佈您的體驗片段的方式基本上與相同 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （從體驗片段主控台或編輯器中存取）。

或者，您也可以 [發佈到預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md) （再次從體驗片段控制檯或編輯器中執行）。

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道均可使用此函式。

若要匯出至Adobe Target，也可以使用JSON。 請參閱：

* [整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [將體驗片段匯出到 Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
