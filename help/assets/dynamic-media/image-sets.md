---
title: 影像集
description: 瞭解如何在Dynamic Media處理影像集。
feature: 影像集
role: Business Practitioner
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '2049'
ht-degree: 9%

---

# 影像集 {#image-sets}

「影像集」為使用者提供整合的檢視體驗，讓使用者按一下縮圖影像，即可看到不同的項目檢視。 「影像集」可讓您呈現項目的替代檢視，而檢視器則提供縮放工具，以密切檢查影像。

影像集由具有單字的橫幅指定 `IMAGESET`。此外，如果影像集已發佈，則橫幅上會顯示以&#x200B;**[!UICONTROL World]**&#x200B;圖示指示的發佈日期。 此外，還顯示由&#x200B;**[!UICONTROL Pencil]**&#x200B;表徵圖指示的最後修改日期。

![chlimage_1-133](assets/chlimage_1-339.png)

在影像集中，您也可以建立「影像集」並新增縮圖，以建立色票。

當您想要以不同的顏色、圖樣或完成來顯示項目時，此應用程式非常實用。 若要使用色票建立影像集，您需要針對要呈現給使用者的不同顏色、圖樣或修飾建立一個影像。 您也需要一種顏色、圖樣或修飾色板來表示每種顏色、圖樣或修飾。

例如，假設您想要呈現不同色彩表的頂蓋影像；賬單是紅的，綠的，藍的。 在這種情況下，你需要三杯相同的帽子。 你需要一張紅的，一張綠的，一張藍的。 您也需要紅色、綠色和藍色色票。 顏色色票會當做使用者在「色票集檢視器」中按一下的縮圖，以查看紅嘴、綠嘴或藍嘴的帽子。

