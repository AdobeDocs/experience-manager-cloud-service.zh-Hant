---
title: 搜尋 Facet.
description: 本文說明如何在Experience Manager中建立、修改和使用搜尋Facet。
feature: Search,Metadata
role: User,Admin
exl-id: f994c1bf-3f9d-4cb2-88f4-72a9ad6fa999
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2425'
ht-degree: 21%

---

# 搜尋 Facet {#search-facets}

Adobe Experience Manager Assets的企業範圍部署可儲存許多資產。 有時候，如果您只使用Experience Manager的一般搜尋功能，尋找合適的資產可能會很費時又費力。

使用「篩選器」面板中的搜尋Facet為您的搜尋體驗新增更多精細度，並讓搜尋功能更有效率且更通用。 搜尋Facet會新增多個維度（述詞），讓您執行更複雜的搜尋。 「篩選器」面板包含幾個標準Facet。 您也可以新增自訂搜尋多面向。

總而言之，搜尋Facet可讓您以多種方式搜尋資產，而非使用單一、預先決定的分類順序。 您可以輕鬆向下鑽研至所需的詳細資訊層級，以更集中地搜尋。

例如，如果您要尋找影像，您可以選擇想要點陣圖或向量影像。 您可以指定影像的MIME型別，進一步縮小搜尋範圍。 同樣地，在搜尋檔案時，您可以指定格式，例如PDF或MS Word。

## 新增述詞 {#adding-a-predicate}

「篩選器」面板中顯示的搜尋Facet是使用述詞在基礎搜尋表單中定義。 若要顯示更多或不同的Facet，您可以將述詞新增至預設表單，或使用包含您所選的Facet的自訂表單。

若要進行全文檢索，請新增 `Fulltext` 表單的述詞。 使用屬性述詞來搜尋符合您指定之單一屬性的資產。 使用「選項」述詞來搜尋符合特定屬性的一個或多個值的資產。 新增日期範圍述詞，以搜尋在指定日期範圍內建立的資產。

1. 按一下Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 從「搜尋Forms」頁面中選取 **[!UICONTROL 資產管理搜尋邊欄]**，然後點選  **編輯** ![aemassets_edit](assets/aemassets_edit.png).

   ![找到並選取資產管理搜尋邊欄](assets/assets_admin_searchrail.png)

1. 在「編輯搜尋Forms」頁面中，從以下位置拖曳述詞： **[!UICONTROL 選取述詞]** 標籤移至主窗格。 例如，拖曳 **[!UICONTROL 屬性述詞]**.

   ![選取並移動述詞以自訂搜尋篩選器](assets/drag_predicate.png)

   *圖：選取並移動述詞以自訂搜尋篩選器。*

1. 在「設定」標籤中，輸入述詞的欄位標籤、預留位置文字和說明。 為您要與述詞關聯的中繼資料屬性指定有效的名稱。 「設定」標籤中的標題標籤可識別所選述詞的型別。

   ![使用「設定」標籤提供謂詞的必要選項](assets/settings.png)

   *圖：使用設定索引標籤提供述詞的必要選項。*

1. 在「屬 **[!UICONTROL 性名稱]** 」欄位中，指定您要與謂語關聯的中繼資料屬性的有效名稱。它是根據其執行搜索的名稱。例如，輸入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。您也可以從選取對話方塊中選取現有節點。

   ![在「屬性名稱」欄位中將中繼資料屬性與述詞建立關聯](assets/property_settings.png)

   *圖：在中繼資料屬性與屬性名稱欄位中的述詞建立關聯。*

1. 按一下 **[!UICONTROL 預覽]** ![預覽](assets/preview.png) 以產生「篩選器」面板在新增述詞後的預覽。
1. 在預覽模式中檢閱述詞的配置。

   ![在提交變更之前預覽搜尋表單](assets/preview-1.png)

   在提交變更之前預覽搜尋表單

