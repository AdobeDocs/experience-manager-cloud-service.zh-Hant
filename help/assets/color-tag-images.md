---
title: 影像的顏色標籤
description: Experience Manager Assets使您能夠區分影像中的顏色，並自動將這些顏色作為標籤應用。 然後，可以使用這些標籤來搜索和篩選影像。
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 2859fa68713b46083314d207abc4dec2e088a173
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 3%

---

# 影像的顏色標籤 {#color-tag-images}

![顏色標籤橫幅](assets/banner-image.png)

Experience Manager Assets使用Adobe SenseiAI功能來區分影像中的顏色，並在攝取時自動將這些顏色作為標籤。 這些標籤基於影像顏色合成，支援增強的搜索體驗。

您可以配置標籤到影像的顏色數量，以便以後可以根據這些顏色搜索影像。 Experience Manager Assets根據影像中的顏色覆蓋率應用標籤。 也可以配置顏色標籤的顯示格式。

下圖說明了在Experience Manager Assets為影像配置和管理顏色標籤時所執行的任務的順序：

![顏色標記](assets/color-tagging-dfd.gif)

## 支援的檔案格式 {#supported-file-formats-color-tags}

| 檔案格式 | 副檔名 | MIME類型 | 輸入顏色空間 | 支援的最大源檔案大小 | 支援的最大檔案大小解析 |
|---|---|---|---|---|---|
| JPEG | .jpg,.jpeg | image/jpeg | sRGB | 15GB | 20000px X 20000px |
| PNG | .PNG | image/png | sRGB | 15GB | 20000px X 20000px |
| TIFF | .tif, .tiff | image/tiff | sRGB | 4GB（受格式規範限制） | 20000px X 20000px |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB（受格式規範限制） | 20000px X 20000px |
| GIF | .gif | image/gif | sRGB | 15GB | 20000px X 20000px |
| BMP | .bmp | image/bmp | sRGB | 4 GB（受格式規範限制） | 20000px X 20000px |

## 管理顏色標籤屬性 {#manage-color-tagging-properties}

要管理影像的顏色標籤屬性：

1. 導航到 **[!UICONTROL 「工具」>「資產」>「顏色標籤」]**。

   ![顏色標籤屬性](assets/color-tag-settings.png)

1. 為中的顏色標籤指定顯示格式 **[!UICONTROL 顯示格式]** 的子菜單。 可能的選項包括顏色名稱、RGB或HEX格式。

1. 為中的影像指定要標籤的顏色數 **[!UICONTROL 限制]** 的子菜單。 當您查看影像的屬性時，這些顏色將顯示。  您可以在此欄位中定義介於1和40之間的數字。 此欄位的預設值為十種顏色。

1. 指定最小顏色覆蓋率百分比以在搜索結果中包含顏色標籤 **[!UICONTROL 覆蓋率/優勢閾值%]** 的子菜單。 例如，如果影像中紅色的覆蓋率為10%，並且您在此欄位中定義了9%，則搜索具有紅色的影像時會包括影像。 但是，如果影像中紅色的覆蓋率為10%，而您在此欄位中定義了11%，則搜索具有紅色的影像時不會包括影像。

   您可以在此欄位中指定介於5和0之間的任意數字。 預設值為11。

   >[!NOTE]
   >
   >Adobe建議使用此欄位中接近預設值的值。 為此欄位設定高數值（例如，大於25）可能返回很少的搜索結果。 同樣，設定一個低數值（例如，小於6）可能會返回太多的搜索結果，這可能沒有用處。

1. 按一下「**[!UICONTROL 儲存]**」。


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### 禁用顏色標籤 {#disable-color-tagging}

預設情況下會啟用影像的顏色標籤。 可以在資料夾級別禁用顏色標籤。 所有子資料夾都從父資料夾繼承顏色標籤屬性。

要在資料夾級別禁用顏色標籤，請執行以下操作：

1. 導航到 **[!UICONTROL Adobe Experience Manager>資產>檔案]**。

1. 選擇資料夾並按一下 **[!UICONTROL 屬性]**。

1. 在 **[!UICONTROL 資產處理]** 頁籤，導航到 **[!UICONTROL 影像的顏色標籤]** 的子菜單。 從下拉清單中選擇以下值之一：

   * 繼承 — 資料夾從父資料夾繼承啟用或禁用選項。

   * 啟用 — 為所選資料夾啟用顏色標籤。

   * 禁用 — 禁用所選資料夾的顏色標籤。

   ![顏色標籤設定](assets/color-tags-folder.png)

## 配置元資料架構以添加智慧顏色標籤元件 {#configure-metadata-schema}

元資料架構包含要填寫的特定資訊的特定欄位。 它還包含佈局資訊，以用戶友好的方式顯示元資料欄位。 元資料屬性包括標題、說明、MIME類型、標籤等。 您可以使用 [!UICONTROL 元資料架構Forms] 編輯器以修改現有架構或添加自定義元資料架構。

