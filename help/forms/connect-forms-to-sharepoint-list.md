---
title: 如何在提交最適化表單時傳送資料至SharePoint清單儲存體？
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: 如何連線至最適化表單的SharePoint清單？、提交至SharePoint、建立SharePoint清單設定、在最適化表單中使用提交至SharePoint提交動作、將最適化表單連線至Microsoft&amp；reg；SharePoint清單。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 30%

---

# 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

若要在最適化表單中使用[!UICONTROL 提交至SharePoint清單]提交動作：

1. [建立SharePoint清單設定](#1-create-a-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存體。
1. [在最適化表單中使用表單資料模型(FDM)提交](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：它會將您的最適化表單連線到已設定的Microsoft® SharePoint。

## 1.建立SharePoint清單設定

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 從下拉式清單中按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]**。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 在`offline_access`Microsoft® Graph`Sites.Manage.All`索引標籤中新增API許可權&#x200B;**和**&#x200B;以提供讀取/寫入許可權。 在`AllSites.Manage`Sharepoint **索引標籤中新增**&#x200B;許可權，以便從遠端與SharePoint資料互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。
1. 從下拉式清單中選取&#x200B;**[!UICONTROL SharePoint網站]**&#x200B;和&#x200B;**[!UICONTROL SharePoint清單]**。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立Microsoft® SharePointList的雲端設定。


## 2.在最適化表單中使用表單資料模型提交(FDM) {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單：

1. [使用Microsoft建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)
1. [設定表單資料模型(FDM)以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立自適應表單](/help/forms/creating-adaptive-form-core-components.md)
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
