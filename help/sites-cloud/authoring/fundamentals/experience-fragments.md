---
title: 體驗片段
description: 使用Adobe Experience Manager as a Cloud Service體驗片段使您的體驗可重複使用且靈活。
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: 9c3153efe4aacd1666663cd5eb718f75329202af
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 6%

---

# 體驗片段 {#experience-fragments}

在Adobe Experience Manager as a Cloud Service，一段經驗片段：

* 是一個或多個元件的組
* 包括內容和佈局
* 可在頁面中引用
* 可以包含任何元件

體驗片段：

* 是體驗（頁）的一部分。
* 可跨多頁使用。
* 基於模板（僅可編輯）來定義結構和元件。
* 此模板用於建立 *根頁* 體驗片段。
* 由段落系統中具有佈局的一個或多個元件組成。
* 可以包含其他體驗片段。
* 可以與其他元件（包括其他體驗片段）組合以形成完整的頁面（體驗）。
* 可基於根頁建立一個或多個變體。
* 這些變體可以共用內容和/或元件。
* 可以分解為可跨片段的多個變體使用的構造塊。

可以使用體驗片段：

* 如果作者希望重新使用頁面的部分（體驗的一部分）。
如果沒有「經驗片段」，作者需要複製並貼上該片段。 建立和維護這些複製/貼上體驗非常耗時且容易出現用戶錯誤。
體驗片段消除了複製/貼上的需要。
* 支援無頭CMS使用案例。
作者只想AEM用於創作，而不想交付給客戶。 第三方系統/觸點將消耗該體驗，然後交付給最終用戶。

>[!NOTE]
>
>**[內容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md)** 和 **體驗片段** 是內部的不同功AEM能：
>* **內容片段** 是編輯內容，具有定義和結構，但沒有附加的視覺設計和/或佈局。 它們可用於訪問結構化資料，包括文本、數字和日期等。
>* **體驗片段** 內容全面，網頁的片段。
>
>體驗片段可以包含內容片段的形式，但不能以相反的方式。
>
>有關詳細資訊，另請參見 [理解中的內容片段和體驗片段AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments)。

>[!NOTE]
>
>對體驗片段的寫入訪問要求在組中註冊用戶帳戶：
>
>* `experience-fragments-editors`
>
>如果遇到任何問題，請與系統管理員聯繫。

## 您何時應使用體驗片段？ {#when-should-you-use-experience-fragments}

應使用經驗片段：

* 無論何時您想要重用體驗。
   * 將使用相同或相似內容重用的體驗。
* 當您用作AEM第三方的內容交付平台時。
   * 任何希望用作內AEM容交付平台的解決方案。
   * 將內容嵌入第三方觸點。
* 如果您有「體驗」，但有不同的變體或格式副本。
   * 渠道或上下文特定變體。
   * 有意義的集體經驗；例如，在不同渠道開展不同經驗的活動。
