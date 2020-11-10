---
title: Dynamic Media 影像設定檔
description: 建立包含非銳利遮色片和智慧型裁切或智慧型色票（或兩者）的設定的動態媒體影像描述檔，然後將描述檔套用至影像資產的資料夾。
translation-type: tm+mt
source-git-commit: d992b68d4a015f8f947167b5b1d5f0a1ac5c09ec
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 9%

---


# Dynamic Media 影像設定檔 {#image-profiles}

上傳影像時，您可以透過將影像描述檔套用至檔案夾，在上傳時自動裁切影像。

>[!IMPORTANT]
>
>影像描述檔不適用於PDF、GIF動畫或INDD(Adobe InDesign)檔案。

## Crop options {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

智慧型裁切座標視長寬比而定。 也就是說，對於影像描述檔中的各種智慧型裁切設定，如果影像描述檔中新增尺寸的長寬比相同，則會傳送相同的長寬比給動態媒體。 因此，Adobe建議您使用相同的裁切區域。 這樣做將確保對「影像描述檔」中使用的不同尺寸沒有影響。

請注意，您建立的每個智慧型裁切產生都需要額外處理。 例如，新增超過5種智慧型裁切外觀比例會導致資產擷取速度變慢。 它還可能增加系統的負載。 由於您可以在資料夾層級套用「智慧裁切」,Adobe建議您僅在需要智慧裁切的 *資料夾* 上使用它。

您有兩個影像裁切選項可供選擇。 您也可以選擇自動建立顏色和影像色票。

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>使用時機</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>像素裁切</td>
   <td>僅根據尺寸大量裁切影像。</td>
   <td><p>若要使用此選項，請從「裁 <strong>切選項」下拉式清單中選取「像素裁切</strong> 」。</p> <p>若要從影像的兩側裁切，請輸入要從影像的任一側或每側裁切的像素數。 影像被裁切的程度取決於影像檔案中的ppi（像素／英吋）設定。</p> <p>「影像描述檔」像素裁切會以下列方式呈現：<br /> </p>
    <ul>
     <li>值有「上」、「下」、「左」和「右」。</li>
     <li>左上角會視為0,0，而像素裁切會從那裡計算。</li>
     <li>裁切起點：左邊是X，上邊是Y</li>
     <li>水準計算：原始影像的水準像素尺寸減去「左」，然後減去「右」。</li>
     <li>垂直計算：垂直像素高度減去「頂端」，然後減去「底部」。</li>
    </ul> <p>例如，假設您有4000 x 3000像素的影像。 您使用值：Top=250,Bottom=500,Left=300,Right=700。</p> <p>從左上角(300,250)，使用（4000-300-700、3000-250-500或3000,2250）的填滿空間進行裁切。</p> </td>
  </tr>
  <tr>
   <td>智慧型裁切</td>
   <td>根據影像的視覺焦點大量裁切影像。</td>
   <td><p>Smart Crop運用Adobe Sensei中的人工智慧功能，快速將影像裁切大量自動化。 智慧型裁切會自動偵測任何影像中的焦點並裁切至焦點，以擷取預期的興趣點，而不論螢幕大小。</p> <p>若要使用智慧型裁切，請從「裁切選項」下拉式清單中選取「智慧型裁切 <strong></strong> 」，然後在「自適應影像裁切」的右側，啟用（開啟）功能。</p> <p>大、中和小的預設中斷點大小通常涵蓋行動與平板電腦裝置、桌上型電腦和橫幅上使用的大多數影像大小。 如果需要，您可以編輯「大」、「中」和「小」的預設名稱。</p> <p>若要新增更多中斷點，請按一下「 <strong>新增裁切</strong>;若要刪除裁切，請按一下「廢棄項目可以」圖示。</p> </td>
  </tr>
  <tr>
   <td>顏色及影像樣本</td>
   <td>大量產生每個影像的影像色票。</td>
   <td><p><strong>注意</strong>:Dynamic Media Classic不支援智慧型色票。</p> <p>從顯示顏色或紋理的產品影像自動尋找並產生高品質色票。</p> <p>若要使用「顏色和影像色票」，請從「裁切選項」下拉式清單中選取「智慧裁切 <strong></strong> 」，然後在「顏色和影像色票」的右側，啟用（開啟）功能。 在「寬度」和「高度」文字方塊中輸入像素值。</p> <p>雖然所有影像裁切都可從「轉譯」邊欄使用，但色票僅能透過「複製URL」功能使用。 請注意，您必須使用自己的檢視元件來轉換網站上的色票。 (這個例外是轉盤橫幅。 動態媒體提供轉盤橫幅中所用色票的檢視元件。)</p> <p><strong>使用影像色票</strong></p> <p>影像色票的URL很簡單。 即：</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>其中 <code>:Swatch</code> 會附加至資產請求。</p> <p><strong>使用色票</strong></p> <p>若要使用色票，請對下列 <code>req=userdata</code> 項目提出要求：</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>例如，以下是Dynamic Media Classic(Scene7)中的色票資產：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>以下是色票資產的對應 <code>req=userdata</code> URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>回 <code>req=userdata</code> 應如下：</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>您也可以要求以XML <code>req=userdata</code> 或JSON格式回應，如下列個別URL範例所示：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## 不銳利化遮色片 {#unsharp-mask}

