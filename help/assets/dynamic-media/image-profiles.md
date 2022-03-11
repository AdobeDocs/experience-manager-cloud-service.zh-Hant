---
title: Dynamic Media 影像設定檔
description: 瞭解如何建立包含非銳化蒙版設定和智慧裁剪或智慧色板設定的Dynamic Media影像配置檔案，或同時包含這兩個設定。 然後，將配置檔案應用到影像資產的資料夾。
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: ee44aa9dd6b7977bfa5460ded4b02f1fcbc67096
workflow-type: tm+mt
source-wordcount: '3234'
ht-degree: 7%

---

# Dynamic Media 影像設定檔 {#image-profiles}

上載影像時，可以通過將影像配置檔案應用到資料夾在上載時自動裁剪影像。

>[!IMPORTANT]
>
>影像配置檔案不適用於PDF、動畫GIF或INDD(Adobe InDesign)檔案。

## 「非銳化蒙版」選項 {#unsharp-mask}

建立影像配置檔案時，可以使用 **[!UICONTROL 非銳化蒙版]** 選項來微調最終下採樣影像上的銳化濾鏡效果。 可以控制效果強度、效果半徑（以像素計量）以及忽略的對比度閾值。 此效果使用的選項與Adobe Photoshop的「遮色片銳利化」濾鏡相同。

>[!NOTE]
>
>非銳化蒙版僅應用於PTIFF（金字塔形）中縮放的格式副本，這些格式副本的縮放幅度大於50%。 這意味著在曲線中最大大小的格式副本不受非銳化蒙版的影響。 而較小的格式副本（如縮覽圖）會被更改（並顯示不銳的蒙版）。

在 **[!UICONTROL 非銳化蒙版]**，您具有以下過濾選項：

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>數量</td>
   <td>控制應用於邊緣像素的對比度量。 預設值為1.75。對於高解析度影像，可將其增加到高達5。 將Amount視為過濾器強度的度量。 範圍是0-5。</td>
  </tr>
  <tr>
   <td>半徑</td>
   <td>決定邊緣像素周圍會影響銳利化的像素數量。若是高解析度影像，輸入介於 1 到 2 之間的值。低數值只會銳利化邊緣的像素；高數值會銳利化較寬的像素範圍。正確的值取決於影像大小。預設值為0.2。範圍是0-250。</td>
  </tr>
  <tr>
   <td>臨界值</td>
   <td><p>確定應用非銳化蒙版濾鏡時要忽略的對比度範圍。換句話說，此選項確定銳化的像素在被視為邊緣像素和銳化之前必須與周圍區域有多大差異。 為了避免引入雜訊，用0-255之間的值進行實驗。</p> </td>
  </tr>
 </tbody>
</table>

銳化在 [銳化影像](/help/assets/dynamic-media/assets/sharpening_images.pdf)。

## 裁剪選項 {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

智慧裁剪坐標與縱橫比相關。 對於影像配置檔案中的智慧裁剪設定，如果影像配置檔案中添加的尺寸的長寬比相同，則向Dynamic Media發送相同的長寬比。 Adobe建議您使用相同的裁剪區域。 這樣可確保對「影像配置檔案」中使用的不同尺寸沒有影響。

您建立的每個智慧裁剪生成都需要額外的處理。 例如，添加5個以上的Smart Crop縱橫比可能導致資產吞吐率降低。 它還可能增加系統負載。 因為您可以在資料夾級別應用Smart Crop，所以Adobe建議您在資料夾上使用它 *僅* 需要它的地方。

您有兩個影像裁剪選項可供選擇。 您還可以選擇自動建立顏色和影像色板，或跨目標解析度保留裁剪內容。

>[!IMPORTANT]
>
>Adobe建議您複查所有生成的作物和色板，以確保它們與您的品牌和價值相適當且相關。

