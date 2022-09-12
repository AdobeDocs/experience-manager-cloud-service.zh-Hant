---
title: 自訂和擴充內容片段
description: 內容片段會延伸標準資產。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 1%

---

# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager as a Cloud Service中，內容片段會延伸標準資產；請參閱：

* [建立和管理內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 和 [使用內容片段進行頁面編寫](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 以取得內容片段的詳細資訊。

* [管理資產](/help/assets/manage-digital-assets.md) 以取得標準資產的詳細資訊。

## 架構 {#architecture}

基本 [組成部分](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 內容片段包括：

* A *內容片段*,
* 由一個或多個 *內容元素*,
* 可以有一個或多個 *內容變數*.

個別內容片段是以內容片段模型為基礎：

* 內容片段模型會在建立內容片段時定義其結構。
* 片段會參照模型；因此，模型的變更可能會/將影響任何相依片段。
* 模型是資料類型的組建。
* 新增變異等的函式必須據以更新片段。

   >[!NOTE]
   >
   >若要顯示/呈現內容片段，您的帳戶必須 `read` 模型的權限。

   >[!CAUTION]
   >
   >對現有內容片段模型的任何變更都可能影響相依片段；這可能會導致這些片段中的孤立屬性。

### Sites與資產的整合 {#integration-of-sites-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 內容片段是資產。
* 它們使用現有的Assets功能。
* 它們已與資產（管理控制台等）完全整合。

內容片段視為Sites功能，如下：

* 編寫頁面時會使用這些參數。

#### 將內容片段對應至資產 {#mapping-content-fragments-to-assets}

![內容片段至資產](assets/content-fragment-to-assets.png)

內容片段會根據內容片段模型對應至單一資產：

* 所有內容都儲存在 `jcr:content/data` 資產的節點：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數儲存在帶有變數名稱的子節點下：例如 `jcr:content/data/myvariation`

   * 每個元素的資料作為具有元素名稱的屬性儲存在相應的子節點中：例如，元素的內容 `text` 儲存為屬性 `text` on `jcr:content/data/master`

* 元資料和相關內容儲存在下方 `jcr:content/metadata`
除了標題和說明，這些內容不被視為傳統中繼資料並儲存在 
`jcr:content`

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於：

`/content/dam`

#### 資產權限 {#asset-permissions}

如需詳細資訊，請參閱 [內容片段 — 刪除考量事項](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### 功能整合 {#feature-integration}

若要與Assets整合核心：

* 內容片段管理(CFM)功能是以資產核心為基礎。

* CFM針對卡片/欄/清單檢視中的項目提供其專屬實作；這些外掛程式會插入現有的Assets內容呈現實作。

* 數個Assets元件已擴充，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [內容片段元件是核心元件的一部分](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html). 請參閱 [開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) 以取得更多詳細資訊。

可從AEM頁面參照內容片段，如同任何其他資產類型。 AEM提供 **[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)** - a [可讓您在頁面上包含內容片段的元件](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). 您也可以延伸此範本 **[內容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** 核心元件。

* 元件使用 `fragmentPath` 屬性來參考實際內容片段。 此 `fragmentPath` 財產的處理方式與其他資產類型的類似財產相同；例如，內容片段移至其他位置時。

* 元件可讓您選取要顯示的變數。

* 此外，可以選擇一系列段落來限制輸出；例如，這可用於多欄輸出。

* 元件允許介入內容：

   * 此元件可讓您放置其他資產（影像等） 在引用片段的段落之間。

   * 針對中間內容，您需要：

      * 注意不穩定的參考資料的可能性；中間內容（製作頁面時新增）與它位於旁邊的段落沒有固定關係，在中間內容的位置之前插入新段落（在內容片段編輯器中）可能會丟失相對位置

      * 請考量其他參數（例如變異和段落篩選器），以設定要在頁面上呈現的內容

>[!NOTE]
>
>**內容片段模型:**
>
>在頁面上使用內容片段時，會參考其所依據的內容片段模型。
>
>這表示如果您在發佈頁面時尚未發佈模型，則會標籤此模型，並將模型新增至要隨頁面發佈的資源。

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可與：

* **翻譯**

   內容片段已與 [AEM翻譯工作流程](/help/sites-cloud/administering/translation/overview.md). 在架構層面，這表示：

   * 內容片段的個別翻譯實際上是個別片段；例如：

      * 它們位於不同的語言根；但在相關語言根下完全共用相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基於規則的路徑外，內容片段的不同語言版本之間沒有進一步的連接；雖然UI提供在語言變體之間導覽的方式，但這些片段會以兩個不同片段的形式處理。
   >[!NOTE]
   >
   >AEM翻譯工作流程可搭配 `/content`:
   >
   >* 由於內容片段模型位於 `/conf`，則這些內容不會包含在此類翻譯中。 您可以將UI字串國際化。


* **中繼資料結構**

   * 內容片段（重新）使用 [中繼資料結構](/help/assets/metadata-schemas.md)，可使用標準資產來定義。

   * CFM提供其專屬的結構：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 各個架構表單與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而非直接存取內容結構。

### 密鑰介面 {#key-interfaces}

以下三個介面可作為入口點：

* **內容片段** ([內容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   該介面提供您以下方法：

   * 管理基本資料(例如取得名稱；get/set title/description)
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素(請參閱 [警告](#caveats))

      * 存取元素資料(請參閱 `ContentElement`)
   * 為片段定義的清單變化
   * 全域建立新變體
   * 管理相關內容：

      * 清單集合
      * 新增集合
      * 移除集合
   * 存取片段的模型

   代表片段主要元素的介面包括：

   * **內容元素** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 元素的存取變化：

         * 清單變數
         * 依名稱取得變體
         * 建立新變體(請參閱 [警告](#caveats))
         * 移除變異(請參閱 [警告](#caveats))
         * 存取變異資料(請參閱 `ContentVariation`)
      * 解決變異的捷徑（如果指定的變異不適用於元素，則套用一些其他的實作專用備援邏輯）
   * **內容變異** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 基於上次修改資訊的簡單同步

   所有三個介面( `ContentFragment`, `ContentElement`, `ContentVariation`)延伸 `Versionable` 介面，新增版本設定功能，內容片段所需：

   * 建立新版本的元素
   * 元素的清單版本
   * 取得版本化元素的特定版本的內容







### 適應 — 使用adapTo() {#adapting-using-adaptto}

可調整下列項目：

* `ContentFragment` 可調整為：

   * `Resource`  — 基礎Sling資源；更新基礎 `Resource` 直接需要重建 `ContentFragment` 物件。

   * `Asset` - DAM `Asset` 代表內容片段的抽象化；更新 `Asset` 直接需要重建 `ContentFragment` 物件。

* `ContentElement` 可調整為：

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html)  — 存取元素的結構資訊。

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` 可調整為：

   * `ContentFragment`

### 警告 {#caveats}

應當指出：

* 整個API的設計目的 **not** 自動保留變更（除非API JavaDoc另有說明）。 因此，您必須一律提交個別請求的資源解析器（或您實際使用的解析器）。

* 可能需要付出額外努力的任務：

   * 強烈建議從 `ContentFragment`. 這可確保所有元素都共用此變數，並且將根據需要更新適當的全局資料結構，以反映內容結構中新建立的變數。

   * 透過元素移除現有變數，使用 `ContentElement.removeVariation()`，將不會更新指派給變數的全域資料結構。 為確保這些資料結構保持同步，請使用 `ContentFragment.removeVariation()` 而會全域移除變數。

## 內容片段管理API — 用戶端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>用戶端API為內部。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

   此 `filter.xml` 針對內容片段管理所設定，使其與「資產」核心內容套件不重疊。

## 編輯工作階段 {#edit-sessions}

>[!CAUTION]
>
>請考慮這個背景資訊。 您不應在此變更任何項目(因為它標示為 *私人區域* )，但在某些情況下，這可能有助於了解外殼下的運作方式。

編輯內容片段可跨越多個檢視(=HTML頁面)是原子。 由於原子多檢視編輯功能不是典型的AEM概念，因此內容片段使用 *編輯工作階段*.

當使用者在編輯器中開啟內容片段時，會啟動編輯工作階段。 當使用者借由選取任一選項離開編輯器時，編輯工作階段就會完成 **儲存** 或 **取消**.

技術上，所有編輯作業都會在上完成 *live* 內容，就像其他所有AEM編輯一樣。 開始編輯工作階段時，會建立目前未編輯狀態的版本。 如果使用者取消編輯，該版本會還原。 如果使用者點按 **儲存**，則不會執行任何特定動作，因為所有編輯都是在上執行 *live* 內容，因此所有變更都已持續存在。 此外，按一下 **儲存** 會觸發某些背景處理（例如建立全文搜尋資訊及/或處理混合媒體資產）。

邊緣案件有一些安全措施；例如，如果使用者嘗試離開編輯器而未儲存或取消編輯工作階段。 此外，還提供定期自動儲存，以防止資料遺失。
請注意，兩個使用者可以同時編輯相同的內容片段，因此可能會覆寫彼此的變更。 若要防止此情況，必須套用DAM管理的 *結帳* 片段上的動作。

## 範例 {#examples}

### 範例：存取現有內容片段 {#example-accessing-an-existing-content-fragment}

若要達成此目標，您可以調整代表API的資源，以：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 範例：建立新內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立新內容片段，您需要使用
`FragmentTemplate` 從模型資源中調整。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

此 [自動儲存間隔](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) （以秒為單位）可使用配置管理器(ConfMgr)來定義：

* 節點： `<conf-root>/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`
* 類型: `Long`

* 預設值： `600` （10分鐘）;此定義於 `/libs/settings/dam/cfm/jcr:content`

如果要設定5分鐘的自動儲存間隔，則需要在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`

* 類型: `Long`

* 值： `300` （5分鐘等於300秒）

## 頁面製作元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) （建議）
