---
title: 如何在AEM中搜尋資產？
description: 瞭解如何使用篩選器面板在AEM中搜尋資產，以及如何使用資產搜尋中顯示的結果。
contentOwner: AG
mini-toc-levels: 1
feature: Search,Metadata,Asset Distribution
role: User,Admin
exl-id: 68bdaf25-cbd4-47b3-8e19-547c32555730
source-git-commit: 35d70cd3843b5e0857a24a17746e05072aed7e1b
workflow-type: tm+mt
source-wordcount: '5564'
ht-degree: 8%

---

# 在AEM中搜尋資產 {#search-assets-in-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets] 提供強大的資產搜尋方法，協助您實現更高的內容速度。 您的團隊可使用開箱即用的功能和自訂方法，透過順暢的智慧型資產搜尋體驗縮短上市時間。 搜尋資產功能是使用數位資產管理系統的核心，不論是供創意人員進一步使用、供業務使用者和行銷人員健全管理資產，還是DAM管理員管理。 您可以透過執行的簡單、進階及自訂搜尋 [!DNL Assets] 使用者介面或其他應用程式和介面有助於完成這些使用案例。

AEM中的資產搜尋支援下列使用案例，本文介紹這些使用案例的使用方式、概念、設定、限制和疑難排解。

| 搜尋資產 | 設定及管理搜尋功能 | 使用資產搜尋結果 |
|---|---|---|
| [基本搜尋](#searchbasics) | [搜尋索引](#searchindex) | [排序結果](#sort) |
| [瞭解搜尋UI](#searchui) | [文字擷取](#extracttextupload) | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必要中繼資料](#mandatorymetadata) | [下載](#download) |
| [瞭解搜尋結果和行為](#searchbehavior) | [修改搜尋多面向](#searchfacets) | [大量中繼資料更新](#metadata-updates) |
| [搜尋排名和提升](#searchrank) | [自訂述詞](#custompredicates) | [智慧型集合](#collections) |
| [進階搜尋：篩選和搜尋範圍](#scope) | | [瞭解並疑難排解非預期的結果](#unexpected-results) |
| [從其他解決方案和應用程式搜尋](#search-assets-other-surfaces)：<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager案頭應用程式](#desktop-app)</li><li>[Adobe Stock影像](#adobe-stock)</li><li>[Dynamic Media資產](#search-dynamic-media-assets)</li></ul> | | |
| [資產選擇器](#asset-picker) | | |
| [限制](#limitations) 和 [提示](#tips) | | |
| [插圖範例](#samples) | | |

使用Omnisearch欄位在頂端搜尋資產 [!DNL Experience Manager] 網頁介面。 前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** 在 [!DNL Experience Manager]，按一下 ![search_icon](assets/do-not-localize/search_icon.png) 在頂端列中，輸入搜尋關鍵字，然後選取 `Return`. 或者，使用關鍵字捷徑 `/` （正斜線）以開啟「全能搜尋」欄位。 `Location:Assets` 已預先選取，以將搜尋限制在DAM資產。 `Path:/content/dam` 當您在「 」中的根層級執行搜尋時，也會顯示 **[!UICONTROL 檔案]** 資料夾。 如果您導覽至任何其他資料夾， `Path:/content/dam/<folder name>` 會顯示在Omnisearch欄位中，以將搜尋範圍限制在目前的資料夾。 [!DNL Experience Manager] 會在您開始輸入搜尋關鍵字時提供建議。

使用 **[!UICONTROL 篩選器]** 面板來搜尋資產、資料夾、標籤和中繼資料。 您可以根據各種選項（述詞）來篩選搜尋結果，例如檔案型別、檔案大小、上次修改日期、資產狀態、見解資料和Adobe Stock授權。 您可以自訂「篩選器」面板，並使用新增或移除搜尋述詞 [搜尋facet](/help/assets/search-facets.md). 此 [!UICONTROL 檔案型別] 在中篩選 [!UICONTROL 篩選器] 面板有混合狀態核取方塊。 因此，除非您選取所有巢狀述詞（或格式），否則會部分勾選第一層核取方塊。

[!DNL Experience Manager] 搜尋功能支援搜尋收藏集和搜尋收藏集中的資產。 另請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 瞭解資產搜尋介面 {#searchui}

請熟悉資產搜尋介面和可用的動作。
<!--
![Understand Experience Manager Assets search results interface](assets/aem_search_results.png)
-->
![瞭解Experience Manager Assets搜尋結果介面](assets/aem-search-interface.png)
*圖：瞭解 [!DNL Experience Manager Assets] 搜尋結果介面。*

**答：** 將搜尋儲存為智慧型集合。
**B.** 篩選或述詞以縮小搜尋結果。
**C.** 顯示檔案、資料夾或兩者。
**D.** 搜尋位置為DAM。
**E.** 存取已儲存的搜尋。
**F.** 按一下「篩選器」以開啟或關閉左側邊欄。
**G.** 將資產顯示為預設搜尋。
**高。** 搜尋位置為DAM。
**I.** 具有使用者提供的搜尋關鍵字的Omnisearch欄位。
**J.** 選取載入的搜尋結果。
**K.** 依建立、修改、名稱、無進行排序。
**L.** 依遞增或遞減順序排序。
**月** 搜尋結果總數中顯示的搜尋結果數目。 **否。** 關閉搜尋。
**O.** 在卡片檢視和清單檢視之間切換。

### 動態搜尋Facet {#dynamicfacets}

您可以使用搜尋Facet中預期搜尋結果數量的動態更新，更快速地從搜尋結果頁面探索所需資產。 甚至在套用搜尋篩選條件之前，資產的預期數量也會更新。 檢視篩選的預期計數，有助於您快速有效瀏覽搜尋結果。

![檢視未篩選搜尋Facet中搜尋結果的資產近似數量。](assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋Facet中檢視未篩選搜尋結果的資產近似數量。*

Experience Manager Assets預設會顯示兩個屬性的Facet計數：

* 資產型別(jcr：content/metadata/dc：format)

* 核准狀態(jcr：content/metadata/dam：status)

截至2023年8月，Experience Manager Assets包含新版9 `damAssetLucene` 索引。 舊版、 `damAssetLucene-8` 在底下，使用 `statistical` 模式，針對每個搜尋面向計數檢查專案範例的存取控制。

`damAssetLucene-9` 將 Oak Query 面向計數的行為變更為不再評估對基本搜尋指數傳回的面向計數存取控制，這會使搜尋回應時間更快。因此，使用者可能會看到面向計數值，其中包括他們無權存取的資產。 這些使用者無法存取、下載或讀取這些資產的任何其他詳細資訊，包括其路徑，或取得任何有關這些資產的進一步資訊。

如果您需要切換到先前的行為(`statistical` 模式)，請參閱 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html) 建立自訂版本的 `damAssetLucene-9` 索引。 Adobe不建議切換至 `secure` 模式，因為對大型結果集的搜尋回應時間造成影響。

如需Oak面向功能的詳細資訊，包括這些模式的詳細說明，請參閱 [本文](https://jackrabbit.apache.org/oak/docs/query/lucene.html#facets).

## 輸入時搜尋建議 {#searchsuggestions}

當您開始輸入關鍵字時，Experience Manager會建議可能的搜尋關鍵字或片語。 這些建議是根據Experience Manager中的資產。 Experience Manager會編制所有中繼資料欄位的索引，以協助搜尋。 為了提供搜尋建議，系統會使用下列幾個中繼資料欄位的值。 若要提供搜尋建議，請考慮將適當的關鍵字填入下列欄位：

* 資產標籤。 (將對應至 `jcr:content/metadata/cq:tags`)
* 資產標題。 (將對應至 `jcr:content/metadata/dc:title`)
* 資產說明。 (將對應至 `jcr:content/metadata/dc:description`)
* JCR存放庫中的標題。 值可能會對應至資產標題。 (將對應至 `jcr:content/jcr:title`)
* JCR存放庫中的說明。 此值可能會對應到資產說明。 (將對應至 `jcr:content/jcr:description`)

## 瞭解搜尋結果和行為 {#searchbehavior}

### 基本搜尋字詞和結果 {#searchbasics}

您可以從OmniSearch欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，且是全文檢索搜尋（涵蓋熱門中繼資料欄位）。 如果使用多個關鍵字， `AND` 是關鍵字之間的預設運運算元。

結果會依相關性排序，從最接近的相符專案開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含兩個字詞的資產。 在中繼資料中，顯示為智慧標籤的關鍵字的排名高於出現在其他中繼資料欄位中的關鍵字。 [!DNL Experience Manager] 允許給予特定搜尋詞較高的權重。 此外，您也可以 [提升排名](#searchrank) 特定搜尋字詞的幾個目標資產中。

為快速找到相關資產，豐富的介面可提供篩選、排序和選取機制。 您可以根據多個條件篩選結果，並檢視各種篩選條件的搜尋資產數目。 或者，您可以透過變更Omnisearch欄位中的查詢來重新執行搜尋。 當您變更搜尋字詞或篩選器時，其他篩選器仍會套用，以保留您的搜尋內容。

當結果為許多資產時， [!DNL Experience Manager] 在卡片檢視中顯示前100個，在清單檢視中顯示前200個。 當使用者捲動時，會載入更多資產。 這是為了改善效能。 觀看影片示範 [顯示的資產數量](https://www.youtube.com/watch?v=LcrGPDLDf4o).

有時，您可能會在搜尋結果中看到一些未預期的資產。 如需詳細資訊，請參閱 [未預期的結果](#unexpected-results).

[!DNL Experience Manager] 可搜尋多種檔案格式，也可自訂搜尋篩選器以符合您的業務需求。 請聯絡您的管理員，瞭解您的DAM存放庫有哪些搜尋選項可用，以及您的帳戶有哪些限制。

<!-- 
### Results with and without enhanced Smart Tags {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using Smart Tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### 搜尋排名和提升 {#searchrank}

符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 在上述範例中，顯示搜尋結果的大約順序為：

1. 符合的 `woman running` 於各種中繼資料欄位中。
1. 符合的 `woman running` 在智慧標籤中。
1. 符合的 `woman` 或 `running` 在智慧標籤中。

您可以改善特定資產的關鍵字關聯性，以協助根據關鍵字提升搜尋次數。 換言之，當您根據這些關鍵字進行搜尋時，您為其升級特定關鍵字的影像會出現在搜尋結果的最上方。

1. 從 [!DNL Assets] 使用者介面，開啟資產的屬性頁面。 按一下 **[!UICONTROL 進階]** 並按一下 **[!UICONTROL 新增]** 在 **[!UICONTROL 針對搜尋關鍵字提升]**.
1. 在 **[!UICONTROL 搜尋提升]** 方塊，指定您要增加影像搜尋的關鍵字，然後按一下 **[!UICONTROL 新增]**. 您可以用相同方式指定多個關鍵字。
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。您針對此關鍵字提升的資產會出現在最上層的搜尋結果中。

您可以藉此機會提升目標關鍵字搜尋結果中某些資產的排名。 請觀看下方的視訊範例。 如需詳細資訊，請參閱 [搜尋 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*影片：瞭解搜尋結果的排名方式，以及如何影響排名。*

## 設定資產批次大小以顯示搜尋結果 {#configure-asset-batch-size}

管理員現在可在您執行搜尋時設定顯示資產的批次大小。當您進一步向下捲動以載入結果時，資產搜尋結果將以設定的批次大小數字的倍數顯示。您可以從 200、500 和 1000 個資產的可用批次大小中進行選擇。將批次大小設定為較低數字時，會使搜尋回應時間更快。

例如，如果您將結果計數限制設為200個資產的批次大小，當您開始執行搜尋時，Experience Manager Assets會在搜尋結果中顯示200個資產的批次大小。 當您向下捲動以導覽搜尋結果時，將顯示下一批的200個資產。 此程式會持續進行，直到顯示符合搜尋查詢的所有資產為止。

若要設定資產批次大小：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資產設定]** > **[!UICONTROL Assets Omnisearch設定]**.

1. 選取結果計數限制並按一下 **[!UICONTROL 儲存]**.

   ![資產批次大小的設定](/help/release-notes/assets/assets-batch-size-configuration.png)

## 進階搜尋 {#scope}

[!DNL Experience Manager] 提供多種方法（例如套用至已搜尋資產的篩選器），協助您更快找到所需資產。 以下說明一些常用方法。 部分 [插圖範例](#samples) 共用。

**搜尋檔案或資料夾**：在搜尋結果中，檢視檔案、資料夾或兩者。 從 **[!UICONTROL 篩選器]** 面板中，您可以選取適當的選項。 另請參閱 [搜尋介面](#searchui).

**在資料夾中搜尋資產**：您可以將搜尋限制在特定資料夾中。 在 **[!UICONTROL 篩選器]** 面板，新增資料夾的路徑。 您一次只能選取一個資料夾。

![在「篩選器」面板中新增資料夾路徑，將搜尋結果限製為資料夾](assets/limiting-search.gif)
<!--
![Limit search results to a folder by adding a folder path in Filters panel](assets/search_folder_select.gif)
-->

*圖：透過在「篩選器」面板中新增資料夾路徑，將搜尋結果限製為資料夾。*

### 尋找類似影像 {#visualsearch}

若要尋找視覺上類似使用者選取之影像的影像，請從影像的卡片檢視或工具列按一下「尋找類似 **** 」選項。[!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。

![使用卡片檢視中的選項尋找類似影像](assets/search_find_similar.png)

*圖：使用卡片檢視中的選項尋找類似影像。*

### Adobe Stock影像 {#adobe-stock}

從 [!DNL Experience Manager] 使用者介面，使用者可搜尋 [Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) 並授權必要的資產。 新增 `Location: Adobe Stock` 在Omnisearch列中。 您也可以使用「篩選器」面板來尋找所有已授權或未授權的資產，或使用Adobe Stock檔案編號來搜尋特定資產。

### Dynamic Media資產 {#dmassets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。

### 使用中繼資料欄位中的特定值的GQL搜尋 {#gql-search}

您可以根據中繼資料欄位的確切值來搜尋資產，例如標題、說明和建立者。 GQL全文檢索搜尋功能只會擷取中繼資料值與搜尋查詢完全相符的資產。 屬性的名稱（建立者、標題等）和值區分大小寫。

| 中繼資料欄位 | Facet值和使用狀況 |
|---|---|
| 標題 | title：John |
| 建立者 | 建立者：John |
| 位置 | 位置：NA |
| 說明 | description：&quot;Sample Image&quot; |
| 建立者工具 | creatortool：&quot;Adobe Photoshop&quot; |
| 版權擁有者 | 版權擁有者：「Adobe Systems」 |
| 參與者 | 貢獻者：John |
| 使用條款 | usageterms：&quot;CopyRights Reserved&quot; |
| 建立日期 | created：YYYY-MM-DDTHH |
| 到期日期 | expires：YYYY-MM-DDTHH |
| 準時 | ontime：YYYY-MM-DDTHH |
| 關閉時間 | offtime：YYYY-MM-DDTHH |
| 時間範圍(expires dateontime，offtime) | Facet欄位：下限……上界 |
| 路徑 | /content/dam/&lt;folder name=&quot;&quot;> |
| PDF 標題 | pdftitle：&quot;Adobe檔案&quot; |
| 主旨 | 主旨：「培訓」 |
| 標記 | 標籤：「地點和旅遊」 |
| 類型 | 型別：&quot;image\png&quot; |
| 影像寬度 | 寬度：下限……上界 |
| 影像高度 | 高度：下限……上界 |
| 人員 | 人員：John |

屬性 `path`， `limit`， `size`、和 `orderby` 無法使用合併 `OR` 運運算元與任何其他屬性。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

使用者產生的屬性的關鍵字是屬性編輯器中的欄位標籤（小寫），其中會移除空格。

以下是複雜查詢的搜尋格式範例：

* 若要顯示具有多個多面向欄位的所有資產(例如： title=John Doe and creator tool = Adobe Photoshop)： `title:"John Doe" creatortool:Adobe*`
* 當Facet值不是單一字詞而是句子時（例如：title=Scott Reynolds），若要顯示所有資產： `title:"Scott Reynolds"`
* 若要顯示具有單一屬性的多個值的資產（例如：title=Scott Reynolds或John Doe）： `title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產（例如：title是Scott Reynolds）： `title:Scott*`
* 若要顯示屬性值以特定字串結尾的資產（例如：title是Scott Reynolds）： `title:*Reynolds`
* 若要以包含特定字串的屬性值來顯示資產（例如：標題= Basel會議室），請執行下列動作： `title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如：在title=John Doe的資產中搜尋字串Adobe)： `*Adobe* title:"John Doe"`

## 從其他專案搜尋資產 [!DNL Experience Manager] 方案或介面 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] 將DAM存放庫連線到其他各種存放庫 [!DNL Experience Manager] 解決方案，提供更快速存取數位資產並簡化創意工作流程。 任何資產探索都會從瀏覽或搜尋開始。 在各種表面和解決方案中，搜尋行為大致相同。 有些搜尋方法會隨著目標對象、使用案例和使用者介面的不同而有所變更。 [!DNL Experience Manager] 解決方案。 以下連結提供各個解決方案的特定方法。 本文記錄通用適用的提示和行為。

### 從Adobe Asset Link面板搜尋資產 {#aal}

創意專業人士現在可以使用Adobe Asset Link存取中儲存的內容 [!DNL Experience Manager Assets]，無需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用 [!DNL Adobe Creative Cloud] 應用程式： [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign]. Asset Link也可讓使用者搜尋視覺上類似的結果。 視覺化搜尋顯示結果由Adobe Sensei的機器學習演演算法提供支援，並幫助使用者尋找在美學上相似的影像。 另請參閱 [搜尋和瀏覽資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 使用Adobe資產連結。

### 搜尋中的資產 [!DNL Experience Manager] 案頭應用程式 {#desktop-app}

創意專業人士使用案頭應用程式來進行 [!DNL Experience Manager Assets] 可輕鬆搜尋並在其本機案頭(Win或Mac)上使用。 創意人員可以輕鬆地在Mac Finder或Windows檔案總管中顯現所需的資產、在案頭應用程式中開啟並在本機變更 — 變更會儲存回 [!DNL Experience Manager] 存放庫中建立新版本。 應用程式支援使用一或多個關鍵字進行基本搜尋。 `*` 和 `?` 萬用字元，和 `AND` 運運算元。 另請參閱 [瀏覽、搜尋和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 在案頭應用程式中。

### 搜尋 [!DNL Brand Portal] 中的資產 {#brand-portal}

業務線使用者和行銷人員可使用Brand Portal，有效率且安全地與擴充的內部團隊、合作夥伴和經銷商共用核准的數位資產。 另請參閱 [在Brand Portal上搜尋資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜尋 [!DNL Adobe Stock] 影像 {#adobe-stock1}

從 [!DNL Experience Manager] 使用者介面，使用者可以搜尋Adobe Stock資產並授權必要的資產。 新增 `Location: Adobe Stock` （在Omnisearch欄位中）。 您也可以使用 **[!UICONTROL 篩選器]** 面板以尋找所有已授權或未授權的資產，或使用Adobe Stock檔案編號搜尋特定資產。 另請參閱 [管理 [!DNL Adobe Stock] 中的影像 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### 搜尋 [!DNL Dynamic Media] 資產 {#search-dynamic-media-assets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。在製作網頁時，作者可在內容尋找工具中搜尋集合。集合的篩選器可從快顯功能表中取得。

### 製作網頁時在「內容尋找器」中搜尋資產 {#content-finder}

作者可使用「內容尋找器」在DAM存放庫中搜尋相關資產，並在他們建立的網頁中使用資產。 作者也可以使用「連線資產」功能來搜尋遠端可用的資產 [!DNL Experience Manager] 部署。 然後，作者便可以在本機的網頁中使用這些資產 [!DNL Experience Manager] 部署。 另請參閱 [使用遠端資產](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜尋集合 {#collections}

[!DNL Experience Manager] 搜尋功能支援搜尋收藏集和搜尋收藏集中的資產。 另請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 資產選擇器 {#asset-picker}

資產選擇器(在舊版中稱為資產選擇器 [!DNL Adobe Experience Manager])可讓您以特殊方式搜尋、篩選及瀏覽DAM資產。 資產選擇器位於 `https://[aem_server]:[port]/aem/assetpicker.html`. 您可以擷取使用資產選擇器所選取資產的中繼資料。 您可以使用支援的請求引數來啟動它，例如資產型別（影像、視訊、文字）和選取模式（單一或多個選取範圍）。 這些引數會為特定搜尋執行個體設定資產選擇器的內容，並在整個選取範圍中維持不變。

資產選擇器使用HTML5 `Window.postMessage` 傳送所選資產的資料給收件者的訊息。 它僅適用於瀏覽模式和Omnisearch結果頁面。

在URL中傳遞下列請求引數，以啟動特定內容中的資產選擇器：

| 名稱 | 值 | 範例 | 用途 |
|---|---|---|---|
| 資源尾碼(B) | URL中作為資源尾碼的資料夾路徑： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 若要在選取特定檔案夾後啟動資產選擇器（例如選取檔案夾後） `/content/dam/we-retail/en/activities` 選取時，URL的格式為： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果您在啟動資產選擇器時要求選擇特定資料夾，請將其作為資源尾碼傳遞。 |
| `mode` | 單一，多個 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多重模式中，您可以使用資產選擇器同時選取數個資產。 |
| `dialog` | true， false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些引數以Granite對話方塊開啟資產選擇器。 此選項僅適用於透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時。 |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在此情況下，資產選擇器可讓您僅選取根資料夾下的子資產（直接/間接）。 |
| `viewmode` | 搜尋 | | 若要在搜尋模式中啟動資產選擇器，請使用 `assettype` 和 `mimetype` 引數。 |
| `assettype` | 影像、檔案、多媒體、封存。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用選項可依據提供的值篩選資產型別。 |
| `mimetype` | MIME型別(`/jcr:content/metadata/dc:format`)（也支援萬用字元）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根據MIME型別篩選資產。 |

若要存取資產選擇器介面，請前往 `https://[aem_server]:[port]/aem/assetpicker`. 導覽至所需的資料夾，然後選取一或多個資產。 或者，從Omnisearch方塊搜尋所需的資產，視需要套用篩選器，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/select-asset.png)

<!--![Browse and select asset in the asset selector](assets/assetpicker.png)-->

*圖：瀏覽並選取資產選擇器中的資產。*

## 限制 {#limitations}

中的搜尋功能 [!DNL Experience Manager Assets] 有以下限制：

* 請勿在搜尋查詢中輸入前導空格，否則搜尋無法運作。
* [!DNL Experience Manager] 當您從搜尋結果中選取資產的屬性，然後取消搜尋之後，可能會繼續顯示搜尋字詞。 <!-- (CQ-4273540) -->
* 搜尋資料夾或檔案和資料夾時，搜尋結果無法依據任何引數排序。
* 如果您選取 `Return` 無需輸入Omnisearch列， [!DNL Experience Manager] 只傳回檔案清單，不傳回資料夾清單。 如果您不使用關鍵字而專門搜尋資料夾， [!DNL Experience Manager] 未傳回任何結果。
* 您可以對資料夾執行全文檢索搜尋。 指定要讓搜尋運作的搜尋字詞。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋最適合用於大型存放庫。 雖然沒有達到良好結果所需的最低影像數量，但少數影像的相符品質不如大型存放庫的相符專案。
* 您無法變更模型或訓練 [!DNL Experience Manager] 以尋找類似的影像。 例如，在少數資產中新增或移除智慧標籤不會變更模型。 這些資產確實會從視覺上相似的搜尋結果中排除。

搜尋功能在下列情況下可能有效能限制：

* 與顯示搜尋結果的清單檢視相比，卡片檢視的載入時間更快。

## 搜尋提示 {#tips}

* 監控資產的稽核狀態時，請使用適當的選項來尋找已核准的資產或待核准的資產。
* 使用見解述詞，根據從各種創意應用程式獲得的使用統計資料來搜尋支援的資產。 使用情況資料會依使用情況分數、曝光數、點按數和資產顯示類別的媒體管道分組。
* 使用 **[!UICONTROL 全選]** 核取方塊以選取搜尋的資產。 [!DNL Experience Manager] 最初在卡片檢視中顯示100個資產，在清單檢視中顯示200個資產。 捲動搜尋結果時會載入更多資產。 您可以選取比已載入資產更多的資產。 所選資產的計數會顯示在搜尋結果頁面的右上角。 您可以對選取範圍進行操作，例如，下載所選資產、大量更新所選資產的中繼資料屬性，或將所選資產新增到收藏集。 當選取的資產多於顯示時，動作會套用於所有選取的資產，或對話方塊顯示套用於的資產數量。 若要將動作套用至未載入的資產，請確定已明確選取所有資產。
* 若要搜尋不含必要中繼資料的資產，請參閱 [必要中繼資料](#mandatorymetadata).
* 搜尋會使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為了獲得更好的結果，請使用雙（非單）引號，或確保數字與沒有特殊字元的字詞相鄰(例如 `shoe12`)。
* 全文檢索搜尋支援下列運運算元： `-` 和 `^`. 若要將這些字母搜尋為字串常值，請以雙引號括住搜尋運算式。 例如，使用 `"Notebook - Beauty"` 而非 `Notebook - Beauty`.
* 如果搜尋結果太多，請限制 [搜尋範圍](#scope) 零入所需的資產。 當您知道如何更妥善尋找所需資產（例如特定檔案型別、特定位置、特定中繼資料等）時，此功能就會最有效。

* **標籤**：標籤可協助您更有效率地將可瀏覽和搜尋的資產分類。 標記有助於將適當的分類法傳播給其他使用者和工作流程。[!DNL Experience Manager] 提供使用Adobe Sensei的人工智慧服務自動標籤資產的方法，以透過使用和培訓持續更有效地標籤您的資產。 搜尋資產時，智慧標籤會納入考量。 它可與內建搜尋功能搭配使用。 另請參閱 [搜尋行為](#searchbehavior). 若要最佳化搜尋結果的顯示順序，您可以 [提升搜尋排名](#searchrank) 中的幾個選取資產。

* **索引**：搜尋結果中只會傳回已編制索引的中繼資料和資產。 為了獲得更好的涵蓋範圍和效能，請確保建立適當的索引並遵循最佳實務。 另請參閱 [索引](#searchindex).

## 說明搜尋的一些範例 {#samples}

在關鍵字周圍使用雙引號來尋找包含精確片語的資產，其順序與使用者指定的完全一致。

![有引號和無引號的搜尋行為](assets/search_with_quotes.gif)

*圖：使用引號和不使用引號的搜尋行為。*

**使用星號萬用字元搜尋**：若要擴大搜尋範圍，可在搜尋字詞前後使用星號，以比對任意數量的字元。 例如，搜尋沒有星號的執行不會傳回包含任何字詞變數的資產（包括中繼資料中的）。 星號可取代任意數目的字元。 例如，

* `run` 傳回帶有exactly run關鍵字的資產
* `run*` 傳回資產方法 `running`， `run`， `runaway`、等等。
* `*run` 傳回資產方法 `outrun`， `rerun`、等等。
* `*run*` 傳回所有可能的組合。

![舉例說明在資產搜尋中使用星號萬用字元](assets/search_with_asterisk_run.gif)

*圖：使用範例說明在資產搜尋中使用星號萬用字元的情形。*

**使用問號萬用字元搜尋**：若要擴大搜尋範圍，請使用一或多個「？」 個字元，以符合確切的字元數。 例如，在下圖中，

* `run???` 查詢不符合任何資產。

* `run????` 查詢符合單字 `running` 後面有四個字元 `run`.

* `??run` 查詢符合單字 `rerun` 前面有兩個字元 `run`.

![舉例說明在資產搜尋中使用問號萬用字元](assets/search_with_questionmark_run.gif)

*圖：說明在資產搜尋中使用問號萬用字元的範例。*

**排除關鍵字**：使用破折號來搜尋不含關鍵字的資產。 例如， `running -shoe` 查詢傳回的資產包含 `running`，但不提供 `shoe`. 同樣地， `camp -night` 查詢傳回的資產包含 `camp` 但不是 `night`. 查詢 `camp-night` 傳回同時包含兩者的資產 `camp` 和 `night`.

![使用破折號來搜尋不包含排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)

*圖：使用破折號來搜尋不包含已排除關鍵字的資產。*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses Smart Tags. After configuring smart tagging functionality, follow these steps.

1. In [!DNL Experience Manager] CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your [!DNL Experience Manager] repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save the changes.

For related information, see [understand smart tags in Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, [!DNL Experience Manager Assets] offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. [!DNL Experience Manager] provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure [!DNL Experience Manager] to extract the text from the assets when users upload assets, such as PSD or PDF files. [!DNL Experience Manager] indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

### 用於篩選搜尋結果的自訂述詞 {#custompredicates}

述詞用於建立Facet。 管理員可以使用預先設定的述詞來自訂「篩選器」面板中的搜尋Facet。 這些述詞可使用覆蓋圖加以自訂。 另請參閱 [建立自訂述詞](/help/assets/search-facets.md).

您可以根據下列一或多個屬性來搜尋數位資產。 依預設，您可以對其中一些屬性套用篩選器，也可自訂建立其他某些篩選器以套用至其他屬性。

| 搜尋欄位 | 搜尋屬性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 類型 | 影像、檔案、多媒體、封存或其他。 |
| 上次修改時間 | 小時、日、周、月或年。 |
| 檔案大小 | 小、中、大。 |
| 發佈狀態 | 已發佈或已取消發佈。 |
| 已核准狀態 | 已核准或已拒絕。 |
| 方向 | 水準、垂直或正方形。 |
| 樣式 | 彩色或黑白。 |
| 視訊高度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊寬度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值會儲存在來源視訊的中繼資料和任何轉譯中。 |
| 視訊轉碼器 | x264。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊位元速率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音訊轉碼器 | Libvorbis、Lame MP3、AAC編碼。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音訊位元速率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |

## 使用資產搜尋結果 {#aftersearch}

您可以使用搜尋過的資產進行下列操作 [!DNL Experience Manager]：

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用「案頭動作」在案頭應用程式中開啟這些資產。
* 建立智慧型集合。
* 建立版本
* 啟動工作流程
* 建立資產關聯或取消關聯
* 使用執行搜尋後自動顯示的「篩選器」面板，套用篩選器以縮小搜尋結果。
* 導覽至資產位置

### 排序搜尋結果 {#sort}

排序搜尋結果以更快找到所需資產。 您可以在清單檢視中排序搜尋結果，而且只有在您選取 **[[!UICONTROL 檔案]](#searchui)** 從 **[!UICONTROL 篩選器]** 面板。 [!DNL Assets]使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產 (無論多少)。伺服器端排序比用戶端排序提供更快速且更精確的結果。

在清單檢視中，您可以排序搜尋結果，就像排序任何資料夾中的資產一樣。 排序功能適用於這些欄 — 名稱、標題、狀態、Dimension、大小、評等、使用狀況、（日期）建立時間、（日期）修改時間、（日期）發佈時間、工作流程和出庫。

如需排序功能的限制，請參閱 [限制](#limitations).

### 檢查資產的詳細資訊 {#checkinfo}

您可以從搜尋結果頁面中檢查已搜尋資產的詳細資訊。

若要檢視資產的所有中繼資料，請選取該資產並按一下 **[!UICONTROL 屬性]** 工具列中的。

若要檢查資產或資產版本記錄的註解，請按一下資產以開啟大型預覽。在左側導軌中開啟時間軸，並選取「 **[!UICONTROL 注釋]** 」或「 **[!UICONTROL 版本」]**。您也可以依時間順序將時間軸活動 (例如注釋或版本) 排序。

![排序搜尋資產的時間軸專案](assets/sort_timeline_search_results.gif)

*圖：排序搜尋資產的時間軸專案。*

### 下載搜尋的資產 {#download}

您可以下載搜尋的資產及其轉譯，就像從資料夾下載一般資產一樣。 從搜尋結果中選取一或多個資產，然後按一下 **[!UICONTROL 下載]** 工具列中的。

### 大量更新中繼資料屬性 {#metadata-updates}

您可以對多個資產的常見中繼資料欄位進行大量更新。 從搜尋結果中選取一或多個資產。 按一下 **[!UICONTROL 屬性]** ，並視需要更新中繼資料。 按一下 **[!UICONTROL 儲存並關閉]** 完成時。 更新欄位中先前存在的中繼資料會被覆寫。

若為可在單一資料夾或集合中使用的資產，將可更輕鬆進行 [大量更新中繼資料](/help/assets/manage-metadata.md#manage-assets-metadata) 而不使用搜尋功能。 對於跨資料夾可用的資產或符合共同條件的資產，透過搜尋大量更新中繼資料會更快一些。

### 智慧型集合 {#smart-collections}

集合是一組經過排序的資產，可以包含來自不同位置的資產，因為集合僅包含這些資產的參考。 集合分為以下兩種型別：

* 資產、資料夾和其他集合的靜態參考清單。
* 根據搜尋條件填入集合中資產的動態清單（智慧型集合）。

您可以根據搜尋准則建立智慧型系列。從「濾鏡 **[!UICONTROL 器]** 」面板中，選 **[!UICONTROL 擇「檔案]** 」並單 **[!UICONTROL 擊「保存智慧集」]**。請參閱 [管理系列](/help/assets/manage-collections.md)。

### 建立版本 {#create-version}

建立顯示在搜尋結果中的資產版本。 選取資產並按一下 **[!UICONTROL 建立]** > **[!UICONTROL 版本]**. 新增選用標籤或註解，然後按一下 **[!UICONTROL 建立]**. 您也可以選取多個資產，並同時為其建立版本。

### 建立工作流程 {#create-workflow}

與建立版本功能類似，您也可以為搜尋結果中顯示的資產建立工作流程。 選取資產並按一下 **[!UICONTROL 建立]** > **[!UICONTROL 工作流程]**. 選取工作流程模型，指定工作流程的標題，然後按一下 **[!UICONTROL 開始]**.

### 建立資產關聯及取消關聯 {#relate-unrelate-assets}

建立顯示在搜尋結果中的資產關聯及取消關聯。 選取資產並按一下 **[!UICONTROL 相關]** 或 **[!UICONTROL 取消關聯]**.

### 導覽至資產資料夾位置 {#navigate-asset-folder-location}

導覽至搜尋結果中所顯示資產的資料夾位置。 選取資產並按一下 **[!UICONTROL 顯示檔案位置]**.

## 未預期的搜尋結果和問題 {#unexpected-results}

<!--
**Partially related or unrelated search results**: Experience Manager may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| 錯誤、問題、症狀 | 可能的原因 | 對問題的可能修正或瞭解 |
|---|---|---|
| 搜尋缺少中繼資料的資產時，結果不正確。 | 搜尋缺少必要中繼資料的資產時， [!DNL Experience Manager] 可能會顯示某些具有有效中繼資料的資產。 結果是根據已編制索引的中繼資料屬性。 | 更新中繼資料後，需要重新索引以反映資產中繼資料的正確狀態。 另請參閱 [必要中繼資料](metadata-schemas.md#define-mandatory-metadata). |
| 搜尋結果太多。 | 廣泛搜尋引數。 | 考慮限制 [搜尋範圍](#scope). 使用智慧標籤可能會為您提供比您預期更多的搜尋結果。 另請參閱 [使用智慧標籤搜尋行為](#withsmarttags). |
| 不相關或部分相關的搜尋結果。 | 使用智慧標籤來變更搜尋行為。 | 瞭解 [搜尋在智慧型標籤後如何變更](#withsmarttags). |
| 沒有資產的自動完成建議。 | 新上傳的資產尚未編列索引。 當您開始在Omnisearch列中輸入搜尋關鍵字時，中繼資料無法立即作為建議使用。 | [!DNL Experience Manager] 會等到逾時期間到期（預設為一小時）後才執行背景工作，為所有新上傳或更新資產的中繼資料編制索引，然後將中繼資料新增到建議清單中。 |
| 沒有搜尋結果. | <ul><li>符合您查詢的資產不存在。 </li><li> 在搜尋查詢前新增空格。 </li><li> 不支援的中繼資料欄位包含您搜尋的關鍵字。</li><li> 在資產休假期間進行搜尋。 </li></ul> | <ul><li>使用不同的關鍵字進行搜尋。 或者，使用智慧標籤或相似性搜尋來改善搜尋結果。 </li><li>[已知限制](#limitations).</li><li>所有中繼資料欄位都不會考慮進行搜尋。 另請參閱 [範圍](#scope).</li><li>稍後搜尋或修改所需資產的開啟時間和關閉時間。</li></ul> |
| 無法使用搜尋篩選器或述詞。 | <ul><li>搜尋篩選器可能未設定。</li><li>無法供您的登入使用。</li><li>（不太可能）搜尋選項沒有在您使用的部署上自訂。</li></ul> | <ul><li>請聯絡管理員，檢查搜尋自訂專案是否可用。</li><li>請連絡系統管理員，檢查您的帳戶是否有使用自訂的許可權。</li><li>請聯絡管理員，並檢查以下專案的可用自訂專案： [!DNL Assets] 您正在使用的部署。</li></ul> |
| 搜尋視覺上相似的影像時，缺少預期的影像。 | <ul><li>影像在中無法使用 [!DNL Experience Manager].</li><li>影像未編列索引。 通常是在最近上傳時。</li><li>影像未使用智慧標籤。</li></ul> | <ul><li>將影像新增至 [!DNL Assets].</li><li>請聯絡您的管理員以重新索引存放庫。 此外，請確定您使用的是適當的索引。</li><li>請聯絡您的管理員，為相關資產設定智慧標籤。</li></ul> |
| 搜尋視覺上相似的影像時，會顯示不相關的影像。 | 視覺化搜尋行為。 | [!DNL Experience Manager] 會儘可能顯示潛在的相關資產。 將相關性較低的影像（如果有的話）新增到結果中，但搜尋排名較低。 當您向下捲動搜尋結果時，相符專案的品質和搜尋資產的相關性會降低。 |
| 選取並操作搜尋結果時，不會操作所有搜尋的資產。 | 此 [!UICONTROL 全選] 選項只會選取卡片檢視中的前100個搜尋結果，以及清單檢視中的前200個搜尋結果。 | |

**另請參閱**

* [搜尋最佳實務](search-best-practices.md)
* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜尋實作指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [提升搜尋結果的進階設定](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [設定智慧型翻譯搜尋](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)
