---
title: 管理數位資產集合
description: 瞭解Adobe Experience Manager Assets中的集合概念。 瞭解如何與其他使用者一起收集、管理、編輯和收集。
contentOwner: AG
mini-toc-levels: 1
feature: Collections, Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 19%

---

# 管理集合 {#manage-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

集合是Adobe Experience Manager Assets中的一組資產。 使用集合在使用者之間共用資產。集合可以是靜態集合或基於搜尋結果的動態集合。

和檔案夾不同，集合可包含來自不同位置的資產。您可以與獲指派不同許可權層級（包括檢視、編輯等）的各種使用者共用集合。

您可以和使用者共用多個集合。每個集合都包含資產的參考資料。資產的參考完整性會跨越集合來維護。

根據集合整理資產的方式，集合有下列型別：

* 包含資產、資料夾和其他集合之靜態參考清單的集合。

* 根據搜尋條件動態包含資產的智慧型集合。

## 存取集合主控台 {#navigate-the-collections-console}

若要開啟&#x200B;**[!UICONTROL 集合]**&#x200B;主控台：

若要開啟&#x200B;**[!UICONTROL 集合]**，請選取Experience Manager標誌。 從導覽頁面，移至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 集合]**。

## 建立集合 {#create-a-collection}

您可以使用[靜態參考](#create-a-collection-with-static-references)或根據[搜尋條件型篩選器](#create-a-smart-collection)來建立集合。 您也可以從Lightbox建立集合。

### 使用靜態參考建立集合 {#create-a-collection-with-static-references}

您可以建立具有靜態參照的集合，例如，具有資產、資料夾、集合、迴轉集及影像集參照的集合。

1. 導覽至&#x200B;**[!UICONTROL 集合]**&#x200B;主控台。
1. 從工具列中選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立集合]**&#x200B;頁面中，輸入集合的標題和選擇性說明。
1. 新增成員至系列並指派適當的權限。或者，選取「 **[!UICONTROL 公用系列]** 」，讓所有使用者都能存取系列。

   >[!NOTE]
   >
   >若要讓成員與其他使用者共用集合，請在路徑`home/users`提供`dam-users`群組讀取許可權。 將許可權授與位於`/content/dam/collections`位置的使用者，讓使用者可以在彈出式清單中檢視集合。 或者，讓使用者成為`dam-users`群組的一部分。

