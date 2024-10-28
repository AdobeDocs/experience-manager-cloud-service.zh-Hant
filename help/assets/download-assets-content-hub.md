---
title: 從Content Hub下載資產
description: 瞭解如何從Content Hub入口網站下載資產
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 96b7b7fe32aefc81a9fde15d79e9089f71cb5d31
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# 從Content Hub下載資產 {#download-assets}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![下載資產](assets/download-asset-genstudio.jpeg)

Content Hub可讓您下載和共用資產。 這些資產可能包括影像、影片或任何其他數位內容。 Content Hub可增強協助工具及適應能力，以進行有效的資產分發。

您可以使用Content Hub下載單一資產或多個資產。 資產的原始版本已下載。

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以執行本文所述的動作。

## 下載資產 {#download-single-asset}

[先核准資產的授權](/help/assets/approve-assets-content-hub.md)，然後再下載。

### 單一下載 {#single-download-asset}

選取資產，然後從頂端邊欄按一下![下載](/help/assets/assets/download-icon.svg)。 下載資產對話方塊會顯示資產的授權。 接受授權條款與條件，然後按一下[下載]。****
或者，按一下資產卡中的![下載](/help/assets/assets/download-icon.svg)以下載資產。

#### 從「資產」對話方塊下載單一資產 {#single-download-from-asset-dialog-box}

1. 按一下資產縮圖。 資產對話方塊隨即顯示。
1. 按一下最右邊工具列中的![下載](/help/assets/assets/download-icon.svg)。 下載窗格會顯示資產轉譯與授權條款與條件接受核取方塊。
   ![單一下載對話方塊](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * 按一下條款與條件連結，在左窗格中檢視授權條款。

     >[!NOTE]
     >
     >條款和條件核取方塊只會針對授權資產顯示。 此外，資產對話方塊只會針對具有已核准授權的資產，顯示授權條款與條件的預覽。 [下載前請先核准資產的授權](/help/assets/approve-assets-content-hub.md)，以在資產對話方塊中啟用授權條款預覽。

   * 按一下&#x200B;**原始轉譯方塊**&#x200B;以回到左窗格中的原始資產轉譯。
1. 接受授權條款與條件（針對授權資產），然後按一下[下載] **下載資產**。

### 多重下載 {#multi-download}

1. 選取資產，然後從頂端邊欄按一下![下載](/help/assets/assets/download-icon.svg)。 顯示的對話方塊取決於下載清單是否包含過期的資產或僅包含未過期的資產。<br/>
   **下載過期的資產對話方塊：**&#x200B;此對話方塊在左窗格中顯示過期的資產預覽及其到期日期。 所選總數的過期資產計數會顯示在右窗格中。 按一下&#x200B;**繼續處理所有資產**，以其他資產（如果有的話）下載過期的資產。 「下載資產」對話方塊隨即顯示。 請參閱[下載資產對話方塊](#Download-asset-dialog-box)以繼續進行。

   >[!NOTE]
   >
   >[啟用過期資產的下載選項](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub)即可下載。 只有已啟用下載的過期資產才可供下載。

   <a id="Download-asset-dialog-box"></a> **下載資產對話方塊：**&#x200B;此對話方塊會在左窗格中顯示與所選資產相關聯的授權清單。 選取授權以在中間窗格中預覽其條款與條件（以pdf格式），並在右側窗格中預覽相關資產的預覽及其計數。 已檢閱的授權會以淺藍色強調顯示。

   >[!NOTE]
   >
   > **下載資產對話方塊**&#x200B;只會預覽已核准授權的授權條款與條件。 [先核准資產的授權](/help/assets/approve-assets-content-hub.md)，再下載資產，以在&#x200B;**下載資產對話方塊**&#x200B;中預覽其授權條款。

1. 按一下![移除圖示](/help/assets/assets/remove-icon.svg)，從下載對話方塊移除授權。

1. 接受條款與條件，然後按一下[下載]，下載與左窗格中可用的授權相關聯的資產。****
   ![下載多重授權](/help/assets/assets/download-multiple-license.png)

### 下載未授權的資產 {#download-non-licensed-assets}

若要下載未授權的資產，請選取該資產，然後從頂端邊欄按一下![下載](/help/assets/assets/download-icon.svg)。







