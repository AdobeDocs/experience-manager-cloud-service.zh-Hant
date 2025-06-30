---
title: 管理影片資產
description: 在 [!DNL Adobe Experience Manager]中上傳、預覽、註釋及發佈視訊資產。
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '4983'
ht-degree: 6%

---

# 管理影片資產 {#manage-video-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

視訊格式是組織數位資產的重要一環。 [!DNL Adobe Experience Manager]提供成熟的產品和功能，可在建立視訊資產後管理其整個生命週期。

瞭解如何在[!DNL Adobe Experience Manager Assets]中管理和編輯視訊資產。 可以使用「處理設定檔」和[!DNL Dynamic Media]整合來進行視訊編碼和轉碼（例如FFmpeg轉碼）。 如果沒有[!DNL Dynamic Media]授權，[!DNL Experience Manager]會提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援檔案格式的預覽縮圖，以及在使用者介面中直接在瀏覽器中支援播放的格式進行預覽。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

您可以將支援格式的視訊資產上傳並預覽至[!DNL Experience Manager Assets]。
<!-- It generates previews for video assets with the extension MP4. -->

### 上傳視訊資產

若要上傳視訊資產，請遵循下列步驟：

1. 在數位資產資料夾或子資料夾中，導覽至您需要新增資產的位置。
1. 按一下工具列中的[建立]，然後選擇[檔案]。****。 ****<br>或者，在使用者介面上拖曳檔案。
深入瞭解[!DNL Experience Manager Assets]中的[上傳資產](manage-digital-assets.md#uploading-assets)。

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### 預覽視訊資產

您可以在[!DNL Assets]使用者介面中預覽支援的轉譯影片。 若要預覽視訊資產，請執行下列步驟：

1. 將支援格式的視訊資產上傳至[!DNL Experience Manager Assets]。 深入瞭解[支援的視訊格式](file-format-support.md#video-formats)。 <br>上傳後，系統會處理視訊資產，並產生預覽轉譯。
1. 按一下資產，然後從頂端工具列選取![詳細資訊選項](assets/do-not-localize/details_icon.svg) **[!UICONTROL 詳細資訊]**。 視訊資產會在視訊檢視器中開啟。
1. 按一下視訊縮圖上的![播放選項](assets/do-not-localize/play.png)圖示。 <br>您可以播放、暫停、控制音量，以及將視訊縮放成全熒幕。

針對[!DNL Experience Manager Assets]中的現有視訊資產，您需要&#x200B;**[!UICONTROL 重新處理[!DNL Experience Manager]中的資產]**&#x200B;以啟用視訊預覽功能。 瞭解如何在[!DNL Experience Manager]中[重新處理數位資產](reprocessing.md)。

### 視訊預覽的限制

* 即使產生轉譯，MXF檔案也不會顯示視訊預覽。
* WebM檔案不會產生預覽轉譯，因為這些轉譯可由網頁瀏覽器以原生方式播放。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL形式納入網頁中，或直接內嵌資產。 如需詳細資訊，請參閱[發佈 [!DNL Dynamic Media] 資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將視訊發佈至YouTube {#publishing-videos-to-youtube}

您可以將Experience Manager Assets中管理的視訊資產直接發佈至您先前建立的YouTube頻道。

若要將視訊資產發佈至YouTube，請在Experience Manager Assets中使用標籤來標籤視訊資產。 您可以將這些標籤與YouTube頻道建立關聯。 如果視訊資產的標籤符合YouTube頻道的標籤，則視訊會發佈至YouTube。 只要使用關聯的標籤，發佈至YouTube就會與視訊的正常發佈同時發生。

YouTube會自行編碼。 因此，上傳至Experience Manager的原始視訊檔案會發佈至YouTube，而不會發佈至Dynamic Media編碼所建立的任何視訊轉譯。 雖然視訊不需要使用Dynamic Media來處理，但如果播放需要檢視器預設集，預計會予以處理。

當您略過視訊處理設定檔並直接發佈至YouTube時，這僅代表您在Experience Manager資產中的視訊資產沒有取得可檢視的縮圖。 這也表示未編碼的視訊不適用於任何Dynamic Media資產型別。

將視訊資產發佈至YouTube伺服器需要完成下列工作，以確保透過YouTube進行安全無虞的伺服器對伺服器驗證：

1. [配置Google雲端設定](#configuring-google-cloud-settings)
1. [建立YouTube管道](#creating-a-youtube-channel)
1. [新增標籤以供發佈](#adding-tags-for-publishing)
1. [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)
1. [（可選）為您上傳的視訊自動設定預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將影片發佈至您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（選用）驗證YouTube上的已發佈影片](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTube URL連結至您的網頁應用程式](#linking-youtube-urls-to-your-web-application)

您也可以[取消發佈視訊，以從YouTube](#unpublishing-videos-to-remove-them-from-youtube)中移除這些視訊。

### 配置Google雲端設定 {#configuring-google-cloud-settings}

若要發佈至YouTube，您需要Google帳戶。 如果您有GMAIL帳戶，表示您已經擁有Google帳戶；如果您沒有Google帳戶，可以輕鬆建立帳戶。 您需要帳戶，因為您需要憑證才能將視訊資產發佈到YouTube。<!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Google Cloud所用的帳戶與YouTube所用的Google帳戶不必相同。

Google會定期變更其使用者介面。 因此，將視訊發佈至YouTube的步驟可能會與以下說明略有不同。 此警告也適用於您嘗試檢查是否將視訊上傳到YouTube的。

>[!NOTE]
>
>在撰寫時，下列步驟是準確的。 不過，Google會定期更新其雲端網頁，恕不另行通知。 因此，某些設定選項在Google使用者介面中的名稱可能與步驟中使用的名稱略有不同。

**若要設定Google雲端設定：**

1. 建立Google帳戶。

   如果您已有Google帳戶，可跳至下一個步驟。

1. 移至[https://cloud.google.com/](https://cloud.google.com/)。
1. 在&#x200B;**[!UICONTROL Google Cloud]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 主控台]**。

   如有必要，請使用您的Google帳戶認證&#x200B;**[!UICONTROL 登入]**&#x200B;以檢視&#x200B;**[!UICONTROL 主控台]**&#x200B;選項。

1. 在&#x200B;**[!UICONTROL 儀表板]**&#x200B;頁面的&#x200B;**[!UICONTROL Google Cloud Platform]**&#x200B;右側，選取&#x200B;**[!UICONTROL 專案]**&#x200B;下拉式清單以開啟&#x200B;**[!UICONTROL 選取專案]**&#x200B;對話方塊。
1. 在&#x200B;**[!UICONTROL 選取專案]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 新增專案]**。
1. 在&#x200B;**[!UICONTROL 新專案]**&#x200B;對話方塊的&#x200B;**[!UICONTROL 專案名稱]**&#x200B;欄位中，輸入新專案的名稱。

   您的專案ID是以專案名稱為基礎。 因此，請謹慎選擇專案名稱；專案建立後即無法變更。 此外，您稍後在Experience Manager中設定YouTube時，必須再次輸入相同的專案ID。 因此，請寫下來。

1. 選取「**[!UICONTROL 建立]**」。

1. 執行下列其中一項：

   * 在您的專案的[儀表板]上，在&#x200B;**[!UICONTROL 開始使用]**&#x200B;卡片中，選取&#x200B;**[!UICONTROL 探索並啟用API]**。
   * 在您的專案的[儀表板]上，在&#x200B;**[!UICONTROL API]**&#x200B;卡片中，選取&#x200B;**[!UICONTROL 移至API總覽]**。

1. 在&#x200B;**[!UICONTROL API與服務]**&#x200B;頁面的頂端中間附近，選取&#x200B;**[!UICONTROL 啟用API與服務]**。<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在&#x200B;**[!UICONTROL API資料庫]**&#x200B;頁面的左側，**[!UICONTROL 類別]**&#x200B;底下，選取&#x200B;**[!UICONTROL YouTube]**。 在頁面右側，選取&#x200B;**[!UICONTROL YouTube]**。
1. 在&#x200B;**[!UICONTROL YouTube]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL YouTube Data API v3]**。
1. 在&#x200B;**[!UICONTROL YouTube Data API v3]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 管理]**。

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 若要使用API，您需要憑證。 如有必要，請在&#x200B;**[!UICONTROL API與服務]**&#x200B;頁面的左側，選取&#x200B;**[!UICONTROL 認證]**。
1. 在&#x200B;**[!UICONTROL 認證]**&#x200B;頁面的頂端附近，選取&#x200B;**[!UICONTROL 建立認證]**，然後選取&#x200B;**[!UICONTROL OAuth使用者端識別碼]**。
1. 在&#x200B;**[!UICONTROL 建立OAuth使用者端識別碼]**&#x200B;頁面的&#x200B;**[!UICONTROL 應用程式型別]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 網頁應用程式]**。

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 執行下列任一項作業：

   * 在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中，輸入您OAuth 2.0使用者端的唯一名稱。
   * 使用Google已在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中提供的預設名稱。

1. 在&#x200B;**[!UICONTROL 已授權的JavaScript來源]**&#x200B;標題下，選取&#x200B;**[!UICONTROL 新增URI]**。

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在&#x200B;**[!UICONTROL URI]**&#x200B;文字欄位中，輸入下列路徑，在路徑中取代您自己的網域和連線埠號碼，然後按&#x200B;**[!UICONTROL Enter]**&#x200B;將路徑新增至清單：

   `https://<servername.domain>:<port_number>`

   例如 `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上述URI路徑範例是假設性的，僅供說明之用。

1. 在&#x200B;**[!UICONTROL 授權的重新導向URI]**&#x200B;標題下，選取[新增URI]。
1. 在&#x200B;**[!UICONTROL URI]**&#x200B;文字欄位中，輸入下列路徑，在路徑中取代您自己的網域和連線埠號碼，然後按&#x200B;**[!UICONTROL Enter]**&#x200B;將路徑新增至清單：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如 `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上述URI路徑範例是假設性的，僅供說明之用。

1. 在&#x200B;**[!UICONTROL 建立OAuth使用者端識別碼]**&#x200B;頁面的底部附近，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL OAuth使用者端已建立]**&#x200B;對話方塊上，執行下列動作：

   * （選擇性）複製&#x200B;**[!UICONTROL 您的使用者端識別碼]**&#x200B;和&#x200B;**[!UICONTROL 您的使用者端密碼]**&#x200B;欄位中的值，並儲存。
   * 選取「**[!UICONTROL 下載JSON]**」，然後儲存JSON檔案。

   您稍後在Adobe Experience Manager中設定YouTube時，需要此下載的JSON檔案。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在&#x200B;**[!UICONTROL OAuth使用者端已建立]**&#x200B;對話方塊上，選取&#x200B;**[!UICONTROL 確定]**。
1. 登出您的Google帳戶。 現在建立YouTube管道。

### 建立YouTube管道 {#creating-a-youtube-channel}

若要將影片發佈至YouTube，您必須具備一或多個管道。 如果您已建立YouTube管道，則可以略過此工作，並移至[新增標籤以進行發佈](/help/assets/dynamic-media/video.md#adding-tags-for-publishing)。

>[!CAUTION]
>
>請確定您已在YouTube *中設定一或多個管道*&#x200B;之前，在Experience Manager的YouTube設定下新增管道(請參閱下方的[在Experience Manager中設定YouTube](#setting-up-youtube-in-aem))。 如果您無法設定頻道，則不會警告您沒有現有頻道。 不過，當您新增頻道時，Google驗證仍會發生，但無法選擇傳送視訊的頻道。

**若要建立YouTube頻道：**

1. 移至[https://www.youtube.com](https://www.youtube.com/)並使用您的Google帳戶認證登入。
1. 在YouTube頁面的右上角，選取您的個人資料圖片（也可以顯示為實色圓圈中的字母），然後選取&#x200B;**[!UICONTROL YouTube設定]** （圓形齒輪圖示）。
1. 在「概觀」頁面的「其他功能」標題下，選取「**[!UICONTROL 檢視我的所有管道」或建立管道]**。
1. 在[頻道]頁面上，選取&#x200B;**[!UICONTROL 建立新頻道]**。
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入您要發佈視訊資產的公司名稱或任何其他管道名稱，然後選取「**[!UICONTROL 建立]**」。

   請記住您在這裡輸入的名稱；當您必須在Experience Manager中設定YouTube時，必須再次輸入。

1. （選用）如有需要，請新增更多管道。

   現在新增標籤以進行發佈。

### 新增標籤以供發佈 {#adding-tags-for-publishing}

若要將影片發佈至YouTube，Experience Manager會將標籤與一個或多個YouTube管道建立關聯。 若要新增標籤以進行發佈，請參閱[管理標籤](/help/sites-cloud/authoring/sites-console/tags.md)。

或者，如果您想要在Experience Manager中使用預設標籤，您可以略過此工作，並移至[在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)。

>[!NOTE]
>
>設定Cloud Service後，此時啟用YouTube發佈復寫代理程式不需要其他設定。 原因是因為它在Cloud Service設定儲存時啟用。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中設定YouTube {#setting-up-youtube-in-aem}

從Experience Manager 6.4開始，引進了全新的觸控使用者介面方法，以在Experience Manager中設定YouTube發佈。 根據您所使用的Experience Manager安裝例項，執行下列任一項作業：

* 若要在6.4之前的Experience Manager中設定YouTube，請參閱[在6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before)之前的Experience Manager中設定YouTube 。
* 若要在Experience Manager 6.4或更新版本中設定YouTube，請參閱[在Experience Manager 6.4及更新版本中設定YouTube](#setting-up-youtube-in-aem-and-later)。

#### 在Experience Manager 6.4和更新版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側導軌中，導覽至&#x200B;**[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 雲端服務]** > **[!UICONTROL YouTube Publishing Configuration]**。
1. 選取&#x200B;**[!UICONTROL 全域]** （不要選取它）。

1. 在全域頁面的右上角附近，選取&#x200B;**[!UICONTROL 建立]**。
1. 在「建立YouTube設定」頁面的「Google cloud 平台設定」下方的「應用程式名稱」欄位 **[!UICONTROL 中]** ，輸入Google專案ID。

   您已在先前設定Google Cloud設定時指定專案ID。
讓「建立YouTube設定」頁面保持開啟；您稍後就會返回。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字編輯器，開啟您先前在[設定Google雲端設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**。

   現在請在Experience Manager中設定YouTube管道。

1. 選取&#x200B;**[!UICONTROL 新增頻道]**。
1. 在「頻道名稱」欄位中，輸入您在&#x200B;**[!UICONTROL 先前新增一或多個頻道至YouTube]**&#x200B;工作中建立的頻道名稱。

   如有需要，您可以選擇新增說明。

1. 選取「**[!UICONTROL 新增]**」。
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID及上述JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少個管道會顯示兩個或更多專案而定。 選取管道。 請勿選取電子郵件地址；此地址不是管道。
   * 在下一頁，選取&#x200B;**[!UICONTROL 接受]**&#x200B;以允許存取此頻道。

1. 選取&#x200B;**[!UICONTROL 允許]**。

   現在設定標籤以供發佈。

1. **[!UICONTROL 設定標籤以進行發佈]** — 在Cloud Services > YouTube頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要顯示Experience Manager中可用標籤的清單，請選取下拉式清單圖示（上下顛倒的插入號）。
1. 若要新增這些標籤，請選取一或多個標籤。

   若要刪除您已新增的標籤，請選取標籤，然後選取&#x200B;**[!UICONTROL X]**。

1. 完成新增您想要的標籤後，請選取&#x200B;**[!UICONTROL 儲存]**。

   現在您可將視訊發佈至YouTube頻道。

#### 在6.4之前的Experience Manager中設定YouTube {#setting-up-youtube-in-aem-before}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側導軌中，導覽至&#x200B;**[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**。
1. 在「協力廠商服務」標題的「YouTube」下方，選取&#x200B;**[!UICONTROL 立即設定]**。
1. 在「建立組態」對話方塊的個別欄位中，輸入標題（必要）和名稱（選用）。
1. 選取「**[!UICONTROL 建立]**」。
1. 在「YouTube帳戶設定」對話方塊的「應用程式名 **[!UICONTROL 稱」欄位中]** ，輸入Google專案ID。

   您已在最初[設定Google雲端設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)時指定專案ID。
讓YouTube帳戶設定對話方塊保持開啟；您稍後就會回到對話方塊。

1. 使用純文字編輯器，開啟您先前在「設定Google雲端設定」工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 選取&#x200B;**[!UICONTROL 確定]**。

   現在請在Experience Manager中設定YouTube管道。

1. 在&#x200B;**[!UICONTROL 可用頻道]**&#x200B;的右側，選取&#x200B;**+** （加號圖示）。
1. 在「YouTube頻道設定」對話方塊的「標題」欄位中，輸入您在「先前新增一或多個頻道至YouTube」工作中建立的頻道名稱 **** 。

   如有需要，您可以選擇新增說明。

1. 選取&#x200B;**[!UICONTROL 確定]**。
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID及上述JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少個管道會顯示兩個或更多專案而定。 選取管道。 請勿選取電子郵件地址；此地址不是管道。
   * 在下一頁，選取&#x200B;**[!UICONTROL 接受]**&#x200B;以允許存取此頻道。

1. 選取&#x200B;**[!UICONTROL 允許]**。

   現在設定標籤以供發佈。

1. **[!UICONTROL 設定標籤以進行發佈]** — 在Cloud Services > YouTube頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要顯示Experience Manager中可用標籤的清單，請選取下拉式清單圖示（上下顛倒的插入號）。
1. 若要新增這些標籤，請選取一或多個標籤。

   若要刪除您已新增的標籤，請選取標籤，然後選取&#x200B;**X**。

1. 完成新增您想要的標籤後，請選取&#x200B;**[!UICONTROL 確定]**。

   現在您可將視訊發佈至YouTube頻道。

### （可選）為您上傳的視訊自動設定預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以選擇在上傳視訊時自動設定YouTube屬性。 在Experience Manager中建立中繼資料處理設定檔。

若要建立中繼資料處理設定檔，您必須先從「欄位標籤 **[!UICONTROL 」、「對應至屬性]********** 」和「選擇」欄位複製值，這些全都可在視訊的中繼資料結構中找到。然後，您可以新增這些值，以建立您的YouTube視訊中繼資料處理設定檔。

**若要針對您上傳的視訊自動設定預設YouTube屬性：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側導軌中，導覽至&#x200B;**[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
1. 選取&#x200B;**[!UICONTROL 預設]**。 （請勿在「預設」左側的選取方塊中新增核取記號。）
1. 在&#x200B;**[!UICONTROL 預設]**&#x200B;頁面上，勾選&#x200B;**[!UICONTROL 影片]**&#x200B;左側的方塊，然後選取&#x200B;**[!UICONTROL 編輯]**。
1. 在「中繼資料結構編輯器」頁面上，選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 在「YouTube發佈」標題下，選取&#x200B;**[!UICONTROL YouTube類別]**。
1. 在頁面右側的&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下方，執行下列動作：

   * 在&#x200B;**[!UICONTROL 對應至屬性]**文字欄位中，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 當您稍後建立中繼資料處理設定檔時，會需要此值。 讓文字編輯器保持開啟狀態。

   * 在&#x200B;**[!UICONTROL 選擇]**下，選取並複製您要使用的預設值（例如「人員與部落格」或「科學與技術」）。
將複製的值貼到開啟的文字編輯器中。 當您稍後建立中繼資料處理設定檔時，會需要此值。 讓文字編輯器保持開啟狀態。

1. 在「YouTube發佈」標題下，選取&#x200B;**[!UICONTROL YouTube隱私權]**。
1. 在頁面右側的&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下方，執行下列動作：

   * 在&#x200B;**[!UICONTROL 對應至屬性]**文字欄位中，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 當您稍後建立中繼資料處理設定檔時，會需要此值。 讓文字編輯器保持開啟狀態。

   * 在&#x200B;**[!UICONTROL 選擇]**下，選取並複製您要使用的預設值。 請注意，「選擇」會組成兩個選項組。 配對中的底部欄位是您要複製的預設值，例如public、unlisted或private。
將複製的值貼到開啟的文字編輯器中。 當您稍後建立中繼資料處理設定檔時，會需要此值。 讓文字編輯器保持開啟狀態。

1. 在「中繼資料結構描述編輯器」頁面的右上角附近，選取&#x200B;**[!UICONTROL 取消]**。
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側導軌中，選取&#x200B;**[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**。

1. 在「中繼資料描述檔」頁面的右上角，選取&#x200B;**[!UICONTROL 建立]**。
1. 在「新增中繼資料描述檔」對話方塊的&#x200B;**[!UICONTROL 描述檔標題]**&#x200B;文字欄位中，輸入名稱`YouTube Video`，然後選取&#x200B;**[!UICONTROL 建立]**。
1. 在中繼資料設定檔編輯器頁面上，選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 執行下列操作，將複製的YouTube發佈值新增至設定檔：

   * 在頁面的右側，選取&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤。
   * （可選）將標示為&#x200B;**[!UICONTROL Section Header]**&#x200B;的元件拖曳至左側，並將它拖放到表單區域中。
   * （選擇性）選取&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;以選取元件。
   * （選擇性）在頁面右側的「設定」標籤下方，於「欄位標籤」文字欄位中輸入`YouTube Publishing`。
   * 選取&#x200B;**[!UICONTROL 建置表單]**&#x200B;標籤，然後拖曳標示為&#x200B;**[!UICONTROL 多值文字]**&#x200B;的元件，並將它拖曳至您建立的&#x200B;**[!UICONTROL YouTube發佈]**&#x200B;標題下方。

   * 若要選取元件，請選取&#x200B;**[!UICONTROL 欄位標籤]**。
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（「欄位標籤」值和「對應至屬性值」）貼入表單上各自的欄位中。 將選擇值貼到「預設值」欄位中。

1. 執行下列操作，將複製的YouTube隱私權值新增至設定檔：

   * 在頁面的右側，選取&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤。
   * （可選）將標示為&#x200B;**[!UICONTROL Section Header]**&#x200B;的元件拖曳至左側，並將它拖放到表單區域中。
   * （選擇性）選取&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;以選取元件。
   * （選擇性）在頁面右側的「設定」標籤下方，於「欄位標籤」文字欄位中輸入`YouTube Privacy`。
   * 選取&#x200B;**[!UICONTROL 建置表單]**&#x200B;標籤，然後拖曳標示為&#x200B;**[!UICONTROL 多值文字]**&#x200B;的元件，並將它拖曳至您建立的&#x200B;**[!UICONTROL YouTube隱私權]**&#x200B;標題下方。

   * 若要選取元件，請選取&#x200B;**[!UICONTROL 欄位標籤]**。
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（「欄位標籤」值和「對應至屬性值」）貼入表單上各自的欄位中。 將選擇值貼到「預設值」欄位中。

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**。
1. 將YouTube發佈中繼資料設定檔套用至您要上傳影片的資料夾。 您必須同時設定中繼資料設定檔和視訊設定檔。

   請參[閱中繼資料設定檔](/help/assets/metadata-profiles.md)和[視訊設定檔](/help/assets/dynamic-media/video-profiles.md)。

### 將影片發佈至您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您將先前新增的標籤關聯至視訊資產。 此程式可讓Experience Manager知道要將哪些資產發佈至您的YouTube頻道。

>[!NOTE]
>
>立即發佈不會自動發佈至YouTube。 設定動態媒體時，有兩個發佈選項可供選擇：立 **[!UICONTROL 即或]****[!UICONTROL 啟動後]**。
>
>**[!UICONTROL 立即發佈]**&#x200B;表示上傳的資產（在與IPS同步之後）會自動發佈至傳遞系統。 雖然這對Dynamic Media是如此，對YouTube則否。 若要發佈至YouTube，您必須透過Experience Manager Author發佈。

>[!NOTE]
>
>若要從YouTube發佈內容，Experience Manager會使用&#x200B;**[!UICONTROL 發佈至YouTube]**&#x200B;工作流程，讓您監視進度並檢視任何失敗資訊。
>
>請參閱[監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。
>
>如需詳細進度資訊，您可以在復寫下監視YouTube記錄。 但是，請注意，此類監視需要管理員存取權。

**若要將視訊發佈至您的YouTube頻道：**

1. 在Experience Manager中，導覽至您要發佈至YouTube頻道的視訊資產。
1. 選取視訊資產（最適化視訊集）。
1. 在工具列上，選取&#x200B;**[!UICONTROL 屬性]**。
1. 在「基本」頁簽的「中繼資料」標題下，選取「標籤」欄位右側的&#x200B;**[!UICONTROL 開啟選取範圍對話方塊]**。
1. 在「選取標籤」頁面上，導覽至您要使用的標籤，然後選取一或多個標籤。

   請記住，標籤必須與YouTube管道相關聯。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 選取]**。
1. 在視訊的屬性頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。
1. 在工具列上，選取&#x200B;**[!UICONTROL 快速發佈]**。

   另請參閱[搭配Experience Manager Sites使用出版物管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring)。

   您可以選擇驗證在YouTube頻道上發佈的影片。

### （選用）驗證YouTube上的已發佈影片 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監視YouTube發佈（或取消發佈）的進度。

請參閱[監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。

發佈時間可能會因多項因素而有很大的差異，包括主要來源視訊格式、檔案大小和上傳流量。 發佈程式可能需要幾分鐘到幾小時的時間。 此外，解析度較高的格式呈現得也比較慢。 例如，720p和1080p需要比480p更長的時間。

八小時後，如果您仍然看到顯示&#x200B;**[!UICONTROL 已上傳（正在處理，請稍候）]**&#x200B;的狀態訊息，請嘗試從您的網站移除視訊，然後再次上傳。

### 將YouTube URL連結至您的網頁應用程式 {#linking-youtube-urls-to-your-web-application}

您可以取得Dynamic Media在發佈視訊後產生的YouTube URL字串。 當您複製YouTube URL時，它會貼到剪貼簿，以便您視需要將其貼到網站或應用程式中的頁面。

>[!NOTE]
>
>您必須先將視訊資產發佈至YouTube，才能複製YouTube URL。

若要將YouTube URL連結至您的Web應用程式：

1. 導覽至您要複製其URL的&#x200B;*YouTube已發佈*&#x200B;視訊資產，然後選取該資產。

   請記住，YouTube URL僅可在您首次&#x200B;*發佈*&#x200B;視訊資產至YouTube *後複製*。

1. 在工具列上，選取&#x200B;**[!UICONTROL 屬性]**。
1. 選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 在「YouTube發佈」標題下方的「YouTube URL清單」中，選取URL文字，並將URL文字複製到網頁瀏覽器，以預覽資產或新增至網頁內容頁面。

### 取消發佈影片，以便從YouTube中將其移除 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消發佈視訊資產時，會從YouTube中移除視訊。

>[!CAUTION]
>
>如果您直接從YouTube中移除視訊，Experience Manager不會察覺，並持續以視訊仍發佈至YouTube的方式處理。 一律透過Experience Manager從YouTube取消發佈視訊資產。

>[!NOTE]
>
>若要從YouTube移除內容，Experience Manager會使用&#x200B;**[!UICONTROL 從YouTube取消發佈]**&#x200B;工作流程，讓您監視進度並檢視任何失敗資訊。
>
>請參閱[監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。

**若要取消發佈視訊以從YouTube移除它們：**

1. 導覽至您要從YouTube頻道取消發佈的視訊資產。
1. 在資產選擇模式中，選取一或多個已發佈的視訊資產。
1. 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。 如有必要，請選取工具列上的三個點圖示(`. . .`)以檢視&#x200B;**[!UICONTROL 管理出版物]**。
1. 在[管理出版物]頁面上，選取[**[!UICONTROL 取消發佈]**]。
1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 下一步]**。
1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 取消發佈]**。

## 監視視訊編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

當您將新視訊上傳到已套用視訊編碼的資料夾時，或者您將視訊發佈到YouTube時，請監視您的視訊編碼/Youtube發佈的進度（或失敗）。 您只能透過記錄檔取得實際YouTube發佈進度。 但無論成功與否，都會以下列程式所述的其他方式列出它。 此外，當YouTube發佈工作流程或視訊編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

您可以監視進度，包括失敗的編碼/YouTube發佈。

1. 在您的資產資料夾中檢視視訊編碼進度：

   * 在卡片檢視中，視訊編碼進度會依百分比顯示在資產上。 如果發生錯誤，資產上也會顯示此資訊。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在清單檢視中，視訊編碼進度會顯示在&#x200B;**[!UICONTROL 處理狀態]**&#x200B;欄中。 如果出現錯誤，則該欄會顯示此訊息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   預設不會顯示此欄。若要啟用欄，請從檢視下拉式功能表中選取&#x200B;**[!UICONTROL 檢視設定]**，然後新增&#x200B;**[!UICONTROL 處理狀態]**&#x200B;欄，並選取&#x200B;**[!UICONTROL 更新]**。

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 在資產詳細資料中檢視進度。 當您選取資產時，請開啟下拉式功能表，然後選取&#x200B;**[!UICONTROL 時間軸]**。 若要將其縮小至工作流程活動，例如編碼或YouTube發佈，請選取&#x200B;**[!UICONTROL 工作流程]**。

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   任何工作流程資訊（例如編碼）都會顯示在時間軸中。 就YouTube發佈而言，工作流程時間軸也包含YouTube頻道名稱和YouTube影片URL。 此外，發佈完成後，您會在工作流程時間軸中看到任何失敗通知。

   >[!NOTE]
   >
   >由於來自[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的&#x200B;**[!UICONTROL 重試]**、**[!UICONTROL 重試延遲]**&#x200B;及&#x200B;**[!UICONTROL 逾時]**&#x200B;有多個工作流程設定，因此最終記錄失敗/錯誤訊息可能需要較長時間，例如：
   >
   >* Apache Sling工作佇列設定
   >* Adobe Granite工作流程外部程式工作處理常式
   >* Granite工作流程逾時佇列
   >
   >您可以調整這些組態中的&#x200B;**[!UICONTROL 重試]**、**[!UICONTROL 重試延遲]**&#x200B;和&#x200B;**[!UICONTROL 逾時]**&#x200B;屬性。

1. 如需進行中的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >例項」中的「工作流程例 **[!UICONTROL 項」]******。

   >[!NOTE]
   >
   >您需要管理許可權才能存取&#x200B;**[!UICONTROL 工具]**&#x200B;功能表。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   選取執行個體並選取&#x200B;**[!UICONTROL 開啟歷程記錄]**。

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   您也可以從「工作流程例證」區域暫停、終止或重新命名工作流程。 如需詳細資訊，請參閱[管理工作流程](/help/sites-cloud/authoring/workflows/overview.md)。

1. 有關失敗的作業，請參閱「工具」>「工作流 **[!UICONTROL 程」]** > 「失敗 **[!UICONTROL 」中的「工]** 作流失敗 ****」。「工作 **[!UICONTROL 流失敗]** 」(Workflow Failure)列出所有失敗的工作流活動。

   >[!NOTE]
   >
   >您需要管理許可權才能存取&#x200B;**[!UICONTROL 工具]**&#x200B;功能表。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由於來自[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的&#x200B;**[!UICONTROL 重試]**、**[!UICONTROL 重試延遲]**&#x200B;及&#x200B;**[!UICONTROL 逾時]**&#x200B;有多個工作流程組態，最終記錄錯誤訊息可能需要較長時間，例如：
   >
   >* Apache Sling工作佇列設定
   >* Adobe Granite工作流程外部程式工作處理常式
   >* Granite工作流程逾時佇列
   >
   >您可以調整這些組態中的&#x200B;**[!UICONTROL 重試]**、**[!UICONTROL 重試延遲]**&#x200B;和&#x200B;**[!UICONTROL 逾時]**&#x200B;屬性。

1. 如需完成的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >封存 **[!UICONTROL 」中的「工作流程封存]******」。「工作 **[!UICONTROL 流程存檔]** 」會列出所有已完成的工作流活動。

   >[!NOTE]
   >
   >您需要管理許可權才能存取&#x200B;**[!UICONTROL 工具]**&#x200B;功能表。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您會收到有關已中止或失敗的工作流程作業的電子郵件通知。 這些電子郵件通知可由管理員設定。 請參閱[設定電子郵件通知](#configuring-e-mail-notifications)。

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## 使用處理設定檔進行轉碼 {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service]可讓您使用處理設定檔進行MP4視訊檔案的基本轉碼。 功能不僅可讓您上傳，也可讓您預覽和縮放MP4視訊檔案。

![在[!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)中建立視訊轉碼的處理設定檔

*圖： [!DNL Experience Manager].*&#x200B;中視訊轉碼的處理設定檔

如果您只提供寬度或高度，並將其他欄位保留為空白，則轉譯會維持長寬比。 H.264視訊轉碼器可用於轉碼。

若要使用處理設定檔處理資產，請將設定檔新增至資料夾。 請參閱[使用處理設定檔來處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 為視訊資產加上註釋 {#annotate-video-assets}

您可以將註解新增至視訊資產。 在影片的註解時，播放器會暫停，讓您在影格上註解。 如需詳細資訊，請參閱[管理視訊資產](manage-video-assets.md)。

>[!NOTE]
>
>視訊資產註解尚不支援MXF視訊格式。

1. 從[!DNL Assets]主控台，選取資產卡上的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示資產詳細資訊頁面。
1. 若要播放視訊，請按一下[預覽]。****
1. 若要為視訊加上註解，請按一下&#x200B;**[!UICONTROL 加上註解]**。 註解會新增至視訊中的特定時間（影格）。 在註解時，您可以在畫布上繪圖，並在繪圖中包含註解。 註解會自動儲存。 若要結束註解精靈，請按一下&#x200B;**[!UICONTROL 關閉]**。
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 若要在時間軸中檢視註釋，請按一下註釋。 若要從時間表刪除附註，請按一下&#x200B;**[!UICONTROL 刪除]**。

## 最佳作法和限制 {#tips-limitations}

* 如果沒有[!DNL Dynamic Media]授權，您只能使用處理設定檔來處理MP4檔案。
* 使用「處理設定檔」轉碼MP4檔案時，會套用下列准則和限制：

   * Apple ProRes檔案只能轉碼為最大解析度1080p。
   * 如果來源檔案的位元速率大於200 Mbps，您只能轉碼為最大解析度1080p。
   * 如果來源影格速率>=60 fps，則您可使用的來源檔案大小上限為

      * 400 MB （4k轉碼）。
      * 1080p轉碼為800 MB。
      * 720p轉碼為8 GB。

   * 您可以轉碼為4k解析度的檔案大小上限為2.55 GB MP4檔案，解析度為4k、位元速率為12 Mbps和23 fps。

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

>[!MORELIKETHIS]
>
>* [Dynamic Media視訊檔案](/help/assets/dynamic-media/video.md)。
>* [進一步瞭解處理設定檔的使用、型別和設定](/help/assets/asset-microservices-configure-and-use.md)。
