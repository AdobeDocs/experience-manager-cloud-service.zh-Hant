---
title: 分發和共用資產、資料夾和集合
description: 使用共用作為連結、下載和透過 [!DNL Brand Portal]、 [!DNL desktop app]和 [!DNL Asset Link]等方法散發您的數位資產。
feature: Asset Management, Collaboration, Asset Distribution
role: Admin, User
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 3%

---

# 共用和散發在[!DNL Experience Manager]中管理的資產 {#share-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets]可讓您與組織成員和外部實體（包括合作夥伴和廠商）共用資產、資料夾和集合。 使用下列方法以[!DNL Cloud Service]形式共用[!DNL Experience Manager Assets]中的資產：

* [以連結共用](#sharelink)。
* [下載資產](/help/assets/download-assets-from-aem.md)並單獨共用。
* 使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)共用。
* 使用[[!DNL Adobe Asset Link]](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)共用。
* 使用[[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)共用。

## 先決條件 {#prerequisites}

您需要系統管理員許可權，才能[設定以連結](#config-link-share-settings)形式共用資產的設定。

## 設定連結共用設定 {#config-link-share-settings}

[!DNL Experience Manager Assets]可讓您設定預設的連結共用設定。

1. 按一下[!DNL Experience Manager]標誌，然後導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Assets組態]** > **[!UICONTROL 連結共用]**。
1. 初始設定：

   * **包含原始專案：**

      * 選取`Select Include Originals`以在連結共用對話方塊中依預設選取`Include Originals`選項。
      * 選取`Include Originals`選項在連結共用對話方塊中呈現給您的方式。 [!UICONTROL 可編輯]可讓使用者變更[初始設定]中在此定義的設定。 使用`Read-only`會顯示設定，但無法修改。 `Hidden`會隱藏設定，並使用此處在初始設定中設定的值。
   * **包含轉譯：**
      * 選取`Select Include Renditions`選項，以在連結共用對話方塊中依預設選取`Include Renditions`選項。
      * 選取`Include Renditions`選項在連結共用對話方塊中呈現給您的方式。 [!UICONTROL 可編輯]可讓使用者變更[初始設定]中在此定義的設定。 使用`Read-only`會顯示設定，但無法修改。 `Hidden`會隱藏設定，並使用此處在初始設定中設定的值。

1. 在`Expiration date`區段的`Validity Period`欄位中指定連結的預設有效期。

1. 動作列中的&#x200B;**[!UICONTROL 連結共用]**&#x200B;按鈕：
   * 所有具有`jcr:modifyAccessControl`許可權的使用者都可以檢視[!UICONTROL 連結共用]選項。 依預設，所有管理員都可看見它。 依預設，[!UICONTROL 連結共用]按鈕對所有人都可見。 您可以設定只對已定義的群組顯示此選項，也可以拒絕特定群組的此選項。 若要允許特定群組檢視`Share Link`選項，請選取`Allow only for groups`。 選取`Deny from groups`以拒絕特定群組的`Share Link`選項。 選取任何這些選項後，請使用`Select Groups`欄位指定群組名稱，以新增您需要允許或拒絕的群組名稱。

如需電子郵件組態相關設定，請瀏覽[電子郵件服務檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/email-service.html)

![設定電子郵件服務](/help/assets/assets/config-email-service.png)

## 以連結方式共用資產 {#sharelink}

透過連結共用資產是讓外部對象、行銷人員和其他[!DNL Experience Manager]使用者能夠使用資源的便利方式。 功能可讓匿名使用者存取及下載與其共用的資產。 從共用連結下載資產時，[!DNL Experience Manager Assets]會使用非同步服務，提供更快速且無中斷的下載。 要下載的資產會在背景排入可管理檔案大小的ZIP封存檔中。 對於大型下載，下載會整合到多個檔案中，每個檔案大小為100 GB。

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* 您需要對要以連結形式共用的資料夾或資產具有「編輯ACL」許可權。
>* [在與使用者共用連結前，啟用外寄電子郵件](/help/implementing/developing/introduction/development-guidelines.md#sending-email)。

使用連結共用功能時，有兩種方式可共用資產：

1. 產生共用連結[複製，並與其他使用者共用資產連結](#copy-and-share-assets-link)。
1. 產生共用連結並[透過電子郵件](#share-assets-link-through-email)共用資產連結。 您可以修改預設值（例如到期日和時間），並允許下載原始資產及其轉譯。 您可以新增多個使用者的電子郵件地址，以傳送電子郵件給他們。

   ![連結共用對話方塊](assets/share-link.png)

在這兩種情況下，您都可以修改預設值（例如到期日和時間），並允許下載原始資產及其轉譯。

### 複製並共用資產連結{#copy-and-share-asset-link}

若要以公用URL形式共用資產：

1. 登入[!DNL Experience Manager Assets]並導覽至&#x200B;**[!UICONTROL 檔案]**。
1. 選取資產或包含資產的檔案夾。 在工具列中按一下&#x200B;**[!UICONTROL 共用連結]**。
1. **[!UICONTROL 連結共用]**&#x200B;對話方塊出現，其中在&#x200B;**[!UICONTROL 共用連結]**&#x200B;欄位中包含自動產生的資產連結。
1. 視需要設定共用連結的到期日。
1. 在&#x200B;**[!UICONTROL 連結設定]**&#x200B;下，核取或取消核取`Include Originals`或`Include Renditions`以包含或排除其中一個。 至少必須選擇選項。
1. 所選Assets的名稱會顯示在[!DNL Share Link]對話方塊的右欄。
1. 複製資產連結並與使用者共用。

### 透過電子郵件通知共用資產連結 {#share-assets-link-through-email}

若要透過電子郵件共用資產：

1. 選取資產或包含資產的檔案夾。 在工具列中按一下&#x200B;**[!UICONTROL 共用連結]**。
1. **[!UICONTROL 連結共用]**&#x200B;對話方塊出現，其中在&#x200B;**[!UICONTROL 共用連結]**&#x200B;欄位中包含自動產生的資產連結。

   * 在電子郵件地址方塊中，輸入您要共用連結之使用者的電子郵件地址。 您可以與多位使用者共用連結。 如果使用者是您組織的成員，請從下拉式清單中顯示的建議中選取其電子郵件地址。 在電子郵件地址文字欄位中，輸入您要共用連結之使用者的電子郵件地址，然後按一下[!UICONTROL 輸入]。 您可以與多位使用者共用連結。

   * 在&#x200B;**[!UICONTROL 主旨]**&#x200B;方塊中，輸入主旨以指定共用資產的用途。
   * 在&#x200B;**[!UICONTROL 訊息]**&#x200B;方塊中，視需要輸入訊息。
   * 在&#x200B;**[!UICONTROL 到期]**&#x200B;欄位中，使用日期選擇器來指定連結的到期日期和時間。
   * 啟用&#x200B;**[!UICONTROL 允許下載原始檔案]**&#x200B;核取方塊，允許收件者下載原始轉譯。

1. 按一下&#x200B;**[!UICONTROL 共用]**。 訊息會確認此連結已與使用者共用。 使用者會收到包含共用連結的電子郵件。

   ![連結共用電子郵件](assets/link-sharing-email-notification.png)

### 自訂電子郵件範本 {#customize-email-template}

精心設計的範本可傳達專業精神與能力，提升訊息與組織的信譽。 [!DNL Adobe Experience Manager]可讓您自訂電子郵件範本，此範本會傳送給接收包含共用連結之電子郵件的收件者。 此外，自訂的電子郵件範本可讓您透過提供收件者名稱並參考與他們相關的特定詳細資訊，來個人化您的電子郵件內容。 這種個人接觸可能會讓收件者感受到價值，並提升參與度。 不僅如此，自訂範本還可確保您的電子郵件與品牌身分一致，包括標誌、顏色和字型。 一致性可加強品牌認知度，以及收件者之間的信任。

#### 自訂電子郵件範本的格式 {#format-of-custom-email-template}

可使用純文字或HTML自訂電子郵件範本。 可在`/libs/settings/dam/adhocassetshare/en.txt`找到預設的可編輯範本連結。 您可以建立檔案`/apps/settings/dam/adhocassetshare/en.txt`來覆寫範本。 您可以視需要多次修改電子郵件範本。

| 預留位置 | 說明 |
|---|-----|
| `${emailSubject}` | 電子郵件的主旨 |
| `${emailInitiator}` | 建立電子郵件的使用者的電子郵件ID |
| `${emailMessage}` | 電子郵件內文 |
| `${pagePath}` | 共用連結的URL |
| `${linkExpiry}` | 共用連結到期日 |

<!--| `${host.prefix}` | Origin of the [!DNL Experience Manager] instance, for example `http://www.adobe.com"` |-->

#### 自訂電子郵件範本範例 {#custom-email-template-example}

```
subject: ${emailSubject}

<!DOCTYPE html>
<html><body>
<p><strong>${emailInitiator}</strong> invited you to review assets.</p>
<p>${emailMessage}</p>
<p>The shared link will be available until ${linkExpiry}.
<p>
    <a href="${pagePath}" target="_blank"><strong>Open</strong></a>
</p>

</body></html>
```

<!--Sent from instance: ${host.prefix}-->

### 使用資產連結下載資產 {#download-assets-using-asset-link}

任何有權存取共用資產連結的使用者都可以下載zip資料夾中隨附的資產。 無論使用者是存取複製的資產連結，或使用透過電子郵件共用的資產連結，下載程式都相同。

* 按一下資產連結，或將URL貼到瀏覽器中。 [!UICONTROL 連結共用]介面會開啟，您可以在其中切換至[!UICONTROL 卡片檢視]或[!UICONTROL 清單檢視]。

* 在[!UICONTROL 卡片檢視]中，您可以將滑鼠停留在共用資產或共用資產資料夾上，以選取資產或將它們排入下載佇列。

* 依預設，使用者介面會顯示&#x200B;**[!UICONTROL 下載收件匣]**&#x200B;選項。 它反映所有佇列等待下載的共用資產或資料夾的清單及其狀態。

* 選取資產或資料夾時，畫面上會顯示&#x200B;**[!UICONTROL 佇列下載]**&#x200B;選項。 按一下&#x200B;**[!UICONTROL 佇列下載]**&#x200B;選項以啟動下載程式。

  ![將下載排入佇列](assets/queue-download.png)

* 準備下載檔案時，請按一下&#x200B;**[!UICONTROL 下載收件匣]**&#x200B;選項以檢視下載狀態。 若是大型下載，請按一下&#x200B;**[!UICONTROL 重新整理]**&#x200B;按鈕以更新狀態。

  ![下載收件匣](assets/link-sharing-download-inbox.png)

* 處理完成後，按一下&#x200B;**[!UICONTROL 下載]**&#x200B;按鈕以下載zip檔案。

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>如果共用資產移至其他位置，其連結會停止運作。 重新建立連結，並與使用者重新共用。


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

## 分別下載資產和共用 {#download-and-share-assets}

使用者可以下載必要的資產，並在[!DNL Experience Manager]之外共用這些資產。 如需詳細資訊，請參閱[如何搜尋資產](/help/assets/search-assets.md)、[如何下載資產](/help/assets/download-assets-from-aem.md)以及[如何下載集合](manage-collections.md#download-a-collection)

## 與創意專業人士共用資產 {#share-with-creatives}

行銷人員和業務線使用者可透過輕鬆與其創意專業人士共用已核准的資產，

* **Experience Manager案頭應用程式**：此應用程式可在Windows和Mac上運作。 請參閱[案頭應用程式總覽](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)。 若要瞭解任何授權案頭使用者如何輕鬆存取共用資產，請參閱[瀏覽、搜尋及預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。 案頭使用者可以建立資產，並透過上傳新影像等方式與身為Experience Manager使用者的同行共用資產。 請參閱[使用案頭應用程式上傳資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

* **Adobe Asset Link**：創意專業人士可以直接從[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]中搜尋和使用資產。

## 設定資產共用 {#configure-sharing}

共用資產的不同選項需要特定設定，且具備特定先決條件。

### 設定資產連結共用 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

若要產生您要與使用者共用之資產的URL，請使用連結共用對話方塊。 具有管理員許可權或在`/var/dam/share`位置具有讀取許可權的使用者可以檢視與他們共用的連結。 透過連結共用資產是一種便利的方法，讓外部對象無需先登入[!DNL Assets]即可使用資源。

>[!NOTE]
>
>如果您想要將來自作者執行個體的連結分享至外部實體，請確定您僅公開`GET`請求的下列URL。 封鎖其他URL以確保您的Author例項安全。
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`

<!--
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password
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

### 啟用案頭動作以與案頭應用程式搭配使用 {#desktop-actions}

從瀏覽器的[!DNL Assets]使用者介面中，您可以探索資產位置或取出並開啟資產，以在您的案頭應用程式中進行編輯。 這些選項稱為案頭動作，若要啟用它，請參閱[在 [!DNL Assets] 網頁介面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)中啟用案頭動作。

![啟用案頭動作，以便在使用案頭應用程式時作為捷徑](assets/enable_desktop_actions.png)

### 使用[!DNL Adobe Asset Link]的設定 {#configure-asset-link}

Adobe Asset Link可簡化創意人員與行銷人員在內容建立過程中的合作。 它將[!DNL Adobe Experience Manager Assets]與[!DNL Creative Cloud]個案頭應用程式、[!DNL Adobe InDesign]、[!DNL Adobe Photoshop]和[!DNL Adobe Illustrator]連線。 [!DNL Adobe Asset Link]面板可讓創意人員存取及修改儲存在[!DNL Assets]中的內容，而不需離開他們最熟悉的創意應用程式。

請參閱[如何設定 [!DNL Assets] 以搭配 [!DNL Adobe Asset Link]](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html)使用。

## 最佳作法和疑難排解 {#bestpractices}

* 名稱中包含空白字元的資產資料夾或集合可能無法共用。
* 如果使用者無法下載共用資產，請洽詢Experience Manager管理員的下載限製為何。 預設值為100 MB。
* 若要讓使用者預覽使用連結共用共用的視訊，該視訊必須在存放庫內視訊節點中的`/jcr:content/renditions`位置提供靜態視訊轉譯。 預覽不依存於[!DNL Dynamic Media]轉譯的可用性。
* 透過連結共用下載視訊資產時，[!DNL Dynamic Media]轉譯未包含在已下載的封存檔中。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

