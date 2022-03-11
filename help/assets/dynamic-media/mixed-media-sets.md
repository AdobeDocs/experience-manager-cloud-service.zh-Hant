---
title: 混合媒體集
description: 瞭解如何在Dynamic Media處理混合媒體集。
feature: Mixed Media Sets
role: User
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: b31fa5af7bcaa944d8bd7b0bb7d7b8deb36906a8
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 11%

---

# 混合媒體集{#mixed-media-sets}

混合媒體集使您能夠在一個演示文稿中提供影像、影像集、旋轉集和視頻的混合。

混合媒體集由橫幅指定，並加上單字 **[!UICONTROL MixedMediaSet]**。此外，如果「混合媒體集」已發佈，則會顯示「鉛筆」圖示所指示的發佈日期(以 **[!UICONTROL World]** 圖示指示)與上次修改日期(以 **** Pencil圖示表示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>有關Assets用戶介面的資訊，請參閱 [使用Touch UI管理資產](/help/assets/manage-digital-assets.md)。

## 快速啟動：混合媒體集 {#quick-start-mixed-media-sets}

要使用混合媒體集快速啟動並運行，請執行以下步驟：

1. [上載資產](#uploading-assets)。

   首先，上傳混合媒體集的影像和視訊。如有必要，請建立 [影像集](/help/assets/dynamic-media/image-sets.md)[和回轉集](/help/assets/dynamic-media/spin-sets.md)。由於用戶可以在混合媒體集查看器中放大影像，因此，在選擇影像時，請確保對縮放進行了說明。 確保影像在最大大小中至少為2000像素。

   請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 清單。

1. [建立混合媒體集](#creating-mixed-media-sets)。

   要建立混合媒體集，請從「資產」頁轉到 **[!UICONTROL 建立]** > **[!UICONTROL 混合媒體集]** 然後命名集，選擇資產，然後選擇影像的顯示順序。

   請參閱 [使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 設定 [混合媒體查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)，根據需要。

   管理員可以建立或修改混合媒體集檢視器預設集。若要檢視您的混合媒體與檢視器預設集，請選取混合媒體集，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   要建立或編輯查看器預設，請導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 查看器預設]**。

   請參閱 [添加和編輯查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)。

1. [預覽混合媒體集](#previewing-mixed-media-sets)。

   選擇「混合媒體集」，您可以預覽它。 要在選定的查看器中檢查混合媒體集，請選擇縮略圖表徵圖。 您可以從 **[!UICONTROL 查看者]** 菜單開啟它。

1. [發佈混合媒體集](#publishing-mixed-media-sets)。

   發佈混合媒體集將激活URL和嵌入字串。 此外，您必須 [發佈查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

1. [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 或 [嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。

   Adobe Experience Manager資產為混合媒體集建立URL調用，並在發佈混合媒體集後激活它們。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們嵌入到您的網站中。

   選擇「Mixed Media Set（混合媒體集）」 ，然後在左滑軌下拉菜單中，選擇 **[!UICONTROL 查看者]**。

   請參閱 [將混合媒體集連結到網頁](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) 和 [嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。

如有必要，可以編輯 [混合媒體集](#editing-mixed-media-sets)。 此外，您還可以查看和修改 [混合媒體集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

>[!NOTE]
>
>如果建立集時遇到問題，請參閱 [排除Dynamic Media故障](/help/assets/dynamic-media/troubleshoot-dm.md)。

## 上載資產 {#uploading-assets}

首先，上傳混合媒體集的影像和視訊。請記住，用戶可以在混合媒體集查看器中放大影像。 因此，在選擇具有此縮放功能的影像時應牢記這一點。 確保影像在最大大小中至少為2000像素。

此外，如果要將旋轉集或映像集添加到混合介質集，也可建立它們。

請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/file-format-support.md#image-support-dynamic-media) 清單。

## 建立混合媒體集 {#creating-mixed-media-sets}

您可以將影像、影像集、旋轉集和視頻添加到混合媒體集。 在將檔案、映像集和旋轉集添加到混合媒體集之前，請確保已準備好發佈它們。

在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或對其排序。

**建立混合媒體集：**

1. 在資產中，導航到要建立混合介質集的位置，然後選擇 **[!UICONTROL 建立]**，然後選擇 **[!UICONTROL 混合媒體集]**。 您也可以從包含資產的資料夾內建立資產集。顯示混合媒體集編輯器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在混合媒體集編輯器中，在 **[!UICONTROL 標題]**，輸入混合媒體集的名稱。 該名稱出現在混合媒體集的標題中。 （可選）輸入說明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >建立混合媒體集時，可以更改混合媒體集縮略圖，或允許Experience Manager根據混合媒體集中的資產自動選擇縮略圖。 要選擇縮略圖，請選擇 **[!UICONTROL 更改縮略圖]** 並選擇任何影像（您也可以導航到其他資料夾以查找影像）。 如果已選擇縮略圖，則決定要Experience Manager從混合媒體集生成縮略圖，請選擇 **[!UICONTROL 切換到自動縮略圖]**。

1. 要選擇要包括在混合媒體集中的資產，請選擇資產選擇器。 選擇它們並選擇 **[!UICONTROL 選擇]**。

   使用資產選擇器，可以通過鍵入關鍵字並選擇 **[!UICONTROL 返回]**。 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後選擇 **[!UICONTROL 篩選]** 的子菜單。 通過選擇「視圖」圖 **[!UICONTROL 標]** ，然後選擇「清單視圖」、「列 **[!UICONTROL 視圖」]**&#x200B;或「卡片視圖 **[!UICONTROL 」來更]******&#x200B;改視圖。

   請參閱 [使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. 通過向上或向下拖動資產(必須選擇 **[!UICONTROL 重新排序]** 表徵圖)。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果要添加縮略圖，請選擇 **+** **[!UICONTROL 縮略圖]** 表徵圖，然後導航到所需的縮略圖。 選擇完所有縮略圖後，選擇 **[!UICONTROL 保存]**。

   >[!NOTE]
   >
   >如果要添加資產，請選擇 **[!UICONTROL 添加資產]**。

1. 要刪除資產，請選中相應的複選框並選擇 **[!UICONTROL 刪除資產]**。
1. 要應用預設，請選擇 **[!UICONTROL 預設]** ，然後選擇要應用於資產的預設。
1. 選擇 **[!UICONTROL 保存]**。 新建立的「混合媒體集」會顯示在您建立的資料夾中。

## 編輯混合媒體集 {#editing-mixed-media-sets}

您可以直接在用戶介面中對混合媒體集中的資產執行各種編輯任務 [就像你在資產中](/help/assets/manage-digital-assets.md)。 也可以在「混合介質集」中執行以下操作：

* 將資產添加到混合媒體集。
* 對混合媒體集中的資產重新排序。
* 刪除混合媒體集中的資產。
* 應用查看器預設。
* 更改預設縮略圖。

**編輯混合媒體集：**

1. 執行下列任一操作：

   * 將滑鼠懸停在混合媒體集資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。
   * 將滑鼠懸停在混合媒體集資產上，選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖），然後選擇 **[!UICONTROL 編輯]** 的上界。

   * 選擇混合介質集資產，然後選擇 **[!UICONTROL 編輯]** 表徵圖)。

1. 在「混合媒體集編輯器」中，執行下列任一操作：

   * 重新排序資產 — 在左側面板中，選擇 **[!UICONTROL 資產]** （圖片表徵圖），將資產拖動到新位置。
   * 添加資產 — 在工具欄上，選擇 **[!UICONTROL 添加資產]**。 定位至資產。 對於要添加的每個資產，將滑鼠懸停在資產的影像上（而不是資產的名稱），然後選擇複選標籤表徵圖。 在右上角，選擇 **[!UICONTROL 選擇]**。

   * 要刪除資產 — 在左面板中，選擇 **[!UICONTROL 資產]** （圖片表徵圖），然後選擇資產。 在工具欄上，選擇 **[!UICONTROL 刪除資產]**。

   * 要按資產名稱按升序或降序排序，請在左側面板中選擇 **[!UICONTROL 資產]** （圖片表徵圖）。 在 **[!UICONTROL 資產]** 標題，選擇插入符號上下表徵圖。

      >[!NOTE]
      >
      >* 從任何查看模式(如 **[!UICONTROL 卡視圖]** 或 **[!UICONTROL 列視圖]**)導航到「Mixed Media Set（混合媒體集）」。 將滑鼠懸停在資產上，然後選擇複選標籤表徵圖，以便選擇它。 按 **[!UICONTROL 回空格]** 或選擇 **[!UICONTROL 更多]** （三點），然後選擇 **[!UICONTROL 刪除]**。
      >
      >* 通過導航到混合媒體集，可以編輯該集中的資產。 在左滑軌中，選擇 **[!UICONTROL 設定成員]**，然後選擇 **[!UICONTROL 鉛筆]** 表徵圖以開啟編輯窗口。


1. 選擇 **[!UICONTROL 保存]** 編輯。

   >[!NOTE]
   >
   >* 編輯混合介質集中的資產 — 導航到混合介質集。 點擊（不選擇）該集，以便可以在「Experience Manager集預覽」頁中開啟它。 在左滑軌中，選擇向下插入符號以開啟下拉清單，然後選擇 **[!UICONTROL 設定成員]**。 在「設定成員」頁中，懸停在資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）以開啟編輯頁面。
   >
   >* 要刪除整個混合介質集 — 從任何查看模式（如卡視圖或列視圖），導航到混合介質集。 懸停在集上，然後選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖）。 按 **[!UICONTROL 回空格]** 鍵盤上，或選擇 **[!UICONTROL 更多]** （三點行），然後選擇 **[!UICONTROL 刪除]**。


## 預覽混合媒體集 {#previewing-mixed-media-sets}

請參閱 [預覽資產](/help/assets/dynamic-media/previewing-assets.md) 的子菜單。

## 發佈混合媒體集 {#publishing-mixed-media-sets}

請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 的子菜單。

>[!NOTE]
>
>如果混合媒體集在您第一次發佈時未完全到達傳遞服務，則第二次發佈混合媒體集。
