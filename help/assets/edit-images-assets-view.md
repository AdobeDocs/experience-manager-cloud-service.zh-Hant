---
title: 編輯影像
description: 使用  [!DNL Adobe Express]  支援的選項編輯影像，並將更新的影像另存新版。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
source-git-commit: 42d3751a4a29149f3b31dbc28555b81aa7ed43cc
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 70%

---

# 在 [!DNL Assets view] 中編輯影像 {#edit-images}

[!DNL Assets view] 提供 [!DNL Adobe Express] 所支援的人性化編輯選項。可用的編輯動作，使用 [!DNL Adobe Express] 是「調整影像大小」、「移除背景」、「裁切影像」和「將JPEG轉換為PNG」，反之亦然。

編輯影像後，即可將新影像另存新版。版本設定功能有助於您稍後在必要時還原成原始資產。此外，版本設定僅適用於PNG檔案型別，這表示當您嘗試從JPG檔案型別移除背景時，JPG會自動轉換為PNG。 要編輯影像，[開啟其預覽](navigate-assets-view.md)，然後按一下「**[!UICONTROL 編輯影像]**」。

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 編輯 PNG 和 JPEG 檔案類型的影像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 使用 Adobe Express 編輯影像 {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express 整合"
>abstract="簡單直觀的影像編輯工具是由 Adobe Express 提供支援，可直接在 AEM Assets 中使用；此工具可增加內容重複使用性並加快內容流通速度。"

### 調整影像大小 {#resize-image-using-express}

熱門的使用案例是將影像調整成特定大小。[!DNL Assets view] 可讓您快速調整影像大小，為特定相片大小提供預先計算好的新解析度，以符合常見的相片大小。若要使用 [!DNL Assets view] 調整影像大小，請按照以下步驟動作：

1. 從中選擇影像 [!DNL Experience Manager] 資產存放庫並按一下 **編輯**.
2. 從左窗格中可用的快速動作中，按一下「**[!UICONTROL 調整影像大小]**」。
3. 從「**[!UICONTROL 調整大小的內容]**」下拉清單選取適當的社交媒體平台，然後從顯示的選項中選取影像大小。
4. 如果需要，使用「**[!UICONTROL 影像比例]**」欄位來縮放影像。
5. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 進行影像編輯](assets/adobe-express-resize-image.png)

   您已編輯的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-resize-save.png)

### 移除背景 {#remove-background-using-express}

您可以透過幾個簡單的步驟從影像中移除背景，如下所述：

1. 從中選擇影像 [!DNL Experience Manager] 資產存放庫並按一下 **編輯**.
2. 從左窗格中可用的快速動作中，按一下「**[!UICONTROL 移除背景]**」。 Experience Manager Assets 會顯示沒有背景的影像。
3. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-remove-background.png)

### 裁切影像 {#crop-image-using-express}

使用嵌入式 [!DNL Adobe Express] 快速動作可輕鬆將影像轉換為完美大小。

1. 從中選擇影像 [!DNL Experience Manager] 資產存放庫並按一下 **編輯**.
2. 從左窗格中可用的快速動作中，按一下「**[!UICONTROL 裁切影像]**」。
3. 拖曳影像角落上的控點，建立所要的裁切大小。
4. 按一下「**[!UICONTROL 套用]**」。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-crop-image.png)
裁切後的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。

### 將 JPEG 轉換為 PNG {#convert-jpeg-to-png-using-express}

您可以使用 Adobe Express 將 JPEG 影像快速轉換為 PNG 格式。 執行以下步驟：

1. 從中選擇影像 [!DNL Experience Manager] 資產存放庫並按一下 **編輯**.
2. 按一下 **[!UICONTROL 轉換為PNG]** 從左側窗格中可用的快速動作。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. 按一下「**[!UICONTROL 套用]**」。
4. 瀏覽至 **[!UICONTROL 另存新檔在右上方]** 並按一下 **[!UICONTROL 另存為新資產]**.

### 將PNG轉換為JPEG {#convert-png-to-jpeg-using-express}

您可以使用Adobe Express快速將PNG影像轉換為JPEG格式。 執行以下步驟：

1. 從中選擇影像 [!DNL Experience Manager] 資產存放庫並按一下 **編輯**.
2. 按一下 **[!UICONTROL 轉換為JPEG]** 從左側窗格中可用的快速動作。
3. 按一下「**[!UICONTROL 套用]**」。
4. 瀏覽至 **[!UICONTROL 另存新檔在右上方]** 並按一下 **[!UICONTROL 另存為新資產]**.

### 限制 {#limitations-adobe-express}

* 支援的影像解析度：最小 — 50畫素，最大 — 6000畫素/維度。

* 支援的檔案大小上限： 17 MB。

## 使用 Adobe Express 嵌入式編輯器編輯影像 {#edit-using-embedded-editor}

有權存取Adobe Express的組織可以使用整合式影像編輯和建立工具，從資產檢視中直接取得的Adobe Express和Adobe Firefly改善內容重複使用和加快內容速度。 您還可以使用預先定義的元素賦予資源令人驚嘆的效果，或者只需點擊幾下即可執行快速動作來編輯影像。

若要使用 [!DNL Adobe Express] 嵌入式編輯器編輯影像，請依照下列步驟進行：

1. 從您的 [!DNL Experience Manager] 資產存放庫中選取一個影像。
1. 按一下「**[!UICONTROL 在 Adobe Express 中開啟]**」。

   ![Adobe Express 嵌入式編輯器](assets/embedded-editor.png)

   您可以利用 [!DNL Adobe Express] 的功能來執行所有與影像編輯相關的動作，例如「[調整影像大小](https://helpx.adobe.com/tw/express/using/resize-image.html)」、「[移除或變更背景顏色](https://helpx.adobe.com/tw/express/using/remove-background.html)」、「[裁切影像](https://helpx.adobe.com/tw/express/using/crop-image.html)」等。

1. 完成影像編輯後，您可以將資產下載為新資產或將資產另存為新版本。

## 使用 Adobe Express 建立新資產 {#create-new-embedded-editor}

[!DNL Assets view] 可讓您使用 [!DNL Adobe Express] 嵌入式編輯器從頭開始建立新範本。若要使用 [!DNL Adobe Express] 建立新資產，請執行以下步驟：

1. 瀏覽至 **[!UICONTROL 我的工作區]** 並按一下 **[!UICONTROL 建立]** 顯示在頂端的Adobe Express橫幅內。 [!DNL Adobe Express] 空白畫布會顯示在 [!DNL Assets view] 使用者介面中。
1. 使用「[範本](https://helpx.adobe.com/tw/express/using/work-with-templates.html)」建立您的內容。否則，請瀏覽至「**[!UICONTROL 您的資料]**」以修改現有內容。
1. 完成編輯後，按一下「**[!UICONTROL 另存為新資產]**」。
1. 指定已建立資產的目標路徑，然後按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>* 您只能修改 `JPEG` 和 `PNG` 格式類型的影像。
>* 資產大小必須小於 17 MB。
>* 您可以將影像儲存在 `PDF`， `JPEG`，或 `PNG` 格式；而如果有多個頁面，您可以將其儲存為 `PDF`.

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

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Adobe Express中的快速動作](https://helpx.adobe.com/tw/express/using/resize-image.html)
>* [檢視資產的版本記錄](navigate-assets-view.md)
