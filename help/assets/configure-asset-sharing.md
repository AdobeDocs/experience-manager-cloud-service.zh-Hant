---
title: 將資產、檔案夾和系列共用為連結
description: 本文說明如何在Experience Manager Assets中以超連結的形式共用資產、檔案夾和系列。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 設定資產連結共用 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

若要產生您要與使用者共用之資產的URL，請使用「連結共用」對話方塊。 具有管理員權限或在位置具有讀取權 `/var/dam/share` 限的使用者可檢視與其共用的連結。 透過連結分享資產是讓外部廠商可使用資源的便利方式，而不需要先登入AEM Assets。

>[!NOTE]
>
>如果您想要將AEM Author例項的連結共用給外部實體，請確定您只針對請求公開下列 `GET` URL。 封鎖其他URL，以確保您的AEM Author例項安全。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## 配置日CQ郵件服務 {#configmailservice}

在可以將資產共用為連結之前，請先設定電子郵件服務。

1. 按一下或點選AEM標誌，然後導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 從服務清單中，找到 **[!UICONTROL Day CQ Mail Service]**。
1. 按一下 **[!UICONTROL 服務旁的]** 「編輯」圖示，並設定下列 **** Day CQ Mail Services參數，並依其名稱提及詳細資訊：

   * SMTP伺服器主機名：電子郵件伺服器主機名
   * SMTP伺服器埠：電子郵件伺服器端
   * SMTP用戶：電子郵件伺服器使用者名稱
   * SMTP密碼：電子郵件伺服器密碼

1. 按一下／點選「 **儲存**」。

## 配置最大資料大小 {#maxdatasize}

當您使用「連結共用」功能從共用的連結下載資產時，AEM會從儲存庫壓縮資產階層，然後以ZIP檔案傳回資產。 但是，在ZIP檔案中壓縮的資料量沒有限制的情況下，大量資料會遭受壓縮，造成JVM中記憶體錯誤。 要防止系統因此遭受潛在的拒絕服務攻擊，請使用Configuration Manager中的Day CQ DAM Adhoc Asset Share Proxy Servlet的 **Max Content Size（未壓縮）** （未壓縮）參數配置最大大小。 如果資產的未壓縮大小超過設定的值，資產下載請求便會遭拒。 預設值為100 MB。

1. 按一下/點選AEM標誌，然後前往「工 **具** > **作業** >網 **頁主控台**」。
1. 在Web主控台中，找 **到Day CQ DAM Adhoc Asset Share Proxy Servlet設定** 。
1. 在編輯模 **式中開啟「日CQ DAM臨機資產共用代理Servlet** 」設定，並修改「最大內容大小 (未壓縮) 」 **參數的值** 。
1. 儲存變更。

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
