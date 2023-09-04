---
title: 編輯影像
description: 使用  [!DNL Adobe Photoshop Express]  支援的選項編輯影像，並將更新的影像另存新版。
role: User
exl-id: fc21a6ee-bf23-4dbf-86b0-74695a315b2a
source-git-commit: 30b8c9b8eaee6292323dde4b436c29fe8290c910
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 54%

---

# 在 [!DNL Assets view] 中編輯影像 {#edit-images}

[!DNL Assets view] 提供簡單易用的編輯選項，由 [!DNL Adobe Express] 和 [!DNL Adobe Photoshop Express]. 可用的編輯動作，使用 [!DNL Adobe Express] 包括「調整影像大小」、「移除背景」、「裁切影像」和「將JPEG轉換為PNG」。

編輯影像後，即可將新影像另存新版。版本設定功能有助於您稍後在必要時還原成原始資產。若要編輯影像， [開啟其預覽](/help/assets/navigate-assets-view.md) 並按一下 **[!UICONTROL 編輯影像]**.

>[!NOTE]
>
>您可以使用編輯PNG影像和JPEG檔案型別 [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 使用Adobe Express編輯影像 {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express 整合"
>abstract="簡單直觀的影像編輯工具是由 Adobe Express 提供支援，可直接在 AEM Assets 中使用；此工具可增加內容重複使用性並加快內容流通速度。"

### 調整影像大小 {#resize-image-using-express}

熱門的使用案例是將影像調整成特定大小。[!DNL Assets view] 可讓您快速調整影像大小，為特定相片大小提供預先計算好的新解析度，以符合常見的相片大小。若要使用調整影像大小 [!DNL Assets view]，請遵循下列步驟：

1. 選取影像並按一下 **編輯**.
2. 按一下 **[!DNL Resize Image]** 從左側窗格中可用的快速動作。
3. 從中選擇適當的社群媒體平台 **[!UICONTROL 調整大小]** 下拉式清單，並從顯示的選項中選取影像大小。
4. 如有必要，請使用 **[!UICONTROL 影像比例]** 欄位。
5. 按一下 **[!DNL Apply]** 以套用您的變更。
   ![使用Adobe Express編輯影像](assets/adobe-express-resize-image.png)

   您編輯的影像可供下載。 您可以將編輯後的資產儲存為相同資產的新版本，或儲存為新資產。
   ![以Adobe Express儲存影像](assets/adobe-express-resize-save.png)

### 移除背景 {#remove-background-using-express}

您只需要幾個簡單的步驟，就可以移除影像的背景，如下所述：

1. 選取影像並按一下 **編輯**.
2. 按一下 **[!DNL Remove Background]** 從左側窗格中可用的快速動作。 Experience Manager Assets會顯示沒有背景的影像。
3. 按一下 **[!DNL Apply]** 以套用您的變更。
   ![以Adobe Express儲存影像](assets/adobe-express-remove-background.png)

   您編輯的影像可供下載。 您可以將編輯後的資產儲存為相同資產的新版本，或儲存為新資產。

### 裁切影像 {#crop-image-using-express}

使用內嵌技術，輕鬆將影像轉換為完美大小 [!DNL Adobe Express] 快速動作。

1. 選取影像並按一下 **編輯**.
2. 按一下 **[!DNL Crop Image]** 從左側窗格中可用的快速動作。
3. 拖曳影像邊角的操作框以建立您想要的裁切。
4. 按一下 **[!DNL Apply]**.
   ![以Adobe Express儲存影像](assets/adobe-express-crop-image.png)
裁切的影像可供下載。 您可以將編輯後的資產儲存為相同資產的新版本，或儲存為新資產。

### 將JPEG轉換為PNG {#convert-jpeg-to-png-using-express}

您可以使用Adobe Express快速將JPEG影像轉換為PNG格式。 執行以下步驟：

1. 選取影像並按一下 **編輯**.
2. 按一下 **[!DNL JPEG to PNG]** 從左側窗格中可用的快速動作。
   ![轉換成PNG並加上Adobe Express](assets/adobe-express-convert-image.png)
3. 按一下&#x200B;**[!UICONTROL 下載]**。

### 限制 {#limitations-adobe-express}

* 支援的影像解析度：最小值 — 50畫素，最大值 — 6000畫素/維度

* 支援的檔案大小上限： 17MB

## 編輯影像，使用 [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](//help/navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->

### 污點修復影像 {#spot-heal-images-using-photoshop-express}

如果影像上出現細微污點或小型物件，您可以使用 Adobe Photoshop 提供的污點修復功能編輯和移除污點。

筆刷會取樣修飾過的區域，然後將修復的像素完美融入影像的其餘部份。請使用只比您要修復的污點稍大的筆刷大小。

![污點修復編輯選項](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->

### 裁切和拉直影像 {#crop-straighten-images-using-photoshop-express}

使用裁切和拉直選項，您就能執行基本的裁切、旋轉影像、水平或垂直翻轉影像，以及將影像裁切成適合熱門社群媒體網站的尺寸。

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

* 連絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [檢視資產的版本記錄](/help/assets/navigate-assets-view.md)
