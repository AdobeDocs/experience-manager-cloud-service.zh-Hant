---
title: 瞭解如何搜尋和探索 [!DNL Assets view]中的資產？
description: 瞭解如何在AEM Assets檢視中搜尋和探索資產。 強大的搜尋功能可讓您快速探索合適的資產，協助您改善內容速度。
role: User
exl-id: abfe6a91-1699-436f-8bf4-0d0bf2369f46
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 74%

---

# 搜尋 [!DNL Assets view] 中的資產 {#search-assets}

>[!CONTEXTUALHELP]
>id="assets_search"
>title="搜尋資產"
>abstract="透過指定搜尋列中的關鍵字或根據資產的狀態、檔案類型、MIME 類型、大小、建立、修改和過期日期篩選資產，來搜尋資產。除了標準篩選器之外，您也可以套用自訂篩選器。您可以將篩選的結果另存為「已儲存搜尋」或「智慧型集合」。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-collections.html?lang=zh-Hant#manage-smart-collection" text="建立智慧型集合"

[!DNL Assets view] 的預設功能即提供有效的搜尋。由於是全文檢索搜尋，因此十分全面。強大的搜尋功能可讓您快速探索合適的資產，協助您改善內容速度。[!DNL Assets view] 提供全文檢索搜尋，甚至還透過如智慧標記、標題、建立的日期和版本等中繼資料進行搜尋。

若要搜尋資產：

* 按一下頁面頂部的搜尋方塊。預設為在您目前瀏覽的資料夾內進行搜尋。執行下列任一項作業：

  ![搜尋方塊](assets/search-box.png)

   * 使用關鍵字進行搜尋，並選擇變更資料夾。按下「Return」。

   * 開始直接搜尋最近檢視的資產，然後使用該資產。在搜尋方塊中按一下，然後從建議中選取最近檢視的資產。

## 篩選搜尋結果 {#refine-search-results}

您可以套用多個篩選條件，調整搜尋結果以尋找相關資產。 這些篩選器由管理員設定，且以檔案、資料夾和集合為基礎。 請參閱[自訂搜尋篩選器](custom-search-filters.md)。

![搜尋篩選器](assets/filters-panel.gif)

您可以根據以下參數來篩選搜尋結果。

* 資產狀態：使用 `Approved`、`Rejected` 或 `No Status` 資產狀態來篩選搜尋結果。
* 檔案類型：依照支援的檔案類型篩選搜尋結果，也就是 `Images`、`Documents` 和 `Videos`。
* MIME 類型：篩選一個或更多支援的檔案格式。<!-- TBD:  [supported file formats](/help/using/supported-file-formats.md). -->
* 影像大小：提供一個或更多最小和最大尺寸，以篩選影像。以尺寸 (像素) 提供大小，而非影像的檔案大小。
* 建立日期：資產的建立日期如中繼資料中所提供。使用的標準日期格式為 `yyyy-mm-dd`。
* 修改日期：上次修改資產的日期。使用的標準日期格式為 `yyyy-mm-dd`。
* 過期日期：根據`Expired`資產狀態來篩選搜尋結果。此外，您可以指定資產的過期日期範圍以進一步篩選搜尋結果。
* 自訂篩選器： [新增自訂篩選器](#custom-filters)至Assets檢視使用者介面。 除了標準篩選器之外，您還可以套用自訂篩選器來縮小您的搜尋結果。

您可以依照 `Name`、`Relevance`、`Size`、`Modified` 和 `Created` 的遞增或遞減順序排序搜尋的資產。已搜尋的資產會依`Relevance` (依預設) 進行排序。

<!--
  
## Manage custom filters {#custom-filters}

**Permissions required:**  `Can Edit`, `Owner`, or Administrator.

Assets view also enable you to add custom filters to the user interface. You can then apply those custom filters in addition to the [standard filters](#refine-search-results) to refine your search results.

Assets view provides the following custom filters:

<table>
    <tbody>
     <tr>
      <th><strong>Custom filter name</strong></th>
      <th><strong>Description</strong></th>
     </tr>
     <tr>
      <td>Title</td>
      <td>Filter assets using the asset title. The title that you specify in the case-sensitive search criteria must match the exact title of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Name</td>
      <td>Filter assets using the asset file name. The name that you specify in the case-sensitive search criteria must match the exact file name of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Asset Size</td>
      <td>Filter assets by defining a size range, in bytes, in the search criteria for an asset to display in the results.</td>
     </tr>
     <tr>
      <td>Predicted Tags</td>
      <td>Filter assets using the asset smart tag. The smart tag name that you specify in the case-sensitive search criteria must match the exact smart tag name of the asset to display in the results. You cannot specify multiple smart tags in search criteria.</td>
     </tr>    
    </tbody>
   </table>

   <!--
   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. For example, if you define <b>ma*</b> as the search criteria, Assets view displays assets with title, such as, market, marketing, man, manchester, and so on in the results.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. You can specify multiple smart tags separated by a comma in the search criteria.

   

### Add custom filters {#add-custom-filters}

To add custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]** or **[!UICONTROL Add Filters]**.

   ![Add custom filters](assets/add-custom-filters.png)

1. On the **[!UICONTROL Custom filters management]** dialog box, select the filters that you need to add to the existing list of filters. Select **[!UICONTROL Custom Filters]** to select all filters.

1. Click **[!UICONTROL Confirm]** to add the filters to the user interface.

### Remove custom filters {#remove-custom-filters}

To remove custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]**.

