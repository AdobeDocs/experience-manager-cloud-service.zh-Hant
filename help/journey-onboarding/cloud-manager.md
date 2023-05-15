---
title: 存取 Cloud Manager
description: 了解如何存取 Cloud Manager，以便您可以設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# 存取 Cloud Manager {#cloud-resources}

在 [入門旅程，](overview.md) 您會學習如何存取Cloud Manager，以便設定專案資源。

## 目標 {#objective}

在這次上線之旅的上一篇文章中，[將團隊成員指派給 Cloud Manager 產品設定檔，](assign-profiles-cloud-manager.md)您授予您的 AEMaaCS 團隊適當的角色。現在了解如何存取Cloud Manager，以便設定您的團隊使用的專案資源。

由於您完成了此歷程的上一步，您的團隊可以存取 Cloud Manager。Cloud Manager 用於建立和管理您的專案資源，例如程序和環境。

閱讀本檔案後，您應了解下列內容：

* 指派給 **業務負責人** 角色必須是您組織中第一個登入及存取Cloud Manager的人。
* 如何登入 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。透過其專門建構的 CI/CD 管道支援具有企業開發設定的客戶，這些管道可確保進行徹底的測試和最高的程式碼品質，以提供卓越的體驗。Cloud Manager 提供以自助方式開始所需的一切，包括建立雲端資源和環境的能力。

通常是指派給&#x200B;**業主**&#x200B;產品設定檔負責新增您的雲端資源，例如程序和環境。此人了解業務需求以及完成初始 Cloud Manager 設定的人員。

在上線歷程中，您身為系統管理員，已將自己指派給 **業務負責人** 產品設定檔，並可以設定雲端資源。 根據實際項目要求，業務所有者可能與系統管理員不同。

## Access Cloud Manager 可作為系統管理員和業主 {#access-sysadmin-bo}

在您指派給 **業務負責人** 角色可以存取cloud manager並開始建立雲端資源，必須指派系統管理員 **業務負責人** 角色。 他們也必須像您在此入門歷程的上一步步驟一樣登入Cloud Manager。

1. 確保您作為系統管理員擁有&#x200B;**業主**&#x200B;指派的角色。

   * 返回此歷程的上一步， [將團隊成員指派給Cloud Manager產品設定檔，](assign-profiles-cloud-manager.md) ，以了解有關分配 **業務負責人** 角色給系統管理員。

1. 登入 Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)並顯示正常的登陸頁面。

透過以系統管理員身份成功登入&#x200B;**業主**&#x200B;角色，您初始化 Cloud Manager 以供其他使用者使用&#x200B;**業主**&#x200B;角色。您未收到確認或任何訊息。 僅僅登錄就足夠了。

直到您以系統管理員身分登入Cloud Manager，並透過 **業務負責人** 角色，其他具有 **業務負責人** 角色無法在Cloud Manager中建立程式。 即使獲派正確角色，此規則仍為true。

## 瀏覽至 Cloud Manager {#navigate-cloud-manager}

具有 **業務負責人** 角色會收到歡迎電子郵件，內含要開始使用的連結。 按照以下步驟使用此歡迎電子郵件瀏覽到 Cloud Manager。

1. 在歡迎電子郵件中，按一下 **開始使用**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 導覽至Cloud Manager的 **計畫和產品** 頁面。

   >[!TIP]
   >
   >您也可以從以下位置直接瀏覽到 Cloud Manager 的登入頁面`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。將此頁面加入書籤，以供日後參考。

1. 系統會將您導向至Cloud Manager的登陸頁面。

您還可以按照以下步驟從 Adobe Experience Cloud 主頁瀏覽到 Cloud Manager 的&#x200B;**程序和產品**&#x200B;頁面。

1. 直接瀏覽至的 [Adobe Experience Cloud](https://experience.adobe.com) 並使用您的 Adobe ID 憑證登入。

1. 從Adobe Experience Cloud首頁，選取 **Experience Manager** 以開啟AEM首頁。

   ![Experience Cloud 首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 在 **Cloud Manager** 拼貼，選擇 **Launch**.

   ![AEM 首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登入後，系統會將您導向至Cloud Manager登陸頁面。 請參閱 [檢視Cloud Manager的方案](#viewing-programs) 以取得更多詳細資訊。

您如何透過 Cloud Manager 存取您的程序和產品取決於您，並且不會影響您如何使用 Cloud Manager 或您如何管理您的程序。

>[!NOTE]
>
>根據在Cloud Manager中指派的角色和應用程式的狀態，您在使用Cloud Manager使用者介面時會看到不同的畫面。

## 檢視程序 {#viewing-programs}

成功存取Cloud Manager後，您所看到的內容取決於程式的狀態，如下節所述。

### 不存在程序時 {#no-programs}

如果您的組織中不存在任何程序，那麼您的登入頁面會指導您建立您的第一個程序。

![無程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 已存在程序時 {#programs-exist}

如果方案存在於您的組織中，則您的登錄頁面會顯示您現有的方案，並提供可新增其他方案的按鈕。

![存在程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程序存在並且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中存在程式，且您是系統管理員，則會顯示您的登錄頁面 **管理存取** 按鈕 **添加程式** 選項。

![系統管理員檢視](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 使用者驗證您的使用者角色 {#verify-user-roles}

成功登入 Cloud Manager 後，您可以驗證您是否已被指派&#x200B;**業主**&#x200B;產品簡介。

1. 從窗口的右上角選擇您的個人資料。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 要顯示分配給用戶的角色，請選擇 **使用者角色**.

   ![使用者角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 該對話框應確認您的使用者擁有&#x200B;**業主**&#x200B;角色。

   ![使用者角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已成功以業主身份登入 Cloud Manager！如果您未指派&#x200B;**業主**&#x200B;角色，請聯絡您的系統管理員。

## 下一步 {#whats-next}

現在您可以作為系統管理員存取 Cloud Manager，您可以建立您的第一個程序了。

接下來檢閱檔案，繼續您的入門歷程 [建立方案](create-program.md) 你學會怎麼做。

## 其他資源 {#additional-resources}

如果您想要超越入門歷程的內容，以下是其他選用資源。

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 程序和環境。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
