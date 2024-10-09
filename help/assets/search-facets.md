---
title: 搜尋Facet。
description: 本文說明如何在Experience Manager中建立、修改和使用搜尋Facet。
feature: Metadata
role: Admin, User
exl-id: f994c1bf-3f9d-4cb2-88f4-72a9ad6fa999
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '2523'
ht-degree: 19%

---

# 搜尋 Facet {#search-facets}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/search-facets.html) |
| AEM as a Cloud Service  | 本文章 |

Adobe Experience Manager Assets的企業範圍部署可儲存許多資產。 有時候，如果您只使用Experience Manager的一般搜尋功能，尋找正確的資產可能會很困難且耗時。

使用「篩選器」面板中的搜尋Facet為您的搜尋體驗新增更多精細度，並讓搜尋功能更有效率且更通用。 搜尋Facet會新增多個維度（述詞），讓您執行更複雜的搜尋。 「篩選器」面板包含幾個標準Facet。 您也可以新增自訂搜尋多面向。

總而言之，搜尋Facet可讓您以多種方式搜尋資產，而非使用單一、預先決定的分類順序。 您可以輕鬆向下展開至所需的詳細資訊層級，以更集中地搜尋。

例如，如果您要尋找影像，您可以選擇您要點陣圖或向量影像。 您可以指定影像的MIME型別，進一步縮小搜尋範圍。 同樣地，在搜尋檔案時，您可以指定格式，例如PDF或MS Word。

## 新增述詞 {#adding-a-predicate}

顯示在「篩選器」面板中的搜尋Facet是使用述詞定義在基礎搜尋表單中。 若要顯示更多或不同的Facet，您可以將述詞新增至預設表單，或使用包含您所選Facet的自訂表單。

若要進行全文檢索搜尋，請將`Fulltext`述詞新增至表單。 使用屬性述詞來搜尋符合您指定之單一屬性的資產。 使用「選項」述詞來搜尋符合特定屬性的一個或多個值的資產。 新增日期範圍述詞，以搜尋在指定日期範圍內建立的資產。

1. 按一下Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 從「搜尋Forms」頁面中，選取&#x200B;**[!UICONTROL Assets管理搜尋邊欄]**，然後選取&#x200B;**編輯** ![aemassets_edit](assets/aemassets_edit.png)。

   ![尋找並選取Assets管理搜尋邊欄](assets/assets_admin_searchrail.png)

1. 在「編輯搜尋Forms」頁面中，將述詞從&#x200B;**[!UICONTROL 選取述詞]**&#x200B;標籤拖曳至主窗格。 例如，拖曳&#x200B;**[!UICONTROL 屬性述詞]**。

   ![選取並移動述詞以自訂搜尋篩選器](assets/drag_predicate.png)

   *圖：選取並移動述詞以自訂搜尋篩選器。*

1. 在「設定」標籤中，輸入欄位標籤、預留位置文字和述詞說明。 為您要與述詞關聯的中繼資料屬性指定有效的名稱。 「設定」標籤中的標題標籤可識別所選述詞的型別。

   ![使用[設定]索引標籤提供述詞的必要選項](assets/settings.png)

   *圖：使用[設定]索引標籤提供述詞的必要選項。*

1. 在「屬 **[!UICONTROL 性名稱]** 」欄位中，指定您要與謂語關聯的中繼資料屬性的有效名稱。它是根據其執行搜索的名稱。例如，輸入`jcr:content/metadata/dc:description`或`./jcr:content/metadata/dc:description`。 您也可以從選取對話方塊中選取現有節點。

   ![在屬性名稱欄位中將中繼資料屬性與述詞建立關聯](assets/property_settings.png)

   *圖：將中繼資料屬性與[屬性名稱]欄位中的述詞建立關聯。*

1. 按一下&#x200B;**[!UICONTROL 預覽]** ![預覽](assets/preview.png)，在您新增述詞之後產生「篩選器」面板的預覽。
1. 在預覽模式中檢閱述詞的版面。

   ![在提交變更之前先預覽搜尋表單](assets/preview-1.png)

   在提交變更之前預覽搜尋表單

1. 若要關閉預覽，請按一下預覽右上角的&#x200B;**[!UICONTROL 關閉]** ![關閉](assets/do-not-localize/close_icon.png)。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存設定。
1. 導覽至Assets使用者介面中的「搜尋」面板。 屬性述詞會新增至面板。
1. 在文字方塊中輸入要搜尋之資產的說明。 例如，輸入「Adobe」。 執行搜尋時，說明符合「Adobe」的資產會列在搜尋結果中。

