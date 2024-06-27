---
title: 設定Content Hub使用者介面
description: 設定Content Hub使用者介面
source-git-commit: 85ccd23df4ac320d6da37c54b72f0f93916e65a1
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 4%

---

# 設定Content Hub使用者介面 {#configure-content-hub-user-interface}

<!-- ![Download assets](assets/download-asset.jpg) -->
![在Content Hub上設定資產](assets/configure-assets.png)

Experience Manager Assets可讓管理員設定Content Hub使用者介面上的可用選項。 根據管理員選取的設定選項，Content Hub使用者可以在Content Hub上檢視欄位。 組態選項包括：

* 使用者在搜尋資產時可使用的篩選器。

* 每個資產的可用資產詳細資訊或屬性。

* 將資產新增至Content Hub時，使用者可用的中繼資料欄位。

* 可在Content Hub上搜尋的資產中繼資料欄位。

* 您需要為組織顯示的品牌化內容。

* 除了資產、集合和深入分析之外，您還需要在Content Hub中加入的任何自訂連結。

## 先決條件 {#prerequisites-configuration-ui}

[Content Hub管理員](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator) 您可以將資產新增至Content Hub，也可以為組織內的其他使用者設定「設定」選項。

## 存取Content Hub上的設定選項 {#access-configuration-options-content-hub}

若要存取Content Hub上的設定選項：

1. 按一下右窗格中的使用者圖示。

1. 在 **[!UICONTROL 產品設定]** 區段，選取 **[!UICONTROL 設定]**.

   ![存取Content Hub上的設定選項](assets/access-content-hub-configuration-ui.png)

## 在Content Hub上管理設定選項 {#manage-configuration-options}

為您的使用者管理下列設定選項：

