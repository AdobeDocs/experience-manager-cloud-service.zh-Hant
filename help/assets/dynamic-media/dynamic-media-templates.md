---
title: 如何管理Dynamic Media範本？
description: 瞭解如何使用Dynamic Media範本編輯器建立WYSIWYG範本，並包含多個影像和文字圖層，以快速建立橫幅和傳單，並將其用於下游應用程式。
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: ea903daafedb420602700f4b1b4a3ad6bd8ede97
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 0%

---

# Dynamic Media範本{#dynamic-media-templates}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

使用Dynamic Media範本編輯器建立WYSIWYG範本，並包含多個影像和文字圖層，以快速建立橫幅和傳單，並將其用於下游應用程式。 您也可以將引數新增至範本中包含的影像和文字圖層，並使用[Dynamic Media URL](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media)即時更新這些圖層的值。

部分主要功能包括：

* **Dynamic Media WYSIWYG範本編輯器：**&#x200B;建立可自訂的橫幅（含影像與文字圖層）。
* **圖層引數化：**&#x200B;定義圖層的動態索引鍵值配對，以啟用即時更新。
* **Dynamic Media URL支援：**&#x200B;使用Dynamic Media URL作為範本，整合來自第一方或第三方應用程式的個人化值。
* **圖層可見性控制：**&#x200B;視需要動態隱藏或顯示圖層。
* **智慧型文字調整大小：**&#x200B;自動調整文字大小以符合指定的區域。

Dynamic Media範本的一些主要優點包括：

* **最佳化1:1 Personalization：**&#x200B;根據即時客戶訊號量身打造內容。
* **減少手動工作：**&#x200B;自動化並加速內容建立和管理。
* **確保一致的全通路體驗：**&#x200B;保持通路間的品牌一致性。
* **有效地重複使用內容：**&#x200B;避免單一使用內容，並透過動態引數化範本進行縮放。
* **降低風險：**&#x200B;即時更新定價、折扣和連結。
* **增強客戶參與度：**&#x200B;推動互動式、情境相關的體驗。

>[!NOTE]
>
>訂閱增強式安全性SKU的客戶無法在該Cloud Service方案中使用任何Dynamic Media功能，包括Dynamic Media範本。

## 開始之前{#prerequisites-for-dynamic-media-wysiwyg-template}

若要建立Dynamic Media範本，您必須擁有：

1. 存取Dynamic Media。
1. [已將AEM Assets執行個體中可用的影像與Dynamic Media同步，以便用於建立範本](/help/assets/dynamic-media/config-dm.md)。

## 建立Dynamic Media WYSIWYG範本{#how-to-create-dynamic-media-wysiwyg-template}

若要建立DM範本，請遵循下列步驟：

