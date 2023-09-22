---
title: 影像的顏色標記
description: Adobe Experience Manager資產可讓您區分影像中的顏色，並自動將這些差異套用為標籤。 然後，您可以使用這些標籤來搜尋和篩選影像。
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 57d6b50ef5256bf6e8fce84100eed4690b77cb87
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 6%

---

# 影像的顏色標記 {#color-tag-images}

![顏色標籤橫幅](assets/banner-image.png)

Adobe Experience Manager (AEM) Assets使用Adobe Sensei AI功能來區分影像中的顏色，並在擷取時自動將這些差異套用為標籤。 這些標籤會根據影像顏色組合來增強搜尋體驗。

您可以設定標籤到影像的顏色數量（範圍在1到40之間），以便日後可以根據這些顏色搜尋影像。 Experience Manager Assets會根據影像中的顏色涵蓋範圍套用標籤。 您也可以設定顏色標籤的顯示格式。

下圖說明在Experience Manager Assets中設定和管理影像的顏色標籤時所執行的工作順序：

![顏色標記](assets/color-tagging-dfd.gif)

## 支援的檔案格式 {#supported-file-formats-color-tags}

| 檔案格式 | 副檔名 | MIME型別 | 輸入色域 | 支援的來源檔案大小上限 | 支援的最大檔案大小解析度 |
|---|---|---|---|---|---|
| JPEG | .jpg和.jpeg | image/jpeg | sRGB | 15 GB | 20000 × 20000畫素 |
| PNG | .PNG | image/png | sRGB | 15 GB | 20000 × 20000畫素 |
| TIFF | .tif和.tiff | image/tiff | sRGB | 4 GB （受格式規格限制） | 20000 × 20000畫素 |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB （受格式規格限制） | 20000 × 20000畫素 |
| GIF | .gif | image/gif | sRGB | 15 GB | 20000 × 20000畫素 |
| BMP | .bmp | image/bmp | sRGB | 4 GB （受格式規格限制） | 20000 × 20000畫素 |

## 管理顏色標籤屬性 {#manage-color-tagging-properties}

若要管理影像的顏色標籤屬性：

1. 瀏覽至 **[!UICONTROL 「工具>資產>顏色標籤」]**.

   ![顏色標籤屬性](assets/color-tag-settings.png)

1. 在「 」中指定顏色標籤的顯示格式 **[!UICONTROL 顯示格式]** 欄位。 可能的選項包括顏色名稱、RGB或十六進位格式。

1. 指定您要為影像標籤的顏色數目 **[!UICONTROL 限制]** 欄位。 當您檢視影像的屬性時，會顯示這些顏色。 您可以在此欄位中定義介於1到40之間的數字。 此欄位的預設值為10色。

1. 指定在搜尋結果中包含顏色標籤的最小顏色涵蓋範圍百分比 **[!UICONTROL 覆蓋率/優勢臨界值%]** 欄位。 例如，如果影像中紅色顏色的涵蓋範圍是10%，而您在此欄位中定義了9%，當您搜尋紅色影像時，系統就會包含該影像。 不過，如果影像中紅色顏色的涵蓋範圍是10%，而您在此欄位中定義了11%，當您搜尋紅色影像時，系統不會包含該影像。

   您可以在此欄位中指定介於5到100之間的任何數字。 預設值為 11。

   >[!NOTE]
   >
   >Adobe建議在此欄位中使用接近預設值的值。 設定為此欄位設定的高數值（例如，大於25）可能會傳回幾個搜尋結果。 同樣地，設定低數值（例如，小於6）可能會傳回太多搜尋結果，因此可能沒有用處。

1. 按一下「**[!UICONTROL 儲存]**」。


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### 停用顏色標籤 {#disable-color-tagging}

預設會啟用影像的顏色標籤。 您可以在資料夾層級停用顏色標籤。 所有子資料夾都會繼承父資料夾的顏色標籤屬性。

若要停用資料夾層級的顏色標籤：

1. 瀏覽至 **[!UICONTROL Adobe Experience Manager >資產>檔案]**.

1. 選取資料夾並按一下 **[!UICONTROL 屬性]**.

1. 在 **[!UICONTROL 資產處理]** 標籤，導覽至 **[!UICONTROL 影像的顏色標籤]** 資料夾。 從下拉式清單中選取下列其中一個值：

   * 繼承 — 資料夾繼承父資料夾的啟用或停用選項。

   * 啟用 — 為選取的資料夾啟用顏色標籤。

   * 停用 — 停用所選資料夾的顏色標籤。

   ![顏色標籤設定](assets/color-tags-folder.png)

## 設定中繼資料結構以新增智慧顏色標籤元件 {#configure-metadata-schema}

中繼資料結構包含要填寫之特定資訊的特定欄位。 它也包含版面資訊，以便以方便使用的方式顯示中繼資料欄位。 中繼資料屬性包括標題、說明、MIME型別、標籤等。 您可以使用 [!UICONTROL 中繼資料結構Forms] 編輯器以修改現有方案或新增自訂中繼資料方案。

