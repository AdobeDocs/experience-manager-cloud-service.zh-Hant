---
title: 混合媒體集
description: 瞭解如何在Dynamic Media使用混合媒體集。
feature: 混合媒體集
topic: 業務從業人員
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 22%

---


# 混合媒體集{#mixed-media-sets}

混合媒體集可讓您在單一簡報中混合提供影像、影像集、回轉集和視訊。

混合媒體集由橫幅指定，並加上單字 **[!UICONTROL MixedMediaSet]**。此外，如果「混合媒體集」已發佈，則會顯示「鉛筆」圖示所指示的發佈日期(以 **[!UICONTROL World]** 圖示指示)與上次修改日期(以 **** Pencil圖示表示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>如需「資產」使用者介面的詳細資訊，請參閱「使用Touch UI](/help/assets/manage-digital-assets.md)管理資產」。[

## 快速入門：混合媒體集{#quick-start-mixed-media-sets}

要使用混合媒體集快速啟動並運行，請執行以下步驟：

1. [上傳您的資產](#uploading-assets)。

   首先，上傳混合媒體集的影像和視訊。如有必要，請建立 [影像集](/help/assets/dynamic-media/image-sets.md)[和回轉集](/help/assets/dynamic-media/spin-sets.md)。由於使用者可在混合媒體集檢視器中放大影像，因此當您選擇影像時，請務必考慮縮放。 請確定影像在最大尺寸中至少為2000像素。

1. [建立混合媒體集。](#creating-mixed-media-sets)

   若要建立混合媒體集，請從「資產」頁面，點選「建立>混合媒體集 **** 」，然後命名該集合，選擇資產，然後選擇影像的顯示順序。

   請參閱[使用選擇器。](/help/assets/dynamic-media/working-with-selectors.md)

1. 視需要設定[混合媒體檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

   管理員可以建立或修改混合媒體集檢視器預設集。若要檢視您的混合媒體與檢視器預設集，請選取混合媒體集，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   若要建立或編輯檢視器預設集，請參閱&#x200B;**[!UICONTROL 工具>資產>檢視器預設集]**。

   請參閱[新增和編輯檢視器預設集。](/help/assets/dynamic-media/managing-viewer-presets.md)

1. [預覽混合媒體集。](#previewing-mixed-media-sets)

   選取「混合媒體集」，您就可以預覽它。 若要在選取的檢視器中檢查混合媒體集，請按一下縮圖圖示。 您可以從左側導軌下拉式選單的&#x200B;**[!UICONTROL 檢視器]**&#x200B;選單中選擇不同的檢視器。

1. [發佈混合媒體集。](#publishing-mixed-media-sets)

   發佈混合媒體集會啟動URL和內嵌字串。 此外，您必須[發佈檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

1. [將URL連結至您的Web應](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 用程 [式或內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

   Adobe Experience Manager資產會建立混合媒體集的URL呼叫，並在您發佈混合媒體集後啟動這些呼叫。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選擇混合媒體集，然後在左側導軌下拉菜單中選擇&#x200B;**[!UICONTROL 查看器]**。

   請參 [閱將混合媒體集連結至網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)[和內嵌視訊或影像檢視器](/help/assets/dynamic-media/embed-code.md)。

如有必要，您可以編輯[混合媒體集](#editing-mixed-media-sets)。 此外，您還可以查看和修改[混合媒體集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

>[!NOTE]
>
>如果建立集時遇到問題，請參閱[疑難排解Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md)。

## 上傳資產 {#uploading-assets}

首先，上傳混合媒體集的影像和視訊。請記住，使用者可以在混合媒體集檢視器中放大影像。 因此，您可以考慮到這種縮放功能來選擇影像。 請確定影像在最大尺寸中至少為2000像素。

此外，如果您想要將回轉集或影像集新增至混合媒體集，也請建立它們。

## 建立混合媒體集{#creating-mixed-media-sets}

您可以將影像、影像集、回轉集和視訊新增至混合媒體集。 在將檔案、影像集和回轉集新增至混合媒體集之前，請確定檔案、影像集和回轉集已準備好發佈。

當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在資產新增後手動重新排序或排序。

**建立混合媒體集**

1. 在「資產」中，導覽至您要建立混合媒體集的位置，然後按一下「建 **[!UICONTROL 立]**」，然後選 **[!UICONTROL 取「混合媒體集」]**。您也可以從包含資產的資料夾內建立資產集。顯示混合媒體集編輯器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在混合媒體集編輯器的&#x200B;**[!UICONTROL 標題]**&#x200B;中，輸入混合媒體集的名稱。 名稱會出現在混合媒體集的橫幅中。 （可選）輸入說明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >建立混合媒體集時，您可以變更混合媒體集縮圖，或允許Experience Manager根據混合媒體集中的資產自動選取縮圖。 若要選取縮圖，請按一下「變更縮圖&#x200B;**[!UICONTROL 」，然後選取任何影像（您也可以導覽至其他檔案夾以尋找影像）。]**&#x200B;如果您已選取縮圖，然後決定要Experience Manager從混合媒體集產生縮圖，請選取「切換至自動縮圖」]**。**[!UICONTROL 

1. 若要選取您要納入混合媒體集的資產，請點選「資產選擇器」。 選擇它們，然後按一下&#x200B;**[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選「回報」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後從工具列點選 **[!UICONTROL 「篩選]** 」圖示。通過選擇「視圖」圖 **[!UICONTROL 標]** ，然後選擇「清單視圖」、「列 **[!UICONTROL 視圖」]**&#x200B;或「卡片視圖 **[!UICONTROL 」來更]******&#x200B;改視圖。

   請參閱[使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. 視需要將資產上或下拖曳至清單以重新排序（必須選取&#x200B;**[!UICONTROL Reorder]**&#x200B;圖示）。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果您想要新增縮圖，請按一 **下影像旁** 的+ **[!UICONTROL 縮圖]** 圖示，並導覽至您想要的縮圖。選取完所有縮圖影像後，按一下「 **[!UICONTROL 儲存]**」。

   >[!NOTE]
   >
   >如果您想要新增資產，請點選&#x200B;**[!UICONTROL 新增資產]**。

1. 若要刪除資產，請選取對應的核取方塊，然後點選「刪除資產」。****
1. 若要套用預設，請點選右上角的&#x200B;**[!UICONTROL Preset]**，然後選取要套用至資產的預設。
1. 按一下「**[!UICONTROL 儲存]**」。您新建立的「混合媒體集」會顯示在您所建立的資料夾中。

## 編輯混合媒體集{#editing-mixed-media-sets}

您可以直接在使用者介面[中，對混合媒體集中的資產執行各種編輯工作，就像對資產](/help/assets/manage-digital-assets.md)中的任何資產一樣。 您也可以在混合媒體集中執行下列動作：

* 將資產新增至混合媒體集。
* 在混合媒體集中重新排序資產。
* 刪除混合媒體集中的資產。
* 套用檢視器預設集。
* 變更預設縮圖。

**要編輯混合媒體集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在「混合媒體集」資產上，然後點選「編輯&#x200B;****」（鉛筆圖示）。
   * 將滑鼠指標暫留在「混合媒體集」資產上，點選「**[!UICONTROL 選擇]**」（勾選圖示），然後點選工具列上的「編輯」。****

   * 點選「Mixed Media Set（混合媒體集）」資產，然後點選工具列上的「Edit（編輯）」**[!UICONTROL （鉛筆圖示）。]**

1. 在混合媒體集編輯器中，執行下列任一操作：

   * 若要重新排序資產——在左側面板中，點選&#x200B;**[!UICONTROL Assets]**（圖片圖示），將資產拖曳至新位置。
   * 若要新增資產——在工具列上，點選&#x200B;**[!UICONTROL 新增資產]**。 導覽至資產。 對於您要新增的每個資產，將滑鼠指標暫留在資產的影像（而非資產名稱）上，然後點選核取標籤圖示。 在右上角，點選&#x200B;**[!UICONTROL 選擇]**。

   * 若要刪除資產——在左側面板中，點選&#x200B;**[!UICONTROL Assets]**（圖片圖示），然後選取資產。 在工具列上，點選「刪除資產」。****

   * 若要依資產名稱的遞增或遞減順序排序，請在左側面板中點選&#x200B;**[!UICONTROL Assets]**（圖片圖示）。 在&#x200B;**[!UICONTROL Assets]**&#x200B;標題的右側，點選上或下脫字元號圖示。

      >[!NOTE]
      >
      >* 要刪除整個混合介質集，請從任何查看模式（如&#x200B;**[!UICONTROL 卡片視圖]**&#x200B;或&#x200B;**[!UICONTROL 列視圖]**）導航到混合介質集。 將滑鼠指標暫留在資產上，然後點選核取標籤圖示以選取它。 按鍵盤上的&#x200B;**[!UICONTROL Backspace]**，或按一下工具欄上的&#x200B;**[!UICONTROL More]**（三個點），然後按一下&#x200B;**[!UICONTROL Delete]**。
         >
         >
      * 您可以導覽至混合媒體集，編輯資產。 在左側導軌中，點選「設定成員」，然後點選個別資產上的「鉛筆」圖示以開啟編輯視窗。********


1. 完成編輯時，點選「**[!UICONTROL 儲存]**」。

   >[!NOTE]
   >
   >* 若要編輯混合媒體集中的資產——導覽至混合媒體集。 點選（不要選取）設定，以在「Experience Manager設定預覽」頁面中開啟該設定。 在左側導軌中，按一下向下插入符號以開啟下拉式清單，然後點選「設定成員&#x200B;**[!UICONTROL 」。]**&#x200B;在「設定成員」頁面中，將滑鼠指標暫留在資產上，然後點選「編輯&#x200B;****」（鉛筆圖示）以開啟編輯頁面。
      >
      >
   * 要刪除整個混合媒體集——從任何查看模式（如卡片視圖或列視圖），導航到混合媒體集。 將滑鼠指標暫留在設定上，然後點選&#x200B;**[!UICONTROL Select]**（勾選圖示）。 按鍵盤上的&#x200B;**[!UICONTROL Backspace]**&#x200B;或點選&#x200B;**[!UICONTROL More]**（三個點列），然後點選&#x200B;**[!UICONTROL Delete]**。


## 預覽混合媒體集{#previewing-mixed-media-sets}

如需如何預覽混合媒體集的詳細資訊，請參閱[預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

## 發佈混合媒體集{#publishing-mixed-media-sets}

如需如何發佈混合媒體集的詳細資訊，請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

>[!NOTE]
>
>如果混合媒體集未在您第一次發佈時完全進入傳送服務，請第二次發佈混合媒體集。

