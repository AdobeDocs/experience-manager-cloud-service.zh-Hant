---
title: 設定轉錄服務
description: Adobe Experience Manager Assets已設定 [!DNL Azure Media Services] ，它會自動產生WebVTT (Vtt)格式之支援音訊或視訊檔案中的口語文字轉錄。
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
exl-id: e96c8d68-74a6-4d61-82dc-20e619338d4b
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 2%

---

# 在[!DNL Experience Manager Assets]中設定轉錄 {#configure-transcription-service}

轉錄是使用語音辨識技術，將音訊或視訊檔案中的音訊轉換為文字（語音轉換為文字）的過程。
[!DNL Adobe Experience Manager Assets]已設定[!DNL Azure Media Services]，它會自動產生WebVTT (.vtt)格式之支援音訊或視訊檔案中的口語文字轉錄。 在[!DNL Experience Manager Assets]中處理音訊或視訊資產時，轉譯服務會自動產生音訊或視訊資產的文字轉譯，並將其儲存在原始資產所在的Assets存放庫中的相同位置。 [!DNL Experience Manager Assets]轉錄服務可讓行銷人員透過新增的文字內容可發現性來有效管理其音訊與視訊內容，並透過支援協助工具與本地化來提高這些資產的ROI。

轉錄是口語內容的文字版本；例如，您在任何OTT平台上觀看的電影通常都包含字幕，以協助協助協助協助存取或使用其他語言的內容。 或任何用於行銷、學習或娛樂目的的音訊或視訊檔案。 這些體驗從轉錄開始，然後視需要將其格式化或翻譯。 當手動執行時，轉錄音訊或視訊是一項耗時且容易出錯的程式。 鑑於對音訊/視訊內容的需求不斷增加，擴展手動程式也是一個挑戰。 [!DNL Experience Manager Assets]使用Azure的AI型轉錄，允許音訊和視訊資產進行大規模處理，並產生文字轉錄（.vtt檔案）以及時間戳記詳細資料。 除了Assets，Dynamic Media也支援轉錄功能。

