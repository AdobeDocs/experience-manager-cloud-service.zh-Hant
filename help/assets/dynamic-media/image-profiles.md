---
title: Dynamic Media影像設定檔
description: 瞭解如何建立包含遮色片銳利化設定和/或智慧型裁切或智慧型色票設定的Dynamic Media影像設定檔。 然後，將設定檔套用至影像資產的資料夾。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions,Best Practices
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 35f31c95e92148ff5f3472f26ea9c40fa5a17947
workflow-type: tm+mt
source-wordcount: '3555'
ht-degree: 5%

---

# Dynamic Media影像設定檔 {#image-profiles}

上傳影像時，您可以套用影像設定檔至資料夾，在上傳時自動裁切影像。

>[!IMPORTANT]
>
>「影像設定檔」不適用於PDF、動畫GIF或INDD (Adobe InDesign)檔案。

## 「不銳利化遮色片」選項 {#unsharp-mask}

建立影像設定檔時，您可以使用 **[!UICONTROL 不銳利化遮色片]** 在最終縮減取樣影像上微調銳利化濾鏡效果的選項。 您可以控制效果的強度、效果的半徑（以畫素測量），以及被忽略的對比度臨界值。 此效果使用與Adobe Photoshop的「遮色片銳利化」濾鏡相同的選項。

>[!NOTE]
>
>USM銳利化遮色片只會套用在PTIFF （金字塔tiff）內縮減取樣超過50%的縮減比例轉譯。 這表示ptiff內大小最大的轉譯不會受到不銳利化遮色片的影響。 而大小較小的轉譯（例如縮圖）會變更（並顯示不銳利化遮色片）。

在 **[!UICONTROL 不銳利化遮色片]**，則您有以下篩選選項：

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>數量</td>
   <td>控制套用至邊緣畫素的對比量。 預設值為1.75。若是高解析度的影像，最高可增加至5。 將「數量」視為濾鏡強度的量度。 範圍為0到5。</td>
  </tr>
  <tr>
   <td>半徑</td>
   <td>決定邊緣畫素周圍影響銳利化的畫素數量。對於高解析度的影像，請輸入1到2。低值只會銳利化邊緣畫素；高值會銳利化較寬的畫素範圍。 正確的值取決於影像的大小。 預設值為0.2。範圍為0到250。</td>
  </tr>
  <tr>
   <td>臨界值</td>
   <td><p>決定套用遮色片銳利化調整濾鏡時要忽略的對比範圍。換言之，此選項決定銳化畫素與周圍區域的差異程度，才會被視為邊緣畫素並予以銳化。 為避免引入雜訊，請嘗試使用0到255之間的值。</p> </td>
  </tr>
 </tbody>
</table>

