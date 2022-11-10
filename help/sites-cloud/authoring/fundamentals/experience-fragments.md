---
title: 體驗片段
description: 使用Adobe Experience Manager as a Cloud Service體驗片段，讓您的體驗可重複使用且靈活。
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: ccf5cdf56867ca077d7ff71bfb2f1f4af1b32bd9
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 6%

---

# 體驗片段 {#experience-fragments}

在Adobe Experience Manager as a Cloud Service中，體驗片段：

* 是一或多個元件的群組
* 包含內容和版面
* 可在頁面內參照
* 可包含任何元件

體驗片段：

* 是體驗（頁面）的一部分。
* 可用於多個頁面。
* 以範本為基礎（僅可編輯），以定義結構和元件。
* 此範本用於建立 *根頁面* 體驗片段的。
* 由段落系統中的一個或多個元件（具有佈局）組成。
* 可包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合，以形成完整的頁面（體驗）。
* 可以根據根頁面建立一或多個變異。
* 這些變化可能會共用內容和/或元件。
* 可劃分為可跨片段的多個變數使用的建立區塊。

您可以使用體驗片段：

* 如果作者想要重複使用頁面的部分（體驗的片段）。
若沒有體驗片段，作者將需要複製並貼上該片段。 建立和維護這些複製/貼上體驗非常耗時，且容易發生使用者錯誤。
體驗片段不需要複製/貼上。
* 支援無頭式CMS使用案例。
作者只想使用AEM進行製作，而不想提供給客戶。 協力廠商系統/接觸點會使用該體驗，然後傳送給使用者。

>[!NOTE]
>
>體驗片段的寫入存取權要求使用者帳戶須在群組中註冊：
>
>* `experience-fragments-editors`
>
>如果您遇到任何問題，請與系統管理員聯繫。

## 何時該使用體驗片段？ {#when-should-you-use-experience-fragments}

該使用體驗片段的情況：

* 每當您想要重複使用體驗時。
   * 將透過相同或類似內容重複使用的體驗。
* 當您使用AEM作為協力廠商的內容傳遞平台時。
   * 任何想使用AEM作為內容傳遞平台的解決方案。
   * 將內容內嵌在協力廠商接觸點中。
* 如果您的體驗有不同的變體或轉譯。
   * 管道或內容特定變數。
   * 對群組有意義的體驗；例如，跨管道具有不同體驗的促銷活動。
