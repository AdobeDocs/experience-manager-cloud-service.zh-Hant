---
title: 如何使用授權範圍設定具有有限存取權的SharePoint網站？
description: 瞭解如何使用授權範圍以有限存取權設定SharePoint網站。
keywords: 如何設定具有有限存取權的SharePoint網站？、設定具有有限存取權的SharePoint、使用授權範圍來限制SharePoint網站的存取權。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 13%

---

# 使用授權範圍設定 SharePoint 網站，使其擁有有限的存取權

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

有限或受限存取的目的是透過允許管理員控制使用者對特定SharePoint網站或一組SharePoint網站的存取來增強安全管理。 當您需要授予使用者或群組存取特定網站的許可權，而不允許他們檢視任何其他不允許的SharePoint網站時，許可權層級就十分實用。

## 以有限存取權設定SharePoint Site的優勢

提供SharePoint網站有限存取權的好處：

* **增強式安全性**：透過限制存取權，您可以確保只有授權人員才能檢視或操控敏感資訊，減少未經授權存取的風險。

* **最低許可權原則**：它為使用者提供執行其工作功能所需的最低存取層級（或許可權）。 如此一來，每位使用者所暴露的網路敏感部分便能降至最低，避免潛在內部威脅。

* **資料保護**：限制存取有助於保護重要資料免於洩露。 這可確保只有需要檢視資料的使用者才能存取資料，這對於遵守資料保護法規至關重要。

* **預防意外資料遺失**：因為能夠修改內容的人越來越少，所以重要資料意外刪除或變更的機率就會大幅降低。

* **控制的資料流程**：這有助於控制組織內外的資訊流程，確保資料不會落入不法之徒手中。

## 使用授權範圍以有限存取權設定SharePoint

請依照下列步驟，使用授權範圍將SharePoint Sites設定為具有有限存取權：

1. [建立應用程式，使用 &#x200B;](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [在AEM執行個體設定授權範圍](#set-the-authorization-scope-at-aem-instance)

### 在Azure入口網站中建立具有有限許可權的應用程式

在Microsoft的Graph API中，以[許可權範圍在](https://portal.azure.com/#home)Microsoft Azure入口網站`Sites.Selected`中建立應用程式。

![SharePoint選取的網站](/help/forms/assets/sharepoint-selected-site.png)

如需如何擷取`Client ID`之`Client Secret`、`Tenant ID`和`OAuth URL`的相關資訊，請參閱[Microsoft®檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
* 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
* 在Microsoft的Graph API中新增`offline_access`和`Sites.Selected`許可權範圍，以提供受限制的網站存取權。
* 針對OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

若要使用`Sites.Selected` API許可權，必須在Azure入口網站中註冊的應用程式，並為SharePoint Online Sites設定適當的許可權。 此設定可確保應用程式擁有必要授權，可在定義的範圍內與SharePoint網站互動，從而提供所需的有限存取權。

請參考[部落格 — 開發使用Sites的應用程式。SPO網站的選取許可權](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476)，瞭解開發使用SharePoint Online Sites `Sites.Selected`許可權的應用程式的說明。

### 在AEM執行個體設定授權範圍

若要提供對Microsoft SharePoint網站的有限存取，必須正確設定授權範圍。 若要設定授權範圍並將AEM Forms連線至您的Microsoft® SharePoint儲存空間：

1. 前往您的&#x200B;**AEM Forms作者**&#x200B;執行個體> **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 選取&#x200B;**[!UICONTROL Microsoft® SharePoint]**&#x200B;後，系統會將您重新導向至&#x200B;**[!UICONTROL SharePoint瀏覽器]**。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 從下拉式清單中按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL SharePoint檔案庫]**。 此時會顯示 SharePoint 設定精靈。

   ![SharePoint網站有限網站存取權](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. 指定&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 使用者端識別碼]**&#x200B;和&#x200B;**[!UICONTROL 使用者端密碼]**。 如需如何擷取使用者端ID和使用者端密碼的詳細資訊，請參閱[Microsoft®檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。

1. 使用OAuth URL做為`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

   >[!NOTE]
   >
   > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 在`offline_access Sites.Selected`欄位中新增`Authorization Scope`。 當您在`offline_access Sites.Selected`文字方塊欄位中新增`Authorization Scope`範圍時，`SharePoint Site ID`文字方塊會顯示在畫面上。

1. 指定SharePoint網站ID。 若要瞭解如何擷取SharePoint網站ID，請參閱[額外位元組](#extra-bytes)區段。

1. 按一下&#x200B;**[!UICONTROL 檢查站台連線]**。 連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在選取&#x200B;**SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 依預設，`forms-ootb-storage-adaptive-forms-submission`存在於選取的SharePoint網站。
   >* 按一下`forms-ootb-storage-adaptive-forms-submission`建立資料夾`Documents`，將資料夾建立為&#x200B;**(如果尚未存在於所選SharePoint網站的**&#x200B;資料庫中)。

現在，您可以在最適化表單[中針對提交動作使用此](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af)SharePoint Sites設定。

## 額外的位元組

若要擷取`SharePoint Site ID`的值：
1. 移至[Microsoft Graph Explorer API](https://developer.microsoft.com/en-us/graph/graph-explorer)。
1. 在左窗格的`SharePoint Sites` API底下，按一下`Search for a SharePoint site by keyword`。
1. 將預留位置`contoso`取代為SharePoint網站的實際名稱，以擷取對應的網站識別碼。

   ![SharePoint檔案庫ID](/help/forms/assets/sharepoint-site-id.png)

按一下`Run Query`按鈕後，熒幕上會顯示網站ID。
