---
title: 螢幕中視頻的縮略圖支援as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中為視頻添加縮略圖支援。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 視頻縮略圖支援 {#thumbnail-support-videos}

## 簡介 {#introduction}

內容作者可以定義視頻的縮略圖，以便影像可以用作佔位符並正確地test內容回放和目標，同時由適當的團隊最終確定實際視頻。 在視頻回放失敗時，也可以使用影像。

在視頻元件上添加對縮略圖的支援使客戶能夠正確地在頻道中添加有效元件（包含實際內容），並在視頻實際交付之前執行任何目標配置。

>[!NOTE]
>如果在視頻元件上設定縮略圖，則在播放器上出現視頻回放失敗時播放縮略圖。 這允許您將所需的消息（通過播放內容）傳遞給觀眾，而不是完全跳過它。

縮略圖支援允許您：

* 當視頻尚未準備好或您不一定想在播放器上test大型資產下載時，準備一次頻道體驗

* 設定回退機制，以防設備出現回放問題。

## 在視頻中使用縮略圖 {#using-thumbnails}

>[!IMPORTANT]
>**必備條件**
>在學習如何將縮略圖用於視頻之前，請確保瞭解如何在「螢幕as a Cloud Service」項目中為頻道建立視頻格式副本。 請參閱 [這裡](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) 的子菜單。

按照以下步驟在視頻中使用縮略圖：

1. 導航到現有的螢幕通道或建立新通道。

   >[!NOTE]
   >要瞭解如何建立頻道和向頻道添加內容，請參見 [在螢幕中建立和管理通道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en)。

1. 選擇頻道並按一下 **編輯** 的子菜單。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 添加或編輯現有視頻元件，如下圖所示。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 選擇視頻，然後按一下 *扳* 表徵圖以開啟視頻屬性。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. 的 **視頻** 對話框，您可以在其中查看 **縮略圖** 刪除區域。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. 將影像從資產選取器拖放到 **縮略圖** 刪除區域，然後按一下 **完成**。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 按一下 **預覽**。

1. 如果元件上設定了視頻，則視頻將播放。 如果沒有，並且縮略圖已設定，則縮略圖將播放。 否則，元件將被視為未配置，並將跳過。

## 在視頻中使用縮略圖時支援的使用案例 {#understand-use-case}

視頻中的縮略圖支援以下使用情形：

* 將跳過未設定任何內容的視頻元件。

* 僅具有縮略圖集的視頻元件將播放縮略圖。

* 具有視頻（如果視頻的格式副本正確）和縮略圖設定的視頻元件將播放視頻。

* 帶有視頻集的視頻元件將在出現播放錯誤時播放縮略圖，或者在縮略圖未配置時只跳到下一個項目。