1. [建立空白畫布](#create-a-canvas)
1. [將影像新增至畫布](#add-images-to-the-canvas)
1. [新增文字圖層至畫布](#add-text-to-the-canvas)
1. [編輯或刪除圖層](#edit-or-delete-a-layer)
1. [引數化圖層](#parameterise-a-layer)

### 建立空白畫布{#create-a-canvas}

執行以下步驟來建立空白畫布：

1. 導覽至Assets檢視，然後按一下左側面板中可用的&#x200B;**[!UICONTROL Dynamic Media Assets]**。

   ![](/help/assets/assets/dm-templates/DM-Assets1.png)

1. 按一下&#x200B;**[!UICONTROL 「建立範本]**」，將範本儲存在Dynamic Media Assets下，或導覽至資料夾，然後按一下&#x200B;**[!UICONTROL 「建立範本]**」，將範本儲存在該資料夾中。 **[!UICONTROL 新範本]**對話方塊隨即顯示。
   ![](/help/assets/assets/dm-templates/new-template.png)
若要[在&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;下建立資料夾](/help/assets/add-delete-assets-view.md)，請在&#x200B;**[!UICONTROL Assets]**&#x200B;下建立資料夾。 **[!UICONTROL Assets]**&#x200B;下的資料夾樹狀結構會復寫至&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;下。
1. 指定範本名稱、定義畫布寬度和高度，然後按一下[建立]。**** 空白畫布顯示，兩側都有選單選項以用於建立範本。 將游標停留在選單選項上可檢視其工具提示。
   ![](/help/assets/assets/dm-templates/blank-canvas-page.png)

>[!NOTE]
>
> 允許的寬度和高度範圍是從50到5000。

**右窗格上的功能表選項：**&#x200B;使用這些選項將必要的影像和文字圖層新增至畫布。

* ![](/help/assets/assets/dm-templates/add-image.svg)：按一下以將影像新增至畫布。
* ![](/help/assets/assets/dm-templates/add-text.svg)：按一下以新增文字至畫布。
* ![](/help/assets/assets/dm-templates/show-layers-list.svg)：按一下以檢視畫布上的所有圖層（影像和文字）清單。 加入畫布的每個影像和文字都會以個別的圖層表示。

**左窗格上的功能表選項：**&#x200B;請將這些選項用於一般編輯器動作，如下所述。

* ![](/help/assets/assets/dm-templates/layer-selector.svg)：選取圖層。
* ![](/help/assets/assets/dm-templates/bring-forward.svg)：按一下以將選取的圖層往前移，或按&#x200B;**Ctrl** + **]** (Windows)或&#x200B;**Cmd** + **]** (Mac)。
* ![](/help/assets/assets/dm-templates/send-backward.svg)：按一下以向後傳送選取的圖層，或按&#x200B;**Ctrl** + **[** (Windows)或&#x200B;**Cmd** + **[** (Mac)。
* ![](/help/assets/assets/dm-templates/undo.svg)：按一下以復原上一個動作，或按&#x200B;**Ctrl** + **Z** (Windows)或&#x200B;**Cmd** + **Z** (Mac)。
* ![](/help/assets/assets/dm-templates/redo.svg)：按一下以重做最後一個動作，或按&#x200B;**Ctrl** + **Y** (Windows)或&#x200B;**Cmd** + **Y** (Mac)。
* ![](/help/assets/assets/dm-templates/zoomin.svg)：按一下以放大畫布，或按&#x200B;**Ctrl** + **+** (Windows)或Cmd + **+** (Mac)。
* ![](/help/assets/assets/dm-templates/zoomout.svg)：按一下以縮小畫布或按&#x200B;**Ctrl** + **-** (Windows)或&#x200B;**Cmd** + **-** (Mac)。
* 如果沒有編輯文字或屬性，請按&#x200B;**退格鍵**&#x200B;或&#x200B;**刪除**&#x200B;刪除選取的圖層。

在畫布圖層上按一下![](/help/assets/assets/dm-templates/show-layers-list.svg) **>其他**&#x200B;個選項(![](/help/assets/assets/dm-templates/three-dots.svg))，即可在建立範本時隨時編輯畫布維度。
![](/help/assets/assets/dm-templates/edit-canvas1.png)

>[!NOTE]
>
> 範本最多允許20個圖層，包括「畫布」。

### 將影像新增至畫布{#add-images-to-the-canvas}

執行以下步驟，將影像新增至畫布：

1. 按一下![](/help/assets/assets/dm-templates/add-image.svg)以顯示[資產選擇器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)面板。 面板會顯示AEM Assets執行個體中同步至Dynamic Media的影像。
1. 瀏覽面板或使用搜尋列中的關鍵字來尋找特定影像。
1. 將影像拖放到畫布上以使用。 請參閱[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)，以調整畫布上的圖層大小或重新定點陣圖層。
   ![](/help/assets/assets/dm-templates/add-image-to-canvas.png)

### 新增文字圖層至畫布{#add-text-to-the-canvas}

執行以下步驟，將文字圖層新增至畫布：

1. 按一下![](/help/assets/assets/dm-templates/add-text.svg)將文字圖層新增至畫布並開啟「屬性」面板。
1. 選取圖層並按一下文字進行更新。
1. 啟用「屬性」面板中的&#x200B;**[!UICONTROL 智慧型文字調整大小]**，自動調整文字長度和字型大小，以最佳方式符合指定的區域。
   ![](/help/assets/assets/dm-templates/add-text-layer.png)

請參閱[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)來重新定位、調整大小、旋轉或刪除圖層。 在面板的&#x200B;**[!UICONTROL 文字]**&#x200B;區段下的個別欄位中變更文字的值，將文字格式設定為您所需的字型、大小、顏色、樣式、對齊方式（在圖層中）。

>[!NOTE]
>
> 若要使用預設AdobeSans F2字型系列以外的字型，您必須上傳字型檔案並發佈至AEM Assets和Dynamic Media。 如果您的執行個體中有一些舊字型，請確定[重新處理](/help/assets/reprocessing-assets-view.md)以在範本編輯器中檢視這些字型。

### 編輯或刪除圖層 {#edit-or-delete-a-layer}

執行以下步驟來編輯或刪除畫布圖層：

1. 按一下「![](/help/assets/assets/dm-templates/show-layers-list.svg)」，然後在畫布上或從「圖層」清單中選取圖層。
1. 按一下&#x200B;**更多選項** (![](/help/assets/assets/dm-templates/three-dots.svg))以編輯或刪除圖層。
1. 按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除圖層。
1. 按一下「**[!UICONTROL 編輯]**」以使用「[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)」編輯圖層。
   ![](/help/assets/assets/dm-templates/edit-delete-layer.png)

### 屬性面板{#properties-panel}

若要瀏覽至圖層的屬性面板，請執行下列動作：

1. 按一下「![](/help/assets/assets/dm-templates/show-layers-list.svg)」。
1. 從清單中選取圖層。

此面板會顯示圖層中心點在畫布平面上的位置（X和Y值）、圖層的尺寸（寬度和高度）以及文字格式選項。

![](/help/assets/assets/dm-templates/properties-panel.png)

從圖層的屬性面板中，選取畫布上的另一個圖層以導覽至其屬性面板。


#### 重新定位、調整大小、旋轉或刪除圖層{#reposition-resize-delete-a-layer}

請參閱這些常見的圖層編輯動作，以編輯文字或影像圖層：

* **重新定點陣圖層：**&#x200B;拖曳圖層以將它移動到畫布上的任何位置。 此動作會更新屬性面板中的X和Y值。
* **調整圖層大小：**&#x200B;選取圖層並拖曳其邊緣控點以調整其大小。 此動作會更新屬性面板中的W （寬度）和H （高度）值。
* **旋轉圖層：**&#x200B;拖曳垂直放置在圖層上方的方形控點，使其繞其中心旋轉。 這個動作會更新屬性面板中的角度值。
* **刪除圖層：**&#x200B;按&#x200B;**退格鍵**&#x200B;或&#x200B;**刪除**，然後按一下&#x200B;**[!UICONTROL 確認]**&#x200B;刪除選取的圖層。

#### 文字格式選項{#text-formatting-options-on-properties-panel}

在面板的&#x200B;**[!UICONTROL 文字]**&#x200B;區段下的個別欄位中變更文字的值，將文字格式設定為您所需的字型、大小、顏色、樣式、對齊方式（在圖層中）。

**[!UICONTROL 智慧型文字調整大小]**&#x200B;請確定包含&#x200B;**[!UICONTROL 智慧型文字調整大小]** ([Copyfitting](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting))以最佳方式調整字型大小和長度，讓任何文字元合指定區域。 此功能可防止文字溢位，或將文字底部的額外空格縮到最少。
![](/help/assets/assets/dm-templates/smart-text-resize.png)

### 引數化圖層 {#parameterise-a-layer}

建立包含多圖層影像和文字的範本後，將選取的圖層引數化。 將圖層或其屬性引數化後，它會取得索引鍵/值組（也稱為引數）。 此引數可包含在範本URL中，以即時更新圖層的位置、大小或內容，從而即時自訂範本。

欲引數化圖層：

1. 按一下![](/help/assets/assets/dm-templates/show-layers-list.svg)，選取圖層並按一下&#x200B;**[!UICONTROL 引數]**。 **[!UICONTROL 引數]**&#x200B;面板隨即顯示。
1. 切換&#x200B;**[!UICONTROL 包含引數]**&#x200B;以引數化屬性。 請參閱[這個](#parameterisation-options-or-allowed-parameters)以瞭解引數化後的屬性行為。
1. **選擇性：**&#x200B;重新命名引數名稱。 引數名稱具有圖層名稱及尾碼。 對於選取的圖層，其所有引數化屬性會共用相同的圖層名稱，後面跟著不同的尾碼。 依照語意命名慣例重新命名圖層名稱，這樣當您在URL中包含引數時，引數名稱就會自行說明圖層的內容或其用途。
1. 按一下「**[!UICONTROL 儲存]**」。
   ![](/help/assets/assets/dm-templates/parameterise-a-layer.png)
若要在影像和文字圖層的「引數」面板之間切換，請選取畫布上的圖層，然後按一下**[!UICONTROL 引數]**。

#### 引數面板選項 {#parameterisation-options-or-allowed-parameters}

引數化的屬性可作為URL引數包含在範本URL中，以使用URL即時編輯範本。

**影像引數：**

**X：**包含以變更URL中的引數值，沿著圖層的中心線水準移動圖層，平行於範本平面的X軸。
**Y：** Include可透過變更URL中的引數值，沿著圖層的中心線垂直移動圖層，平行於範本平面的Y軸。
**寬度：**包含以變更URL中的引數值來調整圖層的寬度。
**高度：**包含以變更URL中的引數值來調整圖層高度。
**隱藏：**使用0 （顯示）和1 （隱藏）來隱藏或顯示範本中的圖層。
**Source：**&#x200B;包含以變更URL中引數值的影像路徑，用新影像取代圖層的影像。

**文字格式設定引數：**

納入以下引數，藉由更新URL中的引數值，從URL編輯文字、其字型、顏色和大小。

**文字：**包含以從URL更新文字。
**字型系列：**包含以從URL更新文字的字型。
**字型大小：**包含以從URL更新文字的字型大小。
**文字色彩：**&#x200B;包含以從URL更新文字的字型色彩。

### 群組圖層以同時控制其可見性{#group-layers}

另一種保持範本靈活性的方式是使用單一引數名稱來控制多個圖層。 此策略有助於顯示可見性（隱藏或顯示圖層）引數，以更新單一範本的設計或圖形。

請依照下列步驟，為多個圖層的隱藏引數(![](/help/assets/assets/dm-templates/Visibility-icon.svg))指定相同的名稱，讓您同時隱藏或顯示它們。

1. 導覽至圖層的[**[!UICONTROL 屬性面板]**](#parameterise-a-layer)。
1. 若之前未設定引數，請切換&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數。
1. **選擇性：**&#x200B;重新命名Hide引數。
1. 複製隱藏引數名稱。
1. 從畫布中選取其他圖層的「引數」面板，然後切換其&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數（如果未設定引數），即可移至這些圖層。
1. 以複製名稱取代其&#x200B;**[!UICONTROL 隱藏引數]**&#x200B;名稱。
1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;將圖層分組。
1. 在[**[!UICONTROL 預覽和Publish]**](#preview-and-publish-template-and-copy-template-deliver-url)區段中執行步驟3然後執行步驟4，以檢視您的變更。

## 預覽並發佈範本以複製傳遞URL{#preview-and-publish-template-and-copy-template-deliver-url}

執行以下步驟來預覽和發佈範本，並複製傳送URL：

1. 在畫布頁面上，按一下&#x200B;**[!UICONTROL 預覽]**。 您也可以瀏覽至&#x200B;**[!UICONTROL Assets檢視]** **>** **[!UICONTROL Dynamic Media Assets]** **>**&#x200B;尋找並選取您的範本&#x200B;**>**&#x200B;按一下&#x200B;**[!UICONTROL 編輯範本]** **>**&#x200B;按一下&#x200B;**[!UICONTROL 預覽]**。 預覽頁面會顯示範本、其引數（引數化的圖層和屬性）、發佈狀態以及&#x200B;**[!UICONTROL Publish]**&#x200B;選項。
1. 從&#x200B;**[!UICONTROL 範本引數]**&#x200B;面板中選取引數，以編輯其值，並立即更新預覽中對應範本圖層的內容、大小、位置或文字格式。 例如：
   1. 選取文字圖層並編輯其文字，或
   1. 選取影像層，按一下![](/help/assets/assets/dm-templates/add-image.svg)，從資產選擇器選取影像，然後按一下&#x200B;**[!UICONTROL 重新整理]**。

   範本會立即更新，顯示編輯過的文字，並將先前的影像取代為新影像。 此外，影像引數值會反映新的影像路徑。 同樣地，您可以調整圖層的值來調整其大小，變更會即時套用至範本。
1. 從清單中選取[群組圖層](#group-layers)的隱藏引數，以便在範本中顯示或隱藏它們。
1. **選擇性：**&#x200B;將&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數值變更為0到1，然後按一下&#x200B;**[!UICONTROL 重新整理]**&#x200B;檢視變更。 具有相同隱藏引數的圖層會一起隱藏或顯示。 同樣地，您可以從URL控制圖層的可見度。

   ![](/help/assets/assets/dm-templates-publish-status.png)
您也可以切換**[!UICONTROL 包含所有引數]**以編輯所有顯示的引數值，並在範本預覽中檢視更新。
   <br>
1. 若要在預覽頁面上發佈範本，請按一下&#x200B;**[!UICONTROL Publish]**&#x200B;並確認發佈。 Publish完成訊息隨即顯示，且發佈狀態會更新為「已發佈」。

>[!NOTE]
>
>發佈範本需要先發佈範本影像。

### 複製傳遞URL

在&#x200B;**[!UICONTROL 預覽]**&#x200B;頁面上選取的引數會成為範本URL中的URL引數。

若要複製預覽中顯示的已發佈範本的URL：

1. 按一下&#x200B;**[!UICONTROL 複製URL]**。 **[!UICONTROL 複製URL]**&#x200B;對話方塊隨即顯示。 選取並複製顯示的URL。 請注意，URL中的第一個引數在問號&#x200B;**(？)之後開始**&#x200B;和索引鍵值配對的開頭為&#x200B;**$**，結尾為&#x200B;**&amp;**。 金鑰和值由等號&#x200B;**(=)**&#x200B;分隔，金鑰在左側，值在右側。
1. 將此URL貼到瀏覽器標籤中，即可檢視您的即時範本。 直接在URL中更新所需引數的值（索引鍵值），即時自訂範本，如&#x200B;**預覽和Publish**&#x200B;區段的[步驟2](#preview-and-publish-template-and-copy-template-deliver-url)所示。
1. 使用此URL來快速銷售您的產品或服務。 您可以與客戶共用此URL，或將其整合至您的網站或任何下游第三方應用程式，以顯示橫幅並即時更新以反映持續優惠。

瞭解如何在本影片中逐步建立Dynamic Media範本。
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## 從URL即時更新範本{#update-the-template-from-the-url}

直接在URL中編輯引數可能會很繁瑣。 若要簡化：

1. 複製URL並貼到記事本中。
1. 使用Cmd+F (Mac)或Ctrl+F (Windows)來尋找及編輯引數值。 例如：
   * 取代影像圖層的影像路徑。
   * 調整圖層尺寸與位置（如果[引數化](#parameterise-a-layer)）。
   * 編輯文字圖層的文字、字型、顏色、大小或對齊方式。
   * 在0和1之間變更可見度值。

將此更新的URL貼到瀏覽器中以檢視變更。

## 編輯範本{#edit-the-template}

請依照下列步驟編輯範本：

1. 在Assets檢視中，按一下&#x200B;**[!UICONTROL Dynamic Media Assets]**。
2. 導覽至範本位置。
3. 選取範本。
4. 按一下&#x200B;**[!UICONTROL 編輯範本]**。 範本畫布會在「圖層」面板中顯示範本及其所有圖層的清單。 根據您的需求開始編輯範本。

## 需要注意的重要事項 {#important-points-to-note}

* 在使用引數化影像圖層建立範本以進行動態更新後，請確保打算用於未來更新的影像共用與引數化影像相同的尺寸。 這可確保影像完全符合圖層內，不會溢滿或留下空白空間。 目前，範本不支援自動調整尺寸以讓影像符合圖層。
* 文字圖層不支援子字串。 使用者無法在文字圖層的子字串上套用不同的字型屬性。
* Dynamic Media範本目前不支援多家Dynamic Media公司。
* 若是複製或移動，Destination Selector會顯示所有資料夾(包括非Dynamic Media同步資料夾)。 此外，目前也不會顯示Dynamic Media範本資產（兩者皆為目的地選擇器的限制）。
* Assets區段對資料夾所做的任何更新操作(例如，Publish或刪除)都會影響該資料夾中可用的Dynamic Media範本。
* 垃圾桶無法用於Dynamic Media範本。 如果資產移至垃圾桶後還原，資產會在AEM中還原，但不會在Dynamic Media上還原。 同樣的情況對Dynamic Media範本有效。

## 另請參閱

1. 探索[Dynamic Media及其功能](/help/assets/dynamic-media/dynamic-media.md)
1. 探索[具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)
