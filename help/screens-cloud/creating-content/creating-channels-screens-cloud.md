---
title: 在螢幕中建立和管理通道as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中建立和管理通道。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# 在螢幕中建立和管理通道as a Cloud Service {#creating-channels-screens-cloud}

建立AEM Screens項目後，必須建立渠道。
***頻道***、顯示一系列內容（影像和視頻）、網站或單頁應用程式。

## 目標 {#objective}

本文檔幫助您瞭解在螢幕內容提供商中為您的AEM Screens項目建立和管理渠道。 閱讀後，您應：

* 瞭解如何建立螢幕內容提供程式的通道
* 管理和編輯您的渠道中的內容

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


## 下一步是什麼 {#whats-next}

現在，在您的項目中設定了AEM Screens頻道，您需要發佈您的頻道。 請參閱 [在螢幕中發佈通道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) 從螢幕服務提供商管理玩家之前。
