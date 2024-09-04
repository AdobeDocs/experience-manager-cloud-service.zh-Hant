---
title: 設定Dynamic MediaCloud Service
description: 瞭解如何在Adobe Experience Manager as a Cloud Service中設定Dynamic Media。
contentOwner: Rick Brough
feature: Configuration,Dynamic Media
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '3811'
ht-degree: 2%

---

# 關於設定Dynamic MediaCloud Service {#configuring-dynamic-media}

{{work-with-dynamic-media}}

如果您將Adobe Experience Manager用於不同的環境，例如開發、測試和即時生產，請為每個環境設定Dynamic MediaCloud Service。

另請參閱[設定Dynamic Media公司別名帳戶](/help/assets/dynamic-media/dm-alias-account.md)

## Dynamic Media的架構圖 {#architecture-diagram-of-dynamic-media}

下列架構圖說明Dynamic Media的運作方式。

透過新架構，Experience Manager負責主要來源資產，並與Dynamic Media同步，以處理及發佈資產：

1. 主要來源資產上傳至Adobe Experience Manager as a Cloud Service後，系統會將其復寫至Dynamic Media。 此時，Dynamic Media會處理所有資產處理和轉譯產生作業，例如影像的視訊編碼和動態變體。
1. 產生轉譯後，Experience Manager as a Cloud Service可以安全地存取和預覽遠端Dynamic Media轉譯(不會將二進位檔傳回Experience Manageras a Cloud Service執行個體)。
1. 內容準備好發佈並核准後，就會觸發Dynamic Media服務，將內容推送至傳遞伺服器，並在CDN （內容傳遞網路）快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>下列功能清單會要求您使用Adobe Experience Manager - Dynamic Media隨附的現成可用CDN。 這些功能不支援任何其他自訂CDN。
>
>* [智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
>* [快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [直接連結保護](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2內容傳遞](/help/assets/dynamic-media/http2faq.md)
>* cdn層級的URL重新導向
>* Akamai ChinaCDN （針對中國境內的最佳傳送方式）

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

## 在Cloud Service中建立Dynamic Media設定 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manageras a Cloud Service中，選取Experience Manageras a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取[工具]圖示，然後移至&#x200B;**[!UICONTROL Cloud Service> Dynamic Media設定]**。
1. 在「Dynamic Media設定瀏覽器」頁面的左側窗格中，選取「**[!UICONTROL 全域]**」 （請勿選取「**[!UICONTROL 全域]**」左側的資料夾圖示）。 然後選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立Dynamic Media設定]**&#x200B;頁面上，輸入Dynamic Media帳戶的公司管理員的標題、Dynamic Media帳戶電子郵件地址和密碼，然後選取您的地區。 這些資訊會透過在布建電子郵件中Adobe來提供給您。 如果您沒有收到此電子郵件，請聯絡Adobe客戶支援。
1. 選取&#x200B;**[!UICONTROL 連線至Dynamic Media]**。
1. 在&#x200B;**[!UICONTROL 變更密碼]**&#x200B;對話方塊的&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中，輸入包含8-25個字元的新密碼。 密碼至少必須包含下列其中一項：

   * 大寫字母
   * 小寫字母
   * 數字
   * 特殊字元： `# $ & . - _ : { }`

   **[!UICONTROL 目前密碼]**&#x200B;欄位是刻意預先填入且隱藏在互動中。

   如有必要，您可以選取密碼眼睛圖示來顯示密碼，以檢查您已輸入或重新輸入的密碼的拼字。 再次選取圖示以隱藏密碼。

1. 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新輸入新密碼，然後選取&#x200B;**[!UICONTROL 完成]**。

   當您在「**[!UICONTROL 建立Dynamic Media設定]**」頁面的右上角選取「**[!UICONTROL 儲存]**」時，新密碼便會儲存。

   如果您在&#x200B;**[!UICONTROL 變更密碼]**&#x200B;對話方塊中選取&#x200B;**[!UICONTROL 取消]**，則儲存已建立的Dynamic Media組態時，仍須輸入新密碼。

   另請參閱[變更Dynamic Media的密碼](#change-dm-password)。

1. 連線成功後，您可以設定下列專案：

   | 屬性 | 說明 |
   |---|---|
   | 公司 | Dynamic Media帳戶的名稱。<br>**重要**：Experience Manager的執行個體只支援Cloud Service中的一個Dynamic Media設定；請勿新增多個設定。 Experience Manager執行個體上的多個Dynamic Media設定是&#x200B;_不支援或Adobe建議的_。<!-- CQDOC-19579 and CQDOC-19612 --><br>另請參閱[設定Dynamic Media公司別名帳戶](/help/assets/dynamic-media/dm-alias-account.md)。 |
   | 公司根資料夾路徑 | 您公司的根資料夾路徑。 |
   | 發佈Assets | 您可以從下列三個選項中選擇：<br>**[!UICONTROL 立即&#x200B;]**— 上傳資產時，系統會內嵌資產並立即提供URL/內嵌。 發佈資產不需要使用者介入。<br>**[!UICONTROL 啟動時]** — 您必須先明確發佈資產，才能提供URL/內嵌連結。<br>**[!UICONTROL 選擇性Publish ]**- Assets會自動發佈，但僅供安全預覽。 它們也可以明確發佈到as a Cloud ServiceExperience Manager，而無需發佈到DMS7以供在公共域中傳送。 此選項未來會打算將資產發佈至Experience Manageras a Cloud Service，並將資產發佈至Dynamic Media，兩者會互斥。 也就是說，您可以將資產發佈至DMS7，以使用智慧型裁切或動態轉譯等功能。 或者，您可以僅以Experience Manageras a Cloud Service發佈資產以供預覽；這些相同的資產不會發佈在DMS7中以供在公共網域中傳送。 |
   | 安全預覽伺服器 | 可讓您指定安全轉譯預覽伺服器的URL路徑。 也就是說，產生轉譯後，Experience Manager as a Cloud Service就可安全地存取及預覽遠端Dynamic Media轉譯(不會將二進位檔傳回Experience Manageras a Cloud Service執行個體)。<br>除非您有特殊安排使用您自己公司的伺服器或特殊伺服器，否則Adobe建議您保留此設定為指定的設定。 |
   | 同步處理所有內容 | 預設為選取。 如果您想要選擇性地在同步至Dynamic Media時包含或排除資產，請取消選取此選項。 取消選取此選項可讓您從下列兩種Dynamic Media同步模式中選擇：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 預設啟用&#x200B;]**— 除非您特別將資料夾標籤為排除，否則此設定預設會套用至所有資料夾。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 預設為停用]** — 在您明確標示選取的資料夾以同步至Dynamic Media之前，此設定不會套用至任何資料夾。<br>若要將選取的資料夾標示為同步至Dynamic Media，請選取一個資產資料夾，然後在工具列中選取&#x200B;**[!UICONTROL 屬性]**。 在&#x200B;**[!UICONTROL 詳細資料]**&#x200B;標籤的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉式清單中，從下列三個選項中選擇。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。 _請記住：如果您先前選取了&#x200B;**同步所有內容**，則無法使用這三個選項。_&#x200B;另請參閱[在Dynamic Media的資料夾層級使用選擇性Publish](/help/assets/dynamic-media/selective-publishing.md)。<br>**[!UICONTROL 已繼承&#x200B;]**— 資料夾上沒有明確的同步值。 而是由資料夾從其中一個上階資料夾繼承同步值，或是從雲端設定中的預設模式繼承。 繼承的詳細狀態會透過工具提示顯示。<br>**[!UICONTROL 啟用子資料夾]** — 包含此子樹狀結構中的所有專案，以便同步至Dynamic Media。 資料夾特定的設定會覆寫雲端設定中的預設模式。<br>**[!UICONTROL 已停用子資料夾&#x200B;]**— 排除此子樹狀結構中所有要同步至Dynamic Media的內容。 |

   >[!NOTE]
   >
   >動態媒體中不支援版本修訂。此外，只有在「編輯Publish設定」頁面中的&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;設定為&#x200B;**[!UICONTROL 啟動時]**&#x200B;時，延遲啟動才適用。 然後，直到第一次啟動資產為止。
   >
   >
   >資產啟動後，所有更新都會立即上線發佈至S7傳送。

   ![dynamicmediaconfiguration2已更新](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**。新的Dynamic Media密碼和設定已儲存。 如果您選取&#x200B;**[!UICONTROL 取消]**，則不會更新密碼。
1. 在&#x200B;**[!UICONTROL 設定Dynamic Media]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 確定]**&#x200B;以開始設定。

   >[!IMPORTANT]
   >
   >新的Dynamic Media組態完成設定時，您會在Experience Manageras a Cloud Service收件匣內收到狀態通知。
   >
   >此收件匣通知會通知您設定是否成功。
   > 如需詳細資訊，請參閱[新Dynamic Media組態疑難排解](#troubleshoot-dm-config)和[您的收件匣](/help/sites-cloud/authoring/inbox.md)。

1. 為了在發佈Dynamic Media內容之前安全地預覽內容，Experience Manager as a Cloud Service會使用權杖型驗證，因此Experience Manager Author預設會預覽Dynamic Media內容。 不過，您可以&#x200B;*加入允許清單*&#x200B;更多IP，讓使用者存取安全地預覽內容。 若要在as a Cloud ServiceExperience Manager中設定此動作，請參閱[設定影像伺服器的Dynamic Media Publish設定 — 安全性索引標籤](/help/assets/dynamic-media/dm-publish-settings.md#security-tab)。<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

您現在已經完成基本設定；您已準備好使用Dynamic Media了。

如果您想進一步自訂設定，例如啟用ACL （存取控制清單）許可權，您可以選擇在Dynamic Media的[設定進階設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)下完成任何工作。

### 疑難排解新的Dynamic Media設定 {#troubleshoot-dm-config}

新的Dynamic Media組態完成設定時，您會在Experience Manageras a Cloud Service收件匣內收到狀態通知。 此通知會通知您組態是否成功，如下列收件匣中個別影像所示。

![Experience Manager收件匣成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件匣失敗](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另請參閱[您的收件匣](/help/sites-cloud/authoring/inbox.md)。

**若要疑難排解新的Dynamic Media組態：**

1. 在Experience Manageras a Cloud Service頁面的右上角附近，選取鈴鐺圖示，然後選取&#x200B;**[!UICONTROL 全部檢視]**。
1. 在收件匣頁面上，選取成功通知以讀取設定的狀態和記錄檔的概觀。

   如果設定失敗，請選取與下列熒幕擷圖類似的失敗通知。

   ![Dynamic Media安裝失敗](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在&#x200B;**[!UICONTROL DMSETUP]**&#x200B;頁面上，檢閱描述失敗的組態詳細資訊。 請特別記下任何錯誤訊息或錯誤代碼。 請連絡Adobe客戶支援，並提供這項資訊。

   ![Dynamic Media設定頁面](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 變更Dynamic Media的密碼 {#change-dm-password}

Dynamic Media中的密碼到期日設為目前系統日期起的100年。

密碼至少必須包含下列其中一項：

* 大寫字母
* 小寫字母
* 數字
* 特殊字元： `# $ & . - _ : { }`

如有必要，您可以選取密碼眼睛圖示來顯示密碼，以檢查您已輸入或重新輸入的密碼的拼字。 再次選取圖示以隱藏密碼。

當您在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的右上角選取「**[!UICONTROL 儲存]**」時，已變更的密碼便會儲存。

1. 在Experience Manageras a Cloud Service中，選取Experience Manageras a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取[工具]圖示，然後移至&#x200B;**[!UICONTROL Cloud Service> Dynamic Media設定]**。
1. 在[Dynamic Media設定瀏覽器]頁面的左窗格中，選取&#x200B;**[!UICONTROL 全域]**。 請勿選取&#x200B;**[!UICONTROL 全域]**&#x200B;左側的資料夾圖示。 然後，選取&#x200B;**[!UICONTROL 編輯]**。
1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media組態]**&#x200B;頁面的&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位正下方，選取&#x200B;**[!UICONTROL 變更密碼]**。
1. 在&#x200B;**[!UICONTROL 變更密碼]**&#x200B;對話方塊中，執行下列動作：

   * 在&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中輸入新密碼。

     **[!UICONTROL 目前密碼]**&#x200B;欄位是刻意預先填入且隱藏在互動中。

   * 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新輸入新密碼，然後選取&#x200B;**[!UICONTROL 完成]**。

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 確定]**。

## （可選）在Dynamic Media中設定進階設定{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

若要進一步自訂Dynamic Media的組態和設定，或最佳化其效能，您可以完成下列&#x200B;_選擇性_&#x200B;工作中的一或多個：

* [（選用）在Dynamic Media中啟用ACL許可權](#optional-enable-acl)
* [（可選） Dynamic Media設定的設定和組態](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（可選）調整Dynamic Media的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （選用）在Dynamic Media中啟用存取控制清單許可權 {#optional-enable-acl}

當您在AEM上執行Dynamic Media時，它目前會將`/is/image`個要求轉送至「安全預覽影像伺服」，而不檢查PlatformServerServlet上的ACL （存取控制清單）許可權。 但是，您可以&#x200B;_啟用_ ACL許可權。 這樣做會轉寄授權的`/is/image`要求。 如果使用者無權存取資產，則會顯示「403 — 禁止」錯誤。

**若要在Dynamic Media中啟用ACL許可權：**

1. 從Experience Manager，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的瀏覽器標籤會開啟&#x200B;**[!UICONTROL Adobe Experience Manager Web主控台組態]**&#x200B;頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，捲動至名稱&#x200B;_Adobe CQ Scene7 PlatformServer_。

1. 在名稱的右側，選取鉛筆圖示（**[!UICONTROL 編輯組態值]**）。

1. 在&#x200B;**com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name**&#x200B;頁面上，選取下列兩個設定的核取方塊：

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` — 啟用時，此設定會快取許可權結果兩分鐘（預設）以儲存。
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` — 啟用時，此設定會在使用者透過Dynamic Media影像伺服器預覽資產時，驗證使用者的存取權。

   ![在Dynamic Media - Scene7模式中啟用存取控制清單設定](/help/assets/dynamic-media/assets/acl.png)

1. 在頁面的右下角附近，選取&#x200B;**[!UICONTROL 儲存]**。

### （可選） Dynamic Media設定的設定和組態 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic使用者介面變更您的Dynamic Media設定。

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

設定和組態工作包括下列各項：

* [設定影像伺服器的Dynamic Media Publish設定](#publishing-setup-for-image-server)
* [配置Dynamic Media一般設定](#configuring-application-general-settings)
* [設定色彩管理](#configuring-color-management)
* [編輯支援格式的MIME型別](#editing-mime-types-for-supported-formats)
* [針對不支援的格式新增MIME型別](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 設定影像伺服器的Dynamic Media Publish設定 {#publishing-setup-for-image-server}

Dynamic Media Publish設定頁面會建立預設設定，用來決定如何從AdobeDynamic Media伺服器將資產傳送至網站或應用程式。

請參閱[設定影像伺服器的Dynamic Media Publish安裝程式](/help/assets/dynamic-media/dm-publish-settings.md)。

#### 配置Dynamic Media一般設定 {#configuring-application-general-settings}

設定Dynamic Media **[!UICONTROL Publish伺服器名稱]** URL和&#x200B;**[!UICONTROL 原始伺服器名稱]** URL。 您也可以指定&#x200B;**[!UICONTROL 上載至應用程式]**&#x200B;設定和&#x200B;**[!UICONTROL 預設上載選項]**，全部根據您的特定使用案例。

請參閱[設定Dynamic Media一般設定](/help/assets/dynamic-media/dm-general-settings.md)。

#### 設定色彩管理 {#configuring-color-management}

Dynamic Media色彩管理可讓您校正資產的色彩。 透過色彩校正，擷取的資產可保留其色域(RGB、CMYK、灰色)和內嵌色彩設定檔。 當您要求動態轉譯時，會使用CMYK、RGB或灰階輸出將影像顏色校正到目標色域。

請參閱[設定影像預設集](/help/assets/dynamic-media/managing-image-presets.md)。

若要設定預設色彩屬性，以便在要求影像時啟用色彩校正：

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後使用布建期間提供的認證登入您的帳戶。
1. 移至&#x200B;**[!UICONTROL 設定>應用程式設定]**。
1. 展開「發 **[!UICONTROL 布設定]** 」區域並選 **[!UICONTROL 取「影像伺服器」]**。設定發 **[!UICONTROL 布例項的預設值]** ，將「發佈內容」設 **** 定為「影像伺服」。
1. 捲動至您必須變更的屬性，例如&#x200B;**[!UICONTROL 色彩管理屬性]**區域中的屬性。
您可以設定下列色彩校正屬性：

   | 屬性 | 說明 |
   |---|---|
   | CMYK預設色域 | 預設CMYK色彩設定檔的名稱。 |
   | 灰階預設色域 | 預設灰階色彩設定檔的名稱。 |
   | RGB預設色域 | 預設RGB色彩設定檔的名稱。 |
   | 色彩轉換色彩演算比對方式 | 指定演算色彩比對方式。 可接受的值為： **[!UICONTROL 感應式]**、**[!UICONTROL 相對色度]**、**[!UICONTROL 飽和度]**、**[!UICONTROL 絕對色度]**。 Adobe建議使用&#x200B;**[!UICONTROL 相對]**&#x200B;作為預設值。 |

1. 選取「**[!UICONTROL 儲存]**」。

例如，您可以將「 **[!UICONTROL RGB預設顏色空間]** 」設 *為sRGB*，將「 **[!UICONTROL CMYK預設顏色空間」設為]**** WebCobatedCholor。

這麼做會執行下列動作：

* 啟用RGB和CMYK影像的色彩校正。
* 沒有色彩設定檔的RGB影像假設在&#x200B;*sRGB*&#x200B;色域中。
* 沒有色彩設定檔的CMYK影像被假設為&#x200B;*WebCoated*&#x200B;色域。
* 傳回RGB輸出的動態轉譯，以&#x200B;*sRGB*&#x200B;色域傳回。
* 傳回CMYK輸出的動態轉譯，在&#x200B;*WebCoated*&#x200B;色域中傳回。

#### 編輯支援格式的MIME型別 {#editing-mime-types-for-supported-formats}

您可以定義Dynamic Media要處理的資產型別，並自訂進階資產處理引數。 例如，您可以指定資產處理引數，以執行下列作業：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop檔案(.PSD)轉換為橫幅範本資產以進行個人化。
* 點陣化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視訊設定檔](/help/assets/dynamic-media/video-profiles.md)和[影像設定檔](/help/assets/dynamic-media/image-profiles.md)分別可用來定義視訊和影像的處理方式。

請參閱[上傳資產](/help/assets/add-assets.md)。

**若要編輯支援格式的MIME型別：**

1. 以產品管理員身分登入您的Experience Manageras a Cloud Service。
1. 在Experience Manageras a Cloud Service中，選取Experience Manageras a Cloud Service標誌以存取全域導覽主控台，然後前往&#x200B;**[!UICONTROL 一般>CRXDE Lite]**。

   如果您沒有CRXDE Lite的存取權，請參閱[使用CRXDE Lite](/help/implementing/developing/tools/crxde.md)。

1. 在左側邊欄中，導覽至下列專案：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME型別](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選取MIME型別。
1. 在CRXDE Lite頁面的右側，下半部：

   * 連按兩下&#x200B;**[!UICONTROL 已啟用]**&#x200B;欄位。 預設會啟用所有資產MIME型別（設為&#x200B;**[!UICONTROL true]**），這表示資產會同步至Dynamic Media進行處理。 如果您要排除此資產MIME型別而不進行處理，請將此設定變更為&#x200B;**[!UICONTROL false]**。

   * 連按兩下&#x200B;**[!UICONTROL jobParam]**&#x200B;以開啟其相關的文字欄位。 如需可用於指定MIME型別的允許處理引數值清單，請參閱[支援的MIME型別](/help/assets/file-format-support.md)。

1. 執行下列任一項作業：
   * 重複步驟3至4以編輯更多MIME型別。
   * 在CRXDE Lite頁面的功能表列上，選取&#x200B;**[!UICONTROL 全部儲存]**。

1. 在頁面的左上角，選取&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回Experience Manageras a Cloud Service。

#### 針對不支援的格式新增MIME型別 {#adding-mime-types-for-unsupported-formats}

您可以針對Experience Manager Assets中不支援的格式新增自訂MIME型別。 若要確保Experience Manager不會刪除您在CRXDE Lite中新增的任何新節點，請將MIME型別移動到`image_`之前。 另外，請確定它的啟用值設定為&#x200B;**[!UICONTROL false]**。

**若要針對不支援的格式新增MIME型別：**

1. 以產品管理員身分登入您的Experience Manageras a Cloud Service。
1. 從Experience Manageras a Cloud Service，移至&#x200B;**[!UICONTROL 工具>作業> Web主控台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的瀏覽器標籤會開啟&#x200B;**[!UICONTROL Adobe Experience Manager Web主控台組態]**&#x200B;頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱的右側，選取&#x200B;**[!UICONTROL 編輯組態值]** （鉛筆圖示）。

   ![編輯設定值](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7 Asset MIME型別服務**&#x200B;頁面上，選取任何加號圖示&lt;+>。 在表格中選取加號以新增新MIME型別的位置並不重要。

   ![Adobe CQ Scene7資產Mime型別服務](assets/2019-08-02_16-27-27.png)

1. 在您剛新增的空白文字欄位中輸入`DWG=image/vnd.dwg`。

   `DWG=image/vnd.dwg` MIME型別僅供範例使用。 您在此處新增的MIME型別可以是任何其他不支援的格式。

   ![正在新增DWG MIME型別](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選取&#x200B;**[!UICONTROL 儲存]**。

   此時，您可以關閉已開啟Adobe Experience Manager Web主控台設定頁面的瀏覽器索引標籤。

1. 返回含有已開啟Experience Manageras a Cloud Service主控台的瀏覽器標籤。
1. 從Experience Manageras a Cloud Service，移至&#x200B;**[!UICONTROL 工具>一般>CRXDE Lite]**。

   如果您沒有CRXDE Lite的存取權，請參閱[使用CRXDE Lite](/help/implementing/developing/tools/crxde.md)。

   ![工具>一般>CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. 在左側邊欄中，導覽至下列專案：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 將MIME型別`image_vnd.dwg`拖放到樹狀結構中`image_`的正上方，如下列熒幕擷圖所示。

   ![正在編輯CRXDE Lite](assets/crxdelite_cqdoc-14627.png)的DWG檔案

1. 在MIME型別`image_vnd.dwg`仍被選取的情況下，從&#x200B;**[!UICONTROL 屬性]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 已啟用]**&#x200B;列，在&#x200B;**[!UICONTROL 值]**&#x200B;欄標題下，雙選值。 **[!UICONTROL 值]**&#x200B;下拉式清單已開啟。
1. 在欄位中輸入`false` （或從下拉式清單中選取&#x200B;**[!UICONTROL false]**）。

   ![正在編輯CRXDE Lite](assets/2019-08-02_16-60-30.png)中的MIME型別

1. 在CRXDE Lite頁面的左上角附近，選取&#x200B;**[!UICONTROL 全部儲存]**。

### （可選）調整Dynamic Media的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了讓Dynamic Media <!--(with `dynamicmedia_scene7` run mode)-->能夠順暢地執行，Adobe建議下列同步處理效能/可擴充性微調秘訣：

* [更新預先定義的作業引數，以處理不同的檔案格式](#update-job-para)。
* [更新預先定義的Granite工作流程佇列（視訊資產）背景工作執行緒](#update-granite-workflow-queue-worker-threads-video)
* [更新預先定義的Granite暫時性工作流程佇列（影像和非視訊資產）工作者執行緒](#update-granite-transient-workflow-queue-worker-threads-images)。
* [更新與Dynamic Media Classic (Scene7)伺服器的最大上傳連線數](#update-max-s7-upload-connections)。

#### 更新預先定義的作業引數以處理不同的檔案格式 {#update-job-para}

您可以調整工作引數，以便在上傳檔案時更快地處理。 例如，如果您上傳PSD檔案，但不想將其當成範本處理，您可以將圖層提取設定為false （關閉）。 在這種情況下，調整的工作引數會顯示如下： `process=None&createTemplate=false`。

如果您確實要開啟範本建立，請使用下列引數： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議針對PDF、PostScript®和PSD檔案使用下列「調整」工作引數：

| 檔案型別 | 建議的工作引數 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

若要更新任何這些引數，請參閱[編輯支援格式的MIME型別](#editing-mime-types-for-supported-formats)。

另請參閱[新增不支援格式的MIME型別](#adding-mime-types-for-unsupported-formats)。

#### 更新預先定義的Granite工作流程佇列（視訊資產）背景工作執行緒 {#update-granite-workflow-queue-worker-threads-video}

Granite工作流程佇列用於非暫時性工作流程。 在Dynamic Media中，它以前是使用&#x200B;**[!UICONTROL Dynamic Media編碼視訊]**&#x200B;工作流程來處理視訊。

>[!NOTE]
>
>您必須以產品管理員的身分登入Experience Manager as a Cloud Service，才能完成此工作。

如果您沒有OSGi的存取權，請參閱[OSGi設定](/help/implementing/developing/components/overview.md#osgi-configuration)。

**若要更新預先定義的Granite工作流程佇列（視訊資產）背景工作執行緒：**

1. 瀏覽至`https://<server>/system/console/configMgr`並搜尋&#x200B;**佇列： Granite工作流程佇列**。

   >[!NOTE]
   >
   >必須進行文字搜尋，而非直接URL，因為OSGi PID是動態產生的。

1. 在&#x200B;**[!UICONTROL 最大平行工作]**&#x200B;欄位中，將數字變更為所要的值。

   根據預設，平行作業的最大數量取決於可用的CPU核心數量。 例如，在4核心伺服器上，它會指派兩個背景工作執行緒。 （介於0.0和1.0之間的值是以比率為基礎，或任何大於一的數字都會指定工作者執行緒的數量。）

   對於大多數使用案例，0.5的預設設定就足夠了。

   ![工作處理佇列的設定](assets/chlimage_1-1.jpeg)

1. 選取「**[!UICONTROL 儲存]**」。

#### 更新預先定義的Granite暫時工作流程佇列工作者執行緒 {#update-granite-transient-workflow-queue-worker-threads-images}

Granite傳輸工作流程佇列已用於&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。 在Dynamic Media中，它用於影像和非視訊資產的擷取與處理。

>[!NOTE]
>
>您必須以產品管理員的身分登入Experience Manager as a Cloud Service，才能完成此工作。

**若要更新預先定義的Granite暫時性工作流程佇列工作者執行緒：**

1. 瀏覽至`http://<host>:<port>/system/console/configMgr`的&#x200B;**Adobe Experience Manager Web Console設定**
1. 搜尋&#x200B;**佇列： Granite暫時性工作流程佇列**。

   >[!NOTE]
   >
   >必須進行文字搜尋，而非直接URL，因為OSGi PID是動態產生的。

1. 在&#x200B;**[!UICONTROL 最大平行工作]**&#x200B;欄位中，將數字變更為所要的值。

   您可以增加&#x200B;**[!UICONTROL 個最大平行工作]**，以充分支援將大量檔案上傳至Dynamic Media。 確切的值取決於硬體容量。 在某些情況下（例如初始移轉或一次性大量上傳），您可以使用大型值。 但是請注意，使用很大的數值（例如核心數的兩倍）可能會對其他並行活動產生負面影響。 因此，請根據您的特定使用案例來測試和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 選取「**[!UICONTROL 儲存]**」。

#### 更新與Dynamic Media Classic (Scene7)伺服器的最大上傳連線 {#update-max-s7-upload-connections}

Dynamic Media Classic (Scene7)上傳連線設定會將Experience Manager資產同步至Dynamic Media Classic伺服器。

>[!NOTE]
>
>您必須以產品管理員的身分登入Experience Manager as a Cloud Service，才能完成此工作。

**若要更新與Dynamic Media Classic (Scene7)伺服器的最大上傳連線數：**

1. 瀏覽至`https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 連線數目]**&#x200B;欄位或&#x200B;**[!UICONTROL 作用中作業逾時]**&#x200B;欄位中，或兩者中，視需要變更數目。

   **[!UICONTROL 連線數目]**&#x200B;設定會控制Experience Manager至Dynamic Media上傳所允許的最大HTTP連線數目。 通常預先定義的十個連線值就足夠了。

   **[!UICONTROL 作用中作業逾時]**&#x200B;設定會決定已上傳Dynamic Media資產在傳遞伺服器上發佈的等待時間。 此值預設為2100秒或35分鐘。

   對於大多數使用案例，設定2100已足夠。

   ![Adobe Scene7上傳服務](assets/chlimage_1-2.jpeg)

1. 選取「**[!UICONTROL 儲存]**」。

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
