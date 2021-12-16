---
title: 影像集
description: 了解如何在Dynamic Media中使用影像集。
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: b31fa5af7bcaa944d8bd7b0bb7d7b8deb36906a8
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 5%

---

# 影像集 {#image-sets}

影像集可為使用者提供整合的檢視體驗，讓使用者按一下縮圖影像即可看見項目的不同檢視。 「影像集」可讓您呈現項目的替代檢視，而檢視器提供縮放工具，以密切檢查影像。

影像集由具有單字的橫幅指定 `IMAGESET`。此外，如果已發佈影像集，則會顯示發佈日期(以 **[!UICONTROL 世界]** 表徵圖。 此外，上次修改日期(以 **[!UICONTROL 鉛筆]** 的上界。

![chlimage_1-133](assets/chlimage_1-339.png)

在影像集內，您也可以建立「影像集」並新增縮圖來建立色票。

當要以不同顏色、模式或完成顯示項目時，此應用程式非常有用。 要使用顏色色板建立影像集，需要為要呈現給用戶的不同顏色、圖案或完成建立一個影像。 每種顏色、圖樣或完成還需要一個顏色、圖樣或完成色板。

例如，假設您想要呈現具有不同顏色鈔票的大寫影像；賬單是紅色、綠色和藍色的。 在這個情況下，你需要三槍一槍。 你需要一張紅色的，一張綠色的，一張藍色的。 您也需要紅色、綠色和藍色色票。 顏色色板用作縮圖，用戶可在「色板集查看器」中按一下該縮圖，以查看紅色計費、綠色計費或藍色計費的帽子。

>[!NOTE]
>
>如需Assets使用者介面的資訊，請參閱 [使用觸控式UI管理資產](/help/assets/manage-digital-assets.md).

## 快速入門：影像集 {#quick-start-image-sets}

快速啟動並運行：

1. 選填。[建立批集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md) 並將其套用至上傳回轉集影像的新資料夾。

   批次集預設集可協助您自動建立影像集。

   >[!IMPORTANT]
   >
   >批集由IPS(Image Production System)建立，作為資產提取的一部分。

1. [上傳多個檢視的主要來源影像](#uploading-assets-in-image-sets).

   上傳影像集的影像。 請記住，用戶可以在影像集查看器中放大影像。 因此，請謹慎選擇影像。 請確定影像大小最大時至少為2000像素。

   請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 以取得影像集支援的格式清單。

1. [建立影像集](#creating-image-sets).

   在「影像集」中，用戶按一下「影像集查看器」中的縮圖影像。

   若要在資產中建立影像集，請選取 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]**. 然後，添加影像並按一下 **[!UICONTROL 儲存]**.

   請參閱 [準備影像集資產以上傳和上傳您的檔案](#uploading-assets-in-image-sets).

   請參閱 [使用選取器](/help/assets/dynamic-media/working-with-selectors.md).

1. 新增 [影像集查看器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)，視需要。

   管理員可以建立或修改影像集檢視器預設集。 若要檢視您的影像集與檢視器預設集，請選取該影像集，然後在左側邊欄下拉式清單中選取 **[!UICONTROL 檢視器]**.

   要建立或編輯查看器預設集，請參閱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.

1. （可選） [檢視影像集](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) 使用批集預設集建立的。
1. [預覽影像集](/help/assets/dynamic-media/previewing-assets.md).

   選取「影像集」，即可預覽。 若要在選取的檢視器中檢查影像集，請選取縮圖圖示。 您可以從 **[!UICONTROL 檢視器]** 功能表（從左側欄下拉式清單中取得）。

1. [發佈影像集](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   「發佈影像集」會啟用URL和「內嵌」字串。 此外，您必須 [發佈任何自訂檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md) 已建立的。 已發佈現成可用的檢視器預設集。

1. [將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 或 [內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md).

   Experience Manager Assets會建立影像集的URL呼叫，並在您發佈影像集後啟用它們。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選取「影像集」，然後在左側邊欄下拉式清單中選取 **[!UICONTROL 檢視器]**.

   請參閱 [將影像集連結至網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 和 [內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md).

若要編輯影像集，請參閱 [編輯影像集](#editing-image-sets). 此外，您也可以檢視及編輯 [影像集屬性](/help/assets/manage-digital-assets.md#editing-properties).

如果建立集時遇到問題，請參閱 [疑難排解Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## 上傳影像集的資產 {#uploading-assets-in-image-sets}

首先，請上傳影像集的影像資產。 請記住，用戶可以在影像集查看器中放大影像。 因此，請謹慎選擇影像。 請確定影像大小最大，至少為2000像素，以獲得最佳縮放詳細資訊。 Dynamic Media可以每張2500萬像素的影像呈現。 例如，您可以使用5000x5000萬像素影像或任何其他大小組合，最高2500萬像素。

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 以取得影像集支援的格式清單。

您可以像上傳一樣上傳影像集的影像 [上傳資產中的任何其他資產](/help/assets/manage-digital-assets.md#uploading-assets).

### 準備影像集資產以供上傳 {#preparing-image-set-assets-for-upload}

建立影像集之前，請確定影像的大小和格式正確。

要建立多視圖影像集，您需要顯示不同視點的項目或顯示同一項目的不同方面的影像。 其目的是要反白標示項目的重要功能，讓檢視者能完整了解項目的顯示方式或運作方式。

因為使用者可以在影像集中縮放影像，請確定影像大小至少為2000像素。 Experience Manager Assets支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

>[!NOTE]
>
>如果您使用縮圖來指示產品色票，請執行下列操作：
>
>為相同影像建立暈映或不同的擷取畫面，以不同的顏色、圖案或完整顯示。 您還需要與不同顏色、圖案或結束相對應的縮圖檔案。 例如，若要以影像集呈現縮圖，並以黑色、棕色和綠色顯示相同的夾克，您需要：
>
>* 黑色、棕色和綠色的同一件夾克。
>* 黑色、棕色和綠色縮圖。


## 建立影像集 {#creating-image-sets}

您可以透過使用者介面或API來建立影像集。

>[!NOTE]
>
>您也可以透過 [批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**** 重要：批集由IPS(Image Production System)建立，作為資產提取的一部分。

將資產新增至資產集時，資產會以英數字元順序自動新增。 新增資產後，您可以手動重新排序或排序資產。

>[!NOTE]
>
>檔案名稱中包含「，」（逗號）的資產不支援影像集。

**要建立影像集：**

1. 在Adobe Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 點選 **[!UICONTROL 導覽]** > **[!UICONTROL 資產]**. 導覽至您要建立影像集的位置，然後前往 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]** 開啟「影像集編輯器」頁。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁中， **[!UICONTROL 標題]** 欄位，輸入影像集的名稱。 名稱會出現在影像集的橫幅中。 （可選）輸入說明。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一操作：

   * 在「影像集編輯器」頁面的左上角附近，選擇 **[!UICONTROL 新增資產]**.

   * 在「影像集編輯器」頁面的中間附近，選擇 **[!UICONTROL 點選以開啟資產選擇器]**.
   點選以選取您要納入影像集的資產。 選取的資產上面有核取標籤圖示。 完成後，在頁面右上角附近，選取 **[!UICONTROL 選擇]**.

   使用「資產選擇器」，您可以輸入關鍵字並選取 **[!UICONTROL 傳回]**. 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後選取 **[!UICONTROL 篩選]** 圖示。 選擇「視圖」表徵圖並選擇 **[!UICONTROL 欄檢視]**, **[!UICONTROL 卡片檢視]**，或 **[!UICONTROL 清單檢視]**.

   請參閱 [使用選取器](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 將資產新增至資產集時，資產會以英數字元順序自動新增。 新增資產後，您可以手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以在設定清單上或下重新排序影像。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請按一 **下影像旁** 的+ **縮圖** 圖示，並導覽至您想要的縮圖或色票。選取完所有影像後，按一下「 **[!UICONTROL 儲存]**」。

1. （選用）執行下列任一操作：

   * 若要刪除影像，請選取影像並選取 **[!UICONTROL 刪除資產]**.

   * 若要套用預設集，請在頁面右上角附近選取 **[!UICONTROL 預設集]**，然後選取要一次套用至所有資產的預設集。
   >[!NOTE]
   >
   >建立影像集時，您可以變更影像集縮圖。 或者，您可以讓Experience Manager根據影像集中的資產自動選取縮圖。 若要選取縮圖，請選取 **[!UICONTROL 變更縮圖]** 位於「影像集編輯器」頁面上的「標題」欄位上方。 然後，選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您選取縮圖，然後決定要Experience Manager從影像集產生縮圖，請選取 **[!UICONTROL 切換至]** **[!UICONTROL 自動縮圖]**.

1. 按一下「**[!UICONTROL 儲存]**」。新建立的「影像集」(Image Set)會顯示在您建立該影像集的資料夾中。

## 檢視影像集 {#viewing-image-sets}

您可以在使用者介面中建立影像集，或自動使用 [批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>批集由IPS建立 [影像製作系統] 作為資產擷取的一部分。

但是，使用批集預設集建立的集，請執行 *not* 顯示在使用者介面中。 您可以透過三種不同方式來檢視這些集合。 （即使您在使用者介面中建立影像集，這些方法仍可供使用）。

* 開啟資產的屬性。 屬性會指出所參考之選定資產或其成員的設定。 要查看整個集，請選擇集名。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* 來自任何組的成員映像。選取 **[!UICONTROL 集]** 功能表來顯示資產所屬的集。

   ![6_5_imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜尋中，您可以選取 **[!UICONTROL 篩選]**，然後展開 **[!UICONTROL Dynamic Media]** 選取 **[!UICONTROL 集]**.

   搜尋會傳回在UI中手動建立或透過批次集預設集自動建立的相符集。 對於自動化集，搜尋查詢是使用「開頭為」進行。 此搜尋條件與以「包含」為基礎的Experience Manager不同。 將篩選器設定為 **[!UICONTROL 集]** 是搜尋自動化集的唯一方式。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以透過使用者介面來檢視集，如 [編輯影像集](#editing-image-sets).

## 編輯影像集 {#editing-image-sets}

您可以對影像集執行各種編輯任務，如：

* 將影像新增至影像集。
* 重新排序影像集中的影像。
* 刪除影像集中的資產。
* 套用檢視器預設集。
* 刪除影像集。

**要編輯影像集：**

1. 執行下列任一操作：

   * 暫留在影像集資產上，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。
   * 暫留在影像集資產上，選取 **[!UICONTROL 選擇]** （勾選標籤圖示），然後選取 **[!UICONTROL 編輯]** 的下一頁。
   * 點選「影像集」資產，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。

1. 要編輯「影像集」中的影像，請執行以下操作之一：

   * 若要重新排序資產，請拖曳影像至新位置（選取重新排序圖示以移動項目）。
   * 若要依遞增或遞減順序排序項目，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下 **[!UICONTROL 新增資產]**. 導覽至資產，選取資產，然後選取 **[!UICONTROL 選擇]** 靠近頁面的右上角。

      >[!NOTE]
      >
      >如果您以其他影像取代縮圖，以刪除Experience Manager用於縮圖的影像，仍會顯示原始資產。
   * 若要刪除資產，請選取資產並選取 **[!UICONTROL 刪除資產]**.
   * 若要套用預設集，請在頁面右上角附近選取 **[!UICONTROL 預設集]**，然後選取檢視器預設集。
   * 若要新增或變更縮圖，請選取資產右側的縮圖圖示。 導覽至新的縮圖或色票資產，選取它，然後選取 **[!UICONTROL 選擇]**.
   * 若要刪除整個影像集，請導覽至影像集，選取它，然後選取 **[!UICONTROL 刪除]**.

   >[!NOTE]
   >
   >您可以編輯影像集中的影像。 導覽至集合併選取 **[!UICONTROL 設定成員]** 在左側邊欄。 若要開啟編輯視窗，請選取資產上的鉛筆圖示。

1. 點選 **[!UICONTROL 儲存]** 編輯完畢。

## 預覽影像集 {#previewing-image-sets}

請參閱 [預覽資產](/help/assets/dynamic-media/previewing-assets.md).

## 發佈影像集 {#publishing-image-sets}

請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
