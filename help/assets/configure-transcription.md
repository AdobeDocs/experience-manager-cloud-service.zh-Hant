---
title: 設定轉錄服務
seo-title: Configure transcription service
description: Adobe Experience Manager資產已設定為 [!DNL Azure Media Services] 會以WebVTT (vtt)格式自動產生支援音訊或視訊檔案中的口語文字記錄。
seo-description: When an audio or video asset is processed in Experience Manager Assets, the AI-based transcription service automatically generates the text transcript rendition of the audio or video asset and stores it at the same location within your Assets repository where the original asset resides. The Experience Manager Assets transcription service allows marketers to effectively manage their audio and video content with added discoverability of the text content and increase the ROI of these assets by supporting accessibility and localization.
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
exl-id: e96c8d68-74a6-4d61-82dc-20e619338d4b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# 在中設定轉錄 [!DNL Experience Manager Assets] {#configure-transcription-service}

轉錄是使用語音辨識技術，將音訊或視訊檔案中的音訊轉換為文字（語音轉換為文字）的過程。
[!DNL Adobe Experience Manager Assets] 已設定為 [!DNL Azure Media Services] 它會自動產生WebVTT (.vtt)格式之支援音訊或視訊檔案中的口語文字記錄。 在中處理音訊或視訊資產時 [!DNL Experience Manager Assets]，轉錄服務會自動產生音訊或視訊資產的文字轉錄轉譯，並將其儲存在原始資產所在的Assets存放庫中的相同位置。 此 [!DNL Experience Manager Assets] 轉錄服務可讓行銷人員透過新增的文字內容可發現性來有效管理其音訊和視訊內容，並透過支援可存取性和本地化來提高這些資產的ROI。

文字記錄是口語內容的文字版本；例如，您在任何OTT平台上觀看的電影通常包含字幕或字幕，以協助協助協助存取或使用其他語言的內容。 或任何用於行銷、學習或娛樂目的的音訊或視訊檔案。 這些體驗從轉錄開始，然後視需要格式化或翻譯。 手動執行時，音訊或視訊的轉譯需要大量時間且容易出錯。 鑑於對音訊/視訊內容的需求不斷增加，擴展手動程式也是一個挑戰。 [!DNL Experience Manager Assets] 使用Azure的AI型轉錄，允許大規模處理音訊和視訊資產，並產生文字轉錄（.vtt檔案）和時間戳記詳細資料。 除了Assets，Dynamic Media也支援轉錄功能。

