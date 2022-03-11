---
title: 設定搜尋表單
description: 正在配置搜索Forms以查找Adobe Experience Manager as a Cloud Service。
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 16%

---

# 設定搜尋表單 {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service帶著 [搜索](/help/sites-cloud/authoring/getting-started/search.md) 機制。

與此結合，還有一組預定義選項可幫助您篩選內容。 這些保留預定義小平面，如 **修改日期**。 **發佈狀態**&#x200B;或 **Livecopy狀態** 幫助您快速細化到所需資源。

![搜索和篩選使用](assets/csf-usage.png)

這些組合旨在幫助您快速輕鬆地從以下位置查找內容：

* [搜尋與篩選](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [軌道選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* 這樣 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) （編輯頁面時）

>[!NOTE]
>
>您可以配置基礎 [內容搜索和索引](/help/operations/indexing.md) 服務。

使用 **搜索Forms**，您可以根據您的特定需求定制和擴展這些面板。

的 **搜索Forms** 提供現成選擇 [謂語](#predicates-and-their-settings) 你可以組合和定義。 的 [配置這些表單的對話框](#configuring-your-search-forms) 可通過以下方式訪問：

* **工具**
   * **一般**
      * **搜尋表單**

## 預設Forms {#default-forms}

當您首次訪問 **搜索Forms** 控制台，您可以看到所有配置都有掛鎖符號。 這表示相應的配置是預設（現成）配置 — 無法刪除。 自定義並保存後，鎖將消失。 它會在你 [刪除自定義配置](#deleting-a-configuration-to-reinstate-the-default)，在此情況下，將恢復預設值（和掛鎖指示器）。

![配置搜索表單概述](assets/csf-overview.png)

The default configurations (listed alphabetically) available are:

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
>有關與資產相關的搜索表單的詳細資訊，請參閱 [資產 — 搜索小面](/help/assets/search-facets.md)


## Predicates and Their Settings {#predicates-and-their-settings}

### 謂語 {#predicates}

以下謂詞可用，取決於配置：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>目的</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析</td>
   <td>顯示分析支援的資料時，在「站點」瀏覽器中搜索/篩選功能。 Analytics search filters load up to match the mapped customized analytics columns.</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>審批狀態</td>
   <td>根據批准狀態搜索。</td>
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
   <td>Search according to author.</td>
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
   <td>搜索由特定用戶簽出的資產。</td>
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
   <td>搜索具有特定簽出狀態的資產。</td>
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
   <td>允許作者搜索/篩選具有特定元件的頁面。 例如，影像庫。<br /> </td>
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
   <td>搜索在日期屬性的指定範圍內建立的資源。 在「搜索」面板中，可以指定「開始」和「結束日期」。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>Range text (From)*</li>
     <li>範圍文本（至）*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期狀態</td>
   <td>Search resources based on expiry status.</td>
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
   <td>根據檔案/mime類型搜索資產。</td>
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
   <td>Search predicate for full-text searches. It is mapped with the ´jcr:contains´ operator.</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>群組</td>
   <td>Search predicate for group (only used within the Insights Predicate).</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隱藏的篩選器</td>
   <td>A filter on property and value, not visible to the user.</td>
   <td>
    <ul>
     <li>屬性名稱*</li>
     <li>屬性值*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>分析</td>
   <td>根據選擇的Insights參數進行搜索。</td>
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
   <td>搜索屬於集合成員的資產</td>
   <td>
    <ul>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>多值屬性</td>
   <td>搜索指定屬性的多個值。</td>
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
   <td><p>這些選項是用戶建立的內容節點。</p> <p>請參閱 <a href="#addinganoptionspredicate">添加選項謂詞</a> 的子菜單。</p> </td>
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
   <td>Options Property</td>
   <td>Search on one, or more, properties of the option.</td>
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
   <td>根據特定路徑進行篩選。 可以指定多個路徑作為選項。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>添加搜索路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑瀏覽器</td>
   <td>Provide a path browser to search under a predefined root path.</td>
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
   <td>路徑上的篩選器，用戶不可見。</td>
   <td>
    <ul>
     <li>屬性名稱('path')</li>
     <li>屬性值(「/content/dam」)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>搜索指定的屬性。</td>
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
   <td>搜索位於指定範圍內的資源。 在「搜索」面板中，可以指定範圍的最小值和最大值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>評等</td>
   <td>根據資源的平均評級搜索資源。<br /> </td>
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
   <td>根據建立資源的相對日期篩選資源。 比如，一週前，一個月前。</td>
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
   <td>使用滑塊功能擴展範圍謂詞的通用搜索謂詞。 搜索的屬性的值必須介於滑塊限制之間。</td>
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
   <td>根據審批和簽出狀態進行搜索。</td>
   <td>這是由多個謂語組成的複雜謂語：
    <ul>
     <li>審批狀態</li>
     <li>簽出狀態</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>標記</td>
   <td>基於標籤進行搜索。</td>
   <td>
    <ul>
     <li>菲爾德·拉韋爾</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>顯示配對所有標記選項</li>
     <li>根標籤路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範本</td>
   <td>Search according to the selected template.</td>
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
>常用搜索謂語在中定義：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>此資訊僅供參考，您不得更改 `/libs`。

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 謂詞設定 {#predicate-settings}

根據謂語，可以選擇以下設定進行配置：

* **欄位標籤**

   The label that will appear as the collapsible header or as the field label of the predicate.

* **說明**

   用戶的描述性詳細資訊。

* **預留位置**

   空文本或謂語的佔位符（如果未輸入過濾文本）。

* **屬性名稱**

   要搜索的屬性。 它使用相對路徑和通配符 `*/*/*` 指定屬性相對於 `jcr:content` 節點（每個星號表示一個節點級別）。

   如果您只想在具有 `x` 屬性 `jcr:content` 節點使用 `*/jcr:content/x`

* **屬性深度**

   在資源中搜索該屬性的最大深度。 因此，可以對資源和遞歸子項執行對該屬性的搜索，直到子項的級別等於指定的深度。

* **屬性值**

   屬性值作為絕對字串或表達式語言；比如說， `cq:Page` 或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文本**

   中範圍欄位的標籤 **日期範圍** 謂語。

* **選項路徑**

   用戶可以使用謂詞設定頁籤中的「路徑瀏覽器」選擇路徑。 選擇 **+** 表徵圖用於將所選內容添加到有效選項清單( **-** 表徵圖（如果需要）。

   這些選項是用戶建立的內容節點，具有以下結構：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節點路徑**
與 
**選項路徑**，僅此欄位位於公共謂語欄位中，另一個欄位特定於資產。

* **單選**
如果選中，則這些選項將呈現為僅允許單個選擇的複選框。 如果錯誤選中，則可取消選中複選框。

* **發佈和即時複製屬性名稱**
「站點」特定謂詞的發佈和即時複製複選框的標籤。

* &amp;ast;的 **設定** 頁籤表示欄位是必填的，如果留空，則會顯示錯誤消息。

## 配置搜索Forms {#configuring-your-search-forms}

### 建立/開啟自定義配置 {#creating-opening-a-customized-configuration}

1. 導航到 **工具**。 **常規**。 **搜索Forms**。

1. 選擇要自定義的配置。
1. 使用 **編輯** 表徵圖以開啟要更新的配置。
1. 如果您想要新定制 [添加新謂詞欄位並定義設定](#add-edit-a-predicate-field-and-define-field-settings) 按需要。 如果是現有自定義項，則可以選擇現有欄位 [更新設定](#add-edit-a-predicate-field-and-define-field-settings)。
1. 選擇 **完成** 的子菜單。 下次使用配置時，可以看到您所做的更改。

   >[!NOTE]
   >
   >定制配置儲存（如適用）在以下位置：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 添加/編輯謂詞欄位和定義欄位設定 {#add-edit-a-predicate-field-and-define-field-settings}

您可以添加或編輯欄位，並定義/更新其設定：

1. [開啟自定義配置](#creating-opening-a-customized-configuration) 的子菜單。
1. 如果要添加新欄位，請開啟 **選擇謂詞** 頁籤，並將所需謂詞拖到所需位置。 例如， **日期範圍謂詞**:

   ![添加謂語](assets/csf-add-predicate.png)

1. 取決於：

   * 您正在添加新欄位：

      添加謂詞後， **設定** 頁籤，並顯示可定義的屬性。

   * 要更新現有謂詞：

      選擇謂詞欄位（在右側），然後開啟 **設定** 頁籤。
   For example, the settings for the **Date Range Predicate**:

   ![修改謂詞](assets/csf-modify-predicate.png)

1. 根據需要進行更改並確認 **完成**。 下次使用配置時，可以看到您所做的更改。

### 預覽搜索配置 {#previewing-the-search-configuration}

1. 選擇「預覽」表徵圖：

   ![預覽表徵圖](assets/csf-preview-icon.png)

1. 這將顯示搜索表單，如相應控制台的「搜索」列中將顯示（完全展開）的搜索表單。

   ![預覽](assets/csf-preview-form.png)

1. **關閉** 返回並完成配置的預覽。

### Deleting a Predicate Field {#deleting-a-predicate-field}

1. [開啟自定義配置](#creating-opening-a-customized-configuration) 的子菜單。
1. 選擇謂詞欄位（在右側），開啟 **設定** ，然後選擇 **刪除** 表徵圖（左下）。

   ![刪除表徵圖](assets/csf-delete-icon.png)

1. 對話框將請求確認刪除操作。

1. 確認此更改和任何其他更改 **完成**。

### Deleting a Configuration (to Reinstate the Default) {#deleting-a-configuration-to-reinstate-the-default}

Once you have customized a configuration this will override the defaults. 您可以通過刪除自定義配置來重新聲明預設配置。

>[!NOTE]
>
>無法刪除預設配置。

Deleting a customized configuration is done from the console:

1. Select the required configuration (for example, **Page Editor (Paragraphs search)**) and then the **Delete** icon in the toolbar:

   ![恢復預設](assets/csf-restore-default.png)

1. 將刪除自定義配置並恢復預設配置（這由掛鎖符號在控制台中的再現指示）。

### 添加選項謂詞 {#adding-options-predicates}

Option predicates (Options, Options Property) allow you to configure an item to be searched for. 通常用來在頁面的正下面搜索，例如，頁節點上的屬性。

下面的示例（根據用於建立頁面的模板進行搜索）說明了涉及的步驟：

1. 建立定義要搜索的屬性的節點。

   您需要一個根節點，該根節點保存各個選項的定義，以便用戶可用。

   各個選項的節點需要以下屬性：

   * `jcr:title`  — 要在搜索欄中顯示的欄位標籤
   * `value`  — 要搜索的屬性值

   ![謂詞定義](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >你 ***必須*** 沒有改變 `/libs` 路徑。
   >
   >This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
   >
   >建議的配置和其他更改方法是：
   >
   >1. 重新建立所需項，因為它存在於 `/libs`下 `/apps`。 在本例中，來自：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在 `/apps.`


1. 開啟 **搜索Forms** 並選擇要更新的配置。 比如說， **站點管理搜索欄**。 然後選擇 **編輯**。

1. 根據配置，添加 **選項** 或 **選項屬性** 到配置。
1. 更新欄位，特別是：

   * **屬性名稱**

      在目標節點上指定要搜索的節點屬性。 例如：

      `jcr:content/cq:template`

   * **選項節點路徑**

      選擇保留選項的路徑。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![選項謂語](assets/csf-options-predicate-02.png)

1. 選擇 **完成** 保存配置。
1. 導航到相應的控制台(在本示例中， **站點**)並開啟 **搜索 — 篩選器** 鐵軌。 新定義的搜索表單以及各種選項將可見。 選擇所需選項以查看搜索結果。

   ![選項](assets/csf-options-usage.png)


## 使用者權限 {#user-permissions}

下表列出了對搜索表單執行編輯、刪除和預覽操作所需的權限。

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
   <td>讀取、寫入 <code>/apps </code>的下界。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td>讀取、寫入、刪除 <code>/apps</code> 節點</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td>Read, Write, Delete permissions on the <code>/var/dam/content</code> node.<br /> 讀取、寫入 <code>/apps</code> 的下界。</td>
  </tr>
 </tbody>
</table>
