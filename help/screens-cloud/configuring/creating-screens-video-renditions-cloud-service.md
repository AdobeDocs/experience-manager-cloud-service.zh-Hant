---
title: 在螢幕中建立視頻格式副本as a Cloud Service
description: 此頁介紹如何在螢幕as a Cloud Service中建立視頻格式副本。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 在螢幕中建立視頻格式副本as a Cloud Service {#creating-screens-video-renditions}

## 簡介 {#introduction}

本節介紹如何建立在螢幕播放器中使用的視頻格式副本。

>[!IMPORTANT]
>如果計畫在「螢幕」通道中使用視頻，則必須配置本節中突出顯示的步驟。

## 在螢幕中建立視頻格式副本的步驟as a Cloud Service {#steps-creating-screens-video-renditions}

按照以下步驟在「螢幕」中建立視頻格式副本，該螢幕as a Cloud Service於「螢幕內容提供程式」：

1. 在「螢幕內容提供程式」中導航到您的頻道。

   >[!NOTE]
   >請參閱 [使用螢幕內容提供程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) 的子菜單。

1. 按一下左導航欄中的「工具」部分，然後按一下 **資產** 然後按一下 **處理配置檔案**。

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 按一下 **建立** 建立新的處理配置檔案。

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 輸入 **名稱**，例如 **螢幕處理配置檔案**。

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 導航到 **視頻** 頁籤，添加視頻編碼並按一下 **添加新**。

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 輸入 **編碼名稱** 例如， **螢幕全高清** 和 **比特率** 如 **2500**。

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >請確保使用以「screens — 」開頭的「Encoding（編碼）」名稱，只有這些視頻格式副本才被視為在「Screensas a Cloud Service」中播放視頻體驗。 輸入視頻的比特率（720px視頻為2500kbps,1080px為5000 kbps）。

   >[!NOTE]
   >可以添加多個視頻格式副本，其寬度/高度/比特率可變，以處理您的視頻。 請記住，所有螢幕格式副本都將由「螢幕」設備下載，即使該設備只播放視頻格式副本。

1. 按一下 **保存**。

1. 選擇「處理」配置檔案，然後按一下 **將配置檔案應用到資料夾**。

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 選擇保留「螢幕」視頻的資料夾，然後按一下 **應用**。

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* 您可以建立多個「處理」配置檔案並將其應用到相應的資料夾，以便這些資料夾中的視頻獲得特定的視頻格式副本。
   >* 將任何視頻上載到應用「處理」配置檔案的資料夾時，會處理視頻並建立配置的格式副本，螢幕設備會進一步使用這些格式副本來播放視頻。