>[!NOTE]
>
>如需「資產」使用者介面的詳細資訊，請參閱「使用Touch UI](/help/assets/manage-digital-assets.md)管理資產」。[

## 快速入門：影像集{#quick-start-image-sets}

要快速啟動並運行，請執行以下操作：

1. 選填。[建立批次集預](/help/assets/dynamic-media/batch-set-presets-dm.md) 設集，並將它套用至上傳回轉集影像的新資料夾。

   批次集預設集可協助您自動建立影像集。

   >[!IMPORTANT]
   >
   >批集由IPS(Image Production System)建立，作為資產提取的一部分。

1. [上傳多個檢視的主要來源影像](#uploading-assets-in-image-sets)。

   上傳影像集的影像。 請記住，使用者可以在「影像集檢視器」中縮放影像。 因此，請謹慎選擇您的影像。 請確定影像在最大尺寸中至少為2000像素。「Experience Manager資產」支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

1. [建立影像集](#creating-image-sets)。

   在「影像集」中，使用者按一下「影像集檢視器」中的縮圖影像。

   若要在「資產」中建立影像集，請點選或按一下「建立>影像集&#x200B;]**」。**[!UICONTROL &#x200B;然後，添加影像並按一下&#x200B;**[!UICONTROL 保存]**。

   請參閱[準備要上傳和上傳檔案的影像集資產](#uploading-assets-in-image-sets)。

   請參閱[使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 視需要新增[影像集檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

   管理員可以建立或修改影像集檢視器預設集。 若要查看您的影像集及檢視器預設集，請選取影像集，然後在左側導軌下拉式清單中，選取「**[!UICONTROL 檢視器]**」。

   若要建立或編輯檢視器預設集，請參閱&#x200B;**[!UICONTROL 工具>資產>檢視器預設集]**。

1. （可選）[檢視使用批集預設集建立的影像集](/help/assets/dynamic-media/image-sets.md#viewing-image-sets)。
1. [預覽影像集](/help/assets/dynamic-media/previewing-assets.md)。

   選取「影像集」，您就可以預覽它。 若要在選取的檢視器中檢查影像集，請點選縮圖圖示。 您可以從左側導軌下拉式清單中的&#x200B;**[!UICONTROL 檢視器]**&#x200B;選單選擇不同的檢視器。

1. [發佈影像集](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

   發佈影像集會啟動URL和內嵌字串。 此外，您必須[發佈您所建立的任何自訂檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。 現成可用的檢視器預設集已發佈。

1. [將URL連結至您的Web應](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 用程 [式或內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

   Experience Manager資產會建立影像集的URL呼叫，並在您發佈影像集後加以啟動。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選擇「影像集」，然後在左側導軌下拉式清單中，選取「**[!UICONTROL 檢視器]**」。

   請參 [閱連結影像集至網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)[和內嵌影片或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

要編輯影像集，請參閱[編輯影像集](#editing-image-sets)。 此外，您還可以檢視和編輯[影像集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

如果建立集時遇到問題，請參閱[疑難排解Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets)中的映像和集。

## 上傳影像集{#uploading-assets-in-image-sets}的資產

首先，上傳影像集的影像資產。 請記住，使用者可以在「影像集檢視器」中縮放影像。 因此，請謹慎選擇您的影像。 請確定影像在最大尺寸中至少有2000像素，以獲得最佳縮放細節。 Dynamic Media每幅影像的轉譯率高達2500萬像素。 例如，您可使用5000 x 5000百萬像素影像或任何其他大小的組合，最高2500萬像素。

「影像集」支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

您可以像[上傳資產](/help/assets/manage-digital-assets.md#uploading-assets)中的任何其他資產一樣，上傳影像集的影像。

### 準備上傳{#preparing-image-set-assets-for-upload}的影像集資產

在建立影像集之前，請確定影像的大小和格式正確。

若要建立多檢視影像集，您需要顯示來自不同視點的項目或顯示相同項目不同方面的影像。 其目標是強調項目的重要功能，讓檢視者可完整瞭解項目的外觀或行為。

因為使用者可以在影像集中縮放影像，所以請確定影像在最大尺寸中至少為2000像素。 「Experience Manager資產」支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

>[!NOTE]
>
>如果您使用縮圖來表示產品色票，請執行下列動作：
>
>為相同影像建立暈映或不同的像片，以不同的顏色、圖樣或光潔度顯示。 您也需要對應不同顏色、圖樣或修飾的縮圖檔案。 例如，若要以影像集呈現縮圖，並以黑色、棕色和綠色顯示相同的外套，您需要：
>
>* 黑色、棕色和綠色的相同夾克。
>* 黑色、棕色和綠色縮圖。


## 建立影像集{#creating-image-sets}

您可以透過使用者介面或透過API建立影像集。

>[!NOTE]
>
>您也可以透過[批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)自動建立影像集。
>**** 重要：批集由IPS(Image Production System)建立，作為資產提取的一部分。

當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在資產新增後手動重新排序或排序。

>[!NOTE]
>
>檔案名稱中具有&quot;,&quot;（逗號）的資產不支援影像集。

**若要建立影像集**

1. 在Adobe Experience Manager，點選Experience Manager標誌以存取全球導覽主控台。
1. 點選&#x200B;**[!UICONTROL 導覽>資產]**。 導覽至您要建立影像集的位置，然後點選「建 **[!UICONTROL 立>影像集]** 」以開啟「影像集編輯器」頁面。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁面的&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，輸入影像集的名稱。 名稱會出現在影像集的橫幅中。 （可選）輸入說明。

   ![6_5-影像集——建立新集](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一項作業：

   * 在「影像集編輯器」頁面的左上角附近，點選「新增資產」**[!UICONTROL 。]**

   * 在「影像集編輯器」頁面的中間，點選&#x200B;**[!UICONTROL 以開啟「資產選擇器」]**。
   點選以選取您要納入影像集的資產。 選取的資產上面有核取標籤圖示。 完成後，在頁面右上角附近點選&#x200B;**[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後點選工具列中的&#x200B;**[!UICONTROL Filter]**&#x200B;圖示。 點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱[使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![6_5-影像集——新增資產](assets/6_5_imageset-addingassets.png)

1. 當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在新增資產後手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以在設定清單上或下重新排序影像。

   ![6_5-影像集——重新排序資產](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請按一 **下影像旁** 的+ **縮圖** 圖示，並導覽至您想要的縮圖或色票。選取完所有影像後，按一下「 **[!UICONTROL 儲存]**」。

1. （可選）執行下列任一項作業：

   * 若要刪除影像，請選取影像並點選「刪除資產」。****

   * 若要套用預設，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**，然後選取一個預設，一次套用至所有資產。
   >[!NOTE]
   >
   >建立影像集時，您可以變更影像集縮圖。 或者，您可讓Experience Manager根據影像集中的資產自動選取縮圖。 若要選取縮圖，請點選「影像集編輯器」頁面上「標題」欄位上方的「變更縮圖&#x200B;**[!UICONTROL 」。然後，選擇任何影像（您也可以導覽至其他檔案夾以尋找影像）。]**&#x200B;如果您選取了縮圖，然後決定要Experience Manager從影像集產生縮圖，請選取「切換至&#x200B;]****[!UICONTROL &#x200B;自動縮圖&#x200B;]**」。**[!UICONTROL 

1. 按一下「**[!UICONTROL 儲存]**」。您新建立的「影像集」會顯示在您所建立的檔案夾中。

## 查看影像集{#viewing-image-sets}

您可以在使用者介面中建立影像集，或使用[批次集預設集](/help/assets/dynamic-media/batch-set-presets-dm.md)自動建立影像集。

>[!IMPORTANT]
>
>批集由IPS [映像生產系統]建立，作為資產提取的一部分。

不過，使用批集預設集建立的集合，請&#x200B;*not*&#x200B;出現在使用者介面中。 您可以以三種不同的方式檢視這些集。 （即使您在使用者介面中建立影像集，這些方法也可用）。

* 開啟資產的屬性。 屬性指出所選資產被參考或成員的設定。 若要查看整個集，請點選集名。

   ![6_5_imageset-asset屬性](assets/6_5_imageset-assetproperties.png)

* 來自任何組的成員映像。選擇&#x200B;**[!UICONTROL Sets]**&#x200B;菜單以顯示資產所屬的集。

   ![6_5_imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，可以選擇&#x200B;**[!UICONTROL Filter]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;並選擇&#x200B;**[!UICONTROL Sets]**。

   搜尋會傳回在UI中手動建立或透過批次集預設集自動建立的相符集。 對於自動集，使用「開頭為」執行搜尋查詢。 此搜尋准則與使用「包含」的Experience Manager不同。 將篩選器設定為&#x200B;**[!UICONTROL Sets]**&#x200B;是搜索自動集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以透過使用者介面來檢視集，如[編輯影像集](#editing-image-sets)所述。

## 編輯影像集{#editing-image-sets}

您可以對影像集執行各種編輯工作，例如：

* 將影像新增至影像集。
* 在影像集中重新排序影像。
* 刪除影像集中的資產。
* 套用檢視器預設集。
* 刪除影像集。

**若要編輯影像集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在「影像集」資產上，然後點選「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 將滑鼠指標暫留在影像集資產上，點選「**[!UICONTROL 選擇]**」（勾選標籤圖示），然後點選工具列中的「編輯」。****
   * 點選影像集資產，然後點選工具列中的&#x200B;**[!UICONTROL Edit]**（鉛筆圖示）。

1. 若要編輯影像集中的影像，請執行下列任一項作業：

   * 若要重新排序資產，請將影像拖曳至新位置（選取重新排序圖示以移動項目）。
   * 若要依遞增或遞減順序排序項目，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下「新增資產」。 ****&#x200B;導覽至資產，選取它，然後點選頁面右上角的&#x200B;**[!UICONTROL Select]**。

      >[!NOTE]
      >
      >如果您將Experience Manager用縮圖取代為其他影像，以刪除縮圖所使用的影像，原始資產仍會顯示。
   * 若要刪除資產，請選取資產並點選或按一下「刪除資產」。****
   * 若要套用預設，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**，然後選取檢視器預設集。
   * 若要新增或變更縮圖，請選取資產右側的縮圖圖示。 導覽至新的縮圖或色票資產，選取它，然後點選&#x200B;**[!UICONTROL Select]**。
   * 若要刪除整個影像集，請導覽至影像集，選取它，然後點選&#x200B;**[!UICONTROL Delete]**。

   >[!NOTE]
   >
   >您可以編輯影像集中的影像。 導覽至該集，然後點選左側導軌中的「設定成員」。 ****&#x200B;若要開啟編輯視窗，請點選資產上的「鉛筆」圖示。

1. 完成編輯時，點選「**[!UICONTROL 儲存]**」。

## 預覽影像集{#previewing-image-sets}

請參閱[預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

## 發佈影像集{#publishing-image-sets}

請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
