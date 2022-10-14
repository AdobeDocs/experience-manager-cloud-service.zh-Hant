---
title: 存取 Admin Console
description: 一旦您了解了上線所需的準備工作和 AEMaaCS 結構的基礎知識，您就可以首次登入 Admin Console 了。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 100%

---

# 存取 Admin Console {#accessing-admin-console}

在這部分[上線歷程，](overview.md)您將了解在首次登入系統之前所需的準備工作。

## 目標 {#objective}

既然你已經閱讀了這篇文章[AEM as a Cloud Service術語](terminology.md)並了解 AEMaaCS 結構的基礎知識，您就可以第一次登入 Admin Console 了！

作為系統管理員，您負責管理組織內的使用者。您可以使用 Admin Console 來執行此操作。閱讀本區段後，您應該：

* 了解什麼是 Adobe ID。
* 能夠登入 Admin Console。
* 了解如何透過 Admin Console 查看您作為系統管理員的權限。
* 了解如何联系 Adobe 支援以尋求幫助。

## Admin Console {#admin-console}

Adobe Admin Console 是管理您的 Adobe 產品授權和使用者的中心位置。Admin Console 允許您在單個位置而不是在各種單獨的解決方案中建立和管理使用者。

## Adobe ID {#adobe-id}

若要登入 Admin Console，您需要一個 Adobe ID。Adobe ID 是與特定電子郵件地址綁定的帳戶，需要登入和存取 AEM as a Cloud Service 或您的任何 Adobe 解決方案。透過使用您的 Adobe ID，您可以將所有 Adobe 計劃和產品與一個帳戶相關聯。

當您作為系統管理員在 Admin Console 中設定您的團隊時，您指定將用作 Adobe ID 的電子郵件地址。

有三種不同類型的 Adobe ID：

* **個人身份證件**：這是 Adobe ID 的預設類型，在 adobe.com 上建立。此帳戶由 Adobe 管理，任何人都可以建立此類帳戶。

* **Enterprise ID**：組織通常希望增加對使用者帳戶的控制。只有系統管理員可以建立 Enterprise ID，並且組織擁有這些帳戶，Adobe 僅作為主機。

* **Federated ID**：使用 Federated ID，組織可以完全擁有和控制帳戶。為此，您的組織需要將 Adobe Experience Cloud 與您的 SAML2 單點登入 (SSO) 系統整合。這允許使用者根據其組織的 SSO 系統而不是 Adobe 託管的帳戶進行身份驗證。

作為系統管理員，您可以決定在設定 Enterprise ID 或 Federated ID 之前使用個人 ID 將自己和您的團隊加入 AEM as a Cloud Service。設定 Enterprise ID 或 Federated ID 後，成員可以轉換為使用這些 ID。

## 登入 Admin Console {#steps-admin-console}

在您可以使用 Admin Console 管理團隊中的使用者之前，您需要確保您自己可以正確存取它並擁有適當的權限。

1. 作為系統管理員，您將在上線流程中收到來自 Adobe 的多封電子郵件。查找提供有關您已被授予存取權限的組織名稱資訊的歡迎電子郵件。

1. 點擊&#x200B;**開始使用**&#x200B;歡迎電子郵件中的鏈接以瀏覽到 Admin Console。如果找不到電子郵件，請直接打開瀏覽器存取 Admin Console，網址為 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

   ![歡迎電子郵件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用 Adobe ID 登入。登入成功後會看到&#x200B;**總覽** Adobe Admin Console 頁面。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您可以存取多個組織，請確保您已登入正確的組織。要更改您的組織，請單擊右上角的組織名稱，然後選擇您需要存取的所需組織。

   ![變更組織](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 選擇&#x200B;**管理員**&#x200B;來自&#x200B;**使用者**&#x200B;卡以驗證您是系統管理員。

   ![審視管理員](/help/journey-onboarding/assets/get-started2.png)

1. 一旦你點擊&#x200B;**管理員**&#x200B;來自&#x200B;**使用者**&#x200B;卡，您可以透過輸入您的 Adobe ID 電子郵件、使用者名、名字或姓氏進行搜索。

   ![搜尋使用者](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切正常，搜索將返回您的記錄。如果值在&#x200B;**管理員角色**&#x200B;列顯示&#x200B;**系統**，您知道您 (或顯示的使用者) 是系統管理員。

   ![系統狀態](/help/journey-onboarding/assets/get-started4.png)

恭喜你，系統管理員！

## Adobe Identity Management 系統 {#ims}

AEM as a Cloud Service預配置了 Adobe Identity Management 系統 (也稱為 IMS) 以進行身份驗證。作為系統管理員，您無需執行任何操作即可啟用此功能。

透過使用 IMS，AEM as a Cloud Service整合了 AEM 與 Adobe Experience Cloud 其餘部分之間的登入體驗。擁有多個 Adobe 產品的組織尤其受益於在 Admin Console 中建立基於角色的組，然後透過 IMS 指派對多個產品 (包括 AEM as a Cloud Service) 的存取權限。

您將在此入門歷程的下一部分中了解有關產品設定檔和指派使用者的更多資訊。

## 連絡 Adobe 支援人員 {#support}

如果您有任何問題，可以透過 Admin Console 存取 Adobe 支援。**支援**&#x200B;索引標籤可讓您透過簡單易用的界面存取各種 Adobe 支援功能。

![支援索引標籤](/help/journey-onboarding/assets/support-menu.png)

索引標籤允許您建立和管理案例、直接與 Adobe 客戶支援代表聊天以及安排與專家的會議。系統管理員和支援管理員必須登入才能存取支援案例和專家會話選項。

## 下一步 {#whats-next}

閱讀了本文件後，您應該：

* 了解什麼是 Adobe ID。
* 能夠登入 Admin Console。
* 了解如何透過 Admin Console 查看您作為系統管理員的權限。
* 了解如何聯絡 Adobe 支援以尋求幫助。

您已準備好透過學習如何繼續您的上線之旅[將團隊成員指派給 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md)以便您的同事也可以存取 AEMaaCS。

## 其他資源 {#additional-resources}

* [Admin Console 總覽](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)- Admin Console 的全面總覽
* [建立或更新您的 Adobe ID](https://helpx.adobe.com/tw/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - 了解如何建立、更改和管理多個 Adobe ID。
* [SAML 2.0 身份驗證處理程序](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=zh-Hant)- AEM 附帶 SAML 身份驗證處理程序。此處理程序使用 HTTP POST 綁定提供對 SAML 2.0 身份驗證請求協議（Web-SSO 設定檔）的支援。
* [管理職務](https://helpx.adobe.com/tw/enterprise/using/admin-roles.ug.html) - 使用 Adobe Admin Console，組織可以定義靈活的管理層次結構，以實現對 Adobe 產品存取和使用的精細管理。
* [支援和專家工作階段](https://helpx.adobe.com/tw/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - 了解如何存取 Admin Console 上的支援選項、管理您的支援案例、安排專家會議等。
