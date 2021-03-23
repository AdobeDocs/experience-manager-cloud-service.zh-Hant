---
title: 在 [!DNL Adobe Experience Manager]中搜尋數位資產和影像。
description: 瞭解如何使用「篩選器」面板在 [!DNL Adobe Experience Manager] 中尋找所需資產，以及如何使用顯示在搜尋中的資產。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0e5d49b8781ebe0c5785a14800bcaec223da809c
workflow-type: tm+mt
source-wordcount: '4755'
ht-degree: 5%

---


# 在[!DNL Adobe Experience Manager] {#search-assets-in-aem}中搜尋資產

[!DNL Adobe Experience Manager Assets] 提供強穩的資產搜尋方法，協助您提高內容速度。您的團隊可運用現成可用的功能和自訂方法，以順暢、智慧的搜尋體驗縮短上市時間。 搜尋資產是數位資產管理系統的核心使用，不論是供創意人員進一步使用、由商業使用者和行銷人員強穩管理資產，或由DAM管理員管理。 您可透過[!DNL Assets]使用者介面或其他應用程式和介面執行簡單、進階和自訂的搜尋，以協助您完成這些使用案例。

[!DNL Experience Manager Assets] 支援下列使用案例，而本文則說明這些使用案例的使用、概念、設定、限制和疑難排解。

