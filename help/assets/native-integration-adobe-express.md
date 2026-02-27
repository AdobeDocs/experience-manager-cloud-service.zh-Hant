---
title: 使用內容建議程式存取Adobe Express中的AEM Assets
description: 透過內容建議程式，直接在原生AEM Assets整合中探索及存取Adobe Express。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 6d80567106fe7c32d8073ca093f895ff28500413
workflow-type: tm+mt
source-wordcount: '2581'
ht-degree: 1%

---

# 使用內容建議程式存取Adobe Express中的AEM Assets {#native-integration-adobe-express-using-content-advisor}

Adobe Experience Manager (AEM) Assets與Adobe Express原生整合，可讓您使用「內容顧問」，直接在Express介面中探索、存取及使用AEM Assets的資產。

Content Advisor將智慧型內容感知資產探索直接帶給您的創意工作流程，可轉換您在Adobe Express中探索和使用資產的方式。 內容顧問不會透過輸入關鍵字來搜尋資產，而是會根據您的畫布內容、行銷活動簡訊和意圖，顯示相關的已核准資產，協助您更快找到正確的資產。

透過智慧的建議、對Dynamic Media轉譯的存取權以及資產中繼資料的完整可見度，內容警告器可讓您在不離開Adobe Express的情況下有效找到、評估及使用AEM Assets中的資產。 這可確保更快速地建立內容、改善資產重複使用，以及一致地使用經過核准、符合品牌規範的資產。

![內容顧問橫幅影像](assets/content-advisor-banner-image.png)

您也可以將資產放入Express畫布並將新內容或已編輯的內容儲存回AEM Assets，確保資產管理和治理的中央化。 與Adobe Express的原生整合提供下列主要優點：

* 透過內容感知資產探索和建議，加速內容建立。

* 透過編輯現有資產和將新資產儲存到AEM Assets提高了內容重複使用率。

* 更快速地存取已核准、通道最佳化的Dynamic Media轉譯。

* 減少建立新資產或新版本的時間和精力，同時維持品牌一致性。

## 先決條件 {#prerequisites}

存取Adobe Express和AEM Assets內至少一個環境的許可權。 環境可以是任何Assets as a Cloud Service存放庫。

## 在 Adobe Express 編輯器中使用 AEM Assets {#use-aem-assets-in-express}

執行以下步驟，開始在Adobe Express編輯器中使用AEM Assets：

1. 開啟 Adobe Express Web 應用程式。

2. 載入新範本或專案，或建立資產，以開啟新的空白畫布。

3. 按一下左側導覽窗格中可用的&#x200B;**[!UICONTROL Assets]**。 Adobe Express會顯示[內容警告器](#intelligent-asset-discovery-content-advisor)，其中列出您有權存取的存放庫，以及根層級可用的資產和資料夾清單。