您可以使 **[!UICONTROL 用「銳利化遮色片]** 」來微調最終縮減取樣影像的銳利化濾鏡效果。您可以控制效果的強度、效果半徑 (以像素計量)，以及將忽略的對比度臨界值。此效果使用的選項與Adobe Photoshop的「遮色片銳利化」濾鏡相同。

>[!NOTE]
>
>非銳利化遮色片只會套用至PTIFF（金字塔型Tiff）中縮小取樣超過50%的轉譯。 這表示Ptiff中最大尺寸的轉譯不受非銳利遮色片影響，而較小尺寸的轉譯（例如縮圖）則會變更（並顯示非銳利遮色片）。

在「 **[!UICONTROL 遮色片銳利化]**」中，您有下列篩選選項：

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>數量</td>
   <td>控制套用至邊緣像素的對比度。 預設值為1.75。對於高解析度的影像，您可將影像增加到高達5。 將「量」視為濾鏡強度的度量。 範圍是0-5。</td>
  </tr>
  <tr>
   <td>半徑</td>
   <td>決定邊緣像素周圍會影響銳利化的像素數量。若是高解析度影像，輸入介於 1 到 2 之間的值。低數值只會銳利化邊緣的像素；高數值會銳利化較寬的像素範圍。正確的值取決於影像大小。預設值為0.2。範圍是0-250。</td>
  </tr>
  <tr>
   <td>臨界值</td>
   <td><p>決定套用非銳利遮色片濾鏡時要忽略的對比範圍。換言之，此選項可決定銳化的像素在被視為邊緣像素並銳化之前，必須與周圍區域有多大差異。 為避免引入雜訊，請嘗試0-255之間的值。</p> </td>
  </tr>
 </tbody>
</table>

銳利化影像中會 [說明銳利化。](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf)

## Creating Dynamic Media Image Profiles {#creating-image-profiles}

要定義其他資產類型的高級處理參數，請參 [閱配置資產處理](config-dm.md#configuring-asset-processing)。

請參閱 [關於動態媒體影像描述檔和視訊描述檔](/help/assets/dynamic-media/about-image-video-profiles.md)。

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/dynamic-media/best-practices-for-file-management.md)。