>[!NOTE]
>
>預設元資料架構中提供了「智慧顏色標籤」欄位。 如果使用自定義元資料架構，請將架構配置為添加智慧顏色標籤欄位。

要將智慧顏色標籤元件添加到元資料架構表單編輯器中，請執行以下操作：

1. 導航到 **[!UICONTROL 「工具」>「資產」>「元資料架構」]**。

1. 選擇架構名稱並按一下 **[!UICONTROL 編輯]**。

1. 拖動 **[!UICONTROL 智慧顏色標籤]** 從 **[!UICONTROL 生成窗體]** 頁籤 **[!UICONTROL 元資料架構窗體編輯器]**。

1. 按一下 **[!UICONTROL 智慧顏色標籤欄位]** 的 **[!UICONTROL 元資料架構窗體編輯器]**。

1. 在 **[!UICONTROL 欄位標籤]** 的 **[!UICONTROL 設定]**  頁籤。

1. 按一下「**[!UICONTROL 儲存]**」。

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## DAM中現有影像的顏色標籤 {#color-tags-existing-images}

DAM中已有的影像不會自動進行顏色標籤。 你需要 [!UICONTROL 重新處理資產] 手動為其生成顏色標籤。

要為資產儲存庫中已存在的資產的標籤影像或資料夾（包括子資料夾）添加顏色，請執行以下步驟：

1. 選擇 [!DNL Adobe Experience Manager] 標識，然後從 [!UICONTROL 導航] 的子菜單。

1. 選擇 [!UICONTROL 檔案] 顯示「資產」介面。

1. 導航到要應用顏色標籤的資料夾。

1. 選擇整個資料夾或特定影像。

1. 選擇 ![「重新處理資產」表徵圖](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新處理資產] 表徵圖，然後選擇 [!UICONTROL 完整流程] 的雙曲餘切值。

流程完成後，導航到 [!UICONTROL 屬性] 資料夾中任何影像的頁面。 在中可看到自動添加的標籤 [!UICONTROL 智慧顏色標籤] 部分 [!UICONTROL 基本] 頁籤。


## 查看影像的智慧顏色標籤 {#view-color-tags}

要查看影像的智慧顏色標籤，請執行以下操作：

1. 導航到 **[!UICONTROL Adobe Experience Manager>資產>檔案]**。

1. 按一下相應的資料夾並選擇影像。

1. 選擇 **[!UICONTROL 屬性]** 並查看 **[!UICONTROL 智慧顏色標籤]** 的子菜單。

   ![查看顏色標籤](assets/view-color-tags.png)

   將滑鼠懸停在顏色標籤上以查看 **[!UICONTROL 覆蓋率/優勢閾值%]** 的下界。

## 配置AEM Assets顏色謂詞 {#configure-search-predicate}

可以配置影像的搜索篩選器。 然後，您可以根據特定顏色來篩選結果。

>[!NOTE]
>
>僅在不使用預設搜索表單時配置AEM Assets顏色謂詞。

要配置搜索篩選器，請使用資產管理搜索導軌建立資產顏色謂詞。

配置搜索篩選器：

1. 導航到 **[!UICONTROL 工具>常規>搜索Forms]**。

1. 選擇 **[!UICONTROL 資產管理搜索欄]** 按一下 **[!UICONTROL 編輯]**。

1. 拖動 **[!UICONTROL 資產顏色謂詞]** 從 **[!UICONTROL 選擇謂詞]** 頁籤 **[!UICONTROL 搜索表單編輯器]**。

1. 在 **[!UICONTROL 欄位標籤]** 的 **[!UICONTROL 設定]**  頁籤。

1. 按一下 **[!UICONTROL 完成]** 按鈕。

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## 根據顏色搜索影像 {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

配置所有顏色標籤屬性和 [配置資產顏色謂詞](#search-images-based-on-colors)，可以根據顏色作為濾鏡搜索影像。

要根據顏色搜索影像：

1. 導航到 **[!UICONTROL 資產>檔案]**。

1. 選擇 **[!UICONTROL 篩選]** 清單中。
   ![篩選資產](assets/filter-assets.png)

1. 選擇 [AEM Assets色謂語](#configure-search-predicate)。

1. 拖動顏色選取器以選擇適當的顏色。 所選顏色顯示在顏色選取器下方的只讀欄位中。 可以選擇RGB或十六進位作為顏色的顯示格式。

   ![檢色器](assets/color-picker-color-tags.png)

   可以根據選擇的一種顏色來過濾影像。 將選定顏色作為智慧顏色標籤之一且位於 [覆蓋/佔優閾值%](#manage-color-tagging-settings) 顯示。

1. 在「搜索」欄中按一下x以清除篩選器。
