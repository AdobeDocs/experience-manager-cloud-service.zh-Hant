---
title: 混合媒體集
description: 瞭解如何在Dynamic Media中使用混合媒體集。
contentOwner: Rick Brough
feature: Mixed Media Sets
role: User
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 12%

---

# 混合媒體集{#mixed-media-sets}

混合媒體集可讓您在單一簡報中提供影像、影像集、迴轉集和視訊的混合。

混合媒體集由橫幅指定，並加上單字 **[!UICONTROL MixedMediaSet]**。此外，如果「混合媒體集」已發佈，則會顯示「鉛筆」圖示所指示的發佈日期(以 **[!UICONTROL World]** 圖示指示)與上次修改日期(以 **&#x200B;**&#x200B;Pencil圖示表示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>如需Assets使用者介面的相關資訊，請參閱[使用觸控式UI管理資產](/help/assets/manage-digital-assets.md)。

## 快速入門：混合媒體集 {#quick-start-mixed-media-sets}

若要快速啟動並執行「混合媒體集」，請遵循下列步驟：

1. [上傳您的資產](#uploading-assets)。

   首先，上傳混合媒體集的影像和視訊。如有必要，請建立 [影像集](/help/assets/dynamic-media/image-sets.md) [和回轉集](/help/assets/dynamic-media/spin-sets.md)。由於使用者可以在混合媒體集檢視器中放大影像，因此當您選擇影像時，請務必說明要放大哪些影像。 請確定影像的大小至少為2000畫素。

   如需混合媒體集支援的格式清單，請參閱[Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media)。

1. [建立混合媒體集](#creating-mixed-media-sets)。

   若要建立混合媒體集，請從Assets頁面，前往&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 混合媒體集]**，然後命名該集合、選擇資產，然後選擇影像的顯示順序。

   請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 視需要設定[混合媒體檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

   管理員可以建立或修改混合媒體集檢視器預設集。若要檢視您的混合媒體與檢視器預設集，請選取混合媒體集，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   若要建立或編輯檢視器預設集，請瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 檢視器預設集]**。

   請參閱[新增及編輯檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

1. [預覽混合媒體集](#previewing-mixed-media-sets)。

   選取「混合媒體集」，您就可以預覽它。 若要在選取的檢視器中檢查您的混合媒體集，請選取縮圖圖示。 您可以從&#x200B;**[!UICONTROL 檢視器]**&#x200B;功能表（可從左側導軌下拉式功能表取得）中選擇不同的檢視器。

1. [發佈混合媒體集](#publishing-mixed-media-sets)。

   發佈混合媒體集時會啟用URL和內嵌字串。 此外，您必須[發佈檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

1. [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

   Adobe Experience Manager Assets會為混合媒體集建立URL呼叫，並在您發佈混合媒體集後加以啟用。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選取混合媒體集，然後在左側導軌下拉式選單中選取&#x200B;**[!UICONTROL 檢視器]**。

   請參閱[將混合媒體集連結至網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)以及[內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

如有必要，您可以編輯[混合媒體集](#editing-mixed-media-sets)。 此外，您可以檢視及修改[混合媒體集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

>[!NOTE]
>
>如果您無法建立集合，請參閱[Dynamic Media疑難排解](/help/assets/dynamic-media/troubleshoot-dm.md)。

## 上傳資產 {#uploading-assets}

首先，上傳混合媒體集的影像和視訊。請記住，使用者可以在混合媒體集檢視器中放大影像。 因此，選擇具有此縮放功能的影像。 請確定影像的大小至少為2000畫素。

此外，如果您想要將迴轉集或影像集新增至混合媒體集，請一併建立它們。

如需混合媒體集支援的格式清單，請參閱[Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media)。

## 建立混合媒體集 {#creating-mixed-media-sets}

您可以將影像、影像集、迴轉集和視訊新增至混合媒體集。 將檔案、影像集和迴轉集新增至混合媒體集之前，請確定檔案和影像集已可發佈。

將資產新增至集時，資產會自動以字母數字順序新增。 在新增資產後，您可以手動重新排序或排序資產。

**若要建立混合媒體集：**

1. 在Assets中，導覽至您要建立混合媒體集的位置，然後選取「**[!UICONTROL 建立]**」，然後選取「**[!UICONTROL 混合媒體集]**」。 您也可以從包含資產的資料夾內建立資產集。顯示混合媒體集編輯器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在混合媒體集編輯器的&#x200B;**[!UICONTROL 標題]**&#x200B;中，輸入混合媒體集的名稱。 此名稱會出現在混合媒體集的橫幅中。 選擇性地輸入說明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >建立混合媒體集時，您可以變更混合媒體集縮圖，或允許Experience Manager根據混合媒體集中的資產自動選取縮圖。 若要選取縮圖，請選取&#x200B;**[!UICONTROL 變更縮圖]**&#x200B;並選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要讓Experience Manager從混合媒體集產生縮圖，請選取&#x200B;**[!UICONTROL 切換至自動縮圖]**。

1. 若要選取您要納入混合媒體集的資產，請選取「資產選擇器」。 選取它們，然後選取&#x200B;**[!UICONTROL 選取]**。

   使用「資產選擇器」，您可以輸入關鍵字並選取&#x200B;**[!UICONTROL 退貨]**&#x200B;來搜尋資產。 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後從工具列選取&#x200B;**[!UICONTROL 篩選]**&#x200B;圖示。 通過選擇「視圖」圖 **[!UICONTROL 標]** ，然後選擇「清單視圖」、「列 **[!UICONTROL 視圖」]**&#x200B;或「卡片視圖 **[!UICONTROL 」來更]**&#x200B;**&#x200B;**&#x200B;改視圖。

   請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. 視需要透過將資產向上或向下拖曳至清單來重新排序資產（必須選取&#x200B;**[!UICONTROL 重新排序]**&#x200B;圖示）。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果您想要新增縮圖，請選取影像旁的&#x200B;**+** **[!UICONTROL 縮圖]**&#x200B;圖示，並導覽至您想要的縮圖。 選取完所有縮圖影像後，選取&#x200B;**[!UICONTROL 儲存]**。

   >[!NOTE]
   >
   >若要新增資產，請選取&#x200B;**[!UICONTROL 新增資產]**。

1. 若要刪除資產，請選取對應的核取方塊，然後選取&#x200B;**[!UICONTROL 刪除資產]**。
1. 若要套用預設集，請選取右上角的&#x200B;**[!UICONTROL 預設集]**，然後選取要套用至資產的預設集。
1. 選取&#x200B;**[!UICONTROL 儲存]**。您建立的混合媒體集會顯示在您建立的資料夾中。

## 編輯混合媒體集 {#editing-mixed-media-sets}

您可以直接在使用者介面[中，對混合媒體集中的資產執行各種編輯工作，就像在Assets](/help/assets/manage-digital-assets.md)中編輯任何資產一樣。 您也可以在「混合媒體集」中執行下列動作：

* 將資產新增至混合媒體集。
* 重新排序混合媒體集中的資產。
* 刪除混合媒體集中的資產。
* 套用檢視器預設集。
* 變更預設縮圖。

**若要編輯混合媒體集：**

1. 執行下列任一項作業：

   * 將游標暫留在混合媒體集資產上，然後選取「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 將滑鼠懸停在混合媒體集資產上，選取「**[!UICONTROL 選取]**」（勾選圖示），然後在工具列上選取「**[!UICONTROL 編輯]**」。

   * 選取混合媒體集資產，然後在工具列上選取&#x200B;**[!UICONTROL 編輯]** （鉛筆圖示）。

1. 在混合媒體集編輯器中，執行下列任一項作業：

   * 若要重新排序資產 — 在左側面板中，選取&#x200B;**[!UICONTROL Assets]** （圖片圖示），將資產拖曳至新位置。
   * 若要新增資產 — 在工具列上，選取[新增資產]。**&#x200B;** 導覽至資產。 針對您要新增的每個資產，將滑鼠指標暫留在資產的影像（而非資產名稱）上，然後選取核取標籤圖示。 在右上角，選取&#x200B;**[!UICONTROL 選取]**。

   * 若要刪除資產 — 在左側面板中，選取&#x200B;**[!UICONTROL Assets]** （圖片圖示），然後選取資產。 在工具列上，選取&#x200B;**[!UICONTROL 刪除資產]**。

   * 若要依名稱遞增或遞減順序排序資產，請在左側面板中選取&#x200B;**[!UICONTROL Assets]** （圖片圖示）。 在&#x200B;**[!UICONTROL Assets]**&#x200B;標題的右側，選取向上或向下插入號圖示。

     >[!NOTE]
     >
     >* 若要刪除整個混合媒體集，請從任何檢視模式（例如&#x200B;**[!UICONTROL 卡片檢視]**&#x200B;或&#x200B;**[!UICONTROL 欄檢視]**）導覽至混合媒體集。 將滑鼠指標暫留在資產上，然後選取核取標籤圖示，讓您可以加以選取。 按鍵盤上的&#x200B;**[!UICONTROL 退格鍵]**，或選取工具列上的&#x200B;**[!UICONTROL 更多]** （三個點），然後選取&#x200B;**[!UICONTROL 刪除]**。
     >
     >* 您可以導覽至混合媒體集，編輯該集中的資產。 在左側邊欄中，選取「**[!UICONTROL 設定成員]**」，然後選取個別資產上的「**[!UICONTROL 鉛筆]**」圖示以開啟編輯視窗。

1. 完成編輯後，選取&#x200B;**[!UICONTROL 儲存]**。

   >[!NOTE]
   >
   >* 若要編輯混合媒體集中的資產 — 導覽至混合媒體集。 選取（不要選取）該集，以便在「Experience Manager集預覽」頁面中將其開啟。 在左側邊欄中，選取向下插入符號以開啟下拉式清單，然後選取&#x200B;**[!UICONTROL 設定成員]**。 在「設定成員」頁面中，將滑鼠指標暫留在資產上，然後選取「**[!UICONTROL 編輯]**」（鉛筆圖示）以開啟編輯頁面。
   >
   >* 要刪除整個混合媒體集 — 從任何檢視模式（例如卡片檢視或欄檢視），導覽至混合媒體集。 將滑鼠指標暫留在集合上，然後選取&#x200B;**[!UICONTROL 選取]** （勾選圖示）。 在鍵盤上按&#x200B;**[!UICONTROL 退格鍵]**，或選取&#x200B;**[!UICONTROL 更多]** （三個點列），然後選取&#x200B;**[!UICONTROL 刪除]**。

## 預覽混合媒體集 {#previewing-mixed-media-sets}

如需如何預覽混合媒體集的詳細資訊，請參閱[預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

## 發佈混合媒體集 {#publishing-mixed-media-sets}

如需如何發佈混合媒體集的詳細資訊，請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

>[!NOTE]
>
>如果混合媒體集在您第一次發佈時沒有完全進入傳送服務，請再次發佈混合媒體集。
