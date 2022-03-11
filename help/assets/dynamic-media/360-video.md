---
title: 360/VR視頻
description: 瞭解如何在Dynamic Media使用360和虛擬現實(VR)視頻。
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: fa6de4e383b4de628938fce455f321911cad452c
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 360/VR視頻 {#vr-video}

360°的視頻同時記錄每個方向的視圖。 它們是用全向相機或一組相機拍攝的。 在回放期間，在平面顯示器上，用戶可以控制視角；在移動設備上播放通常應用其內置的陀螺控制。

Dynamic Media提供360個視頻資產的本地支援。 預設情況下，查看或回放不需要其他配置。 使用標準視頻擴展(如.mp4、.mkv和.mov)提供360視頻。 最常見的編解碼器是H.264。

可以使用360/VR視頻查看器來渲染等長形視頻。 結果是，您可以在房間、房產、位置、景觀、醫療程式等方面體驗到身臨其境的觀看體驗。

當前不支援空間音頻；如果立體聲中混合了音頻，則餘額(L/R)不會隨著客戶更改攝像機視角而改變。

請參閱 [將Dynamic Media360視頻和自定義視頻縮略圖與AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media)。

另請參閱 [管理查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 360視頻正在執行 {#video-in-action}

選擇 [360號空間站](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 開啟瀏覽器窗口，觀看360度視頻。 在視頻回放期間，將指針拖動到新位置以更改視角。

![360視頻示例](assets/6_5_360videoiss_simplified.png)
*360空間站視頻幀*

## 360/VR視頻和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro查看和編輯360/VR素材。 例如，您可以將徽標和文本正確放置在場景中，並應用專門為等矩形介質設計的效果和過渡。

請參閱 [編輯360/VR視頻](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上載用於360視頻查看器的資產 {#uploading-assets-for-use-with-the-video-viewer}

上傳到的360個視頻資產 [!DNL Experience Manager] 標籤為 **多媒體** 在「資產」頁面上，與普通視頻資產類似。

![6_5_360視頻選擇預覽](assets/6_5_360video-selecttopreview.png)
*在「卡」視圖中看到已上載360個視頻資產。 該資產被標籤為「多媒體」。*

**上載用於360視頻查看器的資產：**

1. 已建立專用於360視頻資產的資料夾。
1. [將自適應視頻配置檔案應用到資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   與標準非360視頻內容相比，呈現360視頻內容對源視頻解析度和編碼格式副本解析度的要求更高。

   您可以使用現成的Adaptive Video Profile（自適應視頻配置檔案），該配置檔案已隨Dynamic Media提供。 但是，它會使360視頻質量明顯低於使用非360視頻查看器呈現的相同設定編碼的非360視頻。 因此，如果需要高質量360視頻，請執行以下操作：

   * 理想情況下，您的原始360視頻內容具有下列解析度之一：

      * 1080p - 1920 x 1080，稱為全高清或全高清解析度或，
      * 2160p - 3840 x 2160，稱為4k、UHD或Ultra高清解析度。 這種大的顯示解析度通常在高端電視機和電腦顯示器上找到。 2160p解析度通常稱為「4k」，因為寬度接近4000像素。 換句話說，它的像素是1080p的四倍。
   * [建立自定義自適應視頻配置檔案](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 以更高質量的格式副本。 例如，可以建立包含以下三種設定的自適應視頻配置檔案：

      * 寬度=自動；高度=720;比特率= 2500 kbps
      * 寬度=自動；高度=1080;比特率= 5000 kbps
      * 寬度=自動；高度=1440;比特率= 6600 kbps
   * 處理專用於360個視頻資產的資料夾中的360個視頻內容。

   這種方法對最終用戶的網路和CPU提出了更高的要求。

1. [將視頻上載到資料夾](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## 預覽360視頻 {#previewing-video}

您可以使用「預覽」查看360視頻對客戶的顯示方式，並確保其正常運行。

另請參閱 [編輯查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets)。

如果您對360視頻滿意，可以發佈該視頻。

請參閱 [在網頁上嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。
請參閱 [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容具有與相對URL(特別是與 [!DNL Experience Manager Sites] 頁。
請參閱 [將Dynamic Media資產添加到頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

**要預覽360個視頻：**

1. 在 **[!UICONTROL 資產]**，導航到您建立的現有360視頻。 要在預覽模式下開啟它，請選擇360視頻資產。

   ![6_5_360視頻選擇預覽–1](assets/6_5_360video-selecttopreview-1.png)

   要預覽視頻，請選擇360視頻資產。

1. 在預覽頁面的左上角附近，選擇下拉清單，然後選擇 **[!UICONTROL 查看者]**。

   ![6_5_360視頻預覽 — 查看器](assets/6_5_360video-preview-viewers.png)

   從「查看者」清單中，選擇 **[!UICONTROL Video360_social]**，然後執行以下操作之一：

   * 要更改靜態場景的視角，請將指針拖動到視頻上。
   * 要開始播放，請選擇視頻 **[!UICONTROL 播放]** 按鈕 播放視頻時，將指針拖過視頻以更改視角。

   ![6_5_360視頻預覽 — video360-social ](assets/6_5_360video-preview-video360-social.png)*360個視頻截圖。*

   * 從「查看者」清單中，選擇 **[!UICONTROL Video360VR]**。

      虛擬現實(VR)視頻是使用虛擬現實耳機訪問的沈浸式視頻內容。 與普通視頻一樣，在開始錄制或使用360°攝像頭捕獲視頻時，您會建立VR視頻。
   ![6_5_360視頻預覽 — video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR視頻螢幕截圖*

1. 在預覽頁面右上角附近，選擇 **[!UICONTROL 關閉]**。

## 發佈360視頻 {#publishing-video}

要使用360視頻，必須發佈它。 發佈360視頻會激活URL和嵌入代碼。 它還將360視頻發佈到Dynamic Media雲，該雲與CDN整合，可進行可擴展和效能交付。

請參閱 [出版Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 有關如何發佈360視頻的詳細資訊。
另請參閱 [在網頁上嵌入視頻或影像查看器](/help/assets/dynamic-media/embed-code.md)。
另請參閱 [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容具有與相對URL(特別是與 [!DNL Experience Manager Sites] 頁。
另請參閱 [將Dynamic Media資產添加到頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
