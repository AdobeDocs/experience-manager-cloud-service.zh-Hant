---
title: 管理影片資產
description: 在中上載、預覽、注釋和發佈視頻資產 [!DNL Adobe Experience Manager]。
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 038dbc4b0febfa58f69e05f837760162210f8689
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 6%

---

# 管理影片資產 {#manage-video-assets}

視頻格式是組織數字資產的關鍵部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，以在視頻資產建立後管理其整個生命週期。

瞭解如何在中管理和編輯視頻資產 [!DNL Adobe Experience Manager Assets]。 視頻編碼和轉碼，例如，FFmpeg轉碼，可以使用處理配置檔案和使用 [!DNL Dynamic Media] 整合。 沒有 [!DNL Dynamic Media] 許可證， [!DNL Experience Manager] 為視頻提供基本支援，如使用FFmpeg轉碼、提取支援的檔案格式的預覽縮略圖，以及在用戶介面中預覽直接支援在瀏覽器中播放的格式。

## 上載和預覽視頻資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 為副檔名為MP4的視頻資產生成預覽。 您可以在 [!DNL Assets] 用戶介面。

1. 在數字資產資料夾或子資料夾中，導航到要添加數字資產的位置。
1. 要上載資產，請按一下 **[!UICONTROL 建立]** ，然後選擇 **[!UICONTROL 檔案]**。 或者，在用戶介面上拖動檔案。 請參閱 [上載資產](manage-digital-assets.md#uploading-assets) 的雙曲餘切值。
1. 要在卡視圖中預覽視頻，請按一下 **[!UICONTROL 播放]** ![播放選項](assets/do-not-localize/play.png) 的子菜單。 您只能在卡視圖中暫停或播放視頻。 的 [!UICONTROL 播放] 和 [!UICONTROL 暫停] 選項在清單視圖中不可用。
1. 要在資產詳細資訊頁面中預覽視頻，請選擇 **[!UICONTROL 編輯]** 卡上。 視頻在瀏覽器的本機視頻播放器中播放。 您可以播放、暫停、控制音量，並將視頻縮放到全屏。

## 發佈視頻資產 {#publish-video-assets}

發佈後，可以將視頻資產作為URL包括在網頁中，或直接嵌入資產。 有關詳細資訊，請參閱 [發佈 [!DNL Dynamic Media] 資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 使用處理配置檔案進行轉碼 {#transcode-video}

[!DNL Experience Manager] 作為 [!DNL Cloud Service] 允許您使用「處理配置檔案」對MP4視頻檔案執行基本轉碼。 該功能不僅允許您上載MP4視頻檔案，還允許您預覽和縮放MP4視頻檔案。

![建立處理配置檔案以在中進行視頻轉碼 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：一種視頻轉碼處理簡檔 [!DNL Experience Manager]。*

如果僅提供寬度或僅提供高度，並將其他欄位留空，則格式副本將保持長寬比。 H.264視頻編解碼器可用於轉碼。

要使用處理配置檔案處理資產，請將配置檔案添加到資料夾。 請參閱 [使用處理配置檔案處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 注釋視頻資產 {#annotate-video-assets}

您可以向視頻資產添加註釋。 在注釋視頻時，播放器會暫停以允許您在框架上進行注釋。 有關詳細資訊，請參閱 [管理視頻資產](manage-video-assets.md)。

>[!NOTE]
>
>視頻資產批注尚不支援MXF視頻格式。

1. 從 [!DNL Assets] 控制台，選擇 **[!UICONTROL 編輯]** 顯示資產詳細資訊頁面。
1. 要播放視頻，請按一下 **[!UICONTROL 預覽]**。
1. 要注釋視頻，請按一下 **[!UICONTROL 注釋]**。 在視頻中的特定時間（幀）添加註釋。 注釋時，可以在畫布上進行繪製，並在繪圖中包括注釋。 注釋將自動保存。 要退出注釋嚮導，請按一下 **[!UICONTROL 關閉]**。
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 要在時間軸中查看它，請按一下注釋。 要從時間軸中刪除注釋，請按一下 **[!UICONTROL 刪除]**。

## 最佳做法和限制 {#tips-limitations}

* 沒有 [!DNL Dynamic Media] 許可證，您只能使用處理配置檔案處理MP4檔案。
* 使用「處理配置檔案」對MP4檔案進行轉碼時，將適用以下准則和限制：

   * AppleProRes檔案只能將代碼轉換為最大解析度1080p。
   * 如果源檔案的比特率大於200 Mbps，則只能將代碼轉碼到最大解析度1080p。
   * 如果源幀數>=60 fps，則可以使用的源檔案的最大大小為，

      * 400 MB，用於4k轉碼。
      * 800 MB用於1080p轉碼。
      * 8 GB用於720p轉碼。
   * 可轉碼到4k解析度的最大檔案大小為2.55 GB MP4檔案，解析度為4k、12 Mbps比特率和23 fps。


>[!MORELIKETHIS]
>
>* [Dynamic Media視頻文檔](/help/assets/dynamic-media/video.md)。
>* [瞭解有關處理配置檔案的使用、類型和配置的更多資訊](/help/assets/asset-microservices-configure-and-use.md)。

