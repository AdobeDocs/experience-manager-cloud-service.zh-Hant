---
title: 在Screens as a Cloud Service中建立和管理管道
description: 本頁說明如何在Screens as a Cloud Service中建立和管理管道。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---

# 在Screens as a Cloud Service中建立和管理管道 {#creating-channels-screens-cloud}

建立AEM Screens專案後，您必須建立管道。
***管道***，顯示一系列內容（影像和視訊）、網站或單頁應用程式。

## 目標 {#objective}

本檔案可協助您瞭解如何在Screens Content Provider中為AEM Screens專案建立和管理管道。 閱讀本檔案後，您應該：

* 瞭解如何建立Screens內容提供者的管道
* 管理和編輯您的頻道中的內容
* 在[Screens服務提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=zh-Hant)中管理您頻道的指派與啟用排程

## 在Screens as a Cloud Service中建立新順序頻道的步驟 {#create-new-channel}

>[!NOTE]
>**先決條件**
>在開始本指南的本節之前，請先檢閱[在Screens as a Cloud Service中建立和管理專案](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)。

請依照下列步驟，在Screens as a Cloud Service中建立順序頻道：

1. 導覽至Screens內容提供者。

1. 導覽至您的AEM Screens專案，例如&#x200B;*FirstDigitalExperience*。

1. 從您的專案中選取&#x200B;**Channels**&#x200B;資料夾，例如&#x200B;**FirstDigitalExperience** —> **Channels**，然後按一下動作列中的&#x200B;**建立**。

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 從&#x200B;**建立**&#x200B;精靈中選取範本，例如&#x200B;**序列頻道**，然後按一下&#x200B;**下一步**。

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > **建立**&#x200B;精靈在建立頻道時提供不同型別的範本。 如需詳細資訊，請參閱建立精靈中的[可用範本](#available-templates)。

