---
title: 如何將最適化表單的資料提交至Microsoft&amp； reg； OneDrive？
description: 探索使用提交至OneDrive提交動作將AEM Forms與Microsoft&amp；reg； OneDrive連線的簡化流程。 瞭解設定OneDrive和設定提交動作以有效儲存及擷取資料的逐步指南
keywords: AEM Forms OneDrive整合，連線至Microsoft OneDrive，使用AEM Forms設定OneDrive設定
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 50%

---

# 將最適化表單提交至 Microsoft® OneDrive

「**[!UICONTROL 提交到 OneDrive]**」提交動作會將最適化表單連結到 Microsoft® OneDrive。您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Microsoft® OneDrive儲存體。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/aem-forms-submit-action.md)文章中進一步瞭解這些選項。

## 優點

AEM Forms與Microsoft® OneDrive無縫整合的一些優點包括：

* OneDrive的跨裝置協助工具可確保儲存的表單資料在不同平台上都能使用。 使用者可從桌上型電腦、筆記型電腦、平板電腦和行動裝置存取提交的資料、附件和檔案，進而增強協助工具與彈性。
* OneDrive與AEM Forms整合，提供穩定且可擴充的解決方案，有助於有效率地儲存資料。 所有最適化表單提交（例如檔案、附件和記錄檔案）都可方便地儲存在OneDrive中，確保資料有條理且可存取。

## 將OneDrive連線至最適化表單

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

設定OneDrive以提交AEM Forms，請執行以下步驟：

1. [建立 OneDrive 設定](#create-a-onedrive-configuration-create-onedrive-configuration)：將 AEM Forms 連接到您的 Microsoft® OneDrive 儲存空間。
2. [在最適化表單中使用提交至OneDrive提交動作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：它會將您的最適化表單連線到已設定的Microsoft® OneDrive。

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
   >* 建立一個資料夾做為 `forms-ootb-storage-adaptive-forms-submission`；如果尚未出現，請按一下「**建立資料夾**」。

現在，您可以使用此 OneDrive 儲存空間設定，在最適化表單中使用該提交動作。

### 在最適化表單中使用 OneDrive 設定 {#use-onedrive-configuartion-in-af}

您可以使用在最適化表單中建立的OneDrive儲存體設定，將資料或產生的記錄檔案儲存到OneDrive資料夾中。

>[!NOTE]
>
> * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
> * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

>[!BEGINTABS]

>[!TAB 基礎元件]

執行以下步驟，在以Foundation元件為基礎的最適化表單中使用OneDrive儲存設定，如下所示：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至OneDrive]**。
   ![OneDrive GIF](/help/forms/assets/wubmit-to-onedrive-fc.png){width=50%，height=50%}
您也可以在OneDrive中儲存記錄檔案(DoR)。
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

您提交表單時，資料將儲存在指定的 Microsoft® OneDrive 儲存空間。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

>[!TAB 核心元件]

執行以下步驟，根據核心元件在最適化表單中使用OneDrive儲存設定，如下所示：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至OneDrive]**。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
您也可以在OneDrive中儲存記錄檔案(DoR)。
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

>[!TAB 通用編輯器]

執行以下步驟，使用在Universal Editor中編寫的最適化表單中的OneDrive儲存體設定：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 若您在通用編輯器介面中沒有看到「**編輯表單屬性**」圖示，請在 Extension Manager 中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱 [Extension Manager 功能重點介紹](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用編輯器中啟用或停用擴充功能。
1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 提交至OneDrive]**。
   ![OneDrive GIF](/help/forms/assets/submit-to-onedrive-ue.png)
如果您選取**以原始名稱儲存附件**，則附件會使用其原始檔案名稱儲存在資料夾中。 您也可以將記錄檔案(DoR)儲存在Azure Blob儲存體中。
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**

>[!ENDTABS]

## 相關文章

{{af-submit-action}}