## 新增選項述詞 {#adding-an-options-predicate}

選項述詞可讓您在「篩選器」面板中新增多個搜尋選項。 您可以在「篩選器」面板中選取這些選項中的一或多個來搜尋資產。 例如，若要根據檔案型別搜尋資產，請在搜尋表單中設定選項，例如「影像」、「多媒體」、「檔案」和「封存」。 設定這些選項後，當您在「濾鏡」面板中選取「影像」選項時，系統會對GIF、JPEG、PNG等型別的資產執行搜尋。

若要將選項對應至個別屬性，請建立選項的節點結構，並在Options述詞的Property Name屬性中提供父節點的路徑。 父節點應屬於型別`sling`： `OrderedFolder`。 選項應屬於型別`nt:unstructured`。 選項節點應設定屬性`jcr:title`和`value`。

`jcr:title`屬性是顯示在「篩選器」面板上之選項的使用者易記名稱。 `value`欄位用於查詢中，以符合指定的屬性。

當您選取選項時，會根據選項節點及其子節點（如果有的話）的`value`屬性來執行搜尋。 系統會周遊選項節點下的整個樹狀結構，並使用OR運算來結合每個子節點的`value`屬性，以形成搜尋查詢。

例如，如果您為檔案類型選取「影像」，則會使用OR運算結合屬性來建立資 `value` 產的搜尋查詢。例如，通過組合影像/jpeg *、* image/gif *、* png影像、影像 */jpeg影像、以及使用OR操作對Tiff屬性進行搜索的Joff影像*****`jcr:content/metadata/dc:format` /Tiff影像的匹配結果來構建影像搜索查詢。

檔案型別的Value屬性（如CRXDE中所見）可用來讓搜尋查詢運作

您不必在CRX儲存庫中手動建立選項的節點結構，而是可以透過指定對應的索引鍵值配對，在JSON檔案中定義選項。在「屬性名稱」欄位中指定JSON檔 **[!UICONTROL 案的路徑]** 。例如，您可以定義鍵值配對、 `image/bmp`、 `image/gif``image/jpeg`、和 `image/png` 並指定其值，如下列範例JSON檔案中所示。在「屬 **[!UICONTROL 性名稱]** 」欄位中，您可以指定此檔案的CRX路徑。

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

如果要使用現有的節點，請使用選取對話方塊來指定它。

>[!NOTE]
>
>Options述詞是包含屬性述詞的自訂包裝函式，可示範所描述的行為。 目前沒有可用的REST端點可原生支援此功能。

1. 選取Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具>一般>搜尋Forms]**。
1. 從&#x200B;**[!UICONTROL 搜尋Forms]**&#x200B;頁面，選取&#x200B;**[!UICONTROL Assets管理搜尋邊欄]**，然後選取「編輯」圖示。
1. 在「編 **[!UICONTROL 輯搜索表單]** 」頁中，將「選 **[!UICONTROL 項謂詞」從]** 「選擇謂詞 **** 」頁籤拖到主窗格。
1. 在「設 **[!UICONTROL 定]** 」標籤中，輸入屬性的標籤和名稱。例如，若要根據資產的格式來搜尋資產，請為標籤指定好記的名稱，例如&#x200B;**[!UICONTROL 檔案型別]**。 指定在屬性欄位中執行搜尋時所依據的屬性，例如`jcr:content/metadata/dc:format.`
1. 執行下列任一項作業：

   * 在&#x200B;**[!UICONTROL 屬性名稱]**&#x200B;欄位中，提及JSON檔案的路徑，您可在此定義選項的節點，並指定對應的索引鍵值配對。
   * 選取「選項」欄位旁的![Assets新增圖示](assets/do-not-localize/aem_assets_add_icon.png)，以指定您要在「篩選器」面板中提供的選項之顯示文字和值。 若要新增其他選項，請選取![Assets新增圖示](assets/do-not-localize/aem_assets_add_icon.png)並重複此步驟。

1. 確保清 **[!UICONTROL 除「單選]** 」，讓使用者一次為檔案類型選取多個選項 (例如影像、檔案、多媒體和封存)。如果您選 **[!UICONTROL 取「單選]**」，使用者一次只能為檔案類型選取一個選項。

   ![選項述詞中的可用欄位](assets/options_predicate.png)

   選項述詞中的可用欄位

1. 在&#x200B;**描述**&#x200B;欄位中輸入選擇性描述，然後按一下&#x200B;**[!UICONTROL 完成]**。
1. 導覽至「搜尋」面板。 選項述詞已新增至&#x200B;**搜尋**&#x200B;面板。 **[!UICONTROL 檔案型別]**&#x200B;的選項會顯示為核取方塊。

