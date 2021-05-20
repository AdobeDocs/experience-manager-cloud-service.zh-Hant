---
title: 設定搜尋表單
description: 將搜尋Forms設定為Adobe Experience Manager作為Cloud Service。
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 16%

---

# 設定搜尋表單 {#configuring-search-forms}

Adobe Experience Manager as aCloud Service隨附強大的[Search](/help/sites-cloud/authoring/getting-started/search.md)機制。

此外，還有一組預先定義的選項可協助您篩選內容。 這些保留預先定義的Facet，如&#x200B;**修改日期**、**發佈狀態**&#x200B;或&#x200B;**Livecopy狀態**，以幫助您快速深入鑽研到所需資源。

![搜尋和篩選使用情形](assets/csf-usage.png)

這些功能可協助您快速輕鬆地從以下位置找到內容：

* [搜尋與篩選](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [邊欄選取器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)（編輯頁面時）

>[!NOTE]
>
>您可以配置基礎的[內容搜索和索引](/help/operations/indexing.md)服務。

您可以使用&#x200B;**搜尋Forms**，根據您的特定需求自訂和擴充這些面板。

**搜尋Forms**&#x200B;提供可結合併定義的[述詞](#predicates-and-their-settings)的現成選項。 可通過以下方式訪問用於配置這些表單的[對話框：](#configuring-your-search-forms)

* **工具**
   * **一般**
      * **搜尋表單**

## 預設Forms {#default-forms}

首次訪問&#x200B;**搜索Forms**&#x200B;控制台時，您會看到所有配置都帶有掛鎖符號。 這表示對應的設定是預設（現成）設定，且無法刪除。 自訂並儲存後，鎖定就會消失。 當您[刪除自定義配置](#deleting-a-configuration-to-reinstate-the-default)時，它將重新出現，在這種情況下，將恢復預設值（和掛鎖指示器）。

![配置搜索表單概述](assets/csf-overview.png)

可用的預設配置（按字母順序列出）有：

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
>如需與資產相關的搜尋表單的詳細資訊，請參閱[資產 — 搜尋Facet](/help/assets/search-facets.md)


## 謂語及其設定{#predicates-and-their-settings}

### 謂語 {#predicates}

下列謂語可用，視設定而定：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>用途</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析</td>
   <td>顯示分析支援的資料時，在Sites瀏覽器中執行搜尋/篩選功能。 載入Analytics搜尋篩選器，以符合對應的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>核准狀態</td>
   <td>根據批准狀態進行搜索。</td>
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
   <td>根據作者進行搜尋。</td>
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
   <td>搜尋特定使用者結帳的資產。</td>
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
   <td>可讓作者搜尋/篩選含有特定元件的頁面。 例如，影像庫。<br /> </td>
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
   <td>搜尋在日期屬性的指定範圍內建立的資源。 在「搜尋」面板中，您可以指定「開始」和「結束」日期。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>範圍文本（從）*</li>
     <li>範圍文本（至）*</li>
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
   <td>根據資源的大小篩選資源。</td>
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
   <td>根據檔案/mime類型搜尋資產。</td>
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
   <td>搜尋述詞以搜尋全文搜尋。 它與「jcr:contains」運算子映射。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>群組</td>
   <td>搜尋群組的述詞（僅用於前瞻分析述詞中）。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隱藏的篩選器</td>
   <td>屬性和值的篩選器，使用者看不到。</td>
   <td>
    <ul>
     <li>屬性名稱*</li>
     <li>屬性值*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>分析</td>
   <td>根據選取的前瞻分析參數進行搜尋。</td>
   <td>這是由多個謂語組成的複雜謂語：
    <ul>
     <li>群組</li>
     <li>範圍</li>
     <li>選項</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>集合成員</td>
   <td>搜尋屬於集合成員的資產</td>
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
   <td><p>選項是使用者建立的內容節點。</p> <p>如需詳細資訊，請參閱<a href="#addinganoptionspredicate">新增選項述詞</a> 。</p> </td>
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
   <td>根據頁面的狀態篩選頁面。</td>
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
   <td>根據特定路徑篩選。 您可以指定多個路徑作為選項。</td>
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
     <li>屬性名稱('path')</li>
     <li>屬性值(「/content/dam」)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>在指定的屬性上搜索。</td>
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
   <td>根據資源的平均評分搜索資源。<br /> </td>
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
   <td>使用滑桿功能擴充範圍述詞的通用搜尋述詞。 所搜尋屬性的值必須介於滑桿限制之間。</td>
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
     <li>菲爾德拉韋爾</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>顯示配對所有標記選項</li>
     <li>根標籤路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範本</td>
   <td>根據所選範本進行搜尋。</td>
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
   <td>根據翻譯狀態進行搜尋。</td>
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
>常見的搜尋述詞定義於：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>此資訊僅供參考，您不得對`/libs`進行變更。

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 謂詞設定{#predicate-settings}

根據述詞，選擇的設定可用於配置，包括：

* **欄位標籤**

   將顯示為可折疊標題或謂語欄位標籤的標籤。

* **說明**

   使用者的描述性詳細資訊。

* **預留位置**

   空文本或謂語的位置保持符，以防未輸入篩選文本。

* **屬性名稱**

   要搜尋的屬性。 它使用相對路徑，通配符`*/*/*`指定相對於`jcr:content`節點的屬性深度（每個星號表示一個節點級別）。

   如果只想在`jcr:content`節點上具有`x`屬性的資源的第一級子節點上搜索，請使用`*/jcr:content/x`

* **屬性深度**

   在資源內搜尋該屬性的最大深度。 因此，可以對資源和遞歸子項執行對該屬性的搜索，直到子項的級別等於指定深度為止。

* **屬性值**

   屬性值作為絕對字串或作為表達式語言；例如`cq:Page`或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文字**

   **日期範圍**&#x200B;謂語中範圍欄位的標籤。

* **選項路徑**

   用戶可以使用謂詞設定頁簽中的路徑瀏覽器選擇路徑。 選取&#x200B;**+**&#x200B;圖示後，系統會將選取項目新增至有效選項清單（視需要而移除的&#x200B;**-**&#x200B;圖示）。

   這些選項是用戶建立的內容節點，具有以下結構：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節**
點路徑與 
**選項路徑**，只有這在通用述詞欄位中，另一個是資產專屬的。

* **單選**
項如果選中，則選項將呈現為僅允許單個選擇的複選框。如果錯誤選取，則可取消選取核取方塊。

* **Publish和Live Copy屬性名稱**
 Sites特定述詞的發佈和Live Copy核取方塊標籤。

* &amp;ast;在&#x200B;**設定**&#x200B;標籤的欄位標籤上，表示欄位是必填欄位，若保留為空白，則會顯示錯誤訊息。

## 設定搜尋Forms {#configuring-your-search-forms}

### 建立/開啟自定義配置{#creating-opening-a-customized-configuration}

1. 導覽至&#x200B;**工具**、**一般**、**搜尋Forms**。

1. 選取您要自訂的設定。
1. 使用&#x200B;**Edit**&#x200B;圖示開啟要更新的配置。
1. 如果是新的自訂，您可能想要[新增謂詞欄位，並視需要定義設定](#add-edit-a-predicate-field-and-define-field-settings)。 如果現有自定義項，則可以選擇現有欄位並更新設定](#add-edit-a-predicate-field-and-define-field-settings)。[
1. 選擇&#x200B;**Done**&#x200B;以保存配置。 下次使用設定時，就會看到您的變更。

   >[!NOTE]
   >
   >自訂設定會（視情況）儲存在：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 添加/編輯謂詞欄位和定義欄位設定{#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義/更新其設定：

1. [開啟要更新的](#creating-opening-a-customized-configuration) 自訂設定。
1. 如果要添加新欄位，請開啟&#x200B;**Select Predicate**&#x200B;頁簽，並將所需的謂詞拖到所需位置。 例如，**日期範圍述詞**:

   ![新增述詞](assets/csf-add-predicate.png)

1. 取決於：

   * 正在添加新欄位：

      新增述詞後，**Settings**&#x200B;標籤將開啟並顯示可定義的屬性。

   * 要更新現有謂詞：

      選擇謂語欄位（在右側），然後開啟&#x200B;**Settings**&#x200B;標籤。
   例如，**日期範圍述詞**&#x200B;的設定：

   ![修改謂語](assets/csf-modify-predicate.png)

1. 視需要進行變更，並使用&#x200B;**Done**&#x200B;確認。 下次使用設定時，就會看到您的變更。

### 預覽搜索配置{#previewing-the-search-configuration}

1. 選取「預覽」圖示：

   ![預覽圖示](assets/csf-preview-icon.png)

1. 這樣，在適當控制台的「搜尋」欄中，搜尋表單就會顯示為（完全展開）。

   ![預覽表單](assets/csf-preview-form.png)

1. **** 關閉預覽以傳回並完成設定。

### 刪除謂詞欄位{#deleting-a-predicate-field}

1. [開啟要更新的](#creating-opening-a-customized-configuration) 自訂設定。
1. 選取謂語欄位（在右側），開啟&#x200B;**Settings**&#x200B;標籤，然後選取&#x200B;**Delete**&#x200B;圖示（左下）。

   ![刪除圖示](assets/csf-delete-icon.png)

1. 對話方塊會要求確認刪除動作。

1. 以&#x200B;**Done**&#x200B;確認此變更和任何其他變更。

### 刪除配置（恢復預設值）{#deleting-a-configuration-to-reinstate-the-default}

自訂設定後，這將覆寫預設值。 您可以刪除自訂設定，以重新設定預設設定。

>[!NOTE]
>
>您無法刪除預設配置。

從主控台刪除自訂設定：

1. 選擇所需的配置(例如&#x200B;**頁面編輯器（段落搜索）**)，然後在工具欄中選擇&#x200B;**刪除**&#x200B;表徵圖：

   ![還原預設值](assets/csf-restore-default.png)

1. 將刪除自定義配置並恢復預設配置（這由控制台中的掛鎖符號的再現指示）。

### 添加選項謂詞{#adding-options-predicates}

選項謂語（選項、選項屬性）可讓您設定要搜尋的項目。 它們通常用於直接在頁面下方搜尋內容；例如，頁面節點上的屬性。

以下範例（根據用來建立頁面的範本進行搜尋）說明了相關步驟：

1. 建立定義要搜索的屬性的節點。

   您需要一個根節點，其中包含使用者可使用的個別選項定義。

   個別選項的節點需要屬性：

   * `jcr:title`  — 要在搜尋邊欄中顯示的欄位標籤
   * `value`  — 要搜尋的屬性值

   ![謂詞定義](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
   >
   >這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   >
   >設定和其他變更的建議方法為：
   >
   >1. 在`/apps`下重新建立所需項，因為它存在於`/libs`中。 在此案例中，來源為：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在`/apps.`內進行任何更改


1. 開啟&#x200B;**搜尋Forms**&#x200B;主控台，並選取您要更新的設定。 例如， **網站管理員搜尋邊欄**。 然後選擇&#x200B;**Edit**。

1. 視設定而定，將&#x200B;**Options**&#x200B;或&#x200B;**Options屬性**&#x200B;新增至設定。
1. 更新欄位，尤其是：

   * **屬性名稱**

      在目標節點上指定要搜索的節點屬性。 例如：

      `jcr:content/cq:template`

   * **選項節點路徑**

      選取保留選項的路徑。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![選項謂語](assets/csf-options-predicate-02.png)

1. 選擇&#x200B;**Done**&#x200B;以保存配置。
1. 導覽至適當的主控台（在此範例中，為&#x200B;**Sites**），然後開啟&#x200B;**Search - Filters**&#x200B;邊欄。 新定義的搜尋表單以及各種選項將會顯示。 選擇查看搜索結果所需的選項。

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
   <td>對<code>/apps </code>節點讀取、寫入權限。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><code>/apps</code>節點的讀、寫、刪除權限</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td><code>/var/dam/content</code>節點的讀、寫、刪除權限。<br /> 讀取，寫入節點的 <code>/apps</code> 權限。</td>
  </tr>
 </tbody>
</table>
