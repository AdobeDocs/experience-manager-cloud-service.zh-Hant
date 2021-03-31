---
title: 中繼資料設定檔
description: 瞭解資產的中繼資料設定檔。 瞭解如何建立中繼資料描述檔並將它套用至資料夾資產。
contentOwner: AG
feature: 中繼資料
role: 業務從業人員，管理員
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 20%

---


# 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料描述檔並將其套用至資料夾。 您隨後上傳至資料夾的任何資產都會繼承您在中繼資料描述檔中設定的預設中繼資料。

## 新增中繼資料設定檔{#adding-a-metadata-profile}

1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料描述檔]**」，然後按一下「建立&#x200B;**[!UICONTROL 」。]**
1. 輸入中繼資料描述檔的標題，例如範例中繼資料，然後點選&#x200B;**[!UICONTROL Submit]**。 此時將顯示元資料配置檔案的編輯表單。
1. 按一下元件，並在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中設定其屬性。 例如，按一下&#x200B;**[!UICONTROL Description]**元件並編輯其屬性。
編輯**[!UICONTROL Description]**&#x200B;元件的以下屬性：

   * **[!UICONTROL 欄位標籤]** -中繼資料屬性的顯示名稱。僅供使用者參考。
   * **[!UICONTROL 映射到屬性]** -此屬性的值提供到資產節點的相對路徑／名稱，該節點保存在儲存庫中。值應始終以`./`開頭，因為它表示路徑位於資產節點下。

      您為&#x200B;**[!UICONTROL 映射至屬性]**&#x200B;指定的值會儲存為資產中繼資料節點下的屬性。 例如，如果您指定。`/jcr:content/metadata/dc:desc` 作為映射 **[!UICONTROL 至屬性的名稱]**, [!DNL Adobe Experience Manager Assets] 將值儲 `dc:desc` 存在資產的中繼資料節點。

   * **[!UICONTROL 預設值]** -使用此屬性為元資料元件添加預設值。例如，如果您指定「我的說明」，則此值會指派給資產中繼資料節點上的屬性`dc:desc`。

      >[!NOTE]
      >
      >將預設值新增至新的中繼資料屬性（在`/jcr:content/metadata`節點上不存在）時，預設不會在資產的「屬性」頁面上顯示屬性及其值。 要在[!UICONTROL 屬性]頁上查看新屬性，請修改相應的模式表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
|------------------|----------------------------------------------------|
| 區段標題 | 欄位標籤，說明 |
| 單行文字 | 欄位標籤、對應至屬性、預設值 |
| 多值文字 | 欄位標籤、對應至屬性、預設值 |
| 數量 | 欄位標籤、對應至屬性、預設值 |
| 日期 | 欄位標籤、對應至屬性、預設值 |
| 標準標記 | 欄位標籤、對應至屬性、預設值、說明 |

1. 按一下&#x200B;**[!UICONTROL Done]**。 元資料配置檔案將添加到&#x200B;**[!UICONTROL 元資料配置檔案]**&#x200B;頁中的配置檔案清單中。

## 複製元資料配置檔案{#copying-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料描述檔]**&#x200B;頁面中，選取中繼資料描述檔以製作其副本。
1. 按一下工具欄中的&#x200B;**[!UICONTROL Copy]**。
1. 在&#x200B;**[!UICONTROL 複製元資料配置檔案]**&#x200B;對話框中，輸入元資料配置檔案新副本的標題。
1. 按一下&#x200B;**[!UICONTROL Copy]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

## 刪除元資料配置檔案{#deleting-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料描述檔]**&#x200B;頁面中，選取要刪除的描述檔。
1. 按一下工具欄中的&#x200B;**[!UICONTROL 刪除元資料配置檔案]**。
1. 在對話框中，按一下&#x200B;**[!UICONTROL Delete]**&#x200B;以確認刪除操作。 元資料配置檔案將從清單中刪除。

## 將元資料配置檔案應用於資料夾{#applying-a-metadata-profile-to-folders}

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承該配置檔案。 這表示您只能將一個中繼資料描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您指派不同的中繼資料描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，配置有配置檔案的資料夾將通過卡名稱中顯示的配置檔案名稱來指示。

您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。<!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將元資料配置檔案應用於特定資料夾{#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 從Profiles用戶介面{#applying-metadata-profiles-to-folders-from-profiles-user-interface}將元資料配置檔案應用到資料夾

1. 導覽至「**[!UICONTROL 工具>資產>中繼資料描述檔]**」。
1. 選擇要應用於資料夾或多個資料夾的元資料配置檔案。
1. 按一下「將中繼資料描述檔套用至資料夾」]**，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，然後按一下「完成」。**[!UICONTROL ****&#x200B;已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從「屬性{#applying-metadata-profiles-to-folders-from-properties}」將中繼資料描述檔套用至資料夾

1. 在左側導軌中，按一下「**[!UICONTROL 資產]**」，然後導覽至您要套用中繼資料描述檔的檔案夾。
1. 在資料夾上，按一下或按一下複選標籤以選擇它，然後按一下或按一下&#x200B;**屬性**。
1. 選擇&#x200B;**[!UICONTROL 元資料配置檔案]**&#x200B;頁籤，然後從下拉菜單中選擇配置檔案，然後按一下&#x200B;**[!UICONTROL 保存]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 全域套用中繼資料設定檔{#applying-a-metadata-profile-globally}

除了將描述檔套用至資料夾外，您也可以全域套用一個描述檔，如此任何資料夾中上傳至[!DNL Experience Manager Assets]的內容都會套用選取的描述檔。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全域套用中繼資料設定檔，請執行下列其中一項作業**

* 導覽至`https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`並套用適當的描述檔，然後按一下「儲存」。****

* 導航到CRXDE Lite到以下節點：`/content/dam/jcr:content`。 添加屬性`metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`。 按一下&#x200B;**保存全部**。

## 從資料夾{#removing-a-metadata-profile-from-folders}中刪除元資料配置檔案

從資料夾中刪除元資料配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「工具 **」功能表** 移除中繼資料描述檔 ****。本節將說明如何以兩種方式從資料夾中移除中繼資料描述檔。

### 通過Profiles用戶介面{#removing-metadata-profiles-from-folders-via-profiles-user-interface}從資料夾中刪除元資料配置檔案

1. 按一AEM下標誌並導覽至&#x200B;**[!UICONTROL 工具>資產>中繼資料描述檔]**。
1. 選擇要從資料夾或多個資料夾中刪除的元資料配置檔案。
1. 按一下&#x200B;**[!UICONTROL 從資料夾中刪除元資料配置檔案]**&#x200B;並選擇要從中刪除配置檔案的資料夾或多個資料夾，然後按一下&#x200B;**[!UICONTROL Done]**。

   您可以確認中繼資料描述檔不再套用至資料夾，因為該名稱不會再顯示在資料夾名稱下方。

### 透過屬性{#removing-metadata-profiles-from-folders-via-properties}從資料夾移除中繼資料描述檔

1. 按一AEM下標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後導覽至您要移除中繼資料描述檔的資料夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下&#x200B;**[!UICONTROL 屬性]**。
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
