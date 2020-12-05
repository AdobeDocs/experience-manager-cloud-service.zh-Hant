---
title: 360/VR視訊
description: 瞭解如何在動態媒體中處理360和虛擬實境(VR)視訊。
translation-type: tm+mt
source-git-commit: 59d3f95db8ac4b779207bcf3d260067abea40d93
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# 360/VR視訊{#vr-video}

360度影片可同時錄制每個方向的檢視。 它們是使用全方位的相機或一組相機拍攝的。 在平面顯示器上播放時，用戶可以控制視角；在行動裝置上播放時，通常會運用其內建的陀螺控制項。

Dynamic Media包含360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您可使用標準的視訊副檔名（例如。mp4、.mkv和。mov）來傳送360視訊。 最常見的轉碼器是H.264。

本節說明如何與360/VR視訊檢視器搭配使用，以產生等長形視訊，提供身歷其境的房間、財產、位置、風景、醫療程式等觀賞體驗。

目前不支援空間音訊；如果音訊混合在立體聲中，則餘額(L/R)不會隨著客戶變更相機視角而改變。

請參閱「搭配AEM Assets使用動態媒體360視訊和自訂視訊縮圖」[。](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html)

另請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 360視訊的實際運作{#video-in-action}

點選[空間站360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)以開啟瀏覽器視窗並觀看360度視訊。 在視訊播放期間，將滑鼠指標拖曳至新位置以變更檢視角度。

![360視訊范](assets/6_5_360videoiss_simplified.png)
*例來自空間站360的視訊影格*

## 360/VR視訊與Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用Adobe Premier Pro來檢視和編輯360/VR素材。 例如，您可以將標誌和文字正確置入場景中，並套用專為等矩形媒體而設計的效果和轉場效果。

請參閱[編輯360/VR視訊](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上傳資產以搭配360視訊檢視器{#uploading-assets-for-use-with-the-video-viewer}使用

360個上傳至Experience Manager的視訊資產在「資產」頁面上標示為&#x200B;**Multimedia**，與一般視訊資產類似。

![6_5_360video-selectpreview在卡片檢](assets/6_5_360video-selecttopreview.png)
*視中可看到已上傳的360視訊資產。資產標示為「多媒體」。*

**若要上傳資產以搭配360視訊檢視器使用：**

1. 已建立專用於360視訊資產的資料夾。
1. [將最適化視訊描述檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   轉譯360視訊內容比標準非360視訊內容對來源視訊解析度和編碼轉譯解析度的要求更高。

   您可以使用動態媒體隨附的現成可用最適化視訊設定檔。 但是，請注意，相較於使用非360視訊檢視器所轉譯的相同設定來編碼的非360視訊，它會造成明顯低於360視訊品質。 因此，如果需要高品質的360視訊，請執行下列動作：

   * 理想情況下，您的原始360視訊內容應具備下列其中一種解析度：

      * 1080p - 1920 x 1080，稱為全高清或全高清解析度，或
      * 2160p - 3840 x 2160，稱為4K、UHD或Ultra HD解析度。 這種超大的顯示解析度，最常出現在優質的電視機和電腦螢幕上。 2160p的解析度通常稱為「4K」，因為寬度接近4000像素。 換言之，它提供1080p像素的4倍。
   * [建立具有更高品質轉譯的自](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 訂最適化視訊分析。例如，您可能想要建立包含下列三種設定的最適化視訊描述檔：

      * width=auto;height=720;位元速率=2500 kbps
      * width=auto;height=1080;位元速率=5000 kbps
      * width=auto;height=1440;位元速率=6600 kbps
   * 在專屬於360個視訊資產的資料夾中處理360個視訊內容。

   請注意，此方法也會對使用者的網路和CPU提出更高的需求。

1. [將視訊上傳至資料夾](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。

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

## 預覽360視訊{#previewing-video}

您可以使用「預覽」來查看您的360視訊對客戶的外觀，並確保其運作如預期。

另請參閱[編輯查看器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets)。

當您對360視訊感到滿意時，就可以發佈它。

請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/dynamic-media/embed-code.md)。
請參閱[將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 請注意，如果您的互動式內容具有相對URL的連結，尤其是Experience Manager Sites頁面的連結，則無法使用以URL為基礎的連結方法。
請參閱[新增動態媒體資產至頁面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**若要預覽360個視訊**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您所建立的現有360視訊。 點選「360視訊」資產，以預覽模式開啟它。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   點選360視訊資產以預覽視訊。

1. 在預覽頁面上，在頁面左上角附近點選下拉式清單，然後選取&#x200B;**[!UICONTROL 檢視器]**。

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   從「檢視器」清單中，點選&#x200B;**[!UICONTROL Video360_social]**，然後執行下列其中一項作業：

   * 將滑鼠指標拖曳至視訊上，以變更靜態場景的檢視角度。
   * 點選視訊的&#x200B;**[!UICONTROL 播放]**&#x200B;按鈕以開始播放；當視訊播放時，拖曳滑鼠指標至視訊上，以改變您的檢視角度。

   ![6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360視訊螢幕擷取。*

   * 從「檢視器」清單中，點選「**[!UICONTROL Video360VR]**」。

      虛擬實境(VR)視訊是身歷其境的視訊內容，可透過使用虛擬實境頭戴式裝置存取。 和一般視訊一樣，當您使用360度的視訊相機錄制或擷取視訊時，就會在開始時建立VR視訊。
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR視訊的螢幕擷取。*

1. 在預覽頁面的右上方附近，點選&#x200B;**[!UICONTROL Close]**。

## 發佈360視訊{#publishing-video}

您必須發佈360視訊才能使用。 發佈360視訊會啟動URL和內嵌代碼。 此外，它還將360視訊發佈至與CDN整合的Dynamic Media雲端，以進行可擴充且具效能的傳送。

如需如何發佈360視訊的詳細資訊，請參閱[發佈動態媒體資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
另請參閱[將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)。
另請參閱[將URL連結到您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 請注意，如果您的互動式內容具有相對URL的連結，尤其是Experience Manager Sites頁面的連結，則無法使用以URL為基礎的連結方法。
另請參閱[新增動態媒體資產至頁面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
