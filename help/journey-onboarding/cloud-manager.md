---
title: 存取Cloud Manager
description: 了解如何存取Cloud Manager，以便設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# 存取Cloud Manager {#cloud-resources}

在 [入門旅程，](overview.md) 您將學習如何存取Cloud Manager，以便設定專案資源。

## 目標 {#objective}

在上一篇入門歷程中， [將團隊成員指派給Cloud Manager產品設定檔，](assign-profiles-cloud-manager.md) 您已授予AEMaaCS團隊適當的角色。 現在了解如何存取Cloud Manager，以便設定您的團隊將使用的專案資源。

由於您已完成此歷程的上一步，因此您的團隊可以存取Cloud Manager。 Cloud Manager可用來建立及管理專案資源，例如方案和環境。

閱讀本檔案後，您應了解：

* 指派給 **業務負責人** 角色必須是貴組織中第一個登入及存取Cloud Manager的人。
* 如何登入Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，是您團隊的單一進入點。 它透過專門建立的CI/CD管道，為擁有企業開發設定的客戶提供支援，這些管道可確保徹底的測試和最高的程式碼品質，以提供絕佳的體驗。 Cloud Manager提供以自助方式開始使用所需的一切，包括建立雲端資源和環境的能力。

通常指派給 **業務負責人** 產品設定檔負責新增雲端資源，例如程式和環境。 此人了解業務需求，以及完成初始Cloud Manager設定的人員。

在上線歷程中，您身為系統管理員，已將自己指派給 **業務負責人** 產品設定檔和將設定雲端資源。 根據實際項目要求，業務所有者可能與系統管理員不同。

>[!NOTE]
>
>依預設，具有AEM環境存取權的使用者也會擁有「雲端>管理員」使用者角色。 此角色本身和本身不足以讓使用者存取方案詳細資料檢視。 只有Cloud Manager使用者角色的這類使用者，可透過方案功能表選項導覽至AEM環境製作URL（如果存在環境）。 如果這些用戶希望獲得程式級訪問權限，則必須與其管理員聯繫。

## 以系統管理員和業務擁有者身分存取Cloud Manager {#access-sysadmin-bo}

在您指派給 **業務負責人** 角色可以存取cloud manager並開始建立雲端資源，必須指派系統管理員 **業務負責人** 角色和登入Cloud Manager的方式，如您在此入門歷程的上一步所述。

1. 確保您作為系統管理員 **業務負責人** 已指派角色。

   * 返回此歷程的上一步， [將團隊成員指派給Cloud Manager產品設定檔，](assign-profiles-cloud-manager.md) ，以了解有關分配 **業務負責人** 角色（如果尚未完成）。

1. 登入Cloud Manager的網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並顯示一般登陸頁面。

以系統管理員的身分成功登入 **業務負責人** 角色，您可以初始化Cloud Manager，供其他使用者搭配 **業務負責人** 角色。 您不會收到此訊息或任何訊息的確認訊息。 只需簽入即可。

直到您以系統管理員身分登入Cloud Manager，並透過 **業務負責人** 角色，其他具有 **業務負責人** 即使已指派正確的角色，角色仍無法在Cloud Manager中建立程式。

## 導覽至Cloud Manager {#navigate-cloud-manager}

具有 **業務負責人** 角色會收到歡迎電子郵件，內含要開始的連結。 請依照下列步驟，使用這封歡迎電子郵件導覽至Cloud Manager。

1. 從歡迎電子郵件按一下 **開始使用**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 您將導覽至Cloud Manager的 **計畫和產品** 頁面。

   >[!TIP]
   >
   >您也可以從以下位置直接導覽至Cloud Manager的登入頁面： `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. 請將此頁面加入書籤，以供日後參考。

1. 系統會將您導向至Cloud Manager的登陸頁面。

或者，您也可以導覽至Cloud Manager的 **方案和產品** 依照下列步驟從Adobe Experience Cloud首頁開始頁面

1. 直接導覽至 [Adobe Experience Cloud](https://experience.adobe.com) 並使用Adobe ID登入。

1. 從Adobe Experience Cloud首頁，選取 **Experience Manager**.

   ![Experience Cloud首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 這會帶您前往AEM首頁。 按一下這裡 **Launch** 在 **Cloud Manager** 方塊。

   ![AEM首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登入後，系統會將您導向至Cloud Manager的登陸頁面。 請參閱 [檢視Cloud Manager的方案](#viewing-programs) 一節以取得詳細資訊。

如何透過Cloud Manager存取您的方案和產品取決於您，且對您使用Cloud Manager的方式或管理方式無影響。

>[!NOTE]
>
>根據在Cloud Manager中指派的角色和應用程式的狀態，您在使用Cloud Manager UI時會看到不同的畫面。

## 查看程式 {#viewing-programs}

成功存取Cloud Manager後，您所看到的內容將取決於您的程式狀態，如下節所述。

### 當沒有程式時 {#no-programs}

如果您的組織中沒有任何方案，您的登陸頁面會引導您建立第一個方案。

![無程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 程式已存在時 {#programs-exist}

如果程式已存在於您的組織中，您的登錄頁面會顯示您現有的程式，並提供可新增其他程式的按鈕。

![存在程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程式存在且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中已存在程式，且您是系統管理員，則會顯示您的登錄頁面 **管理存取** 按鈕 **添加程式** 選項。

![系統管理員視圖](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 驗證您的使用者角色 {#verify-user-roles}

成功登入Cloud Manager後，您可以確認您已獲派 **業務負責人** 產品設定檔。

1. 從視窗右上角選取您的設定檔。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 選擇 **使用者角色** 來顯示指派給您使用者的角色。

   ![使用者角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 對話方塊應確認您的使用者具有 **業務負責人** 角色。

   ![用戶角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您以業務擁有者身分成功登入Cloud Manager! 若您未獲指派 **業務負責人** 角色，請與您的系統管理員聯繫。

## 下一步 {#whats-next}

現在，您可以以系統管理員的身分存取Cloud Manager，您就可以建立第一個方案了。

您應繼續進行上線歷程，繼續檢閱此檔案 [建立方案](create-program.md) 你將學習如何做到。

## 其他資源 {#additional-resources}

請依照其他資源了解：

* [Cloud Manager簡介](/help/onboarding/cloud-manager-introduction.md)  — 了解Cloud Manager、Cloud Manager程式和環境。
