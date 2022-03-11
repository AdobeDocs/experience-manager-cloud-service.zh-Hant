---
title: 中繼資料設定檔
description: 瞭解資產的元資料配置檔案。 瞭解如何建立元資料配置檔案並將其應用於資料夾資產。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: cec07dad7a62439e26d9657459964b01ce6e3dba
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 18%

---

# 中繼資料設定檔 {#metadata-profiles}

元資料配置檔案允許您將預設元資料應用於資料夾中的資產。 建立元資料配置檔案並將其應用於資料夾。 隨後上載到資料夾的任何資產都會繼承在元資料配置檔案中配置的預設元資料。

關於在Experience Manager Assets使用檔案的一個重要概念是將檔案分配給資料夾。 配置檔案中包括元資料配置檔案以及視頻配置檔案或影像配置檔案的形式的設定。 這些設定處理資料夾及其任何子資料夾的內容。 因此，如何命名檔案和資料夾、如何排列子資料夾以及如何處理這些資料夾中的檔案將對配置檔案處理這些資產的方式產生重大影響。
通過使用一致且適當的檔案和資料夾命名策略以及良好的元資料做法，您可以充分利用數字資產收集，並確保正確的檔案由正確的配置檔案處理。

## 添加元資料配置檔案 {#adding-a-metadata-profile}

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料配置檔案]**，然後按一下 **[!UICONTROL 建立]**。
1. 輸入元資料配置檔案的標題，例如「示例元資料」，然後點擊 **[!UICONTROL 提交]**。 將顯示元資料配置檔案的編輯表單。
1. 按一下元件並在 **[!UICONTROL 設定]** 頁籤。 例如，按一下 **[!UICONTROL 說明]** 並編輯其屬性。
編輯以下屬性 **[!UICONTROL 說明]** 元件：

   * **[!UICONTROL 欄位標籤]**  — 元資料屬性的顯示名稱。 僅供用戶參考。
   * **[!UICONTROL 映射到屬性]**  — 此屬性的值提供了保存在儲存庫中的資產節點的相對路徑/名稱。 值應始終以 `./` 因為它表示路徑位於資產的節點下。

      為指定的值 **[!UICONTROL 映射到屬性]** 儲存為資產的元資料節點下的屬性。 例如，如果您指定。`/jcr:content/metadata/dc:desc` 的名稱 **[!UICONTROL 映射到屬性]**。 [!DNL Adobe Experience Manager Assets] 儲存值 `dc:desc` 元資料節點。

   * **[!UICONTROL 預設值]**  — 使用此屬性為元資料元件添加預設值。 例如，如果指定「我的說明」，則會將此值分配給屬性 `dc:desc` 元資料節點。

      >[!NOTE]
      >
      >向新元資料屬性添加預設值(在 `/jcr:content/metadata` 節點)在預設情況下不會在資產的「屬性」頁上顯示屬性及其值。 查看上的新屬性 [!UICONTROL 屬性] 頁，修改相應的架構窗體。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
|------------------|----------------------------------------------------|
| 區段標題 | 欄位標籤，說明 |
| 單行文字 | 欄位標籤，映射到屬性，預設值 |
| 多值文字 | 欄位標籤，映射到屬性，預設值 |
| 數量 | 欄位標籤，映射到屬性，預設值 |
| 日期 | 欄位標籤，映射到屬性，預設值 |
| 標準標記 | 欄位標籤、映射到屬性、預設值、說明 |

1. 按一下 **[!UICONTROL 完成]**。 元資料配置檔案將添加到 **[!UICONTROL 元資料配置檔案]** 的子菜單。

## 複製元資料配置檔案 {#copying-a-metadata-profile}

1. 從 **[!UICONTROL 元資料配置檔案]** 的子菜單。
1. 按一下 **[!UICONTROL 複製]** 的子菜單。
1. 在 **[!UICONTROL 複製元資料配置檔案]** 對話框，輸入元資料配置檔案新副本的標題。
1. 按一下 **[!UICONTROL 複製]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

## 刪除元資料配置檔案 {#deleting-a-metadata-profile}

