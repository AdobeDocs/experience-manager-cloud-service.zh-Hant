---
title: 階層式中繼資料
description: 本文說明如何定義資產的階層式中繼資料。
contentOwner: AG
feature: Metadata
role: Admin, User
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---

# 階層式中繼資料 {#cascading-metadata}

擷取資產的中繼資料資訊時，使用者會在各種可用欄位中提供資訊。 您可以根據在其他欄位中選取的選項，顯示特定的中繼資料欄位或欄位值。 這類條件式顯示中繼資料稱為階層式中繼資料。 換言之，您可以在特定中繼資料欄位/值與一或多個欄位及/或其值之間建立相依性。

使用中繼資料結構描述來定義顯示階層式中繼資料的規則。 例如，如果您的中繼資料結構描述包含資產型別欄位，您可以根據使用者選取的資產型別定義要顯示的相關欄位集。

以下是您可以定義階層式中繼資料的一些使用案例：

* 需要使用者位置時，根據使用者對國家/地區和州的選擇顯示相關城市名稱。
* 根據使用者選擇的產品類別，在清單中載入相關品牌名稱。
* 根據在另一個欄位中指定的值切換特定欄位的可見度。 例如，如果使用者希望以不同的地址運送出貨，則顯示個別的出貨位址列位。
* 根據在其他欄位中指定的值，將欄位指定為必填欄位。
* 根據在其他欄位中指定的值變更針對特定欄位顯示的選項。
* 根據在其他欄位中指定的值，在特定欄位中設定預設中繼資料值。

## 在[!DNL Experience Manager]中設定階層式中繼資料 {#configure-cascading-metadata-in-aem}

假設您想根據選取的資產型別顯示階層式中繼資料。 部分範例

* 對於視訊，會顯示適用的欄位，例如格式、轉碼器、持續時間等。
* 對於Word或PDF檔案，顯示欄位，例如頁數、作者等。

無論選擇的資產型別為何，都會將版權資訊顯示為必填欄位。

1. 選取[!DNL Experience Manager]標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
1. 在「**[!UICONTROL 結構描述Forms]**」頁面中，選取結構描述表單，然後從工具列選取「**[!UICONTROL 編輯]**」以編輯結構描述。

   ![select_form](assets/select_form.png)

1. （選用）在中繼資料結構編輯器中，建立欄位以進行條件化。 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中指定名稱和屬性路徑。

   若要建立標籤，請選取`+`以新增標籤，然後新增中繼資料欄位。

   ![add_tab](assets/add_tab.png)

1. 新增下拉欄位以取得資產型別。 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中指定名稱和屬性路徑。 新增選擇性說明。

   ![asset_type_field](assets/asset_type_field.png)

1. 機碼值組是提供給表單使用者的選項。 您可以手動或從JSON檔案提供索引鍵/值組。

   * 若要手動指定值，請選取&#x200B;**[!UICONTROL 手動新增]**，然後選取&#x200B;**[!UICONTROL 新增選項]**&#x200B;並指定選項文字和值。 例如，指定視訊、PDF、Word和影像資產型別。

   * 若要從JSON檔案動態擷取值，請選取&#x200B;**[!UICONTROL 透過JSON路徑新增]**&#x200B;並提供JSON檔案的路徑。 當表單呈現給使用者時，[!DNL Experience Manager]會即時擷取機碼值組。

   這兩個選項是互斥的。 您無法從JSON檔案匯入選項並手動編輯。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >新增JSON檔案時，索引鍵/值組不會顯示在中繼資料結構編輯器中，但會顯示在已發佈的表單中。

   >[!NOTE]
   >
   >新增選項時，如果按一下彈出式欄位，介面會扭曲，且選項的刪除圖示會停止運作。 在儲存變更之前，請勿按下拉式清單。 如果您遇到此問題，請儲存結構並再次開啟以繼續編輯。

1. （選用）新增其他必要欄位。 例如，資產型別視訊的格式、轉碼器和持續時間。

   同樣地，為其他資產型別新增相依欄位。 例如，為檔案資產(例如PDF和Word檔案)新增頁面計數和作者欄位。

   ![視訊相依欄位](assets/video_dependent_fields.png)

1. 若要在資產型別欄位與其他欄位之間建立相依性，請選擇相依欄位並開啟&#x200B;**[!UICONTROL 規則]**&#x200B;標籤。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 在&#x200B;**[!UICONTROL 需求]**&#x200B;底下，根據新規則&#x200B;**選項選擇**&#x200B;必要。
1. 選取&#x200B;**[!UICONTROL 新增規則]**&#x200B;並選擇&#x200B;**[!UICONTROL 資產型別]**&#x200B;欄位以建立相依性。 也選擇要在其上建立相依性的欄位值。 在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存變更。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >具有手動預先定義值的下拉式清單可與規則搭配使用。 包含已設定JSON路徑的下拉式功能表，無法搭配使用預先定義值來套用條件的規則使用。 如果值是在執行階段從JSON載入，則無法套用預先定義的規則。

1. 在「可 **[!UICONTROL 見性]**」下，選擇「可 **[!UICONTROL 見」，根據新規則選項]** 。

1. 選取&#x200B;**[!UICONTROL 新增規則]**&#x200B;並選擇&#x200B;**[!UICONTROL 資產型別]**&#x200B;欄位以建立相依性。 也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存變更。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >若要重設值，請在介面中選取值以外的任何位置。 如果值已重設，請再次選取值。

   >[!NOTE]
   >
   >您可以套用 **[!UICONTROL 「需求]** 」條件 **[!UICONTROL 和「可見性]** 」條件，它們彼此獨立。

1. 同樣地，在「資產型別」欄位中的「視訊」值與其他欄位（例如「轉碼器」和「持續時間」）之間建立相依性。
1. 重複這些步驟，在[!UICONTROL 資產型別]欄位和[!UICONTROL 頁面計數]和[!UICONTROL 作者]等欄位中，建立檔案資產(PDF和Word)之間的相依性。
1. 按一下「**[!UICONTROL 儲存]**」。將中繼資料結構套用至資料夾。

1. 導覽至您套用中繼資料結構的資料夾，並開啟資產的屬性頁面。 視您在「資產型別」欄位中的選擇而定，會顯示相關的階層式中繼資料欄位。

   ![視訊資產的階層式中繼資料](assets/video_asset.png)
   *圖：視訊資產*&#x200B;的階層式中繼資料

   ![檔案資產](assets/doc_type_fields.png)的階層式中繼資料
   *圖：檔案資產*&#x200B;的階層式中繼資料

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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
