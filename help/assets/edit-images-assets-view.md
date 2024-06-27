---
title: 編輯影像
description: 使用  [!DNL Adobe Express]  支援的選項編輯影像，並將更新的影像另存新版。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 9a21c9218e45bb6ce91263c9798e3b1c99f369b4
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 33%

---

# 在 [!DNL Assets view] 中編輯影像 {#edit-images-in-assets-view}

「資產檢視」可啟用基本的影像編輯，包括調整大小、移除背景、裁切，以及在JPEG和PNG格式之間轉換。 此外，透過與Adobe Express整合，還可進行進階編輯。 編輯影像後，即可將新影像另存新版。版本設定功能可協助您稍後在需要時還原成原始資產。 要編輯影像，[開啟其預覽](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets)，然後按一下「**編輯影像**」。

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 編輯 PNG 和 JPEG 檔案類型的影像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 編輯影像 {#edit-image}

登陸資產檢視，使用連結 —  [資產檢視](https://experience.adobe.com/#/assets) 並選取正確的存放庫。 若要獲得存取權，請聯絡您組織的管理員。
如需其他參考資訊，請參閱 —  [開始使用Adobe Experience Manager Assets檢視](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view)， [瞭解Assets檢視使用者介面](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation)、和 [Assets檢視使用案例](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### 在Assets檢視上使用Adobe Express編輯影像 {#edit-image-on-assets-view-using-adobe-express}

登入Assets檢視後，按一下 **Assets**，選取影像，然後按一下 **編輯** 從頂端邊欄。 新畫面會顯示可用的編輯選項，包括調整大小、移除背景、裁切以及JPEG和PNG格式之間的轉換。

#### 調整影像大小 {#resize-image-using-express}

熱門的使用案例是將影像調整成特定大小。Assets View可針對特定像片大小提供預先計算好的新解析度，讓您快速調整影像大小以符合常見的像片大小。 若要使用Assets檢視調整影像大小，請遵循下列步驟：

1. 按一下 **調整影像大小** 從左窗格。
1. 從「調整大小」下拉式清單中選取適當的社群媒體平台，然後從顯示的選項中選取影像大小。
1. 如果需要，使用「**影像比例**」欄位來縮放影像。
1. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 進行影像編輯](assets/adobe-express-resize-image.png)

   您已編輯的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-resize-save.png)

#### 移除背景 {#remove-background-using-express}

您可以依照下列步驟移除影像的背景：

1. 按一下 **移除背景** 從左窗格。 Experience Manager Assets 會顯示沒有背景的影像。
1. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-remove-background.png)

   您編輯的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。

#### 裁切影像 {#crop-image-using-express}

將影像轉換為完美大小非常簡單，只需使用內嵌 [!DNL Adobe Express] 快速動作。

1. 按一下 **[!UICONTROL 裁切影像]** 從左窗格。
2. 拖曳影像角落上的控點，建立所要的裁切大小。
3. 按一下「**[!UICONTROL 套用]**」。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-crop-image.png)
裁切後的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。

#### 在影像檔案型別之間轉換 {#convert-image-types-using-express}

您可以使用Adobe Express快速在JPEG和PNG影像格式之間轉換。 執行以下步驟：

1. 按一下 **JPEG至PNG** 或 **PNG至JPEG** 從左窗格。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. 按一下「**[!UICONTROL 下載]**」。

#### 限制 {#limitations-adobe-express}

* 支援的影像解析度：最小 - 每維度 50 像素，最大 - 每維度 6000 像素。

* 支援的檔案大小上限：17 MB。

### 在Adobe Express內嵌編輯器中編輯影像 {#edit-images-in-adobe-express-embedded-editor}

擁有Express許可權的使用者可以使用Assets檢視中的內嵌式Express編輯器，從Adobe Firefly輕鬆編輯內容並使用GenAI建立新內容。 這麼做可改善內容重複使用率，並加快內容速度。 您也可以使用預先定義的元素，讓您的資產看起來令人驚豔，或執行快速動作，只要按幾下即可編輯您的影像。
![在Essentials UI中快取](/help/assets/assets/express-in-essentials-ui.jpg)
若要使用編輯影像 [!DNL Adobe Express] 內嵌編輯器，請遵循下列步驟：