1. On the **[!UICONTROL Custom filters management]** dialog box, deselect the filters that you need to remove from the existing list of filters.

1. Click **[!UICONTROL Confirm]** to remove the filters from the user interface.

-->

## AI 搜尋 {#ai-search}

AI搜尋是一種進階搜尋功能，可瞭解使用者查詢的涵義和意圖，而非依賴精確的關鍵字比對。 它使用人工智慧(AI)和機器學習，提供更準確且內容感知的結果。

傳統關鍵字式搜尋會尋找精確字詞，AI搜尋則不同，它會解譯字詞、概念和使用者意圖之間的關係。 這可確保使用者找到他們要尋找的內容 — 即使他們的查詢用詞不同、包含拼寫錯誤或使用另一種語言。

如果其主要優點包括：

* **多語言支援**：搜尋多種語言，不需要精確翻譯。 使用者無論查詢語言為何，都能找到相關內容。

* **處理錯誤拼字**：解譯拼字錯誤和拼字錯誤，即使輸入不完美也能確保正確的結果。

* **瞭解同義字**：提供相關辭彙和短語的結果，因此使用者不需要猜測正確的關鍵字。

* **內容感知搜尋**：辨識查詢背後的目的，而不只是確切的字詞。

### AI搜尋範例 {#examples-ai-search}

**範例提示**： *喝咖啡的女人*

傳統關鍵字式搜尋會尋找完全符合的資產中繼資料，例如`Woman`、`drinking`、`Coffee`，並傳回包含中繼資料中所有字詞的資產。

不過，AI搜尋在`Girl`的情況下會比對類似字詞，例如`Lady`、`Woman`，在`Cappuccino`的情況下會比對到`Latte`和`Coffee`。

同樣地，您可以用西班牙文或拼錯拼字`Woman`來指定此提示為`Wman`，仍會得到相同的結果。

在Assets檢視中![語意搜尋](assets/semantic-search.png)

### 在Assets檢視中啟用或停用AI搜尋 {#enable-disable-ai-search}

執行以下步驟以啟用或停用AI搜尋：

1. 瀏覽至&#x200B;**[!UICONTROL 設定]** >> **[!UICONTROL 一般設定]**，然後選取&#x200B;**[!UICONTROL 搜尋]**&#x200B;標籤。

1. 在&#x200B;**[!UICONTROL 搜尋]**&#x200B;區段中，選取&#x200B;**[!UICONTROL AI搜尋]**&#x200B;以啟用AI搜尋，或選取&#x200B;**[!UICONTROL 關鍵字]**&#x200B;以停用它。

   在Assets檢視中![語意搜尋](/help/assets/assets/enable-disable-ai-search.png)

1. 按一下&#x200B;**[!UICONTROL 儲存]**。


## 使用 [!DNL Adobe Firefly] 搜尋資產 {#search-firefly}

您可以利用 [!DNL Experience Manager Assets] 中的 [!DNL Adobe Firefly] 資產搜尋功能，搜尋任何資產資料夾中都找不到的資產。您就可以有效率且即時地產生未儲存在資產資料夾中的資產。

### 開始之前 {#search-assets-firefly-prereqs}

您必須擁有使用中的 [!DNL Adobe Express] 訂閱。

### 產生資產 {#generate-assets-firefly}

如要使用 [!DNL Adobe Firefly] 來產生新資產：

1. 瀏覽至 [!DNL AEM Assets] 工作區。