* 使用Omnichannel Commerce時。
   * 使觸地點成為事務。

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上配置允許的模板](#configure-allowed-templates-folder)。

建立資料夾允許您：

* 為「體驗片段」建立有意義的結構；例如，根據分類

   >[!NOTE]
   >
   >無需將「體驗片段」的結構與站點的頁面結構對齊。

* [在資料夾級別分配允許的模板](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >您可以使用 [模板編輯器](/help/sites-cloud/authoring/features/templates.md) 建立自己的模板。

WKND工程根據經驗分段 `Contributors`。 使用的結構還說明了如何使用其他功能，如多站點管理（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-cloud/authoring/assets/xf-folders.png)

## 為您的體驗片段建立和配置資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

要為「體驗片段」建立和配置資料夾，建議：

1. [建立資料夾](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder)。

1. [配置該資料夾允許的體驗片段模板](#configure-allowed-templates-folder)。

>[!NOTE]
>
>還可以配置 [實例允許的模板](#configure-allowed-templates-instance)，但這種方法 **不** 建議，因為這些值可以在升級時被覆蓋。

### 配置資料夾的允許模板 {#configure-allowed-templates-folder}

>[!NOTE]
>
>這是用於指定 **允許的模板**，因為升級時不會覆蓋這些值。

1. 導航到所需 **體驗片段** 的子菜單。

1. 選擇資料夾，然後 **屬性**。

1. 指定用於檢索中所需模板的規則運算式 **允許的模板** 的子菜單。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性 — 允許的模板](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >請參閱 [體驗片段模板](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 的上界。

1. 選擇 **保存並關閉**。

### 配置實例的允許模板 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>不建議更改 **允許的模板** 通過此方法，因為在升級時可以覆蓋指定的模板。
>
>請使用此對話框僅供參考。

1. 導航到所需 **體驗片段** 控制台。

1. 選擇 **配置選項**:

   ![「配置」按鈕](/help/sites-cloud/authoring/assets/xf-18.png)

1. 在 **配置體驗片段** 對話框：

   ![設定體驗片段](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >請參閱 [體驗片段模板](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) 的上界。

1. 選取&#x200B;**儲存**。

## 建立體驗片段 {#creating-an-experience-fragment}

建立體驗片段：

1. 選擇 **體驗片段** 的子菜單。

   ![導航面板中的體驗片段](/help/sites-cloud/authoring/assets/xf-01.png)

1. 導航到所需資料夾並選擇 **建立**:

   ![為體驗片段建立資料夾](/help/sites-cloud/authoring/assets/xf-02.png)

1. 選擇 **體驗片段** 開啟 **建立體驗片段** 的子菜單。

   依次選擇所需 **的範本**、下 **一步**:

   ![選擇體驗片段模板](/help/sites-cloud/authoring/assets/xf-03.png)


1. 輸入 **體驗****片段的屬性**。

   A **標題** 的子菜單。 如果 **名稱** 留空，它將從 **標題**。

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >「體驗片段」模板中的標籤將不會與此「體驗片段」根頁上的標籤合併。
   >
   >這些是完全分開的。

1. 按一下&#x200B;**建立**。

   將顯示一條消息。 選取:

   * **完成** 返回到控制台
   * **開啟** 開啟片段編輯器

## 編輯您的體驗片段 {#editing-your-experience-fragment}

「體驗片段編輯器」提供與普通頁面編輯器類似的功能。

>[!NOTE]
>
>請參閱 [編輯頁面內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 的子菜單。

以下示例過程說明了如何為產品建立預告：

1. 從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。

1. 取決於元件：
   * 根據需要添加任何內容和/或資產。
   * 根據需要配置屬性。

1. 根據需要添加更多元件。

例如：`http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![第頁上的體驗片段](/help/sites-cloud/authoring/assets/xf-05.png)

## 建立體驗片段變體 {#creating-an-experience-fragment-variation}

您可以根據您的需要建立體驗片段的變體：

1. 開啟您的碎片 [編輯](#editing-your-experience-fragment)。
1. 開啟 **變體** 頁籤。

   ![建立體驗片段變體](/help/sites-cloud/authoring/assets/xf-06.png)

1. **建立** 允許您建立：

   * **變異**
   * **變數為 live-copy**.

1. 定義所需的屬性：

   * **範本**
   * **標題**
   * **名稱**  — 如果留空，則從「標題」中派生
   * **說明**
   * **變數標記**

   例如：

   ![變體屬性](/help/sites-cloud/authoring/assets/xf-07.png)


1. 確認 **完成**，新的變體將顯示在面板中。

## 使用您的體驗片段 {#using-your-experience-fragment}

您現在可以在創作頁面時使用您的體驗片段：

1. 開啟任何頁面進行編輯。

1. 在頁面段系統內建立體驗片段元件的實例：

1. 將實際體驗片段添加到元件實例；其中之一：

   * 將所需片段從「資產瀏覽器」中拖放到元件上。
   * 選擇 **配置** 從元件工具欄中指定要使用的片段，確認 **完成**。

   >[!NOTE]
   >
   >在元件工具欄中，編輯作為在片段編輯器中開啟片段的快捷方式。

例如：`http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![頁面編輯器中的體驗片段](/help/sites-cloud/authoring/assets/xf-08.png)

## 建置區塊 {#building-blocks}

您可以選擇一個或多個元件以建立用於回收片段中的構建塊：

### 建立構件塊 {#creating-a-building-block}

要建立新構建基塊：

1. 在「體驗片段」編輯器中，選擇要重新使用的元件：

   ![選擇構建塊的元件](/help/sites-cloud/authoring/assets/xf-09.png)

1. 從元件工具欄中，選擇 **轉換為構建基塊**:

   ![「構建基塊」按鈕](/help/sites-cloud/authoring/assets/xf-10.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![名稱構建塊](/help/sites-cloud/authoring/assets/xf-11.png)

1. 建 **立區塊** (Building Block **)將顯示在左側標籤(** Local)中，並可以選取以執行進一步動作：

   ![鐵軌中的砌塊](/help/sites-cloud/authoring/assets/xf-12.png)

#### 管理構建塊 {#managing-a-building-block}

您的構建基塊在 **構造塊** 頁籤。 對於每個塊，可執行以下操作：

* **轉到首頁**:在新頁籤中開啟根頁變體
* **重新命名**
* **刪除**

![管理構建塊](/help/sites-cloud/authoring/assets/xf-13.png)

#### 使用構建基塊 {#using-a-building-block}

您可以將構建塊拖到任何片段的段落系統，就像與任何元件一樣。

編輯「體驗片段」時，「可用構建塊」將顯示在左手框中。 您可以根據以下內容進行篩選：

* **本地**  — 當前經驗片段的構建基塊
* **全部**  — 所有碎片的構建塊

![選擇構建基塊](/help/sites-cloud/authoring/assets/xf-14.png)

## 體驗片段上的個性化 {#personalization-experience-fragment}

通過個性化體驗片段，作為營銷人員，您可以只為體驗片段定義一次目標受眾，然後在任何頁面中重新使用該片段。 此特性：

* 無需每次使用片段時為每個受眾指定所需的變體
* 在產品中保持造型

可以建立一個「體驗片段」，該片段內分組了多個元件。 您還可以為每個特定受眾段建立片段的變體，然後在所需的頻道中重複使用這些體驗片段。

通過定義 **個性化** 體驗片段或變體或包含片段的資料夾上的屬性；這意味著繼承可以覆蓋個性化屬性。

配置這些屬性還可 **目標** 模式。

### 為您的體驗片段定義個性化 {#defining-personalization-experience-fragment}

要個性化您的碎片：

1. 導航至 **體驗片段** 控制台。

1. 選擇資料夾或片段，然後 **屬性** 的子菜單。

   >[!NOTE]
   >
   >資料夾上定義的個性化屬性將通過子樹和該子樹內的體驗片段（和變體）向下繼承所有子資料夾。 可以通過斷開繼承來覆蓋這些繼承。

1. 開啟 **個性化** 的子菜單。 例如，在資料夾上：

   ![體驗片段 — 個性化屬性](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >當片段嵌入到「站點」頁面時， **個性化** 已配置，則頁面的個性化版本將在頁面呈現時使用。
   >
   >對於在片段中的元件上執行的目標，必須滿足以下條件才能在頁面呈現中工作：
   >
   >的 **上下文中心路徑** 的 **個性化** 頁籤必須為：
   >
   >* 與為將呈現片段的頁面配置的路徑相同
      >或:
   >* 包含在為頁配置的ContextHub中定義的儲存子集的路徑

   >
   > 
的 **段路徑** 的 **個性化** 頁籤必須為：
   * 與為將呈現片段的頁配置的路徑相同，或
   * 包含為頁面配置的段子子集的路徑


### 為您的體驗片段定義目標 {#defining-targeting-experience-fragment}

配置個性化屬性後，開啟片段進行編輯時，「目標」模式將可用。

![體驗片段編輯器 — 目標模式](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

此模式與頁面編輯的方式相同。 請參閱 [頁面編輯器的目標模式](/help/sites-cloud/authoring/personalization/targeted-content.md) 的子菜單。

## 您的體驗片段的詳細資訊 {#details-of-your-experience-fragment}

可以查看您的碎片的詳細資訊：

1. 導航到您的體驗片段的位置（不要進一步導航到片段中的變體）。
詳細資訊顯示在 **體驗片段** 控制台， **清單視圖** 包括 [導出到目標](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![體驗片段詳細資訊](/help/sites-cloud/authoring/assets/xf-15.png)

1. 開啟 **屬性** 體驗片段：

   ![「屬性」按鈕](/help/sites-cloud/authoring/assets/xf-16.png)

   這些屬性可在以下各個頁籤中使用：

   >[!CAUTION]
   開啟時會顯示這些頁籤 **屬性** 從「體驗片段」控制台。
   如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 。

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-17.png)

   * **基本**
      * **標題**  — 強制
      * **說明**
      * **標記**
      * **變型總數**  — 僅資訊
      * **Web變型數**  — 僅資訊
      * **非Web變型數**  — 僅資訊
      * **使用此片段的頁數**  — 僅資訊
   * **雲端服務**
      * **雲端設定**
      * **雲端服務設定**
      * **Facebook 頁面 ID**
      * **Pinterest Board**
   * **引用**
      * 引用清單
   * **個人化**
      * **ContextHub 路徑**
      * **區段路徑**
      * **品牌**

## 純HTML格式副本 {#the-plain-html-rendition}

使用 `.plain.` selector中，您可以從瀏覽器訪問純HTML格式副本。

>[!NOTE]
雖然這可以直接從瀏覽器獲得， [主要目的是允許其他應用程式（例如，第三方Web應用程式、自定義移動實現）直接使用URL訪問體驗片段的內容](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition)。

## 發佈體驗片段 {#publishing-experience-fragments}

發佈您的體驗片段與 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （從「體驗片段」控制台或編輯器）。

或者，您也可以 [發佈到預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md) （再次從「體驗片段」控制台或編輯器中）。

## 導出體驗片段 {#exporting-experience-fragments}

預設情況下，「體驗片段」以HTML格式傳遞。 這可供第三方AEM渠道使用。

對於導出到Adobe Target，還可以使用JSON。 請參閱：

* [整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [將體驗片段匯出到 Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
