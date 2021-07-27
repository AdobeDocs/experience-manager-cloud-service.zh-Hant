---
title: 在螢幕中建立視訊轉譯作為Cloud Service
description: 本頁面說明如何在Screens中建立視訊轉譯作為Cloud Service。
source-git-commit: 102aab1d550e950ea880d9b9288bdab41866add6
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# 在螢幕中建立視訊轉譯作為Cloud Service {#creating-screens-video-renditions}

## 簡介 {#introduction}

本指南將說明如何建立在Screens播放器中使用的視訊轉譯。

>[!IMPORTANT]
>如果您打算在Screens頻道中使用視訊，則必須設定本節強調顯示的步驟。

## 在Screens中建立視訊轉譯作為Cloud Service的步驟 {#steps-creating-screens-video-renditions}

請依照下列步驟，從Screens內容提供者在Screens as a Cloud Service中建立視訊轉譯：

1. 在Screens內容提供者中導覽至您的頻道。

   >[!NOTE]
   >如需詳細資訊，請參閱[使用螢幕內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) 。

1. 按一下左側導覽列中的「工具」區段，然後按一下&#x200B;**Assets**，然後按一下&#x200B;**Processing Profiles**。

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 按一下&#x200B;**建立**&#x200B;以建立新的處理設定檔。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 輸入&#x200B;**名稱**，例如&#x200B;**ScreensProcessingProfile**。

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 導覽至&#x200B;**Video**&#x200B;標籤以新增視訊編碼，然後按一下&#x200B;**新增**。

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 輸入&#x200B;**編碼名稱**，例如， **screens-fullhd**&#x200B;和&#x200B;**位元速率**&#x200B;為&#x200B;**2500**。

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >請確定使用以「screens — 」開頭的編碼名稱，只有這些視訊轉譯會被視為以Cloud Service形式在Screens中播放視訊體驗。 輸入適合您視訊的位元速率（720px視訊為2500kbps,1080px為5000 kbps）。

   >[!NOTE]
   >可以以各種寬度/高度/位元速率新增多個視訊轉譯，以便處理您的視訊。 請記住，即使裝置只播放視訊轉譯，所有螢幕轉譯仍會由Screens裝置下載。

1. 按一下&#x200B;**Save**。

1. 選取處理設定檔，然後按一下&#x200B;**將設定檔套用至資料夾**。

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 選取要保留Screens影片的資料夾，然後按一下&#x200B;**Apply**。

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 您可以建立多個處理設定檔並將其套用至對應的資料夾，以便這些資料夾中的視訊取得特定的視訊轉譯。
   >* 將任何影片上傳至套用「處理」設定檔的資料夾時，會處理影片並建立已設定的轉譯，供「螢幕」裝置進一步用來播放影片。