1. 若要關閉預覽，請按一下 **[!UICONTROL 關閉]** ![關閉](assets/do-not-localize/close_icon.png) 在預覽的右上角。
1. 點選 **[!UICONTROL 完成]** 以儲存設定。
1. 導覽至Assets使用者介面中的「搜尋」面板。 屬性述詞會新增至面板。
1. 在文字方塊中輸入要搜尋之資產的說明。 例如，輸入「Adobe」。 執行搜尋時，描述符合「Adobe」的資產會列在搜尋結果中。

## 新增選項述詞 {#adding-an-options-predicate}

選項述詞可讓您在「篩選器」面板中新增多個搜尋選項。 您可以在「篩選器」面板中選取這些選項中的一個或多個來搜尋資產。 例如，若要根據檔案型別搜尋資產，請在搜尋表單中設定選項，例如「影像」、「多媒體」、「檔案」和「封存」。 設定這些選項後，當您在「濾鏡」面板中選取「影像」選項時，會對GIF、JPEG、PNG等型別的資產執行搜尋。

若要將選項對應至個別屬性，請建立選項的節點結構，並在Options述詞的Property Name屬性中提供父節點的路徑。 父節點應為型別 `sling`： `OrderedFolder`. 選項應為型別 `nt:unstructured`. 選項節點應具有屬性 `jcr:title` 和 `value` 已設定。

此 `jcr:title` 屬性是顯示在「篩選器」面板上之選項的使用者易記名稱。 此 `value` 欄位用於查詢，以符合指定的屬性。

當您選取選項時，會根據 `value` 選項節點及其子節點的屬性（如果有）。 系統會遍歷option節點下的整個樹狀結構， `value` 每個子節點的屬性會使用OR運算來組合，以形成搜尋查詢。

例如，如果您為檔案類型選取「影像」，則會使用OR運算結合屬性來建立資 `value` 產的搜尋查詢。例如，通過組合影像/jpeg *、* image/gif *、* png影像、影像 */jpeg影像、以及使用OR操作對Tiff屬性進行搜索的Joff影像*****`jcr:content/metadata/dc:format` /Tiff影像的匹配結果來構建影像搜索查詢。

檔案型別的值屬性（如CRXDE中所見）可用於搜尋查詢

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

如果要使用現有節點，請使用選取對話方塊來指定它。

>[!NOTE]
>
>Options述詞是包含屬性述詞的自訂包裝函式，用於示範所描述的行為。 目前沒有可用的REST端點可原生支援此功能。

1. 點選Experience Manager標誌，然後前往 **[!UICONTROL 「工具>一般>搜尋Forms」]**.
1. 從「搜 **[!UICONTROL 尋表單」頁面]** ，選取「資 ****&#x200B;產管理搜尋邊欄」，然後點選「編輯」圖示。
1. 在「編 **[!UICONTROL 輯搜索表單]** 」頁中，將「選 **[!UICONTROL 項謂詞」從]** 「選擇謂詞 **** 」頁籤拖到主窗格。
1. 在「設 **[!UICONTROL 定]** 」標籤中，輸入屬性的標籤和名稱。例如，若要根據資產的格式來搜尋資產，請為標籤指定好記的名稱，例如「檔案類 **[!UICONTROL 型」]**。指定在屬性欄位中根據其執行搜索的屬性，例如 `jcr:content/metadata/dc:format.`
1. 執行下列任一項作業：

   * 在 **[!UICONTROL 屬性名稱]** 欄位，提及JSON檔案的路徑，您可在此定義選項的節點，並指定對應的索引鍵值配對。
   * 點選 ![資產新增圖示](assets/do-not-localize/aem_assets_add_icon.png) 「選項」欄位旁邊，指定您要在「篩選器」面板中提供之選項的顯示文字和值。 若要新增其他選項，請點選/按一下 ![資產新增圖示](assets/do-not-localize/aem_assets_add_icon.png) 並重複此步驟。

1. 確保清 **[!UICONTROL 除「單選]** 」，讓使用者一次為檔案類型選取多個選項 (例如影像、檔案、多媒體和封存)。如果您選 **[!UICONTROL 取「單選]**」，使用者一次只能為檔案類型選取一個選項。

   ![選項述詞中的可用欄位](assets/options_predicate.png)

   選項述詞中的可用欄位

