---
title: 存取Admin Console
description: 了解上線所需的準備工作，以及AEMaaCS結構的基本概念後，您就可以第一次登入Admin Console。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---

# 存取Admin Console {#accessing-admin-console}

在 [入門旅程，](overview.md) 您將先了解必要的準備，然後才能首次登入系統。

## 目標 {#objective}

既然你已經讀了那篇文章 [AEMas a Cloud Service術語](terminology.md) 了解AEMaaCS結構的基本概念，您就可以第一次登入Admin Console了！

身為系統管理員，您負責管理組織內的使用者。 您可以使用Admin Console來完成此操作。 閱讀本小節後，您應：

* 了解什麼是Adobe ID。
* 能夠登入Admin Console。
* 了解如何透過Admin Console檢閱您身為系統管理員的權限。
* 了解如何聯絡Adobe支援以取得協助。

## Admin Console {#admin-console}

Adobe Admin Console是管理和管理Adobe產品授權和使用者的中央位置。 此Admin Console可讓您在單一位置建立和管理使用者，而非在各種個別解決方案中。

## Adobe ID {#adobe-id}

若要登入Admin Console，您需要Adobe ID。 而Adobe ID是系結至特定電子郵件地址的帳戶，登入及存取AEMas a Cloud Service或任何您的Adobe解決方案都需要此地址。 使用Adobe ID，即可將所有Adobe計畫和產品保留在單一帳戶中。

當您是系統管理員，在Admin Console中設定您的團隊時，您會指定要用作Adobe ID的電子郵件地址。

AdobeID有三種類型：

* **個人ID**:這是預設的Adobe ID類型，建立於adobe.com。 此帳戶由Adobe管理，任何人都可以建立此類型的帳戶。

* **Enterprise ID**:組織通常想要提高對使用者帳戶的控制。 只有系統管理員可以建立企業ID，且組織擁有這些帳戶，且Adobe僅作為主機。

* **Federated ID**:透過同盟ID，組織將擁有帳戶的完整所有權和控制權。 若要這麼做，您的組織需要將Adobe Experience Cloud與SAML2單一登入(SSO)系統整合。 這可讓使用者根據其組織的SSO系統(而非由Adobe托管的帳戶)進行驗證。

身為系統管理員，您可以決定在設定企業ID或同盟ID之前，使用個人ID將您自己和您的團隊上線至AEMas a Cloud Service。 設定Enterprise ID或Federated ID後，即可使用這些ID將成員轉換為。

## 登入Admin Console {#steps-admin-console}

使用Admin Console來管理團隊內的使用者之前，您必須確保自己可以正確存取並擁有適當的權限。

1. 身為系統管理員，您會在上線程中收到來自Adobe的多封電子郵件。 尋找歡迎電子郵件，其中提供您有權存取之組織名稱的相關資訊。

1. 按一下 **開始使用** 在歡迎電子郵件中連結，導覽至Admin Console。 如果您找不到電子郵件，請直接開啟瀏覽器以Admin Console [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![歡迎電子郵件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用 Adobe ID 登入。成功登入後，您會看到 **概述** 頁面。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您有多個組織的存取權，請確定您已登入正確的組織。 若要變更組織，請按一下右上角的組織名稱，然後選擇您需要存取的必要組織。

   ![變更組織](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 選擇 **管理員** 從 **使用者** 用於驗證您是系統管理員的卡。

   ![檢閱管理員](/help/journey-onboarding/assets/get-started2.png)

1. 按一下 **管理員** 從 **使用者** 卡片，您可以輸入Adobe ID電子郵件、使用者名稱、名字或姓氏進行搜尋。

   ![搜尋使用者](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切正常運作，搜尋會傳回您的記錄。 若 **管理員角色** 欄顯示 **系統**，您（或顯示的使用者）是系統管理員。

   ![系統狀態](/help/journey-onboarding/assets/get-started4.png)

恭喜，系統管理員！

## AdobeIdentity Management系統 {#ims}

AEMas a Cloud Service已預先設定AdobeIdentity Management系統（亦稱為IMS）以進行驗證。 您無需以系統管理員身分來啟用此功能。

透過使用IMS,AEM as a Cloud Service整合AEM與其餘Adobe Experience Cloud之間的登入體驗。 具有多個Adobe產品的組織尤其能從中受益，方法是在Admin Console中建立以角色為基礎的群組，然後透過IMS指派對多個產品(包括AEM as a Cloud Service)的存取權。

您將在此入門歷程的下一個階段，進一步了解產品設定檔和指派使用者。

## 聯絡Adobe支援 {#support}

如果您有任何問題，可透過Admin Console存取Adobe支援。 此 **支援** 標籤可讓您透過簡單且簡單易用的介面存取各種Adobe支援功能。

![支援標籤](/help/journey-onboarding/assets/support-menu.png)

此索引標籤可讓您建立和管理案例、直接與Adobe客戶支援代表聊天，以及排程與專家的會議。 系統管理員和支援管理員必須登入才能存取支援案例和專家工作階段選項。

## 下一步 {#whats-next}

現在您已閱讀本檔案，您應：

* 了解什麼和Adobe ID。
* 能夠登入Admin Console。
* 了解如何透過Admin Console檢閱您身為系統管理員的權限。
* 了解如何聯絡Adobe支援以取得協助。

您已準備好透過學習如何 [將團隊成員指派給Cloud Manager產品設定檔](assign-profiles-cloud-manager.md) 讓您的同事也能存取AEMaCS。

## 其他資源 {#additional-resources}

* [Admin Console概述](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)  — 全面概述Admin Console
* [建立或更新您的Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)  — 了解如何建立Adobe ID、變更及管理多個AdobeID。
* [SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM隨附SAML驗證處理常式。 此處理常式支援使用HTTPPOST捆綁的SAML 2.0驗證要求通訊協定（Web-SSO設定檔）。
* [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html)  — 使用Adobe Admin Console，組織可以定義彈性的管理階層，以便對Adobe產品存取和使用進行微調管理。
* [支援與專家會議](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)  — 了解如何存取Admin Console上的支援選項、管理您的支援案例、排程專家座談會等。
