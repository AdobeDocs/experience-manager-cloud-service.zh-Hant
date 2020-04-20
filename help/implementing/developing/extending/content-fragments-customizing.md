---
title: 自訂和擴充內容片段
description: 內容片段可延伸標準資產。
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7

---


# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager中，內容片段延伸了標準資產；請參閱：

* [使用內容片段建立和管理內容片段](/help/assets/content-fragments/content-fragments.md) , [以及使用內容片段製作頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md) ，以取得有關內容片段的詳細資訊。

* [管理資產](/help/assets/manage-digital-assets.md) ，自 [訂和擴充資產編輯器](/help/assets/extend-asset-editor.md) ，以取得標準資產的詳細資訊。

## 架構 {#architecture}

內容片 [段的基](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 本組成部分包括：

* 內容 *片段*,
* 由一或多個內容 *元素組成*,
* 以及哪些變數可包含一或多個 *內容變數*。

視片段類型而定，也會使用模型 **或簡單片段** 範本：

>[!CAUTION]
>
>[現在建議使用內容片段模型](/help/assets/content-fragments/content-fragments-models.md) ，以建立您的所有片段。
>
>內容片段模型用於WKND中的所有範例。

* 內容片段模型:

   * 用於定義包含結構化內容的內容片段。
   * 內容片段模型會定義內容片段建立時的結構。
   * 片段參照模型；因此，對模型的更改可能會／會影響任何相依片段。
   * 模型是由資料類型組成。
   * 新增變數等的函式必須相應地更新片段。
   >[!NOTE]
   >
   >若要顯示／轉譯內容片段，您的帳戶必須擁 `read` 有模型權限。

   >[!CAUTION]
   >
   >對現有內容片段模型所做的任何變更都會影響相關片段；這會導致這些片段中的孤立屬性。

* 內容片段範本——簡 **單片段**:

   * 用於定義簡單內容片段。

   * 此範本定義內容片段建立時的（基本、僅文字）結構。

   * 模板建立時將複製到片段。

   * 新增變數等的函式必須相應地更新片段。

   * 內容片段範本(**Simple Fragment**)的運作方式與AEM生態系統中其他範本機制（例如頁面範本等）的運作方式不同。 因此，應單獨考慮。

   * 基於簡單片 **段模板** ，對內容的MIME類型進行管理；這表示每個元素和變數都可以有不同的MIME類型。

### 整合網站與資產 {#integration-of-sites-with-assets}

內容片段管理(CFM)是AEM資產的一部份，其格式為：

* 內容片段是資產。
* 他們使用現有的資產功能。
* 它們與資產（管理控制台等）完全整合。

內容片段視為網站功能：

* 在編寫頁面時會使用這些工具。

#### 將結構化內容片段對應至資產 {#mapping-structured-content-fragments-to-assets}

![內容片段至資產結構化](assets/content-fragment-to-assets-structured.png)

具有結構化內容的內容片段（即基於內容片段模型）被映射到單一資產：

* 所有內容都儲存在資 `jcr:content/data` 產的節點下：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數會儲存在子節點下，子節點會攜帶變數的名稱：例如， `jcr:content/data/myvariation`

   * 每個元素的資料作為具有元素名稱的屬性儲存在相應的子節點中：例如，元素的內容 `text` 儲存為屬性 `text``jcr:content/data/master`

* 中繼資料和相關內容會儲存在 `jcr:content/metadata`下方，但標題和說明除外，它們不被視為傳統中繼資料，並儲存在 `jcr:content`

#### 將簡單內容片段對應至資產 {#mapping-simple-content-fragments-to-assets}

![內容片段至資產的簡單易用](assets/content-fragment-to-assets-simple.png)

簡單內容片段(以「簡 **單片段** 」範本為基礎)會對應至由主要資產和（選用）子資產組成的組合：

* 片段的所有非內容資訊（例如標題、說明、中繼資料、結構）都會專門管理在主資產上。
* 片段的第一元素的內容被映射到主資產的原始格式副本。

   * 第一個元素的變化（如果有的話）會對應至主要資產的其他轉譯。

* 其他元素（如果現有）會對應至主要資產的子資產。

   * 這些附加元素的主要內容映射到相應子資產的原始格式副本。
   * 其他元素的其他變動（如適用）會對應至個別子資產的其他轉譯。

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段的持有方式如下：

`/content/dam`

#### 資產權限 {#asset-permissions}

如需詳細資訊，請參 [閱內容片段——刪除考量事項](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能整合 {#feature-integration}

要與Assets核心整合：

* 內容片段管理(CFM)功能以資產核心為基礎。

* CFM針對卡片／欄/清單檢視中的項目提供其專屬的實作；這些外掛程式可插入現有的Assets內容轉譯實作。

* 已擴充數個「資產」元件，以迎合內容片段的需求。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>內容 [片段元件是核心元件的一部分](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)。 如需詳 [細資訊，請參閱開發核心](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) 元件。

您可從AEM頁面參考內容片段，就像任何其他資產類型一樣。 AEM提供「內 **[容片段」核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)**-[可讓您在頁面上包含內容片段的元件](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page)。 您也可以延伸此**[內容片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** 核心元件。

* 元件使用屬 `fragmentPath` 性來參考實際內容片段。 該 `fragmentPath` 財產的處理方式與其他資產類型的類似財產相同；例如，當內容片段移至其他位置時。

* 該元件允許您選擇要顯示的變化。

* 此外，還可以選擇一系列段落來限制輸出；例如，這可用於多欄輸出。

* 此元件允許介於內容之間：

   * 此元件可讓您放置其他資產（影像等）在引用片段的段落之間。

   * 對於中介內容，您需要：

      * 注意參考資料不穩定的可能性；內容之間（在編寫頁面時新增）與其旁邊的段落沒有固定關係，在內容之間位置之前插入新段落（在內容片段編輯器中）可能會失去相對位置

      * 請考慮其他參數（例如變數和段落篩選），以設定在頁面上呈現的內容

>[!NOTE]
>
>**內容片段模型:**
>
>當使用以頁面上的內容片段模型為基礎的內容片段時，會參考模型。 這表示如果模型在您發佈頁面時尚未發佈，則會標籤此模型，並將模型新增至要隨頁面一起發佈的資源。
>
>**內容片段範本——簡單片段：**
>
>使用以頁面上的內容片段範本 **Simple Fragment** （簡單片段）為基礎的內容片段時，建立片段時，沒有範本複製的參考。

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可與下列項目整合：

* **翻譯**

   內容片段與AEM轉譯工作流程完全整合。 在建築層面，這意味著：

   * 內容片段的個別翻譯實際上是分開的片段；例如：

      * 它們位於不同的語言根系下；但在相關語言根目錄下，卻有完全相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基於規則的路徑外，內容片段的不同語言版本之間沒有進一步的聯繫；雖然UI提供在語言變數之間導覽的方式，但是它們會以兩個不同的片段處理。
   >[!NOTE]
   >
   >AEM翻譯工作流程可搭配 `/content`:
   >
   >* 由於內容片段模型位於 `/conf`其中，因此這些模型不包含在此類翻譯中。 您可以將UI字串國際化。


* **中繼資料結構**

   * 內容片段（重新）使用可 [以使用標準資產定義的中繼資料結構](/help/assets/metadata-schemas.md)。

   * CFM提供其專屬的特定架構：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 各個模式表單與片段編輯器整合。

## 內容片段管理API —— 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/package-frame.html)

>[!CAUTION]
>
>強烈建議您使用伺服器端API，而非直接存取內容結構。

### 主要介面 {#key-interfaces}

以下三個介面可用作入口點：

* **內容片段** ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   此介面提供您以下方式：

   * 管理基本資料(例如：取得名稱；get/set title/description)
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素(請參閱 [說明](#caveats))

      * 存取元素資料(請參 `ContentElement`閱)
   * 為片段定義的清單變化
   * 全域建立新變化
   * 管理相關內容：

      * 清單系列
      * 新增系列
      * 移除系列
   * 存取片段的模型或範本
   代表片段主要元素的介面包括：

   * **內容元素** ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得／設定內容
      * 存取元素的變化：

         * 清單變化
         * 依名稱取得變化
         * 建立新的變化(請參 [閱說明](#caveats))
         * 移除變數(請參 [閱說明](#caveats))
         * 存取變數資料(請參 `ContentVariation`閱)
      * 解決變數的捷徑（如果指定的變數不適用於元素，則套用某些額外的實施特定備援邏輯）
   * **內容變化** ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得／設定內容
      * 簡單同步，基於上次修改的資訊
   這3個介面( `ContentFragment`、 `ContentElement`、 `ContentVariation``Versionable` )都擴充了新增內容片段所需版本控制功能的介面：

   * 建立元素的新版本
   * 元素的清單版本
   * 取得版本化元素的特定版本內容







### 適應——使用adaptTo() {#adapting-using-adaptto}

可調整下列項目：

* `ContentFragment` 可適用於：

   * `Resource` -基礎Sling資源；直接更新基礎 `Resource` 需要重建對 `ContentFragment` 像。

   * `Asset` -代表內 `Asset` 容片段的DAM抽象化；直接更新 `Asset` 需要重建對 `ContentFragment` 像。

* `ContentElement` 可適用於：

   * `ElementTemplate` -用於訪問元素的結構資訊。

* `Resource` 可適用於：

   * `ContentFragment`

### 注意事項 {#caveats}

應當指出：

* 整個API的設計不會 **自動** 保留變更（除非API JavaDoc另有說明）。 因此，您必須始終提交各個請求（或實際使用的解析程式）的資源解析程式。

* 可能需要額外努力的任務：

   * 建立新的變 `ContentFragment` 數以更新資料結構。

   * 使用元素移除現有變數 `ContentElement.removeVariation()`不會更新指派給變數的全域資料結構。 為確保這些資料結構保持同步，請改 `ContentFragment.removeVariation()` 用，以全域移除變數。

## 內容片段管理API —— 用戶端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>用戶端API為內部。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

   內 `filter.xml` 容片段管理的設定，不會與Assets核心內容套件重疊。

## 編輯工作階段 {#edit-sessions}

>[!CAUTION]
>
>請考慮此背景資訊。 您不應在此更改任何內容(因為它在儲存庫中標籤為 *私用區* )，但在某些情況下，它可能有助於瞭解引擎蓋下的操作方式。

編輯可跨多個檢視（= HTML頁面）的內容片段是原子。 因為原子式多檢視編輯功能不是典型的AEM概念，所以內容片段會使用所謂的編輯 *工作階段*。

當用戶在編輯器中開啟內容片段時，將啟動編輯會話。 當使用者離開編輯器時，編輯工作階段會完成，方法是選取「 **儲存** 」 **或「取消」**。

從技術上講，所有編輯都是在 *即時內容* ，就像所有其他AEM編輯一樣。 啟動編輯會話時，將建立當前未編輯狀態的版本。 如果使用者取消編輯，則會還原該版本。 如果使用者按一下「 **儲存**」，則不會執行任何特定動作，因為所有編輯都會在即時內容上執行 ** ，因此所有變更都會持續存在。 此外，按一下「 **儲存** 」會觸發一些背景處理（例如建立全文搜尋資訊和／或處理混合媒體資產）。

邊緣案件有一些安全措施；例如，如果使用者嘗試離開編輯器而未儲存或取消編輯工作階段。 此外，還提供定期自動儲存功能，以防止資料遺失。
請注意，兩個使用者可同時編輯相同的內容片段，因此可能覆寫彼此的變更。 為避免此情況，內容片段必須套用DAM管理員的 *Checkout* （結帳）動作來鎖定。

## 範例 {#examples}

### 範例：存取現有內容片段 {#example-accessing-an-existing-content-fragment}

若要達成此目的，您可以將代表API的資源調整為：

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

若要以程式設計方式建立新的內容片段，您必須使用模型`FragmentTemplate` 或範本資源所調整的內容片段。

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

使用 [配置管理器](/help/assets/content-fragments/content-fragments-managing.md#save-cancel-and-versions) (ConfMgr)可以定義自動保存間隔（以秒為單位）:

* 節點： `<conf-root>/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`
* 類型: `Long`

* 預設值： `600` （10分鐘）;此定義於 `/libs/settings/dam/cfm/jcr:content`

如果要設定5分鐘的自動儲存間隔，您需要在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`

* 類型: `Long`

* 值： `300` （5分鐘等於300秒）

## 頁面製作的元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件——內容片段元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html) （建議）