| 搜尋資產 | 配置和管理搜索功能 | 使用搜尋結果 |
|---|---|---|
| [基本搜尋](#searchbasics) | [搜尋索引](#searchindex) | [排序結果](#sort) |
| [瞭解搜尋UI](#searchui) | [文字擷取](#extracttextupload) | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必備中繼資料](#mandatorymetadata) | [下載](#download) |
| [瞭解搜尋結果和行為](#searchbehavior) | [修改搜尋刻面](#searchfacets) | [大量中繼資料更新](#metadataupdates) |
| [搜尋排名與提升](#searchrank) | [自訂謂語](#custompredicates) | [智慧型系列](#collections) |
| [進階搜尋：篩選和搜尋範圍](#scope) |  | [瞭解並疑難排解意外結果](#unexpectedresults) |
| [從其他解決方案和應用程式搜尋](#beyondomnisearch):<ul><li>[Adobe資產連結](#aal)</li><li>[品牌入口網站](#brand-portal)</li><li>[Experience Manager案頭應用程式](#desktop-app)</li><li>[Adobe Stock影像](#adobe-stock)</li><li>[Dynamic Media資產](#search-dynamic-media-assets)</li></ul> |  |  |
| [資產選擇器](#assetselector) |  |  |
| [限](#tips) 制和提 [示](#limitations) |  |  |
| [圖示範例](#samples) |  |  |

使用[!DNL Experience Manager]網頁介面頂端的Omnisearch欄位搜尋資產。 前往[!DNL Experience Manager]中的&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**，按一下頂端列中的![search_icon](assets/do-not-localize/search_icon.png)，輸入搜尋關鍵字，然後選取`Return`。 或者，使用關鍵字快速鍵`/`（正斜線）來開啟Omnisearch欄位。 `Location:Assets` 已預先選取，以限制搜尋DAM資產。[!DNL Experience Manager] 在您開始輸入搜尋關鍵字時提供建議。

使用&#x200B;**[!UICONTROL Filters]**&#x200B;面板來搜尋資產、資料夾、標籤和中繼資料。 您可以根據各種選項（謂語）來篩選搜尋結果，例如檔案類型、檔案大小、上次修改日期、資產狀態、前瞻分析資料和Adobe Stock授權。 您可以使用[search facets](/help/assets/search-facets.md)自訂「篩選」面板並新增或移除搜尋謂語。 [!UICONTROL Filters]面板中的[!UICONTROL File Type]篩選器具有混合狀態複選框。 因此，除非選擇所有嵌套的謂語（或格式），否則第一級複選框將被部分選中。

[!DNL Experience Manager] 搜尋功能支援搜尋系列和搜尋系列中的資產。請參閱[搜尋系列](/help/assets/manage-collections.md)。

## 瞭解搜索介面{#searchui}

熟悉搜尋介面和可用動作。

![瞭解Experience Manager資產搜尋結果介面](assets/aem_search_results.png)

*圖：瞭解 [!DNL Experience Manager Assets] 搜尋結果介面。*

**A.將搜** 尋儲存為智慧型系列。**B.篩** 選或謂語以縮小搜尋結果。**C.** 顯示檔案、檔案夾或兩者。**D.** 按一下「篩選器」以開啟或關閉左側邊欄。**E.** 搜尋位置為 DAM。**F.** Omnisearch欄位，包含使用者提供的搜尋關鍵字。**G.選** 擇載入的搜尋結果。**H.** 在總搜索結果中顯示的搜索結果數。**I.關** 閉搜尋。**J.** 在卡片檢視和清單檢視之間切換。

### 動態搜尋Facet {#dynamicfacets}

您可以使用搜尋Facet中動態更新的預期搜尋結果數目，更快地從搜尋結果頁面發現所需資產。 預期的資產數目會在套用搜尋篩選之前更新。 查看篩選的預期計數有助於您快速且有效地瀏覽搜尋結果。

![在搜尋Facet中檢視資產的概約數目，而不篩選搜尋結果。](assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋Facet中檢視資產的概約數目，而不篩選搜尋結果。*

## 鍵入{#searchsuggestions}時搜尋建議

當您開始輸入關鍵字時，建議AEM可能的搜尋關鍵字或片語。 建議以中的資產為基礎AEM。 索引AEM所有中繼資料欄位，以協助搜尋。 為提供搜尋建議，系統會使用下列數個中繼資料欄位的值。 若要提供搜尋建議，請考慮將適當的關鍵字填入下列欄位：

* 資產標籤。 （映射至`jcr:content/metadata/cq:tags`）
* 資產標題。 （映射至`jcr:content/metadata/dc:title`）
* 資產說明。 （映射至`jcr:content/metadata/dc:description`）
* JCR資料庫中的標題。 值可能會對應至資產標題。 （映射至`jcr:content/jcr:title`）
* JCR儲存庫中的說明。 值可能會對應至資產說明。 （映射至`jcr:content/jcr:description`）

## 瞭解搜尋結果和行為{#searchbehavior}

### 基本搜尋詞和結果{#searchbasics}

您可以從OmniSearch欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，而且是全文搜尋（跨常用中繼資料欄位）。 如果使用多個關鍵字，則`AND`是關鍵字之間的預設運算子。

結果會依相關性排序，從最接近的相符項目開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含兩個詞語的資產。 在中繼資料中，顯示為智慧標籤的關鍵字比顯示在其他中繼資料欄位中的關鍵字的排名更高。 [!DNL Experience Manager] 允許賦予特定搜尋詞更高的權重。此外，還可以將特定搜尋詞之少數目標資產的排名[提高。](#searchrank)

為快速找到相關資產，豐富式介面提供篩選、排序和選擇機制。 您可以根據多個條件來篩選結果，並查看搜尋的資產數目，以找出各種篩選條件。 或者，您也可以在Omnisearch欄位中變更查詢，以重新執行搜尋。 當您變更搜尋詞或篩選器時，其他篩選器仍會套用，以保留您搜尋的上下文。

當結果為許多資產時，[!DNL Experience Manager]會在卡片檢視中顯示前100個，在清單檢視中顯示200個。 當使用者捲動時，會載入更多資產。 這是為了改善效能。 觀看顯示[資產數目](https://www.youtube.com/watch?v=LcrGPDLDf4o)的影片展示。

有時候，您會在搜尋結果中看到一些非預期的資產。 如需詳細資訊，請參閱[未預期的結果](#unexpectedresults)。

可以AEM搜索許多檔案格式，並且可以自定義搜索篩選器以滿足您的業務要求。 請洽詢您的管理員，以瞭解您的DAM儲存庫有哪些搜尋選項，以及您的登入可能有哪些限制。

<!-- 
### Results with and without Enhanced Smart Tags {#withsmarttags}

By default, AEM search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### 搜尋排名與提升{#searchrank}

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 在各種中繼資料欄位中符合`woman running`。
1. 在智慧型標籤中符合`woman running`。
1. 在智慧標籤中符合`woman`或`running`。

您可以改善特定資產的關鍵字關聯性，以協助根據關鍵字提高搜尋效率。 換言之，當您根據這些關鍵字進行搜尋時，您促銷特定關鍵字的影像會出現在搜尋結果的頂端。

1. 從[!DNL Assets]使用者介面，開啟資產的屬性頁面。 按一下「**[!UICONTROL Advanced]**」，然後按一下「**[!UICONTROL Elevate for search keywords]**」下方的「新增&#x200B;]**」。**[!UICONTROL 
1. 在&#x200B;**[!UICONTROL 搜尋促銷]**&#x200B;方塊中，指定您要加大影像搜尋的關鍵字，然後按一下&#x200B;**[!UICONTROL 新增]**。 您可以以相同的方式指定多個關鍵字。
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。您為此關鍵字促銷的資產會出現在熱門搜尋結果中。

您可以透過提升目標關鍵字搜尋結果中某些資產的排名，來利用此功能。 請參閱以下範例影片。 如需詳細資訊，請參閱Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)中的[搜尋。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*影片：瞭解搜尋結果的排名方式，以及排名的影響。*

## 進階搜尋{#scope}

提AEM供各種方法，例如套用至已搜尋資產的篩選，以協助您更快找到所需資產。 以下說明一些常用的方法。 以下共用了一些[示例](#samples)。

**搜索檔案或資料夾**:在搜索結果中，查看檔案、資料夾或兩者。從&#x200B;**[!UICONTROL Filters]**&#x200B;面板中，您可以選擇適當的選項。 請參閱[search interface](#searchui)。

**在資料夾中搜尋資產**:您可以將搜尋限制在特定資料夾。在&#x200B;**[!UICONTROL Filters]**&#x200B;面板中，新增資料夾路徑。 一次只能選擇一個資料夾。

![在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中](assets/search_folder_select.gif)

在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Adobe Stock影像{#adobe-stock}

在使用者介AEM面中，使用者可搜尋[Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md)並授權所需資產。 在Omnisearch列中新增`Location: Adobe Stock`。 您也可以使用「篩選」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。

### Dynamic Media資產{#dmassets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」>「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。

### 在元資料欄位{#gql-search}中使用特定值進行GQL搜索

您可以根據中繼資料欄位的確切值來搜尋資產，例如標題、說明和製作程式。 GQL全文搜索功能僅提取那些元資料值與搜索查詢完全匹配的資產。 屬性的名稱（建立者、標題等）和值區分大小寫。

| 中繼資料欄位 | Facet值與使用 |
|---|---|
| 標題 | 標題：John |
| 產生器 | 建立者：John |
| 位置 | 位置： NA |
| 說明 | 說明：「範例影像」 |
| 製作工具 | 創作工具：「Adobe Photoshop CC2015」 |
| 版權擁有者 | 版權人：「Adobe Systems」 |
| 參與者 | 投稿人：John |
| 使用條款 | 使用條款：「保留CopyRights」 |
| 建立日期 | 已建立：YYYY-MM-DDTHH |
| 到期日 | 過期：YYYY-MM-DDTHH |
| 準時 | ontime:YYYY-MM-DDTHH |
| 關閉時間 | offtime:YYYY-MM-DDTHH |
| 時間範圍（過期的dateontime,offtime） | facet欄位：下限……上界 |
| 路徑 | /content/dam/&lt;資料夾名稱> |
| PDF 標題 | pdftitle:&quot;Adobe檔案&quot; |
| 主旨 | 主旨：「訓練」 |
| 標記 | 標籤：「位置與旅行」 |
| 類型 | 類型：&quot;image\png&quot; |
| 影像寬度 | width:lowberbound..上界 |
| 影像高度 | 高度：下限。上界 |
| 人員 | 人：John |

屬性`path`、`limit`、`size`和`orderby`不能與任何其他屬性搭配使用。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

使用者產生屬性的關鍵字是屬性編輯器中的小寫欄位標籤，並移除空格。

以下是複雜查詢的搜尋格式範例：

* 若要顯示具有多個刻面欄位的所有資產(例如：title=John Doe和創作工具=Adobe Photoshop):`title:"John Doe" creatortool : Adobe*`
* 若要在Facet值不是單字而是句子時顯示所有資產(例如：title=Scott Reynolds):`title:"Scott Reynolds"`
* 若要顯示具有單一屬性多個值的資產(例如：title=Scott Reynolds或John Doe):`title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產(例如：標題是Scott Reynolds):`title:Scott*`
* 若要顯示屬性值以特定字串結尾的資產(例如：標題是Scott Reynolds):`title:*Reynolds`
* 若要顯示包含特定字串的屬性值的資產(例如：標題=巴塞爾會議室):`title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如：在具有title=John Doe的資產中搜尋字串Adobe):`*Adobe* title:"John Doe"`

## 從其他產AEM品或介面搜尋資產{#beyondomnisearch}

Adobe Experience Manager(AEM)將DAM存放庫與各種其他解決方案連AEM接，讓您更快速存取數位資產並簡化創意工作流程。 任何資產搜尋都從瀏覽或搜尋開始。 在不同的曲面和解決方案上，搜索行為基本保持不變。 有些搜尋方法會隨著目標對象、使用案例和使用者介面而改變，而且各解決方案的使用者介AEM面也不同。 以下連結說明個別解決方案的特定方法。 本文將說明普遍適用的提示和行為。

### 從「Adobe資產連結」面板{#aal}搜尋資產

使用Adobe資產連結，創意專業人員現在可以存取儲存在AEM Assets的內容，而不需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用Creative Cloud應用程式中的應用程式內面板，順暢地瀏覽、搜尋、結帳和登入資產：Photoshop,Illustrator和InDesign。 資產連結也可讓使用者搜尋視覺上類似的結果。 視覺搜尋顯示結果採用Adobe Sensei的機器學習演算法，並協助使用者尋找美學上類似的影像。 請參閱使用Adobe資產連結搜尋及瀏覽資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)。[

### 在Experience Manager案頭應用程式{#desktop-app}中搜尋資產

創意專業人員使用案頭應用程式，讓AEM Assets可輕鬆搜尋，並可在其本機案頭（Win或Mac）上使用。 創意人員可以輕鬆地在Mac Finder或Windows檔案總管中顯示所需資產、在案頭應用程式中開啟，並在本機進行變更——這些變更會儲存回儲存庫中建立AEM的新版本。 應用程式支援使用一或多個關鍵字*和？的基本搜尋 萬用字元和AND運算子。 請參閱案頭應用程式中的[瀏覽、搜尋和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。

### 在品牌入口網站{#brand-portal}中搜尋資產

業務線使用者和行銷人員使用品牌入口網站，以有效且安全的方式與延伸的內部團隊、合作夥伴和經銷商共用經過核准的數位資產。 請參閱品牌入口網站上的[搜尋資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html)。

### 搜尋Adobe Stock影像{#adobe-stock2}

在使用者介AEM面中，使用者可搜尋Adobe Stock資產並授權所需資產。 在Omnisearch欄位中新增`Location: Adobe Stock`。 您也可以使用&#x200B;**[!UICONTROL Filters]**&#x200B;面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。 請參閱[管理](/help/assets/aem-assets-adobe-stock.md#usemanage)中的AEMAdobe Stock映像。

### 搜尋Dynamic Media資產{#search-dynamic-media-assets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。在製作網頁時，作者可在內容尋找工具中搜尋集合。集合的篩選器可從快顯功能表中取得。

### 在製作網頁{#contentfinder}時，在Content Finder中搜尋資產

作者可以使用Content Finder搜尋DAM儲存庫中的相關資產，並使用他們建立的網頁中的資產。

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### 搜尋系列{#collections}

搜AEM尋功能支援搜尋系列和搜尋系列中的資產。 請參閱[搜尋系列](/help/assets/manage-collections.md)。

## 資產選擇器{#assetselector}

資產選擇器可讓您以特殊方式搜尋、篩選及瀏覽DAM資產。 資產選擇器位於`https://[aem_server]:[port]/aem/assetpicker.html`。 您可以使用資產選擇器擷取所選資產的中繼資料。 您可以使用支援的請求參數來啟動它，例如資產類型（影像、視訊、文字）和選擇模式（單選或多選）。 這些參數會為特定搜尋例項設定資產選取器的上下文，並在整個選取範圍內保持不變。

資產選擇器使用HTML5 `Window.postMessage`訊息，將所選資產的資料傳送給收件者。 資產選擇器是以Granite的基礎選擇器辭彙為基礎。 依預設，資產選擇器會在「瀏覽」模式中運作。

您可以在URL中傳遞下列請求參數，以在特定內容中啟動資產選擇器：

| 名稱 | 值 | 範例 | 目的 |
|---|---|---|---|
| 資源尾碼(B) | URL中作為資源尾碼的資料夾路徑：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 若要啟動已選取特定資料夾的資產選擇器，例如已選取資料夾/content/dam/we-retail/en/activity,URL應為：[https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在啟動資產選擇器時需要選取特定資料夾，請將其作為資源尾碼傳遞。 |
| 模式 | 單一，多重 | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | 在多個模式中，您可以使用資產選擇器同時選取多個資產。 |
| mimetype | 資產的mimetype(s)(`/jcr:content/metadata/dc:format`)（也支援萬用字元） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | 使用它以MIME類型篩選資產 |
| 對話方塊 | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些參數將資產選擇器開啟為「花崗岩」對話方塊。 只有當您透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時，此選項才適用。 |
| assettype(S) | 影像、檔案、多媒體、封存 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用這個選項可根據傳遞的值來篩選資產類型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | 使用此選項可指定資產選擇器的根資料夾。 在這種情況下，資產選擇器可讓您只選取根資料夾下的子資產（直接／間接）。 |

若要存取資產選擇器介面，請前往`https://[aem_server]:[port]/aem/assetpicker`。 導覽至所要的檔案夾，並選取一或多個資產。 或者，從Omnisearch方塊中搜尋所要的資產、視需要套用篩選，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/assetpicker.png)

*圖：在資產選擇器中瀏覽並選取資產。*

## 限制 {#limitations}

[!DNL Experience Manager Assets]中的搜索功能有以下限制：

* 請勿在搜索查詢中輸入前導空格，否則搜索無效。
* [!DNL Experience Manager] 在您從搜尋結果中選取資產屬性，然後取消搜尋後，可能會繼續顯示搜尋詞。  <!-- (CQ-4273540) -->
* 搜索資料夾或檔案和資料夾時，不能對任何參數對搜索結果進行排序。
* 如果您選擇`Return`而未在Omnisearch列中鍵入， [!DNL Experience Manager]將返回僅檔案而非資料夾的清單。 如果您不使用關鍵字而專門搜索資料夾，[!DNL Experience Manager]不會返回任何結果。
* 您可以對資料夾執行全文搜尋。 指定搜尋詞，讓搜尋生效。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋最適合大型儲存庫。 雖然沒有最佳結果所需的影像數量下限，但少數影像的比對品質可能不如大型儲存庫中的比對品質好。
* 您無法變更模型或訓練[!DNL Experience Manager]以尋找類似的影像。 例如，新增或移除智慧標籤至少數資產並不會變更模型。 資產確實會從視覺上類似的搜尋結果中排除。

搜尋功能在下列情況下可能會有效能限制：

* 與清單檢視相比，卡片檢視的載入時間更快，可顯示搜尋結果。

## 搜尋提示{#tips}

* 監控資產的審閱狀態時，請使用適當的選項來尋找已核准的資產或待核准的資產。
* 使用「前瞻分析」述詞，根據從各種Creative應用程式取得的資產使用統計資料來搜尋支援的資產。 使用資料會分組在資產顯示類別的「使用分數」、「印象」、「點按」和「媒體」渠道下。
* 使用&#x200B;**[!UICONTROL 選取全部]**&#x200B;核取方塊來選取搜尋的資產。 [!DNL Experience Manager] 一開始會在卡片檢視中顯示100個資產，在清單檢視中顯示200個資產。當您捲動搜尋結果時，會載入更多資產。 您可以選取比載入資產更多的資產。 選取資產的計數會顯示在搜尋結果頁面的右上角。 您可以對選取範圍進行操作，例如下載選取的資產、大量更新選取資產的中繼資料屬性，或將選取的資產新增至系列。 選取的資產比顯示的資產多時，會對所有選取的資產套用動作，或對話方塊顯示套用的資產數。 若要將動作套用至未載入的資產，請確定已明確選取所有資產。
* 若要搜尋不含必要中繼資料的資產，請參閱[必要中繼資料](#mandatorymetadata)。
* 搜尋使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為獲得更佳結果，請使用雙引號（非單引號），或確保數字與沒有特殊字元的單字相鄰（例如`shoe12`）。
* 全文搜索支援`-`和`^`等運算子。 要將這些字母作為字串文本搜索，請用雙引號將搜索表達式括起來。 例如，請使用`"Notebook - Beauty"`取代`Notebook - Beauty`。
* 如果搜尋結果太多，請將所要資產的搜尋範圍限制為[](#scope)為零。 當您對如何更好地尋找所需資產（例如特定檔案類型、特定位置、特定中繼資料等）有一些概念時，效果最佳。

* **標籤**:標籤可協助您將可以更有效率地瀏覽和搜尋的資產分類。標籤有助於將適當的分類傳播給其他用戶和工作流。 [!DNL Experience Manager] 提供使用Adobe Sensei人為智慧型服務自動標籤資產的方法，讓您在使用和訓練中更能標籤資產。當您搜尋資產時，如果您的帳戶已啟用功能，智慧標籤會加入。 它可與內建搜尋功能搭配使用。 請參閱[搜尋行為](#searchbehavior)。 若要最佳化搜尋結果的顯示順序，您可以[提升少數選取資產的搜尋排名](#searchrank)。

* **索引**:搜尋結果中只會傳回已建立索引的中繼資料和資產。為了獲得更好的覆蓋面和效能，請確保正確編製索引並遵循最佳做法。 請參閱[索引](#searchindex)。

## 一些示例說明搜索{#samples}

在關鍵字周圍使用雙引號，以尋找包含使用者指定之確切順序之確切片語的資產。

![使用引號和不使用引號的搜尋行為](assets/search_with_quotes.gif)

*圖：搜尋行為時有引號或無引號。*

**使用星號通配符進行搜索**:若要擴大搜尋範圍，請在搜尋字詞前後使用星號，以比對任意數目的字元。例如，搜尋沒有星號的執行並不會傳回包含字詞變異的資產（包括在中繼資料中）。 星號可取代任意數字元。 例如，

* `run` 返回正確執行關鍵字的資產
* `run*` 傳回資產，包括執行、執行、逃跑等。
* `*run` 傳回Outrun、重新執行等。
* `*run*` 傳回所有可能的組合。

![以範例說明在資產搜尋中使用星號萬用字元](assets/search_with_asterisk_run.gif)

*圖：以範例說明在資產搜尋中使用星號萬用字元。*

**使用問號萬用字元搜尋**:若要擴大搜尋範圍，請使用一或多個「?」字元來比對字元數目。 例如，在下圖中，

* `run???` 查詢不符合任何資產。

* `run????` query與後4個字 `running` 元的字詞相符 `run`。

* `??run` query與之前包含 `rerun` 兩個字元的字詞相 `run`符。

![使用範例說明在資產搜尋中使用問號萬用字元](assets/search_with_questionmark_run.gif)

*圖：以範例說明在資產搜尋中使用問號萬用字元。*

**排除關鍵字**:使用破折號來搜尋不含關鍵字的資產。例如，`running -shoe`查詢會傳回包含`running`但不包含`shoe`的資產。 同樣地，`camp -night`查詢會傳回包含`camp`但不包含`night`的資產。 查詢`camp-night`會傳回同時包含`camp`和`night`的資產。

![使用破折號來搜尋不含已排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)

*圖：使用破折號來搜尋不含已排除關鍵字的資產。*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tags. After configuring smart tagging functionality, follow these steps.

1. In AEM CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html?lang=en#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save all the changes.

For related information, see [understand smart tags in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, AEM Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. AEM provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure AEM to extract the text from the assets when users upload assets, such as PSD or PDF files. AEM indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

<!-- TBD: Check with gklebus and engineering if these customization are possible in CS.

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| Approved Status | Approved or Rejected. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| File Size | Small, Medium, or Large. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Orientation | Horizontal, Vertical, or Square. |
| Publish Status | Published or Unpublished. |
| Style | Color, or Black & White. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## 使用資產搜尋結果{#aftersearch}

您可以對在[!DNL Experience Manager]中搜尋的資產執行下列動作：

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用「案頭動作」在案頭應用程式中開啟這些資產。
* 建立智慧型系列。

### 對搜索結果{#sort}排序

對搜尋結果排序，以更快發現所需資產。 只有當您從&#x200B;**[!UICONTROL Filters]**&#x200B;面板中選擇&#x200B;**[[!UICONTROL Files]](#searchui)**&#x200B;時，才能在清單視圖中對搜索結果進行排序。 [!DNL Assets]使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產 (無論多少)。伺服器端排序比用戶端排序提供更快速且更精確的結果。

在清單檢視中，您可以像排序任何資料夾中的資產一樣，對搜尋結果進行排序。 排序適用於這些列— 「名稱」、「標題」、「狀態」、「Dimension」、「大小」、「評級」、「使用」、「（建立日期）」、「（修改日期）」、「（發佈日期）」、「工作流」和「簽出」。

有關排序功能的限制，請參見[limitations](#limitations)。

### 檢查資產{#checkinfo}的詳細資訊

您可以從搜尋結果頁面檢查搜尋資產的詳細資訊。

若要查看資產的所有中繼資料，請選取資產，然後從工具列按一下&#x200B;**[!UICONTROL 屬性]**。

若要檢查資產或資產版本記錄的註解，請按一下資產以開啟大型預覽。在左側導軌中開啟時間軸，並選取「 **[!UICONTROL 注釋]** 」或「 **[!UICONTROL 版本」]**。您也可以依時間順序將時間軸活動 (例如注釋或版本) 排序。

![排序搜尋資產的時間軸項目](assets/sort_timeline_search_results.gif)

*圖：排序搜尋資產的時間軸項目。*

### 下載搜尋的資產{#download}

您可以從資料夾下載搜尋的資產及其轉譯，就像下載一般資產一樣。 從搜尋結果中選取一或多個資產，然後從工具列按一下「下載&#x200B;**[!UICONTROL 」。]**

### 大量更新中繼資料屬性{#metadataupdates}

您可大量更新多個資產的常用中繼資料欄位。 從搜尋結果中，選取一或多個資產。 從工具列按一下「**[!UICONTROL 屬性]**」，並視需要更新中繼資料。 完成時，按一下「保存並關閉」。 ****&#x200B;會覆寫更新欄位中先前存在的中繼資料。

對於單一資料夾或系列中可用的資產，[較容易批量](/help/assets/manage-metadata.md#manage-assets-metadata)更新中繼資料，而不需使用搜尋功能。 對於跨資料夾可用或符合一般准則的資產，透過搜尋大量更新中繼資料會更快速。

### 智慧型系列{#collections-1}

系列是一組有序的資產，可包含不同位置的資產，因為系列僅包含這些資產的參考。 系列有下列兩種類型：

* 資產、檔案夾和其他系列的靜態參考清單。
* 動態清單（智慧型系列），會根據搜尋准則填入系列中的資產。

您可以根據搜尋准則建立智慧型系列。從「濾鏡 **[!UICONTROL 器]** 」面板中，選 **[!UICONTROL 擇「檔案]** 」並單 **[!UICONTROL 擊「保存智慧集」]**。請參閱 [管理系列](/help/assets/manage-collections.md)。

## 未預期的搜尋結果和問題{#unexpectedresults}

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| 錯誤、問題、症狀 | 可能的原因 | 可能修正或瞭解問題 |
|---|---|---|
| 搜尋遺失中繼資料的資產時，結果不正確。 | 在搜尋遺失必要中繼資料的資產時，[!DNL Experience Manager]可能會顯示某些具有有效中繼資料的資產。 結果基於索引元資料屬性。 | 更新中繼資料後，需要重新建立索引，以反映資產中繼資料的正確狀態。 請參閱[必備中繼資料](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜尋結果太多。 | 廣泛的搜尋參數。 | 考慮限制搜索範圍[](#scope)。 使用智慧型標籤可能會提供比預期更多的搜尋結果。 請參閱[智慧型標籤的搜尋行為](#withsmarttags)。 |
| 不相關或部分相關的搜尋結果。 | 使用智慧標籤來變更搜尋行為。 | 瞭解智慧標籤[後搜尋的變更。](#withsmarttags) |
| 沒有資產的自動完成建議。 | 新上傳的資產尚未建立索引。 當您開始在Omnisearch列中輸入搜尋關鍵字時，中繼資料無法立即當做建議使用。 | [!DNL Assets] 等到逾時期間（預設為一小時）到期後，執行背景工作，為所有新上傳或更新的資產建立中繼資料索引，然後將中繼資料新增至建議清單。 |
| 沒有搜尋結果. | <ul><li>符合查詢的資產不存在。 </li><li> 在搜尋查詢前新增空白字元。 </li><li> 不支援的中繼資料欄位包含您搜尋的關鍵字。</li><li> 在資產的離職期間進行搜尋。 </li></ul> | <ul><li>使用不同關鍵字進行搜尋。 或者，使用智慧標籤或相似性搜尋來改善搜尋結果。 </li><li>[已知限制](#limitations)。</li><li>所有中繼資料欄位都不會被視為搜尋。 請參閱[scope](#scope)。</li><li>稍後搜尋或修改所需資產的準時和非時。</li></ul> |
| 搜尋篩選器或謂語不可用。 | <ul><li>搜尋篩選器未設定。</li><li>登入時無法使用。</li><li>（不太可能）您使用的部署不會自訂搜尋選項。</li></ul> | <ul><li>請連絡管理員以檢查搜尋自訂是否可用。</li><li>請連絡管理員以檢查您的帳戶是否具有使用自訂的權限。</li><li>請聯絡管理員，並檢查您使用的[!DNL Assets]部署的可用自訂項目。</li></ul> |
| 在搜尋視覺上類似的影像時，會遺失預期的影像。 | <ul><li>影像在[!DNL Experience Manager]中無法使用。</li><li>未對影像編製索引。 通常是在最近上傳時。</li><li>影像未標籤智慧型。</li></ul> | <ul><li>將影像新增至[!DNL Assets]。</li><li>請與管理員聯繫以重新為儲存庫編製索引。 此外，請確定您使用的是適當的索引。</li><li>請洽詢您的管理員，以智慧標籤相關資產。</li></ul> |
| 當搜尋視覺上類似的影像時，會顯示不相關的影像。 | 視覺搜尋行為。 | [!DNL Experience Manager] 顯示盡可能多的潛在相關資產。較不相關的影像（如果有）會新增至結果，但搜尋排名較低。 當您向下捲動搜尋結果時，相符項目的品質和搜尋資產的相關性會降低。 |
| 在選取並操作搜尋結果時，不會對所有搜尋的資產進行操作。 | [!UICONTROL 選擇全部]選項僅在卡片視圖中選擇前100個搜索結果，在清單視圖中選擇前200個搜索結果。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜尋實作指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [進階設定可大幅提升搜尋結果](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [配置智慧翻譯搜索](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

