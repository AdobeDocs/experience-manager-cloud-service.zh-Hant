---
title: 將Dynamic Media Assets新增至頁面
description: 了解如何將Dynamic Media元件新增至Adobe Experience Manager中的頁面，作為Cloud Service。
contentOwner: Rick Brough
feature: 資產管理
role: Business Practitioner
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: 0824f77c35fc97a5bf703036d299c37b75935301
workflow-type: tm+mt
source-wordcount: '3242'
ht-degree: 5%

---

# 將Dynamic Media資產新增至頁面{#adding-dynamic-media-assets-to-pages}

若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360全景媒體元件。您可以進入「配置」模式並啟用Dynamic Media元件。 接著，您將這些元件新增至頁面，並新增資產至元件。 動態媒體元件是智慧型的——他們知道您是新增影像還是視訊，而可用的設定選項也會隨之變更。

如果您使用Dynamic Media作為WCM，請直接將Experience Manager新增至頁面。 如果您使用協力廠商來處理WCM，請[link](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[embed](/help/assets/dynamic-media/embed-code.md)您的資產。 如需回應式第三方網站，請參閱將最佳化影像傳送至回應式網站](/help/assets/dynamic-media/responsive-site.md)。[

>[!NOTE]
>
>請務必先發佈資產，再將其新增至Experience Manager中的頁面。 請參閱[發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將Dynamic Media元件新增至頁面{#adding-a-dynamic-media-component-to-a-page}

將3D媒體、Dynamic Media、互動式媒體、全景媒體、智慧型裁切視訊或視訊360媒體元件新增至頁面，與將元件新增至任何頁面相同。

**若要將Dynamic Media元件新增至頁面：**

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 在左窗格中，點選&#x200B;**[!UICONTROL 元件]**&#x200B;圖示，然後篩選Dynamic Media。

   如果沒有可用的Dynamic Media元件清單，您可能必須啟用您要使用的Dynamic Media元件。 請參閱[啟用Dynamic Media元件](#enabling-dynamic-media-components)。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. 拖曳&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件，並將其放置到頁面上的所需位置。

1. 將指標直接暫留在元件上。 當元件被藍色框包圍時，點選一次以顯示元件的工具列。 點選「**[!UICONTROL 設定（扳手）]**」圖示。

   ![6_5_360 video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. 視您拖放至頁面的Dynamic Media元件而定，會開啟設定對話方塊。 [視需要設定元件](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 的選項。

   以下範例顯示Dynamic Media **[!UICONTROL Video 360 Media]**&#x200B;元件對話方塊，以及「檢視器預設集」下拉式清單中可用的選項。

   ![視訊360媒體元件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media Video 360媒體元件。

1. 完成後，在對話框的右上角，點選複選標籤以保存更改。

### 啟用Dynamic Media元件{#enabling-dynamic-media-components}

如果沒有可新增至頁面的Dynamic Media元件，這可能表示您必須啟用您要使用的元件。

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 在工具列的靠近頁面頂端的左側，點選「頁面資訊」圖示，然後從下拉式清單中點選「 **[!UICONTROL 編輯範本]** 」。

   ![編輯範本](/help/assets/assets-dm/edit-template.png)

1. 在工具列的靠近頁面頂端的右側，從下拉式清單中，點選&#x200B;**[!UICONTROL Structure]**。

   ![政策](/help/assets/assets-dm/structure-mode.png)

1. 在頁面底部附近，點選「 **[!UICONTROL Layout Container]** 」以開啟其工具列，然後點選「 Policy 」圖示。
1. 在「**[!UICONTROL 佈局容器]**」頁的「**[!UICONTROL 屬性]**」標題下，確保選中「**[!UICONTROL 允許的元件]**」頁簽。

   ![允許的元件](/help/assets/assets-dm/allowed-components.png)

1. 捲動直到您看見&#x200B;**[!UICONTROL Dynamic Media]**。
1. 點選&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;左側的>圖示，然後選取您要啟用的Dynamic Media元件。

   ![Dynamic Media元件清單](/help/assets/assets-dm/dm-components-select.png)

1. 在「**[!UICONTROL 版面容器]**」頁面的右上角附近，點選「完成」（勾選記號）圖示。

1. 在工具列的靠近頁面頂端的右側，從下拉式清單中，點選&#x200B;**[!UICONTROL 初始內容]**。
1. [照常將Dynamic Media元件新](#adding-a-dynamic-media-component-to-a-page) 增至頁面。

## 將Dynamic Media元件當地語系化{#localizing-dynamic-media-components}

您可以透過下列兩種方式之一，將Dynamic Media元件當地化：

* 在「網站」的網頁中，開啟「屬 **[!UICONTROL 性]** 」並選 **[!UICONTROL 取「進階]** 」標籤。選擇所要的本地化語言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 從網站選擇器中，選取所需的頁面或頁面群組。 點選&#x200B;**[!UICONTROL 屬性]**&#x200B;並選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。 選擇所要的本地化語言。

   >[!NOTE]
   >
   >並非所有在&#x200B;**[!UICONTROL Language]**&#x200B;功能表中可用的語言都當前已分配令牌。

## 可用的Dynamic Media元件{#dynamic-media-components}

點選「**[!UICONTROL 元件]**」圖示，然後依&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;篩選時，可使用Dynamic Media元件。

可用的Dynamic Media元件包括：

* **[!UICONTROL 動態媒體]** -用於影像、視訊、eCatalog和回轉集等資產。
* **[!UICONTROL 互動式媒體]**  — 用於任何互動式資產，例如互動式視訊、互動式影像或轉盤集。
* **[!UICONTROL 全景媒體]**  — 用於全景影像或全景VR影像資產。
* **[!UICONTROL 影片]** 360媒體 — 用於360影片和360 VR影片資產。

>[!NOTE]
>
>這些元件預設不可用，且必須先透過範本編輯器使用，才能使用。 在範本編輯器中使用元件後，您就可以像新增任何其他Experience Manager元件一樣，將元件新增至頁面。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### 元件：Dynamic Media {#dynamic-media-component}

Dynamic Media元件很智慧。 視您新增影像或影片而定，您有各種選項。 元件支援影像預設集、以影像為基礎的檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器具有回應性 — 螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個Dynamic Media元件例項。
>* 每個例項都使用相同的資產類型。

>
>
不支援為該頁面上的每個Dynamic Media元件指派不同的檢視器預設集。
>
>不過，對於在頁面內使用相同類型資產的所有Dynamic Media元件，您可以使用相同的檢視器預設集。

新增Dynamic Media元件且&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;空白或無法正確新增資產時，請檢查下列項目：

* 影像具有金字塔Tiff檔案。 在啟用Dynamic Media之前匯入的影像沒有金字塔Tiff檔案。

#### 使用影像{#when-working-with-images}時

Dynamic Media元件可讓您新增動態影像，包括影像集、回轉集和混合媒體集。 您可以放大、縮小，如果適用，可以在回轉集內開啟影像，或從另一類型的集合中選取影像。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要讓影像具有回應性，您可以設定斷點或套用回應式影像預設集。

您可以點選元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;圖示，然後點選&#x200B;**[!UICONTROL Dynamic Media設定]**，以編輯下列Dynamic Media設定。

![Dynamic Media影像預設集設定](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式清單中選取現有的檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之則無法選取。

   如果您正在檢視影像集、回轉集或混合媒體集，此選項是唯一可用的選項。 顯示的檢視器預設集也是僅智慧型的相關檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**  — 檢視器修飾元會以名稱=值配對和分隔字元的形式，並可讓您依照檢視器參考指南中的概述來變更檢視器。查看器修飾符的示例是`posterimage=img.jpg&caption=text.vtt,1`，它為視頻縮略圖設定不同的影像，並將隱藏式字幕/字幕檔案與視頻關聯。

* **[!UICONTROL 影像預設]**  — 從下拉式清單中選取現有的影像預設集。如果您要尋找的影像預設集未顯示，則必須使其可見。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之則無法選取。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL 影像修飾元]**  — 您可以提供更多影像命令來套用影像效果。這些命令在「影像預設集」和「影像伺服命令」參考中描述。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL 中斷點]**  — 如果您在回應式網站上使用此資產，則必須新增影像中斷點。影像斷點必須用逗號(,)分隔。 當影像預設集中未定義高度或寬度時，此選項即可運作。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

   您可以點選元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;以編輯下列進階設定。

* **[!UICONTROL 針對高解析度裝置最佳化]**  — 選取（預設）核取方塊，以允許最佳化DPR（裝置像素比率）。

   另請參閱[關於裝置像素比例最佳化](/help/assets/dynamic-media/imaging-faq.md#dpr)。

   請注意，會忽略任何Adobe Experience Manager Dynamic Media智慧型影像處理DPR值。

   **[!UICONTROL 僅當以下情況為真時，才會顯示]**&#x200B;為高解析度設備優化選項：
   * 在「預設類型」下，選擇&#x200B;**[!UICONTROL 影像預設集]**，並從&#x200B;**[!UICONTROL 影像預設集]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL RESS_IP]**。

   ![影像預設集中的裝置像素比率設定](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

* **[!UICONTROL 標題]**  — 變更影像的標題。

* **[!UICONTROL 替代文字]**  — 為關閉圖形的使用者新增影像標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL URL，在]** 中開啟 — 您可以設定資產以開啟連結。設定URL，然後在「開啟」中（在中）指出您要在相同視窗還是新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL 寬度]**  — 如果要讓影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

* **[!UICONTROL 高度]**  — 如果影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

#### 使用視訊{#when-working-with-video}時

使用Dynamic Media元件將動態視訊新增至網頁。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來在頁面上播放視訊。

![chlimage_1-173](assets/chlimage_1-540.png)

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列Dynamic Media設定。

>[!NOTE]
>
>依預設，Dynamic Media視訊元件是最適化的。 如果要將其設定為固定大小，請在元件中以&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤中的&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;設定它。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式清單中選取現有的視訊檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 請參閱管理檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**  — 檢視器修飾元會以 `name=value` 分隔字元配對的 `&` 形式。它們可讓您依照「Adobe檢視器參考指南」中的概述來變更檢視器。 檢視器修飾詞的範例為`posterimage=img.jpg&caption=text.vtt,1`

   例如，使用檢視器修飾元，您可以執行下列操作：

   * 將字幕檔案與視頻關聯：[caption](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 將導覽檔案與視訊建立關聯：[navigation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列進階設定。

* **[!UICONTROL 標題]**  — 變更視訊的標題。

* **[!UICONTROL 寬度]**  — 如果要讓影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

* **[!UICONTROL 高度]**  — 如果影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

#### 使用智慧型裁切{#when-working-with-smart-crop}時

使用Dynamic Media元件將智慧型裁切影像資產新增至網頁。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來在頁面上播放視訊。

請參閱[將智慧型裁切與Experience Manager資產搭配使用Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

另請參閱[影像設定檔](/help/assets/dynamic-media/image-profiles.md)。

![Dynamic Media智慧型裁切設定](assets/dm-settings-smart-crop.png)

您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列Dynamic Media設定。

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 影像修飾元]**  — 您可以提供更多影像命令來套用影像效果。這些命令在「影像預設集」和「影像伺服命令」參考中描述。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

   您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列進階設定。

* **[!UICONTROL 啟用外觀比例比對]**  — 若要讓Dynamic Media挑選外觀比例最符合原始影像外觀比例的智慧型裁切輸出，請選取此選項。

* **[!UICONTROL 針對高解析度裝置最佳化]**  — 選取（預設）核取方塊，以允許最佳化DPR（裝置像素比率）。

   另請參閱[關於裝置像素比例最佳化](/help/assets/dynamic-media/imaging-faq.md#dpr)。

   請注意，會忽略任何Adobe Experience Manager Dynamic Media智慧型影像處理DPR值。

   **[!UICONTROL 僅當以下情況為真時，才會顯示]**&#x200B;為高解析度設備優化選項：

   * 在「預設類型」下，選擇了「智慧型裁切」]**選項。**[!UICONTROL 

   ![智慧作物的裝置像素比例設定](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

* **[!UICONTROL 標題]**  — 變更智慧型裁切影像的標題。

* **[!UICONTROL 替代文字]**  — 為關閉圖形的使用者新增智慧型裁切影像的標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL URL，在]** 中開啟 — 您可以設定資產以開啟連結。設定URL，然後在「開啟」中（在中）指出您要在相同視窗還是新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則無法使用此選項。

* **[!UICONTROL 寬度]**  — 如果要讓影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

* **[!UICONTROL 高度]**  — 如果影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

### 元件：互動式媒體{#interactive-media-component}

互動式媒體元件適用於在這些資產上具有互動的熱點或影像地圖。 如果您有互動式影像、互動式視訊或輪播橫幅，請使用&#x200B;**[!UICONTROL 互動式媒體]**&#x200B;元件。

互動式媒體元件是智慧型的。 視您新增影像或影片而定，您有各種選項。 此外，檢視器回應式 — 螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個互動式媒體元件例項。
>* 每個例項都使用相同的資產類型。

>
>
不支援為該頁面上的每個Interactive Media元件指派不同的檢視器預設集。
>
>不過，對於頁面內使用相同類型資產的所有互動式媒體元件，您可以使用相同的檢視器預設集。

![chlimage_1-174](assets/chlimage_1-541.png)

您可以點選元件中的&#x200B;**[!UICONTROL Edit]**，編輯下列&#x200B;**[!UICONTROL 一般]**&#x200B;設定。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式清單中選取現有的檢視器預設集。如果您要尋找的檢視器預設集未顯示，您必須使其顯示。 必須先發佈檢視器預設集，才能使用。 請參閱管理檢視器預設集。

* **[!UICONTROL 標題]**  — 變更視訊的標題。

* **[!UICONTROL 寬度]**  — 如果要讓影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

* **[!UICONTROL 高度]**  — 如果影像大小固定，請輸入像素值。將此值保留為空白可讓資產最適化。

   您可以按一下元件中的&#x200B;**[!UICONTROL Edit]**&#x200B;編輯下列&#x200B;**[!UICONTROL 新增至購物車]**&#x200B;設定。

* **[!UICONTROL 顯示產品資產]**  — 依預設，會選取此值。產品資產會依照商務模組中的定義顯示產品的影像。 清除勾號以不顯示產品資產。

* **[!UICONTROL 顯示產品價格]**  — 依預設，此值會選取。產品價格顯示商務模組中定義的項目價格。 清除勾號以不顯示產品價格。

* **[!UICONTROL 顯示產品表單]**  — 依預設，未選取此值。產品表單包含任何產品變體，例如大小和顏色。 清除勾號以不顯示產品變體。

### 元件：全景媒體{#panoramic-media-component}

全景媒體元件用於那些為球形全景影像的資產。 這些影像提供360°的房間、屬性、位置或景觀的觀看體驗。 要使影像符合球形全景，它必須具有以下一個或兩個：

* 長寬比為2:1。
* 使用關鍵字`equirectangular`或(`spherical` + `panorama`)或(`spherical` + `panoramic`)加上標籤。 請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和全景媒體 **** WCM元件的全景資產。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用的&#x200B;**[!UICONTROL 全景媒體]**&#x200B;元件的多個例項。
>* 每個例項都使用相同的資產類型。

>
>
不支援為該頁面上的每個&#x200B;**[!UICONTROL 全景媒體]**&#x200B;元件指派不同的檢視器預設集。
>
>不過，對於在頁面內使用相同類型資產的所有全景媒體元件，您可以使用相同的檢視器預設集。

![全景媒體檢視器預設集](assets/panoramic-media-viewer-preset.png)

您可以點選元件中的&#x200B;**[!UICONTROL Configure]**&#x200B;以編輯下列設定。

* **[!UICONTROL 檢視器預設]**  — 從「檢視器預設集」下拉式清單中選取現有的檢視器。

如果您要尋找的檢視器預設集未顯示，請核取以確認其已發佈。 請先發佈檢視器預設集，再加以使用。 請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 元件：視頻360媒體{#video-media-component}

使用&#x200B;**[!UICONTROL Video 360 Media]**&#x200B;元件在您的網頁上呈現等矩形視訊。 這樣可確保房間、屬性、位置、景觀或醫療程式的沈浸式觀看體驗。

在平面顯示器上播放期間，使用者可控制觀看角度；在行動裝置上播放通常使用其內建的陀螺控制項。

檢視器包含360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的編解碼器為H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

您可以點選元件中的&#x200B;**[!UICONTROL Configure]**&#x200B;以編輯下列設定。

* **[!UICONTROL 檢視器預設]**  — 從「檢視器預設集」下拉式清單中選取現有的檢視器。使用Video360VR，適合使用虛擬現實眼鏡的最終用戶。 包含基本視訊播放控制項和社交媒體功能。 使用Video360_social，其中包含基本視訊播放控制項。 視訊轉譯是以立體模式完成。 手動視點控制關閉，但陀螺儀控制開啟。 沒有社交媒體功能。

如果您要尋找的檢視器預設集未顯示，請核取以確認其已發佈。 請先發佈檢視器預設集，再加以使用。 請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 使用HTTP/2來傳送Dynamic Media資產{#using-http-to-delivery-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供了更快的資訊傳輸，並降低了所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2，提供更理想的回應和載入時間。

如需開始使用Dynamic Media帳戶的HTTP/2的完整詳細資訊，請參閱[HTTP2內容傳送](/help/assets/dynamic-media/http2faq.md)。

>[!MORELIKETHIS]
>
>* [在Experience ManagerDynamic Media中使用視訊播放器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [使用互動式影片搭配Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [透過Experience ManagerDynamic Media了解資產檢視器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [使用自訂視訊縮圖與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [透過Experience ManagerDynamic Media了解色彩管理](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [將影像銳利化與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

