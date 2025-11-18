---
title: 編輯影像
description: 使用  [!DNL Adobe Express]  支援的選項編輯影像，並將更新的影像另存新版。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 744c76f29a37610313835074f2f13fdd8f098465
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 75%

---

# 在 [!DNL Assets view] 中編輯影像 {#edit-images-in-assets-view}

資產檢視介面支援由 Adobe Express 驅動的基本影像編輯，整合於使用者介面中。 此編輯包括調整大小、背景移除、裁切以及 JPEG 和 PNG 格式之間的轉換。此外，還可透過嵌入資產檢視介面中的 Adobe Express 介面進行進階編輯。

編輯影像後，即可將新影像另存新版。版本設定功能有助於您稍後在必要時還原成原始資產。要編輯影像，[開啟其預覽](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets)，然後按一下「**編輯影像**」。

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 編輯 PNG 和 JPEG 檔案類型的影像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 編輯影像 {#edit-image}

進入資產檢視介面，使用連結 - [資產檢視](https://experience.adobe.com/#/assets) ，並選擇正確的儲存庫。 若要獲得存取權，請聯絡您組織的管理員。
如需更多參考資訊，請參閱「 [開始使用 Adobe Experience Manager 資產檢視](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view)」、「 [了解資產檢視使用者介面](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation)」及 [「資產檢視」的使用案例](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases)。
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### 使用 Adobe Express 編輯素材上的圖片 檢視 {#edit-image-on-assets-view-using-adobe-express}

進入資產檢視後，點選 **資產**，選取圖片，然後從上方欄杆點擊 **編輯** 。 新畫面會顯示 Adobe Express 支援的可用編輯選項，包括調整大小、背景移除、裁切，以及 JPEG 和 PNG 格式之間的轉換。

#### 調整影像大小 {#resize-image-using-express}

熱門的使用案例是將影像調整成特定大小。資產檢視功能讓你能快速調整圖片大小以符合常見照片尺寸，透過預先計算出特定照片尺寸的新解析度。 要使用 Assets View 調整圖片大小，請遵循以下步驟：

1. 按一下左窗格中的「**調整影像大小**」。對話框會顯示 Adob&#x200B;&#x200B;e Express 支援的調整影像大小功能。
1. 從「調整大小」下拉清單選取適當的社交媒體平台，然後從顯示的選項中選擇影像大小。
1. 如果需要，使用「**影像比例**」欄位來縮放影像。
1. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 進行影像編輯](assets/adobe-express-resize-image.png)

   您已編輯的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-resize-save.png)

#### 移除背景 {#remove-background-using-express}

您可以依照下方所述步驟移除影像中的背景：

1. 按一下左窗格中的&#x200B;**移除背景**。Experience Manager Assets 會顯示沒有背景的影像。
1. 按一下「**[!UICONTROL 套用]**」以套用您的變更。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-remove-background.png)

   您編輯的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。

#### 裁切影像 {#crop-image-using-express}

使用嵌入式 [!DNL Adobe Express] 快速動作可簡單地將影像轉換為完美大小。

1. 按一下左窗格中的&#x200B;**[!UICONTROL 裁切影像]**。
2. 拖曳影像角落上的控點，建立所要的裁切大小。
3. 按一下「**[!UICONTROL 套用]**」。
   ![使用 Adobe Express 儲存影像](assets/adobe-express-crop-image.png)
裁切後的影像可供下載。您可以將編輯後的資產另存為同一資產的新版本，也可以將其另存為新資產。

#### 將 JPEG 轉換為 PNG {#convert-image-types-using-express}

您可以使用 Adobe Express 在 JPEG 和 PNG 影像格式之間快速轉換。執行以下步驟：

1. 按一下左窗格中的&#x200B;**將 JPEG 轉換為 PNG** 或&#x200B;**將 PNG 轉換為 JPEG**。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. 按一下「**[!UICONTROL 下載]**」。

#### 限制 {#limitations-adobe-express}

* 支援的影像解析度：最小 - 每維度 50 像素，最大 - 每維度 6000 像素。
* 支援的檔案大小上限：17 MB。

### 在 Adobe Express 嵌入式編輯器中編輯影像 {#edit-images-in-adobe-express-embedded-editor}

