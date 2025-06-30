---
title: 如何在Assets檢視中管理中繼資料？
description: 瞭解如何在Assets檢視中管理中繼資料。 更好的中繼資料管理讓資產更易於存取、更易於管理和完成。
role: User, Leader, Admin, Architect, Developer
contentOwner: AG
exl-id: 7264e8d1-fc8f-4eb3-93a9-a6066ca3f851
feature: Metadata
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2453'
ht-degree: 74%

---

# 資產檢視的中繼資料 {#metadata}

中繼資料為資料或資料相關的說明。例如，作為資產的影像可以包含其所按一下的相機資訊或任何版權資訊。此資訊是影像的中繼資料。中繼資料是進行高效率資產管理的關鍵所在。中繼資料雖然是資產所有可用資料的集合，但並不一定包含在資產內。

中繼資料有助於您進一步將資產分類，而且隨著數位資訊量成長，將相當實用。您可以僅根據檔案名稱、縮圖和記憶體體來管理數百個檔案。然而，此方法並不能調整規模。隨著相關人數和管理的資產數增加，此方法尚嫌不足。

隨著中繼資料增加，數位資產的價值也會成長，因為資產會變成：

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

基於這些原因，Assets 提供建立、管理和交換數位資產的中繼資料的合適方式。

## 檢視中繼資料 {#view-metadata}

若要檢視資產的中繼資料，請瀏覽至資產或搜尋資產、選取資產，然後按一下工具列中的&#x200B;**[!UICONTROL 詳細資訊]**。

![檢視資產的中繼資料](assets/metadata-view.png)

*圖：若要檢視資產及其中繼資料，請從工具列按一下&#x200B;**[!UICONTROL 詳細資訊]**&#x200B;或按兩下資產。*

標題、說明和上傳日期之類的基本中繼資料可在[!UICONTROL 基本]標籤中取得。[!UICONTROL 進階]標籤包含更進階的中繼資料，例如相機型號、鏡頭詳細資訊和地理標籤。[!UICONTROL 標記]標籤會根據影像內容包含自動套用的標記。

## 更新中繼資料 {#update-metadata}

在管理員配置中繼資料表單後，可以手動更新其他欄位。您可能想要變更改此設定，因為那僅根據現成可用的中繼資料表單進行讀取。

## 智慧標記 {#smart-tags}

