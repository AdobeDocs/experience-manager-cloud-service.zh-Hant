---
title: Dynamic Media 影像設定檔
description: 了解如何建立包含遮色片銳利化設定、智慧型裁切或智慧型色票（或兩者）的Dynamic Media影像描述檔。 接著，將設定檔套用至影像資產的資料夾。
feature: 資產管理，影像設定檔，轉譯
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: b6f25c59e7b0cd239a91dc9eb629957905a77574
workflow-type: tm+mt
source-wordcount: '2714'
ht-degree: 7%

---

# Dynamic Media 影像設定檔 {#image-profiles}

上傳影像時，您可以透過將影像描述檔套用至資料夾，在上傳時自動裁切影像。

>[!IMPORTANT]
>
>影像描述檔不適用於PDF、動畫GIF或INDD(Adobe InDesign)檔案。

## 裁切選項 {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

智慧型裁切座標取決於外觀比例。 對於影像設定檔中的智慧型裁切設定，如果影像設定檔中新增的維度的長寬比相同，則會將相同的長寬比傳送至Dynamic Media。 Adobe建議您使用相同的裁切區域。 這樣做可確保對影像設定檔中使用的不同維度沒有影響。

您建立的每個智慧型裁切產生都需要額外處理。 例如，新增超過五個智慧型裁切長寬比會導致資產擷取速度緩慢。 這也可能導致系統負載增加。 因為您可以在資料夾層級套用智慧型裁切，Adobe建議您只在需要的資料夾&#x200B;**&#x200B;上使用智慧型裁切。

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
   <td>僅根據維度大量裁切影像。</td>
   <td><p>要使用此選項，請從「裁切選項」下拉清單中選擇「<strong>像素裁切</strong>」。</p> <p>要從影像的兩側裁切，請輸入要從影像的任何一側或每一側裁切的像素數。 影像被裁切的程度取決於影像檔案中的ppi設定（每英吋像素）。</p> <p>影像輪廓像素裁切以下方式呈現：<br /> </p>
    <ul>
     <li>值為上、下、左、右。</li>
     <li>左上角被視為0,0，從那裡計算像素裁切。</li>
     <li>裁切起始點：左為X，上為Y</li>
     <li>水準計算：原始影像的水準像素大小減去「左」，然後減去「右」。</li>
     <li>垂直計算：垂直像素高度減去「頂部」，然後減去「底部」。</li>
    </ul> <p>例如，假設您有4000 x 3000像素影像。 您使用值：Top=250, Bottom=500, Left=300, Right=700。</p> <p>從左上角(300,250)使用填充空間(4000-300-700、3000-250-500或3000,2250)進行裁切。</p> </td>
  </tr>
  <tr>
   <td>智慧型裁切</td>
   <td>根據影像的視覺焦點來大量裁切影像。</td>
   <td><p>智慧型裁切運用Adobe Sensei中人工智慧的強大功能，大量快速自動裁切影像。 智慧型裁切功能會自動偵測任何影像中的焦點並裁切至焦點，以取得預期的興趣點（不論螢幕大小）。</p> <p>若要使用智慧型裁切，請從「裁切選項」下拉式清單中選取「<strong>智慧型裁切</strong>」，然後在「回應式影像裁切」的右側啟用（開啟）功能。</p> <p>預設斷點大小（大、中、小）涵蓋移動和平板電腦設備、台式機和橫幅上使用的大多數影像的全部大小。 如果需要，可以編輯「大」、「中」和「小」的預設名稱。</p> <p>要添加更多斷點，請選擇<strong>添加裁切</strong>;若要刪除裁切，請選取垃圾桶圖示。</p> </td>
  </tr>
  <tr>
   <td>顏色及影像樣本</td>
   <td>Bulk為每個影像生成一個影像色票。</td>
   <td><p><strong>注意</strong>:Dynamic Media Classic不支援智慧色票。</p> <p>從顯示顏色或紋理的產品影像自動定位並生成高質量色板。</p> <p>要使用「顏色」和「影像色板」，請從「裁切選項」下拉清單中選擇「<strong>智慧裁切</strong>」。 然後在「顏色」和「影像色票」的右側，啟用（開啟）功能。 在「寬度」和「高度」文本框中輸入像素值。</p> <p>雖然所有影像裁切都可從「轉譯」邊欄使用，但僅透過「複製URL」功能使用色票。 使用您自己的檢視元件，在您的網站上轉譯色票。 此規則的例外是輪播橫幅。 Dynamic Media提供輪播橫幅中所用色票的檢視元件。</p> <p><strong>使用影像色票</strong></p> <p>影像色票的URL非常直接：</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>其中<code>:Swatch</code>會附加至資產請求。</p> <p><strong>使用顏色色板</strong></p> <p>若要使用色票，請使用下列項目提出<code>req=userdata</code>請求：</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>例如，下列是Dynamic Media Classic中的色票資產：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>以下是色票資產的對應<code>req=userdata</code> URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p><code>req=userdata</code>回應如下：</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>您也可以要求XML或JSON格式的<code>req=userdata</code>回應，如下列個別URL範例所示：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## 不銳利化遮色片 {#unsharp-mask}

