---
title: 在Screens中建立視訊轉譯as a Cloud Service
description: 本頁面說明如何在Screens中建立視訊轉譯as a Cloud Service。
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 在Screens中建立視訊轉譯as a Cloud Service {#creating-screens-video-renditions}

## 簡介 {#introduction}

本節說明如何建立Screens播放器中使用的視訊轉譯。

>[!IMPORTANT]
>如果您打算在Screens管道中使用影片，則必須設定本節中重點說明的步驟。

## 在Screens中建立視訊轉譯的步驟as a Cloud Service {#steps-creating-screens-video-renditions}

請依照下列步驟，從Screens內容提供者在Screens as a Cloud Service中建立視訊轉譯：

1. 在Screens內容提供者中導覽至您的管道。

   >[!NOTE]
   >如需詳細資訊，請參閱[使用Screens內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=zh-Hant#screens-content-provider)。

1. 從左側導覽列按一下[工具]區段，然後按一下&#x200B;**Assets**，然後按一下&#x200B;**處理設定檔**。

   ![按一下處理設定檔](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. 按一下&#x200B;**建立**&#x200B;以建立處理設定檔。

   ![按一下[建立]](/help/screens-cloud/assets/configure/screens-video-2.png)

1. 輸入&#x200B;**名稱**，例如&#x200B;**ScreensProcessingProfile**。

   ![處理設定檔對話方塊，其中顯示醒目提示的名稱欄位。](/help/screens-cloud/assets/configure/screens-video-3.png)

1. 瀏覽至&#x200B;**視訊**&#x200B;標籤，讓您新增視訊編碼，然後按一下&#x200B;**新增**。

   ![顯示[新增]按鈕的[處理設定檔]對話方塊醒目提示。](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. 輸入&#x200B;**編碼名稱**，例如，**screens-fullhd**&#x200B;和&#x200B;**Bitrate**，作為&#x200B;**2500**。

   ![顯示[儲存]按鈕的[處理設定檔]對話方塊。](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >使用以「screens — 」開頭的編碼名稱。 在Screens as a Cloud Service中播放視訊體驗時，只會考慮使用這些視訊轉譯。 輸入適合您視訊的位元速率（720-px視訊為2500 kbps，1080 px為5000 kbps）。

   >[!NOTE]
   >您可以新增多種視訊轉譯，並具有不同的寬度/高度/位元速率，以使用您的視訊。 Screens裝置會下載所有熒幕和轉譯，即使裝置僅播放視訊轉譯亦然。

1. 按一下「**儲存**」。

1. 選取處理設定檔，然後按一下&#x200B;**將設定檔套用至資料夾**。

   ![將設定檔套用至資料夾](/help/screens-cloud/assets/configure/screens-video-5.png)

1. 選取保留Screens影片的資料夾，然後按一下[套用]。**&#x200B;**

   ![按一下套用](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* 您可以建立多個處理設定檔，並將其套用至對應的資料夾，以便這些資料夾中的視訊取得特定的視訊轉譯。
   >* 當您上傳任何視訊至套用處理設定檔的資料夾時，系統會處理視訊。 已設定的轉譯會建立，供Screens裝置用來播放視訊。
