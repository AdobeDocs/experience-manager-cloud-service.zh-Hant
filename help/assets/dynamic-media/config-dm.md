---
title: 設定 Dynamic Media Cloud Service
description: 了解如何在Adobe Experience Manager中將Dynamic Media設為Cloud Service。
role: Administrator,Business Practitioner
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: c3e8be9809fd07dcc2186a898d9689ae5565620e
workflow-type: tm+mt
source-wordcount: '4057'
ht-degree: 3%

---

# 關於設定Dynamic MediaCloud Service {#configuring-dynamic-media}

如果您將Adobe Experience Manager用於不同環境（例如開發、測試和即時生產），請針對這些環境分別設定Dynamic MediaCloud Services。

## Dynamic Media架構圖 {#architecture-diagram-of-dynamic-media}

下列架構圖表說明Dynamic Media的運作方式。

透過新架構，Experience Manager負責主要來源資產，並與Dynamic Media同步處理及發佈資產：

1. 將主要來源資產上傳至Adobe Experience Manager作為Cloud Service時，會複製至Dynamic Media。 此時，Dynamic Media會處理所有資產處理和轉譯產生，例如影像的視訊編碼和動態變體。
1. 產生轉譯後，Experience Manager作為Cloud Service可以安全地存取和預覽遠端Dynamic Media轉譯(不會以Cloud Service例項的形式將二進位檔傳回Experience Manager)。
1. 內容準備好發佈及核准後，會觸發Dynamic Media服務推送內容至傳遞伺服器，並在CDN（內容傳遞網路）快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>下列功能清單需要您使用隨附於Adobe Experience Manager - Dynamic Media的現成可用CDN。 這些功能不支援任何其他自訂CDN。
>
>* [智慧型影像](/help/assets/dynamic-media/imaging-faq.md)
* [快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [熱連結保護](/help/assets/dynamic-media/hotlink-protection.md)
* [HTTP/2 內容傳送](/help/assets/dynamic-media/http2faq.md)
* CDN層級的URL重新導向
* Akamai ChinaCDN（以最佳方式在中國傳送）


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

## 在Cloud Services中建立Dynamic Media設定 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manager作為Cloud Service中，選取Experience Manager作為Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取「工具」圖示，然後前往&#x200B;**[!UICONTROL Cloud Services>Dynamic Media設定]**。
1. 在「Dynamic Media配置瀏覽器」頁的左窗格中，選擇&#x200B;**[!UICONTROL global]**（不要選擇&#x200B;**[!UICONTROL global]**&#x200B;左側的資料夾表徵圖）。 然後選擇&#x200B;**[!UICONTROL Create]**。
1. 在&#x200B;**[!UICONTROL 建立Dynamic Media設定]**&#x200B;頁面上，輸入標題、Dynamic Media帳戶電子郵件地址、密碼，然後選取您的地區。 此資訊是透過布建電子郵件中的Adobe提供給您的。 如果您未收到此電子郵件，請聯絡Adobe客戶服務。
1. 選擇&#x200B;**[!UICONTROL 連接到Dynamic Media]**。
1. 在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框的&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中，輸入包含8到25個字元的新密碼。 密碼必須至少包含以下各項之一：

   * 大寫字母
   * 小寫字母
   * 數量
   * 特殊字元：`# $ & . - _ : { }`

   **[!UICONTROL 當前密碼]**&#x200B;欄位有意預填和隱藏於交互中。

   如有必要，您可以通過選擇密碼眼表徵圖來顯示密碼來檢查您鍵入或重新鍵入的密碼的拼寫。 再次選擇表徵圖以隱藏密碼。

1. 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新鍵入新密碼，然後選擇&#x200B;**[!UICONTROL 完成]**。

   當您在&#x200B;**[!UICONTROL 建立Dynamic Media設定]**&#x200B;頁面的右上角選取&#x200B;**[!UICONTROL 儲存]**&#x200B;時，會儲存新密碼。

   如果您在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框中選擇了&#x200B;**[!UICONTROL 取消]**，則在保存新建立的Dynamic Media配置時仍必須輸入新密碼。

   另請參閱[將密碼更改為Dynamic Media](#change-dm-password)。

1. 連線成功時，您可以設定下列項目：

   | 屬性 | 說明 |
   |---|---|
   | 公司 | Dynamic Media帳戶的名稱。 您可能有多個Dynamic Media帳戶供不同的子品牌、部門或測試/生產環境使用。 |
   | 公司根資料夾路徑 | 您公司的根資料夾路徑。 |
   | 發佈資產 | 您可以從下列三個選項中選擇：<br>**[!UICONTROL 立即&#x200B;]**— 上傳資產時，系統會擷取資產並立即提供URL/內嵌。 發佈資產不需要使用者干預。<br>**[!UICONTROL 啟動時]**  — 您必須先明確發佈資產，才能提供URL/內嵌連結。<br>**[!UICONTROL 選擇性發佈&#x200B;]**— 資產會自動發佈，僅供安全預覽。也能以Cloud Service形式明確發佈至Experience Manager，而無須發佈至DMS7以在公共網域中傳遞。 未來，此選項會以Cloud Service的形式發佈資產至Experience Manager，並將資產發佈至Dynamic Media，彼此互斥。 也就是說，您可以將資產發佈至DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您可以只發佈Experience Manager中的資產，作為預覽的Cloud Service;這些相同資產不會發佈在DMS7中，以供在公共網域傳送。 |
   | 安全預覽伺服器 | 可讓您指定安全轉譯預覽伺服器的URL路徑。 也就是說，產生轉譯後，Experience Manager作為Cloud Service可以安全地存取和預覽遠端Dynamic Media轉譯(不會以Cloud Service例項的形式將二進位檔傳回Experience Manager)。<br>除非您有使用自己公司的伺服器或特殊伺服器的特殊安排，否則Adobe建議您保留此設定的指定。 |
   | 同步處理所有內容 | 預設為選取。 如果您想要選擇性地包含或排除從同步至Dynamic Media的資產，請取消選取此選項。 取消選取此選項可讓您從下列兩個Dynamic Media同步模式中選擇：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 預設啟用&#x200B;]**— 預設會將設定套用至所有資料夾，除非您特別標示要排除的資料夾。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 預設為停用]**  — 在您明確標示選取的資料夾以同步至Dynamic Media之前，不會將設定套用至任何資料夾。<br>若要將選取的資料夾標示為同步至Dynamic Media，請選取資產資料夾，然後在工具列中選取「屬 **[!UICONTROL 性」]**。在&#x200B;**[!UICONTROL Details]**&#x200B;頁簽的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉清單中，從以下三個選項中選擇。 完成後，選擇&#x200B;**[!UICONTROL Save]**。 *記住：如果您選取「同步所有contentier」，則這三&#x200B;**個選項不**可用。* 另請參 [閱在Dynamic Media的資料夾層級使用選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。<br>**[!UICONTROL 繼承&#x200B;]**— 資料夾上沒有明確的同步值。相反，資料夾會繼承其上階資料夾中的一個同步值或雲配置中的預設模式。 繼承的詳細狀態會透過工具提示顯示。<br>**[!UICONTROL 啟用子資料夾]**  — 在此子樹狀結構中包含所有項目，以便同步至Dynamic Media。資料夾特定設定會覆寫雲端設定中的預設模式。<br>**[!UICONTROL 針對子資料夾停用&#x200B;]**— 排除此子樹狀結構中的所有項目，使其無法同步至Dynamic Media。 |

   >[!NOTE]
   動態媒體中不支援版本修訂。此外，延遲啟動僅適用於在「編輯Dynamic Media設定」頁面中的「發佈資產」設為「啟動時」**[!UICONTROL 「]**」時。然後，直到首次啟動資產為止。****
   啟動資產後，任何更新都會立即上線發佈至S7傳送。

   ![dynamicmediaconfiguration_updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 選擇&#x200B;**[!UICONTROL 保存]**。 新Dynamic Media密碼和設定已儲存。 如果選擇了&#x200B;**[!UICONTROL 取消]**，則不會更新密碼。
1. 在&#x200B;**[!UICONTROL 配置Dynamic Media]**&#x200B;對話框中，選擇&#x200B;**[!UICONTROL 確定]**&#x200B;以開始配置。

   >[!IMPORTANT]
   新Dynamic Media設定完成設定時，您會在Experience Manager內收到狀態通知，作為Cloud Service的收件匣。
   此收件匣通知會通知您設定是否成功。
如需詳細資訊，請參閱[疑難排解新的Dynamic Media設定](#troubleshoot-dm-config)和[您的收件匣](/help/sites-cloud/authoring/getting-started/inbox.md) 。

1. 若要在發佈Dynamic Media內容之前安全地預覽，Experience Manager為Cloud Service預設會使用Token式驗證。 不過，您也可以「允許清單」更多IP，讓使用者存取安全預覽內容。 若要設定此動作，請執行下列動作：<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。 配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請連絡Adobe客戶服務。
   * 在頁面右上角附近的導覽列中，前往&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**。
   * 在「影像伺服器發佈」頁面的「**[!UICONTROL 發佈內容]**」下拉式清單中，選取「測試影像伺服」**[!UICONTROL 。]**
   * 對於「客戶端地址」篩選器，請選擇&#x200B;**[!UICONTROL 添加]**。
   * 若要啟用（開啟）該位址，請選取核取方塊，然後輸入「Experience Manager製作」例項的IP位址（而非Dispatcher IP）。
   * 選擇&#x200B;**[!UICONTROL 保存]**。

您現在已完成基本設定；您已準備好使用Dynamic Media。

如果要進一步自訂配置，您可以選擇完成[在Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)中配置高級設定下的任何任務。

### 疑難排解新的Dynamic Media設定 {#troubleshoot-dm-config}

新Dynamic Media設定完成設定時，您會在Experience Manager內收到狀態通知，作為Cloud Service的收件匣。 如下列收件匣的個別影像所示，此通知會通知您設定是否成功。

![Experience Manager收件匣成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件匣失敗](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另請參閱[您的收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

**若要疑難排解新的Dynamic Media設定：**

1. 在Experience Manager的右上角附近作為Cloud Service頁，選擇鈴聲表徵圖，然後選擇&#x200B;**[!UICONTROL 查看全部]**。
1. 在「收件匣」頁面上，選取成功通知，以閱讀設定狀態和記錄的概觀。

   如果配置失敗，請選擇與以下螢幕截圖類似的失敗通知。

   ![Dynamic Media安裝失敗](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在&#x200B;**[!UICONTROL DMSETUP]**&#x200B;頁上，查看描述故障的配置詳細資訊。 請特別注意任何錯誤訊息或錯誤碼。 請聯絡Adobe客戶服務以取得此資訊。

   ![Dynamic Media設定頁面](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 變更Dynamic Media的密碼 {#change-dm-password}

Dynamic Media中的密碼過期時間會從目前系統日期開始設為100年。

密碼必須至少包含以下各項之一：

* 大寫字母
* 小寫字母
* 數量
* 特殊字元：`# $ & . - _ : { }`

如有必要，您可以通過選擇密碼眼表徵圖來顯示密碼來檢查您鍵入或重新鍵入的密碼的拼寫。 再次選擇表徵圖以隱藏密碼。

當您在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的右上角選取&#x200B;**[!UICONTROL 儲存]**&#x200B;時，會儲存已變更的密碼。

1. 在Experience Manager作為Cloud Service中，選取Experience Manager作為Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取「工具」圖示，然後前往&#x200B;**[!UICONTROL Cloud Services>Dynamic Media設定]**。
1. 在「 Dynamic Media Configuration Browser（配置瀏覽器）」頁的左窗格中，選擇&#x200B;**[!UICONTROL global]**。 請勿選取&#x200B;**[!UICONTROL global]**&#x200B;左側的資料夾圖示。 然後，選擇&#x200B;**[!UICONTROL Edit]**。
1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media配置]**&#x200B;頁面的&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位正下方，選擇&#x200B;**[!UICONTROL 更改密碼]**。
1. 在&#x200B;**[!UICONTROL 更改密碼]**&#x200B;對話框中，執行以下操作：

   * 在&#x200B;**[!UICONTROL 新密碼]**&#x200B;欄位中，輸入新密碼。

      **[!UICONTROL 當前密碼]**&#x200B;欄位有意預填和隱藏於交互中。

   * 在&#x200B;**[!UICONTROL 重複密碼]**&#x200B;欄位中，重新鍵入新密碼，然後選擇&#x200B;**[!UICONTROL 完成]**。

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media配置]**&#x200B;頁的右上角，選擇&#x200B;**[!UICONTROL 保存]**，然後選擇&#x200B;**[!UICONTROL 確定]**。

## （選用）在Dynamic Media中設定進階設定{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

若要進一步自訂Dynamic Media的設定和設定，或最佳化其效能，您可以完成下列一或多個&#x200B;*選用*&#x200B;工作：

* [Dynamic Media設定的設定與設定](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（選用）調整Dynamic Media的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （選用）Dynamic Media設定的設定和設定 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic使用者介面來變更Dynamic Media設定。

上述部分工作需要您開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

設定和設定任務包括：

* [影像伺服器的發佈設定](#publishing-setup-for-image-server)
* [配置應用程式一般設定](#configuring-application-general-settings)
* [配置顏色管理](#configuring-color-management)
* [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)
* [為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 影像伺服器的發佈設定 {#publishing-setup-for-image-server}

「發佈設定」設定決定預設如何從Dynamic Media傳送資產。 如果未指定任何設定，Dynamic Media會根據「發佈設定」中定義的預設設定來傳送資產。 例如，傳送不包含解析度屬性的影像請求，會產生具有預設物件解析度設定的影像。

若要設定發佈設定：在Dynamic Media Classic中，前往&#x200B;**[!UICONTROL 設定>應用程式設定>發佈設定>影像伺服器]**。

「影像伺服器」螢幕建立用於傳送影像的預設設定。 請參閱UI畫面，了解每個設定的說明。

**[!UICONTROL 請求屬性]**  — 這些設定會限制可從伺服器傳送的影像。**[!UICONTROL 預設請求屬性]**  — 這些設定屬於影像的預設外觀。**[!UICONTROL 常見縮圖屬性]**  — 這些設定與縮圖影像的預設外觀相關。**[!UICONTROL 目錄欄位的預設值]** — 這些設定與影像的解析度和預設縮圖類型相關。**[!UICONTROL 顏色管理屬性]**  — 這些設定將決定要使用的ICC顏色配置檔案。**[!UICONTROL 相容性屬性]**  — 此設定可讓文字層中的前導和尾隨段落，如同在3.6版中一樣處理，以提供回溯相容性。**[!UICONTROL 本地化支援]**  — 這些設定可讓您管理多個地區設定屬性。它也可讓您指定地區對應字串，以便定義要在檢視器中支援各種工具提示的語言。 有關設定&#x200B;**[!UICONTROL 本地化支援]**&#x200B;的詳細資訊，請參閱設定資產本地化時的注意事項[](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets)。

#### 配置應用程式一般設定 {#configuring-application-general-settings}

要開啟「應用程式一般設定」頁，請在Dynamic Media Classic全局導航欄中，轉至&#x200B;**[!UICONTROL 設定>應用程式設定>一般設定]**。

**[!UICONTROL 伺服器]**  — 在帳戶布建時，Dynamic Media會自動為您的公司提供指派的伺服器。這些伺服器可用來建構網站和應用程式的URL字串。 這些URL呼叫是您的帳戶專屬的。 除非Experience Manager作為Cloud Service支援明確指示，否則請勿更改任何伺服器名稱。
**[!UICONTROL 覆寫影像]**  - Dynamic Media不允許兩個檔案具有相同的名稱。每個項目的URL ID（檔案名稱減去副檔名）必須是唯一的。 這些選項指定如何上傳取代資產：無論是取代原始檔案還是變成重複檔案。 重複資產會以「–1」重新命名（例如chair.tif已重新命名為chair-1.tif）。 這些選項會影響上傳至不同於原始資料夾的資產，或副檔名與原始資料夾不同的資產。
**[!UICONTROL 在目前資料夾中覆寫，使用相同的基本影像名稱/擴充功能]**  — 此選項是最嚴格的取代規則。它要求您將取代影像上傳至與原始影像相同的資料夾，且副檔名與原始影像相同。 若不符合這些要求，則會建立重複項目。 若要與作為Cloud Service的Experience Manager保持一致，請始終選擇&#x200B;**[!UICONTROL 在當前資料夾中覆蓋，使用相同的基本映像名稱/擴展]**。
**[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱/副檔名]**  — 需要取代影像的副檔名與原始影像相同。例如，chair.jpg必須替換chair.jpg，而不是chair.tif。 不過，您可以將取代影像上傳至與原始影像不同的資料夾。 更新後的影像位於新資料夾中；在檔案的原始位置找不到該檔案。
**[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱(不論副檔名為何]** ) — 此選項是包含最多的取代規則。您可以將取代影像上傳至與原始檔案不同的資料夾、以不同副檔名上傳檔案，然後取代原始檔案。 如果原始檔案位於不同的資料夾中，則替換影像位於上載到的新資料夾中。
**[!UICONTROL 預設色彩描述檔]**  — 如需詳細 [資訊，](#configuring-color-management) 請參閱設定色彩管理。依預設，當您選取「轉譯」時，系統會顯示15個轉譯，當您在資產的詳細資料檢視中選取「檢視器 ******** 」時，系統會顯示15個檢視器預設集。您可以提高此限制。請參閱[增加或減少顯示](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)或[的影像預設集數目增加或減少顯示](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)的檢視器預設集數目。

#### 配置顏色管理 {#configuring-color-management}

Dynamic Media色彩管理可讓您為資產加上色彩校正。 透過色彩校正，擷取的資產可保留其色彩空間（RGB、CMYK、灰色）和內嵌的色彩描述檔。 當您請求動態轉譯時，會使用CMYK、RGB或灰色輸出將影像顏色校正到目標顏色空間。 請參閱[設定影像預設集](/help/assets/dynamic-media/managing-image-presets.md)。

要配置預設顏色屬性，以便在請求影像時啟用顏色校正：

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後使用布建期間提供的憑證登入您的帳戶。
1. 轉到&#x200B;**[!UICONTROL Setup > Application Setup]**。
1. 展開「發 **[!UICONTROL 布設定]** 」區域並選 **[!UICONTROL 取「影像伺服器」]**。設定發 **[!UICONTROL 布例項的預設值]** ，將「發佈內容」設 **** 定為「影像伺服」。
1. 捲動至您必須變更的屬性，例如&#x200B;**[!UICONTROL 色彩管理屬性]**區域中的屬性。
您可以設定下列顏色校正屬性：

   | 屬性 | 說明 |
   |---|---|
   | CMYK預設顏色空間 | 預設CMYK顏色配置檔案的名稱。 |
   | 灰階預設顏色空間 | 預設灰色配置檔案的名稱。 |
   | RGB預設顏色空間 | 預設RGB顏色配置檔案的名稱。 |
   | 色彩轉換演算方式 | 指定渲染目的。 可接受的值為：**[!UICONTROL 知覺]**,**[!UICONTROL 相對冷量]**,**[!UICONTROL 飽和度]**,**[!UICONTROL 絕對冷量]**。 Adobe建議預設值為&#x200B;**[!UICONTROL relative]**。 |

1. 選擇&#x200B;**[!UICONTROL 保存]**。

例如，您可以將「 **[!UICONTROL RGB預設顏色空間]** 」設 *為sRGB*，將「 **[!UICONTROL CMYK預設顏色空間」設為]**** WebCobatedCholor。

這麼做會執行下列動作：

* 啟用RGB和CMYK影像的顏色校正。
* 沒有顏色配置檔案的RGB影像假定位於&#x200B;*sRGB*&#x200B;顏色空間中。
* 假定沒有顏色輪廓的CMYK影像位於&#x200B;*WebCobated*&#x200B;顏色空間中。
* 傳回RGB輸出的動態轉譯，會在&#x200B;*sRGB*&#x200B;色域中傳回。
* 傳回CMYK輸出的動態轉譯，會在&#x200B;*WebCobated*&#x200B;色域中傳回。

#### 編輯支援格式的MIME類型 {#editing-mime-types-for-supported-formats}

您可以定義由Dynamic Media處理的資產類型，並自訂進階資產處理參數。 例如，您可以指定資產處理參數以執行下列動作：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop檔案(.PSD)轉換為橫幅範本資產，以便個人化。
* 柵格化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視訊](/help/assets/dynamic-media/video-profiles.md) 設定檔 [和](/help/assets/dynamic-media/image-profiles.md) 影像設定檔可分別用來定義視訊和影像的處理。

請參閱[上傳資產](/help/assets/add-assets.md)。

**要編輯支援格式的MIME類型，請執行以下操作：**

1. 在作為Experience Manager的Cloud Service中，選擇Experience Manager作為Cloud Service徽標以訪問全局導航控制台，然後轉至&#x200B;**[!UICONTROL 常規>CRXDE Lite]**。
1. 在左側邊欄中，導覽至下列項目：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME類型](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選擇MIME類型。
1. 在CRXDE Lite頁面的右側，下方：

   * 點選兩下&#x200B;**[!UICONTROL enabled]**&#x200B;欄位。 依預設，會啟用所有資產MIME類型（設為&#x200B;**[!UICONTROL true]**），這表示資產會同步至Dynamic Media以進行處理。 如果您想要排除此資產MIME類型，請將此設定變更為&#x200B;**[!UICONTROL false]**。

   * 點選兩下&#x200B;**[!UICONTROL jobParam]**&#x200B;以開啟其相關的文字欄位。 如需指定MIME類型可使用的允許處理參數值清單，請參閱[支援的MIME類型](/help/assets/file-format-support.md)。

1. 執行下列任一操作：
   * 重複步驟3-4以編輯更多MIME類型。
   * 在CRXDE Lite頁面的菜單欄上，選擇&#x200B;**[!UICONTROL 全部保存]**。

1. 在頁面的左上角，選取&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以Cloud Service形式返回Experience Manager。

#### 為不支援的格式添加MIME類型 {#adding-mime-types-for-unsupported-formats}

您可以針對Experience Manager資產中不支援的格式新增自訂MIME類型。 要確保CRXDE Lite中添加的任何新節點不會被Experience Manager刪除，請在`image_`之前移動MIME類型。 同時，請確定其啟用值設為&#x200B;**[!UICONTROL false]**。

**為不支援的格式添加MIME類型：**

1. 從Experience Manager作為Cloud Service，轉至&#x200B;**[!UICONTROL 工具>操作> Web Console]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的瀏覽器頁簽隨即開啟，顯示&#x200B;**[!UICONTROL Adobe Experience Manager Web Console Configuration]**&#x200B;頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱的右側，點選「 **[!UICONTROL Edit the configuration values]** (pencil icon)(編輯配置值 (鉛筆圖示) 」。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7資產MIME類型Service**&#x200B;頁面上，選取任何加號圖示&lt;+>。 表格中您選取加號以新增新MIME類型的位置很瑣碎。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 在您剛新增的空白文字欄位中輸入`DWG=image/vnd.dwg`。

   `DWG=image/vnd.dwg` MIME類型僅用於示例用途。 您在此處新增的MIME類型可能是任何其他不支援的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選擇&#x200B;**[!UICONTROL Save]**。

   此時，您可以關閉開啟「Adobe Experience Manager Web Console設定」頁面的瀏覽器標籤。

1. 返回瀏覽器標籤，該標籤將您開啟的Experience Manager作為Cloud Service控制台。
1. 從Experience Manager作為Cloud Service，轉至&#x200B;**[!UICONTROL 工具>一般>CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左側邊欄中，導覽至下列項目：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖動MIME類型`image_vnd.dwg`，並將其直接拖放到樹的`image_`上方，如下面螢幕截圖所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 在&#x200B;**[!UICONTROL Properties]**&#x200B;標籤中，在&#x200B;**[!UICONTROL enabled]**&#x200B;列的&#x200B;**[!UICONTROL Value]**&#x200B;列標題下，按兩下值，仍選取MIME類型`image_vnd.dwg`。 **[!UICONTROL Value]**&#x200B;下拉清單已開啟。
1. 在欄位中輸入`false`（或從下拉式清單中選取&#x200B;**[!UICONTROL false]**）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁面的左上角附近，選擇「**[!UICONTROL 全部保存]**」。



### （選用）調整Dynamic Media的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了讓Dynamic Media <!--(with `dynamicmedia_scene7` run mode)-->順利運行，Adobe建議使用下列同步效能/可擴充性微調提示：

* 更新預定義的作業參數，以處理不同的檔案格式。
* 更新預先定義的Granite工作流程（視訊資產）佇列背景工作執行緒。
* 更新預先定義的Granite暫時性工作流程（影像和非視訊資產）佇列背景工作執行緒。
* 更新最大上傳連線至Dynamic Media Classic伺服器。

#### 更新預定義的作業參數以處理不同的檔案格式

上傳檔案時，您可以調整工作參數以加快處理速度。 例如，如果上傳PSD檔案，但不想以模板形式處理這些檔案，則可以將圖層提取設定為false(off)。 在這種情況下，調整的作業參數如下所示：`process=None&createTemplate=false`。

如果您確實要開啟範本建立，請使用下列參數：`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議對PDF、PostScript®和PSD檔案使用以下「調整」作業參數：

| 檔案類型 | 建議的作業參數 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

若要更新任何這些參數，請參閱[編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)。

另請參閱[為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)。

#### 更新Granite暫時工作流程佇列 {#updating-the-granite-transient-workflow-queue}

「Granite傳輸工作流程」佇列用於&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。 在Dynamic Media中，它用於影像擷取和處理。

**若要更新Granite暫時工作流程佇列：**

1. 導航到[https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr)並搜索&#x200B;**隊列：Granite暫時工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態產生的，因此必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業]**&#x200B;欄位中，將數字更改為所需值。

   您可以增加&#x200B;**[!UICONTROL 最大並行作業數]**，以充分支援檔案的大量上傳至Dynamic Media。 確切值取決於硬體容量。 在某些情況下（例如初始移轉或一次性大量上傳），您可以使用大值。 但請注意，使用大值（如內核數的2倍）可能會對其他併發活動產生負面影響。 因此，請根據您的特定使用案例來測試和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流程佇列 {#updating-the-granite-workflow-queue}

Granite工作流程佇列用於非暫時性的工作流程。 在Dynamic Media中，它用於透過&#x200B;**[!UICONTROL Dynamic Media編碼視訊]**&#x200B;工作流程處理視訊。

**若要更新Granite工作流程佇列：**

1. 導覽至`https://<server>/system/console/configMgr`並搜尋&#x200B;**佇列：Granite工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態產生的，因此必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業]**&#x200B;欄位中，將數字更改為所需值。

   預設情況下，並行作業的最大數量取決於可用的CPU核心數。 例如，在4核伺服器上，它分配兩個工作線程。 （介於0.0和1.0之間的值是基於比率的，或者任何大於1的數字都分配工作線程數。）

   對於大多數使用案例，0.5的預設設定已足夠。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

#### 更新Scene7上傳連線 {#updating-the-scene-upload-connection}

Scene7上傳連線設定會將Experience Manager資產同步至Dynamic Media Classic伺服器。

**若要更新Scene7上傳連線：**

1. 導航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 連線數]**&#x200B;欄位或&#x200B;**[!UICONTROL 作用中作業逾時]**&#x200B;欄位或兩者中，視需要變更數字。

   **[!UICONTROL 連線數]**&#x200B;設定會控制Experience Manager上傳至Dynamic Media所允許的HTTP連線數量上限。 通常，十個連線的預先定義值就足夠了。

   **[!UICONTROL 作用中工作逾時]**&#x200B;設定決定上傳之Dynamic Media資產在傳送伺服器中發佈的等待時間。 預設情況下，此值為2100秒或35分鐘。

   對於大多數使用案例，2100的設定已足夠。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

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
