---
title: 將資產、檔案夾和系列共用為連結
description: 本文說明如何在Experience Manager Assets中以超連結的形式共用資產、檔案夾和系列。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 分享和分發在Experience Manager中管理的資產 {#share-assets-from-aem}

Adobe Experience Manager(AEM)Assets可讓您與組織成員及外部實體（包括合作夥伴和廠商）共用資產、資料夾和系列。 您可以使用下列方法，將Experience Manager Assets中的資產共用為雲端服務：

* 以連結的形式分享
* 下載資產
* 透過AEM案頭應用程式分享
* 透過Adobe Asset Link分享
* （近期功能）使用品牌入口網站分享

## 以連結方式共用資產 {#sharelink}

若要產生您要與使用者共用之資產的URL，請使用「連結共用」對話方塊。 具有管理員權限或在位置具有讀取權 `/var/dam/share` 限的使用者可檢視與其共用的連結。 透過連結分享資產是讓外部廠商可使用資源的便利方式，而不需要先登入AEM Assets。

>[!NOTE]
>
>* 您需要對要作為連結共用的資料夾或資產的編輯ACL權限。
>* 在您與使用者共用連結之前，請確定已設定Day CQ Mail Service。 否則，會發生錯誤。


1. 在「資產」使用者介面中，選取要以連結形式共用的資產。
1. 在工具列中，按一下／點選「共 **[!UICONTROL 用連結」]**。

   資產連結會在「共用連結」欄位中 **[!UICONTROL 自動建立]** 。 複製此連結並與使用者共用。 連結的預設有效期為一天。

   或者，繼續執行本程式的步驟3-7以新增電子郵件收件者、設定連結的過期時間，並從對話方塊傳送。

   >[!NOTE]
   >
   >如果共用資產移至不同位置，其連結將停止運作。 重新建立連結並與使用者重新共用。

1. 從Web主控台開啟 **[!UICONTROL Day CQ Link Externalizer]** configuration，並在 **[!UICONTROL Domains]** （網域）欄位中修改下列屬性，並針對每個欄位提及值：

   * 本機
   * 作者
   * 發佈
   對於本機和作者屬性，請分別提供本機和作者實例的URL。 如果您執行單一AEM作者例項，本機和作者屬性的值都相同。 對於發佈，請提供發佈例項的URL。

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。 您也可以與多位使用者共用連結。

   如果使用者是您組織的成員，請從顯示在輸入區域下方清單中的建議電子郵件ID中，選取使用者的電子郵件ID。 對於外部使用者，輸入完整的電子郵件ID，然後從清單中選取它。

   要啟用發送給用戶的電子郵件，請在第CQ天郵件服務中配置SMTP服 [務器詳細資訊](/help/assets/configure-asset-sharing.md#configmailservice)。

   >[!NOTE]
   >
   >如果您輸入非您組織成員之使用者的電子郵件ID,「外部使用者」會加上使用者的電子郵件ID前置詞。

1. 在「主 **[!UICONTROL 體]** 」方塊中，輸入您要共用之資產的主體。
1. 在「消 **[!UICONTROL 息]** 」框中，輸入可選消息。
1. 在「過 **[!UICONTROL 期]** 」欄位中，使用日期選擇器指定連結的到期日期和時間。 依預設，到期日是從您共用連結的日期開始的一週。
1. 若要讓使用者下載原始影像以及轉譯，請選取「允 **[!UICONTROL 許下載原始檔案」]**。

   >[!NOTE]
   >
   >依預設，使用者只能下載您以連結形式共用之資產的轉譯。

1. 按一下&#x200B;**[!UICONTROL 「共用」]**。訊息會確認連結是透過電子郵件與使用者共用。
1. 若要檢視共用資產，請按一下／點選傳送給使用者之電子郵件中的連結。 共用資產會顯示在 **[!UICONTROL Adobe Marketing Cloud頁面中]** 。

   若要切換至清單檢視，請按一下／點選工具列中的版面圖示。

1. 若要產生資產的預覽，請按一下／點選共用資產。 若要關閉預覽並返回 **[!UICONTROL Marketing Cloud]** ，請按一下工具列中的「上 **[!UICONTROL 一步]** 」。 如果您已共用資料夾，請按一下／點選「 **[!UICONTROL 上層資料夾]** 」以返回上層資料夾。

   >[!NOTE]
   >
   >AEM支援產生下列MIME類型資產的預覽：JPG、PNG、GIF、BMP、INDD、PDF和PPT。 您只能下載其他MIME類型的資產。

1. 若要下載共用資產，請按一下／點選工具列中的「 **[!UICONTROL Select]** 」（選擇），按一下／點選資產，然後按一下／點選工具列中的「 **[!UICONTROL Download]** 」（下載）。
1. 若要檢視您共用為連結的資產，請前往「資產」UI，然後按一下／點選「GlobalNav」圖示。 從清 **[!UICONTROL 單選擇]** 「導覽」，以顯示「導覽」窗格。
1. 從「導覽」窗格中，選 **[!UICONTROL 擇「共用連結]** 」以顯示共用資產清單。
1. 若要取消共用資產，請選取資產，然後從工具列點選／按 **[!UICONTROL 一下]** 「取消共用」。

訊息會確認您已取消共用資產。 此外，資產的項目也會從清單中移除。

## 下載及分享資產 {#download-and-share-assets}

使用者可以下載一些資產，並在Experience manager之外共用這些資產。 如需詳細資訊，請 [參閱如何搜尋資產](/help/assets/search-assets.md)[、如何下載資產](/help/assets/download-assets-from-aem.md), [以及如何下載系列](manage-collections.md#download-a-collection)

## 與創意專業人員共用資產 {#share-with-creatives}

行銷人員和業務線使用者可以使用、

* **AEM案頭應用程式**:應用程式可在Windows和Mac上運作。 請參閱桌 [面應用程式概觀](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)。 若要瞭解任何授權案頭使用者如何輕鬆存取共用資產，請參 [閱瀏覽、搜尋和預覽資產](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。 案頭使用者可以建立新資產，並與AEM使用者的對應人員共用，例如上傳新影像。 請參閱 [使用案頭應用程式上傳資產](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

* **Adobe Asset Link**:創意專業人員可直接在Adobe inDesign、Adobe Illustrator和Adobe Photoshop中搜尋及使用資產。

### Best practices and troubleshooting {#bestpractices}

* 名稱中包含空白字元的資產資料夾或系列可能無法共用。
* 如果使用者無法下載共用資產，請洽詢您的AEM管理員下 [載限制](/help/assets/configure-asset-sharing.md#maxdatasize) 。
* 如果您無法傳送含有共用資產連結的電子郵件，或如果其他使用者無法收到您的電子郵件，請洽詢您的AEM管理員( [是否已設定](/help/assets/configure-asset-sharing.md#configmailservice) 電子郵件服務)。
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的權限。 請參閱 [分享資產](#sharelink)。

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
