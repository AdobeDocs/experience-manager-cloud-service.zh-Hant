---
title: 存取 Cloud Manager
description: 了解如何存取 Cloud Manager，以便您可以設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 0db48ef4c15b6ca530b2626f7078c7172c872fff
workflow-type: ht
source-wordcount: '909'
ht-degree: 100%

---

# 存取 Cloud Manager {#cloud-resources}

在這部分的[上線歷程](overview.md)，您會了解如何存取 Cloud Manager，以便您可以設定專案資源。

## 目標 {#objective}

在此上線歷程的上一篇文章中，[將團隊成員指派給 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md)，您授予您的 AEMaaCS 團隊適當的角色。現在，了解如何存取 Cloud Manager，讓您能夠設定團隊想要使用的專案資源。

由於您已完成此歷程的前一個步驟，您的團隊可以存取 Cloud Manager。您可以使用 Cloud Manager 來建立和管理專案資源，例如方案和環境。

閱讀本文件後，您應會了解：

* 系統管理員可指派給&#x200B;**業務所有者**，他通常也是系統管理員，並且必須是組織內第一個登入和存取 Cloud Manager 的角色。
* 如何登入 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。透過其專門建構的 CI/CD 管道支援具有企業開發設定的客戶，這些管道可確保進行徹底的測試和最高的程式碼品質，以提供卓越的體驗。Cloud Manager 為您提供以自助方式開始使用所需的一切，包括建立雲端資源和環境的能力。

通常會由指派至&#x200B;**業務所有者**&#x200B;產品設定檔的團隊成員負責新增您的雲端資源，例如方案和環境。此人員了解業務需求，也是完成初始 Cloud Manager 設定的人。

出於此上線歷程的目的，您作為系統管理員已經將自己指派到&#x200B;**業務所有者**&#x200B;產品設定檔，可以設定雲端資源。根據實際專案需求，業務所有者可能與系統管理員相同，也可能不同。

## 以系統管理員和業務所有者的身分存取 Cloud Manager {#access-sysadmin-bo}

在您指派至&#x200B;**業務所有者**&#x200B;角色的團隊成員可以存取 Cloud Manager 並開始建立雲端資源之前，必須先把&#x200B;**業務所有者**&#x200B;角色指派給系統管理員。他們也必須像您在此上線歷程的前一步驟那樣登入 Cloud Manager。

1. 確保您以系統管理員身分獲指派&#x200B;**業務所有者**&#x200B;角色。

   返回前一個步驟[對團隊成員指派 Cloud Manager 產品設定檔](assign-profiles-cloud-manager.md)，了解將&#x200B;**業務所有者**&#x200B;角色指派給系統管理員的詳細資訊。

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在快速存取分組中，按一下「**Experience Manager**」。
1. 在左側面板中，按一下「**Cloud Manager**」。

   ![主控台上的 Cloud Manager](/help/journey-onboarding/assets/consol-cloud-manager.png)

以具有&#x200B;**企業所有者**&#x200B;角色的系統管理員身分成功登入後，您即可使用供其他具有&#x200B;**企業所有者**&#x200B;角色的使用者使用的 Cloud Manager。您不會收到確認或任何訊息。只需登入就可以。

在您以具有&#x200B;**業務所有者**&#x200B;角色的系統管理員身分登入 Cloud Manager 之前，其他具有&#x200B;**業務所有者**&#x200B;角色的使用者無法在 Cloud Manager 中建立方案。即使他們獲指派正確的角色，此規則也為真。

## 瀏覽至 Cloud Manager {#navigate-cloud-manager}

具有&#x200B;**業務所有者**&#x200B;角色的使用者將收到一封歡迎電子郵件，其中包含開始使用的連結。按照以下步驟使用此歡迎電子郵件瀏覽到 Cloud Manager。

1. 從你的歡迎電子郵件，按一下&#x200B;**開始使用**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 瀏覽到 Cloud Manager 的&#x200B;**程序和產品**&#x200B;頁面。

   >[!TIP]
   >
   >您也可以從以下位置直接瀏覽到 Cloud Manager 的登陸頁面`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。請將此頁面新增為書籤以供將來參考。

1. 您會被導向到 Cloud Manager 登陸頁面。

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## 檢視方案 {#viewing-programs}

成功存取 Cloud Manager 後，您所會看到的畫面將取決於方案的狀態，詳情如以下區段所述。

### 不存在任何方案時 {#no-programs}

如果您的組織中不存在任何程序，那麼您的登陸頁面會指導您建立您的第一個程序。

![無程序](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### 已存在方案時 {#programs-exist}

如果您的組織中已經存在程序，那麼您的登陸頁面會顯示您現有的程序，並提供一個按鈕來新增其他程序。

![已存在方案](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### 已存在方案且您是系統管理員時 {#programs-exist-sysadmin}

若您的組織中擁有方案且您是系統管理員，那麼您的登陸頁面會顯示「**管理存取權**」按鈕，以及「**新增方案**」選項。

![系統管理員視圖](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## 驗證您的使用者角色 {#verify-user-roles}

成功登入 Cloud Manager 後，您即可驗證自己是否獲指派&#x200B;**企業所有者**&#x200B;產品設定檔。

1. 在頁面右上角一帶，按一下「**帳戶**」圖示。

1. 按一下「**使用者角色**」。

   ![使用者角色](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. 在「**使用者角色**」對話框中，確認您的使用者具有&#x200B;**企業所有者**&#x200B;角色。

   ![使用者角色清單](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

您已成功以企業所有者身分登入 Cloud Manager。若未獲指派&#x200B;**企業所有者**&#x200B;角色，請聯絡您的系統管理員。

## 後續步驟 {#whats-next}

現在您可以作為系統管理員存取 Cloud Manager，您可以建立您的第一個程序了。

接下來查看文件：[建立程序](create-program.md)來繼續您的上線歷程，您將在其中學習如何操作。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 程序和環境。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
