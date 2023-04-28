---
title: 階層式中繼資料
description: 本文說明如何定義資產的階層式中繼資料。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 14%

---

# 階層式中繼資料 {#cascading-metadata}

擷取資產的中繼資料資訊時，使用者會在各種可用欄位中提供資訊。 您可以顯示與在其他欄位中選取的選項相關的特定中繼資料欄位或欄位值。 這種元資料的條件顯示稱為級聯元資料。 換言之，您可以在特定中繼資料欄位/值與一或多個欄位及/或其值之間建立相依性。

使用中繼資料結構來定義顯示階層式中繼資料的規則。 例如，如果您的中繼資料結構包含資產類型欄位，您可以根據使用者選取的資產類型，定義要顯示的相關欄位集。

以下是您可以定義階層式中繼資料的一些使用案例：

* 如果需要使用者位置，請根據使用者的國家/地區和州選擇，顯示相關的城市名稱。
* 根據使用者對產品類別的選擇，將相關品牌名稱載入清單中。
* 根據在另一個欄位中指定的值，切換特定欄位的可見性。 例如，如果用戶希望將發運傳送到不同地址，則顯示單獨的發運地址欄位。
* 根據其他欄位中指定的值，將欄位指定為必填欄位。
* 根據在另一個欄位中指定的值，變更特定欄位所顯示的選項。
* 根據其他欄位中指定的值，在特定欄位中設定預設中繼資料值。

## 在中設定階層式中繼資料 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

假設您要根據選取的資產類型顯示階層式中繼資料。 一些範例

* 對於視訊，顯示適用的欄位，例如格式、轉碼器、持續時間等。
* 對於Word或PDF文檔，顯示欄位，如頁數、作者等。

無論選擇的資產類型為何，都將版權資訊顯示為必填欄位。

1. 點選/按一下 [!DNL Experience Manager] 標誌，然後 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 在「方 **[!UICONTROL 案表單]** 」頁中，選擇方案表單，然後從工具欄點選/單 **[!UICONTROL 擊「編輯]** 」以編輯方案。

   ![select_form](assets/select_form.png)

1. （選用）在中繼資料結構編輯器中，建立新欄位以條件化。 在 **[!UICONTROL 設定]** 標籤。

   若要建立新標籤，請點選/按一下 `+` 新增索引標籤，然後新增中繼資料欄位。

   ![add_tab](assets/add_tab.png)

1. 為資產類型新增下拉式清單欄位。 在 **[!UICONTROL 設定]** 標籤。 新增選用說明。

   ![asset_type_field](assets/asset_type_field.png)

1. 機碼值組是提供給表單使用者的選項。 您可以手動或從JSON檔案提供索引鍵值配對。

   * 若要手動指定值，請選取 **[!UICONTROL 手動新增]**，然後點選/按一下 **[!UICONTROL 添加選擇]** 和指定選項文本和值。 例如，指定視訊、PDF、字詞和影像資產類型。

   * 若要動態從JSON檔案擷取值，請選取 **[!UICONTROL 透過JSON路徑新增]** 和提供JSON檔案的路徑。 [!DNL Experience Manager] 當表單顯示給使用者時，會即時擷取機碼值組。

   兩個選項互斥。 您無法從JSON檔案匯入選項並手動編輯。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >新增JSON檔案時，索引鍵值配對不會顯示在中繼資料結構編輯器中，但可在已發佈的表單中使用。

   >[!NOTE]
   >
   >添加選擇時，如果按一下彈出欄位，介面將失真，選擇的刪除表徵圖將停止工作。 儲存變更前，請勿按一下下拉式清單。 如果您遇到此問題，請儲存結構並再次開啟以繼續編輯。

1. （選用）新增其他必填欄位。 例如，資產類型視訊的格式、編碼解碼器和持續時間。

   同樣地，為其他資產類型新增相依欄位。 例如，為檔案資產(例如PDF和Word檔案)新增欄位頁數和作者。

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 要在資產類型欄位和其他欄位之間建立相關性，請選擇相依欄位並開啟 **[!UICONTROL 規則]** 標籤。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 在 **[!UICONTROL 需求]**，選擇 **[!UICONTROL 必要，根據新規則]** 選項。
1. 點選/按一 **[!UICONTROL 下「新增規則]** 」，然後選擇「 **** 資產類型」欄位以建立相依性。也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。點選/按一 **[!UICONTROL 下「完成]** 」以儲存變更。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >含有手動預先定義值的下拉式清單可與規則搭配使用。 具有已設定JSON路徑的下拉式功能表無法搭配使用預先定義值來套用條件的規則使用。 如果值在執行階段從JSON載入，則無法套用預先定義的規則。

1. 在「可 **[!UICONTROL 見性]**」下，選擇「可 **[!UICONTROL 見」，根據新規則選項]** 。

1. 點選/按一 **[!UICONTROL 下「新增規則]** 」，然後選擇「 **** 資產類型」欄位以建立相依性。也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。點選/按一 **[!UICONTROL 下「完成]** 」以儲存變更。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >若要重設值，請按一下或點選介面上空白字元或值以外的任何位置。 如果重設值，請再次選取值。

   >[!NOTE]
   >
   >您可以套用 **[!UICONTROL 「需求]** 」條件 **[!UICONTROL 和「可見性]** 」條件，它們彼此獨立。

1. 同樣地，在「資產類型」欄位中的「視訊」值與其他欄位（例如「編碼解碼器」和「持續時間」）之間建立相依性。
1. 重複下列步驟，在 [!UICONTROL 資產類型] 欄位和欄位，例如 [!UICONTROL 頁數] 和 [!UICONTROL 作者].
1. 按一下「**[!UICONTROL 儲存]**」。將中繼資料結構套用至資料夾。

1. 導覽至您套用中繼資料結構的資料夾，然後開啟資產的屬性頁面。 視您在「資產類型」欄位中的選擇而定，會顯示相關的階層式中繼資料欄位。

   ![視訊資產的階層式中繼資料](assets/video_asset.png)
   *圖：視訊資產的階層式中繼資料*

   ![檔案資產的階層式中繼資料](assets/doc_type_fields.png)
   *圖：檔案資產的階層式中繼資料*

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [Assets支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連線資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