1. 在 **說明** 欄位，輸入選擇性說明，然後按一下 **[!UICONTROL 完成]**.
1. 導覽至「搜尋」面板。 「選項」述詞會新增至 **搜尋** 面板。 的選項 **[!UICONTROL 檔案型別]** 會顯示為核取方塊。

## 新增多值屬性述詞 {#adding-a-multi-value-property-predicate}

此 `Multi Value Property` 述詞可讓您搜尋資產以取得多個值。 請考量您在中擁有多個產品影像的情況 [!DNL Assets] 且每個影像的中繼資料都包含與產品相關聯的SKU編號。 您可以使用此述詞來根據多個SKU編號搜尋產品影像。

1. 按一下Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 在「搜尋Forms」頁面上，選取 **[!UICONTROL 資產管理搜尋邊欄]**，點選 **編輯** ![aemassets_edit](assets/aemassets_edit.png).
1. 在「編輯搜索表單」頁中，將「 **[!UICONTROL Multi Value Property Predicate]** 」從「 **[!UICONTROL Select Predicate]** 」頁籤拖動到主窗格。
1. 在 **[!UICONTROL 設定]** 索引標籤中，輸入述詞的標籤和預留位置文字。 在屬性欄位中指定搜尋所依據的屬性名稱，例如 `jcr:content/metadata/dc:value`. 您也可以使用選取對話方塊來選取節點。
1. 請確定已 **[!UICONTROL 選取「分隔字元]** 」支援。在「輸入 **[!UICONTROL 分隔字元]** 」欄位中，指定分隔字元以分隔個別值。依預設，逗號會指定為分隔字元。您可以指定不同的分隔字元。
1. 在 **說明** 欄位，輸入選填的說明，然後點選 **[!UICONTROL 完成]**.
1. 導覽至「資產」使用者介面中的「篩選」面板。The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 在「多值」欄位中指定多個值（以分隔符號分隔），然後執行搜尋。 述詞會擷取與指定值完全相符的文字。

## 新增標籤述詞 {#adding-a-tags-predicate}

此 `Tags` 述詞可讓您對資產執行標籤式搜尋。 依預設， [!DNL Assets] 根據您指定的標籤，在資產中搜尋一或多個相符標籤。 換言之，搜尋查詢會使用指定的標籤執行OR操作。 不過，您可以使用「比對所有標籤」選項來搜尋包含您所指定之所有標籤的資產。

1. 按一下Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 從「搜尋Forms」頁面中選取 **[!UICONTROL 資產管理搜尋邊欄]** 然後點選 **編輯** ![aemassets_edit](assets/aemassets_edit.png).
1. 在「編輯搜尋表單」頁面中，拖曳 **[!UICONTROL 標籤述詞]** 從「選取述詞」標籤移至主窗格。
1. 在設定索引標籤中，輸入述詞的預留位置文字。 在屬性欄位中指定搜尋所依據的屬性名稱，例如 `jcr:content/metadata/cq:tags`. 或者，您也可以從選取對話方塊中選取CRXDE中的節點。
1. 設定此述詞的根標籤路徑屬性，以填入標籤清單中的各種標籤。
1. 選取 **[!UICONTROL 「顯示符合所有標籤」選項]** ，以搜尋包含您所指定之所有標籤的資產。

   ![標籤述詞的典型設定](assets/tags_predicate.png)

1. 在 **[!UICONTROL 說明]** 欄位，輸入選填的說明，然後按一下/點選 **[!UICONTROL 完成]**.
1. 導覽至「搜尋」面板。 此 **[!UICONTROL 標籤]** 述詞會新增至「搜尋」面板。
1. 指定您要依據其搜尋資產的標籤，或從建議清單中選取。
1. 選取 **[!UICONTROL 全部符合]** 以搜尋包含您所指定之所有標籤的相符專案。

