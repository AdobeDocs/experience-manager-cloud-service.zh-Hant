---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: 如何連線SharePoint清單以取得最適化表單？、如何連線SharePoint檔案庫取得最適化表單、提交至SharePoint、建立SharePoint檔案庫組態、在最適化表單中使用提交至SharePoint提交動作、將最適化表單連線至Microsoft&reg； SharePoint清單。
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 34%

---


# 將最適化表單連線至Microsoft® SharePoint

此 **[!UICONTROL 提交至SharePoint]** 提交動作可讓您順暢地將最適化表單與Microsoft® SharePoint儲存空間連結。 它會在您提交表單後，將表單資料傳送至您選擇的SharePoint儲存空間。

AEMas a Cloud Service提供多種現成的提交動作，用於處理表單提交。 如需這些選項的詳細資訊，請參閱 [最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)  文章。

## 優點

從最適化表單提交資料給SharePoint儲存空間的一些優點包括：

* 它有助於將表單資料直接提交至SharePoint，提供一個集中位置來儲存和管理資訊。
* 藉由套用SharePoint的存取控制和許可權功能，可確保只有授權人員才能檢視或修改提交的資料。

使用 **[!UICONTROL 提交至SharePoint]**，您可以：

* [將最適化表單連線至SharePoint檔案庫](#connect-af-sharepoint-doc-library)
* [將最適化表單連線至SharePoint清單](#connect-af-sharepoint-list)

## 將最適化表單連線至SharePoint檔案庫 {#connect-af-sharepoint-doc-library}

若要使用 **[!UICONTROL 提交至SharePoint檔案庫]** 以最適化表單提交動作：

1. [建立SharePoint檔案庫組態](#create-a-sharepoint-configuration-create-sharepoint-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint儲存空間。
2. [使用最適化表單中的「提交到 SharePoint」提交動作](#use-sharepoint-configuartion-in-af)：會將您的最適化表單連結到已設定的 Microsoft® SharePoint。

### 建立SharePoint檔案庫組態 {#create-sharepoint-configuration}

若要將AEM Forms連線至您的Microsoft® Sharepoint檔案庫儲存空間：

1. 前往您的 **AEM Forms Author** 執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 一旦您選取 **[!UICONTROL Microsoft® SharePoint]**，您就會被重新導向至 **[!UICONTROL SharePoint瀏覽器]**.
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下 **[!UICONTROL 建立]** > **[!UICONTROL SharePoint檔案庫]** 下拉式清單中的。 此時會顯示 SharePoint 設定精靈。

   ![SharePoint 設定](/help/forms/assets/sharepoint_configuration.png)
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增 API 權限 `offline_access` 和 `Sites.Manage.All` 以提供讀取/寫入權限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

   >[!NOTE]
   >
   > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在，選取 **SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 根據預設， `forms-ootb-storage-adaptive-forms-submission` 出現在選取的SharePoint網站。
   >* 建立資料夾為 `forms-ootb-storage-adaptive-forms-submission`，如果尚未出現在 `Documents` 所選SharePoint網站的程式庫，方法是按一下 **建立資料夾**.

現在，您可以使用此SharePoint Sites設定，在最適化表單中執行提交動作。

### 在最適化表單中使用SharePoint檔案庫設定 {#use-sharepoint-configuartion-in-af}

您可以使用在最適化表單中建立的SharePoint檔案庫組態，將資料或產生的記錄檔案儲存在SharePoint資料夾中。 執行以下步驟，在最適化表單中使用SharePoint檔案庫儲存設定，如下所示：

1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 選取相同的 [!UICONTROL 設定容器] 最適化表單(您已在其中建立SharePoint檔案庫儲存空間)。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 SharePoint]**」。
   ![SharepointGIF](/help/forms/assets/sharedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

當您提交表單時，資料會儲存在指定的Microsoft® Sharepoint檔案庫儲存空間中。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

若要使用 [!UICONTROL 提交至SharePoint清單] 以最適化表單提交動作：

1. [建立SharePoint清單設定](#create-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存空間。
1. [在最適化表單中使用表單資料模型提交](#use-submit-using-fdm)：此動作會將您的最適化表單連線至設定的Microsoft® SharePoint。

### 建立SharePoint清單設定 {#create-sharepoint-list-configuration}

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下 **[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]** 下拉式清單中的。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增API許可權 `offline_access` 和 `Sites.Manage.All` 在 **Microsoft® Graph** 索引標籤以提供讀取/寫入許可權。 新增 `AllSites.Manage` 中的許可權 **Sharepoint** 索引標籤以與SharePoint資料進行遠端互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。
1. 選取 **[!UICONTROL SharePoint網站]** 和 **[!UICONTROL SharePoint清單]** 下拉式清單中的。
1. 選取 **[!UICONTROL 建立]** 以建立Microsoft® SharePointList的雲端設定。


### 在最適化表單中使用表單資料模型提交 {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單：

1. [使用Microsoft建立表單資料模型](/help/forms/create-form-data-models.md)
1. [設定表單資料模型以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表單資料模型設定提交動作](/help/forms/using-form-data-model.md)

提交表單時，資料會儲存在指定的Microsoft® Sharepoint清單儲存空間中。

>[!NOTE]
>
> Microsoft® SharePoint清單不支援下列欄型別：
* 影像欄
* 中繼資料欄
* 人員欄
* 外部資料欄

## 相關文章

{{af-submit-action}}