---
title: 在中管理視訊資產 [!DNL Adobe Experience Manager]。
description: 在中上傳、預覽、註解和發佈視訊資產 [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d6a0848547a6dcbb058576827d3cacbc8045ae79
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 6%

---


# 管理影片資產 {#manage-video-assets}

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，以管理視訊資產在建立後的整個生命週期。

瞭解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]。 使用「處理設定檔」和整合，就可進行視訊編碼和轉碼，例如FFmpeg轉 [!DNL Dynamic Media] 碼。 無需 [!DNL Dynamic Media] 授權 [!DNL Experience Manager] ，即可提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援檔案格式的預覽縮圖，以及在使用者介面中預覽可直接在瀏覽器中播放的格式。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 使用擴充功能MP4產生視訊資產的預覽。 您可以在使用者介面中預覽 [!DNL Assets] 轉譯。

1. 在數位資產檔案夾或子檔案夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下工 **[!UICONTROL 具列中]** 的「建立」，然後選 **[!UICONTROL 擇「檔案」]**。 或者，在用戶介面上拖動檔案。 如需詳 [細資訊，請參閱](manage-digital-assets.md#uploading-assets) 「上傳資產」。
1. 若要在卡片檢視中預覽視訊，請按一下 **[!UICONTROL 視訊資產]**![上的「播放](assets/do-not-localize/play.png) 」選項。 您只能在卡片檢視中暫停或播放影片。 「播 [!UICONTROL 放] 」和「暫 [!UICONTROL 停] 」選項在清單檢視中不可用。
1. 若要在資產詳細資訊頁面中預覽視訊，請選 **[!UICONTROL 取卡片上的]** 「編輯」。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產加入網頁中做為URL，或直接內嵌資產。 如需詳細資訊，請參 [閱「發佈動態媒體資產」](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 使用處理設定檔進行轉碼 {#transcode-video}

[!DNL Experience Manager] 「雲端服務」可讓您使用「處理設定檔」進行MP4視訊檔的基本轉碼。 此功能可讓您不僅上傳，還預覽和縮放MP4視訊檔案。

![在Experience Manager中建立視訊轉碼的處理設定檔](assets/video-processing-profile-for-mp4.png)

*圖：中用於視頻轉碼的處理配置檔案[!DNL Experience Manager]。*

如果您只提供寬度或高度，而將其他欄位留空，轉譯會維持高寬比。 目前，僅h264 codec可用於轉碼。

若要使用處理設定檔來處理資產，請新增設定檔至資料夾。 請參 [閱使用處理設定檔處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 註解視訊資產 {#annotate-video-assets}

1. 在主控 [!DNL Assets] 台中，選取資 **[!UICONTROL 產卡上的「編輯]** 」以顯示資產詳細資訊頁面。
1. 若要播放影片，請按一下「 **[!UICONTROL 預覽]**」。
1. 若要註解視訊，請按一下「注 **[!UICONTROL 解」]**。 在視訊中的特定時間（畫格）加入註解。 在加上註解時，您可以在畫布上繪圖，並在繪圖中加入註解。 注釋會自動儲存。 要退出注釋嚮導，請按一下「關 **[!UICONTROL 閉」]**。
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 要在時間軸中查看，請按一下注釋。 要從時間軸刪除注釋，請按一下「刪 **[!UICONTROL 除」]**。

## 最佳做法和限制 {#tips-limitations}

* 若沒有Dynamic Media授權，您只能使用處理設定檔來處理MP4檔案。
* 使用

>[!MORELIKETHIS]
>
>* [動態媒體視訊檔案](/help/assets/dynamic-media/video.md)。
>* [進一步瞭解處理設定檔的使用、類型和設定](/help/assets/asset-microservices-configure-and-use.md)。