1. 使用連結登陸AEM Assets檢視 —  [AEM資產檢視](https://experience.adobe.com/#/assets) 並選取正確的存放庫。
1. 按一下 **Assets**，輸入資料夾，然後選取影像。
1. 按一下 **以Adobe Express開啟**. 影像會在快速畫布上開啟。
1. 對影像進行必要的編輯。
1. 如果您的專案需要您新增更多頁面，請按一下 **新增**，選取「Assets」，輸入資料夾，選取要帶入畫布頁面的影像，然後對影像執行所需的編輯。
1. 若要儲存影像，請按一下 **儲存**. 儲存對話方塊隨即顯示。

   >[!NOTE]
   >
   > **1. 針對單頁**
   >
   > **另存為版本：** 此功能僅支援儲存單一資產。 選取此選項可將影像匯出為新版本（保留原始格式），並將它儲存在相同的資料夾中。
   > **另存為新資產：** 選取此選項可將資產以與原始資產不同的格式匯出，並將其另存至任何資料夾中作為新資產。
   >  
   > **2. 針對多頁**
   >
   > **另存為版本：** 此功能僅支援儲存單一資產。 如果您想要從多個頁面儲存單一頁面，請選取此選項，以資產的原始格式和位置儲存資產。\
   > **另存為新資產：** 透過此選項，您可以將多個資產或單一資產匯出至任何檔案夾，並將它們儲存為新資產，其檔案格式為原始檔案或不同檔案。

1. 在「儲存」對話方塊中：
   1. 在中輸入檔案的名稱 **另存為** 欄位。
   1. 選取目的地資料夾。
   1. 可選：提供專案或行銷活動名稱、關鍵字、管道、時間範圍和區域等詳細資訊。
1. 按一下 **另存為版本** 或 **另存為新資產** 以儲存資產。

#### 在快速編輯器中編輯影像的限制 {#limitations-of-editing-images-in-the-express-editor}

* 支援的檔案型別：JPEG或PNG。
* 支援的檔案大小上限：40 MB。
* 支援的寬度和高度範圍：介於50到8000畫素之間。
* 重新載入頁面，以檢視來源資料夾中最新儲存的新資產。

### 使用 Adobe Express 建立新資產 {#create-new-embedded-editor}

[!DNL Assets view] 可讓您使用 [!DNL Adobe Express] 嵌入式編輯器從頭開始建立新範本。若要使用 [!DNL Adobe Express] 建立新資產，請執行以下步驟：

1. 瀏覽至 **[!UICONTROL 我的Workspace]** 並按一下 **[!UICONTROL 建立]** 顯示在頂端的Adobe Express橫幅內。 [!DNL Adobe Express] 空白畫布會顯示在 [!DNL Assets view] 使用者介面中。
1. 使用「[範本](https://helpx.adobe.com/tw/express/using/work-with-templates.html)」建立您的內容。否則，請瀏覽至「**[!UICONTROL 您的資料]**」以修改現有內容。
1. 完成編輯後，請按一下 **[!UICONTROL 儲存]**.
1. 指定已建立資產的目的地路徑，然後按一下 **[!UICONTROL 另存為新資產]**.

#### 限制 {#limitations}

* 您只能修改 `JPEG` 和 `PNG` 格式類型的影像。
* 資產大小必須小於 40 MB。
* 您可以將影像儲存為 `PDF`、`JPEG` 或 `PNG` 格式。

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### 後續步驟 {#next-steps}

* 使用提供產品意見回饋 [!UICONTROL 意見反應] Assets檢視使用者介面提供的選項。

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Adobe Express中的快速動作](https://helpx.adobe.com/tw/express/using/resize-image.html)
>* [檢視資產的版本記錄](navigate-assets-view.md)
