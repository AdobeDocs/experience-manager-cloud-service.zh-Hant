---
title: 設定搜尋表單
description: 將Search Forms for Adobe Experience Manager設定為雲端服務。
translation-type: tm+mt
source-git-commit: c48274f76db764e1cbad459e644d5fb4b753a086
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 16%

---


# 設定搜尋表單 {#configuring-search-forms}

Adobe Experience Manager做為雲端服務，提供強大的[Search](/help/sites-cloud/authoring/getting-started/search.md)機制。

此外，還有一組預先定義的選項可協助您篩選內容。 這些Facet會保留預先定義的Facet，例如&#x200B;**修改日期**、**發佈狀態**&#x200B;或&#x200B;**即時副本狀態**，以協助您快速深入瞭解所需的資源。

![搜尋和篩選使用](assets/csf-usage.png)

這些功能的結合，可協助您快速輕鬆地從下列位置找到內容：

* [搜尋與篩選](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [軌道選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)（編輯頁面時）

>[!NOTE]
>
>您可以配置基礎的[內容搜索和索引](/help/operations/indexing.md)服務。

使用&#x200B;**搜尋表單**，您可以根據您的特定需求自訂和擴充這些面板。

**搜尋表單**&#x200B;提供可結合和定義之[謂語的現成選項。 ](#predicates-and-their-settings)可通過以下方式訪問用於配置這些表單的[對話框：](#configuring-your-search-forms)

* **工具**
   * **一般**
      * **搜尋表單**

## 預設表單{#default-forms}

首次訪問&#x200B;**搜索表單**&#x200B;控制台時，您可以看到所有配置都具有掛鎖符號。 這表示對應的組態是預設（現成可用）組態——且無法刪除。 在您自訂並儲存後，鎖定將消失。 當您[刪除自訂組態](#deleting-a-configuration-to-reinstate-the-default)時，它會重新出現，此時將恢復預設值（和掛鎖指示器）。

![配置搜索表單概述](assets/csf-overview.png)

可用的預設配置（按字母順序列出）包括：

* **資產管理搜尋邊欄**
* **頁面編輯器 (文件搜尋)**
* **頁面編輯器 (體驗片段搜尋)**
* **頁面編輯器 (影像搜尋)**
* **頁面編輯器 (手稿搜尋)**
* **頁面編輯器 (頁面搜尋)**
* **頁面編輯器 (段落搜尋)**
* **頁面編輯器 (產品搜尋)**
* **頁面編輯器 (Scene7 搜尋)**
* **頁面編輯器 (視訊搜尋)**
* **專案管理搜尋邊欄**
* **專案翻譯搜尋邊欄**
* **網站管理搜尋邊欄**
* **代碼片段管理搜尋邊欄**
* **Stock 管理搜尋邊欄**
* **內容片段模型搜尋邊欄**
* **專案管理搜尋邊欄**
* **專案翻譯搜尋邊欄**

>[!NOTE]
>
>如需與資產相關的搜尋表單的詳細資訊，請參閱[資產——搜尋面](/help/assets/search-facets.md)


## 謂語及其設定{#predicates-and-their-settings}

### 謂語{#predicates}

以下謂語可用，取決於配置：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>目的</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析</td>
   <td>顯示分析支援的資料時，在「網站」瀏覽器中執行搜尋／篩選功能。 載入Analytics搜尋篩選器以符合已映射的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>核准狀態</td>
   <td>根據核准狀態進行搜尋。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>作者</td>
   <td>依作者搜尋。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>簽出者</td>
   <td>搜尋由特定使用者簽出的資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>簽出狀態</td>
   <td>搜尋具有特定結帳狀態的資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>元件</td>
   <td>允許作者搜尋／篩選含有特定元件的頁面。 例如，影像圖庫。<br /> </td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>屬性深度</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期範圍</td>
   <td>搜尋在指定範圍內為日期屬性建立的資源。 在「搜尋」面板中，您可以指定開始和結束日期。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>範圍文字（自）*</li>
     <li>範圍文字（至）*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期狀態</td>
   <td>根據到期狀態搜尋資源。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>檔案大小</td>
   <td>根據資源大小篩選資源。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>檔案類型</td>
   <td>根據檔案/MIME類型搜尋資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li> 
     <li>屬性名稱*</li>
     <li>MIME 類型路徑</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>全文</td>
   <td>Search predicate for full-text searches. 它會與'jcr:contains´運算子映射。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>群組</td>
   <td>搜尋群組的謂詞（僅用於前瞻分析謂詞）。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隱藏的篩選器</td>
   <td>屬性和值的篩選器，不對使用者顯示。</td>
   <td>
    <ul>
     <li>屬性名稱*</li>
     <li>屬性值*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>分析</td>
   <td>依據選擇的前瞻分析參數進行搜尋。</td>
   <td>這是由多個謂語組成的複雜謂語：
    <ul>
     <li>群組</li>
     <li>範圍</li>
     <li>選項</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>系列成員</td>
   <td>搜尋屬於系列成員的資產</td>
   <td>
    <ul>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>多值屬性</td>
   <td>搜尋指定屬性的多個值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>分隔符號支援</li>
     <li>輸入分隔字元</li>
     <li>忽略大小寫</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>選項</td>
   <td><p>這些選項是用戶建立的內容節點。</p> <p>如需詳細資訊，請參閱<a href="#addinganoptionspredicate">新增選項謂詞</a>。</p> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>單選</li>
     <li>新增選項</li>
     <li>手動</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>選項屬性</td>
   <td>搜尋選項的一或多個屬性。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項節點路徑</li>
     <li>屬性深度</li>
     <li>單選</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>頁面狀態</td>
   <td>根據頁面狀態篩選頁面。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>發佈屬性名稱*</li>
     <li>鎖定頁面屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>根據特定路徑進行篩選。 您可以指定多個路徑作為選項。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>新增搜尋路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑瀏覽器</td>
   <td>提供路徑瀏覽器，以在預先定義的根路徑下進行搜尋。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>根路徑</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>路徑隱藏</td>
   <td>路徑上的篩選器，使用者看不到。</td>
   <td>
    <ul>
     <li>屬性名稱(`path`)</li>
     <li>屬性值(「/content/dam」)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>在指定的屬性上搜尋。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>部分搜尋</li>
     <li>忽略大小寫</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>發佈狀態</td>
   <td>根據資源的發佈狀態篩選資源。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍</td>
   <td>搜尋位於指定範圍內的資源。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>評等</td>
   <td>根據資源的平均分級搜索資源。<br /> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>相對日期</td>
   <td>根據資源建立的相對日期篩選資源。 例如，1週前，1個月前。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>相對日期</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>滑桿範圍</td>
   <td>使用slider功能擴展範圍謂語的通用搜索謂語。 所搜尋的屬性值必須介於滑桿限制之間。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項節點路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td>根據核准和結帳狀態進行搜尋。</td>
   <td>這是由多個謂語組成的複雜謂語：
    <ul>
     <li>核准狀態</li>
     <li>簽出狀態</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>標記</td>
   <td>根據標籤進行搜尋。</td>
   <td>
    <ul>
     <li>Field Lavel</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>顯示配對所有標記選項</li>
     <li>根標籤路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範本</td>
   <td>根據選取的範本進行搜尋。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>翻譯狀態</td>
   <td>根據翻譯狀態進行搜索。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
    </ul> 
   </td>
  </tr>
 </tbody>
</table>

<!--
  <tr>
   <td>Date ???</td>
   <td>Slider-based search of assets based on a date property.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Asset Last Modified ?????</td>
   <td>Date the asset was last modified.<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>Range Options ???</td>
   <td>A specific search predicate for Assets and the same as common Slider Predicate. Is still available due to backward compatibilty issues.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Search assets based on tags. You can configure the Path property to populate various tags in the Tags list.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
-->

>[!NOTE]
>
>常見搜索謂語定義於：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>此資訊僅供參考，您不得變更`/libs`。

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 謂詞設定{#predicate-settings}

Dependent on the predicate a selection of settings are available for configuration, including:

* **欄位標籤**

   將顯示為可折疊標題或謂語欄位標籤的標籤。

* **說明**

   使用者的說明性詳細資訊。

* **預留位置**

   空文本或謂語的佔位符，以備未輸入篩選文本時使用。

* **屬性名稱**

   要搜索的屬性。 它使用相對路徑，通配符`*/*/*`指定屬性相對於`jcr:content`節點的深度（每個星號代表一個節點級別）。

   如果只想在`jcr:content`節點上具有`x`屬性的資源的第一級子節點上搜索，請使用`*/jcr:content/x`

* **屬性深度**

   在資源中搜索該屬性的最大深度。 因此，可對資源和遞歸子項執行對該屬性的搜索，直到子項的級別等於指定深度。

* **屬性值**

   屬性值是絕對字串或運算式語言；例如，`cq:Page`或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文字**

   **日期範圍**&#x200B;謂語中範圍欄位的標籤。

* **選項路徑**

   用戶可以使用謂詞設定頁籤中的路徑瀏覽器來選擇路徑。 在選擇&#x200B;**+**&#x200B;圖示後，會將選擇項目新增至有效選項清單（然後視需要移除&#x200B;**-**&#x200B;圖示）。

   這些選項是由用戶建立的內容節點，具有以下結構：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節點**
路徑與 
**Options Path**, only this is in the common predicate field, the other is specific for assets.

* **單選**
項選中後，選項將顯示為僅允許單選項的複選框。如果錯誤選取，則可取消選取核取方塊。

* **Publish和Live Copy屬性名稱Sites**
特定述詞的publish和live copy核取方塊標籤。

* &amp;ast;在&#x200B;**Settings**&#x200B;標籤中的欄位標籤上，表示欄位是必填欄位，若保留空白，則會顯示錯誤訊息。

## 配置搜索表單{#configuring-your-search-forms}

### 建立／開啟自定義配置{#creating-opening-a-customized-configuration}

1. 導覽至「**工具**、**一般**、**搜尋表單**」。

1. 選擇要定製的配置。
1. 使用&#x200B;**Edit**&#x200B;表徵圖開啟要更新的配置。
1. 如果是新的自訂，您可能想要[新增謂詞欄位，並視需要定義設定](#add-edit-a-predicate-field-and-define-field-settings)。 如果現有的自訂功能，您可以選取現有欄位，並[更新設定](#add-edit-a-predicate-field-and-define-field-settings)。
1. 選擇&#x200B;**Done**&#x200B;保存配置。 您的變更可在下次使用設定時看到。

   >[!NOTE]
   >
   >自定義的配置儲存在（如果適用）以下位置：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 添加／編輯謂詞欄位和定義欄位設定{#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義／更新其設定：

1. [開啟自訂的](#creating-opening-a-customized-configuration) 設定以進行更新。
1. 如果要添加新欄位，請開啟&#x200B;**選擇謂詞**&#x200B;頁籤，並將所需的謂詞拖動到所需位置。 例如，**日期範圍謂詞**:

   ![添加謂語](assets/csf-add-predicate.png)

1. 取決於：

   * 您正在添加新欄位：

      添加謂語後，**Settings**&#x200B;頁籤將開啟並顯示可定義的屬性。

   * 要更新現有謂詞：

      選擇謂詞欄位（在右側），然後開啟&#x200B;**Settings**&#x200B;頁籤。
   例如，**日期範圍謂詞**&#x200B;的設定：

   ![修改謂語](assets/csf-modify-predicate.png)

1. 視需要進行變更，並使用&#x200B;**Done**&#x200B;確認。 您的變更可在下次使用設定時看到。

### 預覽搜索配置{#previewing-the-search-configuration}

1. 選取「預覽」圖示：

   ![預覽圖示](assets/csf-preview-icon.png)

1. 這會顯示搜尋表單，如同在適當主控台的「搜尋」欄中顯示（完全展開）。

   ![預覽表格](assets/csf-preview-form.png)

1. **關** 閉預覽以返回並完成配置。

### 刪除謂詞欄位{#deleting-a-predicate-field}

1. [開啟自訂的](#creating-opening-a-customized-configuration) 設定以進行更新。
1. 選擇謂詞欄位（在右側），開啟&#x200B;**Settings**&#x200B;頁籤，然後選擇&#x200B;**Delete**&#x200B;表徵圖（左下）。

   ![刪除圖示](assets/csf-delete-icon.png)

1. 對話方塊會要求確認刪除動作。

1. 使用&#x200B;**Done**&#x200B;確認此變更和任何其他變更。

### 刪除配置（恢復預設值）{#deleting-a-configuration-to-reinstate-the-default}

在您自訂設定後，這將覆寫預設值。 您可以刪除自訂的設定，重新設定預設的設定。

>[!NOTE]
>
>不能刪除預設配置。

從控制台刪除自定義配置：

1. 選擇所需的配置(例如，**頁面編輯器（段落搜索）**)，然後選擇工具欄中的&#x200B;**刪除**&#x200B;表徵圖：

   ![恢復預設值](assets/csf-restore-default.png)

1. 將刪除自定義配置並恢復預設配置（這由控制台中重新出現掛鎖符號表示）。

### 添加選項謂語{#adding-options-predicates}

選項謂語（選項、選項屬性）可讓您設定要搜尋的項目。 通常用來搜尋頁面下方的內容；例如，頁面節點上的屬性。

下列範例（根據用於建立頁面的範本進行搜尋）說明相關步驟：

1. 建立定義要搜索的屬性的節點。

   您需要一個根節點，其中包含用戶可以使用的各個選項的定義。

   各個選項的節點需要以下屬性：

   * `jcr:title` -要在搜索邊欄中顯示的欄位標籤
   * `value` -要搜索的屬性值

   ![謂詞定義](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
   >
   >這是因為下次升級實例時會覆寫`/libs`的內容（套用修補程式或功能套件時，很可能會覆寫）。
   >
   >配置和其他更改的建議方法為：
   >
   >1. 在`/libs`中，在`/apps`下重新建立所需項目。 在本例中，來源為：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在`/apps.`中進行任何更改


1. 開啟&#x200B;**搜尋表單**&#x200B;主控台，並選取您要更新的組態。 例如，**網站管理搜尋邊欄**。 然後選擇&#x200B;**編輯**。

1. 視配置而定，將&#x200B;**選項**&#x200B;或&#x200B;**選項屬性**&#x200B;添加到配置中。
1. 更新欄位，尤其是：

   * **屬性名稱**

      在目標節點上指定要搜索的節點屬性。 例如：

      `jcr:content/cq:template`

   * **選項節點路徑**

      選取您的選項所在的路徑。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![選項謂語](assets/csf-options-predicate-02.png)

1. 選擇&#x200B;**Done**&#x200B;以保存配置。
1. 導覽至適當的主控台（在此範例中，為&#x200B;**Sites**），並開啟&#x200B;**搜尋——篩選器**&#x200B;邊欄。 新定義的搜尋表單以及各種選項將會顯示。 選擇所需選項以查看搜索結果。

   ![使用的選項](assets/csf-options-usage.png)


## 使用者權限 {#user-permissions}

下表列出在搜尋表單上執行編輯、刪除和預覽動作所需的權限。

<table>
 <thead>
  <tr>
   <td><strong>動作</strong></td>
   <td><strong>權限</strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>編輯 </td>
   <td>對<code>/apps </code>節點的讀取、寫入權限。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><code>/apps</code>節點上的讀、寫、刪除權限</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td>對<code>/var/dam/content</code>節點執行讀取、寫入、刪除權限。<br /> 讀取、寫入節點 <code>/apps</code> 權限。</td>
  </tr>
 </tbody>
</table>
