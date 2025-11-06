---
title: 設定搜尋表單
description: 設定Adobe Experience Manager as a Cloud Service的搜尋Forms 。
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 9%

---

# 設定搜尋表單 {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service提供強大的[搜尋](/help/sites-cloud/authoring/search.md)機制。

除此之外，還有一組預先定義的選項，可協助您篩選內容。 這些保留預先定義的Facet，例如&#x200B;**修改日期**、**發佈狀態**&#x200B;或&#x200B;**即時副本狀態**，可協助您快速向下展開至您需要的資源。

![搜尋和篩選使用方式](assets/csf-usage.png)

這些目標可協助您從以下位置快速輕鬆地找到您的內容：

* [搜尋和篩選](/help/sites-cloud/authoring/search.md#search-and-filter)
* [邊欄選擇器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)
* [Assets瀏覽器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) （編輯頁面時）

>[!NOTE]
>
>您可以設定基礎[內容搜尋和索引](/help/operations/indexing.md)服務。

使用&#x200B;**搜尋Forms**，您可以根據特定需求自訂及擴充這些面板。

**搜尋Forms**&#x200B;提供您可以組合和定義的[述詞](#predicates-and-their-settings)的現成選擇。 設定這些表單[的](#configuring-your-search-forms)對話方塊可透過下列方式存取：

* **工具**
   * **一般**
      * **搜尋Forms**

## 預設Forms {#default-forms}

第一次存取&#x200B;**搜尋Forms**&#x200B;主控台時，您可以看到所有設定都有掛鎖符號。 這表示對應的設定是預設（現成）設定 — 無法刪除。 一旦您自訂並儲存設定，鎖定就會消失。 當您[刪除自訂的組態](#deleting-a-configuration-to-reinstate-the-default)時，它將會重新出現，在此情況下，預設值（和掛鎖指示器）將會復原。

![設定搜尋表單概觀](assets/csf-overview.png)

可用的預設設定（依字母順序列出）為：

* **Assets管理搜尋邊欄**
* **頁面編輯器（檔案搜尋）**
* **頁面編輯器（體驗片段搜尋）**
* **頁面編輯器（影像搜尋）**
* **頁面編輯器（手稿搜尋）**
* **頁面編輯器（頁面搜尋）**
* **頁面編輯器（段落搜尋）**
* **頁面編輯器（產品搜尋）**
* **頁面編輯器（Scene7搜尋）**
* **頁面編輯器（視訊搜尋）**
* **專案管理搜尋邊欄**
* **專案翻譯搜尋邊欄**
* **網站管理搜尋邊欄**
* **程式碼片段管理搜尋邊欄**
* **Stock管理搜尋邊欄**
* **內容片段模型搜尋邊欄**
* **專案管理搜尋邊欄**
* **專案翻譯搜尋邊欄**

>[!NOTE]
>
>如需資產相關搜尋表單的詳細資訊，請參閱[Assets — 搜尋Facet](/help/assets/search-facets.md)。


## 述詞及其設定 {#predicates-and-their-settings}

### 述詞 {#predicates}

視設定而定，以下述詞可供使用：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>用途</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析</td>
   <td>顯示Analytics支援的資料時，提供Sites瀏覽器中的搜尋/篩選功能。 Analytics搜尋篩選器會載入以符合對應的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>核准狀態</td>
   <td>根據核准狀態搜尋。</td>
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
   <td>搜尋具有特定簽出狀態的資產。</td>
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
   <td>允許作者搜尋/篩選上面有特定元件的頁面。 例如，影像庫。<br /> </td>
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
     <li>範圍文字（從）*</li>
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
   <td>根據檔案/MIME型別搜尋資產。</td>
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
   <td>全文檢索搜尋的搜尋述詞。 對應著jcr：contains運運算元。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>群組</td>
   <td>群組的搜尋述詞（僅用於見解述詞內）。</td>
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
   <td>Insights</td>
   <td>根據選定的見解引數進行搜尋。</td>
   <td>這是一個由多個述片語成的複雜述詞：
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
     <li>輸入分隔符號</li>
     <li>忽略大小寫</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>選項</td>
   <td><p>選項是使用者建立的內容節點。</p> <p>如需詳細資訊，請參閱<a href="#addinganoptionspredicate">新增選項述詞</a>。</p> </td>
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
   <td>根據頁面狀態來篩選頁面。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>發佈屬性名稱*</li>
     <li>鎖定的頁面屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>根據特定路徑篩選。 您可以將多個路徑指定為選項。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>新增搜尋路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑瀏覽器</td>
   <td>提供路徑瀏覽器，在預先定義的根路徑下搜尋。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>根路徑</li>
     <li>說明</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>路徑已隱藏</td>
   <td>路徑上的篩選器，使用者看不到。</td>
   <td>
    <ul>
     <li>屬性名稱(「path」)</li>
     <li>屬性值('/content/dam')</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>搜尋指定的屬性。</td>
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
   <td>根據資源的發佈狀態來篩選資源。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍</td>
   <td>搜尋指定範圍內的資源。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>評等</td>
   <td>根據資源的平均評等搜尋資源。<br /> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>相對時間</td>
   <td>根據資源的相對建立日期篩選資源。 例如1週前、1個月前。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>相對時間</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>滑桿範圍</td>
   <td>使用滑桿功能擴充範圍述詞的常見搜尋述詞。 搜尋的屬性值必須介於滑桿限制之間。</td>
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
   <td>根據核准和簽出狀態進行搜尋。</td>
   <td>這是一個由多個述片語成的複雜述詞：
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
     <li>欄位層級</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>顯示配對所有標記選項</li>
     <li>根標籤路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範本</td>
   <td>根據選取的範本搜尋。</td>
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
>此資訊僅供參考，您不得變更`/libs`。

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 述詞設定 {#predicate-settings}

視述詞而定，有多種設定可供設定，包括：

* **欄位標籤**

  將顯示為可摺疊標題或述詞欄位標籤的標籤。

* **說明**

  使用者的描述性詳細資料。

* **預留位置**

  空白文字或述詞的預留位置（若未輸入篩選文字）。

* **屬性名稱**

  要搜尋的屬性。 它使用相對路徑，萬用字元`*/*/*`指定相對於`jcr:content`節點的屬性深度（每個星號代表一個節點層級）。

  如果您只想在`x`節點上具有`jcr:content`屬性的資源之第一層子節點上搜尋，請使用`*/jcr:content/x`

* **屬性深度**

  在資源中搜尋該屬性的最大深度。 因此，可針對資源及遞回子項執行該屬性的搜尋，直到子項的層級等於指定的深度為止。

* **屬性值**

  屬性值做為絕對字串或做為運算式語言；例如，`cq:Page`或

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文字**

  **日期範圍**&#x200B;述詞中範圍欄位的標籤。

* **選項路徑**

  使用者可以使用述詞設定索引標籤中的路徑瀏覽器來選取路徑。 選取&#x200B;**+**&#x200B;圖示之後，會使用將選取專案新增至有效選項清單（如有必要，則會移除&#x200B;**-**&#x200B;圖示）。

  選項是使用者建立的內容節點，結構如下：

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節點路徑**
實際上與**選項路徑**&#x200B;相同，只有這個在通用述詞欄位中，其他則專用於資產。

* **單選**
如果勾選，選項會呈現為僅允許單一選取的核取方塊。 如果錯誤地選取了，則可取消選取核取方塊。

* **發佈和即時副本屬性名稱**
網站特定述詞的發佈和即時副本核取方塊的標籤。

* **設定**&#x200B;標籤中欄位標籤上的&amp;amp；ast；表示欄位是必填欄位，如果留白，將會出現錯誤訊息。

## 設定搜尋Forms {#configuring-your-search-forms}

### 建立/開啟自訂組態 {#creating-opening-a-customized-configuration}

1. 導覽至&#x200B;**工具**、**一般**、**搜尋Forms**。

1. 選取您要自訂的設定。
1. 使用&#x200B;**編輯**&#x200B;圖示開啟設定以進行更新。
1. 如果新的自訂，您可能要[新增述詞欄位，並視需要定義設定](#add-edit-a-predicate-field-and-define-field-settings)。 如果已有自訂，您可以選取現有欄位並[更新設定](#add-edit-a-predicate-field-and-define-field-settings)。
1. 選取&#x200B;**完成**&#x200B;以儲存組態。 下次使用設定時即可看到您的變更。

   >[!NOTE]
   >
   >自訂組態會視情況儲存在：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### 新增/編輯述詞欄位和定義欄位設定 {#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義/更新其設定：

1. [開啟自訂的設定](#creating-opening-a-customized-configuration)以進行更新。
1. 如果您想要新增欄位，請開啟&#x200B;**選取述詞**&#x200B;索引標籤，並將必要的述詞拖曳到必要的位置。 例如，**日期範圍述詞**：

   ![新增述詞](assets/csf-add-predicate.png)

1. 視以下專案而定：

   * 您正在新增欄位：

     新增述詞之後，**設定**&#x200B;索引標籤會開啟，並顯示可定義的屬性。

   * 您要更新現有的述詞：

     選取述詞欄位（在右側），然後開啟&#x200B;**設定**&#x200B;標籤。

   例如，**日期範圍述詞**&#x200B;的設定：

   ![修改述詞](assets/csf-modify-predicate.png)

1. 視需要進行變更，並透過&#x200B;**完成**&#x200B;確認。 下次使用設定時即可看到您的變更。

### 預覽搜尋組態 {#previewing-the-search-configuration}

1. 選取預覽圖示：

   ![預覽圖示](assets/csf-preview-icon.png)

1. 顯示搜尋表單（完全展開）於適當主控台的「搜尋」欄中的方式。

   ![預覽表單](assets/csf-preview-form.png)

1. **關閉**&#x200B;預覽以傳回並完成設定。

### 刪除述詞欄位 {#deleting-a-predicate-field}

1. [開啟自訂的設定](#creating-opening-a-customized-configuration)以進行更新。
1. 選取述詞欄位（在右側），開啟&#x200B;**設定**&#x200B;標籤，然後選取&#x200B;**刪除**&#x200B;圖示（左下方）。

   ![刪除圖示](assets/csf-delete-icon.png)

1. 對話方塊會要求確認刪除動作。

1. 透過&#x200B;**完成**&#x200B;確認此變更及任何其他變更。

### 刪除組態（恢復預設值） {#deleting-a-configuration-to-reinstate-the-default}

一旦自訂了設定，就會覆寫預設值。 您可以刪除自訂的組態，以重新指定預設組態。

>[!NOTE]
>
>您無法刪除預設組態。

從主控台刪除自訂設定完成：

1. 選取必要的設定(例如，**頁面編輯器（段落搜尋）**)，然後選取工具列中的&#x200B;**刪除**&#x200B;圖示：

   ![還原預設值](assets/csf-restore-default.png)

1. 自訂的組態會遭到刪除，而預設值會恢復（由主控台中掛鎖符號的重新顯示所指示）。

### 新增選項述詞 {#adding-options-predicates}

選項述詞（選項、選項屬性）可讓您設定要搜尋的專案。 它們通常用於直接在頁面下方搜尋某專案，例如頁面節點上的屬性。

以下範例（根據用來建立頁面的範本進行搜尋）說明了相關步驟：

1. 建立定義要搜尋之屬性的節點。

   您需要一個根節點，其中包含使用者可用的個別選項定義。

   個別選項的節點需要屬性：

   * `jcr:title` — 要在搜尋邊欄中顯示的欄位標籤
   * `value` — 要搜尋的屬性值

   ![述詞定義](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何專案。
   >
   >這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，這些內容很可能會被覆寫）。
   >
   >設定和其他變更的建議方法是：
   >
   >1. 重新建立必要專案，因為它存在於`/libs`中的`/apps`下。 在此案例中，來自：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在`/apps.`中進行任何變更

1. 開啟&#x200B;**搜尋Forms**&#x200B;主控台，並選取您要更新的設定。 例如，**網站管理員搜尋邊欄**。 然後選取&#x200B;**編輯**。

1. 視組態而定，將&#x200B;**Options**&#x200B;或&#x200B;**Options屬性**&#x200B;新增至組態。
1. 更新欄位，特別是：

   * **屬性名稱**

     指定要在目標節點上搜尋的節點屬性。 例如：

     `jcr:content/cq:template`

   * **選項節點路徑**

     選取保留選項的路徑。 例如：

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![選項述詞](assets/csf-options-predicate-02.png)

1. 選取&#x200B;**完成**&#x200B;以儲存您的設定。
1. 導覽至適當的主控台（在此範例中為&#x200B;**Sites**）並開啟&#x200B;**搜尋 — 篩選器**&#x200B;邊欄。 會顯示新定義的搜尋表單以及各種選項。 選取必要選項以檢視搜尋結果。

   ![個使用中的選項](assets/csf-options-usage.png)


## 使用者權限 {#user-permissions}

下表列出對搜尋表單執行編輯、刪除和預覽動作所需的許可權。

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
   <td><code>/apps </code>節點的讀取、寫入許可權。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><code>/apps</code>節點的讀取、寫入、刪除許可權</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td><code>/var/dam/content</code>節點的讀取、寫入、刪除許可權。<br />節點上的<code>/apps</code>讀取、寫入許可權。</td>
  </tr>
 </tbody>
</table>
