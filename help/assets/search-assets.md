---
title: 在AEM中搜尋數位資產和影像
description: 瞭解如何使用「篩選」面板在AEM中尋找所需資產，以及如何使用顯示在搜尋中的資產。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7317a5db6ed348f99b2290d72ddf6e540fae5456
workflow-type: tm+mt
source-wordcount: '4529'
ht-degree: 7%

---


# 在AEM中搜尋資產 {#search-assets-in-aem}

您可以使用Experience Manager中方便使用的資產搜尋選項，以提高內容速度。 您的團隊可運用現成可用的功能和自訂方法，以順暢、智慧的搜尋體驗縮短上市時間。 搜尋資產是數位資產管理系統的核心使用，不論是供創意人員進一步使用、由商業使用者和行銷人員強穩管理資產，或由DAM管理員管理。 您可透過AEM Assets使用者介面或其他應用程式和介面執行簡單、進階和自訂的搜尋，以協助您完成這些使用案例。

AEM支援下列使用案例，而本文則說明這些使用案例的使用、概念、設定、限制和疑難排解。

| 搜尋資產 | 配置和管理 | 使用搜尋結果 |
|--- |--- |--- |
| [基本搜尋](#searchbasics) | [搜尋索引](#searchindex) | [排序結果](#sort) |
| [瞭解搜尋UI](#searchui) |  | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必備中繼資料](#mandatorymetadata) | [下載](#download) |
| [瞭解搜尋結果和行為](#searchbehavior) | [修改搜尋刻面](#searchfacets) | [大量中繼資料更新](#metadataupdates) |
| [搜尋排名與提升](#searchrank) | [文字擷取](#extracttextupload) | [智慧型系列](#collections) |
| [進階搜尋： 篩選和搜尋範圍](#scope) | [自訂謂語](#custompredicates) | [瞭解意外結果](#unexpectedresults) ，並疑難排 [解](#troubleshoot) |
| [從其他解決方案和應用程式搜尋](#beyondomnisearch): <br />     [Asset Link](#aal) <br />[Desktop應用程式](#desktopapp) <br />     [Adobe Stock影像](#adobestock) <br />     [動態媒體資產](#dynamicmedia) |  |  |
| [資產選擇器／選擇器](#assetselector) |  |  |
| [限制](#tips) 和提 [示](#limitations) |  |  |
| [圖示範例](#samples) |  |  |

使用AEM網頁介面頂端的Omnisearch欄位來搜尋資產。 前往「 **[!UICONTROL Assets]** > **[!UICONTROL Files]** in AEM」(資產 ![> AEM中的檔案)，按一下頂端列的](assets/do-not-localize/search_icon.png) search_icon，輸入search關鍵字，然後按return。 或者，使用關鍵字快速鍵( `/` 正斜線)來開啟Omnisearch欄位。 `Location:Assets` 已預先選取，以限制搜尋DAM資產。 您可以執行進階搜尋，以增加或限 [制搜尋範圍](#scope)。

使用「 **[!UICONTROL 篩選]** 」面板來搜尋資產、資料夾、標籤和中繼資料。 您可以根據各種選項（謂語）來篩選搜尋結果，例如檔案類型、檔案大小、上次修改的日期、資產狀態、前瞻分析資料和Adobe Stock授權。 您可以自訂「篩選」面板，並使用搜尋Facet新增／移除搜尋 [謂語](/help/assets/search-facets.md)。

AEM搜尋功能支援搜尋系列並搜尋系列中的資產。 請參閱 [搜尋系列](/help/assets/manage-collections.md)。

## 瞭解搜尋介面 {#searchui}

熟悉搜尋介面和可用動作。

![瞭解資產搜尋結果介面的部分](assets/aem_search_results.png)*圖：* 瞭解Assets搜尋結果介面的部分

**A.** 將搜尋儲存為智慧型集合。**B.** 用來縮減搜尋結果的篩選器 (述詞)。**C.** 在搜索結果中顯示檔案和 (或) 資料夾。**D.** 按一下「篩選器」以開啟或關閉左側邊欄。**E.** 搜尋位置為 DAM。**F.** 已由使用者提供搜尋關鍵字的 Omnisearch 欄位 **G.** 用來選取所有搜索結果的核取方塊 **H.** 搜尋結果總數中顯示的搜尋結果數目 **I.** 關閉搜尋 **J.** 在卡片檢視與清單檢視之間切換

### 動態搜尋Facet {#dynamicfacets}

您可以使用搜尋Facet中動態更新的預期搜尋結果數目，更快地從搜尋結果頁面發現所需資產。 預期的資產數目會在套用搜尋篩選之前更新。 查看篩選的預期計數有助於您快速且有效地瀏覽搜尋結果。 如需詳細資訊，請參閱「 [在AEM中搜尋資產」](/help/assets/search-assets.md)。

![在搜尋Facet中檢視資產的概約數目，而不篩選搜尋結果。](assets/asset_search_results_in_facets_filters.png)

在搜尋Facet中檢視資產的概約數目，而不篩選搜尋結果。

## 在您輸入時搜尋建議 {#searchsuggestions}

當您開始輸入關鍵字時，AEM會建議可能的搜尋關鍵字或片語。 建議是以AEM中的資產為基礎。 AEM為所有中繼資料欄位建立索引，以協助搜尋。 為提供搜尋建議，系統會使用下列數個中繼資料欄位的值。 若要提供搜尋建議，請考慮將適當的關鍵字填入下列欄位：

* 資產標籤。 (映射至 `jcr:content/metadata/cq:tags`)
* 資產標題。 (映射至 `jcr:content/metadata/dc:title`)
* 資產說明。 (映射至 `jcr:content/metadata/dc:description`)
* JCR資料庫中的標題。 值可能會對應至資產標題。 (映射至 `jcr:content/jcr:title`)
* JCR儲存庫中的說明。 值可能會對應至資產說明。 (映射至 `jcr:content/jcr:description`)

## 瞭解搜尋結果和行為 {#searchbehavior}

### 基本搜尋詞和結果 {#searchbasics}

您可以從OmniSearch欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，且是全文搜尋（跨常用中繼資料欄位）。 如果使用多個關鍵字，則 `AND` 是關鍵字之間的預設運算元。 結果會依相關性排序，從最接近的相符項目開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含兩個詞語的資產。 在中繼資料中，顯示為智慧標籤的關鍵字比顯示在其他中繼資料欄位中的關鍵字的排名更高。

AEM可讓特定搜尋詞賦予較高的權重。 此外，還可提升特定搜尋詞之少數目標資產的排名。 AEM管理員可依照下列說明進行這些設定。

為快速找到相關資產，豐富式介面提供篩選、排序和選擇機制。 您可以根據多個條件來篩選結果，並查看搜尋的資產數目，以找出各種篩選條件。 或者，您也可以在Omnisearch欄位中變更查詢，以重新執行搜尋。 當您變更搜尋詞或篩選器時，其他篩選器仍會套用，以保留您搜尋的上下文。

有時候，您會在搜尋結果中看到一些非預期的資產。 如需詳細資訊，請查看未 [預期的結果](#unexpectedresults)。

AEM可搜尋許多檔案格式，而且可自訂搜尋篩選器以符合您的業務需求。 請洽詢您的管理員，以瞭解您的DAM儲存庫有哪些搜尋選項，以及您的登入可能有哪些限制。

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

### 搜尋排名與提升 {#searchrank}

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 在各個中 `woman running` 繼資料欄位中的相符項目。
1. 智慧型標 `woman running` 簽中的相符項目。
1. 智慧標 `woman` 簽中 `running` 的或的比對。

您可以改善特定資產的關鍵字關聯性，以協助根據關鍵字提高搜尋效率。 換言之，當您根據這些關鍵字進行搜尋時，您促銷特定關鍵字的影像會出現在搜尋結果的頂端。

1. 從「資產」使用者介面，開啟資產的屬性頁面。按一 **[!UICONTROL 下「進階]** 」，然後按一下/點選「 **[!UICONTROL Elevate for search keywords]** 」下 **[!UICONTROL 方的「新增」]**。
1. 在「搜 **[!UICONTROL 尋促銷]** 」方塊中，指定您要大幅提升影像搜尋的關鍵字，然後按一下／點選「新增」 ****。 您可以以相同的方式指定多個關鍵字。
1. 按一下／點選「 **[!UICONTROL 儲存並關閉]**」。 您為此關鍵字促銷的資產會出現在熱門搜尋結果中。

您可以透過提升目標關鍵字搜尋結果中某些資產的排名，來利用此功能。 請參閱以下範例影片。 如需詳細資訊，請參 [閱「AEM中的搜尋」](https://helpx.adobe.com/experience-manager/kt/help/assets/search-feature-video-use.html)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*瞭解搜尋結果的排名方式，以及排名的影響。*

## Advanced search {#scope}

AEM提供各種方法，例如套用至已搜尋資產的篩選器，以協助您更快找到所需的資產。 以下說明一些常用的方法。 以下 [共用一些](#samples) 圖示範例。

**搜索檔案或資料夾**: 在搜索結果中，查看檔案、資料夾或兩者。 從「篩 **[!UICONTROL 選器]** 」面板中，您可以選取適當的選項。 請參閱 [搜尋介面](#searchui)。

**在資料夾中搜尋資產**: 您可以將搜尋限制在特定資料夾。 在「篩 **[!UICONTROL 選器]** 」面板中，新增資料夾的路徑。 一次只能選擇一個資料夾。

![在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中](assets/search_folder_select.gif)

在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Adobe Stock影像 {#adobestock}

在AEM使用者介面中，使用者可以搜尋 [Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) ，並授權所需的資產。 新增 `Location: Adobe Stock` 至Omnisearch列。 您也可以使用「篩選」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。

### 動態媒體資產 {#dmassets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」>「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。

### 在中繼資料欄位中使用特定值進行搜尋 {#gqlsearch}

您可以根據特定中繼資料欄位的確切值，例如標題、說明和作者，來建立資產。 GQL全文搜索功能僅提取那些元資料值與搜索查詢完全匹配的資產。 屬性的名稱（例如作者、標題等）和值會區分大小寫。

| 中繼資料欄位 | Facet值與使用 |
|---|---|
| 標題 | 標題：John |
| 產生器 | 建立者：John |
| 位置 | 位置： NA |
| 說明 | 說明：「範例影像」 |
| 製作工具 | 創作工具：「Adobe Photoshop CC 2015」 |
| 版權擁有者 | copyrightowner:「Adobe Systems」 |
| 參與者 | 投稿人：John |
| 使用條款 | 使用條款：「保留CopyRights」 |
| 建立日期 | 已建立：YYYY-MM-DDTHH |
| 到期日 | 過期：YYYY-MM-DDTHH |
| 準時 | ontime:YYYY-MM-DDTHH |
| 關閉時間 | offtime:YYYY-MM-DDTHH |
| 時間範圍（過期的dateontime,offtime） | facet欄位： 下限……上界 |
| 路徑 | /content/dam/&lt;資料夾名稱> |
| PDF 標題 | pdftitle:「Adobe檔案」 |
| 主旨 | 主旨：「訓練」 |
| 標記 | 標籤：「位置與旅行」 |
| 類型 | 類型：&quot;image\png&quot; |
| 影像寬度 | width:lowberbound..上界 |
| 影像高度 | 高度：下限。上界 |
| 人員 | 人：John |

屬性路徑、限制、大小和orderby不能與任何其他屬性一起使用ORed。

使用者產生屬性的關鍵字是屬性編輯器中的小寫欄位標籤，並移除空格。

以下是複雜查詢的搜尋格式範例：

* 若要顯示具有多個刻面欄位的所有資產(例如： title=John Doe and creator tool = Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* 若要在Facet值不是單字而是句子時顯示所有資產(例如： title=Scott Reynolds): `title:"Scott Reynolds"`
* 若要顯示具有單一屬性多個值的資產(例如： title=Scott Reynolds或John Doe): `title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產(例如： 標題是Scott Reynolds): `title:Scott*`
* 若要顯示屬性值以特定字串結尾的資產(例如： 標題是Scott Reynolds): `title:*Reynolds`
* 若要顯示包含特定字串的屬性值的資產(例如： 標題=巴塞爾會議室): `title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如： 在具有title=John Doe的資產中搜尋字串Adobe): `*Adobe* title:"John Doe"`

## 從其他AEM產品或介面搜尋資產 {#beyondomnisearch}

Adobe Experience Manager(AEM)將DAM存放庫與各種其他AEM解決方案連結，讓您更快速地存取數位資產，並簡化創意工作流程。 任何資產搜尋都從瀏覽或搜尋開始。 在不同的曲面和解決方案上，搜索行為基本保持不變。 有些搜尋方法會隨著目標對象、使用案例和使用者介面而變更，而且AEM解決方案的使用者介面會有所不同。 以下連結說明個別解決方案的特定方法。 本文將說明普遍適用的提示和行為。

### 從Adobe Asset Link面板搜尋資產 {#aal}

使用Adobe Asset Link，創意專業人員現在可以存取儲存在AEM Assets中的內容，而不需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用Creative Cloud應用程式中的應用程式內面板，順暢地瀏覽、搜尋、結帳和結帳資產： Photoshop、Illustrator和InDesign。 資產連結也可讓使用者搜尋視覺上類似的結果。 視覺化搜尋顯示結果由Adobe Sensei的機器學習演算法提供支援，並協助使用者尋找美學上類似的影像。 請參 [閱使用Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) ，搜尋及瀏覽資產。

### 在AEM案頭應用程式中搜尋資產 {#desktopapp}

創意專業人員使用案頭應用程式，讓AEM Assets可輕鬆搜尋，並可在其本機案頭（Win或Mac）上使用。 創意人員可以輕鬆地在Mac Finder或Windows檔案總管中顯示所需資產、在案頭應用程式中開啟並在本機變更——這些變更會以儲存庫中建立的新版本儲存回AEM。 應用程式支援使用一或多個關鍵字*和？的基本搜尋 萬用字元和AND運算子。 請參閱 [在案頭應用程式中瀏覽](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 、搜尋和預覽資產。

### Search assets in Brand Portal {#brandportal}

業務線使用者和行銷人員使用品牌入口網站，以有效且安全的方式與延伸的內部團隊、合作夥伴和經銷商共用經過核准的數位資產。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜尋Adobe Stock影像 {#adobestock-1}

在AEM使用者介面中，使用者可以搜尋Adobe Stock資產並授權所需的資產。 在Omnisearch `Location: Adobe Stock` 欄位中新增。 您也可以使用「篩 **[!UICONTROL 選器]** 」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。 請參 [閱「在AEM中管理Adobe Stock影像」](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### 搜尋動態媒體資產 {#dynamicmedia}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。在製作網頁時，作者可在內容尋找工具中搜尋集合。集合的篩選器可從快顯功能表中取得。

### 在製作網頁時，在Content Finder中搜尋資產 {#contentfinder}

作者可以使用Content Finder搜尋DAM儲存庫中的相關資產，並使用他們建立的網頁中的資產。

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### 搜尋系列 {#collections}

AEM搜尋功能支援搜尋系列並搜尋系列中的資產。 請參閱 [搜尋系列](/help/assets/manage-collections.md)。

## Asset selector {#assetselector}

資產選擇器可讓您以特殊方式搜尋、篩選及瀏覽DAM資產。 資產選擇器可在取得 `https://[aem_server]:[port]/aem/assetpicker.html`。 您可以使用資產選擇器擷取所選資產的中繼資料。 您可以使用支援的請求參數來啟動它，例如資產類型（影像、視訊、文字）和選擇模式（單選或多選）。 這些參數會為特定搜尋例項設定資產選取器的上下文，並在整個選取範圍內保持不變。

資產選擇器會使用HTML5 `Window.postMessage` 訊息，將所選資產的資料傳送給收件者。 資產選擇器是以Granite的基礎選擇器辭彙為基礎。 依預設，資產選擇器會在「瀏覽」模式中運作。

您可以在URL中傳遞下列請求參數，以在特定內容中啟動資產選擇器：

| 名稱 | 值 | 範例 | 目的 |
|---|---|---|---|
| 資源尾碼(B) | 資料夾路徑作為URL中的資源尾碼：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 若要啟動已選取特定資料夾的資產選擇器，例如已選取資料夾/content/dam/we-retail/en/activity,URL應為： [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在啟動資產選擇器時需要選取特定資料夾，請將其作為資源尾碼傳遞。 |
| 模式 | 單一，多重 | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | 在多個模式中，您可以使用資產選擇器同時選取多個資產。 |
| mimetype | 資產的mimetype(s`/jcr:content/metadata/dc:format`)（也支援萬用字元） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | 使用它以MIME類型篩選資產 |
| 對話方塊 | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些參數將資產選擇器開啟為「花崗岩」對話方塊。 只有當您透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時，此選項才適用。 |
| assettype(S) | 影像、檔案、多媒體、封存 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用這個選項可根據傳遞的值來篩選資產類型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | 使用此選項可指定資產選擇器的根資料夾。 在這種情況下，資產選擇器可讓您只選取根資料夾下的子資產（直接／間接）。 |

若要存取資產選擇器介面，請前往 `https://[AEM server]:[port]/aem/assetpicker`。 導覽至所要的檔案夾，並選取一或多個資產。 或者，從Omnisearch方塊中搜尋所要的資產、視需要套用篩選，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/assetpicker.png)

在資產選擇器中瀏覽並選取資產

## 限制 {#limitations}

AEM Assets中的搜尋功能有下列限制：

* 請勿在搜索查詢中輸入前導空格，否則搜索無效。
* AEM可能會在您從搜尋結果中選取資產的屬性，然後取消搜尋後繼續顯示搜尋詞(CQ-4273540)。
* 搜索資料夾或檔案和資料夾時，不能對任何參數對搜索結果進行排序。
* 如果您按return鍵而未在Omnisearch列中系結任何項目，AEM會傳回僅包含檔案而非檔案夾的清單。 如果您在未使用關鍵字的情況下特別搜尋資料夾，AEM不會傳回任何結果。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋最適合大型儲存庫。 雖然沒有最佳結果所需的影像數量下限，但少數影像的比對品質可能不如大型儲存庫中的比對品質好。
* 您無法變更模型或訓練AEM以尋找類似的影像。 例如，新增或移除智慧標籤至少數資產並不會變更模型。 資產確實會從視覺上類似的搜尋結果中排除。

## 搜尋秘訣 {#tips}

* 監控資產的審閱狀態時，請使用適當的選項來尋找已核准的資產或待核准的資產。
* 使用「前瞻分析」述詞，根據從各種Creative應用程式取得的資產使用統計資料來搜尋支援的資產。 使用資料會分組在資產顯示類別的「使用分數」、「印象」、「點按」和「媒體」渠道下。
* 使用複選框可選擇所有搜索結果或要對所選內容進行操作的篩選搜索結果。 不論目前使用者檢視中顯示多少資產，都會選取所有搜尋的資產。 例如，您可以下載所有選取的資產、大量更新所有選取資產的中繼資料屬性，或將選取的資產新增至系列。
* 若要搜尋不含必要中繼資料的資產，請參閱必 [要中繼資料](#mandatorymetadata)。
* 搜尋使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為獲得更佳結果，請使用雙引號（非單引號），或確保數字與沒有特殊字元的單字相鄰(例如 *shoe12*)。
* 全文搜尋支援運算子，例如-、^等。 要將這些字母作為字串文本搜索，請用雙引號將搜索表達式括起來。 例如，使用「筆記型電腦——美容」而非「筆記型電腦——美容」。
* 如果搜尋結果太多，請將 [搜尋範圍限制](#scope) 為所要資產的零值。 當您對如何更好地尋找所需資產（例如特定檔案類型、特定位置、特定中繼資料等）有一些概念時，效果最佳。

* **標籤**: 標籤可協助您將可以更有效率地瀏覽和搜尋的資產分類。 標籤有助於將適當的分類傳播給其他用戶和工作流。 AEM提供使用Adobe Sensei人工智慧服務自動標籤資產的方法，這些服務可讓您在使用和訓練資產時不斷取得進步。 當您搜尋資產時，如果您的帳戶已啟用功能，智慧標籤會加入。 它可與內建搜尋功能搭配使用。 請參閱 [搜尋行為](#searchbehavior)。 若要最佳化搜尋結果的顯示順序，您可以提 [高少數選取資產的搜尋](#searchrank) 排名。

* **索引**: 搜尋結果中只會傳回已建立索引的中繼資料和資產。 為了獲得更好的覆蓋面和效能，請確保正確編製索引並遵循最佳做法。 請參 [閱索引](#searchindex)。

## 一些範例說明搜尋 {#samples}

在關鍵字周圍使用雙引號，以尋找包含使用者指定之確切順序之確切片語的資產。

![使用引號和不使用引號的搜尋行為](assets/search_with_quotes.gif)

使用引號和不使用引號的搜尋行為

**使用星號通配符進行搜索**: 若要擴大搜尋範圍，請在搜尋字詞前後使用星號，以比對任意數目的字元。 例如，搜尋沒有星號的執行並不會傳回包含字詞變異的資產（包括在中繼資料中）。 星號可取代任意數字元。 例如，

* `run` 返回正確執行關鍵字的資產
* `run*` 傳回資產，包括執行、執行、逃跑等。
* `*run` 傳回Outrun、重新執行等。
* `*run*` 傳回所有可能的組合。

![以範例說明在資產搜尋中使用星號萬用字元](assets/search_with_asterisk_run.gif)

以範例說明在資產搜尋中使用星號萬用字元

**使用問號萬用字元搜尋**: 若要擴大搜尋範圍，請使用一或多個「?」 字元來比對字元數目。 例如，在下圖中，

* `run???` 查詢不符合任何資產。

* `run????` query與後4個字 `running` 元的字詞相符 `run`。

* `??run` query與之前包含兩 `rerun` 個字元的單字相符 `run`。

![使用範例說明在資產搜尋中使用問號萬用字元](assets/search_with_questionmark_run.gif)

使用範例說明在資產搜尋中使用問號萬用字元

**排除關鍵字**: 使用破折號來搜尋不含關鍵字的資產。 例如，查 `running -shoe` 詢會傳回包含但 `running`不包含的資產 `shoe`。 同樣地， `camp -night` 查詢會傳回包含但不包含 `camp` 的資產 `night`。 請注意， `camp-night` 查詢會傳回同時包含和的 `camp` 資產 `night`。

![使用破折號來搜尋不含已排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)*圖： 使用破折號來搜尋不含已排除關鍵字的資產*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tagging and requires AEM 6.5.2.0 or later. After configuring smart tagging functionality, follow these steps.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
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

<!-- Check with gklebus if this customization is possible in Cloud Service now

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| File Size | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientation | Horizontal, Vertical, or Square. |
| Style | Color, or Black & White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## 使用資產搜尋結果 {#aftersearch}

在您看到一些符合標準的搜尋資產後，您可以執行下列典型工作，或對這些搜尋結果執行下列動作：

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用「案頭動作」在案頭應用程式中開啟這些資產。
* 建立智慧型系列。

### 排序搜尋結果 {#sort}

排序搜尋結果有助於您更快找到所需資產。排序搜索結果在清單視圖中工作，且僅當從「篩選器」面板 **[!UICONTROL [中選擇「檔案](#searchui)]**」時**[!UICONTROL &#x200B;工作&#x200B;]**。[!DNL Assets]使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產 (無論多少)。伺服器端排序比用戶端排序提供更快速且更精確的結果。

在清單檢視中，您可以像排序任何資料夾中的資產一樣，對搜尋結果進行排序。 排序功能適用於這些欄——名稱、標題、狀態、維度、大小、評分、使用狀況、（日期）建立、（日期）修改、（日期）發佈、工作流程和檢出。

有關排序功能的限制，請參見 [限制](#limitations)。

### 檢查資產的詳細資訊 {#checkinfo}

您可以從搜尋結果頁面檢查搜尋資產的詳細資訊。

若要查看資產的所有中繼資料，請選取資產，然後從工具 **[!UICONTROL 列按一]** 下屬性。

若要檢查資產或資產版本記錄的註解，請按一下資產以開啟大型預覽。在左側導軌中開啟時間軸，並選取「 **[!UICONTROL 注釋]** 」或「 **[!UICONTROL 版本」]**。您也可以依時間順序將時間軸活動 (例如注釋或版本) 排序。

![排序搜尋資產的時間軸項目](assets/sort_timeline_search_results.gif)

排序搜尋資產的時間軸項目

### 下載搜尋的資產 {#download}

您可以從資料夾下載搜尋的資產及其轉譯，就像下載一般資產一樣。 從搜尋結果中選取一或多個資產，然後按一下工 **[!UICONTROL 具列中]** 的「下載」。

### 大量更新中繼資料屬性 {#metadataupdates}

您可大量更新多個資產的常用中繼資料欄位。 從搜尋結果中，選取一或多個資產。 按一 **[!UICONTROL 下工具列]** 中的「屬性」，並視需要更新中繼資料。 完成 **[!UICONTROL 時，按一下「儲存]** 」並關閉。 會覆寫更新欄位中先前存在的中繼資料。

對於單一資料夾或系列中可用的資產，大量更新中繼 [資料會比較容易](/help/assets/manage-metadata.md#manage-assets-metadata)。 對於跨資料夾可用或符合一般准則的資產，透過搜尋大量更新中繼資料會更快速。

### 智慧型系列 {#collections-1}

系列是一組有序的資產，可包含不同位置的資產，因為系列僅包含這些資產的參考。 系列有下列兩種類型：

* 資產、檔案夾和其他系列的靜態參考清單。
* 動態清單（智慧型系列），會根據搜尋准則填入系列中的資產。

您可以根據搜尋准則建立智慧型系列。從「濾鏡 **[!UICONTROL 器]** 」面板中，選 **[!UICONTROL 擇「檔案]** 」並單 **[!UICONTROL 擊「保存智慧集」]**。請參閱 [管理系列](/help/assets/manage-collections.md)。

## 意外的搜尋結果 {#unexpectedresults}

**搜尋遺失的中繼資料**: 當搜尋遺失必要中繼資料的資產時，AEM可能會顯示某些具有有效中繼資料的資產。 會根據索引的中繼資料屬性來偵測和報告遺失的中繼資料。 即使資產中繼資料已修正，它仍會繼續顯示為遺失的中繼資料，直到重新建立索引為止。 請參 [閱必要中繼資料](/help/assets/metadata-schemas.md#defining-mandatory-metadata)。

**搜尋結果太多**: 為避免搜尋結果過多，請考慮限制搜尋結果。 例如，若要在DAM中搜尋資產，請在Omnisearch `Location:Assets` 列中選取。 如需更多搜尋篩選，請參 [閱搜尋範圍](#scope)。

<!-- Another reason to get more than expected search results can be use of smarts tags. See [search behavior with smart tags](#withsmarttags). 
-->

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

**新上傳的資產無自動完成建議**: 當您開始在Omnisearch列中輸入搜尋關鍵字時，最近上傳資產的中繼資料（標題、標籤等）不會立即做為建議使用。 AEM Assets會等到逾時期間（預設為一小時）到期後，再執行背景工作，為所有新上傳或更新的資產建立中繼資料索引，然後將中繼資料新增至建議清單。

**無搜尋結果**: 如果AEM並顯示搜尋查詢的空白頁面，可能是下列原因：

* 沒有與查詢相符的資產。
* 在搜索查詢前添加空格。 這是已知 [的限制](#limitations)。

* 不支援的中繼資料欄位包含您搜尋的關鍵字。 並非所有中繼資料欄位都會被視為搜尋。 請參 [閱範圍](#scope)。
* 會為資產設定啟動和關閉時間，而搜尋是在資產關閉時間進行。

**Search filter/predicate is not available**: 如果使用者介面上沒有搜尋篩選器的預期自訂功能，請連絡您的管理員，以檢查自訂是否已針對所有作者以及您使用的生產伺服器實施。 可能配置不正確。

## 疑難排解搜尋相關問題 {#troubleshoot}

請參閱以下問題和可能的行動方針：

* 如果未顯示預期的搜尋篩選器／謂詞，請聯絡您的管理員。
* 在搜尋視覺上類似的影像時，搜尋結果有時候會遺失預期的影像。 檢查此類資產是否已建立索引並加上智慧標籤。
* 當搜索視覺上類似的影像時，有時在搜索結果中顯示看似無關的影像。 AEM會顯示盡可能多的潛在相關資產。 較不相關的影像（如果有）會新增至結果，但搜尋排名較低。 當您向下捲動搜尋結果時，相符項目的品質和搜尋資產的相關性會降低。
