---
title: 中繼資料設定檔
description: 了解資產的中繼資料設定檔。 了解如何建立中繼資料設定檔，並將其套用至資料夾資產。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 19%

---

# 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾內的資產。 建立中繼資料描述檔並將其套用至資料夾。 您隨後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

有關在Experience Manager Assets中使用設定檔的重要概念，是將它們指派給資料夾。 設定檔中是中繼資料設定檔的設定，以及視訊設定檔或影像設定檔。 這些設定會處理資料夾的內容及其任何子資料夾。 因此，為檔案和資料夾命名的方式、子資料夾排列方式以及這些資料夾內檔案的處理方式，都會對設定檔處理這些資產的方式產生重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可充份運用數位資產集合，並確保正確的設定檔能處理正確的檔案。

## 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**，然後按一下 **[!UICONTROL 建立]**.
1. 輸入中繼資料描述檔的標題，例如範例中繼資料，然後點選 **[!UICONTROL 提交]**. 此時將顯示元資料配置檔案的編輯表單。
1. 按一下元件，並在 **[!UICONTROL 設定]** 標籤。 例如，按一下 **[!UICONTROL 說明]** 元件並編輯其屬性。
編輯下列屬性 **[!UICONTROL 說明]** 元件：

   * **[!UICONTROL 欄位標籤]**  — 中繼資料屬性的顯示名稱。 僅供使用者參考。
   * **[!UICONTROL 對應至屬性]**  — 此屬性的值提供儲存在儲存庫中的資產節點的相對路徑/名稱。 值應一律以開頭 `./` 因為它表示路徑位於資產的節點下。

      您為指定的值 **[!UICONTROL 對應至屬性]** 會儲存為資產中繼資料節點下的屬性。 例如，如果您指定。`/jcr:content/metadata/dc:desc` 作為的名稱 **[!UICONTROL 對應至屬性]**, [!DNL Adobe Experience Manager Assets] 儲存值 `dc:desc` 在資產的中繼資料節點。

   * **[!UICONTROL 預設值]**  — 使用此屬性為元資料元件添加預設值。 例如，如果您指定「My description」，則會將此值指派給屬性 `dc:desc` 在資產的中繼資料節點。

      >[!NOTE]
      >
      >將預設值新增至新中繼資料屬性(不存在於 `/jcr:content/metadata` 節點)預設不會在資產的「屬性」頁面上顯示屬性及其值。 若要在上檢視新屬性， [!UICONTROL 屬性] 頁，修改相應的架構表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| Component | 屬性 |
|------------------|----------------------------------------------------|
| 區段標題 | 欄位標籤，說明 |
| 單行文字 | 欄位標籤，映射至屬性，預設值 |
| 多值文字 | 欄位標籤，映射至屬性，預設值 |
| 數字 | 欄位標籤，映射至屬性，預設值 |
| 日期 | 欄位標籤，映射至屬性，預設值 |
| 標準標記 | 欄位標籤，映射到屬性，預設值，說明 |

1. 按一下 **[!UICONTROL 完成]**. 中繼資料描述檔會新增至 **[!UICONTROL 中繼資料設定檔]** 頁面。

## 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面中，選擇元資料配置檔案以製作其副本。
1. 按一下 **[!UICONTROL 複製]** 的上界。
1. 在 **[!UICONTROL 複製中繼資料設定檔]** 對話框，輸入元資料配置檔案新副本的標題。
1. 按一下 **[!UICONTROL 複製]**. 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

## 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面，選擇要刪除的配置檔案。
1. 按一下 **[!UICONTROL 刪除中繼資料設定檔]** 的下一頁。
1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 確認刪除操作。 元資料設定檔會從清單中刪除。

## 將中繼資料設定檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 將不同的配置檔案應用到子資料夾時，繼承將停止。 您只能將一個中繼資料描述檔指派給資料夾。 因此，請仔細考慮上傳、儲存、使用和封存資產的資料夾結構。

如果您指派不同的中繼資料描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 先前的資料夾資產維持不變。 新設定檔會套用至變更後新增至資料夾的資產。 您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

在用戶介面中，會以卡片名稱中顯示的設定檔名稱來表示已為其指派設定檔的資料夾。

您可以重新處理資料夾中的資產，該資料夾中已有您後來變更的現有中繼資料設定檔。 <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將中繼資料設定檔套用至特定資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 從設定檔使用者介面將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取您要套用至資料夾或多個資料夾的中繼資料設定檔。
1. 按一下 **[!UICONTROL 將中繼資料描述檔套用至資料夾]** 並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從屬性將元資料配置檔案應用到資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側邊欄中，按一下 **[!UICONTROL 資產]** 然後導覽至您要套用中繼資料描述檔的資料夾。
1. 在資料夾中，按一下或按一下核取記號以選取，然後按一下或按一下 **屬性**.
1. 選取 **[!UICONTROL 中繼資料設定檔]** ，然後從下拉式選單中選取設定檔，然後按一下 **[!UICONTROL 儲存]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 全域套用中繼資料設定檔 {#applying-a-metadata-profile-globally}

除了將設定檔套用至資料夾外，您也可以全域套用一個設定檔，這樣任何內容都能上傳至 [!DNL Experience Manager Assets] 在任何資料夾中，都會套用選取的設定檔。

您可以重新處理資料夾中的資產，該資料夾中已有您後來變更的現有中繼資料設定檔。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全域套用中繼資料設定檔，請執行下列其中一項作業**

* 導覽至 `https://[aem_server]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並套用適當的設定檔，然後按一下 **[!UICONTROL 儲存]**.

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`. 新增屬性 `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. 按一下 **全部儲存**.

## 從資料夾中移除中繼資料描述檔 {#removing-a-metadata-profile-from-folders}

從資料夾移除中繼資料描述檔時，任何子資料夾都會自動從其父資料夾移除描述檔。 不過，資料夾內發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「工具 **」功能表** 移除中繼資料描述檔 ****。本節將說明如何以兩種方式從資料夾中移除中繼資料描述檔。

### 透過設定檔使用者介面從資料夾移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下Experience Manager標誌並導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取要從資料夾或多個資料夾中移除的中繼資料設定檔。
1. 按一下 **[!UICONTROL 從資料夾中移除中繼資料描述檔]** ，然後選擇要用於從中刪除配置檔案的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**.

   您可以確認中繼資料描述檔不再套用至資料夾，因為資料夾名稱下方不再顯示該名稱。

### 透過屬性從資料夾中移除中繼資料描述檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下Experience Manager標誌並導覽 **[!UICONTROL 資產]** 然後，移至您要從中移除中繼資料描述檔的資料夾。
1. 在資料夾中，按一下核取記號以選取，然後按一下 **[!UICONTROL 屬性]**.
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

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