1. 輸入順序頻道的名稱，例如&#x200B;**LoopingChannelOne**，然後按一下&#x200B;**建立**。

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   您現在會在AEM Screens專案的「管道」資料夾中看到&#x200B;**LoopingChannelOne**。

   建立管道後，您現在可以將內容新增到管道中。 請參閱[新增內容至頻道](#add-content)，瞭解如何新增資產（影像/影片）至您的頻道。

## 管理管道 {#managing-channels}

您可以編輯、檢視屬性和控制面板，複製、預覽和刪除管道。

從您的專案導覽至該頻道，然後選取該頻道，如下圖所示。 您現在可以選取選項，例如編輯頻道、檢視屬性、預覽內容、管理出版物，或從動作列刪除頻道。

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### 新增內容至頻道 {#add-content}

若要新增或編輯管道中的內容，請遵循下列步驟：

1. 選取您要編輯的頻道，如下圖所示。 按一下動作列左上角的&#x200B;**編輯**&#x200B;以開啟編輯器。

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 編輯器可讓您將資產/元件新增至您要發佈的管道。

1. 從左側窗格拖放資產，並將其新增至編輯器。

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >按一下&#x200B;**預覽**&#x200B;以預覽您的頻道內容。
   >![edit-channelpreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 建立精靈中的可用範本 {#available-templates}

使用&#x200B;**建立**&#x200B;頻道精靈時，可以使用下列範本：

| 可用的範本 | 說明 |
|--- |--- |
| 頻道資料夾 | 可讓您建立資料夾以儲存管道集合。 |
| 順序頻道 | 可讓您建立依序播放元件的色版（在投影片放映中逐一播放）。 |
| 左或右L列拆分畫面頻道 | 可讓內容作者在適當大小的區域中檢視不同型別的資產。 |

## 使用管道的預設指派詳細資料 {#default-channels}

此功能可讓您定義頻道的預設啟用排程，並預設用於顯示的每個指派。 此方法可讓繁瑣的排程定義不需要重複。

1. 導覽至[Screens服務提供者](https://experience.adobe.com/screens)。

### 建立管道的預設指派詳細資料 {#create-default}

1. 導覽至您要設定之頻道的詳細資訊頁面。
1. 在頁面上找到&#x200B;**預設指派詳細資料**&#x200B;圖磚。

   ![影像](/help/screens-cloud/assets/display/Assignment1.png)

1. 按一下&#x200B;**設定預設詳細資料**。
1. 設定預設指派詳細資料，包括頻道的優先順序、開始和結束日期以及週期模式，然後按一下&#x200B;**指派**。

   ![影像](/help/screens-cloud/assets/display/Assignments2.png)

1. 請注意，指派的詳細資訊顯示在&#x200B;**預設指派詳細資料**&#x200B;圖磚中：

   ![影像](/help/screens-cloud/assets/display/Assignments3.png)

此圖磚會顯示下列資訊：

* 管道在顯示中的預設優先順序。
* 頻道排程播放時的啟用開始和結束日期。
* 週期的綜合檢視（每小時/每日/每週/每月/每年，以及指定給該週期的名稱）。

### 指派給顯示區時，使用預設指派詳細資料 {#default-display}

具有預設指派詳細資訊的管道可以指派給以與一般管道相同的顯示方式，新增選項以使用預設指派詳細資訊，而不是每次都手動定義自訂指派詳細資訊。

1. 導覽至您要指派頻道的顯示詳細資訊頁面，然後按一下&#x200B;**指派頻道**。
或者，在[詳細目錄](https://experience.adobe.com/screens/displays)檢視中選取想要的顯示，然後按一下&#x200B;**指派管道**。
1. 通道指定對話方塊隨即開啟。

   ![影像](/help/screens-cloud/assets/display/Assignments4.png)

1. 從管道選擇器中選取具有預設指派詳細資訊的所需管道。
1. 請注意，頻道指派對話方塊會變更，讓您選擇預設指派詳細資料，或選取自訂指派詳細資料：

   ![影像](/help/screens-cloud/assets/display/Assignments5.png)

1. 按一下&#x200B;**指派**&#x200B;以完成指派，或按一下&#x200B;**設定自訂指派詳細資料** （如果您偏好以特定顯示內容中的其他值覆寫預設值）。

   ![影像](/help/screens-cloud/assets/display/Assignments6.png)

1. 請注意，**指派的管道**&#x200B;圖磚已更新為新指派：

   ![影像](/help/screens-cloud/assets/display/Assignments7.png)

1. 請注意，視頻道使用自訂排程（「時鐘」圖示）或繼承預設詳細資訊（「世界時鐘」圖示）而定，頻道會有不同的圖示，按一下這些圖示會顯示排程詳細資訊。
1. 也請注意，每種型別的可用動作會有所不同。

   ![影像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：**&#x200B;使用預設指派詳細資訊的頻道指派在顯示的內容中將不可編輯。

* 如果您必須將其變更為自訂工作分派，請先將其移除，然後使用&#x200B;**設定自訂工作分派詳細資料**&#x200B;選項再次新增。
* 如果您必須變更預設指派專案詳細資料的屬性，請直接從管道詳細資料頁面進行變更。

### 從頻道移除預設指派詳細資料 {#remove-display}

1. 瀏覽至您要移除預設指派詳細資訊之管道的詳細資訊頁面。
1. 在頁面中找到&#x200B;**預設指派詳細資料**&#x200B;圖磚
1. 按一下&#x200B;**移除預設值**。

   ![影像](/help/screens-cloud/assets/display/Assignments9.png)

1. 確認對話方塊隨即顯示，且詳細資訊符合下列條件之一：
   **a.**&#x200B;頻道未用於任何顯示。

   ![影像](/help/screens-cloud/assets/display/Assignments10.png)

**b.**&#x200B;頻道用於單一顯示器。

![影像](/help/screens-cloud/assets/display/Assignment11.png)

**c.**&#x200B;頻道已用於數個顯示器。

![影像](/help/screens-cloud/assets/display/Assignments12.png)

1. 按一下&#x200B;*移除*&#x200B;以驗證變更。

**注意：**&#x200B;從頻道移除預設指派詳細資料，將會移除所有使用它的顯示器上的相符指派。
因此，如果沒有其他內容可播放，這可能會導致空白熒幕。

## 後續步驟 {#whats-next}

現在，您已在專案中設定AEM Screens管道，因此需要發佈您的管道。 從Screens服務提供者管理您的播放器之前，請參閱[在Screens as a Cloud Service中發佈管道](manage-publish.md)。
