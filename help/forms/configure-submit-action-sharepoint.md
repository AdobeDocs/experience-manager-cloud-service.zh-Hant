---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: 如何連線SharePoint清單以取得最適化表單？、如何連線SharePoint檔案庫取得最適化表單、提交至SharePoint、建立SharePoint檔案庫組態、使用提交至SharePoint在最適化表單中的提交動作、連結最適化表單至Microsoft&amp；reg； SharePoint清單。
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: 「如何設定最適化表單的提交動作？」
role: User, Developer
source-git-commit: 5e1d08e82cafc3a8a715653727f42ce0048f2b1f
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 31%

---

# 將最適化表單連線至Microsoft® SharePoint

**[!UICONTROL 提交至SharePoint]**&#x200B;提交動作可讓您順暢地將最適化表單與Microsoft® SharePoint儲存體連線。 它會在您提交表單後，將表單資料傳送至您選擇的SharePoint儲存空間。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

## 優點

從最適化表單提交資料給SharePoint儲存空間的一些優點包括：

* 它有助於將表單資料直接提交至SharePoint，提供一個集中位置來儲存和管理資訊。
* 藉由套用SharePoint的存取控制和許可權功能，可確保只有授權人員才能檢視或修改提交的資料。

使用&#x200B;**[!UICONTROL 提交至SharePoint]**，您可以：

* [將最適化表單連線至SharePoint檔案庫](#connect-af-sharepoint-doc-library)
* [將最適化表單連線至SharePoint清單](#connect-af-sharepoint-list)

## 將最適化表單連線至SharePoint檔案庫 {#connect-af-sharepoint-doc-library}

若要以最適化表單使用&#x200B;**[!UICONTROL 提交至SharePoint檔案庫]**&#x200B;提交動作：

1. [建立SharePoint檔案庫組態](#create-a-sharepoint-configuration-create-sharepoint-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint儲存體。
2. [使用最適化表單中的「提交到 SharePoint」提交動作](#use-sharepoint-configuartion-in-af)：會將您的最適化表單連結到已設定的 Microsoft® SharePoint。

### 建立SharePoint檔案庫組態 {#create-sharepoint-configuration}

若要將AEM Forms連線至您的Microsoft® Sharepoint檔案庫儲存空間：

1. 前往您的&#x200B;**AEM Forms Author**&#x200B;執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**。
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

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在選取&#x200B;**SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 依預設，`forms-ootb-storage-adaptive-forms-submission`存在於選取的SharePoint網站。
   >* 按一下&#x200B;**建立資料夾**，將資料夾建立為`forms-ootb-storage-adaptive-forms-submission` (如果尚未存在於所選SharePoint網站的`Documents`資料庫中)。

現在，您可以使用此SharePoint Sites設定，在最適化表單中執行提交動作。

### 在最適化表單中使用SharePoint檔案庫設定 {#use-sharepoint-configuartion-in-af}

您可以使用在最適化表單中建立的SharePoint檔案庫組態，將資料或產生的記錄檔案儲存在SharePoint資料夾中。 執行以下步驟，在最適化表單中使用SharePoint檔案庫儲存設定，如下所示：

1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 為最適化表單選取相同的[!UICONTROL 設定容器]，您已在其中建立SharePoint檔案庫儲存空間。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 SharePoint]**」。
   ![SharepointGIF](/help/forms/assets/sharedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

當您提交表單時，資料會儲存在指定的Microsoft® Sharepoint檔案庫儲存空間中。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

若要在最適化表單中使用[!UICONTROL 提交至SharePoint清單]提交動作：

1. [建立SharePoint清單設定](#create-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存體。
1. [在最適化表單中使用表單資料模型(FDM)提交](#use-submit-using-fdm)：它會將您的最適化表單連線到已設定的Microsoft® SharePoint。

### 建立SharePoint清單設定 {#create-sharepoint-list-configuration}

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 從下拉式清單中按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]**。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 在&#x200B;**Microsoft® Graph**&#x200B;索引標籤中新增API許可權`offline_access`和`Sites.Manage.All`以提供讀取/寫入許可權。 在&#x200B;**Sharepoint**&#x200B;索引標籤中新增`AllSites.Manage`許可權，以便從遠端與SharePoint資料互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。
1. 從下拉式清單中選取&#x200B;**[!UICONTROL SharePoint網站]**&#x200B;和&#x200B;**[!UICONTROL SharePoint清單]**。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立Microsoft® SharePointList的雲端設定。


### 在最適化表單中使用表單資料模型提交(FDM) {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單：

1. [使用Microsoft建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)
1. [設定表單資料模型(FDM)以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表單資料模型(FDM)設定提交動作](/help/forms/using-form-data-model.md)

提交表單時，資料會儲存在指定的Microsoft® Sharepoint清單儲存空間中。

>[!NOTE]
>
> Microsoft® SharePoint清單不支援下列欄型別：
> * 影像欄
> * 中繼資料欄
> * 人員欄
> * 外部資料欄

## 相關文章

{{af-submit-action}}
