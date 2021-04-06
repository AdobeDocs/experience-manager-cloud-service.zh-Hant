---
title: 自訂和擴充內容片段
description: 內容片段可延伸標準資產。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
translation-type: tm+mt
source-git-commit: 24da05afce75a16ed2223130ac1825b10ee964e1
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 1%

---

# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager，內容片段作為Cloud Service延伸了標準資產；請參閱：

* [使用內容片段建](/help/assets/content-fragments/content-fragments.md) 立和管 [理內容片段和](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 頁面編寫，以取得內容片段的詳細資訊。

* [管理資](/help/assets/manage-digital-assets.md) 產，以取得有關標準資產的詳細資訊。

<!-- Removing the extend-asset-editor article for now as I'm unsure of its accuracy. Hence commenting this link.
* [Managing Assets](/help/assets/manage-digital-assets.md) and [Customizing and Extending the Asset Editor](/help/assets/extend-asset-editor.md) for further information about standard assets.
-->

## 架構 {#architecture}

內容片段的基本[組成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)為：

* A *內容片段*,
* 由一個或多個&#x200B;*內容元素*&#x200B;組成，
* 且其中可以有一或多個&#x200B;*內容變化*。

個別內容片段是以內容片段模型為基礎：

* 內容片段模型會定義內容片段建立時的結構。
* 片段參照模型；因此，對模型的更改可能會／會影響任何相依片段。
* 模型是由資料類型組成。
* 新增變數等的函式必須相應地更新片段。

   >[!NOTE]
   >
   >若要顯示／轉譯內容片段，您的帳戶必須擁有模型的`read`權限。

   >[!CAUTION]
   >
   >對現有內容片段模型所做的任何變更都會影響相關片段；這會導致這些片段中的孤立屬性。

### 整合網站與資產{#integration-of-sites-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，具體為：

* 內容片段是資產。
* 他們使用現有的資產功能。
* 它們與資產（管理控制台等）完全整合。

內容片段視為網站功能：

* 在編寫頁面時會使用這些工具。

#### 將內容片段對應至資產{#mapping-content-fragments-to-assets}

![內容片段至資產](assets/content-fragment-to-assets.png)

內容片段會根據內容片段模型，對應至單一資產：

* 所有內容都儲存在資產的`jcr:content/data`節點下：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數會儲存在子節點下，子節點會攜帶變數的名稱：
例如，`jcr:content/data/myvariation`

   * 每個元素的資料作為具有元素名稱的屬性儲存在相應的子節點中：
例如，元素`text`的內容儲存為`jcr:content/data/master`上的屬性`text`

* 中繼資料和相關內容會儲存在`jcr:content/metadata`下方
除標題和說明外，標題和說明不被視為傳統中繼資料，並儲存在 
`jcr:content`

#### 資產位置{#asset-location}

與標準資產一樣，內容片段的持有方式如下：

`/content/dam`

#### 資產權限{#asset-permissions}

如需詳細資訊，請參閱[內容片段——刪除考量事項](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能整合{#feature-integration}

要與Assets核心整合：

* 內容片段管理(CFM)功能以資產核心為基礎。

* CFM針對卡片／欄/清單檢視中的項目提供其專屬的實作；這些外掛程式可插入現有的Assets內容轉譯實作。

* 已擴充數個「資產」元件，以迎合內容片段的需求。

### 在頁面{#using-content-fragments-in-pages}中使用內容片段

>[!CAUTION]
>
>[內容片段元件是核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)的一部分。 如需詳細資訊，請參閱[開發核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)。

您可從頁面參考內容AEM片段，就像其他資產類型一樣。 提供AEM **[內容片段核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)** - [元件，可讓您在頁面上包含內容片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page)。 您也可以延伸此&#x200B;**[內容片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)**&#x200B;核心元件。

* 元件使用`fragmentPath`屬性來引用實際內容片段。 `fragmentPath`屬性的處理方式與其他資產類型的相似屬性相同；例如，當內容片段移至其他位置時。

* 該元件允許您選擇要顯示的變化。

* 此外，還可以選擇一系列段落來限制輸出；例如，這可用於多欄輸出。

* 此元件允許介於內容之間：

   * 此元件可讓您放置其他資產（影像等） 在引用片段的段落之間。

   * 對於中介內容，您需要：

      * 注意參考資料不穩定的可能性；內容之間（在編寫頁面時新增）與其旁邊的段落沒有固定關係，在內容之間位置之前插入新段落（在內容片段編輯器中）可能會失去相對位置

      * 請考慮其他參數（例如變數和段落篩選），以設定在頁面上呈現的內容

>[!NOTE]
>
>**內容片段模型:**
>
>在頁面上使用內容片段時，會參考其所依據的內容片段模型。
>
>這表示如果模型在您發佈頁面時尚未發佈，則會標籤此模型，並將模型新增至要隨頁面一起發佈的資源。

### 與其他Frameworks {#integration-with-other-frameworks}整合

內容片段可與下列項目整合：

* **翻譯**

   內容片段與翻譯工作流程完AEM全整合。 在建築層面，這意味著：

   * 內容片段的個別翻譯實際上是分開的片段；例如：

      * 它們位於不同的語言根系下；但在相關語言根目錄下，卻有完全相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基於規則的路徑外，內容片段的不同語言版本之間沒有進一步的聯繫；雖然UI提供在語言變數之間導覽的方式，但是它們會以兩個不同的片段處理。
   >[!NOTE]
   >
   >翻譯工AEM作流可與`/content`一起使用：
   >
   >* 由於內容片段模型位於`/conf`中，因此這些轉換中不包括這些模型。 您可以將UI字串國際化。


* **中繼資料結構**

   * 內容片段(re)使用[中繼資料結構](/help/assets/metadata-schemas.md)，可以與標準資產一起定義。

   * CFM提供其專屬的特定架構：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 各個模式表單與片段編輯器整合。

## 內容片段管理API —— 伺服器端{#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>強烈建議您使用伺服器端API，而非直接存取內容結構。

### 關鍵介面{#key-interfaces}

以下三個介面可用作入口點：

* **內容片段** ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   此介面提供您以下方式：

   * 管理基本資料(例如：取得名稱；get/set title/description)
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素（請參閱[Panuons](#caveats)）

      * 存取元素資料（請參閱`ContentElement`）
   * 為片段定義的清單變化
   * 全域建立新變化
   * 管理相關內容：

      * 清單系列
      * 新增系列
      * 移除系列
   * 存取片段的模型

   代表片段主要元素的介面包括：

   * **內容元素** ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得／設定內容
      * 存取元素的變化：

         * 清單變化
         * 依名稱取得變化
         * 建立新變化（請參閱[Panuons](#caveats)）
         * 移除變數（請參閱[注意事項](#caveats)）
         * 存取變數資料（請參閱`ContentVariation`）
      * 解決變數的捷徑（如果指定的變數不適用於元素，則套用某些額外的實施特定備援邏輯）
   * **內容變化** ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得／設定內容
      * 簡單同步，基於上次修改的資訊

   這3個介面(`ContentFragment`、`ContentElement`、`ContentVariation`)都擴充了`Versionable`介面，其中新增了內容片段所需的版本控制功能：

   * 建立元素的新版本
   * 元素的清單版本
   * 取得版本化元素的特定版本內容







### 適應——使用adaptTo(){#adapting-using-adaptto}

可調整下列項目：

* `ContentFragment` 可適用於：

   * `Resource` -基礎Sling資源；直接更新基 `Resource` 礎需要重建對 `ContentFragment` 像。

   * `Asset` -代表內 `Asset` 容片段的DAM抽象化；直接更新 `Asset` 需要重建對 `ContentFragment` 像。

* `ContentElement` 可適用於：

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) -用於訪問元素的結構資訊。

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` 可適用於：

   * `ContentFragment`

### 警告{#caveats}

應當指出：

* 整個API的設計目的是自動&#x200B;**not**&#x200B;保留變更（除非API JavaDoc另有說明）。 因此，您必須始終提交各個請求（或實際使用的解析程式）的資源解析程式。

* 可能需要額外努力的任務：

   * 強烈建議從`ContentFragment`建立新的變數。 這可確保所有元素將共用此變化，並且會視需要更新適當的全域資料結構，以反映內容結構中新建立的變化。

   * 使用`ContentElement.removeVariation()`移除元素中現有的變數，將不會更新指派給變數的全域資料結構。 為確保這些資料結構保持同步，請改用`ContentFragment.removeVariation()`，以全域移除變數。

## 內容片段管理API —— 用戶端{#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>用戶端API為內部。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

   內容片段管理的`filter.xml`已設定為不會與Assets核心內容套件重疊。

## 編輯會話{#edit-sessions}

>[!CAUTION]
>
>請考慮此背景資訊。 您不應在此更改任何內容（因為儲存庫中標籤為&#x200B;*專用區域*），但在某些情況下，它可能有助於瞭解引擎蓋下的操作方式。

編輯可跨多個檢視（= HTML頁面）的內容片段是原子。 由於原子多視圖編輯功能不是典型的概AEM念，因此內容片段使用稱為&#x200B;*編輯會話*&#x200B;的內容片段。

當用戶在編輯器中開啟內容片段時，將啟動編輯會話。 當用戶離開編輯器時，通過選擇&#x200B;**保存**&#x200B;或&#x200B;**取消**&#x200B;完成編輯會話。

從技術上講，所有編輯作業都是在&#x200B;*live*&#x200B;內容上完成，就像所有其他編輯作業一AEM樣。 啟動編輯會話時，將建立當前未編輯狀態的版本。 如果使用者取消編輯，則會還原該版本。 如果使用者按一下&#x200B;**Save**，則不會執行任何特定動作，因為所有編輯作業都是在&#x200B;*live*&#x200B;內容上執行，因此所有變更都已持續存在。 此外，按一下&#x200B;**Save**&#x200B;會觸發一些背景處理（例如建立全文搜尋資訊和／或處理混合媒體資產）。

邊緣案件有一些安全措施；例如，如果使用者嘗試離開編輯器而未儲存或取消編輯工作階段。 此外，還提供定期自動儲存功能，以防止資料遺失。
請注意，兩個使用者可同時編輯相同的內容片段，因此可能覆寫彼此的變更。 為避免此情況，內容片段必須套用DAM管理對片段的*Checkout*&#x200B;動作來鎖定。

## 範例{#examples}

### 範例：訪問現有內容片段{#example-accessing-an-existing-content-fragment}

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

### 範例：建立新內容片段{#example-creating-a-new-content-fragment}

若要以程式設計方式建立新的內容片段，您必須使用
`FragmentTemplate`適用於模型資源。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動保存間隔{#example-specifying-the-auto-save-interval}

[自動保存間隔](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions)（以秒為單位）可使用配置管理器(ConfMgr)定義：

* 節點：`<conf-root>/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`
* 類型: `Long`

* 預設值：`600`（10分鐘）;此定義於`/libs/settings/dam/cfm/jcr:content`

如果要設定5分鐘的自動儲存間隔，您需要在節點上定義屬性；例如：

* 節點：`/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`

* 類型: `Long`

* 值：`300`（5分鐘等於300秒）

## 頁面編寫元件{#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件——內容片段元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html) （建議）