您可以根據 **[!UICONTROL 名稱]** （依字母順序）， **[!UICONTROL 已建立]** 日期，或 **[!UICONTROL 修改時間]** 日期。 在下圖中，標籤結構是根據 **[!UICONTROL 名稱]**.

![add-tag](assets/add-tags-to-asset.png)


## 新增其他述詞 {#adding-other-predicates}

與新增「屬性」述詞或「選項」述詞的方式類似，您也可以將下列其他述詞新增至「搜尋」面板：

<table>
 <tbody>
  <tr>
   <td><p><strong>述詞名稱</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>屬性</strong></p> </td>
  </tr>
  <tr>
   <td><p>全文</p> </td>
   <td>搜尋述詞，以在整個資產節點上執行全文搜尋。 對應有 <code>jcr</code>：<code>contains</code> 運運算元。 如果要對資產節點的特定部分執行全文搜尋，您可以指定相對路徑。</td>
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
   <td><p>使用它來篩選位置的結果。 您可以將不同的路徑指定為選項。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>發佈狀態</p> </td>
   <td><p>搜尋述詞，以根據資產的發佈狀態來搜尋資產</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>相對日期</p> </td>
   <td><p>搜尋述詞，以根據資產的相對建立日期來搜尋資產。 例如，您可以設定選項，例如2個月前、3週前等。 </p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>相對日期</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>範圍</p> </td>
   <td><p>搜尋述詞，可搜尋指定範圍內的資產。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</p> </td>
   <td>
    <ul>
     <li>標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日期範圍</p> </td>
   <td><p>搜尋述詞，以搜尋在指定範圍內建立的資產，以取得日期屬性。 在「搜尋」面板中，您可以使用日期選擇器來指定開始和結束日期。</p> </td>
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
   <td><p>搜尋述詞，以根據資產的大小進行搜尋。 這是以Silder為基礎的述詞，您可以從可設定的節點選取滑桿選項。 預設選項定義於CRX存放庫中的/libs/dam/options/predicates/filesize 。 檔案大小以位元組為單位。</p> </td>
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
   <td>發佈狀態</td>
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
   <td>搜尋述詞，以根據資產的到期狀態來搜尋資產 </td>
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

## 還原預設搜尋Facet {#restoring-default-search-facets}

依預設，「鎖定」圖示會出現在之前 **[!UICONTROL 資產管理搜尋邊欄]** 在 **[!UICONTROL 搜尋Forms]** 頁面。 如果您將搜尋Facet新增至表單，指出預設表單已修改，則「鎖定」圖示會消失。

「搜尋Forms」頁面上某個選項的鎖定圖示表示預設設定完整且未自訂。

若要還原預設的搜尋Facet，請執行下列步驟：

1. 選取 **[!UICONTROL 資產管理搜尋邊欄]** 在 **[!UICONTROL 搜尋Forms]** 頁面。
1. 點選 **[!UICONTROL 刪除]** ![刪除圖示](assets/do-not-localize/deleteoutline.png) （在工具列中）。
1. 在確認對話方塊中，點選 **[!UICONTROL 刪除]** 以移除自訂變更。

   刪除搜尋Facet的自訂變更後，在「搜尋表單」頁面的「資產管 **[!UICONTROL 理搜尋邊欄]** 」前會重 **** 新顯示「鎖定」圖示。

## 使用者許可權 {#user-permissions}

如果您未獲指派管理員角色，以下列出執行與搜尋Facet相關的編輯、刪除和預覽動作所需的許可權。

| 動作 | 權限 |
|---|---|
| 編輯 | 的讀取和寫入許可權 `/apps` CRX中的節點。 |
| 刪除 | 對的讀取、寫入和刪除許可權 `/apps` CRX中的節點。 |
| 預覽 | 對的讀取、寫入和刪除許可權 `/var/dam/content` CRX中的節點。 此外，的讀取和寫入許可權 `/apps` 節點。 |

**另請參閱**

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

>[!MORELIKETHIS]
>
>* [搜尋數位資產](search-assets.md).

