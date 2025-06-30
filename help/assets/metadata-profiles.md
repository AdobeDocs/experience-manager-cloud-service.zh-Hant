---
title: 中繼資料設定檔
description: 瞭解資產的中繼資料設定檔。 瞭解如何建立中繼資料設定檔，並將其套用至資料夾資產。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 21%

---

# 中繼資料設定檔 {#metadata-profiles}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料設定檔，並將其套用至資料夾。 您之後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

在Experience Manager Assets中使用設定檔的重要概念是，設定檔會指派給資料夾。 設定檔中的設定為中繼資料設定檔的形式，以及視訊設定檔或影像設定檔。 這些設定會處理資料夾的內容及其任何子資料夾。 因此，您如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案對於設定檔處理這些資產的方式有重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料做法，您可以充分利用數位資產集合，並確保由正確的設定檔處理正確的檔案。

## 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**，然後按一下&#x200B;**[!UICONTROL 建立]**。
1. 輸入中繼資料設定檔的標題，例如「範例中繼資料」，然後選取&#x200B;**[!UICONTROL 提交]**。 此時會顯示中繼資料設定檔的編輯表單。
1. 按一下元件，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中設定其屬性。 例如，按一下&#x200B;**[!UICONTROL Description]**&#x200B;元件並編輯其屬性。
編輯&#x200B;**[!UICONTROL Description]**&#x200B;元件的下列屬性：

   * **[!UICONTROL 欄位標籤]** — 中繼資料屬性的顯示名稱。 僅供使用者參考。
   * **[!UICONTROL 對應到屬性]** — 此屬性的值提供儲存於存放庫中的資產節點相對路徑/名稱。 此值應一律以`./`開頭，因為它表示路徑在資產的節點下。

     您為&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;指定的值會儲存為資產中繼資料節點下的屬性。 例如，如果您指定。`/jcr:content/metadata/dc:desc`作為&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;的名稱，[!DNL Adobe Experience Manager Assets]會將值`dc:desc`儲存在資產的中繼資料節點。

   * **[!UICONTROL 預設值]** — 使用此屬性為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，此值就會指派給資產中繼資料節點上的屬性`dc:desc`。

     >[!NOTE]
     >
     >將預設值新增至新的中繼資料屬性（不存在於`/jcr:content/metadata`節點）時，預設不會在資產的「屬性」頁面上顯示屬性及其值。 若要在[!UICONTROL 屬性]頁面上檢視新屬性，請修改對應的結構描述表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
|------------------|----------------------------------------------------|
| 區段標題 | 欄位標籤，說明 |
| 單行文字 | 欄位標籤，對應至屬性，預設值 |
| 多值文字 | 欄位標籤，對應至屬性，預設值 |
| 數字 | 欄位標籤，對應至屬性，預設值 |
| 日期 | 欄位標籤，對應至屬性，預設值 |
| 標準標記 | 欄位標籤，對應至屬性，預設值，說明 |

1. 按一下&#x200B;**[!UICONTROL 完成]**。 已將中繼資料設定檔新增至&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面中的設定檔清單。

## 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面中，選取一個中繼資料設定檔以製作其副本。
1. 按一下工具列中的&#x200B;**[!UICONTROL 複製]**。
1. 在&#x200B;**[!UICONTROL 複製中繼資料設定檔]**&#x200B;對話方塊中，輸入新中繼資料設定檔副本的標題。
1. 按一下「**[!UICONTROL 複製]**」。中繼資料設定檔的復本會顯示在「中繼資料設定檔」頁面的設定檔 **[!UICONTROL 清單中]** 。

## 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面，選取要刪除的設定檔。
1. 按一下工具列中的&#x200B;**[!UICONTROL 刪除中繼資料設定檔]**。
1. 在對話方塊中，按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認刪除作業。 中繼資料設定檔會從清單中刪除。

## 將中繼資料設定檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

將中繼資料描述檔指派給資料夾時，所有子資料夾都會自動從其父資料夾繼承描述檔。 將不同的設定檔套用至子資料夾時，繼承即會停止。 您只能將一個中繼資料設定檔指派至資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的中繼資料描述檔指派給資料夾，則新的描述檔會覆寫先前的描述檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至變更後新增至資料夾的資產。 您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

在使用者介面中，會以卡片名稱中顯示的設定檔名稱來指出已指派設定檔的資料夾。

若資料夾中已有您後來加以變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。<!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將中繼資料設定檔套用至特定資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料設定檔&#x200B;**[!UICONTROL 應用到資料夾]**&#x200B;**&#x200B;**。本節說明如何以兩種方式將中繼資料設定檔套用至資料夾。

已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 從「設定檔」使用者介面將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets >中繼資料設定檔]**。
1. 選取您要套用至一或多個資料夾的中繼資料設定檔。
1. 按一下&#x200B;**[!UICONTROL 將中繼資料設定檔套用至資料夾]**，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，並按一下&#x200B;**[!UICONTROL 完成]**。 已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

#### 從「屬性」將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側邊欄中，按一下&#x200B;**[!UICONTROL Assets]**，然後導覽至您要套用中繼資料設定檔的資料夾。
1. 在資料夾中，選取核取記號以選取資料夾，然後選取&#x200B;**屬性**。
1. 選取「**[!UICONTROL 中繼資料描述檔]**」標籤，然後從下拉式選單中選取描述檔，然後按一下「**[!UICONTROL 儲存]**」。 已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

### 全域套用中繼資料設定檔 {#applying-a-metadata-profile-globally}

除了將設定檔套用至資料夾之外，您也可以全域套用設定檔，以便任何資料夾中上傳至[!DNL Experience Manager Assets]的任何內容皆已套用選取的設定檔。

若資料夾中已有您後來加以變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全域套用中繼資料設定檔，請執行下列其中一項動作**

* 瀏覽至`https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam`並套用適當的設定檔，然後按一下&#x200B;**[!UICONTROL 儲存]**。

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`。 新增屬性`metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`。 按一下&#x200B;**「儲存全部」**。

## 從資料夾中移除中繼資料設定檔 {#removing-a-metadata-profile-from-folders}

當您從資料夾中移除中繼資料描述檔時，任何子資料夾都會自動繼承其父資料夾中描述檔的移除作業。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料設定檔，或從「屬性」中移除中繼資料設定檔，或從「屬性」中移除中繼資料設定檔，或從「工具」**功能表** 移除中繼資料設定檔 **&#x200B;**。本節將說明如何以兩種方式從資料夾中移除中繼資料設定檔。

### 透過設定檔使用者介面從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具> Assets >中繼資料設定檔]**。
1. 選取您要從資料夾或多個資料夾移除的中繼資料設定檔。
1. 按一下&#x200B;**[!UICONTROL 從資料夾移除中繼資料描述檔]**，然後選取您要用來從中移除描述檔的資料夾或多個資料夾，並按一下&#x200B;**[!UICONTROL 完成]**。

   您可以確認中繼資料描述檔不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下Experience Manager標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後移至您要從中移除中繼資料設定檔的資料夾。
1. 在資料夾上，按一下核取記號以選取資料夾，然後按一下&#x200B;**[!UICONTROL 內容]**。
1. 選擇&#x200B;**[!UICONTROL 「元資料設定檔」]**&#x200B;標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無」]**，然後按一下&#x200B;**[!UICONTROL 「儲存」]**。已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

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
