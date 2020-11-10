---
title: 下載資產
description: 下載資 [!DNL Adobe Experience Manager Assets] 產以啟用或停用下載功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接寄送包含資產連結的電子郵件 [!DNL Adobe Experience Manager Assets]。 已下載的資產會整合在ZIP檔案中。 壓縮的ZIP檔案對於匯出工作的檔案大小上限為1 GB。 每個匯出工作最多允許500個資產。

>[!NOTE]
>
>電子郵件的收件者必須是群組的 `dam-users` 成員，才能存取電子郵件訊息中的ZIP下載連結。 若要下載資產，成員必須擁有啟動觸發資產下載的工作流程的權限。

無法下載資產類型影像集、回轉集、混合媒體集和轉盤集。

您可以使用下列方法下載Experience Manager資產：

* [Experience Manager使用者介面](#download-in-aem)
* 資產連結共用使用者介面
* [資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [品牌入口網站](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用AEM介面下載資產 {#download-in-aem}

非同步下載服務提供架構，可順暢地下載大型資產。 從使用者介面即時下載較小的檔案。 大型檔案會非同步下載，而且使用者會透過收件匣中的Experience Manager通知得知完成。 請參 [閱瞭解Experience Manager收件匣](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html)。

![下載通知](assets/download-notification.png)

*圖：透過收件匣下載 [!DNL Experience Manager] 通知。*

非同步下載會在下列任一情況下觸發：

* 如果要下載的資產超過10個或超過100 MB。
* 如果下載需要30秒以上的時間來準備。

若要下載資產，請依照下列步驟進行：

1. 在使 [!DNL Experience Manager] 用者介面中，按一下「 **[!UICONTROL 資產]** >檔 **[!UICONTROL 案」]**。
1. 導覽至您要下載的資產。 選取資料夾或選取資料夾內的一或多個資產。 在工具列上，按一下「 **[!UICONTROL 下載]**」。

   ![從下載資產時的可用選項 [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *圖：下載對話框選項。*

1. 在「下載」對話方塊中，選取您想要的下載選項。

   | 下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選取此選項，將您下載的每個資產（包括資產）包含在資產父資料夾下巢狀的子資料夾中，並放入本機電腦上的一個資料夾。 如果未選取 *此選項* ，預設會忽略資料夾階層，而所有資產都會下載到本機電腦的一個資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 選取此選項，可傳送電子郵件通知給收件者。 標準電子郵件範本可在下列位置取得：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您在部署期間自訂的範本可在下列位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在下列位置儲存租用戶特定的自訂範本：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取這個選項，以原始格式下載資產，而不需任何轉譯。<br>如果原始資產有子資產，則可使用子資產選項。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產具有主要表示法——已上傳檔案的主要表示法。 它們可以有任意數量的表示。 <br> 使用這個選項，您可以選取您要下載的轉譯。 可用的轉譯取決於您選取的資產。 |
   | **[!UICONTROL 智慧裁切]** | 選取這個選項，可從內部下載所選資產的所有智慧型裁切轉譯 [!DNL Experience Manager]。 系統會建立包含「智慧型裁切」轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項，即時產生一連串的替代轉譯。 當您選取此選項時，也可以從「影像預設集」清單中選取您要動態建立的轉 [譯](/help/assets/dynamic-media/image-presets.md) 。 <br>此外，您還可以選取大小和單位、格式、色域、解析度，以及任何可選的影像修飾元，例如反轉影像。 此選項僅在您已啟用時才可 [!DNL Dynamic Media] 用。 |

1. 在對話方塊中，按一下「 **[!UICONTROL 下載]**」。

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設Servlet [!DNL Experience Manager] 允許驗證用戶發出任意大的併發下載請求，以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至會使伺服器和網路過載。 為了降低此功能造成的類似DoS的潛在風險，發佈例項 `AssetDownloadServlet` 會停用OSGi元件。

若要允許從DAM下載資產，例如，當使用資產共用共用共用或其他類似入口網站的實施時，請透過OSGi組態手動啟用servlet。 Adobe建議盡可能將允許的下載大小設定得盡可能低，而不會影響日常下載需求。 高價值可能會影響效能。

1. 使用命名慣例建立資料夾，以發佈執行模式為目標，即 `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在config資料夾中，建立名為的新文 `nt:file` 件 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. 填 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 入下列。 將下載的最大大小（以位元組為單位）設定為值 `asset.download.prezip.maxcontentsize`。 下面的示例將ZIP下載的最大大小配置為不超過100 kB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

您可 `Asset Download Servlet` 以在「發佈」例項上停用此功能，方法是更新 [!DNL Experience Manager] 分派器組態以封鎖任何資產下載請求。 也可以通過OSGi控制台手動禁用servlet。

1. 若要透過分派器設定封鎖資產下載請求，請編 `dispatcher.any` 輯設定，並新增規則至篩 [選區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下載受DRM保護的資產](drm.md)
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [從支援的Adobe Creative Cloud應用程式使用Adobe Assets Link下載資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)

