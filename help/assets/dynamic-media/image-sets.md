---
title: 影像集
description: 瞭解如何在Dynamic Media處理影像集。
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: b31fa5af7bcaa944d8bd7b0bb7d7b8deb36906a8
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 5%

---

# 影像集 {#image-sets}

「影像集」為用戶提供了整合的查看體驗，用戶可以通過按一下縮略圖來查看項目的不同視圖。 「影像集」(Image Sets)允許您顯示項目的替代視圖，而查看器提供了縮放工具，用於仔細檢查影像。

影像集由具有單字的橫幅指定 `IMAGESET`。此外，如果已發佈映像集，則發佈日期由 **[!UICONTROL 世界]** 表徵圖。 另外，由 **[!UICONTROL 鉛筆]** 的上界。

![chlimage_1-133](assets/chlimage_1-339.png)

在影像集中，還可以通過建立影像集和添加縮略圖來建立色板。

當您希望以不同顏色、圖案或完成顯示項目時，此應用程式非常有用。 要使用顏色色板建立影像集，您需要為要向用戶呈現的每種不同顏色、圖案或完成一幅影像。 每種顏色、圖案或光潔度還需要一個顏色、圖案或光潔度色板。

例如，假設您要顯示具有不同顏色鈔票的大寫影像；賬單是紅的，綠的，藍的。 在這個例子中，你需要三針相同的帽子。 你需要一張紅的，一張綠的，一張藍的。 還需要紅色、綠色和藍色色板。 顏色色板用作縮略圖，用戶在「色板集查看器」中按一下該縮略圖，以查看紅色開單、綠色開單或藍色開單的帽。

>[!NOTE]
>
>有關Assets用戶介面的資訊，請參閱 [使用Touch UI管理資產](/help/assets/manage-digital-assets.md)。

## 快速啟動：影像集 {#quick-start-image-sets}

要快速啟動並運行：

1. 選填。[建立批集預設](/help/assets/dynamic-media/batch-set-presets-dm.md) 並將其應用到上載旋轉集映像的新資料夾。

   批處理集預設可幫助您自動建立映像集。

   >[!IMPORTANT]
   >
   >批集由IPS（映像生產系統）建立，作為資產接收的一部分。