**建立動態媒體影像設定檔**

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 點選「 **[!UICONTROL 建立]** 」以新增影像描述檔。
1. 輸入遮色片、裁切或色票或兩者的描述檔名稱和值。

   您可能會發現，使用符合其預定用途的描述檔名稱會很有幫助。 例如，如果要建立僅生成色板的配置檔案，即禁用（關閉）「智慧裁切」並啟用（開啟）「顏色和影像色板」，則可以使用配置檔案名「智慧色板」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options)[和遮色片銳利化](#unsharp-mask)。

   ![作物](assets/crop.png)

1. 點選「 **[!UICONTROL 儲存]**」。 新建立的配置檔案將出現在可用配置檔案清單中。

## 編輯或刪除動態媒體影像設定檔 {#editing-or-deleting-image-profiles}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 選擇要編輯或移除的影像描述檔。 若要編輯，請選取「編輯影 **[!UICONTROL 像處理設定檔」]**。 若要移除它，請選取「刪 **[!UICONTROL 除影像處理描述檔」]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，請儲存變更。 如果刪除，請確認您要移除描述檔。

## 將動態媒體影像描述檔套用至資料夾 {#applying-an-image-profile-to-folders}

將映像配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 這表示您只能將一個影像描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您將不同的影像描述檔指派給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，會以卡中顯示的配置檔案名稱來指示已為其分配配置檔案的資料夾。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將影像描述檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有影像描述檔的資料夾中的資產，而您稍後會變更該資料夾。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

### 將動態媒體影像描述檔套用至特定資料夾 {#applying-image-profiles-to-specific-folders}

You can apply an Image Profile to a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. 本節將說明如何以兩種方式將映像配置檔案應用於資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

#### 將動態媒體影像描述檔套用至描述檔使用者介面中的資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 選擇要應用於資料夾或多個資料夾的映像配置檔案。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap **[!UICONTROL Apply Processing Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap/click **[!UICONTROL Apply]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 將動態媒體影像描述檔套用至屬性中的資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 點選AEM標誌並導覽至 **[!UICONTROL Assets]** ，然後導覽至您要套用影像描述檔的檔案夾。
1. 在資料夾上，點選核取標籤以選取它，然後點選「 **[!UICONTROL 屬性]**」。
1. 點選「影 **[!UICONTROL 像描述檔]** 」標籤。從「描 **[!UICONTROL 述檔名稱]** 」下拉式清單中，選取描述檔，然後點選「 **[!UICONTROL 儲存並關閉」]**。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全域套用動態媒體影像設定檔 {#applying-an-image-profile-globally}

除了將描述檔套用至檔案夾外，您也可以全域套用一個，如此任何檔案夾中上傳至AEM資產的內容都會套用選取的描述檔。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

**若要全域套用動態媒體影像設定檔**:

1. 執行下列任一項作業：

   * 導覽至 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並套用適當的描述檔，然後點選「 **[!UICONTROL 儲存]**」。

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`.

      新增屬性並 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 點選「 **[!UICONTROL 全部儲存」]**。

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單一影像的智慧裁切或智慧色票 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

您可以手動重新對齊或調整影像的智慧裁切視窗大小，以進一步調整其焦點。

編輯智慧型裁切並儲存後，變更會傳播至您使用特定影像裁切的任何地方。

如有需要，您可以重新執行智慧型裁切，以重新產生其他裁切。

另請參 [閱編輯多張影像的智慧裁切或智慧色票](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**要編輯單一影像的智慧裁切或智慧色票**

1. 點選AEM標誌並導覽至 **[!UICONTROL Assets]**，然後導覽至套用智慧裁切或智慧色票影像描述檔的資料夾。

1. 點選資料夾以開啟其內容。
1. 點選您要調整其智慧裁切或智慧色票的影像。
1. 在工具列中，點選「智慧 **[!UICONTROL 裁切」]**。

1. 執行下列任一操作：

   * 在頁面的右上角附近，分別向左或向右拖曳滑桿以增加或減少影像顯示。
   * 在影像上，拖曳角點控制點以調整裁切或色票的可檢視區域大小。
   * 在影像上，將方塊／色票拖曳至新位置。 您只能編輯影像色票；色票是靜態的。
   * 在影像上方點選「 **[!UICONTROL 回復]** 」以還原您的所有編輯，並還原原始裁切或色票。
   * 使用鍵盤箭頭鍵裁切影格大小，或重新定位影像，或兩者皆可。

1. 在頁面的右上角附近，點選「 **[!UICONTROL Save]**」，然後點選「 **[!UICONTROL Close]** 」以返回資產資料夾。

## 編輯多個影像的智慧裁切或智慧色票 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

將包含智慧裁切的映像配置檔案應用到資料夾後，該資料夾中的所有映像都將對其應用裁切。 視需要，您可以手動 *重新對齊* ，或調整多個影像中智慧型裁切視窗的大小，以進一步調整其焦點。

編輯智慧型裁切並儲存後，變更會傳播至您使用特定影像裁切的任何地方。

如有需要，您可以重新執行智慧型裁切，以重新產生其他裁切。

**若要編輯多張影像的智慧裁切或智慧色票**

1. 點選AEM標誌並導覽至 **[!UICONTROL Assets]**，然後導覽至套用智慧裁切或智慧色票影像描述檔的資料夾。
1. 在資料夾上，點選「 **[!UICONTROL 更多動作]** (...)」圖示，然後點選「智 **[!UICONTROL 慧裁切」]**。

1. 在「編 **[!UICONTROL 輯智慧裁切]** 」頁上，執行下列任一操作：

   * 調整頁面上影像的檢視大小。

      在斷點名稱下拉式清單的右側，向左或向右拖曳滑桿，以變更可檢視影像顯示的大小。

      ![edit_smart_crobs-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據斷點名稱篩選可檢視影像清單。 在下面的示例中，會在斷點名稱&quot;Medium&quot;上過濾影像。

      從下拉式清單中，在頁面的右上角附近選取斷點名稱，以篩選您看到的影像。 （請參閱上圖。）

      ![edit_smart_crobs-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧型裁切方塊的大小。 執行下列任一項作業：

      * 如果影像只有智慧型裁切或智慧型色票，請在影像上拖曳裁切方塊的角部控點，以調整裁切的可檢視區域大小。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上拖曳裁切方塊的角部控點，以調整裁切的可檢視區域大小。 或者，點選或按一下影像下方的智慧型色票（色票是靜態的），然後拖曳裁切方塊的角部控點以調整色票的可檢視區域大小。

      ![調整影像的智慧裁切大小。](assets/edit_smart_crops-resize.png)

   * 移動智慧型裁切方塊。 執行下列任一項作業：

      * 如果影像只有智慧型裁切或智慧型色票，請在影像上拖曳裁切方塊至新位置。
      * 如果影像同時具有智慧型裁切和智慧型色票，請將智慧型裁切方塊拖曳至新位置。 或者，點選或按一下影像下方的智慧型色票（色票為靜態），然後將智慧型色票裁切方塊拖曳至新位置。

      ![edit_smart_crobs-move](assets/edit_smart_crops-move.png)

   * 還原您的所有編輯，並還原原始智慧型裁切或智慧型色票（僅適用於目前的編輯工作階段）。

      點選影 **[!UICONTROL 像上方的]** 「回復」。

      ![edit_smart_crobs_revert](assets/edit_smart_crops-revert.png)



1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**. 然後點 **[!UICONTROL 選「關閉]** 」以返回資產資料夾。

## 從資料夾中刪除映像配置檔案 {#removing-an-image-profile-from-folders}

從資料夾中刪除映像配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除該配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

You can remove an Image Profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. 本節介紹如何以兩種方式從資料夾中刪除映像配置檔案。

### 通過配置式用戶介面從資料夾中刪除動態媒體映像配置檔案 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. 選擇要從資料夾或多個資料夾中刪除的映像配置檔案。
1. 點選 **[!UICONTROL 「從資料夾移除處理描述檔」]** ，然後選取您要用來從中移除描述檔的資料夾或多個資料夾，並點選「 **[!UICONTROL 移除」]**。

   您可以確認「影像描述檔」不再套用至資料夾，因為檔案夾名稱下方不會再顯示該名稱。

### 通過屬性從資料夾中刪除動態媒體映像配置檔案 {#removing-image-profiles-from-folders-via-properties}

1. 點選AEM標誌並導覽 **[!UICONTROL Assets]** ，然後前往您要從中移除影像描述檔的檔案夾。
1. 在資料夾上，點選核取標籤以選取它，然後點選「 **[!UICONTROL 屬性]**」。
1. Select the **[!UICONTROL Image Profiles]** tab.
1. From the **[!UICONTROL Profile Name]** drop-down list, select **[!UICONTROL None]**, then tap **[!UICONTROL Save &amp; Close]**.

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
