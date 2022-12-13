---
title: Dynamic Media 影像設定檔
description: 了解如何建立包含遮色片銳利化設定、智慧型裁切或智慧型色票（或兩者）的Dynamic Media影像描述檔。 接著，將設定檔套用至影像資產的資料夾。
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 08c4474c71d39ba95191225279bbfca92bb64d7c
workflow-type: tm+mt
source-wordcount: '3524'
ht-degree: 7%

---

# Dynamic Media 影像設定檔 {#image-profiles}

上傳影像時，您可以透過將影像描述檔套用至資料夾，在上傳時自動裁切影像。

>[!IMPORTANT]
>
>·智慧型裁切不支援CMYK影像格式。
·影像設定檔不適用於PDF、動畫GIF或INDD(Adobe InDesign)檔案。

## 遮色片不銳利化選項 {#unsharp-mask}

建立影像設定檔時，您可以使用 **[!UICONTROL 不銳利化遮色片]** 選項來微調最終縮減取樣影像的銳利化濾鏡效果。 您可以控制效果的強度、效果半徑（以像素計量），以及忽略的對比度臨界值。 此效果使用的選項與Adobe Photoshop的「遮色片銳利化」濾鏡相同。

>[!NOTE]
不銳利化遮色片只會套用至縮減取樣超過50%的PTIFF（金字塔Tiff）內縮減縮放的轉譯。 這表示Ptiff中大小最大的轉譯不受遮色片銳利化影響。 而縮小的轉譯（例如縮圖）則會更改（並顯示不銳利化遮色片）。

在 **[!UICONTROL 不銳利化遮色片]**，您有下列篩選選項：

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>數量</td>
   <td>控制套用至邊緣像素的對比度量。 預設值為1.75。對於高解析度影像，可將其增加到最高5。 將「量」視為篩選強度的測量。 範圍是0-5。</td>
  </tr>
  <tr>
   <td>半徑</td>
   <td>決定邊緣像素周圍會影響銳利化的像素數量。若是高解析度影像，輸入介於 1 到 2 之間的值。低數值只會銳利化邊緣的像素；高數值會銳利化較寬的像素範圍。正確的值取決於影像大小。預設值為0.2。範圍為0-250。</td>
  </tr>
  <tr>
   <td>臨界值</td>
   <td><p>確定應用不銳利化遮色片濾鏡時要忽略的對比度範圍。換句話說，此選項可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素且銳化。 為避免引入雜訊，請使用0-255之間的值進行實驗。</p> </td>
  </tr>
 </tbody>
</table>