1. 從 **[!UICONTROL 元資料配置檔案]** 的子菜單。
1. 按一下 **[!UICONTROL 刪除元資料配置檔案]** 的子菜單。
1. 在對話框中，按一下 **[!UICONTROL 刪除]** 確認刪除操作。 元資料配置檔案將從清單中刪除。

## 將元資料配置檔案應用於資料夾 {#applying-a-metadata-profile-to-folders}

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承該配置檔案。 當將不同的配置檔案應用到子資料夾時，繼承將停止。 您只能將一個元資料配置檔案分配給資料夾。 因此，請仔細考慮上載、儲存、使用和存檔資產的資料夾結構。

如果為資料夾分配了不同的元資料配置檔案，則新配置檔案將覆蓋以前的配置檔案。 以前現有的資料夾資產保持不變。 新配置檔案將應用於更改後添加到資料夾的資產。 您可以將元資料配置檔案應用於特定資料夾或全局應用於所有資產。

在用戶介面中，將分配了配置檔案的資料夾以卡名稱中顯示的配置檔案的名稱來表示。

您可以在資料夾中重新處理資產，該資料夾中已有您稍後更改的現有元資料配置檔案。 <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將元資料配置檔案應用到特定資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理資料夾中的資產，該資料夾中已有您稍後更改的現有視頻配置檔案。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 將元資料配置檔案應用到配置檔案用戶介面中的資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 導航到 **[!UICONTROL 「工具」>「資產」>「元資料配置檔案」]**。
1. 選擇要應用於資料夾或多個資料夾的元資料配置檔案。
1. 按一下 **[!UICONTROL 將元資料配置檔案應用於資料夾]** 並選擇要用於接收新上載資產的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 將元資料配置檔案應用到屬性中的資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左滑軌中，按一下 **[!UICONTROL 資產]** 然後導航到要應用元資料配置檔案的資料夾。
1. 在資料夾上，按一下或按一下複選標籤以選擇它，然後按一下或按一下 **屬性**。
1. 選擇 **[!UICONTROL 元資料配置檔案]** 頁籤，然後從下拉菜單中選擇配置檔案，然後按一下 **[!UICONTROL 保存]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 全局應用元資料配置檔案 {#applying-a-metadata-profile-globally}

除了將配置檔案應用到資料夾外，您還可以全局應用配置檔案，以便將任何內容上載到 [!DNL Experience Manager Assets] 在任何資料夾中都應用了所選配置檔案。

您可以在資料夾中重新處理資產，該資料夾中已有您稍後更改的現有元資料配置檔案。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**要全局應用元資料配置檔案，請執行以下操作之一**

* 導航到 `https://[aem_server]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並應用相應的配置檔案，然後按一下 **[!UICONTROL 保存]**。

* 導航到CRXDE Lite到以下節點： `/content/dam/jcr:content`。 添加屬性 `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`。 按一下 **全部保存**。

## 從資料夾中刪除元資料配置檔案 {#removing-a-metadata-profile-from-folders}

從資料夾中刪除元資料配置檔案時，任何子資料夾都會自動從其父資料夾中繼承刪除配置檔案。 但是，對資料夾中已發生的檔案的任何處理都保持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「工具 **」功能表** 移除中繼資料描述檔 ****。本節將說明如何以兩種方式從資料夾中移除中繼資料描述檔。

### 通過配置檔案用戶介面從資料夾中刪除元資料配置檔案 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下Experience Manager徽標並導航到 **[!UICONTROL 「工具」>「資產」>「元資料配置檔案」]**。
1. 選擇要從資料夾或多個資料夾中刪除的元資料配置檔案。
1. 按一下 **[!UICONTROL 從資料夾中刪除元資料配置檔案]** 並選擇要用於從中刪除配置檔案的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**。

   您可以確認元資料配置檔案不再應用於資料夾，因為該名稱不再顯示在資料夾名稱下方。

### 通過屬性從資料夾中刪除元資料配置檔案 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下Experience Manager徽標並導航 **[!UICONTROL 資產]** 然後轉到要從中刪除元資料配置檔案的資料夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下 **[!UICONTROL 屬性]**。
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
