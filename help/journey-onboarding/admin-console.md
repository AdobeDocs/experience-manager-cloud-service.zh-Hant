---
title: 訪問Admin Console
description: 一旦您瞭解了登錄所需的準備和AEMaaCS結構的基本知識，您就可以首次登錄Admin Console。
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---


# 訪問Admin Console {#accessing-admin-console}

在 [登機之旅，](overview.md) 在首次登錄系統之前，您將瞭解必要的準備情況。

## 目標 {#objective}

既然你讀過那篇文章 [AEMas a Cloud Service術語](terminology.md) 並瞭解AEMaaCS結構的基礎知識，您已準備好首次登錄Admin Console!

作為系統管理員，您負責管理組織內的用戶。 你用Admin Console。 閱讀此部分後，您應：

* 明白Adobe ID是什麼。
* 能夠登錄到Admin Console。
* 瞭解如何通過Admin Console查看您作為系統管理員的權限。
* 瞭解如何聯繫Adobe支援以獲得幫助。

## Admin Console {#admin-console}

Adobe Admin Console是管理和管理您的Adobe產品許可證和用戶的中心場所。 該Admin Console允許您在單個位置建立和管理用戶，而不是在各個解決方案中建立和管理用戶。

## Adobe ID {#adobe-id}

要登錄Admin Console，你需要一個Adobe ID。 而Adobe ID是一個與特定電子郵件地址綁定的帳戶，該地址是登錄和訪問as a Cloud Service或AEM您的任何Adobe解決方案所必需的。 通過使用您的Adobe ID，您可以保留與單個帳戶關聯的所有Adobe計畫和產品。

當您作為系統管理員在Admin Console中設定您的團隊時，您將指定將用作Adobe ID的電子郵件地址。

有三種類型的AdobeID:

* **個人ID**:這是預設類型的Adobe ID，建立於adobe.com。 此帳戶由Adobe管理，任何人都可以建立此類帳戶。

* **Enterprise ID**:組織通常希望加強對用戶帳戶的控制。 只有系統管理員才能建立企業ID，並且組織擁有這些帳戶，而Adobe僅充當主機。

* **Federated ID**:使用聯合ID，組織將完全擁有和控制帳戶。 為此，您的組織需要將Adobe Experience Cloud與SAML2單一登錄(SSO)系統整合。 這允許用戶根據其組織的SSO系統進行身份驗證，而不是通過Adobe托管的帳戶。

作為系統管理員，您可以決定在設定企業或聯合ID之AEM前，使用個人ID將您自己和您的團隊裝上as a Cloud Service。 建立企業或聯合ID後，可以將成員轉換為使用這些ID。

## 登錄到Admin Console {#steps-admin-console}

在使用Admin Console管理團隊內的用戶之前，您需要確保自己能夠正確訪問該組並擁有相應的權限。

1. 作為系統管理員，您將在登機過程中從Adobe接收多個電子郵件。 查找歡迎電子郵件，該電子郵件提供有關您已被授予訪問權限的組織名稱的資訊。

1. 按一下 **開始** 連結到歡迎電子郵件以導航到Admin Console。 如果找不到電子郵件，請直接開啟瀏覽器以Admin Console [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

   ![歡迎電子郵件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用 Adobe ID 登入。成功登錄後，您將看到 **概述** Adobe Admin Console。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您有權訪問多個組織，請確保您已登錄到正確的組織。 要更改組織，請按一下右上角的組織名稱，然後選擇需要訪問的所需組織。

   ![更改組織](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 選擇 **管理員** 從 **用戶** 卡以驗證您是系統管理員。

   ![查看管理員](/help/journey-onboarding/assets/get-started2.png)

1. 按一下後 **管理員** 從 **用戶** 卡，您可以通過輸入Adobe ID電子郵件、用戶名、名字或姓氏進行搜索。

   ![搜索用戶](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切正常，搜索將返回您的記錄。 如果 **管理員角色** 列顯示 **系統**，您知道您（或顯示的用戶）是系統管理員。

   ![系統狀態](/help/journey-onboarding/assets/get-started4.png)

恭喜，系統管理員！

## AdobeIdentity Management系統 {#ims}

AEMas a Cloud Service預配置了AdobeIdentity Management系統（也稱為IMS）進行身份驗證。 作為系統管理員，您無需執行任何操作即可啟用此功能。

通過使用IMS,AEMas a Cloud Service整合了在Adobe Experience Cloud和其AEM餘地區之間的登錄體驗。 具有多種Adobe產品的組織尤其受益，因為它在Admin Console中建立基於角色的組，然後通過IMS將訪問權分配給包括AEMas a Cloud Service在內的多種產品。

您將在本登機行程的下一部分瞭解有關產品配置檔案和分配用戶的更多資訊。

## 聯繫Adobe支援 {#support}

如果有任何問題，可通過Admin Console訪問Adobe支援。 的 **支援** 頁籤，通過簡單易用的介面訪問各種Adobe支援功能。

![支援頁籤](/help/journey-onboarding/assets/support-menu.png)

該頁籤允許您建立和管理案例、直接與Adobe客戶支援代表聊天以及安排與專家的會議。 系統管理員和支援管理員必須登錄才能訪問支援案例和專家會話選項。

## 下一步 {#whats-next}

現在您已閱讀了此文檔，您應：

* 明白什麼，Adobe ID。
* 能夠登錄到Admin Console。
* 瞭解如何通過Admin Console查看您作為系統管理員的權限。
* 瞭解如何聯繫Adobe支援以獲得幫助。

通過學習如何 [將團隊成員分配給Cloud Manager產品配置檔案](assign-profiles-cloud-manager.md) 這樣你的同事也能訪問AEMaCS。

## 其他資源 {#additional-resources}

* [Admin Console概述](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)  — 全面概述Admin Console
* [建立或更新您的Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)  — 瞭解如何建立Adobe ID、更改它並管理多個AdobeID。
* [SAML 2.0身份驗證處理程式](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html)  — 隨AEMSAML驗證處理程式一起提供。 此處理程式使用HTTPPOST綁定為SAML 2.0身份驗證請求協定（Web-SSO配置檔案）提供支援。
* [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html)  — 使用Adobe Admin Console，組織可以定義靈活的管理層次結構，從而對Adobe產品訪問和使用進行細粒度管理。
* [支援和專家會議](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)  — 瞭解如何訪問Admin Console上的支援選項、管理您的支援案例、安排專家會議等。
