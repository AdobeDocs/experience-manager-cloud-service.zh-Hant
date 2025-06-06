---
title: Screens影片的縮圖支援as a Cloud Service
description: 本頁說明如何在Screens中新增影片的縮圖支援as a Cloud Service。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# 影片的縮圖支援 {#thumbnail-support-videos}

## 簡介 {#introduction}

內容作者可以定義影片的縮圖，好讓影像可以當做預留位置使用，並正確測試內容播放和目標定位，同時由適當的團隊完成實際影片。 如果影片播放失敗，也可以使用該影像。

在視訊元件上新增對縮圖影像的支援，可讓客戶在頻道中正確新增包含實際內容的有效元件，並在視訊傳送前執行任何目標定位設定。

>[!NOTE]
>如果在視訊元件上設定了縮圖影像，則當播放器發生視訊播放失敗時就會播放。 此工作流程可讓您傳遞所需訊息給對象（透過播放內容），而非完全略過。

縮圖支援可讓您進行以下工作：

* 影片尚未準備就緒，或您不想要測試播放器上的大型資產下載時，請準備管道體驗

* 設定後援機制，以防止裝置上發生播放問題。

## 在視訊中使用縮圖 {#using-thumbnails}

>[!IMPORTANT]
>**必備條件**
>在瞭解如何使用影片的縮圖之前，請務必先瞭解如何在Screensas a Cloud Service專案中建立頻道的影片轉譯。 請參閱[在Screens as a Cloud Service](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md)中建立視訊轉譯。

請依照下列步驟，在視訊中使用縮圖：

1. 導覽至現有的Screens頻道或建立頻道。

   >[!NOTE]
   >若要瞭解如何建立管道並將內容新增至管道，請參閱[在Screens中建立和管理管道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=zh-Hant)。

1. 選取頻道。 在動作列上，按一下&#x200B;**編輯**&#x200B;以開啟編輯器。


   ![動作列](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)上的編輯按鈕。

1. 新增或編輯現有的視訊元件，如下圖所示。

   ![視訊資產的醒目提示影像](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)。

1. 新增或編輯現有的視訊元件，如下圖所示。

1. 選取視訊並按一下「設定（*扳手*）」圖示以開啟視訊屬性。

   ![選取的視訊資產影像，其箭頭指向[設定]圖示，表示為扳手。 在工具列](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)上。

1. **視訊**&#x200B;對話方塊開啟，您可以在其中檢視&#x200B;**縮圖**&#x200B;拖放區域。

   ![顯示視訊資產影像的視訊對話方塊和縮圖拖放方塊](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)。

1. 將影像從資產選擇器拖放至&#x200B;**縮圖**&#x200B;拖放區域，然後按一下&#x200B;**完成**。

   ![影像選擇器顯示在視訊對話方塊後方，影像資產顯示在縮圖下拉方塊](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)中。

1. 按一下&#x200B;**預覽**。

1. 若已在元件上設定視訊，則會播放視訊。 如果沒有，且已設定縮圖，則會播放縮圖。 否則，元件會視為未設定並略過。

## 在視訊中使用縮圖時的支援使用案例 {#understand-use-case}

影片中的縮圖支援下列使用案例：

* 未跳過任何設定的視訊元件。

* 只有縮圖集的視訊元件會播放縮圖。

* 同時具有視訊（如果視訊具有正確的轉譯）和縮圖集的視訊元件會播放視訊。

* 如果發生播放錯誤，包含視訊集的視訊元件會播放縮圖，如果未設定縮圖，則會跳至下一個專案。
