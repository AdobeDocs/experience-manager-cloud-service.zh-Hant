---
title: 管理影片資產
description: 在 [!DNL Adobe Experience Manager]中上傳、預覽、註解和發佈視訊資產。
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---


# 管理影片資產 {#manage-video-assets}

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，以管理視訊資產在建立後的整個生命週期。

瞭解如何在[!DNL Adobe Experience Manager Assets]中管理和編輯視訊資產。 使用「處理設定檔」和[!DNL Dynamic Media]整合，就可進行視訊編碼和轉碼，例如FFmpeg轉碼。 沒有[!DNL Dynamic Media]授權，[!DNL Experience Manager]提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援檔案格式的預覽縮圖，以及直接在瀏覽器中播放的支援格式，在使用者介面中預覽。

## 上傳和預覽視訊資產{#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 使用擴充功能MP4產生視訊資產的預覽。您可以在[!DNL Assets]使用者介面中預覽轉譯。

1. 在數位資產檔案夾或子檔案夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請從工具列按一下「建立」，然後選擇「檔案」。 ********&#x200B;或者，在用戶介面上拖動檔案。 如需詳細資訊，請參閱[上傳資產](manage-digital-assets.md#uploading-assets)。
1. 若要在卡片檢視中預覽視訊，請按一下視訊資產上的&#x200B;**[!UICONTROL Play]**![play選項](assets/do-not-localize/play.png)選項。 您只能在卡片檢視中暫停或播放影片。 清單檢視中不提供[!UICONTROL Play]和[!UICONTROL Pause]選項。
1. 若要在資產詳細資訊頁面中預覽視訊，請在資訊卡上選取「編輯」。 ****&#x200B;視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

## 發佈視訊資產{#publish-video-assets}

發佈後，您可以將視訊資產加入網頁中做為URL，或直接內嵌資產。 如需詳細資訊，請參閱[publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 使用處理設定檔{#transcode-video}進行轉碼

[!DNL Experience Manager] as as  [!DNL Cloud Service] lots you do basic codecing of MP4 video files using Processing Profiles.此功能可讓您不僅上傳，還預覽和縮放MP4視訊檔案。

![建立處理設定檔，以在  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：中用於視頻轉碼的處理配置檔案 [!DNL Experience Manager]。*

如果您只提供寬度或高度，而將其他欄位留空，轉譯會維持高寬比。 H.264視訊轉碼器可供轉碼。

若要使用處理設定檔來處理資產，請新增設定檔至資料夾。 請參閱[使用處理設定檔來處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 註解視訊資產{#annotate-video-assets}

1. 在[!DNL Assets]主控台中，選取資產卡上的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示資產詳細資訊頁面。
1. 若要播放視訊，請按一下「預覽」。****
1. 若要註解視訊，請按一下「**[!UICONTROL 註解]**」。 在視訊中的特定時間（畫格）加入註解。 在加上註解時，您可以在畫布上繪圖，並在繪圖中加入註解。 注釋會自動儲存。 要退出注釋嚮導，請按一下&#x200B;**[!UICONTROL 關閉]**。
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 要在時間軸中查看，請按一下注釋。 要從時間軸刪除注釋，請按一下&#x200B;**[!UICONTROL Delete]**。

## 最佳做法和限制{#tips-limitations}

* 沒有[!DNL Dynamic Media]授權，您只能使用處理設定檔來處理MP4檔案。
* 使用處理設定檔轉碼MP4檔案時，會套用下列准則和限制：

   * Apple ProRes檔案只能轉碼至最高解析度1080p。
   * 如果源檔案的位元速率>200 Mbps，則只能將代碼轉碼到最大解析度1080p。
   * 如果來源影格>=60 fps，則您可使用的來源檔案大小上限為：

      * 400 MB的4K轉碼。
      * 800 MB的1080p轉碼。
      * 8 GB的720p轉碼。
   * 可轉碼至4k解析度的檔案大小上限為2.55 GB MP4檔案，解析度為4k、12 Mbps位元速率和23 fps。


>[!MORELIKETHIS]
>
>* [Dynamic Media視訊檔案](/help/assets/dynamic-media/video.md)。
>* [進一步瞭解處理設定檔的使用、類型和設定](/help/assets/asset-microservices-configure-and-use.md)。

