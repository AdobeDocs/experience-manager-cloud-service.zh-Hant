---
title: 在螢幕中建立螢幕視訊轉譯作為Cloud Service
description: 本頁面說明如何在Screens中建立Screens視訊轉譯作為Cloud Service。
source-git-commit: ec939ac6a91523a9ba64a555943eba8e6da071eb
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 在螢幕中建立螢幕視訊轉譯作為Cloud Service {#creating-screens-video-renditions}

## 簡介 {#introduction}

本指南將說明如何建立在Screens播放器中使用的視訊轉譯。

>[!IMPORTANT]
>如果您打算在Screens頻道中使用視訊，則必須設定本節強調顯示的步驟。

## 在Screens中建立Screens視訊轉譯作為Cloud Service的步驟 {#steps-creating-screens-video-renditions}

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


   >[!IMPORTANT]
   >請確定使用以「screens — 」開頭的編碼名稱，只有這些視訊轉譯會被視為以「Screens As a」Cloud Service播放視訊體驗。 輸入適合您視訊的位元速率（720px視訊為2500kbps,1080px為5000 kbps）

   >[!NOTE]
   >您可以根據您的需求，以不同寬度/高度/位元速率新增多個視訊轉譯，但請記住，即使裝置僅播放視訊轉譯，所有螢幕轉譯都會由Screens裝置下載。

1. 按一下儲存

1. 選取處理設定檔，然後按一下「將設定檔套用至資料夾」

1. 選取要保留Screens影片的資料夾，然後按一下「套用」

1. 您可以建立多個處理設定檔並將其套用至對應的資料夾，以便這些資料夾中的視訊取得特定的視訊轉譯

1. 將任何影片上傳至套用「處理」設定檔的資料夾時，會處理影片並建立已設定的轉譯，供「螢幕」裝置用來播放影片。

