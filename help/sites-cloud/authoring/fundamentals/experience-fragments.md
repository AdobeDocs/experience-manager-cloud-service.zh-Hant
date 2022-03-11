---
title: 體驗片段
description: 使用Adobe Experience Manager as a Cloud Service體驗片段使您的體驗可重複使用且靈活。
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: 5c907a26a976b55f1e2850650057d907d358aa07
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 8%

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
Experience Fragments eliminate the need for copy/paste.
* 支援無頭CMS使用案例。
作者只想AEM用於創作，而不想交付給客戶。 第三方系統/觸點將消耗該體驗，然後交付給最終用戶。

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
* When you use AEM as a content delivery platform for third parties.
   * Any solution that wants to use AEM as the content delivery platform.
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

1. [Configure the allowed Experience Fragment templates for that folder](#configure-allowed-templates-folder).

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

1. 選擇 **保存**。

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

   A **標題** 的子菜單。 If the **Name** is left blank it will be derived from the **Title**.

   ![體驗片段屬性](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >Tags from the Experience Fragment template will not be merged with tags on this Experience Fragment root page.
   >
   >These are completely separate.

1. 按一下&#x200B;**建立**。

   將顯示一條消息。 選取:

   * **完成** 返回到控制台
   * **開啟** 開啟片段編輯器

## 編輯您的體驗片段 {#editing-your-experience-fragment}

「體驗片段編輯器」提供與普通頁面編輯器類似的功能。

>[!NOTE]
>
>請參閱 [編輯頁面內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 的子菜單。

The following example procedure illustrates how to create a teaser for a product:

1. 從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。

1. 取決於元件：
   * 根據需要添加任何內容和/或資產。
   * Configure the properties as required.

1. Add more components as required.

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

   ![Name Building Block](/help/sites-cloud/authoring/assets/xf-11.png)

1. 建 **立區塊** (Building Block **)將顯示在左側標籤(** Local)中，並可以選取以執行進一步動作：

   ![鐵軌中的砌塊](/help/sites-cloud/authoring/assets/xf-12.png)

#### 管理構建塊 {#managing-a-building-block}

您的構建基塊在 **構造塊** 頁籤。 對於每個塊，可執行以下操作：

* **Go to master**: open the root page variation in a new tab
* **重新命名**
* **刪除**

![管理構建塊](/help/sites-cloud/authoring/assets/xf-13.png)

#### 使用構建基塊 {#using-a-building-block}

您可以將構建塊拖到任何片段的段落系統，就像與任何元件一樣。

編輯「體驗片段」時，「可用構建塊」將顯示在左手框中。 您可以根據以下內容進行篩選：

* **本地**  — 當前經驗片段的構建基塊
* **全部**  — 所有碎片的構建塊

![選擇構建基塊](/help/sites-cloud/authoring/assets/xf-14.png)

## 您的體驗片段的詳細資訊 {#details-of-your-experience-fragment}

可以查看您的碎片的詳細資訊：

1. 導航到您的體驗片段的位置（不要進一步導航到片段中的變體）。
詳細資訊會顯示在 **Experience Fragments** console的所有檢視中，「清單檢視」包 **** 括匯出至Target的詳細資訊： <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![體驗片段詳細資訊](/help/sites-cloud/authoring/assets/xf-15.png)

1. 開啟 **屬性** 體驗片段：

   ![Properties button](/help/sites-cloud/authoring/assets/xf-16.png)

   The properties are available in various tabs:

   >[!CAUTION]
   >
   >These tabs are shown when you open **Properties** from the Experience Fragments console.
   >
   >如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 。

   ![Experience Fragment properties](/help/sites-cloud/authoring/assets/xf-17.png)

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

## 純HTML格式副本 {#the-plain-html-rendition}

使用 `.plain.` selector中，您可以從瀏覽器訪問純HTML格式副本。

>[!NOTE]
>
>雖然這可以直接從瀏覽器獲得， [主要目的是允許其他應用程式（例如，第三方Web應用程式、自定義移動實現）直接使用URL訪問體驗片段的內容](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition)。

## 導出體驗片段 {#exporting-experience-fragments}

預設情況下，「體驗片段」以HTML格式傳遞。 這可供第三方AEM渠道使用。

對於導出到Adobe Target，還可以使用JSON。 請參閱：

* [整合 Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [將體驗片段導出到Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
