---
title: 存取 Cloud Manager
description: 了解如何存取 Cloud Manager，以便您可以設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 4cad0ea1be4cba1c7f1af55cc760fb65fdc3cc4a
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 75%

---

# 存取 Cloud Manager {#cloud-resources}

在這部分的[上線歷程](overview.md)，您會了解如何存取 Cloud Manager，以便您可以設定專案資源。

## 目標 {#objective}

在此上線歷程的上一篇文章中，[將團隊成員指派給 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md)，您授予您的 AEMaaCS 團隊適當的角色。現在，瞭解如何存取Cloud Manager，以便您可以設定您的團隊打算使用的專案資源。

由於您完成了此歷程的上一步，您的團隊可以存取 Cloud Manager。Cloud Manager用於建立和管理您的專案資源，例如程式和環境。

閱讀本文件後，您應會了解：

* 系統管理員可指派給&#x200B;**業務所有者**，他通常也是系統管理員，並且必須是組織內第一個登入和存取 Cloud Manager 的角色。
* 如何登入 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。透過其專門建構的 CI/CD 管道支援具有企業開發設定的客戶，這些管道可確保進行徹底的測試和最高的程式碼品質，以提供卓越的體驗。Cloud Manager提供以自助方式開始所需的一切，包括建立雲端資源和環境的能力。

通常是指派給&#x200B;**業務負責人**&#x200B;產品設定檔負責新增您的雲端資源，例如程式和環境。 此人了解業務需求以及完成初始 Cloud Manager 設定的人員。

出於此上線歷程的目的，您作為系統管理員已經將自己指派到&#x200B;**業務所有者**&#x200B;產品設定檔，可以設定雲端資源。根據實際專案需求，業務所有者可能與系統管理員相同，也可能不同。

## 以系統管理員和業務所有者的身分存取 Cloud Manager {#access-sysadmin-bo}

在您指派給&#x200B;**業務負責人**&#x200B;角色的團隊成員可以存取Cloud Manager並開始建立雲端資源之前，必須為系統管理員指派&#x200B;**業務負責人**&#x200B;角色。 他們也必須像您在此上線歷程的前一步驟那樣登入 Cloud Manager。

1. 確保您以系統管理員身分獲指派&#x200B;**業務所有者**&#x200B;角色。

   回到上一步[將團隊成員指派給Cloud Manager產品設定檔](assign-profiles-cloud-manager.md)，以取得關於將&#x200B;**業務負責人**&#x200B;角色指派給系統管理員的詳細資訊。

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager。

您以&#x200B;**業務負責人**&#x200B;角色以系統管理員身分成功登入，就能以&#x200B;**業務負責人**&#x200B;角色初始化Cloud Manager，以供其他使用者使用。 您不會收到確認或任何訊息。只需登入就可以。

在您以&#x200B;**業務負責人**&#x200B;角色的系統管理員身分登入Cloud Manager之前，具有&#x200B;**業務負責人**&#x200B;角色的其他使用者無法在Cloud Manager中建立程式。 即使他們獲指派正確的角色，此規則也為真。

## 瀏覽至 Cloud Manager {#navigate-cloud-manager}

具有&#x200B;**業務所有者**&#x200B;角色的使用者將收到一封歡迎電子郵件，其中包含開始使用的連結。按照以下步驟使用此歡迎電子郵件瀏覽到 Cloud Manager。

1. 從你的歡迎電子郵件，按一下&#x200B;**開始使用**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 瀏覽到 Cloud Manager 的&#x200B;**程序和產品**&#x200B;頁面。

   >[!TIP]
   >
   >您也可以從以下位置直接瀏覽到 Cloud Manager 的登陸頁面`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。請將此頁面新增為書籤以供將來參考。

1. 您會被導向到 Cloud Manager 登陸頁面。

或者，您可以使用這些步驟從Cloud Manager首頁瀏覽到Adobe Experience Cloud的&#x200B;**程式和產品**&#x200B;頁面。

1. 直接瀏覽至的 [Adobe Experience Cloud](https://experience.adobe.com) 並使用您的 Adobe ID 憑證登入。

1. 在 Adobe Experience Cloud 首頁中，選取 **Experience Manager** 以開啟 AEM 首頁。

   ![Experience Cloud 首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 在 **Cloud Manager** 方磚中，選取&#x200B;**Launch**。

   ![AEM 首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登入後，您將被導向到 Cloud Manager 登陸頁面。請參閱[檢視 Cloud Manager 程序](#viewing-programs)了解更多詳情。

您如何透過 Cloud Manager 存取您的程序和產品取決於您，並且不會影響您如何使用 Cloud Manager 或您如何管理您的程序。

>[!NOTE]
>
>根據在 Cloud Manager 獲指派的角色和應用程式的狀態，您在使用 Cloud Manager 使用者介面時會看到不同的畫面。

## 檢視程序 {#viewing-programs}

成功存取 Cloud Manager 後，您所看到的畫面將取決於程序的狀態，如以下部分所述。

### 不存在程序時 {#no-programs}

如果您的組織中不存在任何程序，那麼您的登陸頁面會指導您建立您的第一個程序。

![無程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 已存在程序時 {#programs-exist}

如果您的組織中已經存在程序，那麼您的登陸頁面會顯示您現有的程序，並提供一個按鈕來新增其他程序。

![存在程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程序存在並且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中存在程式，並且您是系統管理員，那麼您的登入頁面將顯示&#x200B;**管理存取權**&#x200B;按鈕以及&#x200B;**新增程式**&#x200B;選項。

![系統管理員檢視](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 使用者驗證您的使用者角色 {#verify-user-roles}

成功登入 Cloud Manager 後，您可以驗證您是否已被指派&#x200B;**業務所有者**&#x200B;產品簡介。

1. 從窗口的右上角選擇您的個人資料。

1. 若要顯示指派給您使用者的角色，請選取&#x200B;**使用者角色**。

   ![使用者角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 該對話框應確認您的使用者擁有&#x200B;**業務所有者**&#x200B;角色。

   ![使用者角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已成功以業務所有者身份登入 Cloud Manager！如果您未指派&#x200B;**業務所有者**&#x200B;角色，請聯絡您的系統管理員。

## 下一步 {#whats-next}

現在您可以作為系統管理員存取 Cloud Manager，您可以建立您的第一個程序了。

接下來查看文件：[建立程序](create-program.md)來繼續您的上線歷程，您將在其中學習如何操作。

## 其他資源 {#additional-resources}

如果您想要此上線歷程以外的內容，以下是您可選擇的其他資源。

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 程序和環境。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
