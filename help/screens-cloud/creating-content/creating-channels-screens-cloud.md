---
title: 在螢幕中建立和管理通道as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中建立和管理通道。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 9db22dca0fd6debaff0d93e1958e59536efabad8
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 在螢幕中建立和管理通道as a Cloud Service {#creating-channels-screens-cloud}

建立AEM Screens項目後，必須建立渠道。
***頻道***、顯示一系列內容（影像和視頻）、網站或單頁應用程式。

## 目標 {#objective}

本文檔幫助您瞭解在螢幕內容提供商中為您的AEM Screens項目建立和管理渠道。 閱讀後，您應：

* 瞭解如何建立螢幕內容提供程式的通道
* 管理和編輯您的渠道中的內容
* 您的渠道的激活計畫

## 在螢幕中建立新序列通道的步驟as a Cloud Service {#create-new-channel}

>[!NOTE]
>**必備條件**
>在開始本指南的本節之前，請查看 [在螢幕中建立和管理項目as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)。

按照以下步驟在螢幕as a Cloud Service中建立新序列通道：

1. 導航到「螢幕內容提供程式」。

1. 導航到您的AEM Screens項目，例如 *FirstDigitalExperience*。

1. 選擇 **頻道** 資料夾 **FirstDigitalExperience** —> **頻道** 按一下 **建立** 按鈕。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 選擇模板，如 **序列通道** 從 **建立** 嚮導，然後按一下 **下一個**。

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > 的 **建立** 嚮導在建立通道時提供不同類型的模板。 請參閱一節 [可用模板](#available-templates) 的子菜單。

1. 輸入序列通道的名稱，例如， **循環通道** 按一下 **建立**。

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   您現在將看到 **循環通道** 在「頻道」資料夾中。

   建立頻道後，現在可以將內容添加到頻道。 請參閱 [將內容添加到渠道](#add-content) 瞭解如何將資產（影像/視頻）添加到您的渠道。

## 管理渠道 {#managing-channels}

可以編輯、查看屬性和儀表板、複製、預覽和刪除通道。

從項目導航到頻道，然後選擇頻道，如下圖所示。 現在，您可以選擇選項，如編輯頻道、查看屬性、預覽內容、管理發布或從操作欄中刪除頻道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 將內容添加到渠道 {#add-content}

要添加或編輯頻道中的內容，請執行以下步驟：

1. 選擇要編輯的通道，如下圖所示。 按一下 **編輯** 的子菜單。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 編輯器允許您將資產/元件添加到要發佈的渠道。

1. 從左側窗格拖放資產，並將其添加到編輯器中。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >按一下 **預覽** 預覽頻道的內容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 建立嚮導中的可用模板 {#available-templates}

使用 **建立** 通道嚮導：

| 可用模板 | 說明 |
|--- |--- |
| 頻道資料夾 | 允許建立資料夾以儲存通道集合。 |
| 順序頻道 | 允許建立按順序播放元件的通道（幻燈片放映中逐個播放）。 |
| 左或右L-Bar拆分螢幕通道 | 允許內容作者在適當大小的區域中查看不同類型的資產。 |

## 使用渠道的預設分配詳細資訊 {#default-channels}

此功能允許您為通道定義預設激活計畫，並預設將其用於顯示的每個分配。 這提供了一種方法，使得不需要重複繁瑣的調度定義。

### 為通道建立預設分配詳細資訊 {#create-default}

1. 導航到要配置的通道的詳細資訊頁。
1. 查找 **預設分配詳細資訊** 頁面上的磁貼。

   ![影像](/help/screens-cloud/assets/display/Assignment1.png)

1. 按一下 **設定預設詳細資訊**。
1. 配置預設分配詳細資訊，包括優先順序、開始和結束日期以及渠道的重複模式，然後按一下 **分配**。

   ![影像](/help/screens-cloud/assets/display/Assignments2.png)

1. 請注意，分配的詳細資訊顯示在 **預設分配詳細資訊** 磁貼：

   ![影像](/help/screens-cloud/assets/display/Assignments3.png)

此磁貼顯示以下資訊：
* 顯示中通道的預設優先順序。
* 計畫播放頻道的激活開始和結束日期。
* 定期的綜合視圖（每小時/每日/每週/每月/每年以及指定該定期的名稱）。

### 分配給顯示時使用預設分配詳細資訊 {#default-display}

具有預設分配詳細資訊的通道可以指定為顯示常規通道的方式相同，添加的選項可利用預設分配詳細資訊，而不是每次手動定義自定義分配詳細資訊。

1. 導航到要將通道分配給的顯示詳細資訊頁，然後按一下 **分配通道**。
或者，在清單視圖中選擇所需的顯示，然後按一下 **分配通道**。
1. 通道分配對話框開啟。

   ![影像](/help/screens-cloud/assets/display/Assignments4.png)

1. 從通道選取器中選擇具有預設分配詳細資訊的所需通道。
1. 請注意，通道分配對話框將更改，以便您選擇預設分配詳細資訊，或選擇自定義分配詳細資訊：

   ![影像](/help/screens-cloud/assets/display/Assignments5.png)

1. 按一下 **分配** 完成分配，或 **設定自定義分配詳細資訊** 如果您希望在特定顯示的上下文中用其它值覆蓋預設值。

   ![影像](/help/screens-cloud/assets/display/Assignments6.png)

1. 注意 **分配的頻道** 磁貼已用新分配更新：

   ![影像](/help/screens-cloud/assets/display/Assignments7.png)

1. 請注意，這些通道將具有不同的表徵圖，具體取決於它們是使用自定義時間表（時鐘錶徵圖）還是繼承預設詳細資訊（世界時鐘錶徵圖），按一下這些表徵圖將顯示計畫詳細資訊。
1. 另請注意，每種類型的可用操作將不同。

   ![影像](/help/screens-cloud/assets/display/Assignments8.png)

**注：** 利用預設分配詳細資訊的通道分配在顯示的上下文中不可編輯。

* 如果需要將其更改為自定義分配，則必須先將其刪除，然後使用 **設定自定義分配詳細資訊** 的雙曲餘切值。
* 如果需要更改預設分配詳細資訊的屬性，則必須直接從渠道詳細資訊頁面執行此操作。

### 從通道中刪除預設分配詳細資訊 {#remove-display}

1. 導航到要刪除預設分配詳細資訊的渠道的詳細資訊頁面。
1. 查找 **預設分配詳細資訊** 頁面中的平鋪
1. 按一下 **刪除預設**。

   ![影像](/help/screens-cloud/assets/display/Assignments9.png)

1. 將顯示確認對話框，詳細資訊將與以下條件之一匹配：
   **a.** 任何顯示中均不使用通道。

   ![影像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** 通道用於單個顯示器。

![影像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** 通道用於多個顯示器。

![影像](/help/screens-cloud/assets/display/Assignments12.png)

1. 按一下 *刪除* 來驗證更改。

**注：** 從通道中刪除預設分配詳細資訊將刪除正在使用該分配的所有顯示器上的匹配分配。
因此，如果這些顯示器上沒有要播放的替代內容，則這可能會導致空白螢幕。

## 下一步 {#whats-next}

現在，在您的項目中設定了AEM Screens頻道，您需要發佈您的頻道。 請參閱 [在螢幕中發佈通道as a Cloud Service](manage-publish.md) 從螢幕服務提供商管理玩家之前。
