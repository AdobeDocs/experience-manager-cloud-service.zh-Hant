---
title: 設定 Dynamic Media Cloud Service
description: 瞭解如何將Adobe Experience Manager的Dynamic Media設為Cloud Service。
topic: 管理員
translation-type: tm+mt
source-git-commit: eb00eb6edaebc4dd0a16a99e1223bb806fa7abd9
workflow-type: tm+mt
source-wordcount: '4017'
ht-degree: 4%

---


# 關於配置Dynamic MediaCloud Service{#configuring-dynamic-media}

如果您將Adobe Experience Manager用於不同的環境（如開發、接移和即時生產），請為每個環境配置Dynamic MediaCloud Services。

## Dynamic Media建築圖{#architecture-diagram-of-dynamic-media}

以下架構圖說明Dynamic Media的運作方式。

有了新的架構，Experience Manager負責主要來源資產並與Dynamic Media同步處理及發佈資產：

1. 當主要來源資產作為Cloud Service上傳到Adobe Experience Manager時，它將複製到Dynamic Media。 此時，Dynamic Media會處理所有資產處理和轉譯產生，例如視訊編碼和影像的動態變體。
1. 產生轉譯後，Experience ManagerCloud Service可以安全地存取和預覽遠端Dynamic Media轉譯(不會以Cloud Service實例的形式將二進位檔案傳回Experience Manager)。
1. 在內容準備好發佈及核准後，它會觸發Dynamic Media服務將內容推送至傳送伺服器，並在CDN快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>下列功能清單要求您使用隨附於Adobe Experience Manager-Dynamic Media的現成可用CDN。 這些功能不支援任何其他自訂CDN。
>
>* [智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
>* [快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [熱連結保護](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2 內容傳送](/help/assets/dynamic-media/http2faq.md)
>* CDN層級的URL重新導向
>* Akamai ChinaCDN（在中國以最佳方式傳送）


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

## 在Cloud Services{#configuring-dynamic-media-cloud-services}中建立Dynamic Media配置

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manager為Cloud Service時，點選Experience Manager為Cloud Service標誌以存取全域導覽主控台。
1. 在控制台左側，點選「工具」圖示，然後點選「**[!UICONTROL Cloud Services>Dynamic Media組態]**」。
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，點選&#x200B;**[!UICONTROL global]**（請勿點選或選取&#x200B;**[!UICONTROL global]**&#x200B;左側的資料夾圖示）。 然後點選「**[!UICONTROL 建立]**」。
1. 在&#x200B;**[!UICONTROL 建立Dynamic Media組態]**&#x200B;頁面上，輸入標題、Dynamic Media帳戶電子郵件地址、密碼，然後選取您的地區。 此資訊是透過布建電子郵件中的Adobe提供給您。 如果您未收到此電子郵件，請聯絡Adobe客戶服務。
1. 按一下&#x200B;**[!UICONTROL 連接到Dynamic Media]**。
1. 在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框的&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中，輸入包含8-25個字元的新密碼。 密碼至少必須包含下列各項之一：

   * 大寫字母
   * 小寫字母
   * 數量
   * 特殊字元：`# $ & . - _ : { }`

   **[!UICONTROL 目前密碼]**&#x200B;欄位是有意預先填入並隱藏在互動中。

   如有必要，您可以點選密碼眼睛圖示以顯示密碼，以檢查您輸入或重新輸入的密碼的拼字。 再次點選圖示以隱藏密碼。

1. 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新輸入新密碼，然後點選&#x200B;**[!UICONTROL 完成。]**

   當您點選&#x200B;**[!UICONTROL 建立Dynamic Media組態]**&#x200B;頁面右上角的&#x200B;**[!UICONTROL Save]**&#x200B;時，會儲存新密碼。

   如果您在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框中點選了&#x200B;**[!UICONTROL 取消]**，則在保存新建立的Dynamic Media配置時仍必須輸入新密碼。

   另請參見[將密碼更改為Dynamic Media](#change-dm-password)。

1. 連接成功後，可以設定以下內容：

   | 屬性 | 說明 |
   |---|---|
   | 公司 | Dynamic Media帳戶的名稱。 您可能有多個Dynamic Media帳戶用於不同的子品牌、部門或階移／生產環境。 |
   | 公司根資料夾路徑 | 您公司的根資料夾路徑。 |
   | 發佈資產 | 您可以從下列三個選項中選擇：<br>**[!UICONTROL Immedialed ]**:上傳資產時，系統會收錄資產並立即提供URL/內嵌。 發佈資產不需要使用者干預。<br>**[!UICONTROL 啟動後]**:您必須先明確發佈資產，才能提供URL/內嵌連結。<br>**[!UICONTROL 選擇性發佈&#x200B;]**:資產會自動發佈，僅供安全預覽。也可以明確地以Cloud Service形式發佈到Experience Manager，而不發佈到DMS7，以便在公共域中發佈。 未來，這個選項打算以Cloud Service形式將資產發佈至Experience Manager，並將資產發佈至Dynamic Media，彼此排斥。 也就是說，您可以將資產發佈到DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您可以獨家以Experience Manager方式發佈資產做為預覽Cloud Service;這些相同的資產不會發佈在DMS7中，以便在公共域中交付。 |
   | 安全預覽伺服器 | 可讓您指定安全轉譯預覽伺服器的URL路徑。 也就是說，在產生轉譯後，Experience ManagerCloud Service可以安全地存取和預覽遠端Dynamic Media轉譯(沒有二進位檔會以Cloud Service例項傳回Experience Manager)。<br>除非您有特殊安排來使用您公司的伺服器或特殊伺服器，否則Adobe建議您依指定的方式保留此設定。 |
   | 同步處理所有內容 | 依預設選取。 如果您想要選擇性地包含或排除同步至Dynamic Media的資產，請取消選取此選項。 取消選擇此選項可讓您從以下兩種Dynamic Media同步模式中選擇：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 預設啟用&#x200B;]**:預設情況下，配置將應用於所有資料夾，除非您專門標籤要排除的資料夾。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 依預設停用]**:在您明確標籤要同步到Dynamic Media的選定資料夾之前，配置不會應用於任何資料夾。<br>若要將選取的檔案夾標示為同步至Dynamic Media，請選取資產檔案夾，然後在工具列中，點選「屬 **[!UICONTROL 性」]**。在&#x200B;**[!UICONTROL Details]**&#x200B;標籤的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉式清單中，從下列三個選項中選擇。 完成後，點選&#x200B;**[!UICONTROL Save]**。 *記住：如果您選取「同步所有內容工具」，這三個&#x200B;**選項將**無法使用。* 另請參 [閱Dynamic Media資料夾層級的「使用選擇性發佈」。](/help/assets/dynamic-media/selective-publishing.md)<br>**[!UICONTROL 繼承&#x200B;]**:資料夾上沒有明確的同步值。資料夾會從其上級資料夾或雲端設定的預設模式繼承同步值。 繼承的詳細狀態會透過工具提示顯示。<br>**[!UICONTROL 啟用子檔案夾]**:將所有內容包含在此子樹中，以便與Dynamic Media同步。資料夾特定的設定會覆寫雲端設定中的預設模式。<br>**[!UICONTROL 子檔案夾已停用&#x200B;]**:排除此子樹中的所有項目，以免與Dynamic Media同步。 |

   >[!NOTE]
   >
   >動態媒體中不支援版本修訂。此外，延遲啟動僅適用於在「編輯Dynamic Media設定」頁面中的「發佈資產」設為「啟動時」**[!UICONTROL 時。然後，直到第一次啟動資產為止。****]**
   >
   >
   >啟動資產後，任何更新都會立即即時發佈至S7傳送。

   ![dynamicmediaconfiguration2更新](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 點選&#x200B;**[!UICONTROL Save]**。 新的Dynamic Media密碼和配置將保存。 如果您改為點選&#x200B;**[!UICONTROL Cancel]**，則不會發生密碼更新。
1. 在&#x200B;**[!UICONTROL 配置Dynamic Media]**&#x200B;對話框中，按一下&#x200B;**[!UICONTROL 確定]**&#x200B;開始配置。

   >[!IMPORTANT]
   >
   >當新的Dynamic Media配置完成設定時，您將作為Cloud Service的收件箱在Experience Manager中收到狀態通知。
   >
   >此收件箱通知會通知您配置是否成功。
   > 如需詳細資訊，請參閱[疑難排解新的Dynamic Media配置](#troubleshoot-dm-config)和[您的收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

1. 若要在發佈前安全地預覽Dynamic Media內容，Experience Manager為Cloud Service預設會使用Token型驗證。 不過，您也可以「允許清單」更多IP，讓使用者存取安全地預覽內容。 若要設定此動作，請執行下列動作：<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * 開啟[Dynamic Media經典案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。 您的認證和登入詳細資訊是在布建時由Adobe提供。 如果您沒有此資訊，請聯絡Adobe客戶服務。
   * 在頁面右上角的導覽列上，點選「Setup **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**」。
   * 在「影像伺服器發佈」頁面的「發佈內容」下拉式清單中，選取「測試影像伺服」**[!UICONTROL 。****]**
   * 對於「Client Address Filter」（客戶端地址過濾器），請按一下「Add **[!UICONTROL （添加]**）」。
   * 要啟用（開啟）該地址，請選中該複選框，然後輸入Experience Manager作者實例的IP地址（而非Dispatcher IP）。
   * 按一下「**[!UICONTROL 儲存]**」。

您現在已完成基本配置；你準備好用Dynamic Media了。

如果要進一步自定義配置，您可以選擇在[「在Dynamic Media配置高級設定」下完成任何任務。](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)

### 診斷新的Dynamic Media配置{#troubleshoot-dm-config}

當新的Dynamic Media配置完成設定時，您將作為Cloud Service的收件箱在Experience Manager中收到狀態通知。 此通知會通知您配置是否成功，如下列收件箱中的相應影像所示。

![Experience Manager收件匣成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件匣失敗](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另請參閱[收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

**要診斷新的Dynamic Media配置故障**

1. 在Experience Manager的右上角附近，點選Cloud Service圖示，然後點選「View All」（檢視全部）]**。**[!UICONTROL 
1. 在「收件匣」頁面上，點選成功通知以讀取設定狀態和記錄檔的概述。

   如果設定失敗，請點選類似下列螢幕擷取的失敗通知。

   ![Dynamic Media設定失敗](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在&#x200B;**[!UICONTROL DMSETUP]**&#x200B;頁上，查看說明故障的配置詳細資訊。 尤其要注意任何錯誤資訊或錯誤代碼。 請聯絡Adobe客戶服務。

   ![Dynamic Media設定頁](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 將密碼更改為Dynamic Media{#change-dm-password}

Dynamic Media的密碼過期時間設為從當前系統日期開始100年。

密碼至少必須包含下列各項之一：

* 大寫字母
* 小寫字母
* 數量
* 特殊字元：`# $ & . - _ : { }`

如有必要，您可以點選密碼眼睛圖示以顯示密碼，以檢查您輸入或重新輸入的密碼的拼字。 再次點選圖示以隱藏密碼。

當您點選&#x200B;**[!UICONTROL 編輯Dynamic Media組態]**&#x200B;頁面右上角的&#x200B;**[!UICONTROL Save]**&#x200B;時，會儲存變更的密碼。

1. 在Experience Manager為Cloud Service時，點選Experience Manager為Cloud Service標誌以存取全域導覽主控台。
1. 在控制台左側，點選「工具」圖示，然後點選「**[!UICONTROL Cloud Services>Dynamic Media組態」。]**
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，按一下&#x200B;**[!UICONTROL global]**。請勿點選或選取&#x200B;**[!UICONTROL global]**&#x200B;左側的資料夾圖示。 然後，點選「**[!UICONTROL 編輯」。]**
1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media配置]**&#x200B;頁面的&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位正下方，按一下&#x200B;**[!UICONTROL 更改密碼。]**
1. 在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框中，執行以下操作：

   * 在&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中，輸入新密碼。

      **[!UICONTROL 目前密碼]**&#x200B;欄位是有意預先填入並隱藏在互動中。

   * 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新輸入新密碼，然後點選&#x200B;**[!UICONTROL 完成。]**

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media配置]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 保存]**，然後點選&#x200B;**[!UICONTROL 確定。]**

## （可選）在Dynamic Media配置高級設定{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

要進一步自定義Dynamic Media的配置和設定或優化其效能，可以完成以下一個或多個可選&#x200B;**&#x200B;任務：

* [Dynamic Media設定和配置](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（選用）調整Dynamic Media的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （可選）Dynamic Media設定的設定和配置{#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media經典用戶介面更改您的Dynamic Media設定。

上述部分任務要求您開啟[Dynamic MediaClassic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄您的帳戶。

設定和設定工作包括：

* [影像伺服器的發佈設定](#publishing-setup-for-image-server)
* [配置應用程式常規設定](#configuring-application-general-settings)
* [設定色彩管理](#configuring-color-management)
* [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)
* [為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 影像伺服器{#publishing-setup-for-image-server}的發佈設定

「發佈設定」設定會決定預設從Dynamic Media傳送資產的方式。 如果未指定任何設定，Dynamic Media會根據「發佈設定」中定義的預設設定傳送資產。 例如，傳送不含解析度屬性的影像請求，會產生具有預設物件解析度設定的影像。

若要設定發佈設定：在Dynamic MediaClassic中，按一下「設定」>「應用程式設定」>「發佈設定」>「影像伺服器」]**。**[!UICONTROL 

「影像伺服器」畫面會建立傳送影像的預設設定。 請參閱UI畫面，以取得每個設定的說明。

**[!UICONTROL 請求屬性]** -這些設定會限制從伺服器傳送的影像。**[!UICONTROL 預設請求屬性]** -這些設定屬於影像的預設外觀。**[!UICONTROL 常用縮圖屬性]** -這些設定屬於縮圖影像的預設外觀。**[!UICONTROL 目錄欄位的預設值]**-這些設定與影像的解析度和預設縮略圖類型相關。**[!UICONTROL 色彩管理屬性]** -這些設定會決定使用哪些ICC色彩描述檔。**[!UICONTROL 相容性屬性]** -此設定可讓文字圖層中的前導和尾隨段落視為3.6版中的段落，以提供回溯相容性。**[!UICONTROL 本地化支援]** -這些設定可讓您管理多個地區設定屬性。它也可讓您指定地區對應字串，以便定義您要在檢視器中支援哪些語言。 有關設定&#x200B;**[!UICONTROL 本地化支援]**&#x200B;的詳細資訊，請參閱[設定資產本地化時的注意事項](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets)。

#### 配置應用程式常規設定{#configuring-application-general-settings}

要開啟「應用程式常規設定」頁，請在「Dynamic Media經典全局導航」欄中按一下「設定」>「應用程式設定」>「常規設定」。]****[!UICONTROL 

**[!UICONTROL Servers]**  —— 在帳戶布建時，Dynamic Media會自動為您的公司提供指派的伺服器。這些伺服器可用來建構網站和應用程式的URL字串。 這些URL呼叫是您帳戶專屬的。 除非Experience Manager作為Cloud Service支援明確指示，否則不要更改任何伺服器名稱。
**[!UICONTROL 覆寫影像]** -Dynamic Media不允許兩個檔案具有相同名稱。每個項目的URL ID（檔案名稱減去副檔名）必須是唯一的。 這些選項指定如何上傳取代資產：不論是替換原稿還是變成重複。 重複資產會以&quot;-1&quot;（例如chair.tif會更名為chair-1.tif）重新命名。 這些選項會影響上傳至不同於原始檔案夾的資產，或具有不同於原始檔案副檔名的資產。
**[!UICONTROL 在目前資料夾中覆寫相同的基本影像名稱／副檔名]** -此選項是最嚴格的取代規則。它要求您將取代影像上傳至與原始影像相同的檔案夾，且檔案副檔名與原始影像相同。 如果未滿足這些要求，則會建立重複項。 要與Experience Manager保持一致性，請始終選擇&#x200B;**[!UICONTROL 在當前資料夾中覆蓋，相同的基本映像名／副檔名]**。
**[!UICONTROL 在任何資料夾中覆寫基本資產名稱／副檔名]** -需要取代的影像與原始影像具有相同的副檔名。例如，chair.jpg必須取代chair.jpg，而非chair.tif。 不過，您可以將取代影像上傳至原始檔案夾以外的其他檔案夾。 更新後的影像位於新資料夾中；在檔案的原始位置中無法再找到該檔案。
**[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱(不論副檔名為何]** )-此選項是最包含的取代規則。您可以將取代影像上傳至原始檔案夾以外的其他檔案夾、以不同的副檔名上傳檔案，以及取代原始檔案。 如果原始檔案位於不同的檔案夾中，則取代影像會位於上傳檔案的新檔案夾中。
**[!UICONTROL 預設色彩描述檔]** -如需詳細 [資訊，](#configuring-color-management) 請參閱設定色彩管理。依預設，當您選取「轉譯」時，系統會顯示15個轉譯，當您在資產的詳細資料檢視中選取「檢視器 ******** 」時，系統會顯示15個檢視器預設集。您可以提高此限制。請參 [閱增加或減少顯示的影像預設集數目](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) , [或增加或減少顯示的檢視器預設集數目](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)。

#### 配置色彩管理{#configuring-color-management}

Dynamic Media色彩管理可讓您為正確資產加上色彩。 透過色彩校正，收錄的資產會保留其色域（RGB、CMYK、灰色）和內嵌的色彩描述檔。 當您請求動態轉譯時，會使用CMYK、RGB或「灰色」輸出，將影像色彩校正為目標色域。 請參閱[設定影像預設集](/help/assets/dynamic-media/managing-image-presets.md)。

若要設定在請求影像時啟用色彩校正的預設色彩屬性：

1. 開啟[Dynamic Media經典案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後使用布建期間提供的認證登入您的帳戶。
1. 導覽至「**[!UICONTROL 設定>應用程式設定]**」。
1. 展開「發 **[!UICONTROL 布設定]** 」區域並選 **[!UICONTROL 取「影像伺服器」]**。設定發 **[!UICONTROL 布例項的預設值]** ，將「發佈內容」設 **** 定為「影像伺服」。
1. 捲動至您必須變更的屬性，例如&#x200B;**[!UICONTROL 色彩管理屬性]**區域中的屬性。
您可以設定下列色彩校正屬性：

   | 屬性 | 說明 |
   |---|---|
   | CMYK預設色域 | 預設CMYK色彩描述檔的名稱。 |
   | 灰階預設色域 | 預設灰色描述檔的名稱。 |
   | RGB預設色域 | 預設RGB顏色配置檔案的名稱。 |
   | 色彩轉換演算方式 | 指定渲染方式。 可接受的值為：**[!UICONTROL 感性]**、**[!UICONTROL 相對測冷]**、**[!UICONTROL 飽和]**、**[!UICONTROL 絕對測冷。]** Adobe建 **** 議相對於預設值。 |

1. 點選&#x200B;**[!UICONTROL Save]**。

例如，您可以將「 **[!UICONTROL RGB預設顏色空間]** 」設 *為sRGB*，將「 **[!UICONTROL CMYK預設顏色空間」設為]**** WebCobatedCholor。

這麼做會執行下列動作：

* 啟用RGB和CMYK影像的色彩校正。
* 沒有顏色描述檔的RGB影像假設在&#x200B;*sRGB*&#x200B;色域中。
* 沒有色彩描述檔的CMYK影像會假設在&#x200B;*WebCopated*&#x200B;色域中。
* 傳回RGB輸出的動態轉譯，在&#x200B;*sRGB*&#x200B;色域中傳回。
* 傳回CMYK輸出的動態轉譯，在&#x200B;*WebCopated*&#x200B;色域中傳回。

#### 編輯支援格式{#editing-mime-types-for-supported-formats}的MIME類型

您可以定義由Dynamic Media處理的資產類型，並自訂進階資產處理參數。 例如，您可以指定資產處理參數以執行下列動作：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop檔案(.PSD)轉換為橫幅範本資產，以利個人化。
* 柵格化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視訊](/help/assets/dynamic-media/video-profiles.md) 描述檔 [和影](/help/assets/dynamic-media/image-profiles.md) 像描述檔可分別用來定義視訊和影像的處理。

請參閱[上傳資產](/help/assets/add-assets.md)。

**要編輯支援格式的MIME類型**

1. 在Experience ManagerCloud Service中，按一下Experience Manager作為Cloud Service徽標以訪問全局導航控制台，然後按一下&#x200B;**[!UICONTROL 常規>CRXDE Lite]**。
1. 在左側導軌中，導覽至下列項目：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME類型](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選擇MIME類型。
1. 在CRXDE Lite頁面的右側，在下方：

   * 連按兩下&#x200B;**[!UICONTROL enabled]**&#x200B;欄位。 預設會啟用所有資產MIME類型（設為&#x200B;**[!UICONTROL true]**），這表示資產會同步至Dynamic Media以進行處理。 如果您想要排除此資產MIME類型，請將此設定變更為&#x200B;**[!UICONTROL false]**。

   * 連按兩下&#x200B;**[!UICONTROL jobParam]**&#x200B;以開啟其相關的文字欄位。 有關允許的處理參數值清單，請參見[支援的MIME類型](/help/assets/file-format-support.md)。

1. 執行下列任一項作業：
   * 重複步驟3-4以編輯更多MIME類型。
   * 在CRXDE Lite頁的菜單欄上，按一下「全部保存」。]****[!UICONTROL 

1. 在頁面的左上角，點選&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回Experience Manager作為Cloud Service。

#### 為不支援的格式添加MIME類型{#adding-mime-types-for-unsupported-formats}

您可以在「Experience Manager資產」中為不支援的格式新增自訂MIME類型。 要確保CRXDE Lite中添加的任何新節點不被Experience Manager刪除，請在`image_`之前移動MIME類型。 此外，請確定其啟用值設為&#x200B;**[!UICONTROL false]**。

**要為不支援的格式添加MIME類型**

1. 從Experience Manager作為Cloud Service，點選&#x200B;**[!UICONTROL 工具>操作> Web控制台。]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的瀏覽器頁籤開啟至&#x200B;**[!UICONTROL Adobe Experience ManagerWeb控制台配置]**&#x200B;頁。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱的右側，點選「 **[!UICONTROL Edit the configuration values]** (pencil icon)(編輯配置值 (鉛筆圖示) 」。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQScene7資產MIME類型服務**&#x200B;頁上，按一下任何加號表徵圖&lt;+>。 在表格中，您按一下加號以新增MIME類型的位置微不足道。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 在您剛新增的空白文字欄位中鍵入`DWG=image/vnd.dwg`。

   範例`DWG=image/vnd.dwg`僅供圖例之用。 您在此處添加的MIME類型可以是任何其他不支援的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，點選&#x200B;**[!UICONTROL Save]**。

   此時，您可以關閉具有開啟的「Adobe Experience ManagerWeb控制台配置」頁的瀏覽器頁籤。

1. 返回瀏覽器頁籤，該頁籤將開啟的Experience Manager作為Cloud Service控制台。
1. 從Experience Manager作為Cloud Service，點選&#x200B;**[!UICONTROL 工具>一般>CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左側導軌中，導覽至下列項目：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖曳MIME類型`image_vnd.dwg`，並直接放在樹狀結構中的`image_`上方，如下面的螢幕擷取所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤中，在&#x200B;**[!UICONTROL enabled]**&#x200B;列的&#x200B;**[!UICONTROL 值]**&#x200B;欄標題下，仍選取MIME類型`image_vnd.dwg`時，連按兩下值。 **[!UICONTROL Value]**&#x200B;下拉式清單隨即開啟。
1. 在欄位中鍵入`false`（或從下拉式清單中選取&#x200B;**[!UICONTROL false]**）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁的左上角附近，按一下「全部保存」。****



### （可選）調整Dynamic Media的效能{#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為使Dynamic Media<!--(with `dynamicmedia_scene7` run mode)-->正常運行，Adobe建議使用以下同步效能／可擴充性微調提示：

* 更新預定義的作業參數，以處理不同的檔案格式。
* 更新預先定義的Granite工作流程（視訊資產）佇列工作程式執行緒。
* 更新預先定義的Granite暫時工作流程（影像和非視訊資產）佇列工作線程。
* 更新到Dynamic Media經典伺服器的最大上載連接數。

#### 更新預定義的作業參數，以處理不同的檔案格式

您可以在上傳檔案時調整工作參數，以加快處理速度。 例如，如果您上傳PSD檔案，但不想以範本的形式處理，則可將圖層擷取設為false(off)。 在這種情況下，已調整的作業參數將顯示為`process=None&createTemplate=false`。

Adobe建議對PDF、PostScript®和PSD檔案使用下列「已調整」的工作參數：

| 檔案類型 | 建議的作業參數 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- To update any of these parameters, follow the steps in [Enabling MIME type-based Assets/Dynamic Media Classic upload job parameter support](#enabling-mime-type-based-assets-scene-upload-job-parameter-support). -->

#### 更新Granite Transient Workflow queue {#updating-the-granite-transient-workflow-queue}

「Granite傳輸工作流程」佇列用於&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。 在Dynamic Media，它用於影像攝取和處理。

**要更新Granite瞬態工作流隊列，請執行以下操作：**

1. 導覽至[https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr)並搜尋&#x200B;**佇列：Granite Transient Workflow Queue**。

   >[!NOTE]
   >
   >由於OSGi PID是動態產生的，所以必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業數]**&#x200B;欄位中，將數字更改為所需值。

   您可以增加&#x200B;**[!UICONTROL 最大並行作業數]**，以充分支援將檔案重量上傳到Dynamic Media。 確切值取決於硬體容量。 在某些情況下（例如初始移轉或一次性大量上傳），您可以使用較大的值。 但是，請注意，使用大值（如兩倍的內核數）可能會對其他併發活動產生負面影響。 因此，請根據您的特定使用案例來測試和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 點選&#x200B;**[!UICONTROL Save]**。

#### 更新Granite工作流隊列{#updating-the-granite-workflow-queue}

「Granite工作流程」佇列用於非暫時性工作流程。 在Dynamic Media，它使用&#x200B;**[!UICONTROL Dynamic Media編碼視訊工作流程來處理視訊。]**

要更新Granite工作流隊列，請執行以下操作：

1. 導覽至`https://<server>/system/console/configMgr`並搜尋&#x200B;**佇列：Granite Workflow Queue**。

   >[!NOTE]
   >
   >由於OSGi PID是動態產生的，所以必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業數]**&#x200B;欄位中，將數字更改為所需值。

   預設情況下，並行作業的最大數量取決於可用CPU內核的數量。 例如，在4核伺服器上，它分配兩個工作線程。 （0.0到1.0之間的值是基於比率的，或者任何大於1的數字都分配了工作線程數。）

   對於大多數使用案例，0.5預設設定已足夠。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 點選&#x200B;**[!UICONTROL Save]**。

#### 更新Scene7上載連接{#updating-the-scene-upload-connection}

「Scene7上傳連線」設定會同步Experience Manager資產至Dynamic Media經典伺服器。

要更新Scene7上載連接：

1. 導航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 連接數]**&#x200B;欄位或&#x200B;**[!UICONTROL 活動作業超時]**&#x200B;欄位中，或在兩者中，根據需要更改數字。

   **[!UICONTROL 連接數]**&#x200B;設定控制允許Experience Manager到Dynamic Media上載的HTTP連接數上限。 通常，十個連接的預定義值就足夠了。

   **[!UICONTROL 作用中工作逾時]**&#x200B;設定會決定已上傳Dynamic Media資產在傳送伺服器中發佈的等待時間。 此值預設為2100秒或35分鐘。

   對於大多數使用情況，2100的設定就足夠了。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 點選&#x200B;**[!UICONTROL 儲存。]**

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

1. In Experience Manager as a Cloud Service, tap the Experience Manager as a Cloud Service logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
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

