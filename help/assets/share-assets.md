---
title: 分發和共用資產、資料夾和收集
description: 使用共用作為連結、下載和通過 [!DNL Brand Portal]。 [!DNL desktop app], [!DNL Asset Link]。
contentOwner: AG
feature: Asset Management,Collaboration,Asset Distribution
role: User,Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: c74846dc4d4da9fa5050ce7b8ffce7f27e77269b
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 1%

---

# 分享及分派於中國管理之資產 [!DNL Experience Manager] {#share-assets-from-aem}

[!DNL Adobe Experience Manager Assets] 允許您與組織成員和外部實體（包括合作夥伴和供應商）共用資產、資料夾和集合。 使用以下方法共用資產 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service]:

* [作為連結共用](#sharelink)。
* [下載資產](/help/assets/download-assets-from-aem.md) 分享。
* 共用使用 [[!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)。
* 共用使用 [[!DNL Adobe Asset Link]](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)。
* 共用使用 [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)。

## 以連結方式共用資產 {#sharelink}

通過連結共用資產是使外部各方無需登錄即可獲得資源的一種便捷方式 [!DNL Assets]。 該功能允許匿名用戶訪問和下載與他們共用的資產。 當用戶從共用連結下載資產時， [!DNL Assets] 使用非同步服務，提供更快且不間斷的下載。 要下載的資產將在收件箱的後台排隊到可管理檔案大小的ZIP存檔中。 對於大型下載，下載內容捆綁到100 GB的檔案中。

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* 您需要對要作為連結共用的資料夾或資產的「編輯ACL」權限。
>* [啟用出站電子郵件](/help/implementing/developing/introduction/development-guidelines.md#sending-email) 與用戶共用連結。


使用連結共用功能共用資產有兩種方法：

1. 生成共用連結， [複製並共用資產連結](#copy-and-share-assets-link) 與其他用戶。 連結的預設過期時間為一天。 無法在與其他用戶共用複製的連結時更改過期時間。

1. 生成共用連結並 [通過電子郵件共用資產連結](#share-assets-link-through-email)。 在這種情況下，您可以修改預設值，如到期日期和時間，並允許下載原始資產及其格式副本。 您可以通過添加多個用戶的電子郵件地址向其發送電子郵件。

![連結共用對話框](assets/link-sharing-dialog.png)

### 複製和共用資產連結{#copy-and-share-asset-link}

要將資產作為公共URL共用：

1. 登錄到 [!DNL Experience Manager Assets] 導航 **[!UICONTROL 檔案]**。
1. 選擇包含資產的資產或資料夾。 在工具欄中，按一下 **[!UICONTROL 共用連結]**。
1. 的 **[!UICONTROL 連結共用]** 對話框，其中包含自動生成的資產連結 **[!UICONTROL 共用連結]** 的子菜單。
1. 複製資產連結並與用戶共用。

### 通過電子郵件通知共用資產連結 {#share-assets-link-through-email}

要通過電子郵件共用資產：

1. 選擇包含資產的資產或資料夾。 在工具欄中，按一下 **[!UICONTROL 共用連結]**。
1. 的 **[!UICONTROL 連結共用]** 對話框，其中包含自動生成的資產連結 **[!UICONTROL 共用連結]** 的子菜單。

   * 在電子郵件地址框中，鍵入要與其共用連結的用戶的電子郵件ID。 您可以與多個用戶共用該連結。 如果用戶是您組織的成員，請從下拉清單中顯示的建議中選擇其電子郵件ID。 如果用戶是外部用戶，請鍵入完整的電子郵件ID並按 **[!UICONTROL 輸入]**;電子郵件ID將添加到用戶清單。

   * 在 **[!UICONTROL 主題]** 框中，鍵入主題以指定共用資產的用途。
   * 在 **[!UICONTROL 消息]** 框中，鍵入消息。
   * 在 **[!UICONTROL 到期]** 欄位，使用日期選取器指定連結的到期日期和時間。
   * 啟用 **[!UICONTROL 允許下載原始檔案]** 複選框，以允許收件人下載原始格式副本。

1. 按一下&#x200B;**[!UICONTROL 「共用」]**。一條消息確認該連結已與用戶共用。 用戶接收包含共用連結的電子郵件。

![連結共用電子郵件](assets/link-sharing-email-notification.png)

### 使用資產連結下載資產

任何有權訪問共用資產連結的用戶都可以下載綁定在zip資料夾中的資產。 下載過程相同，用戶是訪問複製的資產連結，還是使用通過電子郵件共用的資產連結。

* 按一下資產連結或在瀏覽器中貼上URL。 的 [!UICONTROL 連結共用] 介面開啟，您可以在其中切換到 [!UICONTROL 卡視圖] 或 [!UICONTROL 清單視圖]。

* 在 [!UICONTROL 卡視圖]，可以將滑鼠懸停在共用資產或共用資產資料夾上，以選擇資產或將其排隊以供下載。

* 預設情況下，用戶介面顯示 **[!UICONTROL 下載收件箱]** 的雙曲餘切值。 它反映排隊等待下載的所有共用資產或資料夾的清單及其狀態。

* 選擇資產或資料夾時， **[!UICONTROL 隊列下載]** 選項。 按一下 **[!UICONTROL 隊列下載]** 選項啟動下載進程。

   ![隊列下載](assets/queue-download.png)

* 準備下載檔案時，按一下 **[!UICONTROL 下載收件箱]** 的子菜單。 對於大型下載，請按一下 **[!UICONTROL 刷新]** 按鈕來更新狀態。

   ![下載收件箱](assets/link-sharing-download-inbox.png)

* 處理完成後，按一下 **[!UICONTROL 下載]** 按鈕下載zip檔案。

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>如果共用資產被移動到其他位置，則其連結將停止工作。 重新建立連結並與用戶重新共用。


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## 單獨下載資產和共用 {#download-and-share-assets}

用戶可以下載所需資產並在外部共用這些資產 [!DNL Experience Manager]。 有關詳細資訊，請參見 [如何搜索資產](/help/assets/search-assets.md)。 [如何下載資產](/help/assets/download-assets-from-aem.md), [如何下載收藏](manage-collections.md#download-a-collection)

## 與創意專業人員共用資產 {#share-with-creatives}

營銷人員和業務線用戶可以輕鬆地與他們的創造性專業人員共用批准的資產，

* **Experience Manager案頭應用**:該應用在Windows和Mac上運行。 請參閱 [案頭應用概述](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)。 要瞭解任何授權案頭用戶如何輕鬆訪問共用資產，請參閱 [瀏覽、搜索和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。 案頭用戶可以建立資產，並與Experience Manager用戶的對應用戶共用資產，例如，通過上傳新映像。 請參閱 [使用案頭應用上載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

* **Adobe資產連結**:創意專業人士可以直接從內部搜索和使用資產 [!DNL Adobe InDesign]。 [!DNL Adobe Illustrator], [!DNL Adobe Photoshop]。

## 設定資產共用 {#configure-sharing}

共用資產的不同選項需要特定的配置，並具有特定的先決條件。

### 配置資產連結共用 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

要為要與用戶共用的資產生成URL，請使用「連結共用」對話框。 具有管理員權限或具有讀取權限的用戶 `/var/dam/share` 位置可以查看與它們共用的連結。 通過連結共用資產是使外部各方無需首先登錄即可獲得資源的一種便捷方式 [!DNL Assets]。

>[!NOTE]
>
>如果要共用從「作者」實例到外部實體的連結，請確保僅公開以下URL `GET` 請求。 阻止其他URL以確保「作者」實例安全。
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### 啟用案頭應用使用的案頭操作 {#desktop-actions}

從 [!DNL Assets] 用戶介面，您可以瀏覽資產位置或簽出並開啟資產以在案頭應用程式中進行編輯。 這些選項稱為案頭操作，要啟用它，請參見 [啟用案頭操作 [!DNL Assets] Web介面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)。

![啟用案頭操作以在使用案頭應用時用作快捷方式](assets/enable_desktop_actions.png)

### 要使用的配置 [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe資產連結優化了內容建立流程中創意人員和營銷人員之間的協作。 它連接 [!DNL Adobe Experience Manager Assets] 與 [!DNL Creative Cloud] 案頭應用 [!DNL Adobe InDesign]。 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]。 的 [!DNL Adobe Asset Link] 面板允許創意人員訪問和修改儲存在 [!DNL Assets] 不留下他們最熟悉的創意應用。

請參閱 [如何配置 [!DNL Assets] 與 [!DNL Adobe Asset Link]](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html)。

## 最佳實踐和故障排除 {#bestpractices}

* 名稱中包含空白的資產資料夾或集合可能無法共用。
* 如果用戶無法下載共用資產，請與您的Experience Manager管理員檢查 [下載限制](#maxdatasize) 。
* 要讓用戶預覽使用連結共用共用的視頻，該視頻必須具有靜態視頻格式副本，位於 `/jcr:content/renditions` 在儲存庫中視頻節點中的位置。 預覽不取決於 [!DNL Dynamic Media] 格式副本。
* 通過連結共用下載視頻資產時， [!DNL Dynamic Media] 下載的存檔中不包括格式副本。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->
