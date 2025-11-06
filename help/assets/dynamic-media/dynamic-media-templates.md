---
title: 如何管理 [!DNL Dynamic Media] 範本？
description: 瞭解如何使用WYSIWYG範本編輯器建立 [!DNL Dynamic Media] 範本，並包含多個影像、文字和形狀圖層，以快速建立橫幅和傳單，並將其用於下游應用程式。
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3780'
ht-degree: 1%

---


# [!DNL Dynamic Media]個範本{#dynamic-media-templates}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

使用[!DNL Dynamic Media]範本(WYSIWYG範本編輯器)，為您的橫幅和傳單建立即時可自訂的範本。 發佈您的[!DNL Dynamic Media]範本並在下游應用程式中使用。 [!DNL Dynamic Media]範本包含影像和文字圖層。 新增引數至範本的影像和文字圖層，並使用[[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media)來重新定位和調整圖層大小，並即時更新其內容。

部分主要功能包括：

* **[!DNL Dynamic Media]WYSIWYG範本編輯器：**&#x200B;建立可自訂的橫幅（包含影像與文字圖層）。
* **圖層引數化：**&#x200B;定義圖層的動態索引鍵值配對，以啟用即時更新。
* **[!DNL Dynamic Media]URL支援：**&#x200B;使用[!DNL Dynamic Media] URL作為範本，整合來自第一方或第三方應用程式的個人化值。
* **圖層可見性控制：**&#x200B;視需要動態隱藏或顯示圖層。
* **智慧型文字調整大小：**&#x200B;自動調整文字大小以符合指定的區域。

[!DNL Dynamic Media]範本的一些主要優點包括：

* **最佳化1:1 Personalization：**&#x200B;根據即時客戶訊號量身打造內容。
* **減少手動工作：**&#x200B;自動化並加速內容建立和管理。
* **確保一致的全通路體驗：**&#x200B;保持通路間的品牌一致性。
* **有效地重複使用內容：**&#x200B;避免單一使用內容，並透過動態引數化範本進行縮放。
* **降低風險：**&#x200B;即時更新定價、折扣和連結。
* **增強客戶參與度：**&#x200B;推動互動式、情境相關的體驗。

>[!NOTE]
>
>訂閱Enhanced Security SKU的客戶無法在該雲端服務方案上使用任何[!DNL Dynamic Media]功能，包括[!DNL Dynamic Media]範本。

瞭解如何在此影片中逐步建立[!DNL Dynamic Media]範本。

>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## 開始之前{#prerequisites-for-dynamic-media-wysiwyg-template}

滿足下列要求以建立[!DNL Dynamic Media]範本並產生其傳遞URL：

1. 存取[!DNL Dynamic Media]。
1. 在[!DNL Assets View]首頁上，**[!UICONTROL Dynamic Media Assets]**&#x200B;中有資料夾可儲存您的範本。 [在](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view)Assets![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL 中建立資料夾&#x200B;]**，以在&#x200B;**[!UICONTROL &#x200B; Dynamic Media Assets &#x200B;]**&#x200B;中復寫該資料夾。
1. [將您 [!DNL AEM Assets] 執行個體中可用的影像與 [!DNL Dynamic Media] 同步，以便使用這些影像來建立範本](/help/assets/dynamic-media/config-dm.md)。
1. 發佈要在建立範本時使用的影像，以在建立範本後產生範本的傳遞URL。 傳遞URL可用於下游應用程式。
1. 若要在範本的文字圖層中使用預設[!UICONTROL Adobe Sans F2]字型以外的字型，請[同時上傳字型檔案並發佈至AEM和Dynamic Media &#x200B;](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation)。 [支援的字型檔案格式為：AFM、OTF、PFB、PFM、PhotoFont、TTC、TTF](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats)。 此外，請確定[重新處理](/help/assets/reprocessing-assets-view.md)現有的字型以使用這些字型。 如需詳細資訊，請參閱[字型](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/support-files/fonts)。<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. 在觸控式UI中驗證下列專案：
   * 在&#x200B;**[!UICONTROL 編輯[!DNL Dynamic Media]設定頁面]**&#x200B;上，預設設定為&#x200B;**[!UICONTROL [!DNL Dynamic Media]已停用]**&#x200B;的&#x200B;**[!UICONTROL 同步處理模式]**&#x200B;未套用至所有AEM資料夾（**[!UICONTROL 同步處理所有內容]**&#x200B;已取消核取）。 如需詳細資訊，請參閱[設定Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md)。
   * 目的地資料夾或子資料夾的&#x200B;**[!UICONTROL [!DNL Dynamic Media]同步模式]**&#x200B;設定為&#x200B;**[!UICONTROL 啟用子資料夾]**，您會在建立後儲存範本。 如需詳細資訊，請參閱[設定 [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md)。

## 建立[!DNL Dynamic Media]範本{#how-to-create-dynamic-media-template}

執行以下步驟來建立[!DNL Dynamic Media]範本：

<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->

1. [建立空白畫布](#create-a-canvas)
1. [將影像新增至畫布](#add-images-to-the-canvas)
1. [新增文字圖層至畫布](#add-text-to-the-canvas)
1. [將圖案新增至畫布](#add-shapes-to-the-canvas)
1. [編輯或刪除圖層](#edit-or-delete-a-layer)
1. [引數化圖層](#parameterise-a-layer)

### 建立空白畫布{#create-a-canvas}

執行以下步驟來建立空白畫布：

1. 導覽至[!DNL Assets View]，選取左側面板中可用的&#x200B;**[!UICONTROL Dynamic Media Assets]**，然後導覽至您的資料夾，將範本儲存在該資料夾中。

   ![Dynamic Media 範本](/help/assets/assets/DM-Assets1.png)

1. 選取&#x200B;**[!UICONTROL 建立範本]**。 **[!UICONTROL 新範本]**&#x200B;對話方塊隨即顯示。

   ![如何建立可即時自訂的動態範本](/help/assets/assets/new-template.png)

   >[!NOTE]
   >
   >  範本會儲存在您建立它的位置。 在[!DNL Assets View]首頁上，選取&#x200B;**[!UICONTROL Dynamic Media Assets]**，然後按一下&#x200B;**[!UICONTROL 建立範本]**，將範本儲存在&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;根資料夾中。

1. 指定範本名稱、定義畫布寬度和高度，然後按一下[建立]。**&#x200B;** 空白畫布顯示，兩側都有選單選項以用於建立範本。 將游標停留在選單選項上可檢視其工具提示。
   ![即時可自訂的範本](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > 允許的寬度和高度範圍是從50到5000。

**右窗格上的功能表選項：**&#x200B;使用這些選項將必要的影像和文字圖層新增至畫布。

* ![DM範本](/help/assets/assets/add-image.svg)：按一下以將影像新增至畫布。
* ![可自訂的範本](/help/assets/assets/add-text.svg)：按一下以將文字新增至畫布。
* ![可自訂的範本](/help/assets/assets/show-layers-list.svg)：按一下以檢視畫布上的所有圖層（影像和文字）清單。 加入畫布的每個影像和文字都會以個別的圖層表示。

**左窗格上的功能表選項：**&#x200B;請將這些選項用於下列一般編輯器動作。

* ![DM範本](/help/assets/assets/layer-selector.svg)：選取![DM範本](/help/assets/assets/layer-selector.svg)，然後按一下畫布上的圖層來加以選取。
* ![支援自訂的範本](/help/assets/assets/bring-forward.svg)：按一下支援自訂的![範本](/help/assets/assets/bring-forward.svg)，或使用鍵盤快速鍵、**Ctrl** + **`]`** (Windows)或&#x200B;**Cmd** + **`]`** (Mac)，將選取的圖層往前移。
* ![如何建立可輕鬆自訂的範本](/help/assets/assets/send-backward.svg)：按一下![如何建立可輕鬆自訂的範本](/help/assets/assets/send-backward.svg)，或使用鍵盤快速鍵、**Ctrl** + **`[`** (Windows)或&#x200B;**Cmd** + **`[`** (Mac)以向後傳送選取的圖層。
* ![建立可立即自訂的範本](/help/assets/assets/undo.svg)：按一下![建立可立即自訂的範本](/help/assets/assets/undo.svg)或使用鍵盤快速鍵、**Ctrl** + **Z** (Windows)或&#x200B;**Cmd** + **Z** (Mac)以復原上一個動作。
* ![可快速建立橫幅的範本](/help/assets/assets/redo.svg)：按一下![範本可快速建立橫幅](/help/assets/assets/redo.svg)，或使用鍵盤快速鍵，**Ctrl** + **Y** (Windows)或&#x200B;**Cmd** + **Y** (Mac)可重做上一個動作。
* ![快速建立傳單的範本](/help/assets/assets/zoom-in.svg)：按一下![範本快速建立傳單](/help/assets/assets/zoom-in.svg)，或使用鍵盤快速鍵，**Ctrl** + **+** (Windows)或&#x200B;**Cmd** + **+** (Mac)放大畫布。
* ![快速建立橫幅的範本](/help/assets/assets/Zoom-out.svg)：按一下![範本快速建立橫幅](/help/assets/assets/Zoom-out.svg)或使用鍵盤快速鍵、**Ctrl** + **-** (Windows)或&#x200B;**Cmd** + **-** (Mac)以縮小畫布。
* 如果沒有編輯文字或屬性，請按&#x200B;**退格鍵**&#x200B;或&#x200B;**刪除**&#x200B;刪除選取的圖層。

按一下![範本以快速建立傳單](/help/assets/assets/show-layers-list.svg)，並在畫布圖層上選取更多選項(![](/help/assets/assets/three-dots.svg))，以在建立範本時隨時編輯畫布維度。
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> 範本最多允許20個圖層，包括「畫布」。

### 將影像新增至畫布{#add-images-to-the-canvas}

執行以下步驟，將影像新增至畫布：

1. 按一下![立即建立橫幅](/help/assets/assets/add-image.svg)以開啟[資產選擇器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)面板。 面板會顯示您的AEM Assets執行個體中同步至[!DNL Dynamic Media]的影像。
1. 瀏覽面板或使用搜尋列中的關鍵字來尋找特定影像。
1. 將影像拖放到畫布上以使用。 請參閱[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)，以調整畫布上的圖層大小或重新定點陣圖層。
   ![在秒內建立橫幅](/help/assets/assets/add-image-to-canvas.png)
1. 啟用&#x200B;**[!UICONTROL 統一半徑]**&#x200B;切換功能，並使用&#x200B;**[!UICONTROL 圓角半徑]**&#x200B;滑桿來統一調整影像四個角落的圓度。 停用切換功能，藉由指定每個轉角的特定半徑值來自訂轉角圓度。
   ![調整影像的圓角度](/help/assets/assets/enable-uniform-radius-image.png)

### 新增文字圖層至畫布{#add-text-to-the-canvas}

執行以下步驟，將文字圖層新增至畫布：

1. 按一下![建立新橫幅fastly](/help/assets/assets/add-text.svg)以新增文字圖層到畫布並開啟[內容]面板。
1. 選取圖層並按一下文字進行更新。
1. 在「屬性」面板中選取「**[!UICONTROL 智慧型文字調整大小]**」，自動調整文字長度和字型大小，以最佳方式配合指定的區域。
   ![最佳自訂橫幅](/help/assets/assets/add-text-layer.png)

請參閱[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)來重新定位、調整大小、旋轉或刪除圖層。 在面板的&#x200B;**[!UICONTROL 文字]**&#x200B;區段下的個別欄位中變更文字的值，將文字格式設定為所需的字型、大小、顏色、樣式、對齊方式（在圖層中）。 **[!UICONTROL 字型系列]**&#x200B;欄位會顯示[!UICONTROL Adobe Sans F2]預設字型、重新處理的現有字型，以及新上傳和發佈的字型。 如需詳細資訊，請參閱上文[開始之前](#prerequisites-for-dynamic-media-wysiwyg-template)一節中的要點5。

[格式化文字的特定部分](#apply-formatting-to-substring)和[將其引數化，以獨立控制它們](#substring-parameterisation)。

#### 格式化選擇性文字{#apply-formatting-to-substring}

執行以下步驟來格式化字串的特定部分：

1. 在字串中選取一個或多個要格式化的字元。
1. 使用[屬性面板](#properties-panel)格式化選取範圍。 下列格式選項適用於子字串及其部分：
   * **字型樣式**：使用&#x200B;**[!UICONTROL 字型樣式]**&#x200B;選項的粗體、斜體、底線、下標和上標。
   * **字型屬性**：使用個別面板選項變更字型系列、顏色和大小。
     ![format-substring](/help/assets/assets/format-substring.png)

[每個格式化的字串部分都會顯示為子字串選取器（可在引數面板中使用）中的子字串。 將引數新增至這些格式化部分，以使用範本的傳遞URL](#substring-parameterisation)動態格式化它們。

### 將圖案新增至畫布 {#add-shapes-to-the-canvas}

執行以下步驟來將圖案新增至畫布：

1. 按一下![建立形狀](/help/assets/assets/Shapes.svg)，選取形狀（矩形或圓形）以將其加入畫布。 使用圖案的[[!UICONTROL 屬性面板]](#reposition-resize-delete-a-layer)來重新定位、調整大小、旋轉或刪除圖層。
1. 捲動至面板的&#x200B;**[!UICONTROL 樣式]**&#x200B;區段，在&#x200B;**[!UICONTROL 圖案色彩]**&#x200B;欄位中定義十六進位程式碼，或使用檢色器填入選取圖案的色彩。
1. 啟用&#x200B;**[!UICONTROL 統一半徑]**&#x200B;切換功能，並使用&#x200B;**[!UICONTROL 圓角半徑]**&#x200B;滑桿來統一調整矩形四個角落的圓度。 停用切換功能，藉由指定每個轉角的特定半徑值來自訂轉角圓度。
   ![調整形狀的圓角度](/help/assets/assets/enable-uniform-radius-shape.png)
1. [將&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數新增至選取的圖層](#parameterise-a-layer)，以使用範本URL即時顯示或隱藏範本中的圖層。
1. 選取圖層以[新增[!UICONTROL CTA]連結](#add-CTA-in-dynamic-media-templates)，讓使用者在即時範本中按一下形狀做為超連結。

### 編輯或刪除圖層 {#edit-or-delete-a-layer}

執行以下步驟來編輯或刪除畫布圖層：

1. 按一下支援動態更新的![範本](/help/assets/assets/show-layers-list.svg)，然後在畫布上或從「圖層」清單中選取圖層。
1. 按一下&#x200B;**[!UICONTROL 更多選項]** （![支援即時更新的範本](/help/assets/assets/three-dots.svg)）以編輯或刪除圖層。
1. 按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除圖層。
1. 按一下「**[!UICONTROL 編輯]**」以使用「[**[!UICONTROL 屬性面板]**](#reposition-resize-delete-a-layer)」編輯圖層。
   ![快速橫幅建立](/help/assets/assets/dm-templates/edit-delete-layer.png)

### 屬性面板{#properties-panel}

[!UICONTROL 屬性]面板包含區段以[重新定位](#reposition-resize-delete-a-layer)、[調整大小](#reposition-resize-delete-a-layer)和[旋轉](#reposition-resize-delete-a-layer)圖層。  它也會提供[圖案圖層](#add-shapes-to-the-canvas)的填色選項、[文字圖層](#text-formatting-options-on-properties-panel)的[文字格式選項](#add-text-to-the-canvas)，以及[將[!UICONTROL CTA]連結](#add-CTA-in-dynamic-media-templates)新增至任何選取圖層的選項。
若要瀏覽至圖層的屬性面板，請按一下![快速內容建立](/help/assets/assets/show-layers-list.svg)，然後從清單中選取要顯示其[!UICONTROL 屬性]面板的圖層。

![快速內容建立](/help/assets/assets/properties-panel.png)

從圖層的[!UICONTROL 屬性]面板中，選取畫布上的另一個圖層以瀏覽至其[!UICONTROL 屬性]面板。

#### 重新定位、調整大小、旋轉或刪除圖層{#reposition-resize-delete-a-layer}

請參閱這些常見的圖層編輯動作，以編輯文字或影像圖層：

* **重新定點陣圖層：**&#x200B;拖曳圖層以將它移動到畫布上的任何位置。 此動作會更新屬性面板中的X和Y值。 X和Y是畫布平面上圖層中心的座標。
* **調整圖層大小：**&#x200B;選取圖層並拖曳其邊緣控點以調整其大小。 此動作會更新屬性面板中的W （寬度）和H （高度）值。
* **旋轉圖層：**&#x200B;拖曳垂直放置在圖層上方的方形控點，使其繞其中心旋轉。 這個動作會更新屬性面板中的角度值。
* **刪除圖層：**&#x200B;按&#x200B;**退格鍵**&#x200B;或&#x200B;**刪除**，然後按一下&#x200B;**[!UICONTROL 確認]**&#x200B;刪除選取的圖層。

#### 文字格式選項{#text-formatting-options-on-properties-panel}

將文字的格式設定為所需的字型、大小、顏色、樣式、對齊方式（在圖層內），方法是在面板的&#x200B;**[!UICONTROL 文字]**&#x200B;區段下的個別欄位中變更其值。
確定包括&#x200B;**[!UICONTROL 智慧文字調整大小]**。 [!UICONTROL 智慧型文字調整大小]適用於[Copyfitting](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting)演演算法，可在文字區域中以最佳方式填入文字，防止文字溢位，並儘量減少文字底部的額外空間。

![立即建立內容](/help/assets/assets/smart-text-resize.png)

### 引數化圖層 {#parameterise-a-layer}

建立包含多個影像、文字和形狀圖層的範本後，請引數化選取的圖層。 將圖層或其屬性引數化後，它會取得索引鍵/值組（也稱為引數）。 此引數可包含在範本URL中，以即時更新圖層的位置、大小或內容，從而即時自訂範本。

欲引數化圖層：

1. 按一下![即時內容建立](/help/assets/assets/show-layers-list.svg)，選取圖層並按一下&#x200B;**[!UICONTROL 引數]**。 **[!UICONTROL 引數]**&#x200B;面板隨即顯示。
1. 切換&#x200B;**[!UICONTROL 包含引數]**&#x200B;以引數化屬性。 請參閱[引數面板選項](#parameterisation-options-or-allowed-parameters)，瞭解引數化後的屬性行為。
1. **選擇性：**&#x200B;重新命名引數名稱。 引數名稱具有圖層名稱及尾碼。 對於選取的圖層，其所有引數化屬性會共用相同的圖層名稱，後面跟著不同的尾碼。 依照語意命名慣例重新命名圖層名稱，這樣當您在URL中包含引數時，引數名稱就會自行說明圖層的內容或其用途。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。
   ![即時內容建立](/help/assets/assets/parameterise-a-layer.png)
若要在影像和文字圖層的「引數」面板之間切換，請選取畫布上的圖層，然後按一下&#x200B;**[!UICONTROL 引數]**。

#### 引數面板選項 {#parameterisation-options-or-allowed-parameters}

引數化的屬性可作為URL引數包含在範本URL中，以使用URL即時編輯範本。

##### 圖層引數{#layer-parameters}

以下是同時套用至影像和文字圖層的圖層引數。

**[!UICONTROL X]：**&#x200B;包含以變更URL中的引數值，沿圖層中心線水準移動圖層，平行於範本平面的X軸。
**[!UICONTROL Y]：**&#x200B;包含以變更URL中的引數值，沿著圖層的中心線垂直移動圖層，平行於範本平面的Y軸。
**[!UICONTROL 寬度]：**&#x200B;包含以變更URL中的引數值來調整圖層的寬度。
**[!UICONTROL 高度]：**&#x200B;包含以變更URL中的引數值來調整圖層高度。
**[!UICONTROL 隱藏]：**&#x200B;包含以使用0 （顯示）和1 （隱藏）來隱藏或顯示範本中的圖層。

##### 影像引數{#image-parameter}

加入&#x200B;**[!UICONTROL Source]**&#x200B;引數，變更URL中引數值的影像路徑，以新影像取代圖層的影像。
![影像來源引數](/help/assets/assets/image-parameter.png)

##### 文字格式設定引數{#text-formatting-parameters}

納入下列引數，藉由更新URL中的引數值，從傳送URL編輯文字、其字型、顏色和大小：

**[!UICONTROL 文字]：**&#x200B;包含以從URL更新文字。
**[!UICONTROL 字型系列]：**&#x200B;包含以從URL更新文字的字型。
**[!UICONTROL 字型大小]：**&#x200B;包含以從URL更新文字的字型大小。
**[!UICONTROL 文字色彩]：**&#x200B;包含以從URL更新文字的字型色彩。

##### 引數化子字串{#substring-parameterisation}

在&#x200B;**[!UICONTROL 引數]**&#x200B;面板中，捲動至&#x200B;**[!UICONTROL 子字串引數]**&#x200B;區段。 此區段包含一個&#x200B;**子字串選取器**，它會將具有一致格式設定的完整字串（選取的文字圖層）或其格式化部分顯示為個別的子字串。 選取子字串以[引數化其文字、字型系列、字型大小及顏色](#text-formatting-parameters)。
使用子字串選擇器[分割子字串](#split-substring)以引數化其個別部分，或[合併子字串](#merge-substring)以套用統一的引數。

###### 分割子字串{#split-substring}

若要將子字串的特定部分引數化，請拉出該部分，使其成為個別選取和引數化的個別子字串。 執行以下步驟，將子字串分割為個別的子字串：

1. 在子字串選取器中，選取子字串內的字元以區隔它。
1. 按一下![分割子字串](/help/assets/assets/unmerge.svg)以提取選取範圍，並在&#x200B;**子字串選取器**&#x200B;中將其設為個別的子字串。
   ![分割子字串](/help/assets/assets/split-a-substring.png)
您可以選取必要的子字串來[引數化其文字、字型系列、字型大小及顏色](#text-formatting-parameters)。

###### 合併子字串{#merge-substring}

合併子字串會移除其現有的個別引數，並可讓您跨新形成的子字串套用一致的引數。
執行以下步驟來合併兩個相鄰的子字串，以將統一的引數套用至產生的子字串：

1. 在子字串選取器中，選取兩個相鄰子字串間具有相同格式的字元。
1. 按一下![合併子字串](/help/assets/assets/merge.svg)以合併子字串。

   ![合併相同的子字串](/help/assets/assets/merge-two-substrings.png)

   您可以將統一的引數套用至新形成的子字串。

   >[!NOTE]
   >
   >只能合併格式相同的子字串。

### 群組圖層以同時控制其可見性{#group-layers}

另一種保持範本靈活性的方式是使用單一引數名稱來控制多個圖層。 此策略有助於顯示可見性（隱藏或顯示圖層）引數，以更新單一範本的設計或圖形。

請依照下列步驟，為多重圖層的[!UICONTROL 隱藏]引數（![快速內容建立](/help/assets/assets/Visibility-icon.svg)）指定相同的名稱，讓您同時隱藏或顯示它們。

1. 導覽至圖層的[**[!UICONTROL 屬性面板]**](#parameterise-a-layer)。
1. 若之前未設定引數，請切換&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數。
1. **選用：**&#x200B;重新命名&#x200B;**[!UICONTROL Hide]**&#x200B;引數。
1. 複製&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數名稱。
1. 從畫布中選取其他圖層的「引數」面板，然後切換其&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數（如果未設定引數），即可移至這些圖層。
1. 以複製名稱取代其&#x200B;**[!UICONTROL 隱藏引數]**&#x200B;名稱。
1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;將圖層分組。
1. 在[**[!UICONTROL 預覽和發佈]**](#preview-and-publish-template-and-copy-template-deliver-url)區段中執行步驟3然後執行步驟4，以檢視您的變更。

## 預覽並發佈範本以複製傳遞URL{#preview-and-publish-template-and-copy-template-deliver-url}

執行以下步驟來預覽和發佈範本，並複製傳送URL：

1. 在畫布頁面上，按一下&#x200B;**[!UICONTROL 預覽]**。 您也可以導覽至&#x200B;**[!UICONTROL Assets檢視]** **>** **[!UICONTROL Dynamic Media Assets]** **>**&#x200B;尋找並選取您的範本&#x200B;**>**&#x200B;按一下&#x200B;**[!UICONTROL 編輯範本]** **>**&#x200B;按一下&#x200B;**[!UICONTROL 預覽]**。 預覽頁面會顯示範本、其引數（引數化的圖層和屬性）、發佈狀態以及&#x200B;**[!UICONTROL 發佈]**&#x200B;選項。
1. 從&#x200B;**[!UICONTROL 範本引數]**&#x200B;面板中選取引數，以編輯其值，並立即更新預覽中對應範本圖層的內容、大小、位置或文字格式。 例如：
   1. 選取文字圖層並編輯其文字，或
   1. 選取影像層，按一下![即時建立內容](/help/assets/assets/add-image.svg)，從資產選取器選取影像，然後按一下&#x200B;**[!UICONTROL 重新整理]**。

   範本會立即更新，顯示編輯過的文字，並將先前的影像取代為新影像。 此外，影像引數值會反映新的影像路徑。 同樣地，您可以調整圖層的值來調整其大小，變更會即時套用至範本。
1. 從清單中選取&#x200B;**[!UICONTROL 群組圖層]**&#x200B;的[隱藏](#group-layers)引數，以便在範本中顯示或隱藏它們。
1. **選擇性：**&#x200B;將&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數值變更為0到1，然後按一下&#x200B;**[!UICONTROL 重新整理]**&#x200B;檢視變更。 具有相同&#x200B;**[!UICONTROL 隱藏]**&#x200B;引數的圖層會隱藏或同時顯示。 同樣地，您可以從URL控制圖層的可見度。

   ![即時建立內容](/help/assets/assets/dm-templates-publish-status.png)
您也可以切換&#x200B;**[!UICONTROL 包含所有引數]**&#x200B;以編輯所有顯示的引數值，並在範本預覽中檢視更新。
   <br>
1. 若要從預覽頁面發佈範本，請按一下&#x200B;**[!UICONTROL 發佈]**&#x200B;並確認發佈。 顯示&#x200B;**[!UICONTROL 發佈完成]**&#x200B;訊息，且發佈狀態更新為&#x200B;**[!UICONTROL 已發佈]**。

### 複製傳遞URL

在&#x200B;**[!UICONTROL 預覽]**&#x200B;頁面上選取的引數會成為範本URL中的URL引數。

確認範本中的影像已發佈至AEM和Dynamic Media，以產生範本的傳遞URL。

執行以下步驟，複製範本的傳遞URL：

1. 按一下&#x200B;**[!UICONTROL 複製URL]**。 **[!UICONTROL 複製URL]**&#x200B;對話方塊隨即顯示。 選取並複製顯示的URL。 URL中的第一個引數在問號&#x200B;**([!UICONTROL ？])**&#x200B;和索引鍵/值組開頭為&#x200B;**[!UICONTROL $]**，結尾為&#x200B;**[!UICONTROL &amp;]**。 金鑰和值以等號分隔&#x200B;**([!UICONTROL =])**，金鑰在左側，值在右側。
1. 將此URL貼到瀏覽器標籤中，即可檢視您的即時範本。 直接在URL中更新所需引數的值（索引鍵值），即時自訂範本，如[預覽和發佈](#preview-and-publish-template-and-copy-template-deliver-url)區段的&#x200B;**步驟2**&#x200B;所示。
1. 使用此URL來快速銷售您的產品或服務。 您可以與客戶共用此URL，或將其整合至您的網站或任何下游第三方應用程式，以顯示橫幅並即時更新以反映持續優惠。

## 從URL即時更新範本{#update-the-template-from-the-url}

直接在URL中編輯引數可能會很繁瑣。 若要簡化：

1. 複製URL並貼到記事本中。
1. 使用Cmd+F (Mac)或Ctrl+F (Windows)來尋找及編輯引數值。 例如：
   * 尋找和取代影像圖層的影像路徑。
   * 尋找圖層的[引數化](#parameterise-a-layer)座標、寬度和高度，以調整其值。
   * 編輯文字圖層的文字、字型、顏色、大小或對齊方式。
   * 在0和1之間變更可見度值。

將此更新的URL貼到瀏覽器中以檢視變更。

## 編輯範本{#edit-the-template}

請依照下列步驟編輯範本：

1. 在[!DNL Assets view]上，按一下&#x200B;**[!UICONTROL Dynamic Media Assets]**。
2. 導覽至範本位置。
3. 選取範本。
4. 按一下&#x200B;**[!UICONTROL 編輯範本]**。 範本畫布會在「圖層」面板中顯示範本及其所有圖層的清單。 根據您的需求開始編輯範本。

## 將Call to action (CTA)連結新增至範本層{#add-CTA-in-dynamic-media-templates}

將[!DNL Dynamic Media]範本的任何影像、文字或形狀圖層轉換為超連結，方法是新增指向該範本的CTA連結，將使用者導向目標頁面。

執行以下步驟，將CTA連結新增至圖層：

1. 導覽至您的範本位置，選取範本並按一下![編輯](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL 編輯範本]**。 範本會顯示在畫布上。
1. 選取範本圖層並[導覽至其屬性面板](#edit-or-delete-a-layer)以新增CTA連結至該圖層。
1. 在屬性面板上，選取&#x200B;**[!UICONTROL 新增CTA]**，在&#x200B;**[!UICONTROL URL]**&#x200B;欄位中指定目的地URL，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   ![新增CTA](/help/assets/assets/add-cta.png)

1. 按一下[預覽]&#x200B;**&#x200B;**&#x200B;並選取[發佈]&#x200B;**&#x200B;**&#x200B;以發佈您的範本（若未更早發佈）。
1. 導覽至儲存此範本的資料夾，選取此範本並按一下![詳細資料頁面](/help/assets/assets/details-page-icon.svg) **[!UICONTROL 詳細資料]**。
1. 按一下&#x200B;**[!UICONTROL 複製選項]**&#x200B;並選取&#x200B;**[!UICONTROL 複製內嵌程式碼]**。 請確定將範本影像發佈至[!DNL AEM and Dynamic Media]以複製內嵌程式碼。

   ![複製內嵌程式碼](/help/assets/assets/copy-options1.png)

   以下是內嵌程式碼的範例：

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/tw/products.html" alt="Layer with CTA" title="https://business.adobe.com/tw/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/tw/products.html" alt="Layer with CTA" title="https://business.adobe.com/tw/products.html" target="_blank">
    </map>
    </div>
   ```

1. 將複製的內嵌程式碼新增至網站的HTML檔案，並在瀏覽器中執行以顯示範本。

按一下範本上的CTA元素，即可導覽至目的地頁面。

觀看此逐步影片，瞭解如何將CTA連結新增至範本圖層。

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## 需要注意的重要事項 {#important-points-to-note}

* 在使用引數化影像圖層建立範本以進行動態更新後，請確保打算用於未來更新的影像共用與引數化影像相同的尺寸。 這可確保影像完全符合圖層內，不會溢滿或留下空白空間。 目前，範本不支援自動調整尺寸以讓影像符合圖層。
* 文字圖層不支援子字串。 使用者無法在文字圖層的子字串上套用不同的字型屬性。
* [!DNL Dynamic Media]範本目前無法支援多個[!DNL Dynamic Media]公司。
* 若是複製或移動，Destination Selector會顯示所有資料夾（包括非[!DNL Dynamic Media]同步資料夾）。 此外，目前也不會顯示[!DNL Dynamic Media]範本資產（兩者皆為目的地選擇器的限制）。
* 從Assets區段對資料夾執行的任何更新操作（例如「發佈」或「刪除」）都會影響該資料夾中可用的[!DNL Dynamic Media]範本。
* 垃圾桶無法用於[!DNL Dynamic Media]範本。 如果資產移至垃圾桶後還原，資產會在AEM中還原，但不會在[!DNL Dynamic Media]上還原。 [!DNL Dynamic Media]範本也是相同的。

## 另請參閱

1. 探索[[!DNL Dynamic Media] 及其功能](/help/assets/dynamic-media/dynamic-media.md)
1. 使用OpenAPI功能探索[[!DNL Dynamic Media] &#x200B;](/help/assets/dynamic-media-open-apis-overview.md)