1. 在搜尋列中輸入資產名稱。例如，您可以使用關鍵字 `Bugatti Type 57` 來搜尋資產。搜尋資產時，若找不到任何結果，是因為該資產不存在於任何資產資料夾中。若要使用 AI 產生資產，請按一下「**[!UICONTROL 使用 Firefly 生成]**」。出現 [!DNL Adobe Firefly] 畫面。

   ![Firefly 整合](assets/firefly-integration.png)

   已成功產生新資產。此外，您可以在描述框中輸入新的文字提示以變更影像描述。[瞭解如何撰寫良好的AI提示，以產生非凡的相關內容](https://helpx.adobe.com/tw/firefly/using/tips-and-tricks.html)。 或者，您也可以[使用各種其他功能（例如變更樣式、影像尺寸等等）編輯影像](https://helpx.adobe.com/tw/firefly/using/text-to-image.html)。

   ![Firefly 整合](assets/bugatti-type-57.png)

1. 選取您想儲存的影像。按一下「**[!UICONTROL 儲存]**」，在您偏好的資料夾儲存資產以便存取。

1. 出現儲存資產表單。指定以下欄位：

   * 在&#x200B;**另存新檔**&#x200B;欄位中輸入檔案名稱。
   * 選取目的地資料夾。
   * 輸入專案或行銷活動名稱、關鍵字、管道、時間段和區域等詳細資訊。

   ![Firefly 整合](assets/save-generated-asset.png)

1. 按一下「**另存為新資產**」，以儲存資產。

<!--

### Upload assets {#upload-assets-firefly}

To upload the generated asset to the assets repository:

1. Click **[!UICONTROL Upload]**.
1. Select the asset folder to which you need to upload the asset and click **[!UICONTROL Select Folder]**.
 ![Upload asset](assets/upload-asset-firefly.jpg)

 -->

## 已儲存搜尋 {#saved-search}

搜尋功能可以在 [!DNL Assets view] 中輕鬆使用。您不僅可以從搜尋方塊中輸入關鍵字然後按下「Return」來查看結果，也可按一下來快速再次搜尋最近搜尋的關鍵字。

您也可以根據資產的中繼資料和類型的特定條件，來篩選搜尋結果。對於常用的篩選條件，若要改善搜尋體驗，[!DNL Assets view] 可讓您儲存搜尋參數。您稍後可以選取已儲存搜尋，按一下即可搜尋並套用篩選器。

若要建立已儲存搜尋，請搜尋某個資產、套用一個或更多篩選條件，然後按一下「[!UICONTROL 篩選器]」面板中的「**[!UICONTROL 另存新檔]** > **[!UICONTROL 儲存搜尋]**」。您也可以按一下「**[!UICONTROL 另存新檔]**」並選取「**[!UICONTROL 智慧型集合]**」將結果儲存為智慧型集合。如需詳細資料，請參閱[建立智慧型集合](manage-collections.md#create-a-smart-collection)。

![建立智慧型集合](assets/create-smart-collection.png)

<!-- TBD: Search behavior. Full-text search. Ranking and rank boosts. Hidden assets.
Report poor UX that users can only save a filtered search and not a simple search.
.
Are other supported files fully indexed and support full-text search? Eg. audio/videos files can at best have metadata indexed.
Anything about ranking of assets displayed in search results?

What about temporarily hiding an asset (suspending search on it) from the search results? If an asset is undergoing review collaboration, should it be used by others? Should it be hidden in search?

When userA is searching and userB add an asset that matches search results, will the asset display in search as soon as userA refreshes the page? Assuming indexing is near real-time. May not be so for bulk uploads.
-->

## 使用搜尋結果 {#work-with-search-results}

您可以選取搜尋結果中顯示的資產，然後執行以下動作：

* **尋找類似影像**：根據中繼資料和智慧標記在 Assets UI 中尋找類似影像資產。

* **詳細資料**：檢視和編輯資產屬性。

* **下載**：下載資產。

* 按一下&#x200B;**新增到集合**：將所選資產新增到集合中。

* **釘選到快速存取** :[釘選資產](my-workspace-assets-view.md) 以便以後需要時能更快地存取。所有釘選的項目都顯示在「我的工作區」的&#x200B;**快速存取**&#x200B;部分。

* **在 Adobe Express 中開啟**：到 Experience Manager Assets 畫面，在整合的 Adobe Express 中編輯影像。

* **編輯**：使用 Adobe Express 編輯影像。

* **共用連結**：與其他使用者 [共用資產連結](share-links-for-assets-view.md)，以便他們可以存取和下載該資產。

* **刪除**：刪除資產。

* **複製**：將資產複製到其他資料夾位置。

* **移動**：將資產移動到其他資料夾位置。

* **重新命名**：重新命名資產。

* **複製到資料庫**：將資產新增至資料庫。

* **指派任務**：將資產的任務指派給使用者。

* **觀看**：[監視](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/manage/search-assets)針對資產執行的作業。

## 設定搜尋優先首頁 {#configuring-search-first-homepage}

Assets檢視可讓您為組織選取預設登陸頁面。 使用「搜尋優先」作為首頁時，會有幾個選項讓您設定符合您品牌的背景和標誌影像，以量身打造品牌頁面。

若要設定搜尋優先首頁，請執行以下步驟：

1. 瀏覽至「**[!UICONTROL 設定]**」>「**[!UICONTROL 一般設定]**」。
1. 選取「**[!UICONTROL 搜尋優先]**」。接著會開啟搜尋優先相關設定。您可以設定首頁的[對齊方式](#setting-alignment-search-bar)或[設定背景和標誌影像](#setting-background-image-and-logo)。

### 設定搜尋列的對齊方式 {#setting-alignment-search-bar}

[!DNL Assets view] 可讓您變更搜尋列的對齊方式。您可以讓搜尋列顯示在中心或頂端。選取適當的對齊方式，然後按一下「**[!UICONTROL 儲存]**」。

![搜尋優先首頁對齊方式](assets/search-first-alignment.png)

### 設定首頁的背景和標誌影像 {#setting-background-image-and-logo}

您可以將品牌標誌和背景影像新增至搜尋優先首頁。執行以下步驟：

1. 瀏覽到「**[!UICONTROL 背景和標誌影像]**」(在「**[!UICONTROL 首頁]**」下方)。
1. 按一下「**[!UICONTROL 取代]**」以瀏覽現有資產存放庫中的影像。
1. 按一下「**[!UICONTROL 儲存]**」。[預覽](#preview-configured-homepage)變更以查看修改部分。

### 預覽已設定首頁 {#preview-configured-homepage}

您可以預覽以查看搜尋優先首頁的版面配置和格式。使用「**[!UICONTROL 預覽]**」，您可以根據需要更改版面配置或進行修改。若要預覽已設定首頁，請執行以下步驟：

1. 按一下「**[!UICONTROL 一般設定]**」，然後選取「**[!UICONTROL 搜尋優先]**」。
1. 瀏覽到「**[!UICONTROL 自訂搜尋優先首頁]**」，然後按一下「**[!UICONTROL 預覽]**」。切換「**[!UICONTROL 深色主題]**」按鈕以深色或淺色主題預覽首頁。
1. 按一下「**[!UICONTROL 關閉]**」即可關閉預覽畫面。

   ![搜尋優先首頁預覽](/help/assets/assets/search-first-preview.gif)


<!--

## Contextual Search {#contextual-search}

You can also search assets available in the repository by defining text prompts. Experience Manager Assets automatically transforms those text prompts to search filters and displays the search results. You can view and modify automatic filters using the Filters Pane to further narrow down the search results.

### Access Contextual Search {#access-contextual-search}

To access Contextual Search in Experience Manager Assets:

1. Click **[!UICONTROL Search]** in the left pane.

   ![Contextual Search](assets/access-contextual-search.png)

1. Define the text prompt in the Search text box and click **[!UICONTROL Contextual Search]**.

   ![Contextual Search text prompt](/help/assets/assets/wknd-contextual-search.png)

   [!DNL Experience Manager Assets] displays the search results.

### Supported filters {#supported-filters}

Contextual Search supports the following filters out-of-the-box. Base your text prompts on these filters to view appropriate search results.

* Image height

* Image width

* File type: image, document, video, or folder.

* MIME type: JPG, PNG, TIFF, GIF, MP4, PDF, PPTX, DOCX or XLSX

* Created date

* Modified date

* Expiration date

* Asset status: Approved, Rejected, or all

* Expired assets

### Examples for the text prompts {#text-prompts-examples}

**Example 1**

**Text Prompt**: Images created this month.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 1](assets/contextual-search-example1.png)

**Example 2**

**Text prompt**: Images at least 200px tall and 100px wide with beach and clear sky.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 2](assets/contextual-search-example2.png)

**Example 3**

**Text prompt**: I need images of blue sky that are 1500 and 2500 pixel height and created in the past month that is not expired and approved.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 3](assets/contextual-search-example3.png)

The following video illustrates the end-to-end process from accessing the Contextual Search User Interface to defining text prompts, and viewing the search results.

>[!VIDEO](https://video.tv.adobe.com/v/3428407)

### Disable Contextual Search {#disable-contextual-search}

Administrators also have the option to disable Contextual Search for users in your organization. To do so, execute the following steps:

1. Navigate to **[!UICONTROL Settings]** > **[!UICONTROL General Settings]**.

1. In the [!UICONTROL Contextual Search] section, turn off the **[!UICONTROL Enable Contextual Search for your organization]** toggle to disable the Contextual Search feature for all users in your organization.  

### Contextual Search feedback {#contextual-search-feedback}

If you need to provide feedback on the Contextual Search feature, click ![Contextual Search icon](assets/do-not-localize/Smock_Help_18_N.svg)  and click the Feedback icon. Select the feedback type, specify the subject and description, and click **[!UICONTROL Submit]**.

![Contextual Search feedback](assets/contextual-search-feedback.png)

-->

## 後續步驟 {#next-steps}

* [觀看在Assets檢視中搜尋資產的相關影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/using.html?lang=zh-Hant)

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)。

* 聯絡[客戶服務](https://experienceleague.adobe.com/zh-hant?support-solution=General#support)