| 選項 | 何時使用 | 說明 |
| --- | --- | --- |
| **[!UICONTROL 像素裁切]** | 僅基於尺寸批量裁剪影像。 | 從 **[!UICONTROL 裁剪選項]** 下拉清單，選擇 **[!UICONTROL 像素裁剪]**。<br>要從影像的兩側裁剪，請輸入要從影像的任何一側或每一側裁剪的像素數。 剪切的影像量取決於影像檔案中的ppi（像素/英吋）設定。<br>「影像輪廓」像素裁剪按以下方式呈現：<br>·值為「上」、「下」、「左」和「右」。<br>·左上角 `0,0` 像素裁剪是從那裡計算的。<br>·裁剪起點：左為X，上為Y<br>·水準計算：原始影像的水準像素大小減左後減右。<br>·垂直計算：垂直像素高度減去頂部，然後減去底部。<br>例如，假設您有4000 x 3000像素的影像。 您使用值：上=250，下=500，左=300，右=700。<br>從左上角(300,250)以（4000-300-700、3000-250-500或3000,2250）的填充空間作物。 |
| **[!UICONTROL 智慧型裁切]** | 基於視覺焦點批量裁剪影像。 | Smart Crop利用Adobe Sensei人工智慧的力量，快速實現影像批量裁剪的自動化。 Smart Crop自動檢測任何影像中的焦點並將其裁剪到焦點，以獲得預期的興趣點，而不管螢幕大小。<br>從 **[!UICONTROL 裁剪選項]** 下拉清單，選擇 **[!UICONTROL 智慧裁剪]**，然後在右側 **[!UICONTROL 響應影像裁剪]**，啟用（開啟）該功能。<br>預設斷點大小(**[!UICONTROL 大]**。 **[!UICONTROL 中]**。 **[!UICONTROL 小]**)涵蓋大多數影像在移動和平板電腦設備、台式機和橫幅上使用的所有大小。 如果需要，可編輯「大」(Large)、「中」(Medium)和「小」(Small)的預設名稱。<br>要添加更多斷點，請選擇 **[!UICONTROL 添加裁剪]**;要刪除裁剪，請選擇「垃圾桶」表徵圖。 |
| **[!UICONTROL 顏色及影像樣本]** | Bulk為每個影像生成一個影像樣本。 | **注釋**:Smart Swatch在Dynamic Media Classic不受支援。<br>自動從顯示顏色或紋理的產品影像中定位和生成高質量色板。<br>從 **[!UICONTROL 裁剪選項]** 下拉清單，選擇 **[!UICONTROL 智慧裁剪]**。 在右側 **[!UICONTROL 顏色和影像色板]**，啟用（開啟）該功能。 在 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 的子菜單。<br>雖然所有影像作物都可從「格式副本」(Regbrest)滑軌獲得，但只有通過 **[!UICONTROL 複製URL]** 的子菜單。 使用您自己的查看元件在站點上渲染色板。 此規則的例外是旋轉木馬橫幅。 Dynamic Media為旋轉木馬條幅中使用的色板提供查看元件。<br><br>**使用影像色板**<br>&#x200B;影像色板的URL很簡單：<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>位置 `:Swatch` 附加到資產請求。<br><br>**使用顏色色板**<br>&#x200B;要使用顏色色板，請 `req=userdata` 請求，具體如下：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic的色板資產：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>這是樣本資產的對應 `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>的 `req=userdata` 響應如下：<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>您還可以請求 `req=userdata` XML或JSON格式的響應，如下面各個URL示例中所示：<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注釋**:必須建立自己的WCM元件以請求顏色色板並分析 `SmartSwatchColor` 屬性，由24位RGB十六進位值表示。<br>另請參閱 [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) 的下界。 |
| **[!UICONTROL 保留各種目標解析度的裁切內容]** | 跨相同縱橫比維護裁剪內容 | 建立智慧裁剪配置檔案時使用。<br>取消選中此選項可生成新的裁剪內容（同時仍保持焦點），以獲得不同解析度的給定縱橫比。<br>如果決定取消選中此框，請確保原始影像解析度大於您為「智慧裁剪」配置檔案定義的解析度。<br><br>例如，假設您已將長寬比設定為600 x 600（大）、 400 x 400（中）和300 x 300（小）。<br>當 **[!UICONTROL 跨目標解析度保留裁剪內容]** 選項 *已檢查*，在所有三個解析度中都可以看到相同的裁剪，與以下影像樣本輸出類似（僅供說明用途）:<br>![選中](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>當 **[!UICONTROL 跨目標解析度保留裁剪內容]** 選項 *未*，所有三種解析度的裁剪內容都是新的，與以下影像樣本輸出類似（僅供說明用途）:<br>![選項未選中](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### 智慧裁剪和顏色色板支援的影像檔案格式

支援的最大輸入檔案大小解析度為16K。

| 影像格式 | 不區分大小寫的檔案副檔名 | MIME類型 | 支援的輸入顏色空間 | 支援的最大輸入檔案大小 | 是否支援影像格式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | 是 |
| EPS |  |  |  |  | 否 |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 是；動畫GIF的第一幀用於再現。 不能配置或更改第一個幀。 |
| JPEG | `.jpg`與`.jpeg` | image/jpeg | sRGB | 15 GB | 是 |
| PNG | `.png` | image/png | sRGB | 15 GB | 是 |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | 是 |
| SVG |  |  |  |  | 否 |
| TIFF | `.tif`與`.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | 是 |
| WebP/動畫WebP |  |  |  |  | 否 |

## 建立Dynamic Media映像配置檔案 {#creating-image-profiles}

要為其它資產類型定義高級處理參數，請參閱 [配置資產處理](config-dm.md#configuring-asset-processing)。

請參閱 [關於Dynamic Media影像配置檔案和視頻配置檔案](/help/assets/dynamic-media/about-image-video-profiles.md)。

另請參閱 [組織使用處理配置檔案的數字資產的最佳做法](/help/assets/organize-assets.md)。

**要建立Dynamic Media映像配置檔案：**

1. 選擇Adobe Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像配置檔案]**。
1. 要添加映像配置檔案，請選擇 **[!UICONTROL 建立]**。
1. 輸入非銳化蒙版、裁切或色板或兩者的配置檔案名稱和值。

   提示：使用特定於其預期目的的配置檔案名稱。 例如，假設您要建立僅生成色板的配置檔案。 即，禁用（關閉）智慧裁剪，啟用（開啟）顏色和影像色板。 在這種情況下，您可以使用配置檔案名稱「智慧色板」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options)[和遮色片銳利化](#unsharp-mask)。

   ![作物](assets/crop.png)

1. 選擇 **[!UICONTROL 保存]**。 新建立的配置檔案將出現在可用配置檔案清單中。

## 編輯或刪除Dynamic Media映像配置檔案 {#editing-or-deleting-image-profiles}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像配置檔案]**。
1. 選擇要編輯或刪除的影像配置檔案。 要編輯它，請選擇 **[!UICONTROL 編輯影像處理配置檔案]**。 要刪除它，請選擇 **[!UICONTROL 刪除影像處理配置檔案]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，則保存更改。 如果刪除，請確認要刪除配置檔案。

## 將Dynamic Media映像配置檔案應用於資料夾 {#applying-an-image-profile-to-folders}

將「影像配置檔案」分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 因此，您只能將一個映像配置檔案分配給資料夾。 因此，請仔細考慮上載、儲存、使用和存檔資產所在的資料夾結構。

如果為資料夾分配了不同的「影像配置檔案」，則新配置檔案將覆蓋上一個配置檔案。 以前現有的資料夾資產保持不變。 新配置檔案將應用於稍後添加到資料夾的資產。

在用戶介面中指定分配了配置檔案的資料夾，該配置檔案的名稱出現在卡中。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將映像配置檔案應用於特定資料夾或全局應用於所有資產。

您可以重新處理資料夾中的資產，該資料夾中已經有您稍後更改的現有映像配置檔案。 請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

### 將Dynamic Media映像配置檔案應用於特定資料夾 {#applying-image-profiles-to-specific-folders}

您可以將「影像配置檔案」應用到 **[!UICONTROL 工具]** 或 **[!UICONTROL 屬性]**。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理資料夾中的資產，該資料夾中已有您稍後更改的現有視頻配置檔案。 請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

#### 將Dynamic Media映像配置檔案應用於配置檔案用戶介面中的資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像配置檔案]**。
1. 選擇要應用於資料夾或多個資料夾的影像配置檔案。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選擇 **[!UICONTROL 將處理配置檔案應用於資料夾]** 並選擇要用於接收新上載資產的資料夾或多個資料夾，然後選擇 **[!UICONTROL 應用]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 將Dynamic Media映像配置檔案應用到屬性中的資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 點擊Experience Manager徽標並導航到 **[!UICONTROL 資產]**。
1. 導航到 *資料夾* （不是資產），您要將影像配置檔案應用到其中。
1. 根據您所處的視圖，執行以下操作之一：
   * 在「卡視圖」中，將指針懸停在資料夾上，然後選擇複選標籤以選擇它。
   * 在「列視圖」或「清單視圖」中，選中資料夾名稱左側的複選框。
1. 在工具欄上，選擇 **[!UICONTROL 屬性]**。
1. 選擇 **[!UICONTROL Dynamic Media加工]** 頁籤。
1. 下 **[!UICONTROL 影像配置檔案]**，也請參見Wiki頁。 **[!UICONTROL 配置檔案名稱]** 下拉清單中，選擇要應用的配置檔案。
1. 在頁面右上角附近，選擇 **[!UICONTROL 保存並關閉]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局應用Dynamic Media映像配置檔案 {#applying-an-image-profile-globally}

除了將配置檔案應用到資料夾外，還可以全局應用配置檔案。 任何資料夾中上載到Experience Manager Assets的任何內容都應用了所選配置檔案。

您可以重新處理資料夾中的資產，該資料夾中已有您稍後更改的現有視頻配置檔案。 請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

**要全局應用Dynamic Media映像配置檔案：**

1. 執行下列操作之一：

   * 導航到 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並應用相應的配置檔案，然後選擇 **[!UICONTROL 保存]**。

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 導航到CRXDE Lite到以下節點： `/content/dam/jcr:content`。

      添加屬性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 選擇 **[!UICONTROL 全部保存]**。

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單個影像的智慧裁剪或智慧色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe建議您複查生成的任何智慧作物和智慧色板，以確保它們與您的品牌和價值相適合且相關。

您可以手動重新對齊或調整影像的智慧裁剪窗口大小，以進一步細化其焦點。

編輯智慧裁剪並保存後，更改將隨處傳播，無論您對特定影像使用裁剪。

>[!IMPORTANT]
>
>當手動重新對齊或調整資產的智慧裁剪窗口大小時，即使您稍後決定重新處理資產，也會維護並保留該編輯。 但是，如果在 **[!UICONTROL 響應影像裁剪]** 影像配置檔案的區域，然後重新處理該資產。
>請參閱 [在資料夾中重新處理Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

如有必要，您可以重新運行智慧裁剪以再次生成附加作物。

另請參閱 [編輯多個影像的智慧裁剪或智慧色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**要編輯單個影像的智慧裁剪或智慧色板，請執行以下操作：**

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 資產]**，然後到應用了智慧裁剪或智慧色板影像配置檔案的資料夾。
1. 要開啟其內容，請選擇該資料夾。
1. 選擇要調整其智慧裁剪或智慧色板的影像。
1. 在工具欄中，選擇 **[!UICONTROL 智慧裁剪]**。

1. 執行下列任一操作：

   * 在頁面的右上角附近，向左或向右拖動滑塊條以分別增大或減小影像顯示。
   * 在影像上，拖動角手柄以調整裁剪或色板的可視區域的大小。
   * 在影像上，將框/色板拖到新位置。 只能編輯影像色板；顏色色板是靜態的。
   * 在影像上方，選擇  **[!UICONTROL 還原]** 撤消所有編輯內容並恢復原始裁剪或色板。
   * 使用鍵盤箭頭鍵裁剪幀大小，或重新定位影像，或兩者。

1. 在頁面右上角附近，選擇 **[!UICONTROL 保存]**，然後選擇 **[!UICONTROL 關閉]** 返回到資產資料夾。

## 編輯多個影像的智慧裁剪或智慧色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

將包含智慧裁剪的影像配置檔案應用到資料夾後，該資料夾中的所有影像都將應用裁剪。 如果需要，您可以 *手動* 在多個影像中重新對齊或調整智慧裁剪窗口的大小，以進一步細化其焦點。

編輯智慧裁剪並保存後，更改將隨處傳播，無論您對特定影像使用裁剪。

>[!IMPORTANT]
>
>當您手動重新對齊或調整多個資產的智慧裁剪窗口大小時，即使您稍後決定重新處理這些資產，也會維護和保留這些編輯。 然而，如果您在「影像設定檔」的&#x200B;**[!UICONTROL 回應式影像裁切]**區域中編輯寬度或/及高度，這些資產就需要重新處理。
>請參閱 [在資料夾中重新處理Dynamic Media資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

如有必要，您可以重新運行智慧裁剪以再次生成附加作物。

**要編輯多個影像的智慧裁剪或智慧色板：**

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 資產]**，然後轉到應用了智慧裁剪或智慧色板影像配置檔案的資料夾。
1. 在資料夾上，選擇 **[!UICONTROL 更多操作]** (...)表徵圖，然後選擇 **[!UICONTROL 智慧裁剪]**。

1. 在 **[!UICONTROL 編輯智慧作物]** 頁，執行下列任一操作：

   * 調整頁面上影像的查看大小。

      在斷點名稱下拉清單的右側，向左或向右拖動滑塊以更改可視影像顯示的大小。

      ![編輯_smart_crobs_sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據斷點名稱篩選可視影像清單。 在以下示例中，在斷點名稱「Medium」上過濾影像。

      在頁面右上角的下拉清單中，選擇斷點名稱以篩選您看到的影像。 （請參閱上圖。）

      ![edit_smart_crobs_dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧裁剪框的大小。 執行下列任一操作：

      * 如果影像僅具有智慧裁剪或智慧色板，則在影像上拖動裁剪框的角手柄。 調整裁剪的可視區域大小。
      * 如果影像既具有智慧裁剪又具有智慧色板，則在影像上拖動裁剪框的角手柄。 調整裁剪的可視區域大小。 或者，選擇影像下方的智慧色板（顏色色板是靜態的），然後拖動裁剪框的角手柄。 調整色板的可視區域大小。

      ![調整影像的智慧裁剪大小](assets/edit_smart_crops-resize.png)。

   * 移動智慧裁剪框。 執行下列任一操作：

      * 如果影像僅具有智慧裁剪或智慧色板，則將裁剪框拖到新位置。
      * 如果影像既具有智慧裁剪又具有智慧色板，則在影像上將智慧裁剪框拖動到新位置。 或者，選擇影像下方的智慧色板（顏色色板是靜態的），然後將智慧色板裁剪框拖到新位置。

      ![編輯_smart_crobs移動](assets/edit_smart_crops-move.png)

   * 撤消所有編輯並恢復原始智慧裁剪或智慧色板（僅適用於當前編輯會話）。

      選擇 **[!UICONTROL 還原]** 影像上方。

      ![edit_smart_crobs還原](assets/edit_smart_crops-revert.png)



1. 在頁面右上角附近，選擇 **[!UICONTROL 保存]**，然後選擇 **[!UICONTROL 關閉]** 返回到資產資料夾。

## 從資料夾中刪除映像配置檔案 {#removing-an-image-profile-from-folders}

從資料夾中刪除影像配置檔案時，任何子資料夾都會自動從其父資料夾中繼承刪除配置檔案。 但是，對資料夾中已發生的檔案的任何處理都保持不變。

您可以從 **[!UICONTROL 工具]** 或 **[!UICONTROL 屬性]**。

### 通過配置式用戶介面從資料夾中刪除Dynamic Media映像配置式 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像配置檔案]**。
1. 選擇要從資料夾或多個資料夾中刪除的映像配置檔案。
1. 選擇 **[!UICONTROL 從資料夾中刪除處理配置檔案]** 並選擇要用於從中刪除配置檔案的資料夾或多個資料夾，然後選擇 **[!UICONTROL 刪除]**。

   您可以確認「映像配置檔案」不再應用於資料夾，因為該名稱不再出現在資料夾名稱下。

### 通過「屬性」從資料夾中刪除Dynamic Media映像配置檔案 {#removing-image-profiles-from-folders-via-properties}

1. 選擇Experience Manager徽標並導航 **[!UICONTROL 資產]** 然後轉到要從中刪除映像配置檔案的資料夾。
1. 在資料夾上，選擇複選標籤以選擇它，然後選擇 **[!UICONTROL 屬性]**。
1. 選擇 **[!UICONTROL 影像配置檔案]** 頁籤。
1. 從 **[!UICONTROL 配置檔案名稱]** 下拉清單，選擇 **[!UICONTROL 無]**，然後選擇 **[!UICONTROL 保存並關閉]**。

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