在[!DNL Experience Manager Assets]中可以免費使用轉譯功能。 但是，系統管理員需要使用者的Azure認證，才能在[!DNL Experience Manager Assets]中設定轉寫服務。 您也可以[直接從Microsoft®取得試用認證](https://azure.microsoft.com/en-us/pricing/details/media-services/)，體驗Assets的音訊或視訊轉寫功能。

## 轉錄先決條件 {#prerequisites}

1. 正在執行中的[!DNL Experience Manager Assets as a Cloud Service]執行個體。
1. 在[!DNL Experience Manager Assets]中設定需要下列Azure認證：

   * 使用者端ID （API金鑰）
   * 使用者端秘密金鑰
   * 租使用者端點（網域）
   * 媒體帳戶
   * 資源群組
   * 訂閱 ID

   請參閱[Azure檔案](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal)，以取得存取Azure Media Services API的認證。

1. 請確定Azure帳戶有足夠的信用額度來處理新請求。

## 在[!DNL Experience Manager Assets]中設定轉錄 {#configure-transcription}

以下是在[!DNL Experience Manager Assets]中啟用轉錄功能所需的設定：

1. [設定Azure媒體服務](#configure-azure-media-service)
1. [設定音訊/視訊轉譯的處理設定檔](#configure-processing-profile-for-transcription)


### 設定Azure媒體服務 {#configure-azure-media-services}

[!DNL Experience Manager Assets]使用[!DNL Azure Media Services]，自動產生WebVTT (.vtt)格式之[支援音訊或視訊檔](#supported-file-formats-for-transcription)的口語文字轉錄。 管理員可以使用Azure認證設定[!DNL Experience Manager Assets]中的[!DNL Azure Media Services]。 [轉譯先決條件](#transcription-prerequisites)列出組態所需的[!DNL Azure]認證。 如果您沒有[!DNL Azure]帳戶和認證，請參閱[Azure Media Services檔案](https://azure.microsoft.com/en-us/pricing/details/media-services/)以取得試用認證。

![configure-transcription-service](assets/configure-transcription-service.png)

移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Azure媒體服務設定]**。 從左側邊欄選取資料夾（位置），然後按一下「[!UICONTROL 建立]」按鈕，以設定與您的[!DNL Azure]帳戶的連線。 此資料夾是您的[!DNL Azure]雲端設定儲存在Experience Manager Assets中的位置。 輸入[!DNL Azure]認證，然後按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

### 設定轉譯的處理設定檔 {#configure-processing-profile}

在Experience Manager Assets中設定[!DNL Azure Media Services]後，下一步就是建立資產處理設定檔，用於產生音訊和視訊資產的AI型轉錄。 AI型處理設定檔會產生[支援的音訊或視訊資產](#supported-file-formats-for-transcription)的轉譯成Experience Manager Assets中的轉譯，並將轉譯檔案（.vtt檔案）儲存在原始資產所在的相同資料夾中。 因此，使用者更容易搜尋及找到資產及其轉譯檔案。

移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]**，然後按一下&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕，建立以AI為基礎的處理設定檔，以產生音訊和視訊檔案的轉錄。 依預設，處理設定檔頁面只會反映三個索引標籤（影像、視訊和自訂）。 不過，如果您已在[!DNL Experience Manager Assets]執行個體中設定[!DNL Azure Media Services]，則會顯示&#x200B;**[!UICONTROL Content AI]**&#x200B;索引標籤。 如果您在建立處理設定檔時沒有看到&#x200B;**[!UICONTROL Content AI]**&#x200B;標籤，請驗證您的[!DNL Azure]認證。

在&#x200B;**[!UICONTROL Content AI]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕以設定轉錄。 在這裡，您可以從下拉式清單中選取檔案型別，來包含和排除用於產生轉譯的檔案格式（MIME型別）。 在下圖中，包含所有支援的音訊和視訊檔案，並排除文字檔案。

啟用&#x200B;**[!UICONTROL 在相同目錄中建立VTT轉錄]**&#x200B;切換功能，在原始資產所在的相同資料夾中建立並儲存轉錄轉譯（.vtt檔案）。 無論此設定為何，預設DAM資產處理工作流程也會產生其他轉譯。

![configure-transcription-service](assets/configure-transcription-profile.png)

下圖詳細說明在Experience Manager Assets中建立的自訂視訊設定檔。

![configure-transcription-service](assets/video-processing-profile.png)

視訊設定檔也包含下列自訂設定。 如需有關如何建立自訂處理設定檔的詳細資訊，請參閱[處理設定檔檔案](/help/assets/asset-microservices-configure-and-use.md)。

![configure-transcription-service](assets/video-processing-profile2.png)

現在，讓我們在此視訊設定檔中設定轉錄。 導覽至&#x200B;**[!UICONTROL Content AI]**&#x200B;標籤，然後按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕。 包含所有音訊和視訊檔案，並排除影像和應用程式檔案。 啟用&#x200B;**[!UICONTROL 在相同目錄]**&#x200B;中建立VTT文字記錄並儲存組態。

![configure-transcription-service](assets/video-processing-profile1.png)

將處理設定檔設定為音訊和視訊檔案的轉譯後，您可以使用以下方法之一將此處理設定檔套用至資料夾：

* 在&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]**&#x200B;中選取處理設定檔定義，並使用&#x200B;**[!UICONTROL 將設定檔套用至資料夾]**&#x200B;動作。 內容瀏覽器可讓您導覽至特定資料夾、選取資料夾並確認設定檔的應用程式。
* 在Assets使用者介面中選取資料夾，然後按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;動作以開啟資料夾屬性。 按一下&#x200B;**[!UICONTROL 資產處理]**&#x200B;標籤，然後從&#x200B;**[!UICONTROL 處理設定檔]**&#x200B;清單中為資料夾選取適當的處理設定檔。 若要儲存變更，請按一下[儲存並關閉]。**&#x200B;**

  ![configure-transcription-service](assets/video-processing-profile3.png)

* 使用者可以在Assets使用者介面中選取資料夾或特定資產，以套用處理設定檔，然後從上方可用的選項中選取&#x200B;**[!UICONTROL 重新處理Assets]**&#x200B;選項。

>[!TIP]
>一個資料夾只能套用一個處理設定檔。
>
>在處理設定檔套用至資料夾後，此資料夾或其任何子資料夾中上傳（或更新）的所有新資產都會使用設定的其他處理設定檔來處理。 此處理是標準預設設定檔的補充。

>[!NOTE]
>
>套用至資料夾的處理設定檔適用於整個樹狀結構，但可以套用至子資料夾的其他設定檔加以覆寫。
>
>將資產上傳至資料夾時，Experience Manager會與容納資料夾的屬性通訊，以識別處理設定檔。 如果未套用任何設定檔，則會檢查階層中的父資料夾以找出要套用的處理設定檔。


## 產生音訊或視訊資產的轉錄 {#generate-transcription}

處理視訊資產時，[AI型處理設定檔](#configure-processing-profile-for-transcription)會自動產生轉譯（.vtt檔案），連同相同資料夾中的原始資產。

![configure-transcription-service](assets/transcript1.png)

您也可以透過存取原始視訊資產的轉譯來檢視轉譯稿。 若要存取&#x200B;**[!UICONTROL 轉譯]**&#x200B;面板，請選取原始視訊資產並開啟左側邊欄。 您可以看到轉錄轉譯（.vtt檔案）顯示在&#x200B;**[!UICONTROL TRANSCRIPTVTT]**&#x200B;標題下。

![configure-transcription-service](assets/transcript.png)

您可以直接從資料夾中下載轉錄（.vtt文字檔）做為獨立的資產轉譯，或是從原始資產的&#x200B;**[!UICONTROL 轉譯]**&#x200B;面板中下載資產的所有轉譯。

目前，Experience Manager不支援以原生方式預覽或編輯VTT檔案。 不過，您可以下載成績單轉譯，並使用任何文字編輯器來編輯或驗證成績單。 轉錄檔案反映了視訊中指定時間戳記處的口語文字，以及轉錄的信賴度分數（準確性）。

![configure-transcription-service](assets/transcript-text.png)

## 在Dynamic Media中使用轉錄 {#using-transcription-in-dynamic-media}

如果您已在Experience Manager Assets執行個體中設定[Dynamic Media](/help/assets/dynamic-media/config-dm.md)，您可以將資產（音訊或視訊檔案）及其轉錄（.vtt檔案）發佈至Dynamic Media。 如此一來，原始資產（音訊或視訊檔案）及其轉譯的轉譯（.vtt檔案）會發佈至相同資料夾中的Dynamic Media。 Dynamic Media管理員可以使用轉譯檔案（.vtt檔案）為音訊或視訊檔案[啟用CC隱藏式字幕體驗](/help/assets/dynamic-media/video.md#adding-captions-to-video)。

另請參閱：

* [有關如何將CC隱藏式字幕新增至Dynamic Media視訊的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=zh-Hant#add-cc-closed-captioning-to-dynamic-media-video)
* [將Dynamic Media影片發佈至YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

在下圖中，URL會反映參照文字稿（.vtt檔案）的註解部分。 視訊會在視訊中的指定時間戳記，將口語（轉錄文字）反映為&#x200B;**[!UICONTROL 隱藏式字幕]**。 使用者可以使用&#x200B;**[!UICONTROL CC]**&#x200B;按鈕來啟用或停用註解。

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
* 視訊標題不得超過80個字元。
* 支援的檔案大小最高為15 GB。
* 支援的最大處理時間為60分鐘。
* 在付費[!DNL Azure]帳戶中，您每分鐘最多可以上傳50部電影。 不過，在試用帳戶中，您每分鐘最多可以上傳5部電影。

## 疑難排解提示 {#troubleshooting}

以相同的認證（您用於組態）登入您的[!DNL Azure Media Services]帳戶以驗證要求狀態。 如果您的要求未成功處理，請連絡[!DNL Azure]支援。

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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
