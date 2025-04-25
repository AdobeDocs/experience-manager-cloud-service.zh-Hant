---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: 如何連線SharePoint檔案庫取得最適化表單、提交至SharePoint、建立SharePoint檔案庫設定、在最適化表單中使用提交至SharePoint提交動作、AEM Forms資料模型SharePoint檔案庫、Forms資料模型SharePoint檔案庫、將Forms資料模型整合至SharePoint檔案庫
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: a00b4a93-2324-4c2a-824f-49146dc057b0
source-git-commit: 1dddba99c5871d01bf51c335747363af1889738d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 33%

---

# 將最適化表單連線至Microsoft® SharePoint檔案庫 {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

若要以最適化表單使用&#x200B;**[!UICONTROL 提交至SharePoint檔案庫]**&#x200B;提交動作：

1. [建立SharePoint檔案庫組態](#1-create-a-sharepoint-document-library-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint儲存體。
2. [使用最適化表單中的「提交到 SharePoint」提交動作](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form)：會將您的最適化表單連結到已設定的 Microsoft® SharePoint。

## 1.建立SharePoint檔案庫組態

若要將AEM Forms連線至您的Microsoft® Sharepoint檔案庫儲存空間：

1. 前往您的&#x200B;**AEM Forms作者**&#x200B;執行個體> **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 選取&#x200B;**[!UICONTROL Microsoft® SharePoint]**&#x200B;後，系統會將您重新導向至&#x200B;**[!UICONTROL SharePoint瀏覽器]**。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 從下拉式清單中按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL SharePoint檔案庫]**。 此時會顯示 SharePoint 設定精靈。

   ![SharePoint 設定](/help/forms/assets/sharepoint_configuration.png)

1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增API許可權`offline_access`和`Sites.Manage.All`，以提供讀取/寫入許可權。`Sites.Manage.All`是Microsoft Graph API中的許可權範圍，可授予應用程式管理SharePoint Sites所有方面的能力，例如刪除或修改網站。

     >[!NOTE]
     >
     > 您也可以[在SharePoint的Graph API中使用`Sites.Selected`許可權範圍，以有限存取權](/help/forms/configure-sharepoint-site-limited-access.md)設定Microsoft網站。 `Sites.Selected`是Microsoft的Graph API中的許可權範圍，可讓您更精細且受限地存取SharePoint網站。

   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. Microsoft的Graph API中的`offline_access Sites.Selected`許可權範圍，允許對SharePoint網站進行更精細且受限制的存取。 Microsoft的Graph API中的`offline_access Sites.Manage.All`許可權範圍，允許完整存取SharePoint網站。
1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在選取&#x200B;**SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 依預設，`forms-ootb-storage-adaptive-forms-submission`存在於選取的SharePoint網站。
   >* 按一下&#x200B;**建立資料夾**，將資料夾建立為`forms-ootb-storage-adaptive-forms-submission` (如果尚未存在於所選SharePoint網站的`Documents`資料庫中)。

現在，您可以使用此SharePoint Sites設定，在最適化表單中執行提交動作。

### 2.在最適化表單中使用SharePoint檔案庫設定

您可以使用在最適化表單中建立的SharePoint檔案庫組態，將資料或產生的記錄檔案儲存在SharePoint資料夾中。 執行以下步驟，在最適化表單中使用SharePoint檔案庫儲存設定，如下所示：

1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 為最適化表單選取相同的[!UICONTROL 設定容器]，您已在其中建立SharePoint檔案庫儲存空間。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 SharePoint]**」。
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

>[!NOTE]
>
> 當您提交表單時，資料會儲存在指定的Microsoft® Sharepoint檔案庫儲存空間中。 儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

>[!NOTE]
>
> 附件也儲存在`/folder_name/form_name/year/month/date/submission_id/data`目錄中。 不過，如果您選取&#x200B;**以原始名稱儲存附件**，則附件會使用其原始檔案名稱儲存在資料夾中。
> ![影像](/help/forms/assets/sp-doc-attachment-af2.png){height=50%，width=50%}

## 相關文章

{{af-submit-action}}
