---
title: 編輯影像
description: 使用  [!DNL Adobe Photoshop Express]  支援的選項編輯影像，並將更新的影像另存新版。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
source-git-commit: 1147fa8069fc065aed01c75db686cfefee269319
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 80%

---

# 在 [!DNL Assets view] 中編輯影像 {#edit-images}

[!DNL Assets view] 提供 [!DNL Adobe Express] 和 [!DNL Adobe Photoshop Express] 所支援的人性化編輯選項。 可用的編輯動作，使用 [!DNL Adobe Express] 是「調整影像大小」、「移除背景」、「裁切影像」和「將JPEG轉換為PNG」，反之亦然。

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

* 支援的影像解析度：最小 - 50 像素，最大 - 每維度 6000 像素

* 支援的檔案大小上限：17 MB

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


## 使用 [!DNL Adobe Photoshop Express] 編輯影像 {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->

### 修飾影像 {#spot-heal-images-using-photoshop-express}

如果影像上出現細微污點或小型物件，您可以使用 Adobe Photoshop 提供的污點修復功能編輯和移除污點。

筆刷會取樣修飾過的區域，然後將修復的像素完美融入影像的其餘部份。請使用只比您要修復的污點稍大的筆刷大小。

![污點修復編輯選項](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->

### 裁切和拉直影像 {#crop-straighten-images-using-photoshop-express}

您可以使用裁切和拉直選項進行基本的裁切、旋轉影像、水平或垂直翻轉影像，以及將影像裁切成適用於熱門社交媒體網站的尺寸。

若要儲存您的編輯，請按一下&#x200B;**[!UICONTROL 裁切影像]**。編輯後，即可將新影像另存新版。

![裁切和拉直影像的選項](assets/edit-crop-straighten.png)

許多預設選項可讓您將影像裁切成適合各種社交媒體基本資料的最佳比例。

### 調整影像大小 {#resize-image-using-photoshop-express}

您可以用公分或英吋檢視常見的相片大小，以知道尺寸大小。依照預設，調整大小方法仍會保持長寬比。若要手動覆寫長寬比，請按一下「![](assets/do-not-localize/lock-closed-icon.png)」。

請輸入尺寸，然後按一下&#x200B;**[!UICONTROL 調整影像大小]**&#x200B;即可調整影像大小。將變更另存為新版本前，您可以按一下[!UICONTROL 還原]以在儲存前復原所有變更，或按一下[!UICONTROL  回復]以變更編輯流程中的特定步驟。

![調整影像大小時的選項](assets/resize-image.png)

### 調整影像 {#adjust-image-using-photoshop-express}

[!DNL Assets view] 可讓您按幾下滑鼠，即可調整顏色、色調、對比等等。在編輯視窗中，按一下&#x200B;**[!UICONTROL 調整影像]**。在右側邊欄中有以下選項：

* **熱門**：[!UICONTROL 高對比度和細節]、[!UICONTROL 減少飽和對比度]、[!UICONTROL 陳年相片]、[!UICONTROL 黑白柔焦]以及[!UICONTROL 黑白墨色調]。
* **顏色**：[!UICONTROL 自然]、[!UICONTROL 明亮]、[!UICONTROL 高對比度]、[!UICONTROL 高對比度和細節]、[!UICONTROL 鮮豔]以及[!UICONTROL 霧面]。
* **創意**：[!UICONTROL 減少飽和對比度]、[!UICONTROL 冷光]、[!UICONTROL 藍綠色和紅色]、[!UICONTROL 柔霧]、[!UICONTROL 復古即時]、[!UICONTROL 暖對比度]、[!UICONTROL 單調和綠色]、[!UICONTROL 紅色霧面]、[!UICONTROL 溫暖陰影]以及[!UICONTROL 陳年相片]。
* **黑白**：[!UICONTROL 黑白景觀]、[!UICONTROL 黑白高對比度]、[!UICONTROL 黑白力量]、[!UICONTROL 黑白低對比度]、[!UICONTROL 黑白單調]、[!UICONTROL 黑白柔焦]、[!UICONTROL 黑白紅外線]、[!UICONTROL 黑白硒色調]、[!UICONTROL 黑白墨色調]以及[!UICONTROL 黑白分割色調]。
* **周邊暗角**：[!UICONTROL 無]、[!UICONTROL 輕度]、[!UICONTROL 中度]以及[!UICONTROL 重度]。

![透過編輯調整影像](assets/adjust-image.png)

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
