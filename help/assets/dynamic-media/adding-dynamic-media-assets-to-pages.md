---
title: 將Dynamic Media資產添加到頁面
description: 瞭解如何將Dynamic Media元件添加到Adobe Experience Manager as a Cloud Service的頁面。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: da4174929e1eb8e15447f936dc89a67391c72209
workflow-type: tm+mt
source-wordcount: '3216'
ht-degree: 5%

---

# 將Dynamic Media資產添加到頁面{#adding-dynamic-media-assets-to-pages}

若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360全景媒體元件。進入佈局模式並啟用Dynamic Media元件。 然後，將這些元件添加到頁面中，並將資產添加到元件中。 動態媒體元件是智慧型的——他們知道您是新增影像還是視訊，而可用的設定選項也會隨之變更。

如果使用的是Dynamic Media資產，請直接將其添加到頁面 [!DNL Adobe Experience Manager] 你的WCM 如果您使用第三方進行WCM, [連結](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 或 [嵌入](/help/assets/dynamic-media/embed-code.md) 你的資產。 有關響應性第三方網站，請參見 [將優化的映像提供到響應性站點](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>確保在將資產添加到中的頁面之前發佈資產 [!DNL Experience Manager]。 請參閱 [出版Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將Dynamic Media元件添加到頁面 {#adding-a-dynamic-media-component-to-a-page}

將3D媒體、Dynamic Media、互動式媒體、全景媒體、智慧裁剪視頻或視頻360媒體元件添加到頁面與將元件添加到任何頁面相同。

**要將Dynamic Media元件添加到頁面：**

1. 在 [!DNL Experience Manager]，開啟要添加Dynamic Media元件的頁面。
1. 在左窗格中，選擇 **[!UICONTROL 元件]** 表徵圖，然後篩選Dynamic Media。

   如果沒有可用的Dynamic Media元件清單，則可能必須啟用要使用的Dynamic Media元件。 請參閱 [啟用Dynamic Media元件](#enabling-dynamic-media-components)。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. 拖動 **[!UICONTROL Dynamic Media]** 並將其放到頁面上所需的位置。

1. 將指針直接懸停在元件上。 當元件被藍色框包圍時，選擇一次以顯示元件的工具欄。 選擇 **[!UICONTROL 配置（扳手）]** 表徵圖

   ![6_5_360video_wcmcomponent配置](assets/6_5_360video_wcmcomponentconfigure.png)

1. 根據您放到頁面上的Dynamic Media元件，將開啟一個配置對話框。 [設定元件的選項](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 必要時。

   下面的示例顯示了Dynamic Media **[!UICONTROL 視頻360介質]** 對話框，以及「查看器預設」下拉清單中提供的選項。

   ![視頻360媒體元件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media視頻360媒體元件。

1. 完成後，在對話框的右上角，選擇複選標籤以保存更改。

### 啟用Dynamic Media元件 {#enabling-dynamic-media-components}

如果沒有可添加到頁面的Dynamic Media元件，可能意味著必須啟用要使用的元件。

1. 在 [!DNL Experience Manager]，開啟要添加Dynamic Media元件的頁面。
1. 在靠近頁面頂部的工具欄左側，選擇「頁面資訊」表徵圖，然後選擇 **[!UICONTROL 編輯模板]** 從下拉清單中。

   ![編輯模板](/help/assets/assets-dm/edit-template.png)

1. 在工具欄右側靠近頁面頂部，從下拉清單中，選擇 **[!UICONTROL 結構]**。

   ![政策](/help/assets/assets-dm/structure-mode.png)

1. 在頁面底部附近，選擇 **[!UICONTROL 佈局容器]** 開啟其工具欄，然後選擇「策略」表徵圖。
1. 在 **[!UICONTROL 佈局容器]** 的子菜單。 **[!UICONTROL 屬性]** 朝前，確保 **[!UICONTROL 允許的元件]** 的子菜單。

   ![允許的元件](/help/assets/assets-dm/allowed-components.png)

1. 滾動直到您看到 **[!UICONTROL Dynamic Media]**。
1. 選擇左側的>表徵圖 **[!UICONTROL Dynamic Media]**，然後選擇要啟用的Dynamic Media元件。

   ![Dynamic Media元件清單](/help/assets/assets-dm/dm-components-select.png)

1. 靠近 **[!UICONTROL 佈局容器]** 的子菜單。

1. 在工具欄右側靠近頁面頂部，從下拉清單中，選擇 **[!UICONTROL 初始內容]**。
1. [將Dynamic Media元件添加到頁面](#adding-a-dynamic-media-component-to-a-page) 像往常一樣。

## 本地化Dynamic Media元件 {#localizing-dynamic-media-components}

您可以通過以下兩種方式之一來本地化Dynamic Media元件：

* 在「網站」的網頁中，開啟「屬 **[!UICONTROL 性]** 」並選 **[!UICONTROL 取「進階]** 」標籤。選擇所要的本地化語言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 從站點選擇器中，選擇所需的頁或頁組。 選擇 **[!UICONTROL 屬性]** 的 **[!UICONTROL 高級]** 頁籤。 選擇所要的本地化語言。

   >[!NOTE]
   >
   >並非所有可用語言 **[!UICONTROL 語言]** 菜單中當前已分配令牌。

## 可用Dynamic Media元件 {#dynamic-media-components}

Dynamic Media元件在您選擇 **[!UICONTROL 元件]** 表徵圖，然後篩選 **[!UICONTROL Dynamic Media]**。

可用的Dynamic Media元件包括：

* **[!UICONTROL 動態媒體]** -用於影像、視訊、eCatalog和回轉集等資產。
* **[!UICONTROL 互動式媒體]**  — 用於任何互動式資產，如互動式視頻、互動式影像或旋轉盤集。
* **[!UICONTROL 全景媒體]**  — 用於全景影像或全景VR影像資產。
* **[!UICONTROL 視頻360介質]**  — 用於360個視頻和360個VR視頻資產。

>[!NOTE]
>
>預設情況下，這些元件不可用，在使用之前必須通過模板編輯器使用。 在模板編輯器中使這些元件可用後，您可以像添加其它元件一樣將這些元件添加到頁面 [!DNL Experience Manager] 元件。

![6_5動態媒體元件](assets/6_5_dynamicmediawcmcomponents.png)

### 元件：Dynamic Media {#dynamic-media-component}

Dynamic Media是聰明的。 無論您是添加影像還是添加視頻，您都有各種選項。 該元件支援影像預設、基於影像的查看器，如影像集、旋轉集、混合媒體集和視頻。 此外，查看器會響應 — 螢幕大小會根據螢幕大小自動更改。 所有觀眾都是HTML五觀眾。

>[!NOTE]
>
>如果您的網頁具有以下內容：
>
>* 在同一頁上使用的Dynamic Media元件的多個實例。
>* 每個實例使用相同的資產類型。
>
>不支援將不同的查看器預設分配給該頁上的每個Dynamic Media元件。
>
>但是，您可以在頁面內對使用相同類型資產的所有Dynamic Media元件使用相同的查看器預設。

添加Dynamic Media元件時 **[!UICONTROL Dynamic Media設定]** 為空或無法正確添加資產，請檢查以下內容：

* 影像具有金字塔型tiff檔案。 在啟用Dynamic Media之前導入的影像沒有金字塔型Tiff檔案。

#### 使用影像時 {#when-working-with-images}

Dynamic Media元件允許您添加動態映像，包括映像集、旋轉集和混合媒體集。 您可以放大、縮小，如果適用，可以在旋轉集內旋轉影像或從另一類型的集合中選擇影像。

您也可以直接在元件中配置查看器預設、影像預設或影像格式。 要使影像響應，可以設定斷點或應用響應影像預設。

通過選擇以下「Dynamic Media設定」，可以編輯 **[!UICONTROL 編輯]** 表徵圖 **[!UICONTROL Dynamic Media設定]**。

![Dynamic Media影像預設](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 查看器預設]**  — 從下拉清單中選擇現有查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 請參閱管理查看器預設。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

   如果查看映像集、旋轉集或混合媒體集，則此選項是唯一可用的選項。 顯示的查看器預設也是僅智慧相關的查看器預設。

* **[!UICONTROL 查看器修飾符]**  — 查看器修飾符採用名稱=值對和分隔符的形式，並允許您更改查看器，如查看器參考指南中所述。 查看器修飾符的示例是 `posterimage=img.jpg&caption=text.vtt,1` 它為視頻縮略圖設定不同的影像並將隱藏的字幕/字幕檔案與視頻相關聯。

* **[!UICONTROL 影像預設]**  — 從下拉清單中選擇現有影像預設。 如果您要查找的影像預設不可見，則必須使其可見。 請參閱管理影像預設。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 影像修飾符]**  — 可以通過提供更多影像命令來應用影像效果。 這些命令在「影像預設」和「影像服務命令」參考中介紹。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 斷點]**  — 如果在響應站點上使用此資產，則必須添加影像斷點。 影像斷點必須用逗號(,)分隔。 當影像預設中沒有定義高度或寬度時，此選項有效。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

   通過選擇 **[!UICONTROL 編輯]** 的子菜單。

* **[!UICONTROL 針對解析度更高的設備進行優化]**  — 選中（預設）複選框以允許DPR（設備像素比率）優化。

   的 **[!UICONTROL 針對解析度更高的設備進行優化]** 的下界：
   * 在預設類型下， **[!UICONTROL 影像預設]** 的 **[!UICONTROL RESS_IP]** 從 **[!UICONTROL 影像預設]** 的子菜單。

   ![影像預設的裝置像素比率設定](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

   另請參閱 [關於設備像素比優化](/help/assets/dynamic-media/imaging-faq.md#dpr)。

   任意 [!DNL Experience Manager] Dynamic Media智慧成像DPR值被忽略。

* **[!UICONTROL 標題]**  — 更改影像的標題。

* **[!UICONTROL 替代文字]**  — 為關閉圖形的用戶添加影像標題。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL，在中開啟]**  — 您可以設定資產以開啟連結。 設定URL，在「開啟」(Open)中，指明希望在同一窗口或新窗口中開啟它。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

* **[!UICONTROL 高度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

#### 使用視頻時 {#when-working-with-video}

使用Dynamic Media元件將動態視頻添加到網頁。 編輯元件時，您可以選擇使用預定義的視頻查看器預設在頁面上播放視頻。

![chlimage_1-173](assets/chlimage_1-540.png)

通過選擇以下「Dynamic Media設定」，可以編輯 **[!UICONTROL 編輯]** 的子菜單。

>[!NOTE]
>
>預設情況下，Dynamic Media視頻元件是自適應的。 如果要將其設定為固定大小，請在元件中 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 的 **[!UICONTROL 高級]** 頁籤。

* **[!UICONTROL 查看器預設]**  — 從下拉清單中選擇現有視頻查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 請參閱管理查看器預設。

* **[!UICONTROL 查看器修飾符]**  — 查看器修飾符的形式為 `name=value` 帶 `&` 分隔符。 它們允許您更改查看者，如《Adobe查看者參考指南》中所述。 查看器修飾符的示例是 `posterimage=img.jpg&caption=text.vtt,1`

   例如，使用查看器修飾符，您可以執行以下操作：

   * 將字幕檔案與視頻關聯： [字幕](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 將導航檔案與視頻關聯： [導航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      通過選擇 **[!UICONTROL 編輯]** 的子菜單。

* **[!UICONTROL 標題]**  — 更改視頻標題。

* **[!UICONTROL 寬度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

* **[!UICONTROL 高度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

#### 使用Smart Crop時 {#when-working-with-smart-crop}

使用Dynamic Media元件將Smart Crop映像資產添加到網頁。 編輯元件時，您可以選擇使用預定義的視頻查看器預設在頁面上播放視頻。

請參閱 [將Smart Crop與Experience Manager AssetsDynamic Media一起使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

另請參閱 [影像配置檔案](/help/assets/dynamic-media/image-profiles.md)。

![Dynamic Media智慧作物設定](assets/dm-settings-smart-crop.png)

可通過選擇以下Dynamic Media設定 **[!UICONTROL 編輯]** 的子菜單。

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 影像修飾符]**  — 可以通過提供更多影像命令來應用影像效果。 這些命令在「影像預設」和「影像服務命令」參考中介紹。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

   通過選擇 **[!UICONTROL 編輯]** 的子菜單。

* **[!UICONTROL 啟用縱橫比匹配]**  — 要讓Dynamic Media選擇寬高比與原始影像的寬高比最匹配的智慧裁剪格式副本，請選擇此選項。

* **[!UICONTROL 針對解析度更高的設備進行優化]**  — 選中（預設）複選框以允許DPR（設備像素比率）優化。

   的 **[!UICONTROL 針對解析度更高的設備進行優化]** 的下界：

   * 在預設類型下， **[!UICONTROL 智慧裁剪]** 的雙曲餘切值。

   ![智慧作物的設備像素比率設定](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

   另請參閱 [關於設備像素比優化](/help/assets/dynamic-media/imaging-faq.md#dpr)。

   任意 [!DNL Experience Manager] Dynamic Media智慧成像DPR值被忽略。

* **[!UICONTROL 標題]**  — 更改Smart Crop影像的標題。

* **[!UICONTROL 替代文字]**  — 為關閉圖形的用戶添加智慧裁剪影像的標題。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL，在中開啟]**  — 您可以設定資產以開啟連結。 設定URL，在「開啟」(Open)中，指明希望在同一窗口或新窗口中開啟它。

   如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

* **[!UICONTROL 高度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

### 元件：互動式媒體 {#interactive-media-component}

互動式媒體元件用於那些具有交互性的資產，例如熱點或影像映射。 如果您有互動式影像、互動式視頻或旋轉木馬橫幅，請使用 **[!UICONTROL 互動式媒體]** 元件。

交互媒體元件是智慧的。 無論您是添加影像還是添加視頻，您都有各種選項。 此外，查看器會響應 — 螢幕大小會根據螢幕大小自動改變。 所有觀眾都是HTML五觀眾。

>[!NOTE]
>
>如果您的網頁具有以下內容：
>
>* 在同一頁上使用的Interactive Media元件的多個實例。
>* 每個實例使用相同的資產類型。
>
>不支援為該頁面上的每個Interactive Media元件分配不同的查看器預設。
>
>但是，您可以在頁面內對使用相同類型資產的所有Interactive Media元件使用相同的查看器預設。

![chlimage_1-174](assets/chlimage_1-541.png)

可以編輯以下內容 **[!UICONTROL 常規]** 通過選擇 **[!UICONTROL 編輯]** 的子菜單。

* **[!UICONTROL 查看器預設]**  — 從下拉清單中選擇現有查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 必須先發佈查看器預設，然後才能使用它們。 請參閱管理查看器預設。

* **[!UICONTROL 標題]**  — 更改視頻標題。

* **[!UICONTROL 寬度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

* **[!UICONTROL 高度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將此值留空可使資產具有自適應性。

   可以編輯以下內容 **[!UICONTROL 添加到購物車]** 通過選擇 **[!UICONTROL 編輯]** 的子菜單。

* **[!UICONTROL 顯示產品資產]**  — 預設情況下，此值處於選中狀態。 產品資產顯示在「商務」模組中定義的產品影像。 清除複選標籤以不顯示產品資產。

* **[!UICONTROL 顯示產品價格]**  — 預設情況下，此值處於選中狀態。 產品價格顯示在「商務」模組中定義的物料價格。 清除複選標籤以不顯示產品價格。

* **[!UICONTROL 顯示產品窗體]**  — 預設情況下，未選擇此值。 「產品表單」包括任何產品變型，如尺寸和顏色。 清除複選標籤以不顯示產品變型。

### 元件：全景媒體 {#panoramic-media-component}

全景媒體元件用於那些球面全景影像的資產。 這些影像提供房間、房產、位置或景觀的360°觀看體驗。 要使影像符合為球形全景圖，它必須具有以下一個或兩個：

* 寬高比為2:1。
* 用關鍵字標籤 `equirectangular` 或`spherical` + `panorama`)或`spherical` + `panoramic`)。 請參閱 [使用標籤](/help/sites-cloud/authoring/features/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和全景媒體 **** WCM元件的全景資產。

>[!NOTE]
>
>如果您的網頁具有以下內容：
>
>* 多個實例 **[!UICONTROL 全景媒體]** 元件正在同一頁上使用。
>* 每個實例使用相同的資產類型。
>
>為每個用戶分配不同的查看器預設 **[!UICONTROL 全景媒體]** 不支援該頁上的元件。
>
>但是，您可以在頁面內對使用相同類型資產的所有Panoramic Media元件使用相同的查看器預設。

![全景媒體查看器預設](assets/panoramic-media-viewer-preset.png)

通過選擇 **[!UICONTROL 配置]** 的子菜單。

* **[!UICONTROL 查看器預設]**  — 從「查看器」預設下拉清單中選擇現有查看器。

如果您要查找的查看器預設不可見，請檢查以確保已發佈。 在使用查看器預設之前發佈它們。 請參閱 [管理查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 元件：視頻360介質 {#video-media-component}

使用 **[!UICONTROL 視頻360介質]** 元件，在網頁上呈現等長形視頻。 這樣可確保房間、房產、位置、景觀或醫療程式的沈浸式觀看體驗。

在平面顯示器上回放期間，用戶對視角有控制；在移動設備上播放通常使用內置的陀螺控制。

觀眾包括對360個視頻資產的本機支援。 預設情況下，查看或回放不需要其他配置。 使用標準視頻擴展(如.mp4、.mkv和.mov)提供360視頻。 最常見的編解碼器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

通過選擇 **[!UICONTROL 配置]** 的子菜單。

* **[!UICONTROL 查看器預設]**  — 從「查看器」預設下拉清單中選擇現有查看器。 使用Video360VR的最終用戶使用虛擬現實眼鏡。 包括基本視頻播放控制項和社交媒體功能。 使用Video360_social，其中包括基本的視頻播放控制項。 視頻呈現在立體模式下完成。 手動視點控制已關閉，但陀螺儀控制已開啟。 沒有社交媒體功能。

如果您要查找的查看器預設不可見，請檢查以確保已發佈。 在使用查看器預設之前發佈它們。 請參閱 [管理查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)。

### 使用HTTP/2交付Dynamic Media資產 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2是新的、更新的Web協定，它改進了瀏覽器和伺服器的通信方式。 它提供了更快的資訊傳輸，並減少了所需的處理能力。 Dynamic Media資產的交付現在可以通過HTTP/2，從而提供更好的響應和載入時間。

請參閱 [HTTP2內容傳遞](/help/assets/dynamic-media/http2faq.md) 有關使用HTTP/2和您的Dynamic Media帳戶入門的完整詳細資訊。

>[!MORELIKETHIS]
>
>* [在Experience ManagerDynamic Media中使用視頻播放器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [使用互動式視頻與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [瞭解資產查看器，Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [將自定義視頻縮略圖與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [瞭解色彩管理與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [使用影像銳化與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