擁有 Express 權限的使用者可從資產檢視中內嵌的 Express 編輯器輕鬆編輯內容並使用 Adobe Firefly 的 GenAI 創建新內容。 此功能會改善內容的重複使用，並加快建立內容的速度。您還可以使用預先定義的元素賦予資源令人驚嘆的效果，或者只需點擊幾下即可執行快速動作來編輯影像。

![Express in Essentials UI](/help/assets/assets/express-in-essentials-ui.jpg)
要使用嵌入編輯器編輯圖片 [!DNL Adobe Express] ，請依照以下步驟操作：

1. 請使用連結 - [AEM Assets View 進入 AEM 資產檢視](https://experience.adobe.com/#/assets) ，並選擇正確的儲存庫。
1. 按一下&#x200B;**資產**，進入資料夾，然後選取影像。
1. 按一下「**在 Adobe Express 中開啟**」。影像在 Express 畫布上開啟。
1. 對影像進行所需的編輯。
1. 如果您的專案需要新增更多頁面，按一下&#x200B;**新增**，選取「資產」，進入資料夾，選取要放入畫布頁面的影像，然後對影像進行所需的編輯。
1. 若要儲存一項或多項資產，請按一下「**儲存**」。儲存對話框會顯示儲存選項。若要在儲存選項之間選取，請按照以下符合您要求的說明進行操作：
   1. 若要儲存單次頁面，請按一下「**另存為新版本**」，將影像匯出為新版本 (保留原始格式)，並將其儲存在同一資料夾中。

   1. 若要儲存單次頁面，請按一下「**另存為新資產**」，將資產匯出為不同格式，並以新資產將其儲存至任何一個資料夾中。

   1. 若要儲存多個頁面中的單次頁面，按一下「**另存為新版本**」，以其原始格式和位置儲存該資產。

   1. 若要儲存多個頁面或多個頁面中的單次頁面，請按一下「**另存為新資產**」。此操作會將單一或多個資產匯出到任何資料夾中，並將這些儲存為新資產或原始或不同格式的資產。

1. 在「儲存」對話框中：
   1. 在&#x200B;**另存新檔**&#x200B;欄位中輸入檔案名稱。
   1. 選取目的地資料夾。
   1. 選擇性：提供專案或行銷活動名稱、關鍵字、管道、時間範圍和區域等詳細資訊。
1. 按一下&#x200B;**另存新版本**&#x200B;或&#x200B;**另存為新資產**&#x200B;以儲存資產。

#### 在 Express 編輯器中編輯影像的限制 {#limitations-of-editing-images-in-the-express-editor}

* 支援的檔案類型：JPEG 或 PNG。
* 支援的檔案大小上限：40 MB。
* 支援的寬度與高度範圍：65MP（例如 8K x 8K 或 16K x 4K）。
* 重新載入頁面即可查看來源資料夾中最新儲存的新資產。

### 使用 Adobe Express 建立新資產 {#create-new-embedded-editor}

[!DNL Assets view] 可讓您使用 [!DNL Adobe Express] 嵌入式編輯器從頭開始建立新範本。若要使用 [!DNL Adobe Express] 建立新資產，請執行以下步驟：

1. 進入 **[!UICONTROL 「我的工作區]** 」，在頂部顯示的 Adobe Express 橫幅中點擊 **[!UICONTROL 「建立]** 」。 [!DNL Adobe Express] 空白畫布會顯示在 [!DNL Assets view] 使用者介面中。
1. 使用「[範本](https://helpx.adobe.com/tw/express/using/work-with-templates.html)」建立您的內容。否則，請瀏覽至「**[!UICONTROL 您的資料]**」以修改現有內容。
1. 完成編輯後，按一下「**[!UICONTROL 儲存]**」。
1. 指定所建立資產的目的地路徑，然後點選 **[!UICONTROL 「另存為新資產]**」。

#### 限制 {#limitations}

* 您只能修改 `JPEG` 和 `PNG` 格式類型的影像。
* 資產大小必須少於桌面裝置的 80 MB，行動裝置則須少於 40 MB。
* 支援的寬度與高度範圍介於 50 至 8000 像素之間。
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

* 請使用 [!UICONTROL 資產檢視使用者介面中的回饋] 選項提供產品回饋。

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)。

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Adobe Express 快速操作](https://helpx.adobe.com/tw/express/using/resize-image.html)
>* [檢視資產的版本記錄](navigate-assets-view.md)