1. [上載多個視圖的主源映像](#uploading-assets-in-image-sets)。

   上載映像集的映像。 請記住，用戶可以在「影像集查看器」中放大影像。 因此，請仔細選擇您的影像。 確保影像在最大大小中至少為2000像素。

   請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 影像集支援的格式清單。

1. [建立映像集](#creating-image-sets)。

   在「影像集」中，用戶按一下「影像集查看器」中的縮略圖。

   要在資產中建立映像集，請選擇 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]**。 然後，添加影像，然後按一下 **[!UICONTROL 保存]**。

   請參閱 [準備映像集資產以上載和上載檔案](#uploading-assets-in-image-sets)。

   請參閱 [使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 添加 [影像集查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)，根據需要。

   管理員可以建立或修改「影像集查看器預設」。 要使用查看器預設查看影像集，請選擇影像集，然後在左欄下拉清單中，選擇 **[!UICONTROL 查看者]**。

   要建立或編輯查看器預設，請參閱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 查看器預設]**。

1. （可選） [查看影像集](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) 是使用批集預設建立的。
1. [預覽影像集](/help/assets/dynamic-media/previewing-assets.md)。

   選擇「影像集」(Image Set)，您可以預覽它。 要在選定的查看器中檢查影像集，請選擇縮略圖表徵圖。 您可以從 **[!UICONTROL 查看者]** 的子菜單。

1. [發佈映像集](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

   發佈影像集將激活URL和嵌入字串。 此外，您必須 [發佈任何自定義查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md) 你創造的。 已發佈現成查看器預設。

1. [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 或 [嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。

   Experience Manager Assets會建立映像集的URL調用，並在您發佈映像集後激活它們。 您可以在預覽資產時複製這些URL。 或者，您可以將它們嵌入到您的網站上。

   選擇「影像集」，然後在左滑軌下拉清單中選擇 **[!UICONTROL 查看者]**。

   請參閱 [將影像集連結到網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 和 [嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。

要編輯映像集，請參閱 [編輯影像集](#editing-image-sets)。 此外，您還可以查看和編輯 [影像集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

如果建立集時遇到問題，請參閱中的影像和集 [排除Dynamic Media故障](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets)。

## 上載映像集的資產 {#uploading-assets-in-image-sets}

首先上載映像集的映像資產。 請記住，用戶可以在「影像集查看器」中放大影像。 因此，請仔細選擇您的影像。 確保影像大小為2000像素，以便獲得最佳縮放細節。 Dynamic Media可以每張2500萬像素的影像。 例如，您可以使用5000x5000兆像素影像或任何其他大小的組合，最多2500萬像素。

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 影像集支援的格式清單。

可以像您一樣上載映像集的映像 [上載資產中的任何其他資產](/help/assets/manage-digital-assets.md#uploading-assets)。

### 準備映像集資產以供上載 {#preparing-image-set-assets-for-upload}

在建立映像集之前，請確保映像的大小和格式正確。

要建立多視圖影像集，需要顯示來自不同視點的項目或顯示同一項目不同方面的影像。 其目標是突出顯示項目的重要功能，以便查看者能夠完整瞭解項目的顯示方式或功能。

因為用戶可以在影像集中縮放影像，所以請確保影像在最大大小中至少為2000像素。 Experience Manager Assets支援多種影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

>[!NOTE]
>
>如果使用縮略圖來指示產品色板，請執行以下操作：
>
>建立同一影像的小圖或不同的鏡頭，以不同的顏色、圖案或結束顯示影像。 您還需要與不同顏色、圖案或結束相對應的縮略圖檔案。 例如，要顯示縮略圖，並且影像集以黑色、棕色和綠色顯示同一夾克，您需要：
>
>* 同一件夾克的黑色，棕色和綠色。
>* 黑色、棕色和綠色縮略圖。


## 建立映像集 {#creating-image-sets}

可通過用戶介面或通過API建立映像集。

>[!NOTE]
>
>還可以通過 [批集預設](/help/assets/dynamic-media/batch-set-presets-dm.md)。
>**** 重要：批集由IPS(Image Production System)建立，作為資產提取的一部分。

在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或對其排序。

>[!NOTE]
>
>檔案名中具有「，」（逗號）的資產不支援映像集。

**要建立映像集：**

1. 在Adobe Experience Manager，選擇Experience Manager徽標以訪問全局導航控制台。
1. 點擊 **[!UICONTROL 導航]** > **[!UICONTROL 資產]**。 導航到要建立影像集的位置，然後轉到 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]** 開啟「影像集編輯器」頁。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5映像集 — 建立下拉](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁中， **[!UICONTROL 標題]** 欄位，輸入影像集的名稱。 該名稱出現在影像集的標題中。 （可選）輸入說明。

   ![6_5 — 映像集建立新集](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一操作：

   * 在「影像集編輯器」頁的左上角附近，選擇 **[!UICONTROL 添加資產]**。

   * 在「影像集編輯器」頁面的中間，選擇 **[!UICONTROL 點擊以開啟資產選擇器]**。
   點擊以選擇要包括在映像集中的資產。 選定資產上面有複選標籤表徵圖。 完成後，在頁面右上角附近，選擇 **[!UICONTROL 選擇]**。

   使用資產選擇器，可以通過鍵入關鍵字並選擇 **[!UICONTROL 返回]**。 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後選擇 **[!UICONTROL 篩選]** 的子菜單。 通過選擇「視圖」表徵圖並選擇 **[!UICONTROL 列視圖]**。 **[!UICONTROL 卡視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**。

   請參閱 [使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或排序。

   如有必要，將資產的「重新排序」表徵圖拖到資產檔案名的右側，以在設定清單上或下重新排序影像。

   ![6_5映像集 — 重新排序資產](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請按一 **下影像旁** 的+ **縮圖** 圖示，並導覽至您想要的縮圖或色票。選取完所有影像後，按一下「 **[!UICONTROL 儲存]**」。

1. （可選）執行下列任一操作：

   * 要刪除影像，請選擇影像並選擇 **[!UICONTROL 刪除資產]**。

   * 要應用預設，請選擇靠近頁面右上角的 **[!UICONTROL 預設]**，然後選擇一個預設以立即應用於所有資產。
   >[!NOTE]
   >
   >建立影像集時，可以更改影像集縮略圖。 或者，您可以讓Experience Manager根據影像集中的資產自動選擇縮略圖。 要選擇縮略圖，請選擇 **[!UICONTROL 更改縮略圖]** 影像集編輯器頁面上的「標題」欄位上方。 然後，選擇任何影像（您也可以導航到其他資料夾以查找影像）。 如果選擇了縮略圖，則決定要Experience Manager從影像集生成縮略圖，請選擇 **[!UICONTROL 切換到]** **[!UICONTROL 自動縮略圖]**。

1. 按一下「**[!UICONTROL 儲存]**」。您新建立的映像集將顯示在您建立的資料夾中。

## 查看影像集 {#viewing-image-sets}

可以在用戶介面中建立影像集或自動使用 [批集預設](/help/assets/dynamic-media/batch-set-presets-dm.md)。

>[!IMPORTANT]
>
>批集由IPS建立 [影像生成系統] 作為資產消化的一部分。

但是，使用批集預設建立的集，請執行 *不* 在用戶介面中。 您可以用三種不同的方式查看這些集。 （即使您在用戶介面中建立了影像集，這些方法也可用）。

* 開啟資產的屬性。 屬性指明引用的選定資產或其成員的設定。 要查看整個集，請選擇集名。

   ![6_5_imageset-asset屬性](assets/6_5_imageset-assetproperties.png)

* 來自任何組的成員映像。選擇 **[!UICONTROL 集]** 的子菜單。

   ![6_5-imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，您可以選擇 **[!UICONTROL 篩選]**，然後展開 **[!UICONTROL Dynamic Media]** 選擇 **[!UICONTROL 集]**。

   搜索返回在UI中手動建立或通過批集預設自動建立的匹配集。 對於自動集，搜索查詢使用「開始為」進行。 此搜索條件與基於使用「Contains」的Experience Manager不同。 將篩選器設定為 **[!UICONTROL 集]** 是搜索自動集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以通過用戶介面查看集，如中所述 [編輯影像集](#editing-image-sets)。

## 編輯影像集 {#editing-image-sets}

可以對影像集執行各種編輯任務，如：

* 向映像集添加映像。
* 對影像集中的影像重新排序。
* 刪除映像集中的資產。
* 應用查看器預設。
* 刪除映像集。

**要編輯映像集：**

1. 執行下列任一操作：

   * 將滑鼠懸停在影像集資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。
   * 將滑鼠懸停在影像集資產上，選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖），然後選擇 **[!UICONTROL 編輯]** 的子菜單。
   * 點擊影像集資產，然後選擇 **[!UICONTROL 編輯]** 表徵圖)。

1. 要編輯「影像集」中的影像，請執行以下任一操作：

   * 要重新排序資產，請將影像拖到新位置（選擇重新排序表徵圖以移動項目）。
   * 要按升序或降序對項目進行排序，請按一下列標題。
   * 要添加資產或更新現有資產，請按一下 **[!UICONTROL 添加資產]**。 定位至資產，選擇它，然後選擇 **[!UICONTROL 選擇]** 靠近頁面右上角。

      >[!NOTE]
      >
      >如果通過將縮覽圖替換為另一影像來刪除Experience Manager用於縮覽圖的影像，則仍會顯示原始資產。
   * 要刪除資產，請選擇它並選擇 **[!UICONTROL 刪除資產]**。
   * 要應用預設，請選擇靠近頁面右上角的 **[!UICONTROL 預設]**，然後選擇查看器預設。
   * 要添加或更改縮略圖，請選擇資產右側旁邊的縮略圖表徵圖。 導航到新縮略圖或色板資產，選擇它，然後選擇 **[!UICONTROL 選擇]**。
   * 要刪除整個映像集，請導航到映像集，選擇它，然後選擇 **[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >可以編輯影像集中的影像。 導航到集並選擇 **[!UICONTROL 設定成員]** 左欄。 要開啟編輯窗口，請選擇資產上的「鉛筆」表徵圖。

1. 點擊 **[!UICONTROL 保存]** 編輯。

## 預覽影像集 {#previewing-image-sets}

請參閱 [預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

## 發佈映像集 {#publishing-image-sets}

請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
