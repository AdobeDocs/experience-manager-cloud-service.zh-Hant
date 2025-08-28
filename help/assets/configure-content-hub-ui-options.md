---
title: 設定 Content Hub 使用者介面
description: 設定 Content Hub 使用者介面
exl-id: e9e22862-9bcd-459a-bcf4-7f376a0b329a
source-git-commit: 06373e14ff9199d97c03332d95a0d2b024b3220f
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 9%

---

# 設定 Content Hub 使用者介面 {#configure-content-hub-user-interface}

>[!CONTEXTUALHELP]
>id="configure_content_hub"
>title="設定 Content Hub 使用者介面"
>abstract="Experience Manager Assets 可讓管理員設定 Content Hub 使用者介面上的可用選項。根據管理員選取的設定選項，Content Hub 使用者可以查看 Content Hub 上的欄位。設定選項包括匯入資產時的中繼資料、篩選器、資產屬性、搜尋資產時的中繼資料、個人化品牌和任何自訂連結。"
>additional-url="https://images-tv.adobe.com/mpcv3/4477/74a81d1c-0cfe-41f4-8a06-18ff70604e45_1732023385.854x480at800_h264.mp4" text="觀看影片"

<!-- ![Download assets](assets/download-asset.jpg) -->

![在Content Hub上設定資產](assets/configure-assets.png)

Experience Manager Assets 可讓管理員設定 Content Hub 使用者介面上的可用選項。根據管理員選取的設定選項，Content Hub 使用者可以查看 Content Hub 上的欄位。組態選項包括：

* 使用者在搜尋資產時可使用的篩選器。

* 每個資產的可用資產詳細資訊或屬性。

* 將資產新增至Content Hub時，使用者可用的中繼資料欄位。

* 可在Content Hub上搜尋的資產中繼資料欄位。

* 您需要為組織顯示的品牌化內容。

* 除了資產、集合和深入分析之外，您還需要在Content Hub中加入的任何自訂連結。

## 先決條件 {#prerequisites-configuration-ui}

[Content Hub管理員](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator)可以為您組織內的其他使用者設定組態選項。

## 存取Content Hub上的設定選項 {#access-configuration-options-content-hub}

若要存取Content Hub上的設定選項：

1. 按一下右側窗格中的使用者圖示。

1. 在&#x200B;**[!UICONTROL 產品設定]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 組態]**。

   在Content Hub上![存取設定選項](assets/access-content-hub-configuration-ui.png)

## 在Content Hub上管理設定選項 {#manage-configuration-options}

以管理員身分，管理使用者的下列組態選項：

