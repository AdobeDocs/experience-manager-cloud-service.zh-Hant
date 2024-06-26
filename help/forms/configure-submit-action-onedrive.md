---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: AEM Forms OneDrive整合，連線至Microsoft OneDrive，使用AEM Forms設定OneDrive設定
feature: Adaptive Forms, Core Components
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
title: 「如何設定最適化表單的提交動作？」
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 67%

---

# 將最適化表單提交至 Microsoft® OneDrive

「**[!UICONTROL 提交到 OneDrive]**」提交動作會將最適化表單連結到 Microsoft® OneDrive。您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Microsoft® OneDrive儲存體。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 如需這些選項的詳細資訊，請參閱 [最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)  文章。

## 優點

AEM Forms與Microsoft® OneDrive無縫整合的一些優點包括：

* OneDrive的跨裝置協助工具可確保儲存的表單資料在不同平台上都能使用。 使用者可從桌上型電腦、筆記型電腦、平板電腦和行動裝置存取提交的資料、附件和檔案，進而增強協助工具與彈性。
* OneDrive與AEM Forms整合，提供穩定且可擴充的解決方案，有助於有效率地儲存資料。 所有最適化表單提交（例如檔案、附件和記錄檔案）都可方便地儲存在OneDrive中，確保資料有條理且可存取。

## 將OneDrive連線至最適化表單

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

設定OneDrive以提交AEM Forms，請執行以下步驟：

1. [建立 OneDrive 設定](#create-a-onedrive-configuration-create-onedrive-configuration)：將 AEM Forms 連接到您的 Microsoft® OneDrive 儲存空間。
2. [在最適化表單中使用提交至OneDrive提交動作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：此動作會將您的最適化表單連線至設定的Microsoft® OneDrive。

### 建立 OneDrive 設定 {#create-onedrice-configuration}

若要將 AEM Forms 連結到您的 Microsoft® OneDrive 儲存空間：

1. 前往您的 **AEM Forms 作者**&#x200B;執行個體 >「**[!UICONTROL 工具]**」>「**[!UICONTROL 雲端服務]**」>「**[!UICONTROL Microsoft® OneDrive]**」。
1. 一旦您選取了「**[!UICONTROL Microsoft® OneDrive]**」，系統就會將您重新導向到「**[!UICONTROL OneDrive 瀏覽器]**」。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下「**[!UICONTROL 建立]**」。此時會顯示 OneDrive 設定精靈。

   ![OneDrive 設定畫面](/help/forms/assets/onedrive-configuration.png)

1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增 API 權限 `offline_access` 和 `Files.ReadWrite.All` 以提供讀取/寫入權限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

   >[!NOTE]
   >
   > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在，請選取「**[!UICONTROL OneDrive 容器]**」>「**[OneDrive 資料夾]**」以儲存資料。

   >[!NOTE]
   >
   >* 根據預設，`forms-ootb-storage-adaptive-forms-submission` 會顯示在 OneDrive 容器中。
   > * 建立一個資料夾做為 `forms-ootb-storage-adaptive-forms-submission`；如果尚未出現，請按一下「**建立資料夾**」。

現在，您可以使用此 OneDrive 儲存空間設定，在最適化表單中使用該提交動作。

### 在最適化表單中使用 OneDrive 設定 {#use-onedrive-configuartion-in-af}

您可以在最適化表單中使用建立的 OneDrive 儲存空間設定，將資料或產生的記錄文件儲存在 OneDrive 資料夾中。執行以下步驟，即可在最適化表單中使用 OneDrive 儲存空間設定：
1. 建立[最適化表單](/help/forms/creating-adaptive-form.md)。

   >[!NOTE]
   >
   > * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 OneDrive]**」。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

您提交表單時，資料將儲存在指定的 Microsoft® OneDrive 儲存空間。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 相關文章

{{af-submit-action}}