>[!NOTE]
>
>「智慧顏色標籤」欄位可在預設中繼資料結構中使用。 如果您使用自訂的中繼資料結構，請設定結構以新增智慧顏色標籤欄位。

若要將智慧顏色標籤元件新增至中繼資料結構表單編輯器：

1. 瀏覽至 **[!UICONTROL 「工具>資產>中繼資料結構」]**.

1. 選取結構描述名稱，然後按一下 **[!UICONTROL 編輯]**.

1. 拖曳 **[!UICONTROL 智慧顏色標籤]** 從 **[!UICONTROL 建置表單]** 跳至 **[!UICONTROL 中繼資料結構表單編輯器]**.

1. 按一下 **[!UICONTROL 智慧顏色標籤欄位]** 在 **[!UICONTROL 中繼資料結構表單編輯器]**.

1. 在中指定適當的值 **[!UICONTROL 欄位標籤]** 中的欄位 **[!UICONTROL 設定]**  標籤。

1. 按一下「**[!UICONTROL 儲存]**」。

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## DAM中現有影像的顏色標籤 {#color-tags-existing-images}

DAM中的現有影像不會自動加上顏色標籤。 [!UICONTROL 重新處理資產] 手動為其產生顏色標籤。

若要以顏色標籤資產存放庫中存在的影像或資產資料夾（包括子資料夾），請執行下列步驟：

1. 選取 [!DNL Adobe Experience Manager] 標誌，然後選取 [!UICONTROL 導覽] 頁面。

1. 選取 [!UICONTROL 檔案].

1. 在「資產」介面中，導覽至您要套用顏色標籤的資料夾。

1. 選取整個資料夾或特定影像。

1. 選取 ![重新處理資產圖示](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新處理資產] 圖示並選取 [!UICONTROL 完整程式] 選項。

處理完成後，瀏覽至 [!UICONTROL 屬性] 資料夾中任何影像的頁面。 自動新增的標籤會顯示在 [!UICONTROL 智慧顏色標籤] 中的區段 [!UICONTROL 基本] 標籤。


## 檢視影像的智慧顏色標籤 {#view-color-tags}

若要檢視影像的智慧顏色標籤：

1. 瀏覽至 **[!UICONTROL Adobe Experience Manager >資產>檔案]**.

1. 按一下適當的資料夾並選取影像。

1. 選取 **[!UICONTROL 屬性]** 並檢視中的標籤 **[!UICONTROL 智慧顏色標籤]** 欄位。

   ![檢視顏色標籤](assets/view-color-tags.png)

   將滑鼠停留在顏色標籤上，即可檢視 **[!UICONTROL 覆蓋率/優勢臨界值%]** 影像中的顏色。

## 設定AEM Assets色彩述詞 {#configure-search-predicate}

您可以設定影像的搜尋篩選器。 然後，您就可以根據特定顏色來篩選結果，以決定搜尋條件。

>[!NOTE]
>
>僅當您未使用預設搜尋表單時，才設定AEM Assets顏色述詞。

若要設定搜尋篩選器，請使用資產管理員搜尋邊欄建立資產顏色述詞。

若要設定搜尋篩選：

1. 瀏覽至 **[!UICONTROL 「工具>一般>搜尋Forms」]**.

1. 選取 **[!UICONTROL 資產管理搜尋邊欄]** 並按一下 **[!UICONTROL 編輯]**.

1. 拖曳 **[!UICONTROL 資產顏色述詞]** 從 **[!UICONTROL 選取述詞]** 跳至 **[!UICONTROL 搜尋表單編輯器]**.

1. 在中指定適當的值 **[!UICONTROL 欄位標籤]** 中的欄位 **[!UICONTROL 設定]**  標籤。

1. 按一下 **[!UICONTROL 完成]** 以儲存設定。

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## 根據顏色搜尋影像 {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

在設定所有顏色標籤屬性和 [設定資產顏色述詞](#search-images-based-on-colors)，您可以根據作為濾鏡的顏色來搜尋影像。

若要根據顏色搜尋影像：

1. 瀏覽至 **[!UICONTROL 「資產」>「檔案」]**.

1. 選取 **[!UICONTROL 篩選]** 下拉式清單中的。
   ![篩選資產](assets/filter-assets.png)

1. 選取 [AEM Assets色彩述詞](#configure-search-predicate).

1. 拖曳檢色器以選取適當的顏色。 選取的顏色會顯示在檢色器下方的唯讀欄位中。 您可以選取RGB或十六進位作為顏色的顯示格式。

   ![檢色器](assets/color-picker-color-tags.png)

   您可以根據選取的單一顏色來篩選影像。 將選取的顏色當做其中一個智慧顏色標籤，且位於 [覆蓋率/優勢臨界值%](#manage-color-tagging-settings) 會顯示在右窗格中。

1. 按一下搜尋列中的X以清除篩選器。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
