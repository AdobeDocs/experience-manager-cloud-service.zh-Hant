---
title: 新增動態媒體資產至頁面
description: 如何將Dynamic Media元件新增至Adobe Experience Manager中的頁面，做為雲端服務。
translation-type: tm+mt
source-git-commit: c3ada59105cad7c2fc3b36b032d045b91f86b495
workflow-type: tm+mt
source-wordcount: '3135'
ht-degree: 8%

---


# 新增動態媒體資產至頁面{#adding-dynamic-media-assets-to-pages}

若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360全景媒體元件。若要這麼做，請進入「版面」模式並啟用「動態媒體」元件。然後，您可以將這些元件新增至頁面，並新增資產至元件。動態媒體元件是智慧型的——他們知道您是新增影像還是視訊，而可用的設定選項也會隨之變更。

如果您使用Experience Manager做為WCM，則直接將Dynamic Media資產新增至頁面。 如果您使用協力廠商來處理WCM，請連結 [或](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)[內嵌資](/help/assets/dynamic-media/embed-code.md) 產。如需多方互動網站，請參閱將最佳化 [的影像傳送至多方互動網站](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>您必須先發佈資產，才能將資產新增至Experience Manager中的頁面。 請參閱[發佈動態媒體資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 新增動態媒體元件至頁面{#adding-a-dynamic-media-component-to-a-page}

將3D媒體、動態媒體、互動式媒體、全景媒體、智慧型裁切視訊或視訊360媒體元件新增至頁面，與將元件新增至任何頁面相同。 以下各節將介紹動態媒體元件。

**新增動態媒體元件至頁面**

1. 在Experience Manager中，開啟您要新增動態媒體元件的頁面。
1. 在左窗格中，點選&#x200B;**[!UICONTROL 元件]**&#x200B;圖示，然後篩選動態媒體。

   如果沒有可用的動態媒體元件清單，您可能需要啟用您要使用的動態媒體元件。 請參閱[啟用動態媒體元件](#enabling-dynamic-media-components)。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. 拖曳&#x200B;**[!UICONTROL 動態媒體]**&#x200B;元件，並將它拖曳至頁面上所需的位置。

1. 將滑鼠指標直接暫留在元件上。 當元件被藍色方塊包圍時，點選一次即可顯示元件的工具列。 點選「**[!UICONTROL Configuration(wrench)]**(設定(wrench)&lt;a1/>)」圖示。

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. 視您拖放至頁面的動態媒體元件而定，會開啟設定對話方塊。 [視需要設定元件](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 的選項。

   以下範例顯示「動態媒體&#x200B;**[!UICONTROL 視訊360媒體]**」元件對話方塊以及「檢視器預設集」下拉式清單中可用的選項。

   ![視訊360媒體元件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   動態媒體視訊360媒體元件。

1. 完成後，在對話框的右上角點選複選標籤以保存更改。

### 啟用動態媒體元件{#enabling-dynamic-media-components}

如果沒有可新增至頁面的動態媒體元件，可能表示您必須先啟用要使用的元件。

1. 在Experience Manager中，開啟您要新增動態媒體元件的頁面。
1. 在工具列的靠近頁面頂端的左側，點選「頁面資訊」圖示，然後從下拉式清單中點選「編輯範本」。****

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. 在工具列右側靠近頁面頂部的下拉式清單中，點選&#x200B;**[!UICONTROL 結構]**。

   ![政策](/help/assets/assets-dm/structure-mode.png)

1. 在頁面底部附近，點選「Layout Container（版面容器）」以開啟其工具列，然後點選「Policy（原則）」圖示。****
1. 在&#x200B;**[!UICONTROL 版面容器]**&#x200B;頁面的&#x200B;**[!UICONTROL 屬性]**&#x200B;標題下，請確定已選取「允許的元件&#x200B;]**」標籤。**[!UICONTROL 

   ![允許的元件](/help/assets/assets-dm/allowed-components.png)

1. 捲動直到您看到&#x200B;**[!UICONTROL 動態媒體]**。
1. 點選&#x200B;**[!UICONTROL 動態媒體]**&#x200B;左側的>圖示以展開清單，選取您要啟用的動態媒體元件。

   ![動態媒體元件清單](/help/assets/assets-dm/dm-components-select.png)

1. 在&#x200B;**[!UICONTROL 版面容器]**&#x200B;頁面的右上角，點選「完成（勾選）」圖示。

1. 在工具列靠近頁面頂端的右側，從下拉式清單中，點選「初始內容」，然後按一下「a2/」，將動態媒體元件新增至頁面。[****](#adding-a-dynamic-media-component-to-a-page)

## 本地化動態媒體元件{#localizing-dynamic-media-components}

您可透過下列兩種方式將Dynamic Media元件當地語系化：

* 在「網站」的網頁中，開啟「屬 **[!UICONTROL 性]** 」並選 **[!UICONTROL 取「進階]** 」標籤。選擇所要的本地化語言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 從網站選取器中，選取所要的頁面或頁面群組。 點選「**[!UICONTROL 屬性]**」並選取「**[!UICONTROL 進階]**」標籤。 選擇所要的本地化語言。

   >[!NOTE]
   >
   >請注意，**[!UICONTROL Language]**&#x200B;功能表中的所有語言目前並未指派Token。

## 可用動態媒體元件{#dynamic-media-components}

當您點選&#x200B;**[!UICONTROL 元件]**&#x200B;圖示，然後在&#x200B;**[!UICONTROL 動態媒體]**&#x200B;上篩選時，動態媒體元件即可使用。

可用的動態媒體元件包括：

* **[!UICONTROL 動態媒體]** -用於影像、視訊、eCatalog和回轉集等資產。
* **[!UICONTROL 互動式媒體]** -用於任何互動式資產，例如互動式視訊、互動式影像或轉盤集。
* **[!UICONTROL 全景媒體]** -用於全景影像或全景VR影像資產。
* **[!UICONTROL 視訊360媒體]** -用於360視訊和360 VR視訊資產。

>[!NOTE]
>
>這些元件預設不可用，在使用之前必須先透過範本編輯器提供。 在範本編輯器中提供這些元件後，您就可以像新增任何其他Experience Manager元件一樣，將元件新增至頁面。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### 元件：動態媒體{#dynamic-media-component}

動態媒體元件是智慧型元件。 視您新增影像或視訊而定，您有各種選項。 此元件支援影像預設集、影像檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個動態媒體元件例項。
>* 每個例項都使用相同的資產類型。

>
>
請注意，不支援為該頁面上的每個動態媒體元件指派不同的檢視器預設集。
>
>不過，您可以對頁面內使用相同類型資產的所有動態媒體元件使用相同的檢視器預設集。

當您新增動態媒體元件，且&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;為空白或無法正確新增資產時，請勾選下列項目：

* 該影像具有金字塔tiff檔案。 在啟用動態媒體之前匯入的影像沒有金字塔tiff檔案。

#### 使用影像{#when-working-with-images}時

動態媒體元件可讓您新增動態影像，包括影像集、回轉集和混合媒體集。 您可以放大、縮小，如果適用，則可以在回轉集內旋轉影像，或從其他類型的回轉集選取影像。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要讓影像回應，您可以設定中斷點或套用回應式影像預設集。

您可以點選元件中的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示，然後點選&#x200B;**[!UICONTROL 動態媒體設定]**，編輯下列動態媒體設定。

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 檢視器預設]**-從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   如果您要檢視影像集、回轉集或混合媒體集，這是唯一可用的選項。 顯示的檢視器預設集也很聰明——只會顯示相關的檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**-檢視器修飾元採用名稱=值配對與&amp;分隔字元的形式，可讓您變更檢視器，如檢視器參考指南所述。檢視器修飾元的範例是`posterimage=img.jpg&caption=text.vtt,1`，其為視訊縮圖設定不同的影像，並將隱藏字幕／字幕檔案與視訊建立關聯。

* **[!UICONTROL 影像預設集]**-從下拉式選單中選取現有的影像預設集。如果您要尋找的影像預設集不可見，您可能需要將它顯示。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 影像修飾元]**-您可以提供其他影像指令來套用影像效果。這些說明在「影像預設集」和「影像伺服命令」參考中。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 中斷點]**-如果您在回應式網站上使用此資產，則需要新增影像中斷點。影像中斷點必須以逗號(,)分隔。 當影像預設集中未定義高度或寬度時，此選項便可運作。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

   您可以點選元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;來編輯下列進階設定。

* **[!UICONTROL 標題]**-更改影像的標題。

* **[!UICONTROL 替代文字]**-為關閉圖形的使用者新增影像標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL, Open in]** - You can set an asset to open a link.設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。


#### 使用視頻{#when-working-with-video}時

使用動態媒體元件，將動態視訊新增至網頁。 當您編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來播放頁面上的視訊。

![chlimage_1-173](assets/chlimage_1-540.png)

按一下元件中的&#x200B;**[!UICONTROL 編輯]**，即可編輯下列動態媒體設定。

>[!NOTE]
>
>依預設，動態媒體視訊元件是可調式的。 如果要使其成為固定大小，請在元件中將其設定為&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**(**[!UICONTROL Advanced]**)頁籤。

* **[!UICONTROL 檢視器預設]**-從下拉式選單中選取現有的視訊檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱管理檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**-檢視器修飾元採用名稱=值配對與&amp;分隔字元的形式，讓您變更檢視器，如Adobe檢視器參考指南所述。檢視器修飾詞的範例為`posterimage=img.jpg&caption=text.vtt,1`

   例如，使用檢視器修飾元，您可以執行下列動作：

   * 將標題檔案與視訊關聯：[caption](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 將導覽檔案與視訊建立關聯：[navigation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;可以編輯以下高級設定。

* **[!UICONTROL 標題]**-變更影片標題。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

#### 使用Smart Crop {#when-working-with-smart-crop}時

使用動態媒體元件將智慧型裁切影像資產新增至您的網頁。 當您編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來播放頁面上的視訊。

請參閱[搭配使用智慧型裁切與Experience Manager資產動態媒體](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html)

另請參閱[映像配置檔案](/help/assets/dynamic-media/image-profiles.md)。

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

按一下元件中的&#x200B;**[!UICONTROL 編輯]**，即可編輯下列動態媒體設定。

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 影像修飾元]**-您可以提供其他影像指令來套用影像效果。這些說明在「影像預設集」和「影像伺服命令」參考中。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

   按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;可以編輯以下高級設定。

* **[!UICONTROL 啟用外觀比例比對]**-選取此選項，讓動態媒體挑選外觀比例最符合原始影像外觀比例的智慧型裁切轉譯。

* **[!UICONTROL 標題]**-更改「智慧裁切」影像的標題。

* **[!UICONTROL 替代文字]**-為關閉圖形的使用者新增智慧型裁切影像的標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL, Open in]** - You can set an asset to open a link.設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

### 元件：互動式媒體{#interactive-media-component}

互動式媒體元件適用於這些資產上具有互動功能的熱點或影像地圖。 如果您有互動式影像、互動式視訊或轉盤橫幅，請使用&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件。

互動式媒體元件是智慧型的。 視您新增影像或視訊而定，您有各種選項。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個互動式媒體元件例項。
>* 每個例項都使用相同的資產類型。

>
>
請注意，不支援為該頁面上的每個互動式媒體元件指派不同的檢視器預設集。
>
>不過，您可以針對頁面內使用相同類型資產的所有互動式媒體元件使用相同的檢視器預設集。

![chlimage_1-174](assets/chlimage_1-541.png)

您可以點選元件中的&#x200B;**[!UICONTROL Edit]**，編輯下列&#x200B;**[!UICONTROL 一般]**&#x200B;設定。

* **[!UICONTROL 檢視器預設]**-從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 檢視器預設集必須先發佈，才能使用。 請參閱管理檢視器預設集。

* **[!UICONTROL 標題]**-變更影片標題。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。將此值留空可讓資產具有適應性。

   您可以按一下元件中的&#x200B;**[!UICONTROL 編輯]**，編輯下列「新增至購物車」**[!UICONTROL 設定。]**

* **[!UICONTROL 顯示產品資產]**-預設情況下，此值為選定值。產品資產會依「商務」模組中的定義，顯示產品的影像。 清除核取標籤，不會顯示產品資產。

* **[!UICONTROL 顯示產品價格]**-預設情況下，此值處於選中狀態。產品價格顯示「商務」模組中定義的項目價格。 清除勾號以不顯示產品價格。

* **[!UICONTROL 顯示產品表單]**-預設情況下，不選擇此值。「產品表單」包含任何產品變體，例如尺寸和顏色。 清除勾號，不顯示產品變數。

### 元件：全景媒體{#panoramic-media-component}

全景媒體元件適用於球形全景影像的資產。 此類影像可提供360°的房間、房產、位置或風景觀賞體驗。 若要符合球形全景的影像，它必須具備下列其中一個或兩個：

* 寬高比為2:1。
* 使用關鍵字`equirectangular`或(`spherical` + `panorama`)或(`spherical` + `panoramic`)加上標籤。 請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和全景媒體 **** WCM元件的全景資產。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在同一頁上使用&#x200B;**[!UICONTROL 全景媒體]**&#x200B;元件的多個實例。
>* 每個例項都使用相同的資產類型。

>
>
請注意，不支援為該頁面上的每個 **[!UICONTROL Panoramic Media]**  (全景媒體) 元件指派不同的檢視器預設集。
>
>但是，您可以針對頁面內使用相同類型資產的所有全景媒體元件使用相同的檢視器預設集。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

您可以在元件中點選&#x200B;**[!UICONTROL Configure]**&#x200B;來編輯下列設定。

* **[!UICONTROL 檢視器預設]**(Viewer Preset)-從「檢視器預設」下拉式選單中選取現有的檢視器。

如果您所尋找的檢視器預設集不可見，請勾選以確保已發佈。 您必須先發佈檢視器預設集，才能使用。 請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 元件：視訊360媒體{#video-media-component}

使用&#x200B;**[!UICONTROL Video 360 Media]**&#x200B;元件，在您的網頁上演算等長形視訊，以體驗如臨現場的房間、房產、位置、風景或醫療程式。

在平面顯示器上播放時，用戶可以控制視角；在行動裝置上播放時，通常會運用其內建的陀螺控制項。

檢視器包含傳送360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您可使用標準的視訊副檔名（例如。mp4、.mkv和。mov）來傳送360視訊。 最常見的轉碼器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

您可以在元件中點選&#x200B;**[!UICONTROL Configure]**&#x200B;來編輯下列設定。

* **[!UICONTROL 檢視器預設]**(Viewer Preset)-從「檢視器預設」下拉式選單中選取現有的檢視器。使用Video360VR的使用者可使用虛擬實境眼鏡。 包含基本的視訊播放控制項和社交媒體功能。 使用Video360_social，其中包含基本的視訊播放控制項。 視訊演算是在立體模式下完成。 手動視點控制已關閉，但陀螺儀控制已開啟。 沒有社交媒體功能。

如果您所尋找的檢視器預設集不可見，請勾選以確保已發佈。 您必須先發佈檢視器預設集，才能使用。 請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 使用HTTP/2傳送動態媒體資產{#using-http-to-delivery-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並降低所需的處理能力。 動態媒體資產的傳送現在可透過HTTP/2，提供更佳的回應和載入時間。

如需開始使用HTTP/2與動態媒體帳戶的完整詳細資訊，請參閱[HTTP2內容傳送](/help/assets/dynamic-media/http2faq.md)。

>[!MORELIKETHIS]
>
>* [在Experience Manager Dynamic Media中使用視訊播放器](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [將互動式視訊與Experience Manager Dynamic Media搭配使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [使用Experience Manager Dynamic Media瞭解Asset Viewer](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [搭配Experience Manager Dynamic Media使用自訂視訊縮圖](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [使用Experience Manager Dynamic Media瞭解色彩管理](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [搭配Experience Manager Dynamic Media使用影像銳利化](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