## 新增多值屬性述詞 {#adding-a-multi-value-property-predicate}

`Multi Value Property`述詞可讓您搜尋多個值的資產。 假設您在[!DNL Assets]中有多個產品的影像，且每個影像的中繼資料都包含與產品相關聯的SKU編號。 您可以使用此述詞來根據多個SKU編號搜尋產品影像。

1. 按一下Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 在「搜尋Forms」頁面上，選取「**[!UICONTROL Assets管理搜尋邊欄」]**，再選取「**編輯**」![aemassets_edit](assets/aemassets_edit.png)。
1. 在「編輯搜索表單」頁中，將「 **[!UICONTROL Multi Value Property Predicate]** 」從「 **[!UICONTROL Select Predicate]** 」頁籤拖動到主窗格。
1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，輸入述詞的標籤及預留位置文字。 指定在屬性欄位中執行搜尋時所依據的屬性名稱，例如`jcr:content/metadata/dc:value`。 您也可以使用選取對話方塊來選取節點。
1. 請確定已 **[!UICONTROL 選取「分隔字元]** 」支援。在「輸入 **[!UICONTROL 分隔字元]** 」欄位中，指定分隔字元以分隔個別值。依預設，逗號會指定為分隔字元。您可以指定不同的分隔字元。
1. 在&#x200B;**描述**&#x200B;欄位中輸入選擇性描述，然後選取&#x200B;**[!UICONTROL 完成]**。
1. 導覽至「資產」使用者介面中的「篩選」面板。The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 在「多值」欄位中指定多個值（以分隔符號分隔），然後執行搜尋。 述詞會針對您指定的值擷取完全相符的文字。

## 新增標籤述詞 {#adding-a-tags-predicate}

`Tags`述詞可讓您對資產執行標籤式搜尋。 根據預設，[!DNL Assets]會根據您指定的標籤，搜尋符合一或多個標籤的資產。 換言之，搜尋查詢會使用指定的標籤執行OR操作。 不過，您可以使用符合所有標籤選項來搜尋包含您所指定之所有標籤的資產。

1. 按一下Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 從「搜尋Forms」頁面中，選取&#x200B;**[!UICONTROL Assets管理搜尋邊欄]**，然後選取&#x200B;**編輯** ![aemassets_edit](assets/aemassets_edit.png)。
1. 在「編輯搜尋表單」頁中，將&#x200B;**[!UICONTROL 標籤述詞]**&#x200B;從「選擇述詞」頁簽拖到主窗格。
1. 在「設定」標籤中，輸入述詞的預留位置文字。 指定在屬性欄位中執行搜尋時所依據的屬性名稱，例如`jcr:content/metadata/cq:tags`。 或者，您可以從選取對話方塊中選取CRXDE中的節點。
1. 設定此述詞的根標籤路徑屬性，以填入標籤清單中的各種標籤。
1. 選取 **[!UICONTROL 「顯示符合所有標籤」選項]** ，以搜尋包含您所指定之所有標籤的資產。

   ![標籤述詞的一般設定](assets/tags_predicate.png)

1. 在&#x200B;**[!UICONTROL 描述]**&#x200B;欄位中輸入選擇性描述，然後選取&#x200B;**[!UICONTROL 完成]**。
1. 導覽至「搜尋」面板。 **[!UICONTROL 標籤]**&#x200B;述詞已新增至「搜尋」面板。
1. 指定您要依據其搜尋資產的標籤，或從建議清單中選取。
1. 選取「**[!UICONTROL 全部符合]**」以搜尋包含您所指定之所有標籤的符合專案。

您可以根據&#x200B;**[!UICONTROL Name]** （字母順序）、**[!UICONTROL 已建立]**&#x200B;日期或&#x200B;**[!UICONTROL 已修改]**&#x200B;日期，以遞增或遞減順序來排序標籤結構。 在下圖中，標籤結構是根據&#x200B;**[!UICONTROL Name]**&#x200B;依字母順序排序。

![新增標記](assets/add-tags-to-asset.png)


## 新增其他述詞 {#adding-other-predicates}

與新增「屬性」述詞或「選項」述詞的方式類似，您可以將下列其他述詞新增至「搜尋」面板：

