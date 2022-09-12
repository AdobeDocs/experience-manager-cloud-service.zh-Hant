---
title: 下載資產
description: 從下載資產 [!DNL Adobe Experience Manager Assets] 和啟用或停用下載功能。
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 4f6901de479086ac40471885292ae82824516bd1
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 3%

---

# 從下載資產 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接從傳送包含資產連結的電子郵件 [!DNL Adobe Experience Manager Assets]. 下載的資產會以ZIP檔案整合。 <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

下列資產類型無法下載：影像集、回轉集、混合媒體集和轉盤集。

您可以使用下列方法從Experience Manager下載資產：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager使用者介面](#download-assets)
* [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用 [!DNL Experience Manager] 介面 {#download-assets}

Experience Manager會根據資產數量和大小來最佳化下載體驗。 從使用者介面即時下載較小的檔案。 [!DNL Experience Manager] 直接下載原始檔案的單一資產請求，而非將單一資產封裝在ZIP封存中，以加快下載速度。 Experience Manager支援使用非同步請求進行大量下載。 大於100 GB的下載請求會分割為多個ZIP封存檔，每個封存檔的大小上限為100 GB。

依預設， [!DNL Experience Manager] 會在 [[!DNL Experience Manager] 收件匣](/help/sites-cloud/authoring/getting-started/inbox.md) 產生下載封存時。

![收件匣通知](assets/inbox-notification-for-large-downloads.png)


### 啟用大量下載的電子郵件通知 {#enable-emails-for-large-downloads}

在下列任一情況下會觸發非同步下載：

* 如果超過10個資產
* 如果下載大小超過100 MB
* 如果下載需要超過30秒的時間來準備

雖然非同步下載會在後端執行，但使用者可以繼續探索，並在Experience Manager中進一步操作。 除了Experience Manager收件匣通知外，Experience Manager還可以在下載程式完成時傳送電子郵件通知使用者。 若要啟用此功能，管理員可依 [配置SMTP伺服器連接](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

設定電子郵件服務後，管理員和使用者就可以從Experience Manager介面啟用電子郵件通知。

若要啟用電子郵件通知：

1. 登入 [!DNL Experience Manager Assets].
1. 按一下右上角的使用者圖示，然後按一下 **[!UICONTROL 我的偏好設定]** 開啟「用戶首選項」窗口。
1. 選取 **[!UICONTROL 資產下載電子郵件通知]** 核取方塊和按一下 **[!UICONTROL 接受]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


若要下載資產，請依照下列步驟操作：

1. 在 [!DNL Experience Manager] 使用者介面，按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要下載的資產。 選取資料夾，或在資料夾內選取一或多個資產。 在工具列上，按一下 **[!UICONTROL 下載]**.

   ![從下載資產時的可用選項 [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. 在下載對話方塊中，選取您想要的下載選項。

   | 下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選取此選項，為每個包含資產所有已下載轉譯的資產建立資料夾。 如果未選取，每個資產(及其轉譯（若已選取以供下載）將包含在所產生封存的上層資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 選取此選項，將電子郵件通知（包含下載的連結）傳送給其他使用者。 收件者使用者必須是 `dam-users` 群組。 標準電子郵件範本位於下列位置：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署期間自定義的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在下列位置儲存租用戶專用的自訂範本：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取此選項即可下載原始格式的資產。<br>如果原始資產具有子資產，則會提供子資產選項。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產有主要表示法，即上傳之檔案的主要表示法。 它們可以有任意數量的表示。 <br> 使用此選項，您可以選取要下載的轉譯。 可用的轉譯取決於您選取的資產。 |
   | **[!UICONTROL 智慧裁切]** | 選取此選項，即可從內下載所選資產的所有智慧型裁切轉譯 [!DNL Experience Manager]. 會建立包含智慧型裁切轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項即時產生一系列替代轉譯。 選取此選項時，您也可以選取 [影像預設集](/help/assets/dynamic-media/image-presets.md) 清單。 <br>此外，您還可以選取尺寸和單位、格式、顏色空間、解析度，以及任何可選的影像修飾符，如反相影像。 只有在您有 [!DNL Dynamic Media] 已啟用。 |

1. 在對話方塊中，按一下 **[!UICONTROL 下載]**.

   如果為大量下載啟用電子郵件通知，則包含已封存zip資料夾下載URL的電子郵件會顯示在收件匣中。 按一下電子郵件中的下載連結以下載zip封存檔。

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   您也可以在 [!DNL Experience Manager] 收件匣。

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## 下載使用連結共用共用的資產 {#link-share-download}

使用連結共用資產是讓感興趣的人能夠直接使用的便利方式，而無須登入 [!DNL Assets]. 請參閱 [連結共用功能](/help/assets/share-assets.md#sharelink).

使用者從共用連結下載資產時， [!DNL Assets] 使用非同步服務，提供更快速且不間斷的下載。 要下載的資產會在收件匣的背景中排入佇列，並放入可管理檔案大小的ZIP封存檔中。 若是較大的下載量，下載會切分為100 GB的檔案。

此 [!UICONTROL 下載收件匣] 顯示每個封存的處理狀態。 處理完成後，您就可以從收件匣下載封存檔。

![下載收件匣](assets/link-sharing-download-inbox.png)

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設Servlet [!DNL Experience Manager] 可讓已驗證的使用者發出任意大型且同時下載的請求，以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至可能會使伺服器和網路過載。 為降低此功能造成的類似DoS的潛在風險， `AssetDownloadServlet` 發佈執行個體的OSGi元件已停用。 如果您不需要製作例項的下載功能，請停用製作上的servlet。

若要允許從DAM下載資產，例如使用資產共用公域或其他類似入口的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議盡可能低地設定允許的下載大小，而不影響日常下載需求。 高值可能會影響效能。

1. 建立資料夾，使用以發佈運行模式為目標的命名約定，即， `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在設定資料夾中，建立類型的新檔案 `nt:file` 已命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 填入 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 以下內容。 將下載的最大大小（以位元組為單位）設定為 `asset.download.prezip.maxcontentsize`. 以下範例會將ZIP下載的最大大小設定為不超過100 KB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

如果您不需要下載功能，請停用servlet以防止任何類似DoS的風險。 此 `Asset Download Servlet` 可在 [!DNL Experience Manager] 更新dispatcher設定以封鎖任何資產下載請求，以製作和發佈例項。 您也可以直接透過OSGi主控台手動停用servlet。

1. 若要透過Dispatcher設定來封鎖資產下載請求，請編輯 `dispatcher.any` 設定，並將新規則新增至 [篩選器區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## 提示和限制 {#tips-limitations}

* 如果下載空資料夾， [!DNL Experience Manager] 會傳達關於建立ZIP封存的成功訊息，但不會建立封存。

>[!MORELIKETHIS]
>
>* [下載受DRM保護的資產](drm.md)
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [從支援的Adobe Creative Cloud應用程式使用Adobe資產連結下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