1. （選用）為集合新增縮圖影像。
1. 選取「**[!UICONTROL 建立]**」，然後選取「**[!UICONTROL 確定]**」以關閉對話方塊。 具有指定標題和屬性的系列會在「系列」主控台中開啟。

   >[!NOTE]
   >
   >Experience Manager Assets可讓您為集合建立稽核任務，其方式類似於您為資產資料夾建立稽核任務的方式。

   若要將資產新增至收藏集，請導覽至Assets使用者介面。 如需詳細資訊，請參閱[將資產新增至集合](#add-assets-to-a-collection)。

### 使用dropzone建立集合 {#create-collections-using-dropzone}

您可以從Assets UI將資產拖曳至收藏集。 您也可以建立收藏集的副本，並將資產拖曳至該處。

1. 從Assets使用者介面，選取您要新增至集合的資產。
1. 將資產拖曳至集合&#x200B;**區域中的**&#x200B;拖放位置。 或者，從工具列選取&#x200B;**[!UICONTROL 至集合]**&#x200B;圖示。
1. 在&#x200B;**[!UICONTROL 新增至集合]**&#x200B;頁面中，從工具列選取&#x200B;**[!UICONTROL 建立集合]**&#x200B;圖示。 如果您想要將資產新增至現有的集合，請從頁面中選取資產，然後選取「**[!UICONTROL 新增]**」。 依預設，會選取最近更新的系列。
1. 在「建 **[!UICONTROL 立新系列]** 」對話方塊中，指定系列的名稱。如果您希望系列可供所有使用者存取，請選取「公用 **[!UICONTROL 系列」]**。
1. 選取&#x200B;**[!UICONTROL 繼續]**&#x200B;以建立集合。

### 建立智慧型集合 {#create-a-smart-collection}

智慧型集合會使用搜尋條件來動態填入資產。 您可以只使用檔案來建立Smart Collection，而不使用資料夾或檔案與資料夾。

1. 導覽至Assets UI，然後選取&#x200B;**[!UICONTROL 搜尋]**&#x200B;圖示。
1. 在[全域搜尋]方塊中輸入搜尋關鍵字，並選取`Enter`。 選取GlobalNav圖示以顯示「篩選器」面板，並從「搜尋」面板套用搜尋篩選器。
1. 從&#x200B;**[!UICONTROL 檔案與資料夾]**&#x200B;清單中，選取&#x200B;**[!UICONTROL 檔案]**。
1. 選取&#x200B;**[!UICONTROL 儲存智慧型集合]**。
1. 指定集合的名稱。 選取「**[!UICONTROL 公用]**」，將具有檢視器角色的DAM Users群組新增至智慧型集合。

   >[!NOTE]
   >
   >如果您選取&#x200B;**[!UICONTROL 公用]**，在您建立智慧型集合後，所有具有「擁有者」角色的人都可以使用該集合。 如果您取消&#x200B;**[!UICONTROL 公用]**&#x200B;選項，DAM使用者群組將不再與智慧型集合相關聯。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以建立智慧型集合，然後關閉訊息方塊以完成程式。 新的智慧型系列也會新增至&#x200B;**[!UICONTROL 已儲存的搜尋]**&#x200B;清單。
「建立智慧選 **[!UICONTROL 擇」按鈕的標籤將更改為]** 「編 **[!UICONTROL 輯智慧選擇」]**。要編輯智慧系列的設定，請從「檔案和文 **[!UICONTROL 件夾]** 」列 **[!UICONTROL 表中選擇「檔案]** 」。接著，選取&#x200B;**[!UICONTROL 編輯智慧選擇]**&#x200B;按鈕。

## 將資產新增至集合 {#add-assets-to-a-collection}

您可以將資產新增至包含參照資產或資料夾清單的集合。

>[!NOTE]
>
>智慧型集合會使用搜尋查詢來填入資產。 因此，資產和資料夾的靜態參考不適用於它們。

1. 在Assets UI中，導覽至您要新增至集合的資產位置。
1. 選取資產，然後從工具列選取&#x200B;**[!UICONTROL 至集合]**&#x200B;圖示。 或者，您可以將資產拖曳到&#x200B;**[!UICONTROL 拖放至Collection]**&#x200B;區域。 當拖放區域變成使用中且其標籤變更為&#x200B;**[!UICONTROL 拖放到「新增」]**&#x200B;時，請放開滑鼠按鈕。
1. 在&#x200B;**[!UICONTROL 新增至集合]**&#x200B;頁面中，選取您要新增資產的集合。
1. 選取「**[!UICONTROL 新增]**」，然後關閉確認訊息。 資產會新增至集合中。

## 編輯智慧型集合 {#edit-a-smart-collection}

智慧型集合是透過儲存搜尋來建置，因此您可以修改[儲存的搜尋](#saved-searches)的搜尋引數來變更其內容。

1. 在Assets使用者介面中，從工具列選取&#x200B;**[!UICONTROL 搜尋]**&#x200B;圖示。
1. 將游標放在Omnisearch方塊中，選取`Enter`鍵。
1. 選取「全域導覽」圖示以顯示「篩選器」面板。
1. 從「保 **[!UICONTROL 存的搜索]** 」清單中，選擇要修改的智慧系列。「搜尋」面板會顯示為儲存的搜尋設定的篩選器。
1. 從&#x200B;**[!UICONTROL 檔案與資料夾]**&#x200B;清單中，選取&#x200B;**[!UICONTROL 檔案]**。
1. 視需要修改一或多個篩選器。 選取&#x200B;**[!UICONTROL 編輯智慧型集合]**。 您也可以編輯智慧型集合的名稱。
1. 選取&#x200B;**[!UICONTROL 儲存]**。**[!UICONTROL 編輯智慧型集合]**&#x200B;對話方塊就會顯示。
1. 選取&#x200B;**[!UICONTROL 覆寫]**，以已編輯的集合取代原始的智慧型集合。 或者，選取「**[!UICONTROL 另存新檔]**」以個別儲存編輯的集合。
1. 在確認對話方塊中，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成程式。

## 檢視和編輯集合中繼資料 {#view-and-edit-collection-metadata}

收藏集中繼資料包含有關收藏集的資料，包括新增的任何標籤。

1. 從「集合」控制檯選取集合，然後從工具列選取&#x200B;**[!UICONTROL 屬性]**&#x200B;圖示。
1. 在「系列 **[!UICONTROL 中繼資料]** 」頁面中，從「基本」和「進階」標籤檢視系 **[!UICONTROL 列中繼資]** 料 **&#x200B;**&#x200B;。
1. 視需要修改中繼資料，然後從工具列選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存變更。

### 大量編輯收藏集中繼資料 {#edit-collection-metadata-in-bulk}

您可以同時編輯多個集合的中繼資料。 此功能可協助您在多個集合中快速復寫常見的中繼資料。

1. 在「收藏集」控制檯中，選取您要編輯中繼資料的兩個或多個收藏集。
1. 從工具列中選取&#x200B;**[!UICONTROL 屬性]**&#x200B;圖示。
1. 在「系 **[!UICONTROL 列中繼資料]** 」頁面中，視需要編輯「基本」和「進階」標籤下的中繼資料 **&#x200B;**&#x200B;**&#x200B;** 。
1. 從工具列選取&#x200B;**[!UICONTROL 儲存並關閉]**，然後關閉確認對話方塊以完成程式。
1. 若要將新中繼資料附加至現有的中繼資料，請選取「 **[!UICONTROL Apend」模式]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。選取&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >「附加」模式僅適用於可包含多個值的欄位。對於只能包含單一值的欄位，即使您選取「附加」模式，新中繼資料也不會附加至欄位中的現 **[!UICONTROL 有值]**。

## 搜尋 {#searching}

集合內的搜尋功能支援[搜尋集合](#search-collections)和[搜尋集合內的資產](#search-within-collections)。

### 搜尋集合 {#search-collections}

您可以從「集合」控制檯搜尋集合。 當您在Omnisearch方塊中使用關鍵字搜尋時，[!DNL Experience Manager Assets]會搜尋系列名稱、中繼資料和新增至系列中的標籤。

如果您從最上層搜尋集合，搜尋結果中只會傳回個別集合。 會排除Assets或集合中的資料夾。 在所有其他情況下（例如，在個別集合或資料夾階層中），所有相關的資產、資料夾和集合都會傳回。

### 在集合中搜尋 {#search-within-collections}

在「系列」控制檯中，選取要開啟的系列。

在收藏集中，[!DNL Experience Manager]搜尋僅限於您檢視之收藏集中的資產（及其標籤和中繼資料）。 在資料夾中搜尋時，系統將會傳回目前資料夾中所有相符的資產和子資料夾。 在集合中搜尋時，系統只會傳回符合的資產、資料夾及屬於集合直接成員的其他集合。

## 編輯集合設定 {#edit-collection-settings}

您可以編輯收藏集設定（例如標題和說明），或將成員新增至收藏集。

1. 選取集合，然後選取工具列中的&#x200B;**[!UICONTROL 設定]**&#x200B;圖示。 或者，使用集合縮圖中的&#x200B;**[!UICONTROL 設定]**&#x200B;快速動作。
1. 修改「系列設定」頁面中 **[!UICONTROL 的系列設定]** 。例如，修改系列標題、說明、成員和權限，如「新增系列」中所 [述](#create-a-collection)。
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更。

## 刪除集合 {#delete-a-collection}

1. 在「系列」控制檯中，選取一或多個系列，然後在工具列上選取刪除圖示。
1. 在對話方塊中，選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認刪除動作。

   >[!NOTE]
   >
   >您也可以[刪除已儲存的搜尋](#saved-searches)來刪除智慧型集合。

## 下載集合 {#download-a-collection}

下載收藏集時，會下載收藏集中資產的整個階層，包括資料夾和子收藏集。

1. 從「系列」控制檯中，選取要下載的一或多個系列。
1. 從工具列中選取下載圖示。
1. 在&#x200B;**[!UICONTROL 下載]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 下載]**。 如果您想要下載集合中資產的轉譯，請選取「**[!UICONTROL 轉譯]**」。<!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   當您選取要下載的收藏集時，將會下載收藏集下的完整資料夾階層。 若要將您下載的每個收藏集（包括父收藏集下巢狀子收藏集中的資產）加入個別資料夾中，請選取&#x200B;**[!UICONTROL 為每個資產建立個別資料夾]**。

## 編輯多個集合的中繼資料屬性 {#editing-metadata-properties-of-multiple-collections}

Adobe Enterprise Manager Assets可讓您大量編輯許多集合的中繼資料。 使用[!UICONTROL 屬性]頁面對多個集合執行中繼資料變更，例如，將中繼資料屬性變更為通用值，或新增或修改標籤。

若要自訂中繼資料[!UICONTROL 屬性]頁面，包括新增、修改、刪除中繼資料屬性，請使用結構描述編輯器。

>[!NOTE]
>
>大量編輯方法適用於集合中可用的資產。 對於跨資料夾可用的資產，或符合共同條件的資產，可在搜尋[&#128279;](/help/assets/search-assets.md#metadata-updates)後大量更新中繼資料。

1. 在集合控制檯中，選取您要編輯的集合。
1. 從工具列中選取&#x200B;**[!UICONTROL 屬性]**&#x200B;以開啟所選集合的[!UICONTROL 屬性]頁面。
1. 修改各種標籤下所選集合的中繼資料屬性。

   >[!NOTE]
   >
   >您為所選集合新增的中繼資料會覆寫這些集合先前的中繼資料，但標籤除外。 您在&#x200B;**[!UICONTROL 標籤]**&#x200B;欄位中新增的任何標籤都會附加至中繼資料中的現有標籤清單。

1. 若要檢視特定集合的中繼資料屬性，請取消選取集合清單中剩餘的集合。 中繼資料編輯器欄位會填入特定集合的中繼資料。

   >[!NOTE]
   >
   >* 在集合屬性頁面中，您可以取消選取範圍，從集合清單中移除集合。 集合清單預設會選取所有集合。 您移除的集合中繼資料並未更新。
   >* 在清單頂端，選取&#x200B;**[!UICONTROL 標題]**&#x200B;附近的核取方塊，以在選取集合與清除清單之間切換。

1. 儲存變更。

## 建立巢狀集合 {#create-nested-collections}

您可以將集合新增至另一個集合，藉此建立巢狀集合。

1. 從「集合」控制檯中，選取想要的集合或集合群組，然後在工具列中選取&#x200B;**[!UICONTROL 至集合]**。
1. 從&#x200B;**[!UICONTROL 新增至集合]**&#x200B;頁面，選取要新增集合的集合。

   >[!NOTE]
   >
   >預設會在&#x200B;**[!UICONTROL 新增至集合]**&#x200B;頁面中選取最近更新的集合。

1. 選取&#x200B;**[!UICONTROL 新增]**。 訊息會確認此集合已新增至&#x200B;**[!UICONTROL 選取目的地]**&#x200B;頁面中的目標集合。 關閉訊息以完成程式。

>[!NOTE]
>
>智慧型集合無法巢狀化。 換言之，智慧型集合不能包含任何其他集合。

## 已儲存搜尋 {#saved-searches}

在「資產」使用者介面中，您可以根據特定規則、搜尋准則或自訂搜尋刻面來搜尋或篩選資產。如果您將這些項目儲存為「 **[!UICONTROL 已儲存的搜尋]**」，您稍後可從「篩選」面板的「已儲存的搜尋 **&#x200B;**&#x200B;」清單中存取。建立儲存的搜尋也會建立智慧型系列。

儲存的搜尋會在您建立智慧型系列時建立。智慧型系列會自動新增至「已儲 **[!UICONTROL 存的搜尋]** 」清單。集合的「已儲存的搜尋」查詢儲存在CRXDE中相對位置`/content/dam/collections/`的`dam:query`屬性中。 您可以儲存的搜尋以及清單中顯示的已儲存搜尋沒有限制。

>[!NOTE]
>
>您可以使用與共用靜態集合相同的方式來共用智慧型集合。

編輯已儲存的搜尋與編輯智慧型集合相同。 如需詳細資訊，請參閱[編輯智慧型集合](#edit-a-smart-collection)。

若要刪除已儲存的搜尋，請執行下列步驟：

1. 在Assets使用者介面中，從工具列選取搜尋圖示。

1. 將游標放在Omnisearch欄位中，選取`Enter`鍵。
1. 選取「全域導覽」圖示以顯示「篩選器」面板。
1. 從&#x200B;**[!UICONTROL 儲存的搜尋]**&#x200B;清單中，選取您要刪除的智慧型系列旁的&#x200B;**[!UICONTROL 刪除]**。
1. 在對話方塊中，選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除儲存的搜尋。

## 對集合執行工作流程 {#run-a-workflow-on-a-collection}

您可以為集合中的資產執行工作流程。 如果集合包含巢狀集合，工作流程也會在巢狀集合內的資產上執行。 不過，如果收藏集和巢狀收藏集包含重複資產，工作流程僅會針對此類資產執行一次。

1. 在「系列」控制檯中，選取您要執行工作流程的系列。
1. 選取GlobalNav圖示，然後從清單中選擇&#x200B;**[!UICONTROL 時間表]**。
1. 從時間軸選取底部的脫字元圖示，然後選取&#x200B;**[!UICONTROL 開始工作流程]**。
1. 在「開 **[!UICONTROL 始工作流]** 」部分，從清單中選擇工作流模型。例如，選取「 **[!UICONTROL DAM更新資產」模型]** 。
1. 輸入工作流程的標題，並選取&#x200B;**[!UICONTROL 開始]**。
1. 在對話方塊中，選取&#x200B;**[!UICONTROL 繼續]**。 工作流程會在集合中的所有資產上執行。

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
* [搜尋 Facet](search-facets.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [建立集合的稽核任務](/help/assets/bulk-approval.md)
