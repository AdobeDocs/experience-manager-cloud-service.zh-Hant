---
title: 下載資產
description: 從 [!DNL Adobe Experience Manager Assets] 下載資產，並啟用或停用下載功能。
contentOwner: AG
feature: 資產管理
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 2f9e8c00674979c4a245d410b68fd99c60eccfb4
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---

# 從[!DNL Adobe Experience Manager]下載資產 {#download-assets-from-aem}

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接從[!DNL Adobe Experience Manager Assets]傳送包含資產連結的電子郵件。 下載的資產會以ZIP檔案整合。<!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

>[!NOTE]
>
>電子郵件的收件者必須是`dam-users`群組的成員，才能存取電子郵件中的ZIP下載連結。 若要下載資產，成員必須擁有啟動工作流程的權限，該工作流程會觸發資產下載。

無法下載資產類型影像集、回轉集、混合媒體集和轉盤集。

您可以使用下列方法下載Experience Manager資產：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager使用者介面](#download-assets)
* [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [品牌入口網站](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用[!DNL Experience Manager]介面下載資產 {#download-assets}

非同步下載服務提供大型資產無縫下載的架構。 從使用者介面即時下載較小的檔案。 [!DNL Experience Manager] 不會封存下載原始檔案的單一資產下載。此功能可加快下載速度。 大型檔案會以非同步方式下載，而[!DNL Experience Manager]會透過收件匣中的通知通知完成。 請參閱[了解 [!DNL Experience Manager] 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

![下載通知](assets/download-notification.png)

*圖：透過收件匣下載 [!DNL Experience Manager] 通知。*

非同步下載會在下列任一情況下觸發：

* 如果要下載的資產超過10個或超過100 MB。
* 如果下載需要30秒以上的時間準備。

若要下載資產，請依照下列步驟操作：

1. 在[!DNL Experience Manager]使用者介面中，按一下&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 導覽至您要下載的資產。 選取資料夾，或在資料夾內選取一或多個資產。 在工具列上，按一下&#x200B;**[!UICONTROL Download]**。

   ![從下載資產時的可用選項  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *圖：下載對話框選項。*

1. 在下載對話方塊中，選取您想要的下載選項。

   | 下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選取此選項，將您下載的每個資產（包括資產的父資料夾下巢狀子資料夾中的資產），納入本機電腦上的一個資料夾。 當此選項為&#x200B;*not*&#x200B;時，預設情況下，會忽略資料夾層次結構，並將所有資產下載到本地電腦的一個資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 選取此選項可將電子郵件通知傳送至收件者。 標準電子郵件範本位於下列位置：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署期間自定義的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在下列位置儲存租用戶專用的自訂範本：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取此選項即可下載原始格式的資產，而不需任何轉譯。<br>如果原始資產具有子資產，則會提供子資產選項。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產有主要表示法，即上傳之檔案的主要表示法。 它們可以有任意數量的表示。 <br> 使用此選項，您可以選取要下載的轉譯。可用的轉譯取決於您選取的資產。 |
   | **[!UICONTROL 智慧裁切]** | 選取此選項，即可從[!DNL Experience Manager]內下載所選資產的所有智慧型裁切轉譯。 會建立包含智慧型裁切轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項即時產生一系列替代轉譯。 選取此選項時，您也可以從[影像預設集](/help/assets/dynamic-media/image-presets.md)清單中選取，以動態方式選取您要建立的轉譯。 <br>此外，您還可以選取尺寸和單位、格式、顏色空間、解析度，以及任何可選的影像修飾符，如反相影像。只有在您已啟用[!DNL Dynamic Media]時，選項才可用。 |

1. 在對話框中，按一下&#x200B;**[!UICONTROL Download]**。

## 下載使用連結共用共用的資產 {#link-share-download}

>[!NOTE]
>
>此功能可在Experience Manager發行前管道中使用。

使用連結共用資產是讓感興趣的人能使用的便利方式，而不需先登入[!DNL Assets]。 若要產生共用資產的URL，請使用[連結共用功能](/help/assets/share-assets.md#sharelink)。

使用者從共用連結下載資產時，[!DNL Assets]會使用非同步服務，提供更快速且不間斷的下載。 要下載的資產會在收件匣的背景中排入佇列，並放入可管理檔案大小的ZIP封存檔中。 若是下載量非常大，下載會分塊為大小為100 GB的檔案。

收件匣會顯示每個封存的處理狀態。 處理完成後，您就可以從收件匣下載封存檔。

![下載收件匣](assets/download-inbox.png)

## 啟用資產下載servlet {#enable-asset-download-servlet}

[!DNL Experience Manager]中的預設Servlet可讓已驗證的使用者發出任意大的同時下載請求，以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至可能會使伺服器和網路過載。 為了降低此功能造成的類似DoS的潛在風險，發佈執行個體會停用`AssetDownloadServlet` OSGi元件。 如果您不需要製作例項的下載功能，請停用製作上的servlet。

若要允許從DAM下載資產，例如使用資產共用公域或其他類似入口的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議盡可能低地設定允許的下載大小，而不影響日常下載需求。 高值可能會影響效能。

1. 建立資料夾，其命名慣例會鎖定發佈執行模式，即`config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在配置資料夾中，建立名為`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`的`nt:file`類型的新檔案。
1. 用以下填入`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。 將下載的最大大小（以位元組為單位）設定為`asset.download.prezip.maxcontentsize`的值。 以下範例會將ZIP下載的最大大小設定為不超過100千位元組。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

如果您不需要下載功能，請停用servlet以防止任何類似DoS的風險。 您可以更新Dispatcher設定以封鎖任何資產下載請求，以在[!DNL Experience Manager]作者和發佈例項上停用`Asset Download Servlet`。 您也可以直接透過OSGi主控台手動停用servlet。

1. 若要透過Dispatcher設定來封鎖資產下載請求，請編輯`dispatcher.any`設定，並將新規則新增至[篩選器區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下載受DRM保護的資產](drm.md)
* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
* [從支援的Adobe Creative Cloud應用程式使用Adobe資產連結下載資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)