銳利化的說明請參閱 [銳利化影像](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## 裁切選項 {#crop-options}

當您對影像實作智慧型裁切時，Adobe會建議下列最佳作法並強制進行下列限制：

| 資產 — 限制型別 | 最佳實務 | 強加的限制 |
| --- | --- | --- |
| **影像**  — 每個影像的智慧型裁切數目 | 5 | 100 |

另請參閱 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

智慧型裁切座標會根據外觀比例而定。 針對影像設定檔中的智慧型裁切設定，如果影像設定檔中新增維度的外觀比例相同，則會將相同的外觀比例傳送至Dynamic Media。 Adobe建議您使用相同的裁切區域。 這麼做可確保不會對「影像設定檔」中使用的不同維度造成影響。

您建立的每個智慧型裁切產生都需要額外的處理。 例如，新增五個以上的智慧型裁切外觀比例可能會導致資產擷取速度緩慢。 它也會造成系統負載增加。 由於您可以在資料夾層級套用智慧型裁切，Adobe建議您將其用於資料夾 *僅限* 在需要的位置。

**定義影像設定檔中智慧型裁切的指導方針**
為了控制智慧型裁切使用量，並最佳化裁切的處理時間和儲存空間，Adobe建議下列准則和提示：

* 即將套用智慧型裁切的影像資產必須至少為50 x 50畫素或更大。
* 理想情況下，每個影像可裁切10至15顆智慧型影像，以最佳化熒幕比例和處理時間。
* 根據裁切維度而非最終使用狀況來命名智慧型裁切。 這麼做有助於最佳化在多個頁面上使用單一維度的重複專案。
* 為特定資料夾和子資料夾建立頁面/資產型別的影像設定檔，而非套用至所有資料夾或所有資產的通用智慧型裁切設定檔。
* 套用至子資料夾的影像設定檔會覆寫套用至資料夾的影像設定檔。
* 不允許包含重複智慧型裁切尺寸的影像設定檔。
* 不允許設定有智慧型裁切選項的重複已命名影像設定檔。

您有兩個影像裁切選項可供選擇：「畫素裁切」和「智慧型裁切」。 您也可以選擇自動建立顏色和影像色票，或保留各種目標解析度的裁切內容。

>[!IMPORTANT]
>
>Adobe建議您檢閱任何產生的裁切和色票，確保它們適當且與您的品牌和價值相關。

| 選項 | 使用時機 | 說明 |
| --- | --- | --- |
| **[!UICONTROL 畫素裁切]** | 僅根據尺寸大量裁切影像。 | 從 **[!UICONTROL 裁切選項]** 下拉式清單，選取 **[!UICONTROL 畫素裁切]**.<br>若要從影像的側面裁切，請輸入要從影像任何側面或每一側面裁切的畫素數量。 裁切多少影像取決於影像檔案中的ppi （每英吋畫素）設定。<br>「影像設定檔」畫素裁切會以下列方式呈現：<br>·值包括「上」、「下」、「左」和「右」。<br>·考慮左上方 `0,0` 並從此處計算畫素裁切。<br>·裁切起點：左為X，上為Y<br>·水準計算：原始影像的水準畫素大小減去「左」，然後減去「右」。<br>·垂直計算：垂直畫素高度減去「頂端」，然後減去「底部」。<br>例如，假設您有4000 x 3000畫素影像。 您使用下列值：Top=250、Bottom=500、Left=300、Right=700。<br>從左上角(300,250)裁切，使用（4000-300-700、3000-250-500或3000,2250）的填色空間。 |
| **[!UICONTROL 智慧型裁切]** | 根據視覺焦點批次裁切影像。 | 智慧型裁切利用Adobe Sensei中人工智慧的強大功能，快速大量自動裁切影像。 智慧型裁切會自動偵測並裁切至任何影像中的焦點，以取得預期的目標點，無論熒幕大小為何。<br>從 **[!UICONTROL 裁切選項]** 下拉式清單，選取 **[!UICONTROL 智慧型裁切]**，然後在的右側 **[!UICONTROL 回應式影像裁切]**，啟用（開啟）此功能。<br>預設中斷點大小(**[!UICONTROL 大]**， **[!UICONTROL Medium]**， **[!UICONTROL 小]**)涵蓋行動裝置和平板電腦裝置、桌上型電腦及橫幅上大部分影像所使用的各種尺寸。 如有需要，您可以編輯「大」、「中」和「小」的預設名稱。<br>若要新增更多中斷點，請選取 **[!UICONTROL 新增裁切]**；若要刪除裁切，請選取「垃圾桶」圖示。 |
| **[!UICONTROL 顏色和影像色票]** | 大量產生每個影像的影像色票。 | **注意**： Dynamic Media Classic不支援智慧型色票。<br>從顯示顏色或紋理的產品影像中自動尋找並產生高品質色票。<br>從 **[!UICONTROL 裁切選項]** 下拉式清單，選取 **[!UICONTROL 智慧型裁切]**. 然後在右側 **[!UICONTROL 顏色和影像色票]**，啟用（開啟）此功能。 輸入畫素值，在 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 文字方塊。<br>雖然所有影像裁切都可從「轉譯」邊欄使用，但色票僅能透過 **[!UICONTROL 複製URL]** 功能。 使用您自己的檢視元件來呈現網站上的色票。 此規則的例外是輪播橫幅。 Dynamic Media為輪播橫幅中使用的色票提供檢視元件。<br><br>**使用影像色票**<br>&#x200B;影像色票的URL簡單明瞭：<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>位置 `:Swatch` 會附加至資產請求。<br><br>**使用色票**<br>&#x200B;若要使用色票，請製作 `req=userdata` 以下列專案請求：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的色票資產：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>以下是色票資產的對應 `req=userdata` URL：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>此 `req=userdata` 回應如下：<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>您也可以要求 `req=userdata` XML或JSON格式的回應，如下列個別URL範例所示：<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意**：您必須建立自己的WCM元件，以要求色票並剖析 `SmartSwatchColor` 屬性，以24位元RGB的十六進位值表示。<br>另請參閱 [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) 在檢視器參考指南中。 |
| **[!UICONTROL 保留所有目標解析度的裁切內容]** | 若要維持相同外觀比例的裁切內容 | 當您建立智慧型裁切設定檔時使用。<br>若要針對不同解析度中的指定外觀比例產生新的裁切內容（同時仍維持焦點），請取消勾選此選項 <br>如果您決定取消核取此方塊，請確定原始影像解析度大於您為智慧型裁切描述檔定義的解析度。<br><br>例如，假設您已將外觀比例設定為600 x 600 （大）、400 x 400 （中）和300 x 300 （小）。<br>時間 **[!UICONTROL 保留所有目標解析度的裁切內容]** 選項為 *已核取*，您會在所有三個解析度中看到相同的裁切，類似於下列影像輸出範例（僅供說明用途）：<br>![已勾選選項](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>時間 **[!UICONTROL 保留所有目標解析度的裁切內容]** 選項為 *未勾選*，裁切內容在所有三種解析度中都是新的，類似於以下影像輸出範例（僅供說明用途）：<br>![已取消勾選選項](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### 智慧型裁切和色票支援的影像檔案格式

支援的最大輸入檔案大小解析度為16K。

>[!NOTE]
>
>16K解析度是顯示解析度，水準約為16,000畫素。 最常討論的16K解析度是15360 × 8640，這會將每個維度中8K UHD的畫素計數加倍，總共是四倍。 此解析度有132.7百萬畫素，是4K解析度的16倍，是1080p解析度的64倍。

| 影像格式 | 不區分大小寫的副檔名 | MIME型別 | 支援的輸入色域 | 支援的輸入檔案大小上限 | 支援的影像格式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | 是 |
| CMYK | | | | | 是 |
| EPS | | | | | 否 |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 是；動畫GIF的第一個影格用於轉譯。 您無法設定或變更第一個影格。 |
| JPEG | `.jpg` 和 `.jpeg` | image/jpeg | sRGB | 15 GB | 是 |
| PNG | `.png` | image/png | sRGB | 15 GB | 是 |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | 是 |
| SVG | | | | | 否 |
| TIFF | `.tif` 和 `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | 是 |
| WebP/動畫WebP | | | | | 否 |

## 建立Dynamic Media影像設定檔 {#creating-image-profiles}

若要定義其他資產型別的進階處理引數，請參閱 [設定資產處理](config-dm.md#configuring-asset-processing).

另請參閱 [關於Dynamic Media影像設定檔和視訊設定檔](/help/assets/dynamic-media/about-image-video-profiles.md).

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).

**若要建立Dynamic Media影像設定檔：**

1. 選取Adobe Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 若要新增影像設定檔，請選取 **[!UICONTROL 建立]**.
1. 輸入輪廓名稱，以及遮色片、裁切或色票（或兩者）的銳利化調整值。

   提示：使用專屬於其預期用途的設定檔名稱。 例如，假設您想建立只產生色票的輪廓。 也就是說，智慧型裁切已停用（關閉），而顏色和影像色票已啟用（開啟）。 在這種情況下，您可以使用設定檔名稱「智慧型色票」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options)[和遮色片銳利化](#unsharp-mask)。

   ![裁切](assets/crop.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**。建立的設定檔會顯示在可用設定檔清單中。

## 編輯或刪除Dynamic Media影像設定檔 {#editing-or-deleting-image-profiles}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選取您要編輯或移除的影像設定檔。 若要編輯，請選取 **[!UICONTROL 編輯影像處理設定檔]**. 若要移除它，請選取 **[!UICONTROL 刪除影像處理設定檔]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，請儲存變更。 如果刪除，請確認您要移除設定檔。

## 將Dynamic Media影像設定檔套用至資料夾 {#applying-an-image-profile-to-folders}

當您將「影像描述檔」指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承描述檔。 因此，您只能將一個影像設定檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的影像設定檔指派給資料夾，則新的設定檔會覆寫先前的設定檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至稍後新增至資料夾的資產。

已為其指派設定檔的資料夾會在使用者介面中標示，並在卡片中顯示該設定檔的名稱。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將影像設定檔套用至特定資料夾，或全域套用至所有資產。

若資料夾中已有您後來加以變更的現有影像設定檔，您可以重新處理該資料夾中的資產。 另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### 將Dynamic Media影像設定檔套用至特定資料夾 {#applying-image-profiles-to-specific-folders}

您可以從「 」中，將「影像設定檔」套用至資料夾 **[!UICONTROL 工具]** 功能表，或者如果您在資料夾中，請從 **[!UICONTROL 屬性]**.

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### 從「設定檔」使用者介面將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選取您要套用至一或多個資料夾的影像設定檔。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選取 **[!UICONTROL 將處理設定檔套用至資料夾]** 並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後選取「 」 **[!UICONTROL 套用]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從「屬性」將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]**.
1. 導覽至 *資料夾* （非資產）以套用影像設定檔。
1. 根據您所在的檢視，執行下列任一項作業：
   * 在「卡片檢視」中，將指標暫留在資料夾上，然後選取核取記號以選取它。
   * 在「欄檢視」或「清單檢視」中，選取資料夾名稱左邊的核取方塊。
1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL Dynamic Media處理中]** 標籤。
1. 在 **[!UICONTROL 影像設定檔]**，來自 **[!UICONTROL 設定檔名稱]** 下拉式清單，選取要套用的設定檔。
1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存並關閉]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全域套用Dynamic Media影像設定檔 {#applying-an-image-profile-globally}

除了將設定檔套用至資料夾之外，您還可以全域套用設定檔。 任何資料夾中上傳至Experience Manager Assets的任何內容都會套用選取的設定檔。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**若要全域套用Dynamic Media影像設定檔：**

1. 執行下列任一項作業：

   * 瀏覽至 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並套用適當的設定檔，然後選取 **[!UICONTROL 儲存]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`.

     新增屬性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 並選取 **[!UICONTROL 全部儲存]**.

     ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單一影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe建議您檢閱任何產生的智慧型裁切和智慧型色票，以確保它們適當且與您的品牌和價值相關。

您可以手動重新對齊影像的智慧型裁切視窗或調整其大小，以進一步調整其焦點。

在您編輯智慧型裁切並儲存之後，此變更會傳播到您針對特定影像使用裁切的任何地方。

>[!IMPORTANT]
>
>當您手動重新對齊資產的智慧型裁切視窗或調整其大小時，即使您稍後決定重新處理資產，該編輯仍會維持並保留。 不過，如果您在「 」中編輯寬度和/或高度， **[!UICONTROL 回應式影像裁切]** 影像設定檔的區域中，則該資產必須重新處理。
>另請參閱 [重新處理資料夾中的Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新執行智慧型裁切以再次產生其他裁切。

另請參閱 [編輯多個影像的智慧型裁切或智慧型色票](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**若要編輯單一影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]**，然後移至已套用智慧型裁切或智慧型色票影像設定檔的資料夾。
1. 若要開啟其內容，請選取資料夾。
1. 選取您要調整其智慧型裁切或智慧型色票的影像。
1. 在工具列中，選取 **[!UICONTROL 智慧型裁切]**.

1. 執行下列任一項作業：

   * 在頁面的右上角附近，向左或向右拖曳滑桿可分別增加或減少影像顯示。
   * 在影像上，拖曳角落控點來調整裁切或色票的可檢視區域大小。
   * 在影像上，將方塊/色票拖曳到新位置。 您只能編輯影像色票；色票為靜態。
   * 在影像上方，選取  **[!UICONTROL 回覆]** 還原所有編輯並還原原始裁切或色票。
   * 使用鍵盤方向鍵來裁切框架大小、重新定位影像，或兩者皆使用。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 關閉]** 以返回資產的資料夾。

## 編輯多個影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>Adobe建議您檢閱任何產生的智慧型裁切和智慧型色票，以確保它們適當且與您的品牌和價值相關。

將包含智慧型裁切的「影像設定檔」套用至資料夾後，該資料夾中的所有影像都會套用裁切。 如有需要，您可以 *手動* 在多個影像中重新對齊智慧型裁切視窗或調整其大小，以進一步調整其焦點。

在您編輯智慧型裁切並儲存之後，此變更會傳播到您針對特定影像使用裁切的任何地方。

>[!IMPORTANT]
>
>當您手動重新對齊多個資產的智慧型裁切視窗或是調整其大小時，這些編輯會保留下來，即便您稍後決定重新處理這些資產。 然而，如果您在「影像設定檔」的&#x200B;**[!UICONTROL 回應式影像裁切]**區域中編輯寬度或/及高度，這些資產就需要重新處理。
>另請參閱 [重新處理資料夾中的Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新執行智慧型裁切以再次產生其他裁切。

**若要編輯多個影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]**，然後移至已套用智慧型裁切或智慧型色票影像描述檔的資料夾。
1. 在資料夾中，選取 **[!UICONTROL 更多動作]** (...)圖示，然後選取 **[!UICONTROL 智慧型裁切]**.

1. 在 **[!UICONTROL 編輯智慧型裁切]** 頁面，執行下列任一項作業：

   * 調整頁面上影像的檢視大小。

     在中斷點名稱下拉式清單的右側，向左或向右拖曳滑桿以變更可檢視影像顯示的大小。

     ![edit_smart_rances-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據中斷點名稱篩選可檢視影像清單。 在下列範例中，會在中斷點名稱「中」上篩選影像。

     在頁面的右上角，從下拉式清單中選取中斷點名稱，以篩選您看到的影像。 （請參閱上圖。）

     ![edit_smart_rances-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧型裁切方塊的大小。 執行下列任一項作業：

      * 如果影像隻有智慧型裁切或智慧型色票，請在影像上拖曳裁切方塊的邊角控點。 調整裁切的可檢視區域大小。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上拖曳裁切方塊的邊角控點。 調整裁切的可檢視區域大小。 或者，選取影像下方的智慧型色票（色票為靜態），然後拖曳裁切方塊的邊角控點。 調整色票的可檢視區域大小。

     ![調整影像的智慧型裁切大小](assets/edit_smart_crops-resize.png).

   * 移動智慧型裁切方塊。 執行下列任一項作業：

      * 如果影像隻有智慧型裁切或智慧型色票，請在影像上，將裁切方塊拖曳到新位置。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上，將智慧型裁切方塊拖曳到新位置。 或者，選取影像下方的智慧型色票（色票為靜態），然後將智慧型色票裁切方塊拖曳至新位置。

     ![edit_smart_rances-move](assets/edit_smart_crops-move.png)

   * 復原所有編輯並還原原始的智慧型裁切或智慧型色票（僅適用於目前的編輯作業階段）。

     選取 **[!UICONTROL 回覆]** 影像上方。

     ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 關閉]** 以返回資產的資料夾。

## 從資料夾中移除影像設定檔 {#removing-an-image-profile-from-folders}

當您從資料夾中移除「影像描述檔」時，任何子資料夾都會自動繼承從其父資料夾中移除的描述檔。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以從「 」內的資料夾中移除「影像配置檔案」。 **[!UICONTROL 工具]** 功能表，或者如果您在資料夾中，請從 **[!UICONTROL 屬性]**.

### 透過設定檔使用者介面，從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選取您要從資料夾或多個資料夾移除的影像設定檔。
1. 選取 **[!UICONTROL 從資料夾中移除處理設定檔]** 並選取您要用來從中移除設定檔的一個或多個資料夾，然後選取 **[!UICONTROL 移除]**.

   您可以確認「影像設定檔」不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽 **[!UICONTROL 資產]** 然後移至您要從中移除影像設定檔的資料夾。
1. 在資料夾中，選取核取記號以選取資料夾，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 影像設定檔]** 標籤。
1. 從 **[!UICONTROL 設定檔名稱]** 下拉式清單，選取 **[!UICONTROL 無]**，然後選取 **[!UICONTROL 儲存並關閉]**.

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