* 使用全通路商務時。
   * 將接觸點設為交易式。

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上配置允許的模板](#configure-allowed-templates-folder).

建立資料夾可讓您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

   >[!NOTE]
   >
   >不需要將體驗片段的結構與網站的頁面結構對齊。

* [在資料夾層級分配允許的範本](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >您可以使用 [範本編輯器](/help/sites-cloud/authoring/features/templates.md) 來建立自己的範本。

WKND專案會根據 `Contributors`. 使用的結構也說明如何使用其他功能，例如多網站管理（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-cloud/authoring/assets/xf-folders.png)

## 建立和設定體驗片段的資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

若要建立和設定體驗片段的資料夾，建議您：

1. [建立資料夾](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [設定該資料夾允許的體驗片段範本](#configure-allowed-templates-folder).

>[!NOTE]
>
>您也可以設定 [允許的執行個體範本](#configure-allowed-templates-instance)，但此方法 **not** 建議使用，因為值可在升級時覆寫。

### 為資料夾配置允許的模板 {#configure-allowed-templates-folder}

>[!NOTE]
>
>這是指定 **允許的範本**，因為升級時不會覆寫值。

1. 導覽至所需 **體驗片段** 檔案夾。

1. 選取資料夾，然後 **屬性**.

1. 指定用於擷取 **允許的範本** 欄位。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性 — 允許的範本](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >請參閱 [體驗片段的範本](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 以取得詳細資訊。

1. 選擇 **儲存並關閉**.

### 為執行個體設定允許的範本 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>不建議變更 **允許的範本** 此方法可讓您在升級時覆寫指定的範本，
>
>請使用此對話框僅供參考。

1. 導覽至所需 **體驗片段** 控制台。

1. 選擇 **配置選項**:

   ![配置按鈕](/help/sites-cloud/authoring/assets/xf-18.png)

1. 在 **設定體驗片段** 對話框：

   ![設定體驗片段](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >請參閱 [體驗片段的範本](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 以取得詳細資訊。

1. 選取&#x200B;**儲存**。

## 建立體驗片段 {#creating-an-experience-fragment}

若要建立體驗片段：

1. 選擇 **體驗片段** 中。

   ![導覽面板中的體驗片段](/help/sites-cloud/authoring/assets/xf-01.png)

1. 導覽至所需資料夾，然後選取 **建立**:

   ![為體驗片段建立資料夾](/help/sites-cloud/authoring/assets/xf-02.png)

1. 選擇 **體驗片段** 開啟 **建立體驗片段** 嚮導。

   依次選擇所需 **的範本**、下 **一步**:

   ![選取體驗片段範本](/help/sites-cloud/authoring/assets/xf-03.png)


1. 輸入 **體驗****片段的屬性**。

   A **標題** 為必填。 若 **名稱** 保留為空白，則會從中衍生 **標題**.

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >來自體驗片段範本的標籤不會與此體驗片段根頁面上的標籤合併。
   >
   >這些是完全不同的。

1. 按一下&#x200B;**建立**。

   將顯示一條消息。 選取:

   * **完成** 返回控制台
   * **開啟** 開啟片段編輯器

## 編輯體驗片段 {#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
>
>請參閱 [編輯頁面內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 以取得如何使用頁面編輯器的詳細資訊。

以下范常式式說明如何為產品建立預告：

1. 從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. 視元件而定：
   * 視需要新增任何內容和/或資產。
   * 視需要設定屬性。

1. 視需要新增更多元件。

例如：`http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![頁面上的體驗片段](/help/sites-cloud/authoring/assets/xf-05.png)

## 建立體驗片段變異 {#creating-an-experience-fragment-variation}

您可以根據您的需求建立體驗片段的變體：

1. 開啟您的片段 [編輯](#editing-your-experience-fragment).
1. 開啟 **變異** 標籤。

   ![建立體驗片段變數](/help/sites-cloud/authoring/assets/xf-06.png)

1. **建立** 可讓您建立：

   * **變異**
   * **變數為 live-copy**.

1. 定義所需的屬性：

   * **範本**
   * **標題**
   * **名稱**  — 若保留為空白，則從標題衍生
   * **說明**
   * **變數標記**

   例如：

   ![變化屬性](/help/sites-cloud/authoring/assets/xf-07.png)


1. 確認為 **完成**，則新變數會顯示在面板中。

## 使用您的體驗片段 {#using-your-experience-fragment}

編寫頁面時，您現在可以使用體驗片段：

1. 開啟任何頁面進行編輯。

1. 在頁面段落系統內建立體驗片段元件的例項：

1. 將實際的體驗片段新增至元件例項；其中之一：

   * 從「資產瀏覽器」拖曳所需片段，放置到元件。
   * 選擇 **設定** 從元件工具列中，並指定要使用的片段，請使用確認 **完成**.

   >[!NOTE]
   >
   >在元件工具列中，編輯作為在片段編輯器中開啟片段的捷徑。

例如：`http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![頁面編輯器中的體驗片段](/help/sites-cloud/authoring/assets/xf-08.png)

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段內回收的建置區塊：

### 建立建置區塊 {#creating-a-building-block}

要建立新的構建塊：

1. 在體驗片段編輯器中，選取您要重新使用的元件：

   ![為構建塊選擇元件](/help/sites-cloud/authoring/assets/xf-09.png)

1. 從元件工具欄中，選擇 **轉換為建置區塊**:

   ![構建塊按鈕](/help/sites-cloud/authoring/assets/xf-10.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![名稱構建塊](/help/sites-cloud/authoring/assets/xf-11.png)

1. 建 **立區塊** (Building Block **)將顯示在左側標籤(** Local)中，並可以選取以執行進一步動作：

   ![邊欄中的建置區塊](/help/sites-cloud/authoring/assets/xf-12.png)

#### 管理建置區塊 {#managing-a-building-block}

您的建置區塊會顯示在 **建置區塊** 標籤。 對於每個區塊，可使用下列動作：

* **轉到主版**:在新索引標籤中開啟根頁面變異
* **重新命名**
* **刪除**

![管理構建塊](/help/sites-cloud/authoring/assets/xf-13.png)

#### 使用建置區塊 {#using-a-building-block}

您可以將建置區塊拖曳至任何片段的段落系統，如同任何元件。

編輯體驗片段時，可用的建置區塊會顯示在左側標籤中。 您可以根據下列項目進行篩選：

* **本地**  — 目前體驗片段的建置區塊
* **全部**  — 從所有片段建立區塊

![選擇構建塊](/help/sites-cloud/authoring/assets/xf-14.png)

## 體驗片段上的個人化 {#personalization-experience-fragment}

體驗片段上的個人化可讓您身為行銷人員，只定義體驗片段的目標對象一次，然後在任何頁面中重複使用片段。 此特性：

* 無需在每次使用片段時為每個對象指定所需的變數
* 維護選件的樣式

您可以建立體驗片段，其中多個元件分組在此單一片段內。 您也可以為每個特定對象區段建立片段的變體，然後在所需管道重複使用這些體驗片段。

個人化是透過定義 **個人化** 體驗片段或變異，或包含片段的資料夾上的屬性；這表示繼承可以覆寫個人化屬性。

設定這些屬性也可啟用 **定位** 模式。

### 定義體驗片段的個人化 {#defining-personalization-experience-fragment}

若要個人化您的片段：

1. 導覽至 **體驗片段** 控制台。

1. 選取資料夾或您的片段，然後 **屬性** 的上界。

   >[!NOTE]
   >
   >在資料夾上定義的個人化屬性將由所有子資料夾沿子樹繼承，並透過該子樹中的體驗片段（和變數）。 您可以中斷繼承來覆寫繼承。

1. 開啟 **個人化** 標籤來定義和儲存設定。 例如，在資料夾上：

   ![體驗片段 — 個人化屬性](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >片段內嵌於網站頁面時， **個人化** ，則頁面呈現時只會使用頁面的個人化版本。
   >
   >為了讓片段中的元件上執行的定位在頁面呈現時運作，必須符合下列條件：
   >
   >此 **ContextHub路徑** 在 **個人化** 標籤必須是：
   >
   >* 與為要呈現片段的頁面所設定的路徑相同
      >或:
   >* 包含為頁面設定的ContextHub中所定義儲存區子集的路徑

   >
   > 
此 **區段路徑** 在 **個人化** 標籤必須是：
   * 與為要呈現片段的頁面所設定的路徑相同，或
   * 包含為頁面配置的段子集的路徑


### 定義體驗片段的鎖定目標 {#defining-targeting-experience-fragment}

設定個人化屬性後，開啟片段進行編輯時，將可使用鎖定目標模式。

![體驗片段編輯器 — 鎖定目標模式](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

此模式的運作方式與頁面編輯相同。 請參閱 [頁面編輯器的定位模式](/help/sites-cloud/authoring/personalization/targeted-content.md) 以取得更多詳細資訊。

## 體驗片段的詳細資訊 {#details-of-your-experience-fragment}

您可以看到片段的詳細資訊：

1. 導覽至體驗片段的位置（請勿進一步導覽至片段內的變體）。
詳細資料會顯示在 **體驗片段** 主控台，搭配 **清單檢視** 包括 [匯出至Target](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![體驗片段詳細資料](/help/sites-cloud/authoring/assets/xf-15.png)

1. 當您開啟 **屬性** 體驗片段的：

   ![「屬性」按鈕](/help/sites-cloud/authoring/assets/xf-16.png)

   屬性可在各種標籤中使用：

   >[!CAUTION]
   這些標籤會在您開啟 **屬性** 從體驗片段主控台。
   如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 。

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-17.png)

   * **基本**
      * **標題** 必填
      * **說明**
      * **標記**
      * **變體總數**  — 僅資訊
      * **Web變體數**  — 僅資訊
      * **非Web變體的數量**  — 僅資訊
      * **使用此片段的頁數**  — 僅資訊
   * **雲端服務**
      * **雲端設定**
      * **雲端服務設定**
      * **Facebook 頁面 ID**
      * **Pinterest Board**
   * **引用**
      * 參考清單
   * **個人化**
      * **ContextHub 路徑**
      * **區段路徑**
      * **品牌**

## 純HTML轉譯 {#the-plain-html-rendition}

使用 `.plain.` 選取器，您可以從瀏覽器存取純HTML轉譯。

>[!NOTE]
雖然這可直接從瀏覽器取得， [主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## 發佈體驗片段 {#publishing-experience-fragments}

發佈您的體驗片段基本上等同於 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （透過體驗片段主控台或編輯器）。

或者，您也可以 [發佈至預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md) （從體驗片段主控台或編輯器再次執行）。

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道皆可使用。

若要匯出至Adobe Target，也可以使用JSON。 請參閱：

* [整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [將體驗片段匯出至Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