銳利化在 [銳利化影像](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## 裁切選項 {#crop-options}

當您在影像上實作智慧型裁切時，Adobe會建議下列最佳實務並強制執行下列限制：

| 限制類型 | 最佳實務 | 限制 |
| --- | --- | --- |
| 每個影像的智慧作業數 | 5 | 100 |

另請參閱 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

智慧型裁切座標取決於外觀比例。 對於影像設定檔中的智慧型裁切設定，如果影像設定檔中新增的維度的長寬比相同，則會將相同的長寬比傳送至Dynamic Media。 Adobe建議您使用相同的裁切區域。 這樣做可確保對影像設定檔中使用的不同維度沒有影響。

您建立的每個智慧型裁切產生都需要額外處理。 例如，新增超過五個智慧型裁切長寬比可能會導致資產擷取速度緩慢。 這也可能導致系統負載增加。 由於您可以在資料夾層級套用智慧型裁切，因此Adobe建議您在資料夾上使用智慧型裁切 *僅限* 需要的地方。

**定義影像設定檔中智慧型裁切的准則**
為了控制智慧型裁切的使用，並為處理時間和裁切的儲存進行最佳化，Adobe建議下列准則和提示：

* 請避免建立具有相同寬度和高度值的重複智慧型裁切設定檔。
* 根據裁切維度為智慧型裁切命名，而非根據最終用途。 這麼做有助於最佳化多個頁面上使用單一維度的重複項目。
* 為特定資料夾和子資料夾建立頁面式/資產類型式的影像設定檔，而非套用至所有資料夾或所有資產的通用智慧型裁切設定檔。
* 您套用至子資料夾的影像設定檔會覆寫套用至資料夾的影像設定檔。
* 理想情況下，每個影像要有10-15個智慧裁切，以針對螢幕比例和處理時間進行最佳化。

您有兩個影像裁切選項可供選擇。 您也可以選擇自動建立顏色和影像色票，或保留目標解析度間的裁切內容。

>[!IMPORTANT]
·Adobe建議您檢閱任何產生的裁切和色票，以確保這些裁切和色票適當且與您的品牌和值相關。
·智慧型裁切不支援CMYK影像格式。

| 選項 | 使用時機 | 說明 |
| --- | --- | --- |
| **[!UICONTROL 像素裁切]** | 僅根據維度大量裁切影像。 | 從 **[!UICONTROL 裁切選項]** 下拉清單，選擇 **[!UICONTROL 像素裁切]**.<br>要從影像的兩側裁切，請輸入要從影像的任何一側或每一側裁切的像素數。 影像被裁切的程度取決於影像檔案中的ppi設定（每英吋像素）。<br>影像描述檔像素裁切會以下列方式呈現：<br>·值為上、下、左、右。<br>·左上角被視為 `0,0` 像素裁切從那裡計算出來。<br>·裁切起始點：左為X，上為Y<br>·水準計算：原始影像的水準像素大小減去「左」，然後減去「右」。<br>·垂直計算：垂直像素高度減去「頂部」，然後減去「底部」。<br>例如，假設您有4000 x 3000像素影像。 您使用值：Top=250, Bottom=500, Left=300, Right=700。<br>從左上角(300,250)使用填充空間(4000-300-700、3000-250-500或3000,2250)進行裁切。 |
| **[!UICONTROL 智慧型裁切]** | 根據影像的視覺焦點來大量裁切影像。 | 智慧型裁切運用Adobe Sensei中人工智慧的強大功能，大量快速自動裁切影像。 智慧型裁切功能會自動偵測任何影像中的焦點並裁切至焦點，以取得預期的興趣點（不論螢幕大小）。<br>從 **[!UICONTROL 裁切選項]** 下拉清單，選擇 **[!UICONTROL 智慧型裁切]**，則位於的右側 **[!UICONTROL 回應式影像裁切]**，啟用（開啟）功能。<br>預設斷點大小(**[!UICONTROL 大]**, **[!UICONTROL 中]**, **[!UICONTROL 小]**)涵蓋大部分影像用於行動裝置和平板電腦裝置、桌上型電腦和橫幅的所有大小範圍。 如果需要，可以編輯「大」、「中」和「小」的預設名稱。<br>要添加更多斷點，請選擇 **[!UICONTROL 新增裁切]**;若要刪除裁切，請選取垃圾桶圖示。 |
| **[!UICONTROL 顏色及影像樣本]** | Bulk為每個影像生成一個影像色票。 | **附註**:Dynamic Media Classic不支援智慧色票。<br>從顯示顏色或紋理的產品影像自動定位並生成高質量色板。<br>從 **[!UICONTROL 裁切選項]** 下拉清單，選擇 **[!UICONTROL 智慧型裁切]**. 在右邊 **[!UICONTROL 顏色和影像色票]**，啟用（開啟）功能。 在 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 框。<br>雖然所有影像裁切都可從「轉譯」邊欄使用，但只能透過 **[!UICONTROL 複製URL]** 功能。 使用您自己的檢視元件，在您的網站上轉譯色票。 此規則的例外是輪播橫幅。 Dynamic Media提供輪播橫幅中所用色票的檢視元件。<br><br>**使用影像色票**<br>&#x200B;影像色票的URL非常直接：<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>其中 `:Swatch` 會附加至資產請求。<br><br>**使用顏色色板**<br>&#x200B;若要使用顏色色票，請建立 `req=userdata` 請求，並包含下列項目：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，下列是Dynamic Media Classic中的色票資產：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>這是色票資產對應的 `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>此 `req=userdata` 回應如下：<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>您也可以要求 `req=userdata` XML或JSON格式的回應，如下列個別URL範例所示：<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**附註**:您必須建立自己的WCM元件，才能要求色票並剖析 `SmartSwatchColor` 屬性，由24位RGB十六進位值表示。<br>另請參閱 [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) （位於檢視器參考指南中）。 |
| **[!UICONTROL 保留各種目標解析度的裁切內容]** | 維持相同外觀比例的裁切內容 | 建立智慧型裁切描述檔時使用。<br>取消核取此選項，即可針對不同解析度的指定長寬比，產生新的裁切內容（同時仍維持焦點）。<br>如果您決定取消勾選此方塊，請確定原始影像解析度大於您為智慧型裁切設定檔定義的解析度。<br><br>例如，假設您已將長寬比設定為600 x 600（大）、400 x 400（中）和300 x 300（小）。<br>當 **[!UICONTROL 跨目標解析度保留裁切內容]** 選項 *已勾選*，您會在所有三個解析度中看到相同的裁切，類似下列影像範例輸出（僅供說明之用）:<br>![已核取選項](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>當 **[!UICONTROL 跨目標解析度保留裁切內容]** 選項 *未勾選*，則所有三個解析度都新增裁切內容，類似下列影像範例輸出（僅供說明之用）:<br>![未勾選選項](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### 智慧型裁切和色票支援的影像檔案格式

支援的最大輸入檔案大小解析度為16K。

>[!NOTE]
16K解析度是水準約16,000像素的顯示解析度。 最常討論的16K解析度是15360 × 8640，它使每個維度8K UHD的像素計數加倍，總數是像素的4倍。 此解析度為1.327億像素，是4K解析度的16倍，是1080p解析度的64倍。

| 影像格式 | 不區分大小寫的副檔名 | MIME類型 | 支援的輸入色域 | 支援的最大輸入檔案大小 | 支援的影像格式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | 是 |
| CMYK |  |  |  |  | 否 |
| EPS |  |  |  |  | 否 |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 是；動畫GIF的第一幀用於轉譯。 不能配置或更改第一個幀。 |
| JPEG | `.jpg` 和 `.jpeg` | image/jpeg | sRGB | 15 GB | 是 |
| PNG | `.png` | image/png | sRGB | 15 GB | 是 |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | 是 |
| SVG |  |  |  |  | 否 |
| TIFF | `.tif` 和 `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | 是 |
| WebP/動畫WebP |  |  |  |  | 否 |

## 建立Dynamic Media影像設定檔 {#creating-image-profiles}

若要定義其他資產類型的進階處理參數，請參閱 [設定資產處理](config-dm.md#configuring-asset-processing).

請參閱 [關於Dynamic Media影像設定檔和影片設定檔](/help/assets/dynamic-media/about-image-video-profiles.md).

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).

**若要建立Dynamic Media影像設定檔：**

1. 選取Adobe Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 若要新增影像設定檔，請選取 **[!UICONTROL 建立]**.
1. 輸入描述檔名稱和值，以用於遮色片、裁切或色票，或兩者。

   提示：使用符合其預定用途的設定檔名稱。 例如，假設您要建立僅產生色票的設定檔。 也就是說，智慧型裁切已停用（關閉），而顏色和影像色票已啟用（開啟）。 在這種情況下，您可以使用設定檔名稱「智慧色票」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options)[和遮色片銳利化](#unsharp-mask)。

   ![農作物](assets/crop.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**。新建立的配置檔案將顯示在可用配置檔案清單中。

## 編輯或刪除Dynamic Media影像設定檔 {#editing-or-deleting-image-profiles}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選擇要編輯或刪除的「影像配置檔案」。 若要編輯，請選取 **[!UICONTROL 編輯影像處理設定檔]**. 若要移除，請選取 **[!UICONTROL 刪除影像處理設定檔]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，則保存更改。 如果刪除，請確認您要移除設定檔。

## 將Dynamic Media影像設定檔套用至資料夾 {#applying-an-image-profile-to-folders}

將映像配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 因此，您只能將一個影像描述檔指派給資料夾。 因此，請仔細考慮上傳、儲存、使用和封存資產的資料夾結構。

如果為資料夾分配了不同的影像配置檔案，則新配置檔案將覆蓋前一個配置檔案。 先前的資料夾資產維持不變。 新設定檔會套用至稍後新增至資料夾的資產。

在使用者介面中會指出已指派給資料夾的資料夾，且資料夾的名稱會顯示在資訊卡中。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將影像設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理資料夾中的資產，該資料夾中已有您後來變更的現有影像設定檔。 請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### 將Dynamic Media影像設定檔套用至特定資料夾 {#applying-image-profiles-to-specific-folders}

您可以從 **[!UICONTROL 工具]** ，或者如果您位於資料夾中，則從 **[!UICONTROL 屬性]**.

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### 將Dynamic Media影像設定檔套用至設定檔使用者介面的資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選擇要應用於資料夾或多個資料夾的影像配置檔案。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選擇 **[!UICONTROL 將處理設定檔套用至資料夾]** ，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，並選取 **[!UICONTROL 套用]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從屬性將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 點選Experience Manager標誌並導覽至 **[!UICONTROL 資產]**.
1. 導覽至 *資料夾* （非資產），您要套用影像設定檔。
1. 視您所在的檢視而定，執行下列其中一項操作：
   * 在「卡片檢視」中，將指標暫留在資料夾上，然後選取核取記號加以選取。
   * 在「列視圖」或「清單視圖」中，選擇資料夾名稱左側的複選框。
1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL Dynamic Media處理]** 標籤。
1. 在 **[!UICONTROL 影像設定檔]**，從 **[!UICONTROL 設定檔名稱]** 下拉式清單中，選取要套用的設定檔。
1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存並關閉]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全域套用Dynamic Media影像設定檔 {#applying-an-image-profile-globally}

除了將設定檔套用至資料夾之外，您也可以全域套用一個設定檔。 任何資料夾中上傳至Experience Manager Assets的任何內容皆已套用選取的設定檔。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**若要全域套用Dynamic Media影像設定檔：**

1. 執行下列任一項作業：

   * 導覽至 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並應用適當的配置檔案並選擇 **[!UICONTROL 儲存]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`.

      新增屬性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 選取 **[!UICONTROL 全部儲存]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單一影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
·Adobe建議您檢閱任何產生的智慧型裁切和智慧色板，以確保它們適當且與您的品牌和價值相關。
·智慧型裁切不支援CMYK影像格式。

您可以手動重新對齊或調整影像的智慧型裁切視窗大小，以進一步細化其焦點。

編輯智慧型裁切並儲存後，變更會傳播至您對特定影像使用裁切的所有位置。

>[!IMPORTANT]
手動重新對齊或調整資產的智慧型裁切視窗大小時，即使您稍後決定重新處理資產，編輯的項目仍會維持並保留。 不過，如果您在 **[!UICONTROL 回應式影像裁切]** 影像設定檔的區域，則該資產會重新處理。
請參閱 [在資料夾中重新處理Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新執行智慧型裁切，再次產生其他裁切。

另請參閱 [編輯多個影像的智慧型裁切或智慧型色票](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**要編輯單個影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]**，然後套用至智慧型裁切或智慧型色票影像描述檔的資料夾。
1. 要開啟其內容，請選擇資料夾。
1. 選擇要調整其智慧裁切或智慧色票的影像。
1. 在工具列中，選取 **[!UICONTROL 智慧型裁切]**.

1. 執行下列任一操作：

   * 在頁面的右上角附近，向左或向右拖動滑桿，分別增加或減少影像顯示。
   * 在影像上，拖動角手柄以調整裁切或色板的可視區域的大小。
   * 在影像上，將方塊/色票拖曳至新位置。 只能編輯影像色板；色票為靜態。
   * 在影像上方，選取  **[!UICONTROL 還原]** 還原所有編輯內容，並還原原始裁切或色票。
   * 使用鍵盤箭頭鍵裁切幀大小，或重新定位影像，或兩者。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 關閉]** 返回資產資料夾。

## 編輯多個影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
·Adobe建議您檢閱任何產生的智慧型裁切和智慧色板，以確保它們適當且與您的品牌和價值相關。
·智慧型裁切不支援CMYK影像格式。

將包含智慧型裁切的影像描述檔套用至資料夾後，該資料夾中的所有影像都會套用裁切至它們。 如果需要，您可以 *手動* 重新對齊或調整多個影像中智慧型裁切窗口的大小，以進一步細化其焦點。

編輯智慧型裁切並儲存後，變更會傳播至您對特定影像使用裁切的所有位置。

>[!IMPORTANT]
當您手動重新對齊或調整多個資產的智慧型裁切視窗的大小時，即使您稍後決定重新處理這些資產，這些編輯內容仍會保留和保留。 然而，如果您在「影像設定檔」的&#x200B;**[!UICONTROL 回應式影像裁切]**&#x200B;區域中編輯寬度或/及高度，這些資產就需要重新處理。請參閱 [在資料夾中重新處理Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新執行智慧型裁切，再次產生其他裁切。

**要編輯多個影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]**，則會套用至智慧型裁切或智慧型色票影像描述檔的資料夾。
1. 在資料夾中，選取 **[!UICONTROL 更多動作]** (...)圖示，然後選取 **[!UICONTROL 智慧型裁切]**.

1. 在 **[!UICONTROL 編輯智慧裁切]** 頁面，執行下列任一操作：

   * 調整頁面上影像的檢視大小。

      在斷點名稱下拉清單的右側，向左或向右拖動滑塊條，以更改可視影像顯示的大小。

      ![edit_smart_crobs-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據斷點名稱篩選可視影像清單。 在以下示例中，在斷點名稱「Medium」上篩選影像。

      在頁面的右上角附近，從下拉式清單中選取斷點名稱，以篩選您看到的影像。 （請參閱上圖）。

      ![edit_smart_crobs-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧型裁切框的大小。 執行下列任一操作：

      * 如果影像具有智慧型裁切或僅智慧型色票，請在影像上拖動裁切框的角手柄。 調整裁切的可視區域的大小。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上拖動裁切框的角手柄。 調整裁切的可視區域的大小。 或者，選取影像下方的智慧色板（顏色色板為靜態色板），然後拖動裁切框的角手柄。 調整色板的可視區域的大小。

      ![調整影像的智慧裁切大小](assets/edit_smart_crops-resize.png).

   * 移動智慧型裁切框。 執行下列任一操作：

      * 如果影像具有智慧型裁切或僅智慧型色票，請在影像上將裁切框拖曳至新位置。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上將智慧型裁切方塊拖曳至新位置。 或者，選取影像下方的智慧型色板（色板為靜態色板），然後將智慧型色板裁切框拖到新位置。

      ![edit_smart_crobs-move](assets/edit_smart_crops-move.png)

   * 還原所有編輯內容並還原原始的智慧型裁切或智慧型色票（僅適用於目前的編輯工作階段）。

      選擇 **[!UICONTROL 還原]** 在影像上方。

      ![edit_smart_robs_revert](assets/edit_smart_crops-revert.png)



1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 關閉]** 返回資產資料夾。

## 從資料夾中刪除映像配置檔案 {#removing-an-image-profile-from-folders}

從資料夾中移除影像配置檔案時，任何子資料夾都會自動從其父資料夾中繼承移除配置檔案。 不過，資料夾內發生的檔案處理仍維持不變。

您可以從 **[!UICONTROL 工具]** ，或者如果您位於資料夾中，則從 **[!UICONTROL 屬性]**.

### 透過Profiles使用者介面，從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像設定檔]**.
1. 選擇要從資料夾或多個資料夾中刪除的影像配置檔案。
1. 選擇 **[!UICONTROL 從資料夾中移除處理設定檔]** ，然後選擇要用於從中刪除配置檔案的資料夾或多個資料夾，並選擇 **[!UICONTROL 移除]**.

   您可以確認「影像描述檔」不再套用至資料夾，因為名稱不再出現在資料夾名稱下方。

### 透過屬性從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽 **[!UICONTROL 資產]** ，然後轉到要從中刪除映像配置檔案的資料夾。
1. 在資料夾中，選取要選取的核取記號，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 影像設定檔]** 標籤。
1. 從 **[!UICONTROL 設定檔名稱]** 下拉清單，選擇 **[!UICONTROL 無]**，然後選取 **[!UICONTROL 儲存並關閉]**.

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