* [匯入](#configure-import-options-content-hub)

* [篩選條件](#configure-filters-content-hub)

* [資產詳細資料](#configure-asset-details-content-hub)
* [資產卡](#asset-card)

* [搜尋](#configure-metadata-search-content-hub)

* [品牌元素](#configure-branding-content-hub)

* [已到期的資產](#expired-assets-content-hub)

* [轉譯](#renditions-content-hub)

* [自訂連結](#configure-custom-links-content-hub)

* [集合和共用](#configure-collections-content-hub)

<!--* [Enable public link sharing](#enable-public-link-sharing)-->

### 匯入 {#configure-import-options-content-hub}

您可以將資產上傳或匯入至Content Hub入口網站時（例如行銷活動名稱、關鍵字、管道、時間範圍、地區等），設定顯示給使用者的中繼資料欄位。 若要如此做，請執行以下步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 匯入]**。

1. 按一下&#x200B;**[!UICONTROL 新增中繼資料]**。

1. 指定屬性的標籤，使用&#x200B;**[!UICONTROL 中繼資料]**&#x200B;欄位將其對應到屬性，然後選取新資產中繼資料的輸入型別。

1. 按一下&#x200B;**[!UICONTROL 必要欄位]**&#x200B;切換按鈕，讓上傳新資產時，必須讓使用者指定新的中繼資料欄位。

1. 按一下&#x200B;**[!UICONTROL 確認]**。 新的中繼資料會顯示在現有資產屬性清單中。

1. 按一下[儲存]以套用變更。**&#x200B;**

同樣地，您可以按一下每個可用屬性旁的![編輯圖示](assets/do-not-localize/edit_icon.svg)，以編輯標籤，在使用&#x200B;**[!UICONTROL 必要欄位]**&#x200B;切換上傳資產時，讓這些欄位成為使用者強制或非強制的欄位，或按一下「刪除」圖示以刪除任何中繼資料屬性。

如果您需要自動核准新增至Experience Manager Assets存放庫的所有資產，以便這些資產能立即在Content Hub中使用，請按一下&#x200B;**[!UICONTROL 自動核准]**&#x200B;切換按鈕。 否則，DAM作者或管理員需要手動核准資產，才能在Content Hub上使用。 切換預設會設定為「關閉」狀態。

完成所有修改以套用變更後，按一下&#x200B;**[!UICONTROL 儲存]**。

在Content Hub上![設定UI上傳詳細資料](/help/assets/assets/import-content-hub1.png)

在設定使用者介面上啟用的中繼資料會顯示在資產上傳頁面上：
在Content Hub上![上傳中繼資料](assets/add-assets-for-approval1.png)

### 篩選條件 {#configure-filters-content-hub}

Content Hub可讓管理員設定在搜尋資產時顯示的篩選器。 執行以下步驟以新增篩選器：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 篩選器]**。

1. 按一下&#x200B;**[!UICONTROL 新增篩選器]**。

1. 指定篩選的標籤，使用&#x200B;**[!UICONTROL 中繼資料]**&#x200B;欄位將其對應到屬性，然後選取新篩選的輸入型別。
1. 按一下&#x200B;**[!UICONTROL 確認]**。 新篩選器會顯示在現有篩選器的清單中。

1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以套用變更，以便在篩選資產時新篩選器顯示在搜尋頁面上。

   >[!NOTE]
   >
   >只有在存放庫中至少有一個資產符合篩選條件時，新篩選器才會顯示在「搜尋」頁面上。

同樣地，您可以按一下每個可用篩選器旁的![編輯圖示](assets/do-not-localize/edit_icon.svg)來編輯標籤，或按一下刪除圖示來刪除任何現有的篩選器。 完成所有修改以套用變更後，按一下&#x200B;**[!UICONTROL 儲存]**。
在Content Hub![上設定](assets/configuration-filter1.png)使用者介面篩選器

在「組態使用者介面」上啟用的篩選器會顯示在「搜尋」頁面上：
在Content Hub上![搜尋](assets/content-hub-filters1.png)

#### 大量搜尋 {#bulk-search-configuration}

若要在[!DNL Content Hub]中一次搜尋多個資產，請執行下列步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 篩選器]**。

1. 按一下每個可用篩選器旁的![編輯圖示](assets/do-not-localize/edit_icon.svg)。

1. 啟用&#x200B;**[!UICONTROL 大量搜尋]**&#x200B;切換。 預設分隔符號`[ , | \t | \r\n | \r | \n ]`會自動顯示。 此外，您也可以新增其他分隔字元。 若要這麼做，請在以`pipe symbol (|)`分隔的輸入方塊中指定分隔符號。

   ![大量搜尋設定](assets/bulk-search-configuration.png)

1. 按一下&#x200B;**[!UICONTROL 確認]**&#x200B;以儲存變更。 請參閱[Content Hub中的大量搜尋](search-assets-content-hub.md#bulk-search)實際運作中。

### 資產詳細資料 {#configure-asset-details-content-hub}

您也可以設定為每個資產顯示的資產屬性，例如檔案名稱、標題、格式、大小等。 若要如此做，請執行以下步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 資產詳細資料]**。

1. 按一下&#x200B;**[!UICONTROL 新增中繼資料]**。

1. 指定屬性的標籤，使用&#x200B;**[!UICONTROL 中繼資料]**&#x200B;欄位將其對應到屬性，然後選取新資產中繼資料的輸入型別。
1. 按一下&#x200B;**[!UICONTROL 確認]**。 新的中繼資料會顯示在現有資產屬性清單中。

1. 按一下[儲存]&#x200B;**[!UICONTROL 以套用變更，讓新屬性顯示在資產詳細資訊頁面上。]**

同樣地，您可以按一下每個可用屬性旁的![編輯圖示](assets/do-not-localize/edit_icon.svg)來編輯標籤，或按一下刪除圖示來刪除任何現有的資產詳細資訊。 完成所有修改以套用變更後，按一下&#x200B;**[!UICONTROL 儲存]**。

在Content Hub上![設定UI資產詳細資料](assets/configuration-asset-details.png)

「組態使用者介面」上啟用的特性會顯示在「資產詳細資訊」頁面上：

在Content Hub上![資產屬性](assets/asset-details-page-content-hub1.png)

### 資產卡 {#asset-card}

您也可以設定需要顯示在&#x200B;**資產卡**&#x200B;上的金鑰中繼資料屬性，最多可顯示6個欄位。
資產卡上的![金鑰中繼資料](/help/assets/assets/asset-card-metadata.png)
執行以下步驟來設定中繼資料屬性，以在&#x200B;**[!UICONTROL 資產卡]**&#x200B;上顯示：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**資產卡**。
2. 按一下&#x200B;**新增中繼資料**。 **新增資產卡中繼資料**&#x200B;對話方塊隨即顯示。
3. 在&#x200B;**標籤**&#x200B;欄位中指定中繼資料名稱，並在&#x200B;**中繼資料**&#x200B;欄位中選取中繼資料屬性。
4. 按一下&#x200B;**確認**，然後按一下&#x200B;**儲存**&#x200B;以套用變更，讓新屬性顯示在資產詳細資訊頁面上。
   ![資產卡](/help/assets/assets/configuration-asset-card1.png)
同樣地，按一下每個可用屬性旁邊可用的![編輯](/help/assets/assets/edit-content-hub.svg)，以進行任何必要的修改，或按一下![刪除](/help/assets/assets/delete-content-hub.svg)，刪除任何現有的中繼資料屬性。 完成所有修改以套用變更後，按一下&#x200B;**儲存**。

### 搜尋 {#configure-metadata-search-content-hub}

管理員可定義當使用者在Content Hub上指定搜尋條件時所搜尋的中繼資料欄位。 執行以下步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 新增中繼資料]**。

1. 指定中繼資料欄位並按一下&#x200B;**[!UICONTROL 確認]**。

1. 按一下[儲存]&#x200B;**[!UICONTROL 以套用變更，讓新的中繼資料屬性顯示在中繼資料欄位清單中。]**

同樣地，您可以按一下每個可用中繼資料屬性旁的![編輯圖示](assets/do-not-localize/edit_icon.svg)來編輯屬性，或按一下刪除圖示來刪除任何現有的屬性。 完成所有修改以套用變更後，按一下&#x200B;**[!UICONTROL 儲存]**。
在Content Hub上![設定UI搜尋](assets/configuration-search.png)

### 品牌元素 {#configure-branding-content-hub}

以管理員身分，自訂您的[!DNL Content Hub]入口網站以符合您的品牌需求。
![重設預設值](/help/assets/assets/reset-default-content-hub.png)
在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;頁面上使用&#x200B;**[!UICONTROL 橫幅]**、**[!UICONTROL 色彩]**&#x200B;和&#x200B;**[!UICONTROL 橫幅影像]**&#x200B;區段來執行下列自訂：

1. [從[!UICONTROL 標誌影像]區段變更標誌影像](#Change-the-logo-image)
1. [從[!UICONTROL 橫幅影像]區段變更橫幅影像](#Change-the-banner-image)
1. [更新橫幅上的標題和內文，並從[!UICONTROL 橫幅]區段變更文字色彩](#Add-title-and-body-text-to-your-banner-and-change-the-text-color)
1. [從[!UICONTROL 色彩]區段變更主要和次要色彩，以套用符合您品牌主題的色彩配置](#Change-the-primary-and-secondary-color)

選取&#x200B;**[!UICONTROL 重設預設值]**&#x200B;選項以還原您的變更並還原預設主題。

#### 變更標誌影像{#change-the-logo-image}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;頁面上，執行下列步驟以變更[!DNL Content Hub]部署的標誌影像：

1. 按一下![選取影像](/help/assets/assets/Browse.svg) **[!UICONTROL 選取影像]**&#x200B;以使用資產選取器對話方塊選取標誌影像。 資產選擇器只會顯示核准的影像。
1. 選取影像，按一下&#x200B;**[!UICONTROL 選取]**，然後按一下&#x200B;**[!UICONTROL 儲存]**，將其顯示為您[!DNL Content Hub]部署的標誌影像。
   ![橫幅影像](/help/assets/assets/logo-image-content-hub1.png)

#### 變更橫幅影像{#Change-the-banner-image}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;頁面上，執行下列步驟以變更[!DNL Content Hub]部署的橫幅影像：

1. 按一下![選取影像](/help/assets/assets/Browse.svg) **[!UICONTROL 從相簿選取]**&#x200B;以使用資產選取器對話方塊選取橫幅影像。 資產選擇器只會顯示核准的影像。
1. 選取影像，按一下&#x200B;**[!UICONTROL 選取]**，然後按一下&#x200B;**[!UICONTROL 儲存]**，將其顯示為[!DNL Content Hub]部署的橫幅影像。
   ![橫幅影像](/help/assets/assets/banner-image-content-hub1.png)

>[!NOTE]
>
> * 建議的&#x200B;**橫幅影像**&#x200B;大小為`height = 200 to 450px`和`width = 1920 to 2560px`。
> * 建議的&#x200B;**標誌影像**&#x200B;大小為`height = 80 to 120px`和`width = 120 to 200px`。
> * 橫幅和標誌影像的&#x200B;**支援MIME型別**&#x200B;為`'JPG', value: 'image/jpeg'`、`'PNG', value: 'image/png'`、`'WEBP', value: 'image/webp'`、`'TIFF', value: 'image/tiff'`、`'SVG', value: 'image/svg+xml'`、`'GIF', value: 'image/gif'`。

#### 新增標題和內文至橫幅並變更文字顏色{#Add-title-and-body-text-to-your-banner-and-change-the-text-color}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;頁面上，使用&#x200B;**[!UICONTROL 橫幅]**&#x200B;區段中的個別欄位，將標題與內文新增至橫幅。
按一下&#x200B;**[!UICONTROL 橫幅文字色彩]**&#x200B;旁的方塊，從檢色器選取橫幅文字的文字色彩，或在檢色器方塊旁的欄位中指定色彩的十六進位代碼。
![橫幅文字內容中心](/help/assets/assets/banner-text-content-hub.png)

#### 變更主要和次要顏色{#Change-the-primary-and-secondary-color}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;頁面上，使用&#x200B;**[!UICONTROL 顏色]**&#x200B;區段來設定主要和次要顏色，方法為使用檢色器選取顏色，或定義顏色的十六進位代碼。 這些顏色會設定UI元素的背景、文字和圖示顏色，以使[!DNL Content Hub] UI與品牌主題一致。
![主要和次要色彩](/help/assets/assets/primary-secondary-color-content-hub1.png)
**[!UICONTROL 主要色彩]：**&#x200B;主要色彩配置會套用至選取動作、互動式元素（例如核取方塊、搜尋列），以及跨[!DNL Content Hub]切換開關，包括[!DNL Content Hub]首頁和[!UICONTROL 組態]頁面。 它也適用於主要[!DNL Content Hub]介面上可用的動作選項，例如&#x200B;**[!UICONTROL 所有Assets]**&#x200B;和&#x200B;**[!UICONTROL 集合]**&#x200B;頁面上可用的選項。

**[!UICONTROL 次要色彩]：**&#x200B;在[!DNL Content Hub]首頁上，次要色彩配置會套用至對話方塊中可用的UI選項和輸入欄位。 它適用於[!UICONTROL 組態]頁面上可用的所有組態功能表選項，但選取動作、核取方塊、搜尋列和切換開關除外。

### 資產可見性{#asset-visibility-content-hub}

管理員可控制是否需要在Content Hub上顯示過期的資產。 如果要在上面顯示過期資產，這些資產還可以定義使用者是否可以下載資產。

Content Hub預設不會顯示過期的資產。

若要如此做，請執行以下步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 資產可見性]**。

1. 在&#x200B;**[!UICONTROL 可見]**&#x200B;區段中，啟用&#x200B;**[!UICONTROL 允許使用者檢視過期的資產]**&#x200B;切換按鈕，讓所有過期的資產在Content Hub上可見。

1. 啟用資產可見性後，您可以使用&#x200B;**[!UICONTROL 允許使用者下載過期的資產]**&#x200B;切換來啟用或停用下載過期的資產的功能。
1. 啟用&#x200B;**[!UICONTROL 允許使用者檢視核准傳送的資產]**&#x200B;切換功能，在Content Hub中顯示所有核准傳送的資產。
1. 按一下[儲存]以套用變更。**&#x200B;**

   ![Content Hub 上的過期資產](assets/asset-visibility-content-hub1.png)

啟用資產的可見度後，您可以在Content Hub上檢視過期的資產，如下圖所示：

![Content Hub 上的過期資產](assets/view-download-expired-assets.png)

如果管理員已啟用下載，Content Hub使用者也可以下載，如影像中反白顯示的內容。

如果已啟用過期資產的可見度，Content Hub也會使用資產卡上的`Expiring in n days`訊息，強調在未來15天內過期的資產。

### 轉譯 {#renditions-content-hub}

轉譯是數位資產（例如影像、檔案等）的自訂版本，專為不同裝置和平台而設計，可確保最佳效能。 檢視更多有關Adobe Experience Manager Assets[中](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/renditions)轉譯的資訊。

若要如此做，請執行以下步驟：

在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 轉譯]**。 下列選項可供使用：

* 啟用[!UICONTROL 啟用轉譯可用性]切換按鈕，讓所有轉譯都顯示在Content Hub上。

* 啟用或停用&#x200B;**[!UICONTROL 允許使用者下載原始資產]**&#x200B;切換功能，以控制下載原始資產的可用性。

  ![在Content Hub上設定轉譯](assets/configuration-renditions1.png)

如需如何在Content Hub中檢視及下載轉譯的詳細資訊，請參閱[在Content Hub中下載資產](/help/assets/download-assets-content-hub.md)。

### 自訂連結 {#configure-custom-links-content-hub}

除了橫幅正下方的Content Hub入口網站上的標準&#x200B;**[!UICONTROL 所有Assets]**、**[!UICONTROL 集合]**&#x200B;和&#x200B;**[!UICONTROL 深入分析]**&#x200B;標籤之外，您還可以新增自訂標籤。 若要如此做，請執行以下步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 自訂連結]**。

1. 按一下&#x200B;**[!UICONTROL 新增連結]**。

1. 在&#x200B;**[!UICONTROL 標籤]**&#x200B;和&#x200B;**[!UICONTROL URL]**&#x200B;欄位中指定文字。 您定義的標籤會顯示為標籤，當您按一下標籤時，您會導覽至&#x200B;**[!UICONTROL URL]**&#x200B;欄位中定義的URL。

1. 按一下&#x200B;**[!UICONTROL 確認]**。

1. 按一下[儲存]以套用變更。**&#x200B;**

同樣地，您可以按一下每個URL旁邊的![編輯圖示](assets/do-not-localize/edit_icon.svg)來編輯連結，或按一下刪除圖示來刪除任何現有的URL。 完成所有修改以套用變更後，按一下&#x200B;**[!UICONTROL 儲存]**。
在Content Hub上![設定UI自訂連結](assets/configuration-custom-links1.png)

自訂連結在Content Hub首頁的「深入分析」標籤旁邊會顯示為新標籤。
![Content Hub上的設定UI自訂連結標籤](assets/configuration-ui-custom-link-tab.png)

### 集合和共用 {#configure-collections-content-hub}

管理員可在建立集合時定義使用者許可權。 若要啟用這些設定，請遵循下列步驟：

1. 在[組態](#access-configuration-options-content-hub)使用者介面上，按一下&#x200B;**[!UICONTROL 集合]**。

1. 啟用&#x200B;**[!UICONTROL 啟用公用連結]**&#x200B;切換以允許建立外部使用者不需登入Content Hub即可用來存取及下載資產的公用連結。

1. 啟用&#x200B;**[!UICONTROL 僅檢視集合]**&#x200B;切換功能，讓所有人都能存取集合，但只有建立者和管理員才能編輯。

1. 啟用&#x200B;**[!UICONTROL 公用集合]**&#x200B;切換以允許所有人存取及編輯集合。 如果&#x200B;**[!UICONTROL 僅檢視集合]**&#x200B;與&#x200B;**[!UICONTROL 公用集合]**&#x200B;切換已停用，則非管理員使用者預設只能建立私人集合。

1. 按一下[儲存]以套用變更。**&#x200B;**

   Content Hub上的![設定集合索引標籤](assets/collections-and-sharing1.png)

<!--
### Enable public link sharing {#enable-public-link-sharing}

Enable the following setting on the Configurations user interface to allow Content Hub users to generate a public link:

1. On the [Configurations](#access-configuration-options-content-hub) user interface, click **[!UICONTROL Collections and Sharing]**.

1. Enable the **[!UICONTROL Enable Public Link]** toggle and click **[!UICONTROL Save]** to apply the changes.

    ![Enable public link sharing in Content Hub](assets/enable-public-link-sharing-tab.png)

-->

深入瞭解[在 [!DNL Content Hub]](share-assets-content-hub.md)中共用資產。

