---
title: 下載資產
description: Download assets from [!DNL Adobe Experience Manager Assets] and enable or disable the download functionality.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: cf6cfb38a43004c8ac0c1d1e99153335a47860a8
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 3%

---

# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

您可以下載資產，包括靜態和動態格式副本。 Alternatively, you can send emails with links to assets directly from [!DNL Adobe Experience Manager Assets]. 下載的資產捆綁在ZIP檔案中。 <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

無法下載資產類型映像集、旋轉集、混合媒體集和旋轉盤集。

可以使用以下方法下載Experience Manager資產：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager user interface](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 下載資產使用 [!DNL Experience Manager] 介面 {#download-assets}

非同步下載服務為大規模資產的無縫下載提供了一個框架。 下載存檔大於100GB大小，將其拆分為多個zip存檔，每個最大大小為100GB。 可以單獨下載。 Smaller files are downloaded from the user interface in real time. [!DNL Experience Manager] 不存檔下載原始檔案的單個資產下載。 此功能允許更快的下載。

預設情況下， [!DNL Experience Manager] 在下載工作流完成時觸發通知。 下載通知將出現在  [[!DNL Experience Manager] 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

![收件箱通知](assets/inbox-notification-for-large-downloads.png)


### 為大型下載啟用電子郵件通知 {#enable-emails-for-large-downloads}

在以下任何情況下，都會觸發非同步下載：

* 如果有10個以上的資產
* 如果下載大小超過100 MB
* 如果下載需要30秒以上的時間準備

當非同步下載在後端運行時，用戶可以繼續瀏覽並在Experience Manager中進一步工作。 在下載過程完成後，需要開箱即用機制通知用戶。 To achieve this objective, the administrators can configure email service by setting up an SMTP server. 請參閱 [配置郵件服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email)。

Once the email service is configured, the administrators and users can enable email notifications from the Experience Manager interface.

要啟用電子郵件通知：

1. 登錄到 [!DNL Experience Manager Assets]。
1. Click the user icon from the upper-right corner and then click **[!UICONTROL My Preferences]**. 將開啟「用戶首選項」窗口。
1. 選擇 **[!UICONTROL 資產下載電子郵件通知]** 複選框，然後按一下 **[!UICONTROL 接受]**。

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


要下載資產，請執行以下步驟：

1. 在 [!DNL Experience Manager] 用戶介面，按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 導航到要下載的資產。 選擇資料夾或在資料夾中選擇一個或多個資產。 在工具欄上，按一下 **[!UICONTROL 下載]**。

   ![從下載資產時可用的選項 [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. 在下載對話框中，選擇所需的下載選項。

   | 下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選擇此選項可將下載的每個資產包括在嵌套在資產父資料夾下的子資料夾中的資產包括在本地電腦上的一個資料夾中。 When this option is *not* select, by default, the folder hierarchy is ignored and all assets are downloaded into one folder in your local computer. |
   | **[!UICONTROL 電子郵件]** | 選擇此選項可向其他用戶發送電子郵件通知（包含到下載的連結）。 收件人用戶必須是 `dam-users` 組。 標準電子郵件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署過程中自定義的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>You can store tenant-specific custom templates at the following locations:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | Select this option to download the asset in its original form without any renditions.<br>如果原始資產具有子集，則子集選項可用。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產具有主要表示形式 — 上載檔案的主要表示形式。 他們可以有任意數目的表示。 <br> 通過此選項，您可以選擇要下載的格式副本。 可用的格式副本取決於您選擇的資產。 |
   | **[!UICONTROL 智慧裁切]** | Select this option to download all the smart crop renditions of the selected asset from within [!DNL Experience Manager]. 將建立帶有智慧裁剪格式副本的zip檔案並將其下載到您的本地電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選擇此選項可即時生成一系列替代格式副本。 When you select this option, you also select the renditions that you want to create dynamically by selecting from the [Image Preset](/help/assets/dynamic-media/image-presets.md) list. <br>此外，還可以選擇大小和測量單位、格式、顏色空間、解析度以及任何可選的影像修飾符（如反相影像）。 僅當您 [!DNL Dynamic Media] 啟用。 |

1. 在對話框中，按一下 **[!UICONTROL 下載]**。

   如果為大型下載啟用了電子郵件通知，則收件箱中會出現一封包含已存檔zip資料夾的下載URL的電子郵件。 Click on the download link from the email to download the zip folder.

   ![用於大下載的電子郵件通知](/help/assets/assets/email-for-large-notification.png)

   您還可以在 [!DNL Experience Manager] 收件箱。

   ![收件箱通知 — 用於大下載](/help/assets/assets/inbox-notification-for-large-downloads.png)

## 下載使用連結共用共用的資產 {#link-share-download}

Sharing assets using a link is a convenient way to make it available to interested people without them having to log in to [!DNL Assets]. 請參閱 [連結共用功能](/help/assets/share-assets.md#sharelink)。

當用戶從共用連結下載資產時， [!DNL Assets] 使用非同步服務，提供更快且不間斷的下載。 要下載的資產將在收件箱的後台排隊到可管理檔案大小的ZIP存檔中。 對於非常大的下載，下載內容會分組到大小為100 GB的檔案中。

的 [!UICONTROL 下載收件箱] 顯示每個存檔的處理狀態。 處理完成後，可以從收件箱下載存檔。

![下載收件箱](assets/link-sharing-download-inbox.png)

## Enable asset download servlet {#enable-asset-download-servlet}

中的預設servlet [!DNL Experience Manager] 允許經過身份驗證的用戶發出任意大的併發下載請求以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至會使伺服器和網路過載。 為了減輕這種功能所帶來的類似DoS的潛在風險， `AssetDownloadServlet` OSGi元件已禁用發佈實例。 If you do not need the download feature on author instances, disable the servlet on author.

要允許從DAM下載資產，例如，當使用諸如資產共用共用或其他類似門戶的實現時，請通過OSGi配置手動啟用servlet。 Adobe建議將允許的下載大小設定得盡可能低，而不影響日常下載要求。 高值可能會影響效能。

1. 建立具有針對發佈運行模式的命名約定的資料夾， `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在配置資料夾中，建立新類型的檔案 `nt:file` 命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Sets a maximum size (in bytes) for the download as value of `asset.download.prezip.maxcontentsize`. The below sample configures the maximum size of the ZIP download to not exceed 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用資產下載servlet {#disable-asset-download-servlet}

如果不需要下載功能，則禁用servlet以防止任何類似DoS的風險。 的 `Asset Download Servlet` 可在 [!DNL Experience Manager] 通過更新調度程式配置來阻止任何資產下載請求來建立和發佈實例。 也可以通過OSGi控制台直接手動禁用servlet。

1. 要通過調度程式配置阻止資產下載請求，請編輯 `dispatcher.any` 配置並向其中添加新規則 [過濾段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## 提示和限制 {#tips-limitations}

* 如果下載了空資料夾， [!DNL Experience Manager] 傳達了有關建立ZIP存檔的成功消息，但未建立存檔。

>[!MORELIKETHIS]
>
>* [下載受DRM保護的資產](drm.md)
>* [在Win或Mac案頭上使用Experience Manager案頭應用下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [使用受支援的Adobe Creative Cloud應用中的Adobe資產連結下載資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)

