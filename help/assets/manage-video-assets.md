---
title: 管理影片資產
description: 在中上傳、預覽、注釋和發佈視訊資產 [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '4938'
ht-degree: 6%

---

# 管理影片資產 {#manage-video-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service  | 本文 |

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，可在影片資產建立後管理其整個生命週期。

了解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]. 可使用「處理設定檔」和「 [!DNL Dynamic Media] 整合。 無 [!DNL Dynamic Media] 許可證， [!DNL Experience Manager] 提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援檔案格式的預覽縮圖，以及在使用者介面中預覽可直接在瀏覽器中播放支援的格式。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 以副檔名MP4產生視訊資產的預覽。 您可以在 [!DNL Assets] 使用者介面。

1. 在數位資產資料夾或子資料夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下 **[!UICONTROL 建立]** 從工具列中，然後選擇 **[!UICONTROL 檔案]**. 或者，在用戶介面上拖動檔案。 請參閱 [上傳資產](manage-digital-assets.md#uploading-assets) 以取得詳細資訊。
1. 若要在卡片檢視中預覽影片，請按一下 **[!UICONTROL 播放]** ![播放選項](assets/do-not-localize/play.png) 選項。 您只能在卡片檢視中暫停或播放視訊。 此 [!UICONTROL 播放] 和 [!UICONTROL 暫停] 清單檢視中沒有選項可用。
1. 若要在資產詳細資訊頁面中預覽視訊，請選取 **[!UICONTROL 編輯]** 在卡片上。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL的形式包含在網頁中，或直接內嵌資產。 如需詳細資訊，請參閱 [發佈 [!DNL Dynamic Media] 資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 將影片發佈至YouTube {#publishing-videos-to-youtube}

您可以直接將Experience Manager Assets中管理的視訊資產發佈至您先前建立的YouTube管道。

若要將視訊資產發佈至YouTube，您需在Experience Manager Assets中使用標籤標籤視訊資產。 將這些標籤與YouTube管道建立關聯。 如果影片資產的標籤符合YouTube頻道的標籤，則影片會發佈至YouTube。 只要使用相關標籤，發佈至YouTube就會與一般發佈視訊一起發生。

YouTube會自行編碼。 因此，上傳至Experience Manager的原始視訊檔案會發佈至YouTube，而非Dynamic Media編碼已建立的任何視訊轉譯。 雖然使用Dynamic Media處理視訊並非必要動作，但是當播放需要檢視器預設集時，應確實如此。

略過視訊處理設定檔並直接發佈至YouTube時，這只是表示您Experience Manager資產中的視訊資產沒有取得可檢視的縮圖。 這也表示未編碼的視訊無法用於任何Dynamic Media資產類型。

將視訊資產發佈至YouTube伺服器時，必須完成下列工作，以確保透過YouTube進行安全的伺服器對伺服器驗證：

1. [配置Google Cloud設定](#configuring-google-cloud-settings)
1. [建立YouTube管道](#creating-a-youtube-channel)
1. [新增發佈標籤](#adding-tags-for-publishing)
1. [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)
1. [（選用）自動設定您所上傳影片的預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將影片發佈至您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（選用）驗證已發佈的YouTube影片](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTube URL連結至您的Web應用程式](#linking-youtube-urls-to-your-web-application)

您也可以 [取消發佈影片以將其從YouTube中移除](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google Cloud設定 {#configuring-google-cloud-settings}

若要發佈至YouTube，您需要Google帳戶。 如果你有Gmail賬戶，那麼你已經有了Google賬戶；如果您沒有Google帳戶，便可輕鬆建立帳戶。 您需要帳戶，因為您需要憑證才能將影片資產發佈至YouTube。 <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

與Google Cloud搭配使用的帳戶和用於YouTube的Google帳戶不必相同。

Google會定期變更其使用者介面。 因此，將影片發佈至YouTube的步驟可能與下文所述的略有不同。 當您嘗試檢查視訊是否已上傳至YouTube時，也會套用此警告。

>[!NOTE]
>
>下列步驟在編寫時準確無誤。 不過，Google會不經通知便定期更新其雲端網頁。 因此，Google使用者介面中某些設定選項的名稱可能與步驟中使用的名稱稍有不同。

**若要配置Google Cloud設定：**

1. 建立Google帳戶。
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   如果您已有Google帳戶，可以跳至下一個步驟。

1. 前往 [https://cloud.google.com/](https://cloud.google.com/).
1. 在 **[!UICONTROL Google Cloud]** 頁面，在右上角附近，選取 **[!UICONTROL 主控台]**.

   如有必要， **[!UICONTROL 登入]** 使用您的Google帳戶憑證來檢視 **[!UICONTROL 主控台]** 選項。

1. 在 **[!UICONTROL 控制面板]** 頁面，位於 **[!UICONTROL Google Cloud Platform]**，請選取 **[!UICONTROL 專案]** 下拉式清單以開啟 **[!UICONTROL 選取專案]** 對話框。
1. 在 **[!UICONTROL 選取專案]** 對話框，選擇 **[!UICONTROL 新增專案]**.
1. 在 **[!UICONTROL 新增專案]** 對話框， **[!UICONTROL 專案名稱]** 欄位，輸入新專案的名稱。

   您的專案ID以您的專案名稱為基礎。 因此，請謹慎選擇專案名稱；建立後無法變更。 此外，您之後在Experience Manager中設定YouTube時，必須再次輸入相同的專案ID。 所以，把它寫下來。

1. 選擇 **[!UICONTROL 建立]**。

1. 執行下列任一操作：

   * 在專案的控制面板上， **[!UICONTROL 快速入門]** 卡片，選取 **[!UICONTROL 探索並啟用API]**.
   * 在專案的控制面板上， **[!UICONTROL API]** 卡片，選取 **[!UICONTROL 前往API概述]**.

1. 在 **[!UICONTROL API與服務]** 頁面，選取 **[!UICONTROL 啟用API與服務]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在 **[!UICONTROL API程式庫]** 頁面，左側，下方 **[!UICONTROL 類別]**，選取 **[!UICONTROL YouTube]**. 在頁面的右側，選取 **[!UICONTROL YouTube]**.
1. 在 **[!UICONTROL YouTube]** 頁面，選取 **[!UICONTROL YouTube資料API v3]**.
1. 在 **[!UICONTROL YouTube資料API v3]** 頁面，選取 **[!UICONTROL 管理]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 若要使用API，您需要憑證。 如有必要，請在 **[!UICONTROL API與服務]** 頁面，選取 **[!UICONTROL 憑證]**.
1. 在 **[!UICONTROL 憑證]** 頁面，在頂端附近，選取 **[!UICONTROL 建立憑證]**，然後選取 **[!UICONTROL OAuth用戶端ID]**.
1. 在 **[!UICONTROL 建立OAuth用戶端ID]** 頁面，在 **[!UICONTROL 應用程式類型]** 下拉清單，選擇 **[!UICONTROL Web應用程式]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 執行下列任一項作業：

   * 在 **[!UICONTROL 名稱]** 欄位中，輸入OAuth 2.0用戶端的唯一名稱。
   * 使用Google已在 **[!UICONTROL 名稱]** 欄位。

1. 在 **[!UICONTROL 授權的JavaScript原始項]** 標題，選取 **[!UICONTROL 添加URI]**.

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在 **[!UICONTROL URI]** 文本欄位，輸入以下路徑，在路徑中替換您自己的域和埠號，然後按鍵 **[!UICONTROL 輸入]** 要向清單添加路徑：

   `https://<servername.domain>:<port_number>`

   例如 `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上面的URI路徑示例是假設的，僅供說明之用。

1. 在 **[!UICONTROL 授權的重定向URI]** 標題，選擇添加URI。
1. 在 **[!UICONTROL URI]** 文本欄位，輸入以下路徑，在路徑中替換您自己的域和埠號，然後按鍵 **[!UICONTROL 輸入]** 要向清單添加路徑：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如 `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上面的URI路徑示例是假設的，僅供說明之用。

1. 在 **[!UICONTROL 建立OAuth用戶端ID]** 頁面，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL OAuth用戶端已建立]** 對話框，請執行以下操作：

   * （選用）複製 **[!UICONTROL 您的用戶端ID]** 和 **[!UICONTROL 您的用戶端密碼]** 欄位，然後儲存。
   * 選擇 **[!UICONTROL 下載JSON]**，然後儲存JSON檔案。

   稍後在Adobe Experience Manager中設定YouTube時，您需要此下載的JSON檔案。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在 **[!UICONTROL OAuth用戶端已建立]** 對話框，選擇 **[!UICONTROL 確定]**.
1. 登出您的Google帳戶。 現在建立YouTube管道。

### 建立YouTube管道 {#creating-a-youtube-channel}

若要將影片發佈至YouTube，您必須擁有一或多個管道。 如果您已建立YouTube管道，則可略過此工作，然後前往 [新增發佈標籤](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>請確定您已在YouTube中設定一或多個管道 *befor* 您可在「YouTube設定」下方新增管道(請參閱 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem) )。 如果您未進行管道設定，系統不會警告您沒有任何現有管道。 不過，新增頻道時仍會進行Google驗證，但無法選擇要傳送視訊的頻道。

**若要建立YouTube管道：**

1. 前往 [https://www.youtube.com](https://www.youtube.com/) 並使用您的Google帳戶憑證登入。
1. 在YouTube頁面的右上角，選取您的個人資料圖片（也可以以實色圓圈內的字母顯示），然後選取 **[!UICONTROL YouTube設定]** （圓齒輪圖示）。
1. 在「概述」頁面的「其他功能」標題下，選擇 **[!UICONTROL 查看我的所有管道或建立管道]**.
1. 在「管道」頁面上，選取 **[!UICONTROL 建立新管道]**.
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入公司名稱或您選擇要發佈視訊資產的任何其他管道名稱，然後選取 **[!UICONTROL 建立]**.

   記住你在這裡輸入的名字；您必須在Experience Manager中設定YouTube時，必須再次輸入。

1. （選用）如有必要，請新增更多管道。

   現在您已新增要發佈的標籤。

### 新增發佈標籤 {#adding-tags-for-publishing}

若要發佈至YouTube的影片，Experience Manager會將標籤關聯至一或多個YouTube頻道。 若要新增發佈標籤，請參閱 [管理標籤](/help/sites-cloud/authoring/features/tags.md).

或者，如果您想在Experience Manager中使用預設標籤，則可以跳過此任務並轉到 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem).

>[!NOTE]
>
>設定Cloud Service後，此時無需其他設定即可啟用YouTube Publish復寫代理。 原因在於儲存Cloud Service設定時已啟用。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中設定YouTube {#setting-up-youtube-in-aem}

從Experience Manager6.4開始，引入新的觸控使用者介面方法，以在Experience Manager中設定YouTube發佈。 根據您使用的Experience Manager安裝例項，執行下列其中一項操作：

* 若要在6.4之前的Experience Manager中設定YouTube，請參閱 [在6.4之前的Experience Manager中設定YouTube](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* 若要在Experience Manager6.4或更新版本中設定YouTube，請參閱 [在Experience Manager6.4和更新版本中設定YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4和更新版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 請務必以管理員身分登入您的Dynamic Media例項。
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]**（錘子表徵圖）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube發佈設定]**.
1. 選擇 **[!UICONTROL 全球]** （請勿選取）。

1. 在全域頁面的右上角附近，選取 **[!UICONTROL 建立]**.
1. 在「建立YouTube設定」頁面的「Google cloud 平台設定」下方的「應用程式名稱」欄位 **[!UICONTROL 中]** ，輸入Google專案ID。

   您先前初次設定Google Cloud設定時，已指定專案ID。
保留建立YouTube設定頁面開啟；你馬上就回來了。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字編輯器，開啟您先前在工作中下載並儲存的JSON檔案 [配置Google Cloud設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.

   現在在Experience Manager中設定YouTube頻道。

1. 選擇 **[!UICONTROL 新增管道]**.
1. 在「管道名稱」欄位中，輸入您在任務中建立的管道名稱 **[!UICONTROL 新增一或多個管道至YouTube]** 更早。

   您可以視需要選擇新增說明。

1. 選擇 **[!UICONTROL 新增]**.
1. YouTube/Google驗證隨即顯示。 如果您尚未登入Google雲端帳戶，請略過此步驟。

   * 輸入與上述Google專案ID和JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少管道而定，您會看到兩個或多個項目。 選取管道。 不要選擇電子郵件地址；它不是渠道。
   * 在下一頁，選取 **[!UICONTROL 接受]** 允許存取此通道。

1. 選擇 **[!UICONTROL 允許]**.

   現在設定發佈的標籤。

1. **[!UICONTROL 設定發佈的標籤]**  — 在「Cloud Services> YouTube」頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要顯示Experience Manager中可用標籤的清單，請選取下拉式清單圖示（倒轉插入號）。
1. 若要新增，請選取一或多個標籤。

   若要刪除已新增的標籤，請選取標籤，然後選取 **[!UICONTROL X]**.

1. 新增您想要的標籤後，請選取 **[!UICONTROL 儲存]**.

   現在您可將影片發佈至YouTube頻道。

#### 在6.4之前的Experience Manager中設定YouTube {#setting-up-youtube-in-aem-before}

1. 請務必以管理員身分登入您的Dynamic Media例項。

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在「協力廠商服務」標題下方的「YouTube」下方，選取 **[!UICONTROL 立即配置]**.
1. 在「建立配置」對話框中，在相應欄位中輸入標題（必填）和名稱（選填）。
1. 選擇 **[!UICONTROL 建立]**。
1. 在「YouTube帳戶設定」對話方塊的「應用程式名 **[!UICONTROL 稱」欄位中]** ，輸入Google專案ID。

   您最初指定專案ID時 [配置的Google Cloud設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) 更早。
讓「YouTube帳戶設定」對話方塊保持開啟；你馬上就回來了。

1. 使用純文字編輯器，開啟先前在設定Google雲端設定工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 選擇 **[!UICONTROL 確定]**.

   現在在Experience Manager中設定YouTube頻道。

1. 至 **[!UICONTROL 可用通道]**，選取 **+** （加號表徵圖）。
1. 在「YouTube頻道設定」對話方塊的「標題」欄位中，輸入您在「先前新增一或多個頻道至YouTube」工作中建立的頻道名稱 **** 。

   您可以視需要選擇新增說明。

1. 選擇 **[!UICONTROL 確定]**.
1. YouTube/Google驗證隨即顯示。 如果您尚未登入Google雲端帳戶，請略過此步驟。

   * 輸入與上述Google專案ID和JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少管道而定，您會看到兩個或多個項目。 選取管道。 不要選擇電子郵件地址；它不是渠道。
   * 在下一頁，選取 **[!UICONTROL 接受]** 允許存取此通道。

1. 選擇 **[!UICONTROL 允許]**.

   現在設定發佈的標籤。

1. **[!UICONTROL 設定發佈的標籤]**  — 在「Cloud Services> YouTube」頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要顯示Experience Manager中可用標籤的清單，請選取下拉式清單圖示（倒轉插入號）。
1. 若要新增，請選取一或多個標籤。

   若要刪除已新增的標籤，請選取標籤，然後選取 **X**.

1. 新增您想要的標籤後，請選取 **[!UICONTROL 確定]**.

   現在您可將影片發佈至YouTube頻道。

### （選用）自動設定您所上傳影片的預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以選擇在上傳影片時自動設定YouTube屬性。 在Experience Manager中建立中繼資料處理設定檔。

若要建立中繼資料處理設定檔，您必須先從「欄位標籤 **[!UICONTROL 」、「對應至屬性]********** 」和「選擇」欄位複製值，這些全都可在視訊的中繼資料結構中找到。接著，您可以新增這些值，以建立YouTube視訊中繼資料處理設定檔。

**若要自動設定已上傳影片的預設YouTube屬性：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 選擇 **[!UICONTROL 預設]**. （請勿在「預設」左側的選取方塊中新增核取記號。）
1. 在 **[!UICONTROL 預設]** 頁面，核取左側的方塊 **[!UICONTROL 影片]**，然後選取 **[!UICONTROL 編輯]**.
1. 在「元資料結構編輯器」頁上，選擇 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下，選取 **[!UICONTROL YouTube類別]**.
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁簽，執行下列操作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

   * 在 **[!UICONTROL 選擇]**，選擇並複製您要使用的預設值（如「人物與部落格」或「科學與技術」）。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

1. 在「YouTube發佈」標題下，選取 **[!UICONTROL YouTube隱私]**.
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁簽，執行下列操作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

   * 在 **[!UICONTROL 選擇]**，請選取並複製您要使用的預設值。 請注意，「選擇」會分組為兩組。 配對中的底部欄位是您要複製的預設值，例如公用、未列出或私用。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

1. 在「元資料結構編輯器」頁面的右上角附近，選擇 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中，選取 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**.

1. 在「中繼資料描述檔」頁面的右上角附近，選取 **[!UICONTROL 建立]**.
1. 在「添加元資料配置檔案」對話框中， **[!UICONTROL 設定檔標題]** 文本欄位，輸入名稱 `YouTube Video` 然後選取 **[!UICONTROL 建立]**.
1. 在「中繼資料描述檔編輯器」頁面上，選取 **[!UICONTROL 進階]** 標籤。
1. 執行下列動作，將複製的YouTube Publishing值新增至設定檔：

   * 在頁面的右側，選取 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 節標題]** 左邊，放在表單區域。
   * （選用）選取 **[!UICONTROL 欄位標籤]** 來選取元件。
   * （可選）在頁面右側的「設定」標籤下方的「欄位標籤」文字欄位中，輸入 `YouTube Publishing`.
   * 選取 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為的元件 **[!UICONTROL 多值文字]** 把它放下 **[!UICONTROL YouTube發佈]** 標題。

   * 若要選取元件，請選取 **[!UICONTROL 欄位標籤]**.
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（欄位標籤值和對應至屬性值）貼入表單上各自的欄位。 將選擇值貼入預設值欄位。

1. 執行下列動作，將複製的YouTube隱私權值新增至設定檔：

   * 在頁面的右側，選取 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 節標題]** 左邊，放在表單區域。
   * （選用）選取 **[!UICONTROL 欄位標籤]** 來選取元件。
   * （可選）在頁面右側的「設定」標籤下方的「欄位標籤」文字欄位中，輸入 `YouTube Privacy`.
   * 選取 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為的元件 **[!UICONTROL 多值文字]** 把它放下 **[!UICONTROL YouTube隱私]** 標題。

   * 若要選取元件，請選取 **[!UICONTROL 欄位標籤]**.
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（欄位標籤值和對應至屬性值）貼入表單上各自的欄位。 將選擇值貼入預設值欄位。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.
1. 將YouTube發佈中繼資料設定檔套用至您要上傳影片的資料夾。 您必須同時設定「中繼資料描述檔」和「視訊描述檔」。

   請參 [閱中繼資料](/help/assets/metadata-profiles.md)[描述檔和視訊描述檔](/help/assets/dynamic-media/video-profiles.md)。

### 將影片發佈至您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您將先前新增的標籤與視訊資產建立關聯。 此程式可讓Experience Manager知道要發佈至您的YouTube管道的資產。

>[!NOTE]
>
>立即發佈不會自動發佈至YouTube。 設定動態媒體時，有兩個發佈選項可供選擇：立 **[!UICONTROL 即或]****[!UICONTROL 啟動後]**。
>
>**[!UICONTROL 立即發佈]** 表示已上傳的資產（與IPS同步後）會自動發佈至傳送系統。 雖然Dynamic Media的情況確實如此，但YouTube的情況並非如此。 若要發佈至YouTube，您必須透過「Experience Manager作者」發佈。

>[!NOTE]
若要從YouTube發佈內容，Experience Manager會使用 **[!UICONTROL 發佈至YouTube]** 工作流程，可讓您監控進度並檢視任何失敗資訊。
請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).
如需更詳細的進度資訊，您可以在復寫下監控YouTube記錄檔。 但請注意，此類監控需要管理員存取權。

**若要將影片發佈至您的YouTube頻道：**

1. 在Experience Manager中，導覽至您要發佈至YouTube管道的視訊資產。
1. 選取視訊資產（最適化視訊集）。
1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 在「基本」頁簽的「元資料」標題下，選擇 **[!UICONTROL 開啟選取對話方塊]** ，在「標籤」欄位的右側。
1. 在「選取標籤」頁面上，導覽至您要使用的標籤，然後選取一或多個標籤。

   請記住，標籤必須與YouTube管道相關聯。

1. 在頁面的右上角，選取 **[!UICONTROL 選擇]**.
1. 在視訊屬性頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.
1. 在工具列上，選取 **[!UICONTROL 快速發佈]**.

   另請參閱 [搭配Experience Manager Sites使用發佈管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   您可以選擇驗證您的YouTube頻道上已發佈的視訊。

### （選用）驗證已發佈的YouTube影片 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監控YouTube發佈（或取消發佈）的進度。

請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

發佈時間可能會因許多因素而大不相同，這些因素包括主要來源視訊的格式、檔案大小和上傳流量。 發佈程式可能需要幾分鐘到數小時的時間。 另外，更高解析度的格式的呈現速度要慢得多。 例如，720p和1080p的顯示時間比480p要長。

八小時後，如果您仍看到狀態訊息，指出 **[!UICONTROL 已上載（正在處理，請稍候）]**，請嘗試從您的網站移除視訊，然後再次上傳。

### 將YouTube URL連結至您的Web應用程式 {#linking-youtube-urls-to-your-web-application}

您可以取得YouTube URL字串，此字串在您發佈影片後由Dynamic Media產生。 複製YouTube URL時，剪貼簿會隨即顯示，因此您可以視需要將其貼至網站或應用程式中的頁面。

>[!NOTE]
在您將視訊資產發佈至YouTube之前，無法複製YouTube URL。

若要將YouTube URL連結至您的Web應用程式：

1. 導覽至 *YouTube已發佈* 您要複製其URL的視訊資產，然後選取它。

   請記住，YouTube URL僅可複製 *after* 你先 *已發佈* 視訊資產傳送至YouTube。

1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下的「YouTube URL List」（ URL清單）中，選取URL文字，並將其複製至網頁瀏覽器，以預覽資產或新增至您的網頁內容頁面。

### 取消發佈影片，以便從YouTube中移除影片 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消發佈視訊資產時，視訊會從YouTube移除。

>[!CAUTION]
如果您直接從YouTube中移除影片，Experience Manager不會察覺，且會繼續以視訊仍發佈至YouTube的方式運作。 一律透過Experience Manager從YouTube取消發佈視訊資產。

>[!NOTE]
若要從YouTube移除內容，Experience Manager會使用 **[!UICONTROL 從YouTube取消發佈]** 工作流程，可讓您監控進度並檢視任何失敗資訊。
請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

**若要取消發佈影片以從YouTube中移除影片：**

1. 導覽至您要從YouTube管道取消發佈的視訊資產。
1. 在資產選取模式中，選取一或多個已發佈的視訊資產。
1. 在工具列上，選取 **[!UICONTROL 管理出版物]**. 如有必要，請選取三個點圖示(`. . .`)即可檢視 **[!UICONTROL 管理出版物]**.
1. 在管理出版物頁面上，選擇 **[!UICONTROL 取消發佈]**.
1. 在頁面的右上角，選取 **[!UICONTROL 下一個]**.
1. 在頁面的右上角，選取 **[!UICONTROL 取消發佈]**.

## 監視視訊編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

將新視訊上傳至已套用視訊編碼的資料夾時，或將視訊發佈至YouTube、監控視訊編碼/Youtube發佈的進度（或失敗）。 實際YouTube發佈進度僅透過記錄檔提供。 但無論失敗或成功，都會以下列程式中說明的其他方式列出。 此外，當YouTube發佈工作流程或視訊編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

您可以監控進度，包括編碼失敗/YouTube發佈。

1. 在資產資料夾中檢視視訊編碼進度：

   * 在卡片檢視中，視訊編碼進度會依百分比顯示在資產上。 如果發生錯誤，此資訊也會顯示在資產上。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在清單檢視中，視訊編碼進度會顯示在 **[!UICONTROL 處理狀態]** 欄。 如果出現錯誤，則該欄會顯示此訊息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   預設不會顯示此欄。要啟用列，請選擇 **[!UICONTROL 檢視設定]** 從「檢視」下拉式功能表，然後新增 **[!UICONTROL 處理狀態]** 欄和選取 **[!UICONTROL 更新]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 在資產詳細資訊中檢視進度。 選取資產時，請開啟下拉式功能表並選取 **[!UICONTROL 時間表]**. 若要將其縮小至編碼或YouTube發佈等工作流程活動，請選取 **[!UICONTROL 工作流程]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   時間軸中會顯示任何工作流程資訊（例如編碼）。 針對YouTube發佈，工作流程時間軸也包含YouTube管道和YouTube影片URL的名稱。 此外，發佈完成後，您會在工作流程時間軸中看到任何失敗通知。

   >[!NOTE]
   由於上有多個工作流程設定，最終記錄失敗/錯誤訊息可能需花很長時間 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作業佇列設定
   * AdobeGranite工作流程外部流程作業處理常式
   * Granite工作流程逾時佇列

   您可以調整 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 屬性。

1. 如需進行中的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >例項」中的「工作流程例 **[!UICONTROL 項」]******。

   >[!NOTE]
   您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   選取例項並選取 **[!UICONTROL 開啟歷史記錄]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   從「工作流實例」區域，您還可以暫停、終止或更名工作流。 請參閱 [管理工作流程](/help/sites-cloud/authoring/workflows/overview.md) 以取得更多資訊。

1. 有關失敗的作業，請參閱「工具」>「工作流 **[!UICONTROL 程」]** > 「失敗 **[!UICONTROL 」中的「工]** 作流失敗 ****」。「工作 **[!UICONTROL 流失敗]** 」(Workflow Failure)列出所有失敗的工作流活動。

   >[!NOTE]
   您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   由於上有多個工作流程設定，最終記錄錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作業佇列設定
   * AdobeGranite工作流程外部流程作業處理常式
   * Granite工作流程逾時佇列

   您可以調整 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 屬性。

1. 如需完成的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >封存 **[!UICONTROL 」中的「工作流程封存]******」。「工作 **[!UICONTROL 流程存檔]** 」會列出所有已完成的工作流活動。

   >[!NOTE]
   您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您會收到有關中止或失敗工作流程作業的電子郵件通知。 管理員可設定這些電子郵件通知。 請參閱 [設定電子郵件通知](#configuring-e-mail-notifications).

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

[!DNL Experience Manager] as a [!DNL Cloud Service] 可讓您使用「處理設定檔」對MP4視訊檔案執行基本轉碼。 此功能不僅可讓您上傳，還可預覽和縮放MP4視訊檔案。

![在中建立視訊轉碼的處理設定檔 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：中視訊轉碼的處理設定檔 [!DNL Experience Manager].*

如果您只提供寬度或高度，並將其他欄位留空，轉譯會維持外觀比例。 H.264視訊轉碼器可供轉碼使用。

若要使用處理設定檔來處理資產，請新增設定檔至資料夾。 請參閱 [使用處理設定檔來處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## 為視訊資產加上注釋 {#annotate-video-assets}

您可以新增註解至視訊資產。 為視訊加上註解時，播放器會暫停，讓您在影格上加上註解。 如需詳細資訊，請參閱 [管理視訊資產](manage-video-assets.md).

>[!NOTE]
視訊資產註解尚不支援MXF視訊格式。

1. 從 [!DNL Assets] 主控台，選取 **[!UICONTROL 編輯]** 在「資產」卡片上，以顯示「資產詳細資訊」頁面。
1. 若要播放視訊，請按一下 **[!UICONTROL 預覽]**.
1. 若要為視訊加上注釋，請按一下 **[!UICONTROL 注釋]**. 在視訊中的特定時間（幀）添加註釋。 批注時，可以在畫布上繪製，並在繪圖中包括注釋。 注釋會自動儲存。 要退出注釋嚮導，請按一下 **[!UICONTROL 關閉]**.
1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。
1. 要在時間軸中查看它，請按一下注釋。 要從時間軸中刪除注釋，請按一下 **[!UICONTROL 刪除]**.

## 最佳實務和限制 {#tips-limitations}

* 無 [!DNL Dynamic Media] 授權，您只能使用處理設定檔處理MP4檔案。
* 使用處理設定檔將MP4檔案轉碼時，會套用下列准則和限制：

   * Apple ProRes檔案只能將代碼轉換到最高解析度為1080p。
   * 如果源檔案的位元速率大於200 Mbps，則只能將代碼轉換到最大解析度為1080p。
   * 如果源幀數>=60 fps，則可以使用的源檔案的最大大小為，

      * 400 MB（4k轉碼）。
      * 800 MB（1080p轉碼）。
      * 8 GB（720p轉碼）。
   * 可將代碼轉換為4k解析度的最大檔案大小為2.55 GB MP4檔案，解析度為4k、12 Mbps位元速率和23 fps。

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

>[!MORELIKETHIS]
* [Dynamic Media影片檔案](/help/assets/dynamic-media/video.md).
* [深入了解處理設定檔的使用、類型和設定](/help/assets/asset-microservices-configure-and-use.md).

