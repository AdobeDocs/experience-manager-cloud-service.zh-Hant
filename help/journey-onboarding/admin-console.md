---
title: 存取 Admin Console
description: 一旦您瞭解了上線所需的準備工作和AEM as a Cloud Service結構的基礎知識，您就可以首次登入Admin Console了。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 55%

---

# 存取 Admin Console {#accessing-admin-console}

在這部分的[上線歷程](overview.md)中，您會了解在首次登入系統之前所需的準備工作。

## 目標 {#objective}

既然您已經閱讀了 [AEM as a Cloud Service 術語](terminology.md)一文，並了解 AEMaaCS 結構的基礎知識，您就可以第一次登入 Admin Console 了！

作為系統管理員，您負責使用Admin Console管理組織內的使用者。 閱讀本區段後，您應該就能執行下列作業，

* 了解什麼是 Adobe ID。
* 能夠登入Admin Console。
* 瞭解如何透過Admin Console檢視您作為系統管理員的許可權。
* 了解如何聯絡 Adobe 支援以尋求幫助。

## 關於Admin Console {#admin-console}

Adobe Admin Console 是管理您的 Adobe 產品授權和使用者的中心位置。Admin Console 可讓您在單一位置而不是在各種單獨的解決方案中建立和管理使用者。

### Adobe ID {#adobe-id}

您需要一個 Adobe ID 才能登入 Admin Console。Adobe ID是與特定電子郵件地址繫結的帳戶，需要登入並存取AEM as a Cloud Service或任何Adobe解決方案。 透過使用您的Adobe ID，您可以將所有Adobe計畫和產品與單一帳戶建立關聯。

當您作為系統管理員在 Admin Console 中設定您的團隊時，您指定作為 Adobe ID 的電子郵件地址。

有三種不同類型的 Adobe ID：

* **個人識別碼**： Adobe ID的預設型別，建立於adobe.com。 由Adobe管理，任何人都能建立此型別的帳戶。

* **Enterprise ID**：組織通常想要增加對使用者帳戶的控制。 只有系統管理員可以建立 Enterprise ID，並且組織擁有這些帳戶，Adobe 僅作為主機。

* **Federated ID**：使用Federated ID，組織可以完全擁有和控制帳戶。 貴組織必須將Adobe Experience Cloud與SAML2單一登入(SSO)系統整合。 如此可讓使用者根據其組織的SSO系統而不是Adobe託管的帳戶進行驗證。

作為系統管理員，您可以使用個人ID將自己和您的團隊加入AEM as a Cloud Service。 請在準備好Enterprise ID或Federated ID之前完成此工作。 設定 Enterprise ID 或 Federated ID 後，成員可以轉換為使用這些 ID。

### 直接登入Admin Console {#steps-admin-console}

在您可以使用 Admin Console 管理團隊中的使用者之前，您需要確保您自己可以正確存取它並擁有適當的權限。

1. 作為系統管理員，您會在上線流程中收到來自Adobe的多封電子郵件。 查找提供有關您已被授予存取權限的組織名稱資訊的歡迎電子郵件。

1. 按一下歡迎電子郵件中的&#x200B;**開始使用**&#x200B;連結，以瀏覽至Admin Console。 如果找不到電子郵件，請直接開啟瀏覽器存取 Admin Console，網址為 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

   ![歡迎電子郵件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用 Adobe ID 登入。登入成功後，您會看到 Adobe Admin Console 的「**概觀**」頁面。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您可以存取多個組織，請確保您已登入正確的組織。 要更改您的組織，請按一下右上角的組織名稱，然後選擇您需要存取的所需組織。

   ![變更組織](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 選擇&#x200B;**管理員**&#x200B;來自&#x200B;**使用者**&#x200B;卡以驗證您是系統管理員。

   ![審視管理員](/help/journey-onboarding/assets/get-started2.png)

1. 按一下「**管理員**」(位在「**使用者**」卡片) 之後，您可以輸入您的 Adobe ID 電子郵件、使用者名稱、名字或姓氏進行搜尋。

   ![搜尋使用者](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切正常運作，搜尋會傳回您的記錄。 如果值在&#x200B;**管理員角色**&#x200B;列顯示&#x200B;**系統**，您知道您 (或顯示的使用者) 是系統管理員。

   ![系統狀態](/help/journey-onboarding/assets/get-started4.png)

恭喜你，系統管理員！

## 透過Experience Hub存取Admin Console  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md)是AEM的統一個人化首頁。 將AEM工具與Admin Console整合於一處。

顯示於Admin Console首頁的![Experience Hub選項](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**若要透過Experience Hub存取Admin Console：**

1. 按一下[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)開啟Experience Hub的首頁。

1. 在&#x200B;**快速存取**&#x200B;群組中，按一下&#x200B;[**Admin Console**](https://experience.adobe.com)。

## Adobe Identity Management 系統 {#ims}

AEM as a Cloud Service預配置了 Adobe Identity Management 系統 (也稱為 IMS) 以進行身份驗證。作為系統管理員，您不需要執行任何操作即可啟用此功能。

透過使用 IMS，AEM as a Cloud Service整合了 AEM 與 Adobe Experience Cloud 其餘部分之間的登入體驗。擁有許多Adobe產品的組織獲益最大。 在Admin Console中建立角色型群組，並透過IMS (例如AEM as a Cloud Service)授與產品存取權。

您可以透過此上線歷程的下一部分，了解有關產品設定檔和指派使用者的更多資訊。

## 聯絡Adobe支援 {#support}

如果您有任何問題，可以透過 Admin Console 存取 Adobe 支援。**支援**&#x200B;索引標籤可讓您透過簡單易用的界面存取各種 Adobe 支援功能。

![支援索引標籤](/help/journey-onboarding/assets/support-menu.png)

索引標籤可讓您建立和管理案例、直接與 Adobe 客戶支援代表聊天以及安排與專家的會議。系統管理員和支援管理員必須登入才能存取支援案例和專家會話選項。

## 後續步驟 {#whats-next}

閱讀本文件後，您應該：

* 了解什麼是 Adobe ID。
* 能夠登入Admin Console。
* 瞭解如何使用Admin Console檢視您作為系統管理員的許可權。
* 了解如何聯絡 Adobe 支援以尋求幫助。

您已準備好透過學習如何[將團隊成員指派給Cloud Manager產品設定檔](assign-profiles-cloud-manager.md)來繼續您的上線之旅，以便您的同事也可以存取AEMaaCS。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [Admin Console 概觀](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)- Admin Console 的全面概觀
* [建立或更新您的 Adobe ID](https://helpx.adobe.com/tw/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - 了解如何建立、更改和管理多個 Adobe ID。
* [SAML 2.0 身份驗證處理程序](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#)- AEM 附帶 SAML 身份驗證處理程序。此處理程序使用 HTTP POST 綁定提供對 SAML 2.0 身份驗證請求協議（Web-SSO 設定檔）的支援。
* [管理職務](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html) - 使用 Adobe Admin Console，組織可以定義靈活的管理層次結構，以實現對 Adobe 產品存取和使用的精細管理。
* [支援和專家工作階段](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) — 瞭解如何存取Admin Console上的支援選項、管理您的支援案例、安排專家會議等。
