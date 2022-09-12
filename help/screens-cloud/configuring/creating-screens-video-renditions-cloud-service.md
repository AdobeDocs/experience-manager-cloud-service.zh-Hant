---
title: 在螢幕中建立視訊轉譯as a Cloud Service
description: 本頁面說明如何在Screensas a Cloud Service中建立視訊轉譯。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 在螢幕中建立視訊轉譯as a Cloud Service {#creating-screens-video-renditions}

## 簡介 {#introduction}

本節說明如何建立在Screens播放器中使用的視訊轉譯。

>[!IMPORTANT]
>如果您打算在Screens頻道中使用視訊，則必須設定此區段強調顯示的步驟。

## 在Screens中建立視訊轉譯的步驟as a Cloud Service {#steps-creating-screens-video-renditions}

請依照下列步驟，在Screens內容提供者as a Cloud Service的Screens中建立視訊轉譯：

1. 在Screens內容提供者中導覽至您的頻道。

   >[!NOTE]
   >請參閱 [使用Screens內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) 以取得更多詳細資訊。

1. 按一下左側導覽列中的「工具」區段，然後按一下 **資產** 然後按一下 **處理設定檔**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 按一下 **建立** 來建立新的處理設定檔。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 輸入 **名稱**，例如 **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 導覽至 **影片** 標籤來新增視訊編碼，然後按一下 **新增**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 輸入 **編碼名稱** 例如， **screens-fullhd** 和 **位元速率** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >請確定使用以「screens — 」開頭的編碼名稱，只有這些視訊轉譯會被視為在Screensas a Cloud Service播放視訊體驗。 輸入適合您視訊的位元速率（720px視訊為2500kbps,1080px為5000 kbps）。

   >[!NOTE]
   >可以以各種寬度/高度/位元速率新增多個視訊轉譯，以便處理您的視訊。 請記住，即使裝置只播放視訊轉譯，所有螢幕轉譯仍會由Screens裝置下載。

1. 按一下 **儲存**.

1. 選取處理設定檔，然後按一下 **將配置檔案應用到資料夾**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 選取要保留Screens影片的資料夾，然後按一下 **套用**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 您可以建立多個處理設定檔並將其套用至對應的資料夾，以便這些資料夾中的視訊取得特定的視訊轉譯。
   >* 將任何影片上傳至套用「處理」設定檔的資料夾時，會處理影片並建立已設定的轉譯，供「螢幕」裝置進一步用來播放影片。