* [匯入](#configure-import-options-content-hub)

* [篩選條件](#configure-filters-content-hub)

* [資產詳細資料](#configure-asset-details-content-hub)

* [搜尋](#configure-metadata-search-content-hub)

* [品牌元素](#configure-branding-content-hub)

* [自訂連結](#configure-custom-links-content-hub)

### 匯入 {#configure-import-options-content-hub}

您可以將資產上傳或匯入至Content Hub入口網站時（例如行銷活動名稱、關鍵字、管道、時間範圍、地區等），設定顯示給使用者的中繼資料欄位。 若要如此做，請執行以下步驟：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 匯入]**.

1. 按一下 **[!UICONTROL 新增中繼資料]**.

1. 指定屬性的標籤，然後使用 **[!UICONTROL 中繼資料]** 欄位，並選取新資產中繼資料的輸入型別。

1. 按一下 **[!UICONTROL 必要欄位]** 切換以上傳新資產時，讓新中繼資料欄位成為使用者必須指定的欄位。

1. 按一下 **[!UICONTROL 確認]**. 新的中繼資料會顯示在現有資產屬性清單中。

1. 按一下 **[!UICONTROL 儲存]** 以套用變更。

同樣地，您可以按一下 ![編輯圖示](assets/do-not-localize/edit_icon.svg)，位於每個可用屬性旁，若要編輯標籤，請在使用上傳資產時，讓這些欄位成為使用者強制或非強制欄位 **[!UICONTROL 必要欄位]** 切換，或按一下「刪除」圖示以刪除任何中繼資料屬性。

按一下 **[!UICONTROL 自動核准]** 如果您要將新增至Experience Manager Assets存放庫的所有資產自動核准，以便能立即在Content Hub中使用，請切換選項。 否則，DAM作者或管理員需要手動核准資產，才能在Content Hub上使用。 切換預設會設定為「關閉」狀態。

按一下 **[!UICONTROL 儲存]** 完成所有修改以套用變更後。

![在Content Hub上的設定UI上傳詳細資料](assets/configuration-ui-upload-details.png)

在設定使用者介面上啟用的中繼資料會顯示在資產上傳頁面上：

![在Content Hub上上傳中繼資料](assets/configuration-ui-add-assets.png)

### 篩選條件 {#configure-filters-content-hub}

Content Hub可讓管理員設定在搜尋資產時顯示的篩選器。 執行以下步驟以新增篩選器：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 篩選器]**.

1. 按一下 **[!UICONTROL 新增篩選器]**.

1. 指定篩選的標籤，並使用 **[!UICONTROL 中繼資料]** 欄位，並選取新篩選器的輸入型別。
1. 按一下 **[!UICONTROL 確認]**. 新篩選器會顯示在現有篩選器的清單中。

1. 按一下 **[!UICONTROL 儲存]** 套用變更，以便在篩選資產時讓新篩選器顯示在「搜尋」頁面上。

同樣地，您可以按一下 ![編輯圖示](assets/do-not-localize/edit_icon.svg)，可用於每個可用篩選器旁邊，以編輯標籤或按一下刪除圖示以刪除任何現有篩選器。 按一下 **[!UICONTROL 儲存]** 完成所有修改以套用變更後。

![Content Hub上的設定UI篩選器](assets/configuration-ui-filters.png)

在「組態使用者介面」上啟用的篩選器會顯示在「搜尋」頁面上：

![在Content Hub上搜尋](assets/filters-for-search.png)


### 資產詳細資料 {#configure-asset-details-content-hub}

您也可以設定為每個資產顯示的資產屬性，例如檔案名稱、標題、格式、大小等。 若要如此做，請執行以下步驟：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 資產詳細資訊]**.

1. 按一下 **[!UICONTROL 新增中繼資料]**.

1. 指定屬性的標籤，然後使用 **[!UICONTROL 中繼資料]** 欄位，並選取新資產中繼資料的輸入型別。
1. 按一下 **[!UICONTROL 確認]**. 新的中繼資料會顯示在現有資產屬性清單中。

1. 按一下 **[!UICONTROL 儲存]** 以套用變更，讓新屬性顯示在資產詳細資訊頁面上。

同樣地，您可以按一下 ![編輯圖示](assets/do-not-localize/edit_icon.svg)，可用於每個可用屬性旁，以編輯標籤，或按一下刪除圖示以刪除任何現有的資產詳細資訊。 按一下 **[!UICONTROL 儲存]** 完成所有修改以套用變更後。

![Content Hub上的設定UI資產詳細資訊](assets/configuration-ui-asset-details.png)

「組態使用者介面」上啟用的特性會顯示在「資產詳細資訊」頁面上：

![Content Hub的資產屬性](assets/config-ui-asset-properties.png)

### 搜尋 {#configure-metadata-search-content-hub}

管理員可定義當使用者在Content Hub上指定搜尋條件時所搜尋的中繼資料欄位。 執行以下步驟：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 新增中繼資料]**.

1. 指定中繼資料欄位並按一下 **[!UICONTROL 確認]**.

1. 按一下 **[!UICONTROL 儲存]** 以套用變更，讓新的中繼資料屬性顯示在中繼資料欄位清單中。

同樣地，您可以按一下 ![編輯圖示](assets/do-not-localize/edit_icon.svg)，可用於每個可用中繼資料屬性旁，以編輯屬性或按一下「刪除」圖示以刪除任何現有屬性。 按一下 **[!UICONTROL 儲存]** 完成所有修改以套用變更後。

![Content Hub上的設定UI搜尋](assets/configuration-ui-metadata-search.png)


### 品牌元素 {#configure-branding-content-hub}

管理員也可以根據您的品牌需求，個人化Content Hub入口網站橫幅上的標題和內文。 若要如此做，請執行以下步驟：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 品牌化]**.

1. 指定文字 **[!UICONTROL 橫幅上的標題文字]** 和 **[!UICONTROL 橫幅上的內文]** 欄位。

1. 按一下 **[!UICONTROL 儲存]** 以套用變更。

![Content Hub上的設定UI品牌](assets/configuration-ui-branding.png)

在「設定」使用者介面中啟用的品牌更新會顯示在Content Hub入口網站的橫幅上：

![Content Hub上的設定UI品牌](assets/configuration-ui-branding-updates.png)

### 自訂連結 {#configure-custom-links-content-hub}

除了標準標籤之外，您也可以新增自訂標籤 **[!UICONTROL 所有Assets]**， **[!UICONTROL 集合]**、和 **[!UICONTROL Insights]** Content Hub入口網站上的索引標籤，緊接在橫幅下方。 若要如此做，請執行以下步驟：

1. 在 [設定](#access-configuration-options-content-hub) 使用者介面，按一下 **[!UICONTROL 自訂連結]**.

1. 按一下 **[!UICONTROL 新增連結]**.

1. 指定文字 **[!UICONTROL 標籤]** 和 **[!UICONTROL URL]** 欄位。 您定義的標籤會顯示為標籤，當您按一下標籤時，您可以導覽至 **[!UICONTROL URL]** 欄位。

1. 按一下 **[!UICONTROL 確認]**.

1. 按一下 **[!UICONTROL 儲存]** 以套用變更。

同樣地，您可以按一下 ![編輯圖示](assets/do-not-localize/edit_icon.svg)，可用來編輯連結，或按一下刪除圖示來刪除任何現有的URL。 按一下 **[!UICONTROL 儲存]** 完成所有修改以套用變更後。

![Content Hub上的設定UI自訂連結](assets/configuration-ui-custom-links.png)

自訂連結在Content Hub首頁的「深入分析」標籤旁邊會顯示為新標籤。

![Content Hub上的設定UI自訂連結標籤](assets/configuration-ui-custom-link-tab.png)


