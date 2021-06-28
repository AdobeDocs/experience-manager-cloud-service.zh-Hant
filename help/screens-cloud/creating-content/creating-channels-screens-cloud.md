---
title: 在Screens中建立和管理頻道作為Cloud Service
description: 本頁說明如何以Cloud Service的形式在Screens中建立和管理頻道。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# 在Screens中建立和管理頻道作為Cloud Service {#creating-channels-screens-cloud}

建立AEM Screens專案後，您必須建立管道。
***頻道***、顯示一系列內容（影像和視訊）、網站或單頁應用程式。

## 目標 {#objective}

本檔案可協助您了解如何在Screens內容提供者中為您的AEM Screens專案建立和管理管道。 閱讀後，您應該：

* 了解如何為Screens內容提供者建立管道
* 管理和編輯頻道中的內容

## 在Screens中建立新序列管道作為Cloud Service的步驟 {#create-new-channel}

>[!NOTE]
>**必備條件**
>在開始本指南的本節之前，請查看[在Screens中建立和管理作為Cloud Service的項目](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)。

請依照下列步驟，在Screens中建立新的序列管道作為Cloud Service:

1. 導覽至「Screens內容提供者」。

1. 導覽至您的AEM Screens專案，例如&#x200B;*FirstDigitalExperience*。

1. 從專案選取&#x200B;**Channels**&#x200B;資料夾，例如&#x200B;**FirstDigitalExperience** —> **Channels**，然後按一下動作列中的&#x200B;**Create**。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 從&#x200B;**Create**&#x200B;嚮導中選擇模板，如&#x200B;**Sequence Channel**，然後按一下&#x200B;**Next**。

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > **建立**&#x200B;精靈在建立通道時提供不同類型的範本。 如需詳細資訊，請參閱建立精靈中的[可用範本](#available-templates)區段。

1. 輸入序列通道的名稱，例如&#x200B;**LoopingChannelOne**，然後按一下&#x200B;**Create**。

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   您現在會在AEM Screens專案的「管道」資料夾中看到&#x200B;**LoopingChannelOne**。

   建立管道後，您現在可以新增內容至管道。 請參閱[將內容新增至頻道](#add-content) ，了解如何將資產（影像/視訊）新增至頻道。

## 管理管道 {#managing-channels}

您可以編輯、檢視屬性和控制面板、複製、預覽和刪除管道。

從專案導覽至管道，然後選取管道，如下圖所示。 您現在可以選取選項，例如編輯頻道、檢視屬性、預覽內容、管理發布或從動作列刪除頻道。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### 新增內容至管道 {#add-content}

若要新增或編輯頻道中的內容，請遵循下列步驟：

1. 選擇要編輯的通道，如下圖所示。 按一下動作列左上角的&#x200B;**Edit**&#x200B;以開啟編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. 編輯器可讓您新增資產/元件至要發佈的管道。

1. 從左側窗格拖放資產，並將其新增至編輯器。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >按一下&#x200B;**預覽**以預覽頻道內容。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 建立嚮導中的可用模板 {#available-templates}

使用&#x200B;**Create**&#x200B;通道嚮導時，可使用以下模板：

| 可用範本 | 說明 |
|--- |--- |
| 頻道資料夾 | 允許建立資料夾以儲存管道集合。 |
| 順序頻道 | 可建立循序播放元件的管道（在幻燈片放映中逐個播放）。 |
| 左或右L形分屏通道 | 可讓內容作者在適當大小的區域中檢視不同類型的資產。 |


## 下一步 {#whats-next}

現在，您已在專案中設定AEM Screens管道後，就需要發佈管道。 在從Screens服務提供者管理您的播放器之前，請參閱[以Cloud Service形式發佈Screens中的頻道](/help/screens-cloud/creating-content/manage-publish.md)。