<table>
 <tbody>
  <tr>
   <td><p><strong>述詞名稱</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>屬性</strong></p> </td>
  </tr>
  <tr>
   <td><p>全文</p> </td>
   <td>搜尋述詞，在整個資產節點上執行全文搜尋。 它使用<code>jcr</code>：<code>contains</code>運運算元對應。 如果要在資產節點的特定部分執行全文搜尋，您可以指定相對路徑。</td>
   <td>
    <ul>
     <li>標籤</li>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑瀏覽器</td>
   <td>搜尋述詞，以在預先設定的根路徑搜尋資料夾和子資料夾中的資產</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>根路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>路徑</p> </td>
   <td><p>用它來篩選位置結果。 您可以將不同的路徑指定為選項。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Publish狀態</p> </td>
   <td><p>搜尋述詞，以根據資產的發佈狀態進行搜尋</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>相對日期</p> </td>
   <td><p>搜尋述詞，以根據資產的相對建立日期來搜尋資產。 例如，您可以設定2個月前、3週前等選項。 </p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>相對日期</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>範圍</p> </td>
   <td><p>搜尋述詞，以搜尋指定範圍內的資產。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日期範圍</p> </td>
   <td><p>搜尋述詞，針對日期屬性搜尋在指定範圍內建立的資產。 在「搜尋」面板中，您可以使用日期選擇器來指定開始和結束日期。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>範圍文字（從）</li>
     <li>範圍文字（至）</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p>根據日期屬性的資產滑桿式搜尋的搜尋述詞。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>檔案大小</p> </td>
   <td><p>搜尋述詞，以根據資產的大小進行搜尋。 這是以滑桿為基礎的述詞，您可以從可設定的節點選取滑桿選項。 預設選項定義於CRX存放庫中的/libs/dam/options/predicates/filesize 。 檔案大小以位元組為單位。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的資產</td>
   <td>搜尋述詞以搜尋最近修改的資產 </td>
   <td>
    <ul>
     <li>屬性名稱</li>
     <li>屬性值</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Publish狀態</td>
   <td>搜尋述詞，以根據資產的發佈狀態來搜尋資產 </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期狀態</td>
   <td>根據資產的到期狀態搜尋資產的搜尋述詞 </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隱藏</td>
   <td>定義隱藏欄位屬性以搜尋資產的搜尋述詞</td>
   <td>
    <ul>
     <li>屬性名稱</li>
     <li>屬性值</li>
     <li>說明</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 移除預設的搜尋Facet {#removing-default-search-facets}

Adobe建議您在移除預設搜尋Facet時務必小心，以免出現效能問題。 移除預設搜尋Facet也可能會影響預設功能行為。

請勿移除下列隱藏欄位，因為這會導致OmniSearch和智慧型集合出現查詢效能問題：

* group.2_group.type=dam：Asset

* group.1_group.type=nt：folder

* group.p.or=true

## 還原預設搜尋Facet {#restoring-default-search-facets}

根據預設，**[!UICONTROL 搜尋Forms]**&#x200B;頁面中的&#x200B;**[!UICONTROL Assets管理搜尋邊欄]**&#x200B;前會顯示一個鎖定圖示。 如果您將搜尋Facet新增至表單，指出預設表單已修改，則「鎖定」圖示會消失。

「搜尋Forms」頁面上某個選項的鎖定圖示表示，預設設定完整且不會自訂。

若要還原預設的搜尋Facet，請執行下列步驟：

1. 在「**[!UICONTROL 搜尋Forms]**」頁面中選取「**[!UICONTROL Assets管理搜尋邊欄]**」。
1. 在工具列中選取&#x200B;**[!UICONTROL 刪除]** ![刪除圖示](assets/do-not-localize/deleteoutline.png)。
1. 在確認對話方塊中，選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以移除自訂變更。

   刪除搜尋Facet的自訂變更後，在「搜尋表單」頁面的「資產管 **[!UICONTROL 理搜尋邊欄]** 」前會重 **** 新顯示「鎖定」圖示。

## 使用者權限 {#user-permissions}

如果您未獲指派管理員角色，以下是您需要用來執行涉及搜尋Facet的編輯、刪除和預覽動作的許可權清單。

| 動作 | 權限 |
|---|---|
| 編輯 | CRX中`/apps`節點的讀取和寫入許可權。 |
| 刪除 | 在CRX中讀取、寫入及刪除`/apps`節點的許可權。 |
| 預覽 | 在CRX中讀取、寫入及刪除`/var/dam/content`節點的許可權。 另外，`/apps`節點的讀取和寫入許可權。 |

**另請參閱**

* [搜尋最佳實務](search-best-practices.md)
* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [搜尋數位資產](search-assets.md)。
