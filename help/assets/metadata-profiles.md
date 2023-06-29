---
title: 中繼資料設定檔
description: 瞭解資產的中繼資料設定檔。 瞭解如何建立中繼資料設定檔，並將其套用至資料夾資產。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 20%

---

# 中繼資料設定檔 {#metadata-profiles}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service  | 本文 |

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料設定檔，並將其套用至資料夾。 您之後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

在Experience Manager Assets中使用設定檔的重要概念是，設定檔會指派給資料夾。 在設定檔中，設定為中繼資料設定檔的形式，以及視訊設定檔或影像設定檔。 這些設定會處理資料夾及其任何子資料夾的內容。 因此，您如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案，都會對設定檔處理這些資產的方式產生重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充分利用數位資產集合，並確保由正確的設定檔處理正確的檔案。

## 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**，然後按一下 **[!UICONTROL 建立]**.
1. 輸入中繼資料描述檔的標題，例如範例中繼資料，然後點選 **[!UICONTROL 提交]**. 此時會顯示中繼資料設定檔的編輯表單。
1. 按一下元件，然後在下列位置設定其屬性： **[!UICONTROL 設定]** 標籤。 例如，按一下 **[!UICONTROL 說明]** 元件並編輯其屬性。
編輯下列屬性 **[!UICONTROL 說明]** 元件：

   * **[!UICONTROL 欄位標籤]**  — 中繼資料屬性的顯示名稱。 它僅供使用者參考。
   * **[!UICONTROL 對應至屬性]**  — 此屬性的值會提供資產節點的相對路徑/名稱，資產節點會儲存在存放庫中。 此值應一律開頭為 `./` 因為它表示路徑在資產的節點下。

     您為指定的值 **[!UICONTROL 對應至屬性]** 會儲存為資產中繼資料節點下的屬性。 例如，如果您指定。`/jcr:content/metadata/dc:desc` 作為的名稱 **[!UICONTROL 對應至屬性]**， [!DNL Adobe Experience Manager Assets] 儲存值 `dc:desc` 位於資產的中繼資料節點。

   * **[!UICONTROL 預設值]**  — 使用此屬性為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，則會將此值指派給屬性 `dc:desc` 位於資產的中繼資料節點。

     >[!NOTE]
     >
     >新增預設值至新的中繼資料屬性(不存在於 `/jcr:content/metadata` 節點)預設不會在資產的屬性頁面上顯示屬性及其值。 若要檢視上的新屬性 [!UICONTROL 屬性] 頁面，修改對應的結構描述表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| Component | 屬性 |
|------------------|----------------------------------------------------|
| 區段標題 | 欄位標籤，說明 |
| 單行文字 | 欄位標籤，對應至屬性，預設值 |
| 多值文字 | 欄位標籤，對應至屬性，預設值 |
| 數字 | 欄位標籤，對應至屬性，預設值 |
| 日期 | 欄位標籤，對應至屬性，預設值 |
| 標準標記 | 欄位標籤、對應至屬性、預設值、說明 |

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。中繼資料設定檔會新增至 **[!UICONTROL 中繼資料設定檔]** 頁面。

## 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面上，選取一個中繼資料描述檔以製作其副本。
1. 按一下 **[!UICONTROL 複製]** （從工具列）。
1. 在 **[!UICONTROL 複製中繼資料設定檔]** 對話方塊中，輸入中繼資料設定檔新復本的標題。
1. 按一下 **[!UICONTROL 複製]**. 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

## 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面上，選取要刪除的設定檔。
1. 按一下 **[!UICONTROL 刪除中繼資料設定檔]** （在工具列中）。
1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 以確認刪除作業。 中繼資料設定檔會從清單中刪除。

## 將中繼資料設定檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

將中繼資料描述檔指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承描述檔。 將其他設定檔套用至子資料夾時，繼承會停止。 您只能將一個中繼資料設定檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的中繼資料描述檔指派給資料夾，新的描述檔會覆寫先前的描述檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至變更後新增至資料夾的資產。 您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

在使用者介面中，會以卡片名稱中出現的設定檔名稱來指出已指派給其設定檔的資料夾。

若資料夾中已有您之後已變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。 <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將中繼資料設定檔套用至特定資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您之後加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 從「設定檔」使用者介面將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取您要套用至一個資料夾或多個資料夾的中繼資料設定檔。
1. 按一下 **[!UICONTROL 套用中繼資料設定檔至資料夾]** 並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從「屬性」將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側邊欄中，按一下 **[!UICONTROL 資產]** 然後導覽至您要套用中繼資料設定檔的資料夾。
1. 在資料夾上，按一下或按一下核取記號以選取資料夾，然後按一下或按一下 **屬性**.
1. 選取 **[!UICONTROL 中繼資料設定檔]** 標籤並從下拉式選單中選取設定檔，然後按一下 **[!UICONTROL 儲存]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 全域套用中繼資料設定檔 {#applying-a-metadata-profile-globally}

除了將設定檔套用至資料夾外，您還可以全域套用設定檔，以便上傳到的任何內容都能使用 [!DNL Experience Manager Assets] 已套用選取的設定檔。

若資料夾中已有您之後已變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全域套用中繼資料設定檔，請執行下列任一項作業**

* 導覽至 `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam` 並套用適當的設定檔，然後按一下 **[!UICONTROL 儲存]**.

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`. 新增屬性 `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. 按一下 **全部儲存**.

## 從資料夾中移除中繼資料設定檔 {#removing-a-metadata-profile-from-folders}

當您從資料夾中移除中繼資料描述檔時，任何子資料夾都會自動繼承其父資料夾中描述檔的移除動作。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「工具 **」功能表** 移除中繼資料描述檔 ****。本節將說明如何以兩種方式從資料夾中移除中繼資料描述檔。

### 透過設定檔使用者介面從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下Experience Manager標誌並導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取您要從資料夾或多個資料夾中移除的中繼資料描述檔。
1. 按一下 **[!UICONTROL 從資料夾中移除中繼資料設定檔]** 並選取您要用來從中移除設定檔的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**.

   您可以確認中繼資料描述檔不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下Experience Manager標誌並導覽 **[!UICONTROL 資產]** 然後移至您要從中移除中繼資料設定檔的資料夾。
1. 在資料夾上，按一下核取記號以選取資料夾，然後按一下 **[!UICONTROL 屬性]**.
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

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