您可以使 **[!UICONTROL 用「銳利化遮色片]** 」來微調最終縮減取樣影像的銳利化濾鏡效果。您可以控制效果的強度、效果半徑（以像素計量），以及忽略的對比度臨界值。 此效果使用的選項與Adobe Photoshop的「遮色片銳利化」濾鏡相同。

>[!NOTE]
>
>不銳利化遮色片只會套用至縮減取樣超過50%的PTIFF（金字塔Tiff）內縮減縮放的轉譯。 這表示Ptiff中大小最大的轉譯不受遮色片銳利化影響。 而縮小的轉譯（例如縮圖）則會更改（並顯示不銳利化遮色片）。

在&#x200B;**[!UICONTROL 銳利化遮色片]**&#x200B;中，您有下列篩選選項：

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

[銳利化影像](/help/assets/dynamic-media/assets/sharpening_images.pdf)中會說明銳利化。

## 建立Dynamic Media影像設定檔 {#creating-image-profiles}

若要定義其他資產類型的進階處理參數，請參閱[設定資產處理](config-dm.md#configuring-asset-processing)。

請參閱[關於Dynamic Media影像設定檔和視訊設定檔](/help/assets/dynamic-media/about-image-video-profiles.md)。

另請參閱[組織數位資產以使用處理設定檔的最佳實務](/help/assets/dynamic-media/best-practices-for-file-management.md)。

**若要建立Dynamic Media影像設定檔：**

1. 選取Adobe Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**。
1. 若要新增影像設定檔，請選取&#x200B;**[!UICONTROL Create]**。
1. 輸入描述檔名稱和值，以用於遮色片、裁切或色票，或兩者。

   提示：使用符合其預定用途的設定檔名稱。 例如，假設您要建立僅產生色票的設定檔。 也就是說，智慧型裁切已停用（關閉），而顏色和影像色票已啟用（開啟）。 在這種情況下，您可以使用設定檔名稱「智慧色票」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options)[和遮色片銳利化](#unsharp-mask)。

   ![農作物](assets/crop.png)

1. 選擇&#x200B;**[!UICONTROL 保存]**。 新建立的配置檔案將顯示在可用配置檔案清單中。

## 編輯或刪除Dynamic Media影像設定檔 {#editing-or-deleting-image-profiles}

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**。
1. 選擇要編輯或刪除的影像配置檔案。 要編輯它，請選擇&#x200B;**[!UICONTROL 編輯影像處理配置檔案]**。 要刪除它，請選擇&#x200B;**[!UICONTROL 刪除影像處理配置檔案]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，則保存更改。 如果刪除，請確認您要移除設定檔。

## 將Dynamic Media影像設定檔套用至資料夾 {#applying-an-image-profile-to-folders}

將映像配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 因此，您只能將一個影像描述檔指派給資料夾。 因此，請仔細考慮上傳、儲存、使用和封存資產的資料夾結構。

如果為資料夾分配了不同的影像配置檔案，則新配置檔案將覆蓋前一個配置檔案。 先前的資料夾資產維持不變。 新設定檔會套用至稍後新增至資料夾的資產。

在使用者介面中會指出已指派給資料夾的資料夾，且資料夾的名稱會顯示在資訊卡中。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將影像設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理資料夾中的資產，該資料夾中已有您後來變更的現有影像設定檔。 請參閱[編輯資料夾的處理設定檔後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

### 將Dynamic Media影像設定檔套用至特定資料夾 {#applying-image-profiles-to-specific-folders}

您可以從&#x200B;**[!UICONTROL 工具]**&#x200B;菜單或在資料夾中從&#x200B;**[!UICONTROL 屬性]**&#x200B;將影像配置檔案應用到資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱[編輯資料夾的處理設定檔後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

#### 將Dynamic Media影像設定檔套用至設定檔使用者介面的資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**。
1. 選擇要應用於資料夾或多個資料夾的影像配置檔案。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選取&#x200B;**[!UICONTROL 將處理設定檔套用至資料夾]**，並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後選取&#x200B;**[!UICONTROL 套用]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從屬性將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 點選AEM標誌並導覽至「**[!UICONTROL 資產]**」。 然後導覽至您要套用影像設定檔之資料夾的父資料夾。
1. 在資料夾中，選擇複選標籤以選擇它，然後選擇&#x200B;**[!UICONTROL 屬性]**。
1. 選擇&#x200B;**[!UICONTROL Image Profiles]**&#x200B;頁簽。 從&#x200B;**[!UICONTROL 設定檔名稱]**&#x200B;下拉式清單中，選取設定檔，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全域套用Dynamic Media影像設定檔 {#applying-an-image-profile-globally}

除了將設定檔套用至資料夾之外，您也可以全域套用一個設定檔。 任何資料夾中上傳至「Experience Manager資產」的任何內容皆已套用選取的設定檔。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱[編輯資料夾的處理設定檔後，重新處理資料夾中的資產](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

**若要全域套用Dynamic Media影像設定檔：**

1. 執行下列任一操作：

   * 導覽至`https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`並套用適當的設定檔，然後選取&#x200B;**[!UICONTROL 儲存]**。

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 導覽至CRXDE Lite至下列節點：`/content/dam/jcr:content`。

      添加屬性`imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>`並選擇&#x200B;**[!UICONTROL 保存全部]**。

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單一影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

您可以手動重新對齊或調整影像的智慧型裁切視窗大小，以進一步細化其焦點。

編輯智慧型裁切並儲存後，變更會傳播至您對特定影像使用裁切的所有位置。

如有必要，您可以重新執行智慧型裁切，再次產生其他裁切。

另請參閱[編輯多個影像的智慧型裁切或智慧型色票](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**要編輯單個影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]**，然後導覽至套用智慧型裁切或智慧型色票影像描述檔的資料夾。
1. 要開啟其內容，請選擇資料夾。
1. 選擇要調整其智慧裁切或智慧色票的影像。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 智慧裁切]**。

1. 執行下列任一操作：

   * 在頁面的右上角附近，向左或向右拖動滑桿，分別增加或減少影像顯示。
   * 在影像上，拖動角手柄以調整裁切或色板的可視區域的大小。
   * 在影像上，將方塊/色票拖曳至新位置。 只能編輯影像色板；色票為靜態。
   * 在影像上方，選取&#x200B;**[!UICONTROL 還原]**&#x200B;以還原所有編輯內容並還原原始裁切或色票。
   * 使用鍵盤箭頭鍵裁切幀大小，或重新定位影像，或兩者。

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回資產資料夾。

## 編輯多個影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

將包含智慧型裁切的影像描述檔套用至資料夾後，該資料夾中的所有影像都會套用裁切至它們。 如果需要，可以手動&#x200B;*重新對齊或調整多個影像中的智慧型裁切窗口的大小，以進一步細化其焦點。*

編輯智慧型裁切並儲存後，變更會傳播至您對特定影像使用裁切的所有位置。

如有必要，您可以重新執行智慧型裁切，再次產生其他裁切。

**要編輯多個影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]**，然後導覽至套用智慧型裁切或智慧型色票影像描述檔的資料夾。
1. 在資料夾中，選擇&#x200B;**[!UICONTROL 更多操作]**(...)表徵圖，然後選擇&#x200B;**[!UICONTROL 智慧裁切]**。

1. 在&#x200B;**[!UICONTROL 編輯智慧作物]**&#x200B;頁面上，執行下列任一操作：

   * 調整頁面上影像的檢視大小。

      在斷點名稱下拉清單的右側，向左或向右拖動滑塊條，以更改可視影像顯示的大小。

      ![edit_smart_crobs-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據斷點名稱篩選可視影像清單。 在以下示例中，在斷點名稱「Medium」上篩選影像。

      在頁面的右上角附近，從下拉式清單中選取斷點名稱，以篩選您看到的影像。 （請參閱上圖）。

      ![edit_smart_crobs-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧型裁切框的大小。 執行下列任一操作：

      * 如果影像具有智慧型裁切或僅智慧型色票，請在影像上拖動裁切框的角手柄。 調整裁切的可視區域的大小。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上拖動裁切框的角手柄。 調整裁切的可視區域的大小。 或者，選取影像下方的智慧色板（顏色色板為靜態色板），然後拖動裁切框的角手柄。 調整色板的可視區域的大小。

      ![調整影像的智慧型裁切大小](assets/edit_smart_crops-resize.png)。

   * 移動智慧型裁切框。 執行下列任一操作：

      * 如果影像具有智慧型裁切或僅智慧型色票，請在影像上將裁切框拖曳至新位置。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上將智慧型裁切方塊拖曳至新位置。 或者，選取影像下方的智慧型色板（色板為靜態色板），然後將智慧型色板裁切框拖到新位置。

      ![edit_smart_crobs-move](assets/edit_smart_crops-move.png)

   * 還原所有編輯內容並還原原始的智慧型裁切或智慧型色票（僅適用於目前的編輯工作階段）。

      在影像上方選擇&#x200B;**[!UICONTROL 還原]**。

      ![edit_smart_robs_revert](assets/edit_smart_crops-revert.png)



1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回資產資料夾。

## 從資料夾中刪除映像配置檔案 {#removing-an-image-profile-from-folders}

從資料夾中移除影像配置檔案時，任何子資料夾都會自動從其父資料夾中繼承移除配置檔案。 不過，資料夾內發生的檔案處理仍維持不變。

您可以從&#x200B;**[!UICONTROL Tools]**&#x200B;菜單內的資料夾或在資料夾內的&#x200B;**[!UICONTROL Properties]**&#x200B;中刪除影像配置檔案。

### 透過Profiles使用者介面，從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**。
1. 選擇要從資料夾或多個資料夾中刪除的影像配置檔案。
1. 選擇&#x200B;**[!UICONTROL 從資料夾中刪除處理配置檔案]**&#x200B;並選擇要從中刪除配置檔案的資料夾或多個資料夾，然後選擇&#x200B;**[!UICONTROL 刪除]**。

   您可以確認「影像描述檔」不再套用至資料夾，因為名稱不再出現在資料夾名稱下方。

### 透過屬性從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後導覽至您要移除影像設定檔的資料夾。
1. 在資料夾中，選擇複選標籤以選擇它，然後選擇&#x200B;**[!UICONTROL 屬性]**。
1. 選擇&#x200B;**[!UICONTROL Image Profiles]**&#x200B;頁簽。
1. 從&#x200B;**[!UICONTROL 設定檔名稱]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 無]**，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
