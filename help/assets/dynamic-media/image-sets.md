---
title: 影像集
description: 瞭解如何在Dynamic Media中使用影像集。
contentOwner: Rick Brough
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 4%

---

# 影像集 {#image-sets}

影像集為使用者提供整合式檢視體驗，使用者可按一下縮圖影像來檢視專案的不同檢視。 影像集可讓您呈現專案的替代檢視，而檢視器可提供縮放工具，以便更密切地檢查影像。

影像集由具有單字的橫幅指定 `IMAGESET`。此外，如果影像集已發佈，則橫幅上會顯示以&#x200B;**[!UICONTROL World]**&#x200B;圖示表示的發佈日期。 此外，亦會顯示以&#x200B;**[!UICONTROL 鉛筆]**&#x200B;圖示表示的最後修改日期。

![chlimage_1-133](assets/chlimage_1-339.png)

在影像集內，您也可以建立影像集並新增縮圖來建立色票。

當您想要以不同的顏色、圖樣或成品顯示專案時，此應用程式非常有用。 若要使用色票建立「影像集」，您需要為要呈現給使用者的每個不同顏色、圖樣或完成建立一個影像。 您還需要每個顏色、圖樣或光潔度使用一個顏色、圖樣或光潔度色票。

例如，假設您要以不同的顏色清單呈現大寫字的影像；清單為紅色、綠色和藍色。 在此情況下，您需要三個相同帽子的鏡頭。 您需要一個紅色鏡頭，一個綠色鏡頭，一個藍色鏡頭。 您還需要紅色、綠色和藍色色票。 色票可作為縮圖，讓使用者在色票集檢視器中按一下，以檢視紅色計費、綠色計費或藍色計費的次數上限。

>[!NOTE]
>
>如需Assets使用者介面的相關資訊，請參閱[使用觸控式UI管理資產](/help/assets/manage-digital-assets.md)。

建立影像集時，Adobe會建議下列最佳作法並強制進行下列限制：

| 限制型別 | 最佳實務 | 強加的限制 |
| --- | --- | --- |
| 每個集的重複資產數 | 無重複專案 | 20 |
| 每組影像的最大數量 | 每組5至10個影像 | 1000 |

另請參閱[Dynamic Media限制](/help/assets/dynamic-media/limitations.md)。

## 快速入門：影像集 {#quick-start-image-sets}

快速上手並執行：

1. 選擇性。[建立批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)，並將其套用至上傳迴轉集影像的新資料夾。

   批次集預設集可以幫助您自動建立影像集。

   >[!IMPORTANT]
   >
   >批次集由IPS (Image Production System)建立，作為資產提取的一部分。