4. 使用[內容建議程式](#intelligent-asset-discovery-content-advisor)瀏覽或搜尋存放庫中的資產，然後將它們拖放到畫布上。 或者，按一下資產以將其放在畫布上。 您也可以依各種條件篩選![篩選](assets/do-not-localize/filter.svg)資產，例如核准狀態、檔案型別、MIME型別和維度。

   >[!NOTE]
   >
   >依維度篩選不適用於視訊。

   ![包括資產附加元件中的資產](assets/native-express-content-advisor-home.png)

## 使用Content Advisor智慧型資產探索 {#intelligent-asset-discovery-content-advisor}

內容警告器會根據您的畫布內容或行銷活動簡報，使用智慧型、內容感知的建議來協助您探索相關資產。 它也可讓您選取已針對使用案例最佳化的頻道Dynamic Media轉譯。


「內容建議程式」會在「清單」和「格線」檢視中顯示檔案、資料夾和集合的清單。 它可讓您將PNG、JPEG、PSD、MP4、SVG和PDF格式的資產新增至Express畫布。 您也可以按一下資產卡上可用的![資訊圖示](assets/info-icon.svg)圖示，以預覽可捲動的PDF檔案或任何其他格式型別。

按一下「![資訊」圖示](assets/info-icon.svg)圖示，也可以檢視&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中可用的資產中繼資料，或檢視[動態媒體](#dynamic-media-renditions-content-advisor)索引標籤中可用的動態媒體轉譯。 將建議內容拖放至畫布上。 或者，按一下資產以自動將其放到畫布上。

![Adobe Express中的資產中繼資料](assets/express-native-integration-metadata.png)


>[!IMPORTANT]
> 
>請確定您從&#x200B;**存放庫**&#x200B;下拉式清單中選取&#x200B;**作者**&#x200B;存放庫。 **傳遞**&#x200B;存放庫未顯示「內容建議程式」功能。
>
> 此外，**傳遞**&#x200B;存放庫沒有在資料夾和集合中組織的資產。 所有資產都會以平面結構顯示在根層級。

「內容建議程式」提供下列主要功能：

* [更聰明地探索資產的AI 搜尋](#content-advisor-ai-search)

* [根據內容和意圖的智慧型建議](#smart-suggestions-content-advisor)

* [探索相關資產的Campaign簡介](#campaign-briefs-content-advisor)

* [可供使用的Dynamic Media資產轉譯](#dynamic-media-renditions-content-advisor)

* [存取與Assets檢視一致的資產中繼資料](#asset-metadata-content-advisor)

* [存取與Assets檢視一致的篩選器](#filters-content-advisor)

* [存取及重複使用最近和儲存的搜尋](#saved-searches-content-advisor)

* [在集合間和集合內搜尋資產](#search-collections-content-advisor)

### 更聰明地探索資產的AI 搜尋 {#content-advisor-ai-search}

「內容建議程式」使用進階搜尋功能，可瞭解使用者查詢的意義與意圖，而非依賴精確的關鍵字比對。 它使用人工智慧(AI)和機器學習，提供更準確且內容感知的結果。

傳統關鍵字式搜尋會尋找精確字詞，而AI 搜尋則解譯字詞、概念和使用者意圖之間的關係。 這可確保使用者找到他們要尋找的內容 — 即使他們的查詢用詞不同、包含拼寫錯誤或使用另一種語言。

Adobe Express中的![資產AI 搜尋](assets/express-native-integration-ai-search.png)

如果其主要優點包括：

* 多語言支援：可跨多種語言搜尋，不需要精確翻譯。 使用者無論查詢語言為何，都能找到相關內容。

* 處理拼字錯誤：解譯拼字錯誤和拼字錯誤，確保即使輸入不完美也能產生準確的結果。

* 瞭解同義字：提供相關辭彙和片語的結果，因此使用者不需要猜測正確的關鍵字。

* 內容感知搜尋：辨識查詢背後的目的，而不只是確切的字詞。

>[!IMPORTANT]
> 
>* 存取Content Advisor中的AI 搜尋所需的最低AEM發行版本為`21994`。


### 根據內容和意圖的智慧型建議 {#smart-suggestions-content-advisor}

「內容建議程式」會根據「快速」畫布內容的內容與意圖，顯示智慧型建議。 這可協助您快速探索及使用符合內容需求的資產，而不需要費時的手動搜尋。

在Adobe Express中![建議的內容顧問內容](assets/express-native-integration-suggested-content.png)

>[!IMPORTANT]
> 
>* 「內容建議程式」會根據文字圖層或「快速」畫布標題中可用內容的內容和意圖，顯示智慧型建議。 它不會根據畫布中可用的影像顯示結果。
>* 您必須簽署GenAI附加程式才能在「內容警告程式」中存取此功能。 若要簽署GenAI附加條款，請聯絡您的Adobe代表。
>* 存取此功能所需的最低AEM發行版本為`21994`。
>* 當您更新畫布時，智慧型建議不會自動更新。 按一下&#x200B;**建議內容**&#x200B;面板上的重新整理圖示，以檢視更新的建議清單。

### 探索相關資產的Campaign簡介 {#campaign-briefs-content-advisor}

內容警告器可讓您上傳行銷活動摘要檔案，以探索相關資產，而不需手動輸入搜尋關鍵字。 「內容建議程式」會分析行銷活動簡介中的資訊，以瞭解行銷活動的目的，並建議AEM Assets中可用的相關資產。

![包括資產附加元件中的資產](assets/upload-brief-native-express.png)

>[!IMPORTANT]
>
>* 「內容建議程式」會分析行銷活動簡報中文字形式的可用資訊，以建議相關資產。 它不會分析行銷活動簡報中作為影像可用的資訊。
>* 您可以上傳作為行銷活動簡短的支援檔案型別包括PDF、DOCX和TXT檔案。
>* 您必須簽署GenAI附加程式才能在「內容警告程式」中存取此功能。 若要簽署GenAI附加條款，請聯絡您的Adobe代表。
>* 存取此功能所需的最低AEM發行版本為`21994`。

### 可供使用的Dynamic Media資產轉譯 {#dynamic-media-renditions-content-advisor}

Dynamic Media轉譯提供立即可用且通道最佳化的資產版本，包括[影像預設集](/help/assets/dynamic-media/managing-image-presets.md)、[智慧型裁切](/help/assets/dynamic-media/image-profiles.md)、格式型別和色彩設定檔。 這些轉譯有助於確保所選資產符合管道和設計需求，而無需手動編輯或資產複製。

您也可以套用Dynamic Media修飾元來即時預覽調整，然後再將轉譯放到「快速」畫布上，以便在維持資產一致性和品質的同時，更快速地選取最合適的轉譯。

按一下資產卡上的![資訊圖示](assets/info-icon.svg)圖示，然後選取&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;索引標籤以檢視資產的可用轉譯。 您可以選擇檢視[Dynamic Media Scene7](/help/assets/dynamic-media/dynamic-media.md)轉譯或具有OpenAPI的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)轉譯。 當您為資產選取&#x200B;**[!UICONTROL OpenAPI]**&#x200B;時，只有當資產獲得核准且可用於具有OpenAPI的Dynamic Media時，才會顯示可用的轉譯。

您必須具備有效的AEM Dynamic Media授權才能檢視Dynamic Media索引標籤。

![檢視Dynamic Media轉譯](assets/native-express-dynamic-media.png)

按一下![預覽圖示](assets/do-not-localize/preview-icon.svg)圖示以預覽轉譯，或按一下轉譯名稱以自動將其放到畫布上。 您也可以預覽轉譯，然後將其拖放以將影像放置到畫布上。

![預覽Dynamic Media轉譯](assets/native-express-dynamic-media-preview.png)

按一下&#x200B;**[!UICONTROL 新增修飾元]**，在文字方塊中指定修飾元，然後按下Enter以即時將轉換套用至轉譯。 同樣地，您可以將多個修飾元新增至轉譯並預覽這些轉換。 將資產從預覽拖放至畫布上。 套用這些修飾元後的轉譯不會儲存。 檢視[Dynamic Media Scene7](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference)和[Dynamic Media with OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat)支援的修飾元清單。

>[!IMPORTANT]
> 
>Dynamic Media提供最佳化的大型資產轉譯，有助於克服Adobe Express （網頁）中80MB上傳檔案大小的限制。 Dynamic Media轉譯可大幅縮減檔案大小，同時保留視覺品質。 例如，300MB的TIFF資產可以當作2.5MB的轉譯專案來提供，而不會影響品質，讓您能夠在Adobe Express中有效率地使用高解析度資產。

### 存取與Assets檢視一致的資產中繼資料 {#asset-metadata-content-advisor}

內容警告器可讓您存取AEM Assets中定義的資產屬性，包括Assets檢視中可用的中繼資料。 「內容建議程式」會使用與「Assets檢視」相同的中繼資料組態，複製「Assets檢視資產詳細資訊」頁面中的中繼資料標籤和內容清單。 這可讓您在選取資產之前，先檢閱重要資產詳細資訊，例如標題、說明、格式、大小和其他中繼資料。 存取資產屬性可協助您為內容選擇正確且已核准的資產。

![Assets在內容警告器中檢視中繼資料](assets/native-express-asset-metadata.png)

按一下資產卡上的![資訊圖示](assets/info-icon.svg)圖示，然後選取&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤以檢視資產中繼資料。 您也可以檢視與Assets檢視中存在的資產中繼資料一致的其他資產中繼資料標籤，例如「產品」、「促銷活動」和「標籤」。

「內容建議程式」會以唯讀檢視顯示檔案的屬性（中繼資料）。 集合和資料夾不會顯示屬性。

### 存取與Assets檢視一致的篩選器 {#filters-content-advisor}

「內容建議程式」在Express中提供與Assets檢視中相同的篩選功能，可讓您使用預先定義的篩選器來調整資產。 Assets檢視中提供的相同篩選功能也適用於特定於內容型別的篩選器，例如檔案、資料夾和集合。 這可確保一致的資產探索體驗，並幫助您在Adobe Express中有效找到相關資產。

如果您未透過篩選器結構描述在Assets檢視中設定篩選器，內容警告器會顯示立即可用的篩選器，包括檔案型別、檔案格式、資產狀態、檔案大小、影像寬度、影像高度、修改日期和建立日期。

### 存取及重複使用最近和儲存的搜尋 {#saved-searches-content-advisor}

您也可以使用在Assets檢視中建立的已儲存搜尋，讓您重複使用預先定義的搜尋條件。 已儲存的搜尋在Assets檢視和內容警告器之間在各種瀏覽器上運作一致。 這可協助您使用在AEM Assets和Adobe Express中一致的搜尋模式，有效率地找到資產。

若要使用「內容建議程式」儲存您經常使用的搜尋：

1. 指定搜尋字詞（選擇性），按一下篩選器圖示，然後根據您的要求選取選項以建立搜尋查詢。

1. 按一下&#x200B;**[!UICONTROL 套用]**&#x200B;以檢視結果。

1. 按一下篩選器圖示> **管理已儲存的搜尋** > **建立新的已儲存搜尋**。

1. 指定搜尋的名稱，然後按一下![資訊圖示](assets/do-not-localize/checkmark-icon.svg)以儲存。 搜尋會顯示在專案清單中。

   ![已儲存搜尋內容顧問](assets/native-express-saved-searches.png)

若要套用任何已儲存的搜尋專案，請按一下篩選器圖示，從&#x200B;**[!UICONTROL 已儲存的搜尋]**&#x200B;下拉式清單中選取搜尋專案，然後按一下&#x200B;**[!UICONTROL 套用]**。

「內容建議程式」會儲存您最近的搜尋，並可讓您儲存常用的搜尋以供日後快速存取。 Assets檢視和「內容建議程式」之間最近的搜尋清單不一致。 相同使用者在Assets檢視和「內容警告器」中可以有不同的一組最近搜尋。 如果您使用無痕模式來存取「內容建議程式」，則無法使用最近的搜尋清單。 此外，最近使用的搜尋不會跨相同使用者的不同瀏覽器共用，且會因AEM環境而異。



「內容建議程式」中尚未提供Assets檢視中提供的「預設儲存的搜尋」功能。

### 在集合間和集合內搜尋資產 {#search-collections-content-advisor}

內容警告器可讓您搜尋所有集合中的資產或集合，或將搜尋限制在特定集合中。 這可協助您快速找到並使用已組織集合中的資產，同時保留其預期組織內容。

## 使用AEM上傳功能取代影像 {#replace-image-using-aem-upload}

此外，您可以使用&#x200B;**[!UICONTROL AEM上傳]**&#x200B;來取代新增的影像。 要執行此操作，請執行下列步驟：

1. 瀏覽或搜尋資產，並將它拖放至畫布上。

1. 選取您要取代的影像。 按一下「取代」**&#x200B;**，然後選取&#x200B;**[!UICONTROL 「AEM Assets」]**。

   ![AEM取代](assets/aem-replace.png)

1. [內容警告器](#intelligent-asset-discovery-content-advisor)會在左側導覽窗格中開啟。 Adobe Express會顯示您有權存取的存放庫清單，以及在根層級可用的資產和資料夾清單。 從那裡選取要預覽畫布上取代的資產，然後按一下[取代]確認。**&#x200B;**

   >[!NOTE]
   >
   > 不支援SVG檔案型別。

## 將 Adobe Express 專案儲存在 AEM Assets 中 {#save-express-projects-in-assets}

在Express畫布中加入適當的修改後，您便可將其儲存在AEM Assets中。

1. 按一下[共用]&#x200B;**&#x200B;**&#x200B;開啟[共用]&#x200B;**&#x200B;**&#x200B;對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-share.png)

2. 選取&#x200B;**AEM Assets**。 Adobe Express會顯示上傳對話方塊。

3. 選取&#x200B;**目前頁面**&#x200B;或&#x200B;**所有頁面**。 指定要匯出的資產的名稱和格式。 您可以匯出PNG、JPEG、PDF、MP4、MP4+PNG或MP4+JPEG格式的畫布內容。 格式會根據畫布頁面上的資產自動調整。
選取&#x200B;**目前頁面**&#x200B;會將目前頁面上的資產儲存到您的目的地資料夾。 如果您選取「**所有頁面**」，且匯出格式不是PDF，則所有畫布頁面都會以個別檔案的形式儲存在目的地資料夾的新資料夾中。 如果匯出格式為PDF，則所有畫布頁面都會儲存為目的地資料夾中的單一PDF檔案。

4. 按一下&#x200B;**目的地資料夾**&#x200B;下的資料夾圖示，以選取位置並儲存資產。

   ![將資產儲存在 AEM 中](/help/assets/assets/page-selection-and-destination-folder.png)

5. 可選：您可以使用&#x200B;**專案或行銷活動名稱**&#x200B;欄位，新增您上傳的行銷活動中繼資料。 您可以使用現有的名稱或建立新名稱。 您可以為上傳定義多個專案或行銷活動名稱。 若要註冊名稱，只需輸入名稱並按Enter即可。
作為最佳作法，Adobe建議在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

6. 同樣地，定義&#x200B;**[!UICONTROL 關鍵字]**&#x200B;和&#x200B;**[!UICONTROL 管道]**&#x200B;欄位的值。

7. 按一下&#x200B;**[!UICONTROL 上傳]**&#x200B;以將資產上傳至AEM Assets。

   >[!NOTE]
   >
   > 如果您要將資產儲存至Content Hub傳遞存放庫，專案或行銷活動名稱為必填欄位。 在此情況下，您也不需要選取目的地資料夾，因為它是自動從中繼資料衍生的。

## 支援的檔案格式 {#supported-file-formats-import-assets}

Adobe Express原生支援[上可用的格式。檢閱最低影像需求](https://helpx.adobe.com/tw/express/web/image-creation-and-editing/change-file-formats/image-requirements.html)。 不過，AEM Assets支援下列格式型別：

| 支援的格式 | 最大尺寸/解析度 | 檔案大小上限 |
|------------------|---------------------------------------------|---------------|
| JPEG | 65 MP (例如8K × 8K或16K × 4K) | 80 MB桌上型電腦，40 MB行動裝置 |
| PNG | 65 MP (例如8K × 8K或16K × 4K) | 80 MB桌上型電腦，40 MB行動裝置 |
| SVG | — | 250 KB |
| MP4 | 3840 × 3840畫素 | 200 MB |
| PSD | 65 MP (例如8K × 8K或16K × 4K) | 80 MB桌上型電腦，40 MB行動裝置 |
| PDF | — | — |


## 限制 {#limitations}

1. 對於匯入和匯出，支援的視訊檔案型別為MP4。

2. 對於&#x200B;**MP4視訊匯入**，不支援具有透明背景（Alpha色版）的視訊。
   <!--
   1. The maximum file size supported is 200 MB. If this limit exceeds, an alert message displays.
   2. The maximum supported resolution is 3840 X 3840 pixels.
   3. Videos with transparent backgrounds (alpha channel) are not supported.
   -->

3. 對於&#x200B;**MP4視訊匯出**，支援的檔案大小上限為200 MB。 如果超過此限制，警報會建議將視訊縮減至200 MB以下，或在下載視訊後手動上傳至AEM Assets目的地資料夾。

<!--
## Content Advisor Properties {#content-advisor-props}

You can configure following properties for the content advisor:

* `featureSet` : This property enables the Content Advisor MFE.

    ```
    featureSet: [
        ...defaultFeatures, /* to include all default features */
        'advisor', /* enables Content Advisor features */
        'content-fragments', /* enables Content Fragments */
    ],
    ```

* `rail:true/false` : If marked true, Content Advisor is rendered in a left rail view. If it is marked false, the Content Advisor is rendered in modal view.

## Browse assets using Content Advisor {#browse-assets-content-advisor}

<!--In the Modal View of Content Advisor, you can access both [Assets](#using-assets-tab) and [Content Fragments](#using-content-fragments) within a unified interface.

### Assets tab{#assets-tab}

The **[!UICONTROL Assets]** tab allows you to browse or filter available assets, preview them before selection, and choose appropriate **[!UICONTROL Dynamic Media]** [renditions](renditions.md) or [smart crops](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles) as needed. Assets, folders, and collections are presented together in a single, streamlined experience. The interface also provides contextual recommendations based on the integrated application context, helping you quickly identify relevant content.

Within assets tab, you can access content by browsing [Files and folders](#content-advisor-files-and-folders) or viewing [Collections](#content-advisor-collections).

### Files and Folders tab{#content-advisor-files-and-folders}

Browsing content using Files and Folders allows you navigate your assets in a familiar hierarchical structure, making it easy to locate assets within the repository. To browse assets within files and folders, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Files & Folders]**. A hierarchical structure is then displayed, allowing you to easily locate and select the desired assets.

![Browse assets using files and folder](assets/browse-assets-content-advisor.png)

### Collections tab{#content-advisor-collections}

Browsing content using Collections allows you to access curated groups of assets within Collections. To browse assets within Collections, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Collections]**. The interface then displays curated groups of assets, enabling you to browse the content you need.

![Browse assets using Collections](assets/browse-assets-collections.png)

<!--
### Content Fragments tab{#content-fragments}

The [Content Fragments](/help/assets/content-fragments/content-fragments.md) tab displays structured assets, allowing you to browse, search, and filter fragments efficiently within the same interface. To browse assets using Content Fragments, navigate to the **[!UICONTROL Content Fragments]** tab to access and explore the fragments available in the repository.

![Browse assets using Content Fragments](assets/browse-assets-content-fragment.png)
-->