[!DNL Experience Manager Assets] 使用 [Adobe Sensei](https://www.adobe.com/tw/sensei.html) 所提供的人工智慧，自動將相關標記套用至您所有上傳的資產。這些標記名為智慧型標記，有助於您快速尋找相關資產，提高專案的內容速度。智慧型標記即是不含在影像內的中繼資料範例。

智慧型標記近乎即時套用，並根據影像內容產生。上傳資產時，使用者介面會在資產縮圖上顯示[!UICONTROL 處理中]一段時間。待處理完成後，即可[檢視中繼資料](#view-metadata)和智慧型標記。

![檢視資產的智慧型標記](assets/metadata-view-tags.png)

*圖：若要檢視智慧標記，請從工具列按一下&#x200B;**[!UICONTROL 詳細資訊]**&#x200B;或按兩下資產。*

智慧型標記也包含信賴分數 (以百分比呈現)。這表示與套用標記相關的信賴度。您可以審核自動套用的智慧型標記。

## 新增或更新關鍵字 {#manually-tag}

除了使用 [!DNL Adobe Sensei] 智慧型服務自動新增的智慧型標記之外，您還可新增更多標記到您的資產。開啟要預覽的資產，按一下[!UICONTROL 標記]，然後在[!UICONTROL 關鍵字]欄位中輸入所需的關鍵字。若要新增標記，請按一下「Return」。[!DNL Assets view] 會近乎即時地編製關鍵字的索引，因此您的團隊很快就能使用新的關鍵字搜尋更新的資產。

您也可以從[!UICONTROL 智慧標記]區段移除由 [!DNL Assets view] 自動新增到所有上傳資產的標記。

## 分類法管理 {#taxonomy-management}

標記還可以巢狀內嵌到階層中，以支援類別和子類別等關係。如果您需要插入階層式標記，管理員可以在 [!UICONTROL 分類式管理] (屬於 [!UICONTROL 設定]) 部分輕鬆予以管理。您可以建立一組控管的命名空間和標記，讓所有使用者都可以在描述內容時存取與使用。只有管理員可以在 [!UICONTROL Taxonomy Manager] 設定標記階層，確保這些值的一致的控制和使用。

## 設定中繼資料表單 {#metadata-forms}

>[!CONTEXTUALHELP]
>id="assets_metadata_forms"
>title="中繼資料表單"
>abstract="[!DNL Experience Manager Assets] 預設會提供許多標準中繼資料欄位。組織擁有其他中繼資料需求，並需要更多中繼資料欄位以新增特定企業中繼資料。 中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的詳細資訊頁面。特定企業中繼資料能夠改善其資產的控管和探索。"

Assets檢視預設會提供許多標準中繼資料欄位。 組織擁有其他中繼資料需求，並需要更多中繼資料欄位以新增特定企業中繼資料。中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的[!UICONTROL 詳細資訊]頁面。特定企業中繼資料能夠改善其資產的控管和探索。您可以從零開始建立表單，或改變現有表單的用途。

您可以為不同的資產類型 (不同的 MIME 類型) 設定中繼資料表單。使用與檔案的 MIME 類型相同的表單名稱。Assets檢視會自動比對上傳的資產MIME型別與表單的名稱，並根據表單欄位更新上傳資產的中繼資料。
<!--
For example, if a metadata form by the name `PDF` or `pdf` exists, then the uploaded PDF documents contain metadata fields as defined in the form.
-->
Assets檢視使用以下順序搜尋現有中繼資料表單名稱，以將中繼資料欄位套用至特定型別的已上傳資產：

MIME 子類型 > MIME 類型 > `default` 表單 > 現成可用的表單

例如，如果存在名稱為 `PDF` 或 `pdf` 的中繼資料表單，上傳的 PDF 文件則包含如表單中定義的中繼資料欄位。如果名稱為`PDF`或`pdf`的中繼資料表單不存在，則Assets檢視會比對是否存在名稱為`application`的中繼資料表單。 如果有名稱為 `application` 的中繼資料表單，則上傳的 PDF 文件會包含如表單中定義的中繼資料欄位。如果Assets檢視仍找不到符合的中繼資料表單，則會搜尋`default`中繼資料表單，以將表單中定義的中繼資料欄位套用至上傳的PDF檔案。 如果上述任何步驟都無法運作，Assets檢視會將現成可用表單中定義的中繼資料欄位套用至所有上傳的PDF檔案。
如果您想要將中繼資料表單指派給資料夾[，請參閱](#assign-metadata-form-folder)。

>[!IMPORTANT]
>
>特定檔案類型的新中繼資料表單會完成取代 [!DNL Assets view] 所提供的預設中繼資料表單。如果您刪除或重新命名中繼資料表單，新資產便可再次使用預設中繼資料欄位。

若要建立中繼資料表單，請依照下列步驟：

1. 在左側欄中按一下&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 中繼資料表單]**。

   ![左側邊欄中的中繼資料表單選項](assets/metadata-forms-sidebar.png)

1. 按一下使用者介面右上角區域中的&#x200B;**[!UICONTROL 建立]**。
1. 為表單命名，然後按一下&#x200B;**[!UICONTROL 建立]**。
1. 為右側欄中&#x200B;**[!UICONTROL 設定]**&#x200B;中的標籤命名。
1. 從左側欄中可用的&#x200B;**[!UICONTROL 元件]**&#x200B;拖曳表單中標籤上所需的元件。依照所需的序列拖曳元件。

   ![左側邊欄中的中繼資料表單選項](assets/metadata-form-new.png)

   *圖：中繼資料表單建立介面，其中包含新增元件的選項和預覽表單的選項。*

1. 對每個元件，在右側邊欄的「**[!UICONTROL 設定]**」命名，提供支援屬性的對應。
1. 或是對元件選取&#x200B;**[!UICONTROL 必要]**，讓中繼資料欄位成為必要欄位，並選取&#x200B;**[!UICONTROL 唯讀]**&#x200B;讓此欄位在資產[!UICONTROL 詳細資訊]頁面中無法編輯。
1. 或者按一下&#x200B;**[!UICONTROL 預覽]**&#x200B;以預覽您正在建立的表單。
1. 或者在每個標籤中新增更多標籤和所需元件。
1. 表單完成時，按一下&#x200B;**[!UICONTROL 儲存]**。

請觀看此影片以查看步驟的順序：

>[!VIDEO](https://video.tv.adobe.com/v/341275)

建立表單後，便會在使用者上傳相符 MIME 類型的資產時自動套用表單。

若要重複使用現有表單來建立新表單，請選取中繼資料表單，從工具列按一下&#x200B;**[!UICONTROL 複製]**、命名，然後按一下&#x200B;**[!UICONTROL 確認]**。您可以編輯中繼資料表單，進行變更。變更表單時，會在變更後用於上傳的資料。不會變更現有資產。

### 屬性元件 {#property-components}

您可以使用以下任何屬性元件自訂中繼資料表單。只需將元件類型拖放到表單上想要的位置，並修改元件設定即可。以下是每種屬性類型及其儲存方式的概觀。

| 元件名稱 | 說明 |
|---|---|
| 摺疊式功能表容器 | 為常見元件和屬性的清單新增可折疊的標題。預設情況下是可以展開或折疊。 |
| 單行文字 | 新增單行文字屬性。 |
| 多行文字 | 新增多行文字或一個段落。在使用者鍵入時會擴展以包含所有的內容。 |
| 多值文字 | 新增多值文字屬性。 |
| 數字 | 新增數字元件。 |
| 核取方塊 | 新增布林值。在儲存值後，將其儲存為 TRUE 或 FALSE。 |
| 日期 | 新增日期元件。 |
| 下拉式清單 | 新增下拉式清單。 |
| 狀態 | 新增存放庫狀態屬性 (對應到 repo:state) |
| 資產狀態 | 新增預設的資產狀態屬性 (對應到 dam:assetStatus) |
| 標記 | 從分類法管理中儲存的值新增標記 (對應到 xcm:tags)。 |
| 關鍵字 | 新增自由格式關鍵字 (對應到 dc:subject)。 |
| 智慧標記 | 透過自動新增中繼資料標記增強搜尋功能。 |

### 將中繼資料表單指派至資料夾 {#assign-metadata-form-folder}

您也可以將中繼資料表單指派給Assets檢視部署內的資料夾。 當您手動將中繼資料表單套用到資料夾時，根據 MIME 類型，指派至資料夾的中繼資料表單將會被覆寫。然後，資料夾中的所有資產 (包括子資料夾中的資產) 將顯示中繼資料表單中定義的屬性。

若要將中繼資料表單指派至資料夾：

1. 瀏覽至「**[!UICONTROL 設定]** > **[!UICONTROL 中繼資料表單]**」並選取中繼資料表單。

2. 按一下「**[!UICONTROL 指派至資料夾]**」。

3. 選取資料夾並按一下&#x200B;**[!UICONTROL 指派]**。 您可以透過按一下資料夾名稱來選取資料夾。

   ![將中繼資料表單指派至資料夾](assets/assign-to-folder.png)

   您也可以瀏覽至資料夾詳細資料頁面，然後在右側窗格從資料夾屬性中選取中繼資料表單，以將中繼資料表單指派至資料夾。

   ![資料夾屬性中的中繼資料表單](assets/metadata-from-folder-props.png)

### 從資料夾中刪除中繼資料表單 {#remove-metadata-form-folder}

將中繼資料表單指派到一個或多個資料夾後，Experience Manager Assets 還可讓您從所選資料夾中刪除中繼資料表單。

若要從資料夾移除中繼資料表單：

1. 瀏覽至「**[!UICONTROL 設定]** > **[!UICONTROL 中繼資料表單]**」並選取中繼資料表單。

1. 按一下「**[!UICONTROL 從資料夾中移除]**」用來顯示中繼資料表單的已指派資料夾清單。

1. 選取資料夾並按一下「**[!UICONTROL 移除]**」。您也可以從清單中選取多個資料夾。

您也可以導覽至資料夾詳細資料頁面，然後從「**[!UICONTROL 中繼資料表單]**」欄位中選取「**[!UICONTROL 系統對應中繼資料表單]**」，即可從資料夾中刪除已指派的中繼資料表單。

### 使用中繼資料表單中的連結元件 {#link-component-metadata-form}

此連結元件是用來啟用外部 URL，包括儲存連結、版權資訊、聯絡表單等。若要在中繼資料表單上使用連結元件，您需要[設定中繼資料表單](#metadata-forms)。

請依照下列步驟，在中繼資料表單上使用連結元件：

1. 前往資產詳細資料頁面，並導覽至「**[!UICONTROL 連結 URL]**」。
1. 新增要用來重新導向所選資產的 URL。
1. 按一下「**[!UICONTROL 新增連結]**」。執行下列其中一個動作：
   * 按一下 ![複製圖示](assets/do-not-localize/copy.svg) 以複製 URL。
   * 按一下 ![編輯圖示](assets/do-not-localize/edit.svg) 以編輯 URL。
1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。


### 使用中繼資料表單中的標記元件 {#tag-component-metadata-form}

根元素代表可與資產建立關聯之標記的樹狀結構，有助於根據指派給資產的標記來識別該資產。此外，當在中繼資料編輯器中設定中繼資料表單時，您還可以限制特定分類法的存取。

#### 標記元件設定 {#tags-component-configuration}

請執行下列步驟來設定標記元件：

1. 前往中繼資料編輯器，然後導覽至「**[!UICONTROL 標記]**」，並將其放置在畫布上。
1. 重新命名畫布上的元件。若要這麼做，請前往「設定」面板中「[!UICONTROL 中繼資料屬性]」下方的「**[!UICONTROL 標籤]**」，並新增用於識別的文字。
1. 在「設定」面板中的「[!UICONTROL 中繼資料屬性]」下方，搜尋您想要指派給元件的中繼資料屬性。
1. 按一下「**[!UICONTROL 限制在特定的分類法]**」以限制分類法的根路徑。若要這麼做，請瀏覽標記並選擇特定路徑的分類法。
1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。

   ![根標記設定](assets/root-tag-config.png)

1. [將中繼資料表單指派至資料夾](#assign-metadata-form-folder)。

<!--
#### Mapping between assets and taxonomy {#asset-taxonomy-mapping}

See [Assign metadata form to folders](#assign-metadata-form-folder). Follow the steps below to perform mapping between folder and taxonomy:

1. Go back to the Settings and click **[!UICONTROL Metadata forms]** 
1. Select a Metadata form that needs mapping. 
1. Click **[!UICONTROL Assign to folder(s)]**. **[!UICONTROL Select Folder(s)]** screen appears. 
1. Navigate to the folder that you want to assign to the metadata form. You can select multiple folders.
1. Click **[!UICONTROL Assign]**.
-->

若要檢視已設定的根標記，請前往資產的詳細資料頁面，該頁面上會執行中繼資料表單和根標記之間的對應。

## 使用AI產生的中繼資料加強內容探索 {#ai-smart-tags}

AI不會依賴手動輸入，而是自動將描述性標籤指派給數位資產。 這些 AI 產生的標記可提升中繼資料的品質，讓資產搜尋、分類和推薦變得更簡單。此方法不僅可避免手動標籤，進而提升效率，還可確保大量數位內容的一致性和擴充性。 例如，如果資產是影像，AI可以識別其中的物件、場景、情感，或甚至品牌標誌，並產生相關標籤，例如「日落」、「海灘」、「假期」或「微笑」。 AI產生的內容可運用語意和辭彙搜尋技術來增強資產搜尋。 檢視更多[搜尋Assets](search-assets-view.md)。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![AI產生的中繼資料](/help/assets/assets/enhanced-smart-tags.png)

### 如何啟用AI產生的中繼資料？ {#enable-ai-generated-metadata}

若要啟用AI產生的中繼資料：

* 最低必要的AEM發行版本為`20626`。

* 您必須簽署GenAI Rider合約。 如需詳細資訊，請聯絡您的Adobe代表。

  >[!IMPORTANT]
  >
  > 只有當您尚未定義資產標題時，AI產生的資產標題才會顯示在資產卡片中。 不會覆寫您指定的資產標題。

### 使用AI產生的中繼資料 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

若要使用增強智慧標籤功能，請執行下列步驟：

1. 在[!DNL Experience Manager]介面中，前往所需的資料夾，然後按一下&#x200B;**[!UICONTROL 新增Assets]**。 <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->相容的影像檔案格式為`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw`和`bmp`。

1. 等候新上傳的資產處理完畢。 完成後，前往資產詳細資訊。

1. 移至&#x200B;**[!UICONTROL AI產生的]**&#x200B;標籤。 如果[!DNL Experience Manager]版本不相容或未更新，則不會顯示此索引標籤。  有以下欄位：

   * **[!UICONTROL 產生的標題]：**&#x200B;標題提供簡潔的標題，擷取上傳資產的核心概念，讓您一眼就能輕鬆理解。 新增資產時，如果您提供標題（在`dc:title`中），資產瀏覽檢視中會顯示該標題。 如果保留為空白，則會自動指派AI產生的標題。
   * **[!UICONTROL 已產生描述]：**&#x200B;描述提供資產相關資訊的簡短摘要，協助使用者和搜尋模組快速掌握其關聯性。
   * **[!UICONTROL 產生的關鍵字]：**&#x200B;關鍵字是代表資產主要主題的目標辭彙，有助於標籤和內容篩選。

1. [選擇性]如果您覺得遺漏任何相關標籤，可以新增其他標籤或建立自己的標籤。 若要這麼做，請在&#x200B;**[!UICONTROL 產生的關鍵字]**&#x200B;欄位中寫入您的標籤，然後按一下&#x200B;**[!UICONTROL 儲存]**。

## 後續步驟 {#next-steps}

* [觀看在Assets檢視中管理中繼資料表單的相關影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=zh-Hant)

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/zh-hant?support-solution=General#support)

<!-- TBD: Cannot create a form using the second option. Documenting only the first option for now.
To reuse an existing form to create a form, do one of these:

* Select a metadata form and click **[!UICONTROL Copy]** from the toolbar, provide a name, and click **[!UICONTROL Confirm]**.

* Click **[!UICONTROL Create]**, select **[!UICONTROL Use existing form structure as template]** option, and select an existing form. 
-->

<!-- TBD: Queries for PM and engg.

Can we edit the existing metadata in any form?

How to moderate smart tags?

Allow or deny list for smart tags?

What about Tags displayed just above Smart Tags in the UI?

Is there a detailed metadata tab. Where do the other details of an asset go?

How can one search based strictly on the metadata. Similar to AEM Assets GQL queries.
-->

<!-- TBD: Link to related articles if any.

>[!MORELIKETHIS]
>
>* [Search assets](search.md).
-->