1. [上傳多個檢視的主要來源影像](#uploading-assets-in-image-sets)。

   上傳影像集的影像。 請記住，使用者可以在影像集檢視器中放大影像。 因此，請謹慎選擇影像。 請確定影像的大小至少為2000畫素。

   如需影像集支援的格式清單，請參閱[Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media)。

1. [建立影像集](#creating-image-sets)。

   在「影像集」中，使用者按一下「影像集檢視器」中的縮圖影像。

   若要在Assets中建立影像集，請選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 影像集]**。 然後，新增影像並按一下[儲存]。**&#x200B;**

   請參閱[準備影像集資產以上傳及上傳您的檔案](#uploading-assets-in-image-sets)。

   請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 視需要新增[影像集檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

   管理員可以建立或修改影像集檢視器預設集。 若要檢視含有檢視器預設集的影像集，請選取該影像集，然後在左側導軌下拉式清單中選取&#x200B;**[!UICONTROL 檢視器]**。

   若要建立或編輯檢視器預設集，請參閱&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 檢視器預設集]**。

1. （選擇性） [檢視使用批次集預設集建立的影像集](/help/assets/dynamic-media/image-sets.md#viewing-image-sets)。
1. [預覽影像集](/help/assets/dynamic-media/previewing-assets.md)。

   選取「影像集」，即可預覽。 若要在選取的檢視器中檢查影像集，請選取縮圖圖示。 您可以從&#x200B;**[!UICONTROL 檢視器]**&#x200B;功能表（可從左側邊欄下拉式清單取得）中選擇不同的檢視器。

1. [發佈影像集](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

   發佈影像集時會啟用URL和內嵌字串。 此外，您必須[發佈您已建立的任何自訂檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。 現成可用的檢視器預設集已發佈。

1. [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

   Experience Manager Assets會為影像集建立URL呼叫，並在您發佈影像集後加以啟用。 您可以在預覽資產時複製這些URL。 或者，您也可以將其內嵌至您的網站。

   選取「影像集」，然後在左側導軌下拉式清單中選取&#x200B;**[!UICONTROL 檢視器]**。

   請參閱[將影像集連結至網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)以及[內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

若要編輯影像集，請參閱[編輯影像集](#editing-image-sets)。 此外，您也可以檢視及編輯[影像集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

如果您無法建立集合，請參閱[Dynamic Media疑難排解](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets)中的影像和集合。

## 上傳影像集的資產 {#uploading-assets-in-image-sets}

首先，請上傳影像集的影像資產。 請記住，使用者可以在影像集檢視器中放大影像。 因此，請謹慎選擇影像。 請確定影像在最大大小中至少為2000畫素，以獲得最佳縮放細節。 Dynamic Media最多可轉譯每張影像2500萬畫素。 例如，您可以使用5000x5000百萬畫素的影像，或任何其他大小組合，最高可達2500萬畫素。

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

如需影像集支援的格式清單，請參閱[Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media)。

您可以像在Assets[上傳任何其他資產一樣上傳影像集的影像](/help/assets/manage-digital-assets.md#uploading-assets)。

### 準備影像集資產以供上傳 {#preparing-image-set-assets-for-upload}

在建立影像集之前，請確定影像的大小和格式正確。

若要建立多檢視「影像集」，您需要顯示不同檢視點的專案或顯示相同專案的不同外觀的影像。 目標是要強調專案的重要功能，讓檢視者能夠完整瞭解專案的顯示方式或用途。

由於使用者可以在「影像集」中縮放影像，因此請確保影像在最大大小中至少為2000畫素。 Experience Manager Assets支援許多影像檔案格式，但建議使用無損的TIFF、PNG和EPS影像。

>[!NOTE]
>
>如果您使用縮圖來表示產品色票，請執行下列動作：
>
>建立相同影像的暈映或不同快照，以不同的顏色、圖樣或完成顯示影像。 您還需要對應至不同顏色、圖樣或最終處理的縮圖檔案。 例如，若要呈現縮圖，且「影像集」以黑色、棕色和綠色顯示同一夾克，您需要：
>
>* 同一件夾克的黑色、棕色和綠色照片。
>* 黑色、棕色和綠色的縮圖。

## 建立影像集 {#creating-image-sets}

您可以透過使用者介面或透過API建立影像集。

>[!NOTE]
>
>您也可以透過[批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)自動建立影像集。
>**重要：**&#x200B;批次集由IPS (Image Production System)建立，作為資產擷取的一部分。

將資產新增至集時，資產會自動以字母數字順序新增。 在新增資產後，您可以手動重新排序或排序資產。

>[!NOTE]
>
>檔案名稱中有「，」（逗號）的資產不支援影像集。

建立影像集時，Adobe會建議下列最佳作法並強制進行下列限制：

| 限制型別 | 最佳實務 | 強加的限制 |
| --- | --- | --- |
| 每個集的重複資產數 | 無重複專案 | 20 |
| 每組影像的最大數量 | 每組5至10個影像 | 1000 |

另請參閱[Dynamic Media限制](/help/assets/dynamic-media/limitations.md)。

**若要建立影像集：**

1. 在Adobe Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 選取&#x200B;**[!UICONTROL 導覽]** > **[!UICONTROL Assets]**。 導覽至您要建立影像集的位置，然後前往&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 影像集]**&#x200B;以開啟「影像集編輯器」頁面。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁面的&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中，輸入影像集的名稱。 該名稱會出現在整個影像集的橫幅中。 選擇性地輸入說明。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 執行下列其中一項：

   * 在「影像集編輯器」頁面的左上角附近，選取&#x200B;**[!UICONTROL 新增資產]**。

   * 在「影像集編輯器」頁面中間附近，選取&#x200B;**[!UICONTROL 點選以開啟「資產選擇器」]**。

   選取以選取您要納入影像集的資產。 選取的資產上面有勾號圖示。 完成時，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 選取]**。

   使用「資產選擇器」，您可以輸入關鍵字並選取&#x200B;**[!UICONTROL 退貨]**&#x200B;來搜尋資產。 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後在工具列中選取&#x200B;**[!UICONTROL 篩選]**&#x200B;圖示。 選取[檢視]圖示並選取&#x200B;**[!UICONTROL 資料行檢視]**、**[!UICONTROL 卡片檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**，以變更檢視。

   請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 將資產新增至集時，資產會自動以字母數字順序新增。 在新增資產後，您可以手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以將影像重新排序至集清單的上方或下方。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請按一 **下影像旁** 的+ **縮圖** 圖示，並導覽至您想要的縮圖或色票。選取完所有影像後，按一下「 **[!UICONTROL 儲存]**」。

1. (選用) 執行以下任一操作：

   * 若要刪除影像，請選取該影像，然後選取&#x200B;**[!UICONTROL 刪除資產]**。

   * 若要套用預設集，在頁面右上角附近選取「**[!UICONTROL 預設集]**」，然後選取要一次套用至所有資產的預設集。

   >[!NOTE]
   >
   >建立影像集時，您可以變更影像集縮圖。 或者，您也可以讓Experience Manager根據影像集中的資產自動選取縮圖。 若要選取縮圖，請選取[影像集編輯器]頁面上[標題]欄位上方的&#x200B;**[!UICONTROL 變更縮圖]**。 然後，選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要讓Experience Manager從影像集產生縮圖，請選取「**[!UICONTROL 切換至]**」**[!UICONTROL 「自動縮圖]**」。

1. 按一下「**[!UICONTROL 儲存]**」。您建立的影像集會顯示在您建立的資料夾中。

## 檢視影像集 {#viewing-image-sets}

您可以在使用者介面中建立影像集，或自動使用[批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)。

>[!IMPORTANT]
>
>批次集由IPS [Image Production System]建立，作為資產擷取的一部分。

但是，使用批次集預設集建立的集，請&#x200B;*不*&#x200B;出現在使用者介面中。 您可以使用三種不同的方式檢視這些集合。 （即使您在使用者介面中建立影像集，這些方法仍可使用）。

* 開啟資產的屬性。 屬性會指出所選取資產被參考或所屬成員的設定。 若要檢視整個集合，請選取集合名稱。

  ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* 來自任何組的成員映像。選取&#x200B;**[!UICONTROL 集合]**&#x200B;功能表以顯示資產所屬的集合。

  ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 從搜尋中，您可以選取&#x200B;**[!UICONTROL 篩選器]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;並選取&#x200B;**[!UICONTROL 集合]**。

  搜尋會傳回在UI中手動建立，或透過批次集預設集自動建立的相符集。 對於自動化集，搜尋查詢是使用「開頭為」進行。 此搜尋條件與以使用「包含」為基礎的Experience Manager不同。 將篩選器設定為&#x200B;**[!UICONTROL 集]**&#x200B;是搜尋自動化集的唯一方法。

  ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以透過使用者介面檢視影像集，如[編輯影像集](#editing-image-sets)中所述。

## 編輯影像集 {#editing-image-sets}

您可以對「影像集」執行各種編輯工作，例如：

* 將影像新增至影像集。
* 重新排序影像集中的影像。
* 刪除影像集中的資產。
* 套用檢視器預設集。
* 刪除影像集。

**若要編輯影像集：**

1. 執行下列任一項作業：

   * 將游標暫留在影像集資產上，然後選取&#x200B;**[!UICONTROL 編輯]** （鉛筆圖示）。
   * 將游標暫留在影像集資產上，選取&#x200B;**[!UICONTROL 選取]** （勾選圖示），然後在工具列中選取&#x200B;**[!UICONTROL 編輯]**。
   * 在影像集資產上選取，然後在工具列中選取「**[!UICONTROL 編輯]**」（鉛筆圖示）。

1. 若要編輯「影像集」中的影像，請執行下列任一項作業：

   * 若要重新排序資產，請將影像拖曳至新位置（選取重新排序圖示以移動專案）。
   * 若要以遞增或遞減順序排序專案，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下&#x200B;**[!UICONTROL 新增資產]**。 導覽至某個資產，選取該資產，然後選取頁面右上角附近的&#x200B;**[!UICONTROL 選取]**。

     >[!NOTE]
     >
     >如果您刪除Experience Manager用於縮圖的影像，改為其他影像，仍會顯示原始資產。

   * 若要刪除資產，請選取該資產，然後選取&#x200B;**[!UICONTROL 刪除資產]**。
   * 若要套用預設集，在頁面右上角附近，選取&#x200B;**[!UICONTROL 預設集]**，然後選取檢視器預設集。
   * 若要新增或變更縮圖，請選取資產右側旁的縮圖圖示。 導覽至新的縮圖或色票資產，選取它，然後選取&#x200B;**[!UICONTROL 選取]**。
   * 若要刪除整個影像集，請導覽至該影像集，選取該影像集，然後選取&#x200B;**[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >您可以編輯影像集中的影像。 導覽至該集，並在左側邊欄中選取&#x200B;**[!UICONTROL 設定成員]**。 若要開啟編輯視窗，請選取資產上的「鉛筆」圖示。

1. 完成編輯後，選取&#x200B;**[!UICONTROL 儲存]**。

## 預覽影像集 {#previewing-image-sets}

請參閱[預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

## 發佈影像集 {#publishing-image-sets}

請參閱[發佈Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
