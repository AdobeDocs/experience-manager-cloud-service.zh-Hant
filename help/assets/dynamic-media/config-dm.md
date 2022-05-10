---
title: 配置Dynamic MediaCloud Service
description: 瞭解如何在Adobe Experience Manager as a Cloud Service配置Dynamic Media。
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 527c25ef61f9553a9e0012b8413a8bc6ccf4afdd
workflow-type: tm+mt
source-wordcount: '3449'
ht-degree: 3%

---

# 關於配置Dynamic MediaCloud Service {#configuring-dynamic-media}

如果您將Adobe Experience Manager用於不同的環境，例如開發、試運行和即時生產，請為這些環境中的每個環境配置Dynamic MediaCloud Services。

另請參閱 [配置Dynamic Media公司別名帳戶](/help/assets/dynamic-media/dm-alias-account.md)

## Dynamic Media建築圖 {#architecture-diagram-of-dynamic-media}

下面的體系結構圖描述了Dynamic Media的工作原理。

有了新的體系結構，Experience Manager負責主要來源資產，並與Dynamic Media進行資產處理和發佈同步：

1. 當主源資產上載到Adobe Experience Manager as a Cloud Service時，將其複製到Dynamic Media。 此時，Dynamic Media將處理所有資產處理和格式副本生成，如視頻編碼和影像的動態變型。
1. 生成格式副本後，Experience Manageras a Cloud Service可以安全訪問和預覽遠程Dynamic Media格式副本(不會將二進位檔案發回Experience Manageras a Cloud Service實例)。
1. 在內容準備發佈和批准後，它將觸發Dynamic Media服務，將內容推送到CDN（內容分發網路）上的分發伺服器並快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>以下功能清單要求您使用與Adobe Experience Manager-Dynamic Media捆綁的現成CDN。 這些功能不支援任何其他自定義CDN。
>
>* [智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
>* [快取無效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [熱鏈路保護](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2 內容傳送](/help/assets/dynamic-media/http2faq.md)
>* CDN級別的URL重定向
>* Akamai ChinaCDN（在中國實現最佳交付）


<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## 在Cloud Services中建立Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manageras a Cloud Service中，選擇Experience Manageras a Cloud Service徽標以訪問全局導航控制台。
1. 在控制台左側，選擇「工具」表徵圖，然後轉到 **[!UICONTROL Cloud Services>Dynamic Media配置]**。
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，選擇 **[!UICONTROL 全球]** (不選擇資料夾表徵圖 **[!UICONTROL 全球]**)。 然後選擇 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立Dynamic Media配置]** 頁，輸入Dynamic Media帳戶的公司管理員的標題、Dynamic Media帳戶電子郵件地址和密碼，然後選擇您的區域。 此資訊是通過Adobe在預配電子郵件中提供給您的。 如果您未收到此電子郵件，請與Adobe客戶支援聯繫。
1. 選擇 **[!UICONTROL 連接到Dynamic Media]**。
1. 在 **[!UICONTROL 更改密碼]** 對話框 **[!UICONTROL 新密碼]** 欄位中，輸入包含8-25個字元的新密碼。 密碼必須至少包含下列各項之一：

   * 大寫字母
   * 小寫字母
   * 數量
   * 特殊字元： `# $ & . - _ : { }`

   的 **[!UICONTROL 當前密碼]** 欄位被有意預先填充，並且隱藏在交互中。

   如有必要，您可以通過選擇密碼眼表徵圖來顯示密碼來檢查鍵入或重新鍵入的密碼的拼寫。 再次選擇該表徵圖以隱藏密碼。

1. 在 **[!UICONTROL 重複密碼]** ，重新鍵入新密碼，然後選擇 **[!UICONTROL 完成]**。

   新密碼將在您選擇 **[!UICONTROL 保存]** 右上角 **[!UICONTROL 建立Dynamic Media配置]** 的子菜單。

   如果已選擇 **[!UICONTROL 取消]** 的 **[!UICONTROL 更改密碼]** 對話框，在保存新建立的Dynamic Media配置時，仍必須輸入新密碼。

   另請參閱 [將密碼更改為Dynamic Media](#change-dm-password)。

1. 連接成功後，可以設定以下項：

   | 屬性 | 說明 |
   |---|---|
   | 公司 | Dynamic Media帳戶的名稱。 您可能有多個Dynamic Media客戶，分別針對不同的子品牌、部門或分段/生產環境。<br>另請參閱 [配置Dynamic Media公司別名帳戶](/help/assets/dynamic-media/dm-alias-account.md)。 |
   | 公司根資料夾路徑 | 您公司的根資料夾路徑。 |
   | 發佈資產 | 您可以從以下三個選項中進行選擇：<br>**[!UICONTROL 立即&#x200B;]**— 上載資產時，系統將接收資產並立即提供URL/Embed。 發佈資產不需要用戶干預。<br>**[!UICONTROL 激活時]**  — 在提供URL/嵌入連結之前，必須先顯式發佈資產。<br>**[!UICONTROL 選擇性發佈&#x200B;]**— 資產僅自動發佈用於安全預覽。 也可將它們明確發佈到Experience Manageras a Cloud Service，而不發佈到DMS7以在公共域中交付。 今後，此選項打算將資產公佈到Experience Manageras a Cloud Service，並將資產公佈到Dynamic Media，相互排斥。 即，您可以將資產發佈到DMS7，以便可以使用智慧裁剪或動態格式副本等功能。 或者，您可以只發佈Experience Manageras a Cloud Service中的資產以供預覽；這些相同的資產未在DMS7中發佈，以便在公共域中交付。 |
   | 安全預覽伺服器 | 用於指定安全格式副本預覽伺服器的URL路徑。 即，在生成格式副本後，Experience Manageras a Cloud Service可以安全訪問和預覽遠程Dynamic Media格式副本(不會將二進位檔案發回Experience Manageras a Cloud Service實例)。<br>除非您有使用自己公司伺服器或特殊伺服器的特殊安排，否則Adobe建議您保留指定的此設定。 |
   | 同步處理所有內容 | 預設選擇。 如果要有選擇地包括或排除同步到Dynamic Media的資產，請取消選擇此選項。 取消選擇此選項允許您從以下兩種Dynamic Media同步模式中進行選擇：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 預設啟用&#x200B;]**— 預設情況下，該配置將應用於所有資料夾，除非您專門將資料夾標籤為排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 預設禁用]**  — 在明確標籤要同步到Dynamic Media的選定資料夾之前，不會將配置應用於任何資料夾。<br>要將所選資料夾標籤為同步到Dynamic Media，請選擇資產資料夾，然後在工具欄中選擇 **[!UICONTROL 屬性]**。 在 **[!UICONTROL 詳細資訊]** 的 **[!UICONTROL Dynamic Media同步模式]** 下拉清單中，從以下三個選項中選擇。 完成後，選擇 **[!UICONTROL 保存]**。 *記住：如果您選擇了&#x200B;**同步所有內容**早些。* 另請參閱 [在Dynamic Media的資料夾級別使用「選擇性發佈」](/help/assets/dynamic-media/selective-publishing.md)。<br>**[!UICONTROL 繼承&#x200B;]**— 資料夾上沒有顯式同步值。 相反，該資料夾會從其上級資料夾或雲配置中的預設模式繼承同步值。 通過工具提示顯示繼承的詳細狀態。<br>**[!UICONTROL 啟用子資料夾]**  — 包括此子樹中的所有內容以同步到Dynamic Media。 特定於資料夾的設定會覆蓋雲配置中的預設模式。<br>**[!UICONTROL 已禁用子資料夾&#x200B;]**— 從同步到Dynamic Media中排除此子樹中的所有內容。 |

   >[!NOTE]
   >
   >動態媒體中不支援版本修訂。此外，僅當 **[!UICONTROL 發佈資產]** 在「編輯Dynamic Media配置」頁中，設定為 **[!UICONTROL 激活後]**。然後，直到第一次激活資產。
   >
   >
   >激活資產後，任何更新都會立即即時發佈到S7交付。

   ![動態媒體配置更新](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 選擇 **[!UICONTROL 保存]**。 新Dynamic Media密碼和配置已保存。 如果已選擇 **[!UICONTROL 取消]** 而不會進行密碼更新。
1. 在 **[!UICONTROL 配置Dynamic Media]** 對話框，選擇 **[!UICONTROL 確定]** 開始配置。

   >[!IMPORTANT]
   >
   >當新Dynamic Media配置完成其設定時，您將在Experience Manageras a Cloud Service的「收件箱」中收到狀態通知。
   >
   >如果配置成功或未成功，此收件箱通知將通知您。
   > 請參閱 [排除新Dynamic Media配置的故障](#troubleshoot-dm-config) 和 [收件箱](/help/sites-cloud/authoring/getting-started/inbox.md) 的子菜單。

1. 要在發佈Dynamic Media內容之前安全地預覽它，Experience Manageras a Cloud Service使用基於令牌的驗證，因此，Experience Manager作者預設會預覽Dynamic Media內容。 但是， *允許清單* 更多IP，讓用戶能夠安全地預覽內容。 要在Experience Manageras a Cloud Service中設定此操作，請參閱 [配置Dynamic Media映像伺服器的發佈設定 — 安全頁籤](/help/assets/dynamic-media/dm-publish-settings.md#security-tab)。 <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

現在您完成了基本配置；你準備好用Dynamic Media了。

如果要進一步自定義配置，您可以選擇完成以下任務 [在Dynamic Media配置高級設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)。

### 排除新Dynamic Media配置的故障 {#troubleshoot-dm-config}

當新Dynamic Media配置完成其設定時，您將在Experience Manageras a Cloud Service的「收件箱」中收到狀態通知。 如「收件箱」下列相應映像中所示，此通知將通知您配置是否成功。

![Experience Manager收件箱成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件箱失敗](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另請參閱 [收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

**要排除新Dynamic Media配置的故障：**

1. 在Experience Manageras a Cloud Service頁的右上角，選擇鈴表徵圖，然後選擇 **[!UICONTROL 全部查看]**。
1. 在「收件箱」頁面上，選擇成功通知以讀取配置狀態和日誌的概述。

   如果配置失敗，請選擇與以下螢幕快照類似的失敗通知。

   ![Dynamic Media安裝失敗](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在 **[!UICONTROL DMSETUP]** 頁，查看描述故障的配置詳細資訊。 特別要注意任何錯誤消息或錯誤代碼。 與Adobe客戶支援部門聯繫以瞭解此資訊。

   ![Dynamic Media設定頁](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 將密碼更改為Dynamic Media {#change-dm-password}

在Dynamic Media，密碼過期時間設定為自當前系統日期起100年。

密碼必須至少包含下列各項之一：

* 大寫字母
* 小寫字母
* 數量
* 特殊字元： `# $ & . - _ : { }`

如有必要，您可以通過選擇密碼眼表徵圖來顯示密碼來檢查鍵入或重新鍵入的密碼的拼寫。 再次選擇該表徵圖以隱藏密碼。

選擇時，將保存更改的密碼 **[!UICONTROL 保存]** 右上角 **[!UICONTROL 編輯Dynamic Media配置]** 的子菜單。

1. 在Experience Manageras a Cloud Service中，選擇Experience Manageras a Cloud Service徽標以訪問全局導航控制台。
1. 在控制台左側，選擇「工具」表徵圖，然後轉到 **[!UICONTROL Cloud Services>Dynamic Media配置]**。
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，選擇 **[!UICONTROL 全球]**。 不選擇資料夾表徵圖 **[!UICONTROL 全球]**。 然後，選擇 **[!UICONTROL 編輯]**。
1. 在 **[!UICONTROL 編輯Dynamic Media配置]** 頁，位於 **[!UICONTROL 密碼]** 欄位，選擇 **[!UICONTROL 更改密碼]**。
1. 在 **[!UICONTROL 更改密碼]** 對話框，執行以下操作：

   * 在 **[!UICONTROL 新密碼]** 的子菜單。

      的 **[!UICONTROL 當前密碼]** 欄位被有意預先填充，並且隱藏在交互中。

   * 在 **[!UICONTROL 重複密碼]** ，重新鍵入新密碼，然後選擇 **[!UICONTROL 完成]**。

1. 在右上角 **[!UICONTROL 編輯Dynamic Media配置]** ，選擇 **[!UICONTROL 保存]**，然後選擇 **[!UICONTROL 確定]**。

## （可選）在Dynamic Media配置高級設定{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

要進一步自定義Dynamic Media的配置和設定，或優化其效能，可以完成以下一個或多個操作 *可選* 任務：

* [（可選）Dynamic Media設定的設定和配置](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（可選）調整Dynamic Media的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （可選）Dynamic Media設定的設定和配置 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic用戶介面更改您的Dynamic Media設定。

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

安裝和配置任務包括：

* [為映像伺服器配置Dynamic Media發佈設定](#publishing-setup-for-image-server)
* [配置Dynamic Media常規設定](#configuring-application-general-settings)
* [配置顏色管理](#configuring-color-management)
* [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)
* [為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)

<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 為映像伺服器配置Dynamic Media發佈設定 {#publishing-setup-for-image-server}

「Dynamic Media發佈設定」頁建立預設設定，確定如何將資產從AdobeDynamic Media伺服器傳送到網站或應用程式。

請參閱 [為映像伺服器配置Dynamic Media發佈設定](/help/assets/dynamic-media/dm-publish-settings.md)。

#### 配置Dynamic Media常規設定 {#configuring-application-general-settings}

配置Dynamic Media **[!UICONTROL 發佈伺服器名稱]** URL和 **[!UICONTROL 源伺服器名稱]** URL。 也可以指定 **[!UICONTROL 上載到應用程式]** 設定和 **[!UICONTROL 預設上載選項]** 都取決於您的特定用例。

請參閱 [配置Dynamic Media常規設定](/help/assets/dynamic-media/dm-general-settings.md)。

#### 配置顏色管理 {#configuring-color-management}

Dynamic Media色彩管理允許您對正確的資產進行色彩調整。 通過顏色校正，攝取的資產保留其顏色空間(RGB、CMYK、灰色)和嵌入的顏色配置檔案。 請求動態格式副本時，影像顏色將使用CMYK、RGB或「灰色」輸出更正為目標顏色空間。

請參閱 [配置影像預設](/help/assets/dynamic-media/managing-image-presets.md)。

要配置預設顏色屬性以在請求影像時啟用顏色校正：

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後使用設定期間提供的憑據登錄帳戶。
1. 轉到 **[!UICONTROL 設定>應用程式設定]**。
1. 展開「發 **[!UICONTROL 布設定]** 」區域並選 **[!UICONTROL 取「影像伺服器」]**。設定發 **[!UICONTROL 布例項的預設值]** ，將「發佈內容」設 **** 定為「影像伺服」。
1. 滾動到必須更改的屬性，例如， **[!UICONTROL 顏色管理屬性]** 的子菜單。
可以設定以下顏色校正屬性：

   | 屬性 | 說明 |
   |---|---|
   | CMYK預設顏色空間 | 預設CMYK顏色配置檔案的名稱。 |
   | 灰度預設顏色空間 | 預設灰色配置檔案的名稱。 |
   | RGB預設顏色空間 | 預設RGB顏色配置檔案的名稱。 |
   | 色彩轉換色彩演算比對方式 | 指定渲染方法。 可接受值為： **[!UICONTROL 知覺]**。 **[!UICONTROL 相對測量]**。 **[!UICONTROL 飽和]**。 **[!UICONTROL 絕對大氣]**。 Adobe建議 **[!UICONTROL 相對]** 。 |

1. 選擇 **[!UICONTROL 保存]**。

例如，您可以將「 **[!UICONTROL RGB預設顏色空間]** 」設 *為sRGB*，將「 **[!UICONTROL CMYK預設顏色空間」設為]**** WebCobatedCholor。

這樣做將執行以下操作：

* 啟用RGB和CMYK影像的顏色校正。
* RGB影像沒有顏色配置檔案，則假定該影像位於 *sRGB* 顏色空間。
* 假定沒有顏色配置檔案的CMYK影像在 *塗層網* 顏色空間。
* 返回RGB輸出的動態格式副本，在 *sRGB* 顏色空間。
* 返回CMYK輸出的動態格式副本，在 *塗層網* 顏色空間。

#### 編輯支援格式的MIME類型 {#editing-mime-types-for-supported-formats}

您可以定義由Dynamic Media處理的資產類型，並自定義高級資產處理參數。 例如，您可以指定資產處理參數以執行以下操作：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop文檔(.PSD)轉換為橫幅模板資產以進行個性化。
* 柵格化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視頻配置檔案](/help/assets/dynamic-media/video-profiles.md) 和 [影像配置檔案](/help/assets/dynamic-media/image-profiles.md) 可以分別定義視頻和影像的處理。

請參閱 [上載資產](/help/assets/add-assets.md)。

**要編輯支援格式的MIME類型：**

1. 在Experience Manageras a Cloud Service中，選擇Experience Manageras a Cloud Service徽標以訪問全局導航控制台，然後轉到 **[!UICONTROL 常規>CRXDE Lite]**。
1. 在左滑軌中，導航到以下位置：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME類型](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選擇MIME類型。
1. 在CRXDE Lite頁的右側，在下部：

   * 按兩下 **[!UICONTROL 啟用]** 的子菜單。 預設情況下，所有資產MIME類型都已啟用(設定為 **[!UICONTROL 真]**)，這意味著資產將同步到Dynamic Media以進行處理。 如果要排除此資產MIME類型，請將此設定更改為 **[!UICONTROL 假]**。

   * 按兩下 **[!UICONTROL jobParam]** 開啟其關聯的文本欄位。 請參閱 [支援的MIME類型](/help/assets/file-format-support.md) 可用於給定MIME類型的允許處理參數值清單。

1. 執行下列任一項作業：
   * 重複步驟3-4以編輯更多MIME類型。
   * 在CRXDE Lite頁的菜單欄上，選擇 **[!UICONTROL 全部保存]**。

1. 在頁面的左上角，選擇 **[!UICONTROL CRXDE Lite]** 回到Experience Manageras a Cloud Service。

#### 為不支援的格式添加MIME類型 {#adding-mime-types-for-unsupported-formats}

您可以為Experience Manager Assets不支援的格式添加自定義MIME類型。 要確保CRXDE Lite中添加的任何新節點不會被Experience Manager刪除，請在 `image_`。 另外，確保其啟用值設定為 **[!UICONTROL 假]**。

**要為不支援的格式添加MIME類型：**

1. 從Experience Manageras a Cloud Service，轉到 **[!UICONTROL 工具>操作> Web控制台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 將開啟新的瀏覽器頁籤 **[!UICONTROL Adobe Experience ManagerWeb控制台配置]** 的子菜單。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱的右側，點選「 **[!UICONTROL Edit the configuration values]** (pencil icon)(編輯配置值 (鉛筆圖示) 」。

   ![編輯配置值](assets/2019-08-02_16-44-56.png)

1. 在 **Adobe CQScene7資產MIME類型服務** 的上界。 在表中選擇加號以添加新MIME類型的位置很瑣碎。

   ![Adobe CQScene7資產MIME類型服務](assets/2019-08-02_16-27-27.png)

1. 類型 `DWG=image/vnd.dwg` 的子菜單。

   的 `DWG=image/vnd.dwg` MIME類型僅用於示例。 您在此處添加的MIME類型可以是任何其他不受支援的格式。

   ![添加DWGmime類型](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選擇 **[!UICONTROL 保存]**。

   此時，您可以關閉瀏覽器頁籤，該頁籤具有開啟的Adobe Experience ManagerWeb控制台配置頁。

1. 返回到具有開啟的Experience Manageras a Cloud Service控制台的瀏覽器頁籤。
1. 從Experience Manageras a Cloud Service，轉到 **[!UICONTROL 工具>常規>CRXDE Lite]**。

   ![工具>常規>CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. 在左滑軌中，導航到以下位置：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖動MIME類型 `image_vnd.dwg` 然後直接放在上面 `image_` 在樹中顯示，如下面的螢幕截圖所示。

   ![在CRXDE Lite中編輯DWG檔案](assets/crxdelite_cqdoc-14627.png)

1. 使用MIME類型 `image_vnd.dwg` 從 **[!UICONTROL 屬性]** 的 **[!UICONTROL 啟用]** 行，在 **[!UICONTROL 值]** 列標題，按兩下該值。 的 **[!UICONTROL 值]** 開啟下拉清單。
1. 類型 `false` 的 **[!UICONTROL 假]** )。

   ![編輯CRXDE Lite中的MIME類型](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁的左上角附近，選擇 **[!UICONTROL 全部保存]**。

### （可選）調整Dynamic Media的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了留住Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> 運行順利，Adobe建議以下同步效能/可擴充性微調提示：

* [更新預定義的作業參數以處理不同的檔案格式](#update-job-para)。
* [更新預定義的花崗岩工作流隊列（視頻資產）工作線程](#update-granite-workflow-queue-worker-threads-video)
* [更新預定義的花崗岩瞬態工作流隊列（影像和非視頻資產）工作線程](#update-granite-transient-workflow-queue-worker-threads-images)。
* [更新到Dynamic Media Classic(Scene7)伺服器的最大上載連接](#update-max-s7-upload-connections)。

#### 更新預定義的作業參數以處理不同的檔案格式 {#update-job-para}

您可以在上載檔案時調整作業參數以加快處理速度。 例如，如果上載PSD檔案，但不想將其作為模板處理，則可以將圖層提取設定為false(off)。 在這種情況下，調諧的作業參數如下所示： `process=None&createTemplate=false`。

如果確實要開啟模板建立，請使用以下參數： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議對PDF、PostScript®和PSD檔案使用以下「調諧」作業參數：

| 檔案類型 | 建議的作業參數 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新這些參數中的任何一個，請參見 [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)。

另請參閱 [添加不支援格式的MIME類型](#adding-mime-types-for-unsupported-formats)。

#### 更新預定義的花崗岩工作流隊列（視頻資產）工作線程 {#update-granite-workflow-queue-worker-threads-video}

花崗岩工作流隊列用於非暫態工作流。 在Dynamic Media，它用 **[!UICONTROL Dynamic Media編碼視頻]** 工作流。

**要更新預定義的花崗岩工作流隊列（視頻資產）工作線程：**

1. 導航到 `https://<server>/system/console/configMgr` 並搜索 **隊列：花崗岩工作流隊列**。

   >[!NOTE]
   >
   >由於OSGi PID是動態生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大並行作業數]** 欄位中，將編號更改為所需的值。

   預設情況下，最大並行作業數取決於可用CPU內核數。 例如，在4核伺服器上，它分配兩個工作線程。 （介於0.0和1.0之間的值基於比率，或者任何大於1的數字都分配工作線程數。）

   對於大多數使用情形，0.5預設設定就足夠了。

   ![作業處理隊列的配置](assets/chlimage_1-1.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

#### 更新預定義的花崗岩瞬態工作流隊列工作線程 {#update-granite-transient-workflow-queue-worker-threads-images}

花崗岩傳輸工作流隊列用於 **[!UICONTROL DAM更新資產]** 工作流。 在Dynamic Media，它用於影像和非視頻資產的接收和處理。

**要更新預定義的Granite Transient Workflow隊列工作線程，請執行以下操作：**

1. 導航到 **Adobe Experience ManagerWeb控制台配置** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **隊列：花崗岩瞬態工作流隊列**。

   >[!NOTE]
   >
   >由於OSGi PID是動態生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大並行作業數]** 欄位中，將編號更改為所需的值。

   你可以增加 **[!UICONTROL 最大並行作業數]** 足以支援大量檔案上傳到Dynamic Media。 具體值取決於硬體容量。 在某些情況下，如初始遷移或一次批量上載，您可以使用較大的值。 但請注意，使用大值（如內核數的兩倍）可能會對其他併發活動產生負面影響。 因此，根據您的特定使用情形test和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

#### 更新到Dynamic Media Classic(Scene7)伺服器的最大上載連接 {#update-max-s7-upload-connections}

Dynamic Media Classic(Scene7)上載連接設定將Experience Manager資產同步到Dynamic Media Classic伺服器。

**要更新到Dynamic Media Classic(Scene7)伺服器的最大上載連接：**

1. 導航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 連接數]** ，或 **[!UICONTROL 活動作業超時]** 欄位或兩者都可根據需要更改數字。

   的 **[!UICONTROL 連接數]** 設定控制允許Experience Manager到Dynamic Media上載的HTTP連接的最大數量。 通常，十個連接的預定義值就足夠了。

   的 **[!UICONTROL 活動作業超時]** 設定確定在傳遞伺服器中發佈上載的Dynamic Media資產的等待時間。 預設值為2100秒或35分鐘。

   對於大多數使用情形， 2100的設定已足夠。

   ![Adobe Scene7上傳服務](assets/chlimage_1-2.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
