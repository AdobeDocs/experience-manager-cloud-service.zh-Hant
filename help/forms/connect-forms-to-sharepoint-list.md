---
title: 如何在提交最適化表單時傳送資料至SharePoint清單儲存體？
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: 如何連線至最適化表單的SharePoint清單？、提交至SharePoint、建立SharePoint清單設定、在最適化表單中使用提交至SharePoint提交動作、連線最適化表單至Microsoft&reg； SharePoint清單。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="適用於AEM Forms)。"
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 0e5045b87719781301d91874c7355eda9426beef
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 22%

---

# 將最適化表單連線至® SharePoint清單 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

若要在最適化表單中使用[!UICONTROL 提交至SharePoint清單]提交動作：

1. [建立SharePoint清單設定](#1-create-a-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存體。
1. [在最適化表單中使用表單資料模型(FDM)提交](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：它會將您的最適化表單連線到已設定的® SharePoint。

## &#x200B;1. 建立SharePoint清單設定

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL ® SharePoint]**。
1. 選取一個&#x200B;**設定容器**。 設定會儲存在選取的設定容器中。
1. 從下拉式清單中按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]**。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。 如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。 以作者執行個體的 URL 取代 `[author-instance]`。
   * 在&#x200B;**® Graph**&#x200B;索引標籤中新增API許可權`offline_access`和`Sites.Manage.All`以提供讀取/寫入許可權。 在&#x200B;**Sharepoint**&#x200B;索引標籤中新增`AllSites.Manage`許可權，以便從遠端與SharePoint資料互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。 如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。 連結成功後，就會顯示 `Connection Successful` 訊息。
1. 從下拉式清單中選取&#x200B;**[!UICONTROL SharePoint網站]**&#x200B;和&#x200B;**[!UICONTROL SharePoint清單]**。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立® SharePointList的雲端設定。

### 憑證式驗證 {#certificate-based-authentication}

SharePoint清單設定的<span class="preview">憑證式驗證在早期採用者計畫下。 您可以使用官方電子郵件 ID 寫信至 aem-forms-ea@adobe.com，以加入早期採用者計劃並要求存取該功能。</span>

在SharePoint清單設定精靈中：

1. 將&#x200B;**[!UICONTROL 驗證型別]**&#x200B;設定為&#x200B;**憑證式驗證**。
1. 指定&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 使用者端識別碼]**、**[!UICONTROL 憑證別名]**、**[!UICONTROL 租使用者識別碼]**&#x200B;和&#x200B;**[!UICONTROL 租使用者名稱稱]**。
1. 輸入&#x200B;**[!UICONTROL SharePoint網站URL]**，視需要驗證網站連線，然後選取&#x200B;**[!UICONTROL SharePoint清單]**。
1. 按一下[連線]以驗證連線，然後按一下[儲存並關閉]以儲存組態。**&#x200B;**&#x200B;**&#x200B;**

以下熒幕擷圖顯示具有&#x200B;**憑證式驗證**&#x200B;的SharePoint清單組態：

![具有憑證式驗證的SharePoint清單組態](/help/forms/assets/sharepoint-list-certificate-auth-configuration.png){width=50%, height=50%, align=center}

若要為AEM和Microsoft Azure準備憑證，請在AEM中執行以下步驟，然後在Microsoft Azure中註冊公開憑證。

在AEM **中的**

1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
1. 搜尋&#x200B;**[!UICONTROL fd-cloudservice]**，選取使用者，然後按一下&#x200B;**[!UICONTROL 內容]**。
1. 開啟&#x200B;**[!UICONTROL 金鑰存放區]**&#x200B;索引標籤。 如果尚未建立金鑰存放區，請按一下&#x200B;**[!UICONTROL 建立金鑰存放區]**，並完成提示以設定金鑰存放區密碼。
1. 將私密金鑰新增至金鑰存放區：展開&#x200B;**[!UICONTROL 從金鑰存放區檔案新增私密金鑰]**&#x200B;並上傳您的&#x200B;**.jks**&#x200B;檔案。
1. 輸入符合SharePoint清單組態中&#x200B;**[!UICONTROL 憑證別名]**&#x200B;的&#x200B;**[!UICONTROL 別名]**，提交金鑰資料，然後按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

熒幕擷圖顯示新增憑證後的金鑰存放區。 **[!UICONTROL 別名]**&#x200B;必須符合SharePoint清單雲端設定中的&#x200B;**[!UICONTROL 憑證別名]**：

具有憑證別名![&#128279;](/help/forms/assets/fd-cloudservice-keystore-certificate.png){width=50%, height=50%, align=center}的fd-cloudservice使用者金鑰存放區

在Microsoft Azure中&#x200B;**&#x200B;**

1. 開啟您的應用程式註冊，並移至&#x200B;**憑證與密碼** > **憑證**。
1. 選取&#x200B;**上傳憑證**&#x200B;並上傳Azure必須信任該應用程式的憑證檔案（公開金鑰）。

熒幕擷圖顯示Azure入口網站中的&#x200B;**憑證**&#x200B;索引標籤，您可在此處上傳憑證以供應用程式註冊：

![Azure應用程式註冊憑證和密碼](/help/forms/assets/azure-app-registration-sharepoint-certificates.png){width=50%, height=50%, align=center}

## &#x200B;2. 在最適化表單中使用表單資料模型提交(FDM) {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單：

1. [使用® SharePoint清單設定建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)
1. [設定表單資料模型(FDM)以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立自適應表單](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表單資料模型(FDM)設定提交動作](/help/forms/using-form-data-model.md)

提交表單時，資料會儲存在指定的® Sharepoint清單儲存空間中。

>[!NOTE]
>
> ® SharePoint清單不支援下列欄型別：
>
> * 影像欄
> * 中繼資料欄
> * 人員欄
> * 外部資料欄

## 相關文章

{{af-submit-action}}
