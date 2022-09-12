---
title: 在Screens中建立和管理頻道as a Cloud Service
description: 本頁說明如何在Screensas a Cloud Service中建立和管理頻道。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 9db22dca0fd6debaff0d93e1958e59536efabad8
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 在Screens中建立和管理通道as a Cloud Service {#creating-channels-screens-cloud}

建立AEM Screens專案後，您必須建立管道。
***管道***、顯示內容（影像和影片）、網站或單頁應用程式的順序。

## 目標 {#objective}

本檔案可協助您了解如何在Screens內容提供者中為您的AEM Screens專案建立和管理管道。 閱讀後，您應該：

* 了解如何為Screens內容提供者建立管道
* 管理和編輯頻道中的內容
* 您的頻道的啟動排程

## 在Screens中建立新序列管道的步驟as a Cloud Service {#create-new-channel}

>[!NOTE]
>**必備條件**
>開始本指南的本節之前，請先檢閱 [在Screens中建立和管理專案as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

請依照下列步驟，在Screens中建立新的序列管道as a Cloud Service:

1. 導覽至「Screens內容提供者」。

1. 導覽至您的AEM Screens專案，例如 *FirstDigitalExperience*.

1. 選取 **管道** 資料夾，例如 **FirstDigitalExperience** —> **管道** 按一下 **建立** 從動作列。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 選取範本，例如 **序列頻道** 從 **建立** 嚮導，然後按一下 **下一個**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > 此 **建立** 建立管道時，精靈會提供不同類型的範本。 請參閱區段 [可用範本](#available-templates) ，以了解更多詳細資訊。

1. 輸入序列管道的名稱，例如 **LoopingChannelOne** 按一下 **建立**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   您現在會看到 **LoopingChannelOne** 在AEM Screens專案的「管道」資料夾中。

   建立管道後，您現在可以新增內容至管道。 請參閱 [新增內容至管道](#add-content) 了解如何將資產（影像/影片）新增至通道。

## 管理管道 {#managing-channels}

您可以編輯、檢視屬性和控制面板、複製、預覽和刪除管道。

從專案導覽至管道，然後選取管道，如下圖所示。 您現在可以選取選項，例如編輯頻道、檢視屬性、預覽內容、管理發布或從動作列刪除頻道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 新增內容至管道 {#add-content}

若要新增或編輯頻道中的內容，請遵循下列步驟：

1. 選擇要編輯的通道，如下圖所示。 按一下 **編輯** 從動作列的左上角開啟編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 編輯器可讓您新增資產/元件至要發佈的管道。

1. 從左側窗格拖放資產，並將其新增至編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >按一下 **預覽** 來預覽頻道內容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 建立嚮導中的可用模板 {#available-templates}

使用 **建立** 通道精靈：

| 可用範本 | 說明 |
|--- |--- |
| 頻道資料夾 | 允許建立資料夾以儲存管道集合。 |
| 順序頻道 | 可建立循序播放元件的管道（在幻燈片放映中逐個播放）。 |
| 左或右L形分屏通道 | 可讓內容作者在適當大小的區域中檢視不同類型的資產。 |

## 使用通道的預設分配詳細資訊 {#default-channels}

此功能可讓您定義管道的預設啟動排程，並依預設將其用於顯示畫面的每個指派。 這提供了一種方法，因此不需要重複繁瑣的排程定義。

### 為通道建立預設分配詳細資訊 {#create-default}

1. 導覽至您要設定之管道的詳細資訊頁面。
1. 找出 **預設分配詳細資訊** 圖磚。

   ![影像](/help/screens-cloud/assets/display/Assignment1.png)

1. 按一下 **設定預設詳細資訊**.
1. 配置預設分配詳細資訊，包括優先順序、開始和結束日期以及通道的重複模式，然後按一下 **指派**.

   ![影像](/help/screens-cloud/assets/display/Assignments2.png)

1. 請注意，指派的詳細資訊會顯示在 **預設分配詳細資訊** 方塊：

   ![影像](/help/screens-cloud/assets/display/Assignments3.png)

此方塊會顯示下列資訊：
* 顯示中通道的預設優先順序。
* 排程播放管道時的啟動開始和結束日期。
* 週期的合成檢視（每小時/每日/每週/每月/每年，以及為該週期指定的名稱）。

### 分配給顯示時，使用預設分配詳細資訊 {#default-display}

具有預設分配詳細資訊的渠道可以分配給顯示與常規渠道相同的方式，添加的選項是利用預設分配詳細資訊，而不是每次手動定義自定義渠道。

1. 導覽至您要指派管道給的顯示詳細資料頁面，然後按一下 **指派管道**.
或者，在清單檢視中選取所需的顯示，然後按一下 **指派管道**.
1. 通道分配對話框開啟。

   ![影像](/help/screens-cloud/assets/display/Assignments4.png)

1. 從通道選擇器中選擇具有預設分配詳細資訊的所需通道。
1. 請注意，通道分配對話框將更改，以便您選擇預設分配詳細資訊或選擇自定義分配：

   ![影像](/help/screens-cloud/assets/display/Assignments5.png)

1. 按一下 **指派** 要完成分配，或按一下 **設定自定義分配詳細資訊** 如果您偏好在該特定顯示內容中，以某些其他值覆寫預設值。

   ![影像](/help/screens-cloud/assets/display/Assignments6.png)

1. 請注意 **指派的通道** 表徵圖已更新為新分配：

   ![影像](/help/screens-cloud/assets/display/Assignments7.png)

1. 請注意，管道會有不同的圖示，視其是使用自訂排程（時鐘圖示）或繼承預設詳細資料（世界時鐘圖示）而定，按一下這些圖示即可顯示排程詳細資料。
1. 另請注意，每種類型的可用動作會有所不同。

   ![影像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：** 利用預設分配詳細資訊的渠道分配在顯示的上下文中將不可編輯。

* 如果您需要將其變更為自訂指派，您必須先將其移除，然後使用 **設定自定義分配詳細資訊** 選項。
* 如果需要更改預設分配詳細資訊的屬性，則必須直接從渠道詳細資訊頁面執行此操作。

### 從通道中刪除預設分配詳細資訊 {#remove-display}

1. 導覽至您要移除預設指派詳細資料之管道的詳細資訊頁面。
1. 找出 **預設分配詳細資訊** 在頁面中拼貼
1. 按一下 **移除預設值**.

   ![影像](/help/screens-cloud/assets/display/Assignments9.png)

1. 將會顯示確認對話方塊，且詳細資料會符合下列其中一個條件：
   **a.** 管道不用於任何顯示。

   ![影像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** 通道用於單一顯示器。

![影像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** 頻道用於數個顯示器。

![影像](/help/screens-cloud/assets/display/Assignments12.png)

1. 按一下 *移除* 以驗證變更。

**注意：** 從通道中刪除預設分配詳細資訊將刪除使用該資訊的所有顯示器上的匹配分配。
因此，如果這些顯示器上沒有可播放的替代內容，這可能會導致空白畫面。

## 下一步 {#whats-next}

現在，您已在專案中設定AEM Screens管道後，就需要發佈管道。 請參閱 [在Screens中發佈管道as a Cloud Service](manage-publish.md) 從Screens服務提供商管理您的播放器之前。
