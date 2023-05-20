---
title: 管理影片資產
description: 在中上載、預覽、注釋和發佈視頻資產 [!DNL Adobe Experience Manager]。
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

## 將視頻發佈到YouTube {#publishing-videos-to-youtube}

您可以將在Experience Manager Assets管理的視頻資產直接發佈到您以前建立的YouTube渠道。

要向YouTube發佈視頻資產，請在Experience Manager Assets為視頻資產添加標籤。 將這些標籤與YouTube頻道關聯。 如果視頻資產的標籤與YouTube頻道的標籤匹配，則視頻將發佈到YouTube。 只要使用關聯的標籤，發佈到YouTube就會與視頻的正常發佈一起發生。

YouTube自己編碼。 因此，上傳到Experience Manager的原始視頻檔案將發佈到YouTube，而不是Dynamic Media編碼建立的任何視頻格式副本。 雖然不需要使用Dynamic Media處理視頻，但在播放時需要觀眾預設時，應該會這樣做。

當您繞過視頻處理配置檔案並直接發佈到YouTube時，這僅僅意味著您的Experience Manager資產中的視頻資產無法獲得可查看的縮略圖。 這還意味著沒有編碼的視頻與任何Dynamic Media資產類型都無關。

向YouTube伺服器發佈視頻資產涉及完成以下任務，以確保與YouTube進行安全、安全的伺服器對伺服器驗證：

