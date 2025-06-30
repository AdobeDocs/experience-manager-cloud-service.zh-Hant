---
title: 下載資產
description: 從 [!DNL Adobe Experience Manager Assets] 下載資產，並啟用或停用下載功能。
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 4%

---

# 從[!DNL Adobe Experience Manager]下載資產 {#download-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

您可以下載資產，包括靜態和動態轉譯。 或者，您可以直接從[!DNL Adobe Experience Manager Assets]傳送包含資產連結的電子郵件。 下載的資產會整合在ZIP檔案中。<!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

無法下載下列資產型別：影像集、迴轉集、混合媒體集和轉盤集。

您可以使用下列方法，從Experience Manager下載資產：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager使用者介面](#download-assets)
* [資產共用公用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用[!DNL Experience Manager]介面下載資產 {#download-assets}

Experience Manager會根據資產數量和大小來最佳化下載體驗。 從使用者介面即時下載較小的檔案。 [!DNL Experience Manager]會直接下載原始檔案的單一資產請求，而非將單一資產封存在ZIP封存檔中，以加快下載速度。 Experience Manager支援大量非同步請求的下載。 大於100 GB的下載請求會分割為多個ZIP封存檔，每個封存檔的大小上限為100 MB。

根據預設，[!DNL Experience Manager]會在產生下載封存時在[[!DNL Experience Manager] 收件匣](/help/sites-cloud/authoring/inbox.md)中觸發通知。

![收件匣通知](assets/inbox-notification-for-large-downloads.png)


### 啟用大量下載的電子郵件通知 {#enable-emails-for-large-downloads}

非同步下載會在下列任一情況下觸發：

* 如果有十個以上的資產
* 如果下載大小超過100 MB
* 如果下載需要30秒以上的準備時間

雖然非同步下載會在後端執行，但使用者可以繼續探索，並在Experience Manager中進一步工作。 除了Experience Manager收件匣通知之外，Experience Manager還可以傳送電子郵件以在下載程式完成時通知使用者。 若要啟用此功能，系統管理員可以透過[設定SMTP伺服器連線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email)來設定電子郵件服務。

設定電子郵件服務後，管理員和使用者可以從Experience Manager介面啟用電子郵件通知。

若要啟用電子郵件通知：

1. 登入[!DNL Experience Manager Assets]。
1. 從右上角按一下使用者圖示，然後按一下&#x200B;**[!UICONTROL 我的偏好設定]**&#x200B;以開啟「使用者偏好設定」視窗。
1. 選取&#x200B;**[!UICONTROL 資產下載電子郵件通知]**&#x200B;核取方塊，然後按一下&#x200B;**[!UICONTROL 接受]**。

   ![啟用大型下載的電子郵件通知](/help/assets/assets/enable-email-for-large-downloads.png)


若要下載資產，請遵循下列步驟：

1. 在[!DNL Experience Manager]使用者介面中，按一下&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 導覽至您要下載的資產。 選取資料夾，或選取資料夾中一或多個資產。 在工具列上，按一下&#x200B;**[!UICONTROL 下載]**。

   從[!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)下載資產時有![可用選項

1. 在下載對話方塊中，選取您想要的下載選項。

   | 下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每個資產建立個別的資料夾]** | 選取此選項，為每個資產建立一個資料夾，其中包含資產的所有已下載轉譯。 如果取消選取，則每個資產（以及如果選取要下載的其轉譯）都會包含在所產生封存檔的父資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 選取此選項可將電子郵件通知（包含您下載的連結）傳送給其他使用者。 收件者使用者必須是`dam-users`群組的成員。 標準電子郵件範本可在下列位置取得：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您部署期間自訂的範本可在下列位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以將租使用者特定的自訂範本儲存在下列位置：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取此選項，即可以原始格式下載資產。<br>如果原始資產有子資產，則可以使用子資產選項。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。 Assets具有主要表示方式，即上傳檔案的主要表示方式。 它們可以有任意數量的表示。 <br>使用此選項，您可以選取要下載的轉譯。 可用的轉譯取決於您選取的資產。 |
   | **[!UICONTROL 智慧型裁切]** | 選取此選項即可從[!DNL Experience Manager]內下載所選資產的所有智慧型裁切轉譯。 已建立包含「智慧型裁切」轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項可即時產生一系列替代轉譯。 選取此選項時，您也可以從[影像預設集](/help/assets/dynamic-media/image-presets.md)清單中選取要動態建立的轉譯。 <br>此外，您可以選取大小與測量單位、格式、色域、解析度，以及任何選用的影像修飾元，例如反轉影像。 只有在您已啟用[!DNL Dynamic Media]時，才能使用此選項。 |

1. 在對話方塊中，按一下&#x200B;**[!UICONTROL 下載]**。

   如果大型下載已啟用電子郵件通知，則收件匣中會顯示包含封存zip資料夾之下載URL的電子郵件。 按一下電子郵件中的下載連結，以下載zip封存。

   ![大型下載的電子郵件通知](/help/assets/assets/email-for-large-notification.png)

   您也可以在[!DNL Experience Manager]收件匣中檢視通知。

   ![大型下載的收件匣通知](/help/assets/assets/inbox-notification-for-large-downloads.png)

## 下載使用連結共用所共用的資產 {#link-share-download}

使用連結共用資產是便利的方法，讓感興趣的人無需登入[!DNL Assets]即可使用它。 請參閱[連結共用功能](/help/assets/share-assets.md#sharelink)。

使用者從共用連結下載資產時，[!DNL Assets]會使用非同步服務，提供更快速且無中斷的下載。 要下載的資產會在收件匣的背景中排入可管理檔案大小的ZIP封存檔中。 若下載的檔案較大，則會將下載內容分割為100 GB的檔案。

[!UICONTROL 下載收件匣]會顯示每個封存的處理狀態。 處理完成後，您可以從收件匣下載封存。

![下載收件匣](assets/link-sharing-download-inbox.png)

## 啟用資產下載servlet {#enable-asset-download-servlet}

[!DNL Experience Manager]中的預設servlet可讓已驗證的使用者發出任意大型的並行下載請求，以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至可能使伺服器和網路過載。 為了減少此功能造成的潛在DoS風險，`AssetDownloadServlet`個OSGi元件已為發佈執行個體停用。 如果您不需要作者執行個體的下載功能，請停用作者的servlet。

若要允許從您的DAM下載資產，例如在使用Asset Share Commons或其他類似入口網站的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議將允許下載的大小設定為儘可能的低，以免影響日常下載需求。 高值可能會影響效能。

1. 建立以發佈執行模式為目標的命名慣例資料夾，即`config.publish`：

   `/apps/<your-app-name>/config.publish`

1. 在設定資料夾中，建立名為`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`的`nt:file`型別的檔案。
1. 以下列專案填入`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。 將下載的大小上限（以位元組為單位）設定為`asset.download.prezip.maxcontentsize`的值。 以下範例將ZIP下載的大小上限設定為不超過100 KB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

如果您不需要下載功能，請停用servlet以防止任何類似DoS的風險。 可透過更新Dispatcher設定以封鎖任何資產下載請求，在[!DNL Experience Manager]作者和發佈執行個體上停用`Asset Download Servlet`。 此servlet也可以直接透過OSGi主控台手動停用。

1. 若要透過Dispatcher設定封鎖資產下載請求，請編輯`dispatcher.any`設定並新增規則到[篩選區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## 開啟時間或關閉時間轉譯 {#on-off-time-rendition}

若要啟用`OnOffTimeAssetAccessFilter`服務，您必須建立OSGi設定。 此服務可讓您根據開啟/關閉時間設定，封鎖對資產本身以外轉譯和中繼資料的存取。 OSGi設定應該針對`com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`。 請遵循下列步驟：

1. 在Git中的專案程式碼中，於`/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`建立設定檔。 檔案應包含`{}`作為其內容，表示對應OSGi元件的空OSGi設定。 此動作會啟用服務。
1. 透過[!DNL Cloud Manager]部署您的程式碼，包括這個新的組態。
1. 部署後，即可根據資產的開啟/關閉時間設定存取轉譯和中繼資料。 如果目前日期或時間落在開啟時間之前或關閉時間之後，則會顯示錯誤訊息。
如需新增空白OSGi設定的詳細資訊，請參閱本[指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)。

## 提示和限制 {#tips-limitations}

* 如果您下載空白資料夾，[!DNL Experience Manager]會傳達一則關於建立ZIP封存檔的成功訊息，但並未建立封存檔。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [下載DRM保護的資產](drm.md)
>* 在Win或Mac案頭上使用Experience Manager案頭應用程式[下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [從支援的Adobe Assets應用程式中使用Adobe Creative Cloud Link下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
