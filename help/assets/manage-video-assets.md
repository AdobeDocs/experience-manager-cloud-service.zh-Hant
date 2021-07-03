---
title: 管理影片資產
description: 在 [!DNL Adobe Experience Manager]中上傳、預覽、加上注釋及發佈視訊資產。
contentOwner: AG
feature: 資產管理，發佈，協作，視頻
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 6%

---

# 管理影片資產 {#manage-video-assets}

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，可在影片資產建立後管理其整個生命週期。

了解如何在[!DNL Adobe Experience Manager Assets]中管理和編輯視訊資產。 可使用「處理設定檔」和使用[!DNL Dynamic Media]整合，對視訊編碼和轉碼（例如FFmpeg轉碼）進行編碼。 若沒有[!DNL Dynamic Media]授權，[!DNL Experience Manager]便提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援檔案格式的預覽縮圖，以及在使用者介面中預覽直接支援在瀏覽器中播放的格式。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 以副檔名MP4產生視訊資產的預覽。您可以在[!DNL Assets]使用者介面中預覽轉譯。

1. 在數位資產資料夾或子資料夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下工具列中的「**[!UICONTROL 建立]**」，然後選擇「**[!UICONTROL 檔案]**」。 或者，在用戶介面上拖動檔案。 如需詳細資訊，請參閱[上傳資產](manage-digital-assets.md#uploading-assets)。
1. 若要在卡片檢視中預覽視訊，請按一下視訊資產上的&#x200B;**[!UICONTROL Play]** ![play選項](assets/do-not-localize/play.png)選項。 您只能在卡片檢視中暫停或播放視訊。 清單檢視中無法使用[!UICONTROL Play]和[!UICONTROL Pause]選項。
1. 若要在資產詳細資訊頁面中預覽視訊，請選取卡片上的&#x200B;**[!UICONTROL Edit]** 。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL的形式包含在網頁中，或直接內嵌資產。 如需詳細資訊，請參閱[publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 使用處理設定檔進行轉碼 {#transcode-video}

[!DNL Experience Manager] as a可讓 [!DNL Cloud Service] 您使用「處理設定檔」來執行MP4視訊檔案的基本轉碼。此功能不僅可讓您上傳，還可預覽和縮放MP4視訊檔案。

![在中建立視訊轉碼的處理設定檔  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：中的視訊轉碼處理設 [!DNL Experience Manager]定檔。*

如果您只提供寬度或高度，並將其他欄位留空，轉譯會維持外觀比例。 H.264視訊轉碼器可供轉碼使用。

若要使用處理設定檔來處理資產，請新增設定檔至資料夾。 請參閱[使用處理設定檔來處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 為視訊資產加上注釋 {#annotate-video-assets}

1. 在[!DNL Assets]控制台中，選取資產卡上的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示資產詳細資訊頁面。
1. 若要播放視訊，請按一下&#x200B;**[!UICONTROL 預覽]**。
1. 若要為視訊加上注釋，請按一下「**[!UICONTROL 注釋]**」。 在視訊中的特定時間（幀）添加註釋。 批注時，可以在畫布上繪圖，並在繪圖中包括注釋。 注釋會自動儲存。 要退出注釋嚮導，請按一下&#x200B;**[!UICONTROL Close]**。
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 要在時間軸中查看它，請按一下注釋。 要從時間軸中刪除注釋，請按一下&#x200B;**[!UICONTROL Delete]**。

## 最佳實務和限制 {#tips-limitations}

* 若沒有[!DNL Dynamic Media]授權，您只能使用處理設定檔來處理MP4檔案。
* 使用處理設定檔將MP4檔案轉碼時，會套用下列准則和限制：

   * Apple ProRes檔案只能將代碼轉換至解析度上限1080p。
   * 如果源檔案的位元速率大於200 Mbps，則只能將代碼轉換到最大解析度為1080p。
   * 如果源幀數>=60 fps，則可以使用的源檔案的最大大小為，

      * 400 MB（4k轉碼）。
      * 800 MB（1080p轉碼）。
      * 8 GB（720p轉碼）。
   * 可將代碼轉換為4k解析度的最大檔案大小為2.55 GB MP4檔案，解析度為4k、12 Mbps位元速率和23 fps。


>[!MORELIKETHIS]
>
>* [Dynamic Media影片檔案](/help/assets/dynamic-media/video.md)。
>* [深入了解處理設定檔的使用、類型和設定](/help/assets/asset-microservices-configure-and-use.md)。