1. [配置Google雲設定](#configuring-google-cloud-settings)
1. [建立YouTube頻道](#creating-a-youtube-channel)
1. [添加用於發佈的標籤](#adding-tags-for-publishing)
1. [設定YouTubeExperience Manager](#setting-up-youtube-in-aem)
1. [（可選）自動設定上載視頻的預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將視頻發佈到您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（可選）驗證YouTube上發佈的視頻](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTubeURL連結到Web應用程式](#linking-youtube-urls-to-your-web-application)

您也可以 [取消發佈視頻，從YouTube](#unpublishing-videos-to-remove-them-from-youtube)。

### 配置Google雲設定 {#configuring-google-cloud-settings}

要發佈到YouTube，你需要一個Google帳戶。 如果你有GMAIL賬戶，那麼你已經有Google賬戶了；如果您沒有Google帳戶，則可以輕鬆建立一個帳戶。 您需要該帳戶，因為您需要憑據將視頻資產發佈到YouTube。 <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

與Google雲使用的帳戶和用於YouTube的Google帳戶不必相同。

Google定期更改其用戶介面。 因此，向YouTube發佈視頻的步驟與下面記錄的步驟稍有不同。 當您嘗試檢查視頻是否上傳到YouTube時，此警告也適用。

>[!NOTE]
>
>在編寫時，以下步驟是準確的。 不過，Google會不經通知就定期更新其雲網頁。 因此，某些配置選項在Google用戶介面中的命名可能與步驟中使用的名稱稍有不同。

**配置Google雲設定：**

1. 建立Google帳戶。
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   如果您已擁有Google帳戶，則可以跳至下一步。

1. 轉到 [https://cloud.google.com/](https://cloud.google.com/)。
1. 在 **[!UICONTROL Google雲]** 頁面，靠近右上角，選擇 **[!UICONTROL 控制台]**。

   如有必要， **[!UICONTROL 登錄]** 使用你的Google帳戶憑據查看 **[!UICONTROL 控制台]** 的雙曲餘切值。

1. 在 **[!UICONTROL 儀表板]** 頁，位於 **[!UICONTROL Google雲平台]**，選擇 **[!UICONTROL 項目]** 下拉清單以開啟 **[!UICONTROL 選擇項目]** 對話框。
1. 在 **[!UICONTROL 選擇項目]** 對話框，選擇 **[!UICONTROL 新建項目]**。
1. 在 **[!UICONTROL 新建項目]** 對話框 **[!UICONTROL 項目名稱]** 的子菜單。

   您的項目ID基於您的項目名稱。 因此，仔細選擇項目名稱；建立後無法更改。 此外，以後在Experience Manager中設定YouTube時，必須再次輸入相同的項目ID。 所以，記下來。

1. 選擇 **[!UICONTROL 建立]**。

1. 執行下列任一操作：

   * 在項目的儀表板上， **[!UICONTROL 入門]** 卡，選擇 **[!UICONTROL 瀏覽和啟用API]**。
   * 在項目的儀表板上， **[!UICONTROL API]** 卡，選擇 **[!UICONTROL 轉到API概述]**。

1. 靠近 **[!UICONTROL API和服務]** ，選擇 **[!UICONTROL 啟用API和服務]**。<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在 **[!UICONTROL API庫]** 頁面，左側，下方 **[!UICONTROL 類別]**&#x200B;選中 **[!UICONTROL YouTube]**。 在頁面右側，選擇 **[!UICONTROL YouTube]**。
1. 在 **[!UICONTROL YouTube]** ，選擇 **[!UICONTROL YouTube資料API v3]**。
1. 在 **[!UICONTROL YouTube資料API v3]** ，選擇 **[!UICONTROL 管理]**。

   ![6_5_googleaccount-apis manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 要使用API，需要憑據。 如有必要，請在 **[!UICONTROL API和服務]** ，選擇 **[!UICONTROL 憑據]**。
1. 在 **[!UICONTROL 憑據]** 頁，靠近頂部，選擇 **[!UICONTROL 建立憑據]**，然後選擇 **[!UICONTROL OAuth客戶端ID]**。
1. 在 **[!UICONTROL 建立OAuth客戶端ID]** 的 **[!UICONTROL 應用程式類型]** 下拉清單，選擇 **[!UICONTROL Web應用程式]**。

   ![6_5_googleaccount-apis應用程式類型](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 執行下列任一項作業：

   * 在 **[!UICONTROL 名稱]** 欄位，輸入OAuth 2.0客戶端的唯一名稱。
   * 使用Google已在 **[!UICONTROL 名稱]** 的子菜單。

1. 在 **[!UICONTROL 已授權的JavaScript源]** 標題，選擇 **[!UICONTROL 添加URI]**。

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在 **[!UICONTROL URI]** 文本欄位，輸入以下路徑，替換路徑中的域和埠號，然後按 **[!UICONTROL 輸入]** 將路徑添加到清單：

   `https://<servername.domain>:<port_number>`

   例如 `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上面的URI路徑示例是假設的，僅供說明之用。

1. 在 **[!UICONTROL 授權重定向URI]** 標題，選擇「添加URI」。
1. 在 **[!UICONTROL URI]** 文本欄位，輸入以下路徑，替換路徑中的域和埠號，然後按 **[!UICONTROL 輸入]** 將路徑添加到清單：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如 `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上面的URI路徑示例是假設的，僅供說明之用。

1. 靠近 **[!UICONTROL 建立OAuth客戶端ID]** ，選擇 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 已建立OAuth客戶端]** 對話框，執行以下操作：

   * （可選）複製 **[!UICONTROL 您的客戶端ID]** 和 **[!UICONTROL 您的客戶機密碼]** 欄位，然後保存。
   * 選擇 **[!UICONTROL 下載JSON]**，然後保存JSON檔案。

   稍後在Adobe Experience Manager設定YouTube時，需要此下載的JSON檔案。

   ![已建立6_5_googleaccount-apis oauthclient](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在 **[!UICONTROL 已建立OAuth客戶端]** 對話框，選擇 **[!UICONTROL 確定]**。
1. 註銷你的Google帳戶。 現在建立一個YouTube頻道。

### 建立YouTube頻道 {#creating-a-youtube-channel}

向YouTube發佈視頻需要您有一個或多個渠道。 如果已建立YouTube頻道，則可以跳過此任務並轉到 [添加用於發佈的標籤](/help/assets/dynamic-media/video.md#adding-tags-for-publishing)。

>[!CAUTION]
>
>確保已在YouTube設定一個或多個頻道 *先* 在Experience Manager中的YouTube設定下添加頻道(請參閱 [設定YouTubeExperience Manager](#setting-up-youtube-in-aem) )。 如果您未能完成通道設定，則系統不會警告您沒有現有通道。 但是，在添加頻道時仍會進行Google驗證，但無法選擇發送視頻的頻道。

**要建立YouTube頻道：**

1. 轉到 [https://www.youtube.com](https://www.youtube.com/) 並使用你的Google帳戶憑據登錄。
1. 在YouTube頁面的右上角，選擇您的配置檔案圖片（它也可以顯示為實心彩色圓中的字母），然後選擇 **[!UICONTROL YouTube設定]** （圓齒輪表徵圖）。
1. 在「概述」(Overview)頁面的「附加功能」(Additional Features)標題下，選擇 **[!UICONTROL 查看我的所有頻道或建立頻道]**。
1. 在「通道」頁上，選擇 **[!UICONTROL 建立新渠道]**。
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入公司名稱或您選擇的發佈視頻資產的任何其他渠道名稱，然後選擇 **[!UICONTROL 建立]**。

   記住你在這裡輸入的名稱；你必須把YouTube設定為Experience Manager時，必須再次輸入。

1. （可選）如有必要，請添加更多通道。

   現在，添加用於發佈的標籤。

### 添加用於發佈的標籤 {#adding-tags-for-publishing}

要發佈到您的視頻到YouTube,Experience Manager會將標籤關聯到一個或多個YouTube頻道。 要添加用於發佈的標籤，請參見 [管理標籤](/help/sites-cloud/authoring/features/tags.md)。

或者，如果要在Experience Manager中使用預設標籤，可以跳過此任務並轉到 [設定YouTubeExperience Manager](#setting-up-youtube-in-aem)。

>[!NOTE]
>
>配置Cloud Service後，此時不需要其他配置來啟用YouTube發佈複製代理。 原因是在保存Cloud Service配置時啟用了它。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 設定YouTubeExperience Manager {#setting-up-youtube-in-aem}

從Experience Manager6.4開始，介紹了一種新的觸摸式用戶介面方法，用於Experience Manager建立YouTube出版。 根據您正在使用的Experience Manager的已安裝實例，執行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，請參見 [在6.4之前在Experience Manager建立YouTube](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before)。
* 要在Experience Manager6.4或更高版本中配置YouTube，請參見 [在Experience Manager6.4及更高版本中設定YouTube](#setting-up-youtube-in-aem-and-later)。

#### 在Experience Manager6.4及更高版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 確保以管理員身份登錄到Dynamic Media實例。
1. 在Experience Manager的左上角，選擇Experience Manager徽標，然後在左滑軌中導航至 **[!UICONTROL 工具]**（錘子表徵圖）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube發佈配置]**。
1. 選擇 **[!UICONTROL 全球]** （不選）。

1. 在全局頁面的右上角，選擇 **[!UICONTROL 建立]**。
1. 在「建立YouTube設定」頁面的「Google cloud 平台設定」下方的「應用程式名稱」欄位 **[!UICONTROL 中]** ，輸入Google專案ID。

   您最初在較早配置Google雲設定時指定了項目ID。
保持「建立YouTube配置」頁面開啟；你馬上就要回來了。

   ![6_5_youtubepublish-createyoutuconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字檔案編輯器，開啟您在任務早期下載並保存的JSON檔案 [配置Google雲設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)。
1. 選擇並複製整個JSON文本。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 在頁面右上角附近，選擇 **[!UICONTROL 保存]**。

   現在在YouTube開設Experience Manager頻道。

1. 選擇 **[!UICONTROL 添加通道]**。
1. 在「渠道名稱」欄位中，輸入您在任務中建立的渠道的名稱 **[!UICONTROL 向YouTube添加一個或多個頻道]** 早些。

   如果需要，您可以根據需要添加說明。

1. 選擇 **[!UICONTROL 添加]**。
1. 顯示YouTube/Google驗證。 如果您尚未登錄Google雲帳戶，則跳過此步驟。

   * 輸入與上面的Google項目ID和JSON文本關聯的Google用戶名和密碼。
   * 根據您的帳戶有多少個渠道，您可以看到兩個或多個項目。 選擇一個頻道。 不要選擇電子郵件地址；不是頻道。
   * 在下一頁，選擇 **[!UICONTROL 接受]** 允許訪問此頻道。

1. 選擇 **[!UICONTROL 允許]**。

   現在設定發佈標籤。

1. **[!UICONTROL 設定發佈標籤]**  — 在「Cloud Services」>「YouTube」頁面上，選擇鉛筆表徵圖以編輯要使用的標籤清單。
1. 要在Experience Manager中顯示可用標籤的清單，請選擇下拉清單表徵圖（倒置插入符號）。
1. 要添加標籤，請選擇一個或多個標籤。

   要刪除已添加的標籤，請選擇該標籤，然後選擇 **[!UICONTROL X]**。

1. 添加完所需標籤後，選擇 **[!UICONTROL 保存]**。

   現在你將視頻發佈到你的YouTube頻道。

#### 在6.4之前在Experience Manager建立YouTube {#setting-up-youtube-in-aem-before}

1. 確保以管理員身份登錄到Dynamic Media實例。

1. 在Experience Manager的左上角，選擇Experience Manager徽標，然後在左滑軌中導航至 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**。
1. 在「第三方服務」標題下，在「YouTube」下，選擇 **[!UICONTROL 立即配置]**。
1. 在「建立配置」對話框中，在相應欄位中輸入標題（必需）和名稱（可選）。
1. 選擇 **[!UICONTROL 建立]**。
1. 在「YouTube帳戶設定」對話方塊的「應用程式名 **[!UICONTROL 稱」欄位中]** ，輸入Google專案ID。

   最初指定項目ID時 [已配置Google雲設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) 早些。
保持「YouTube帳戶設定」對話框開啟；你馬上就要回來了。

1. 使用純文字檔案編輯器，開啟在「配置Google雲」設定任務中先前下載並保存的JSON檔案。
1. 選擇並複製整個JSON文本。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 選擇 **[!UICONTROL 確定]**。

   現在在YouTube開設Experience Manager頻道。

1. 在 **[!UICONTROL 可用頻道]**&#x200B;選中 **+** （加號表徵圖）。
1. 在「YouTube頻道設定」對話方塊的「標題」欄位中，輸入您在「先前新增一或多個頻道至YouTube」工作中建立的頻道名稱 **** 。

   如果需要，您可以根據需要添加說明。

1. 選擇 **[!UICONTROL 確定]**。
1. 顯示YouTube/Google驗證。 如果您尚未登錄Google雲帳戶，則跳過此步驟。

   * 輸入與上面的Google項目ID和JSON文本關聯的Google用戶名和密碼。
   * 根據您的帳戶有多少個渠道，您可以看到兩個或多個項目。 選擇一個頻道。 不要選擇電子郵件地址；不是頻道。
   * 在下一頁，選擇 **[!UICONTROL 接受]** 允許訪問此頻道。

1. 選擇 **[!UICONTROL 允許]**。

   現在設定發佈標籤。

1. **[!UICONTROL 設定發佈標籤]**  — 在「Cloud Services」>「YouTube」頁面上，選擇鉛筆表徵圖以編輯要使用的標籤清單。
1. 要在Experience Manager中顯示可用標籤的清單，請選擇下拉清單表徵圖（倒置插入符號）。
1. 要添加標籤，請選擇一個或多個標籤。

   要刪除已添加的標籤，請選擇該標籤，然後選擇 **X**。

1. 添加完所需標籤後，選擇 **[!UICONTROL 確定]**。

   現在你將視頻發佈到你的YouTube頻道。

### （可選）自動設定上載視頻的預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以選擇在上傳視頻時自動設定YouTube屬性。 在Experience Manager中建立元資料處理配置檔案。

若要建立中繼資料處理設定檔，您必須先從「欄位標籤 **[!UICONTROL 」、「對應至屬性]********** 」和「選擇」欄位複製值，這些全都可在視訊的中繼資料結構中找到。然後，通過將這些值添加到您的YouTube視頻元資料處理配置檔案中來構建這些值。

**要自動設定上載視頻的預設YouTube屬性，請執行以下操作：**

1. 在Experience Manager的左上角，選擇Experience Manager徽標，然後在左滑軌中導航至 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。
1. 選擇 **[!UICONTROL 預設]**。 （不要在「default」左側的選擇框中添加複選標籤。）
1. 在 **[!UICONTROL 預設]** 頁面，選中 **[!UICONTROL 視頻]**，然後選擇 **[!UICONTROL 編輯]**。
1. 在「元資料架構編輯器」頁上，選擇 **[!UICONTROL 高級]** 頁籤。
1. 在「YouTube出版」標題下，選擇 **[!UICONTROL YouTube類]**。
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁籤中，執行以下操作：

   * 在 **[!UICONTROL 映射到屬性]** 文本欄位，選擇並複製值。
將複製的值貼上到開啟的文本編輯器中。 以後建立元資料處理配置檔案時，您將需要此值。 保持文本編輯器開啟。

   * 下 **[!UICONTROL 選擇]**，選擇並複製您要使用的預設值（如「人員和部落格」或「科學與技術」）。
將複製的值貼上到開啟的文本編輯器中。 以後建立元資料處理配置檔案時，您將需要此值。 保持文本編輯器開啟。

1. 在「YouTube出版」標題下，選擇 **[!UICONTROL YouTube隱私]**。
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁籤中，執行以下操作：

   * 在 **[!UICONTROL 映射到屬性]** 文本欄位，選擇並複製值。
將複製的值貼上到開啟的文本編輯器中。 以後建立元資料處理配置檔案時，您將需要此值。 保持文本編輯器開啟。

   * 下 **[!UICONTROL 選擇]**，選擇並複製要使用的預設值。 請注意，「選項」(Choices)分成兩對。 對中的底部欄位是要複製的預設值，如公共、未列出或私有。
將複製的值貼上到開啟的文本編輯器中。 以後建立元資料處理配置檔案時，您將需要此值。 保持文本編輯器開啟。

1. 在「元資料架構編輯器」頁的右上角，選擇 **[!UICONTROL 取消]**。
1. 在Experience Manager的左上角，選擇Experience Manager徽標，然後在左滑軌中，選擇 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 元資料配置檔案]**。

1. 在「元資料概要檔案」頁面的右上角附近，選擇 **[!UICONTROL 建立]**。
1. 在「添加元資料配置檔案」對話框中， **[!UICONTROL 配置檔案標題]** 文本欄位，輸入名稱 `YouTube Video` 選擇 **[!UICONTROL 建立]**。
1. 在「元資料配置檔案編輯器」頁上，選擇 **[!UICONTROL 先進]** 頁籤。
1. 通過執行以下操作將複製的YouTube發佈值添加到配置檔案：

   * 在頁面的右側，選擇 **[!UICONTROL 生成窗體]** 頁籤。
   * （可選）拖動標有 **[!UICONTROL 節標題]** 左邊，然後放到窗體區域。
   * （可選）選擇 **[!UICONTROL 欄位標籤]** 的子菜單。
   * （可選）在頁面右側的「設定」頁籤下的「欄位標籤」文本欄位中，輸入 `YouTube Publishing`。
   * 選擇 **[!UICONTROL 生成窗體]** 頁籤，然後拖動標籤為 **[!UICONTROL 多值文本]** 放在下面 **[!UICONTROL YouTube出版]** 建立的標題。

   * 要選擇元件，請選擇 **[!UICONTROL 欄位標籤]**。
   * 在頁面右側的「設定」頁籤下，將先前複製的YouTube發佈值（欄位標籤值和映射到屬性值）貼上到窗體中的相應欄位中。 將「選擇」值貼上到「預設值」欄位。

1. 通過執行以下操作將複製的YouTube隱私值添加到配置檔案：

   * 在頁面的右側，選擇 **[!UICONTROL 生成窗體]** 頁籤。
   * （可選）拖動標有 **[!UICONTROL 節標題]** 左邊，然後放到窗體區域。
   * （可選）選擇 **[!UICONTROL 欄位標籤]** 的子菜單。
   * （可選）在頁面右側的「設定」頁籤下的「欄位標籤」文本欄位中，輸入 `YouTube Privacy`。
   * 選擇 **[!UICONTROL 生成窗體]** 頁籤，然後拖動標籤為 **[!UICONTROL 多值文本]** 放在下面 **[!UICONTROL YouTube隱私]** 的子菜單。

   * 要選擇元件，請選擇 **[!UICONTROL 欄位標籤]**。
   * 在頁面右側的「設定」頁籤下，將先前複製的YouTube發佈值（欄位標籤值和映射到屬性值）貼上到窗體中的相應欄位中。 將「選擇」值貼上到「預設值」欄位。

1. 在頁面右上角附近，選擇 **[!UICONTROL 保存]**。
1. 將YouTube發佈元資料配置檔案應用到要上載視頻的資料夾。 必須同時設定元資料配置檔案和視頻配置檔案。

   請參 [閱中繼資料](/help/assets/metadata-profiles.md)[描述檔和視訊描述檔](/help/assets/dynamic-media/video-profiles.md)。

### 將視頻發佈到您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您將先前添加的標籤與視頻資產相關聯。 此過程使Experience Manager知道要發佈到您的YouTube渠道的資產。

>[!NOTE]
>
>立即發佈不會自動發佈到YouTube。 設定動態媒體時，有兩個發佈選項可供選擇：立 **[!UICONTROL 即或]****[!UICONTROL 啟動後]**。
>
>**[!UICONTROL 立即發佈]** 表示上載的資產在與IPS同步後自動發佈到傳遞系統。 雖然Dynamic Media是如此，但YouTube並非如此。 要發表到YouTube，必須以Experience Manager作者的方式發表。

>[!NOTE]
要從YouTube發佈內容，Experience Manager使用 **[!UICONTROL 發佈到YouTube]** 工作流，它允許您監視進度並查看任何故障資訊。
請參閱 [監視視頻編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。
有關更詳細的進度資訊，您可以監視複製下的YouTube日誌。 但是，請注意，此類監視需要管理員訪問權限。

**要將視頻發佈到您的YouTube頻道：**

1. 在Experience Manager中，導航到要發佈到YouTube頻道的視頻資產。
1. 選擇視頻資產（自適應視頻集）。
1. 在工具欄上，選擇 **[!UICONTROL 屬性]**。
1. 在「基本」頁籤的「元資料」標題下，選擇 **[!UICONTROL 開啟選擇對話框]** 的子菜單。
1. 在「選擇標籤」頁上，導航到要使用的標籤，然後選擇一個或多個標籤。

   請記住，標籤必須與YouTube頻道關聯。

1. 在頁面的右上角，選擇 **[!UICONTROL 選擇]**。
1. 在視頻的屬性頁面的右上角，選擇 **[!UICONTROL 保存並關閉]**。
1. 在工具欄上，選擇 **[!UICONTROL 快速發佈]**。

   另請參閱 [將出版物管理與Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring)。

   您可以選擇驗證您的YouTube頻道上發佈的視頻。

### （可選）驗證YouTube上發佈的視頻 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監視YouTube發佈（或取消發佈）的進度。

請參閱 [監視視頻編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。

發佈時間可能會有很大差異，具體取決於包括主源視頻格式、檔案大小和上載通信量在內的眾多因素。 發佈過程可能需要幾分鐘到幾個小時。 此外，解析度更高的格式的渲染速度要慢得多。 例如，720p和1080p的顯示時間要長於480p。

八小時後，如果您仍然看到狀態消息， **[!UICONTROL 已上載（正在處理，請稍候）]**，嘗試從您的站點刪除視頻，然後重新上載。

### 將YouTubeURL連結到Web應用程式 {#linking-youtube-urls-to-your-web-application}

您可以獲取在發佈視頻後由Dynamic Media生成的YouTubeURL字串。 複製YouTubeURL時，它會降落到剪貼簿上，以便您可以根據需要貼上到網站或應用程式中的頁面。

>[!NOTE]
在您將視頻資產發佈到YouTube之前，YouTubeURL不可複製。

要將YouTubeURL連結到Web應用程式：

1. 導航到 *YouTube* 要複製其URL的視頻資產，然後選擇它。

   請記住，YouTubeURL僅可複製 *後* 你先 *出版* 視頻資產給YouTube。

1. 在工具欄上，選擇 **[!UICONTROL 屬性]**。
1. 選擇 **[!UICONTROL 高級]** 頁籤。
1. 在「YouTube發佈」標題下的「YouTubeURL清單」中，選擇URL文本並將其複製到Web瀏覽器以預覽資產或添加到Web內容頁面。

### 取消發佈視頻，以便從YouTube刪除 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消發佈視頻資產時，該視頻將從YouTube刪除。

>[!CAUTION]
如果直接從YouTube內刪除視頻，Experience Manager不會察覺，並繼續表現得好像該視頻仍然發佈到YouTube。 總是通過Experience Manager取消發佈來自YouTube的視頻資產。

>[!NOTE]
要從YouTube刪除內容，Experience Manager使用 **[!UICONTROL 從YouTube取消出版]** 工作流，它允許您監視進度並查看任何故障資訊。
請參閱 [監視視頻編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress)。

**要取消發佈視頻以從YouTube刪除視頻，請：**

1. 導航到要從您的YouTube頻道取消發佈的視頻資產。
1. 在資產選擇模式中，選擇一個或多個已發佈視頻資產。
1. 在工具欄上，選擇 **[!UICONTROL 管理發布]**。 如有必要，請選擇三點表徵圖(`. . .`) **[!UICONTROL 管理發布]**。
1. 在「管理發布」頁上，選擇 **[!UICONTROL 取消發佈]**。
1. 在頁面的右上角，選擇 **[!UICONTROL 下一個]**。
1. 在頁面的右上角，選擇 **[!UICONTROL 取消發佈]**。

## 監視視頻編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

將新視頻上載到應用了視頻編碼的資料夾，或將視頻發佈到YouTube，監視視頻編碼/Youtube發佈的進展（或失敗）。 實際的YouTube發佈進度僅通過日誌提供。 但無論失敗還是成功，都會以下步驟中描述的其他方式列出。 此外，當YouTube發佈工作流或視頻編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

您可以監視進度，包括失敗的編碼/YouTube發佈。

1. 查看資產資料夾中的視頻編碼進度：

   * 在卡視圖中，按百分比顯示資產的視頻編碼進度。 如果出現錯誤，此資訊也會顯示在資產上。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在清單視圖中，視頻編碼進度顯示在 **[!UICONTROL 處理狀態]** 的雙曲餘切值。 如果出現錯誤，則該欄會顯示此訊息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   預設不會顯示此欄。要啟用列，請選擇 **[!UICONTROL 查看設定]** 從「視圖」(views)下拉菜單中，添加 **[!UICONTROL 處理狀態]** 列和選擇 **[!UICONTROL 更新]**。

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 查看資產詳細資訊中的進度。 選擇資產時，開啟下拉菜單並選擇 **[!UICONTROL 時間軸]**。 要將其縮小到工作流活動(如編碼或YouTube發佈)，請選擇 **[!UICONTROL 工作流]**。

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   所有工作流資訊（如編碼）都顯示在時間軸中。 對於YouTube發佈，工作流時間線還包括YouTube頻道和YouTube視頻URL的名稱。 此外，在發佈完成後，在工作流時間線中可以看到任何失敗通知。

   >[!NOTE]
   由於上的多個工作流配置，最終記錄失敗/錯誤消息可能需要很長時間 **[!UICONTROL 重試]**。 **[!UICONTROL 重試延遲]**, **[!UICONTROL 超時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作業隊列配置
   * Adobe花崗岩工作流外部進程作業處理程式
   * 花崗岩工作流超時隊列

   您可以調整 **[!UICONTROL 重試]**。 **[!UICONTROL 重試延遲]**, **[!UICONTROL 超時]** 屬性。

1. 如需進行中的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >例項」中的「工作流程例 **[!UICONTROL 項」]******。

   >[!NOTE]
   您需要管理權限才能訪問 **[!UICONTROL 工具]** 的子菜單。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   選擇實例並選擇 **[!UICONTROL 開啟歷史記錄]**。

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   在「工作流實例」(Workflow Instances)區域中，您還可以掛起、終止或更名工作流。 請參閱 [管理工作流](/help/sites-cloud/authoring/workflows/overview.md) 的子菜單。

1. 有關失敗的作業，請參閱「工具」>「工作流 **[!UICONTROL 程」]** > 「失敗 **[!UICONTROL 」中的「工]** 作流失敗 ****」。「工作 **[!UICONTROL 流失敗]** 」(Workflow Failure)列出所有失敗的工作流活動。

   >[!NOTE]
   您需要管理權限才能訪問 **[!UICONTROL 工具]** 的子菜單。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   由於上的多個工作流配置，最終記錄錯誤消息可能需要很長時間 **[!UICONTROL 重試]**。 **[!UICONTROL 重試延遲]**, **[!UICONTROL 超時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作業隊列配置
   * Adobe花崗岩工作流外部進程作業處理程式
   * 花崗岩工作流超時隊列

   您可以調整 **[!UICONTROL 重試]**。 **[!UICONTROL 重試延遲]**, **[!UICONTROL 超時]** 屬性。

1. 如需完成的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >封存 **[!UICONTROL 」中的「工作流程封存]******」。「工作 **[!UICONTROL 流程存檔]** 」會列出所有已完成的工作流活動。

   >[!NOTE]
   您需要管理權限才能訪問 **[!UICONTROL 工具]** 的子菜單。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您會收到有關已中止或失敗的工作流作業的電子郵件通知。 管理員可配置這些電子郵件通知。 請參閱 [配置電子郵件通知](#configuring-e-mail-notifications)。

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

## 使用處理配置檔案進行轉碼 {#transcode-video}

[!DNL Experience Manager] 作為 [!DNL Cloud Service] 允許您使用「處理配置檔案」對MP4視頻檔案執行基本轉碼。 該功能不僅允許您上載MP4視頻檔案，還允許您預覽和縮放MP4視頻檔案。

![建立處理配置檔案以在中進行視頻轉碼 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：一種視頻轉碼處理簡檔 [!DNL Experience Manager]。*

如果僅提供寬度或僅提供高度，並將其他欄位留空，則格式副本將保持長寬比。 H.264視頻編解碼器可用於轉碼。

要使用處理配置檔案處理資產，請將配置檔案添加到資料夾。 請參閱 [使用處理配置檔案處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 注釋視頻資產 {#annotate-video-assets}

您可以向視頻資產添加註釋。 在注釋視頻時，播放器會暫停以允許您在框架上進行注釋。 有關詳細資訊，請參閱 [管理視頻資產](manage-video-assets.md)。

>[!NOTE]
視頻資產批注尚不支援MXF視頻格式。

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
* [Dynamic Media視頻文檔](/help/assets/dynamic-media/video.md)。
* [瞭解有關處理配置檔案的使用、類型和配置的更多資訊](/help/assets/asset-microservices-configure-and-use.md)。