轉錄功能在中可免費使用 [!DNL Experience Manager Assets]. 但是，管理員需要使用者的Azure憑證才能在中設定轉錄服務 [!DNL Experience Manager Assets]. 您也可以 [取得試用認證](https://azure.microsoft.com/en-us/pricing/details/media-services/) 直接從Microsoft®體驗Assets的音訊或視訊轉錄功能。

## 轉錄先決條件 {#prerequisites}

1. 啟動並執行 [!DNL Experience Manager Assets as a Cloud Service] 執行個體。
1. 需要以下Azure認證才能在中設定 [!DNL Experience Manager Assets]：

   * 使用者端ID （API金鑰）
   * 使用者端秘密金鑰
   * 租使用者端點（網域）
   * 媒體帳戶
   * 資源群組
   * 訂閱ID

   另請參閱 [Azure檔案](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal) 以取得存取Azure Media Services API的認證。

1. 請確定Azure帳戶有足夠的信用額度來處理新請求。

## 在中設定轉錄 [!DNL Experience Manager Assets] {#configure-transcription}

以下是在中啟用轉錄功能所需的設定 [!DNL Experience Manager Assets]：

1. [設定Azure媒體服務](#configure-azure-media-service)
1. [設定音訊/視訊轉錄的處理設定檔](#configure-processing-profile-for-transcription)


### 設定Azure媒體服務 {#configure-azure-media-services}

[!DNL Experience Manager Assets] 使用 [!DNL Azure Media Services] 會自動產生口語文字記錄 [支援的音訊或視訊檔案](#supported-file-formats-for-transcription) WebVTT (.vtt)格式。 管理員可以設定 [!DNL Azure Media Services] 在 [!DNL Experience Manager Assets] 使用Azure認證。 此 [轉錄先決條件](#transcription-prerequisites) 列出 [!DNL Azure] 設定所需的認證。 如果您沒有 [!DNL Azure] 帳戶和認證，請參閱 [Azure媒體服務檔案](https://azure.microsoft.com/en-us/pricing/details/media-services/) 以取得試用認證。

![configure-transcription-service](assets/configure-transcription-service.png)

前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure媒體服務設定]**. 從左側邊欄選取資料夾（位置），然後按一下 [!UICONTROL 建立] 按鈕來設定與的連線 [!DNL Azure] 帳戶。 此資料夾是您的 [!DNL Azure] 雲端設定儲存在Experience Manager Assets中。 輸入 [!DNL Azure] 認證，然後按一下 **[!UICONTROL 儲存並關閉]**.

### 設定轉錄的處理設定檔 {#configure-processing-profile}

一旦 [!DNL Azure Media Services] 已在Experience Manager Assets中設定，下一步是建立資產處理設定檔，用於產生音訊和視訊資產的AI型轉錄。 AI型處理設定檔會產生 [支援的音訊或視訊資產](#supported-file-formats-for-transcription) 將轉譯為Experience Manager Assets中的轉譯，並將轉錄檔（.vtt檔案）儲存在原始資產所在的相同資料夾中。 因此，使用者更容易搜尋和找到資產及其轉譯稿。

前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]** 並按一下 **[!UICONTROL 建立]** 按鈕來建立以AI為基礎的處理設定檔，以產生音訊和視訊檔案的轉錄。 依預設，處理設定檔頁面只會反映三個索引標籤（「影像」、「視訊」和「自訂」）。 不過， **[!UICONTROL Content AI]** 索引標籤可見（如果您已設定） [!DNL Azure Media Services] 在您的 [!DNL Experience Manager Assets] 執行個體。 驗證您的 [!DNL Azure] 認證(如果您沒有看到 **[!UICONTROL Content AI]** 標籤中指定處理設定檔。

在 **[!UICONTROL Content AI]** 索引標籤上，按一下 **[!UICONTROL 新增]** 按鈕以設定轉錄。 在這裡，您可以從下拉式清單中選取檔案型別，來包含和排除用於產生轉譯的檔案格式（MIME型別）。 在下圖中，包含所有支援的音訊和視訊檔案，並排除文字檔案。

啟用 **[!UICONTROL 在相同目錄中建立VTT文字稿]** 切換以在原始資產所在的相同資料夾中建立和儲存轉錄轉譯（.vtt檔案）。 其他轉譯專案也會由預設的DAM資產處理工作流程產生，與此設定無關。

![configure-transcription-service](assets/configure-transcription-profile.png)

下圖詳細說明在Experience Manager Assets中建立的自訂視訊設定檔。

![configure-transcription-service](assets/video-processing-profile.png)

視訊設定檔也包含下列自訂設定。 另請參閱 [處理設定檔檔案](/help/assets/asset-microservices-configure-and-use.md) 以取得有關如何建立自訂處理設定檔的詳細資訊。

![configure-transcription-service](assets/video-processing-profile2.png)

現在，讓我們在此視訊設定檔中設定轉錄。 導覽至 **[!UICONTROL Content AI]** 標籤並按一下 **[!UICONTROL 新增]** 按鈕。 包含所有音訊和視訊檔案，並排除影像和應用程式檔案。 啟用 **[!UICONTROL 在相同目錄中建立VTT文字稿]** 切換並儲存設定。

![configure-transcription-service](assets/video-processing-profile1.png)

一旦處理設定檔設定為音訊和視訊檔案的轉譯後，您就可以使用下列其中一種方法，將此處理設定檔套用至資料夾：

* 在中選取處理設定檔定義 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**，並使用 **[!UICONTROL 將設定檔套用至資料夾]** 動作。 內容瀏覽器可讓您導覽至特定資料夾、選取資料夾並確認設定檔的應用。
* 在Assets使用者介面中選取資料夾，然後按一下 **[!UICONTROL 屬性]** 開啟資料夾屬性的動作。 按一下 **[!UICONTROL 資產處理]** 標籤，然後為資料夾選取適當的處理設定檔 **[!UICONTROL 處理設定檔]** 清單。 若要儲存變更，請按一下 **[!UICONTROL 儲存並關閉]**.

  ![configure-transcription-service](assets/video-processing-profile3.png)

* 使用者可以在Assets使用者介面中選取資料夾或特定資產，以套用處理設定檔，然後選取 **[!UICONTROL 重新處理資產]** 從上方可用的選項中選取。

>[!TIP]
>一個資料夾只能套用一個處理設定檔。
>
>在處理設定檔套用至資料夾後，系統會使用設定的其他處理設定檔來處理此資料夾或其任何子資料夾中上傳（或更新）的所有新資產。 此處理是在標準預設設定檔之外進行的。

>[!NOTE]
>
>套用至資料夾的處理設定檔適用於整個樹狀結構，但可以套用至子資料夾的其他設定檔加以覆寫。
>
>將資產上傳至資料夾時，Experience Manager會與容納資料夾的屬性通訊，以識別處理設定檔。 如果未套用任何設定檔，則會檢查階層中的父資料夾以套用處理設定檔。


## 產生音訊或視訊資產的轉錄 {#generate-transcription}

處理視訊資產時， [AI型處理設定檔](#configure-processing-profile-for-transcription) 系統會自動產生轉譯成的成績單（.vtt檔案），連同相同資料夾中的原始資產。

![configure-transcription-service](assets/transcript1.png)

您也可以存取原始視訊資產的轉譯，以檢視轉錄轉譯。 若要存取 **[!UICONTROL 轉譯]** 面板，選取原始視訊資產並開啟左側邊欄。 您可以看到轉錄轉譯（.vtt檔案）顯示在 **[!UICONTROL TRANSCRIPTVTT]** head.

![configure-transcription-service](assets/transcript.png)

您可以直接從資料夾中下載成績單（.vtt文字檔）作為單獨的資產轉譯，或從 **[!UICONTROL 轉譯]** 原始資產的面板，可下載資產的所有轉譯。

目前，Experience Manager不支援以原生方式預覽或編輯VTT檔案的全文。 不過，您可以下載轉錄轉譯，並使用任何文字編輯器來編輯或驗證轉錄檔案。 轉錄本會以指定時間戳記反映口語作為視訊中的文字，並搭配轉錄的信賴度分數（準確性）。

![configure-transcription-service](assets/transcript-text.png)

## 在Dynamic Media中使用轉錄 {#using-transcription-in-dynamic-media}

如果您有 [已設定的Dynamic Media](/help/assets/dynamic-media/config-dm.md) 在您的Experience Manager Assets執行個體中，您可以將資產（音訊或視訊檔案）及其轉錄檔（.vtt檔案）發佈到Dynamic Media。 如此一來，原始資產（音訊或視訊檔案）及其轉譯檔案（.vtt檔案）會發佈至相同資料夾中的Dynamic Media。 Dynamic Media管理員可以 [啟用CC隱藏式字幕體驗](/help/assets/dynamic-media/video.md#adding-captions-to-video) 音訊或視訊檔案使用轉錄轉譯（.vtt檔案）。

另請參閱:

* [有關如何將CC隱藏式字幕新增到Dynamic Media影片中的影片教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html#add-cc-closed-captioning-to-dynamic-media-video)
* [將Dynamic Media影片發佈至YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

在下圖中，URL反映了參考轉錄檔案（.vtt檔案）的註解部分。 影片將口語（轉錄文字）反映為 **[!UICONTROL 隱藏式字幕]** 在視訊中的指定時間戳記。 使用者可以使用 **[!UICONTROL CC]** 按鈕。

![configure-transcription-service](assets/transcript-example.png)

## 支援的轉錄檔案格式 {#supported-file-format}

轉錄支援下列音訊和視訊檔案格式：

| 支援的音訊/視訊格式 | 擴充功能 |
|----|----|
| FLV （含H.264和AAC轉碼器） | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS、MPEG2-TS、3GP | (.ts， .ps， .3gp， .3gpp， .mpg) |
| Windows Media Video (WMV)/ASF | (.wmv， .asf) |
| AVI （未壓縮8位元/10位元） | (.avi) |
| MP4 | (.mp4， .m4a， .m4v) |
| Microsoft®數位視訊錄製(DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| Quicktime | (.mov) |


>[!NOTE]
>
>應用程式型別的資產（音訊或視訊檔案）不支援轉錄。

## 已知限制 {#known-limitations}

* 轉錄功能支援長達10分鐘的影片。
* 視訊標題長度必須少於80個字元。
* 支援的檔案大小最多為15 GB。
* 支援的最大處理持續時間為60分鐘。
* 在付費中 [!DNL Azure] 帳戶，您每分鐘最多可上傳50部電影。 不過，在試用帳戶中，您每分鐘最多可以上傳5部電影。

## 疑難排解提示 {#troubleshooting}

登入您的 [!DNL Azure Media Services] 具有相同認證（您用於設定）的帳戶，用於驗證請求狀態。 連絡人 [!DNL Azure] 支援未成功處理您的請求。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
