---
title: 存取 Cloud Manager
description: 了解如何存取 Cloud Manager，以便您可以設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 69ac8e444a0f22649b48ec25b549ad60858f8b1b
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 97%

---

# 存取 Cloud Manager {#cloud-resources}

在這部分[上線歷程，](overview.md)您將學習如何存取 Cloud Manager，以便您可以設定專案資源。

## 目標 {#objective}

在這次上線之旅的上一篇文章中，[將團隊成員指派給 Cloud Manager 產品設定檔，](assign-profiles-cloud-manager.md)您授予您的 AEMaaCS 團隊適當的角色。現在了解如何存取 Cloud Manager，以便您設定團隊將使用的專案資源。

由於您完成了此歷程的上一步，您的團隊可以存取 Cloud Manager。Cloud Manager 用於建立和管理您的專案資源，例如計劃和環境。

閱讀本文件後，您應會了解：

* 系統管理員可指派給&#x200B;**業務負責人**，他通常也是系統管理員，並且必須是組織內第一個登入和存取 Cloud Manager 的角色。
* 如何登入 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。透過其專門建構的 CI/CD 管道支援具有企業開發設定的客戶，這些管道可確保進行徹底的測試和最高的計劃碼品質，以提供卓越的體驗。Cloud Manager 提供以自助方式開始所需的一切，包括建立雲端資源和環境的能力。

通常是指派給&#x200B;**業主**&#x200B;產品設定檔負責新增您的雲端資源，例如計劃和環境。此人了解業務需求以及完成初始 Cloud Manager 設定的人員。

出於此上線歷程的目的，您作為系統管理員已經將自己指派到&#x200B;**業主**&#x200B;產品設定檔，並將設定雲端資源。根據實際項目需求，業務所有者可能與系統管理員相同，也可能不同。

## Access Cloud Manager 可作為系統管理員和業主 {#access-sysadmin-bo}

在您指派給&#x200B;**業主**&#x200B;角色可以存取 cloud manager 並開始建立 cloud 資源，必須為系統管理員指派&#x200B;**業主**&#x200B;角色並登入到 Cloud Manager，就像您在此上線過程中的上一步中所做的那樣。

1. 確保您作為系統管理員擁有&#x200B;**業主**&#x200B;指派的角色。

   * 回到這個歷程的上一步，[將團隊成員指派給 Cloud Manager 產品設定檔，](assign-profiles-cloud-manager.md)有關指派的更多資訊&#x200B;**業主**&#x200B;如果您尚未執行此操作，請授予系統管理員角色。

1. 登入 Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)並顯示正常的登陸頁面。

透過以系統管理員身份成功登入&#x200B;**業主**&#x200B;角色，您初始化 Cloud Manager 以供其他使用者使用&#x200B;**業主**&#x200B;角色。您將不會收到對此或任何消息的確認。只需登入就足夠了。

直到您使用系統管理員身份登入 Cloud Manager **業主**&#x200B;角色，其他使用者具有&#x200B;**業主**&#x200B;即使指派了正確的角色，角色也無法在 Cloud Manager 中建立程序。

## 瀏覽至 Cloud Manager {#navigate-cloud-manager}

使用者與&#x200B;**業主**&#x200B;角色將收到一封歡迎電子郵件，其中包含開始使用的連結。按照以下步驟使用此歡迎電子郵件瀏覽到 Cloud Manager。

1. 從你的歡迎電子郵件點擊&#x200B;**開始使用**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 您將瀏覽到 Cloud Manager 的&#x200B;**計劃和產品**&#x200B;頁。

   >[!TIP]
   >
   >您也可以從以下位置直接瀏覽到 Cloud Manager 的登入頁面`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。請將此頁面新增為書籤以供將來參考。

1. 您將被定向到 Cloud Manager 的登陸頁面。

您還可以按照以下步驟從 Adobe Experience Cloud 主頁瀏覽到 Cloud Manager 的&#x200B;**程序和產品**&#x200B;頁面。

1. 直接瀏覽至的 [Adobe Experience Cloud](https://experience.adobe.com) 並使用您的 Adobe ID 憑證登入。

1. 在 Adobe Experience Cloud 主頁中，選擇 **Experience Manager**。

   ![Experience Cloud 首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 這將帶您進入 AEM 主頁。從這裡，點擊&#x200B;**發射**&#x200B;在 **Cloud Manager** 磚塊。

   ![AEM 首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登入後，您將被引導至雲管理器的登入頁面。看[查看 Cloud Manager 的程序](#viewing-programs)部分了解更多詳情。

您如何透過 Cloud Manager 存取您的程序和產品取決於您，並且不會影響您如何使用 Cloud Manager 或您如何管理您的程序。

>[!NOTE]
>
>根據 Cloud Manager 中指派的角色和應用程序的狀態，您在使用 Cloud Manager UI 時會看到不同的畫面。

## 檢視計畫 {#viewing-programs}

成功存取 Cloud Manager 後，您所看到的將取決於程序的狀態，如以下部分所述。

### 不存在計畫時 {#no-programs}

如果您的組織中不存在任何計劃，那麼您的登入頁面會指導您建立您的第一個計劃。

![無計劃](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 已存在計畫時 {#programs-exist}

如果您的組織中已經存在計劃，那麼您的登入頁面會顯示您現有的計劃，並提供一個按鈕來新增其他計劃。

![存在計劃](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程序存在並且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中已經存在程序並且您是系統管理員，那麼您的登入頁面將顯示&#x200B;**管理 Access**&#x200B;按鈕連同&#x200B;**新增程序**&#x200B;選項。

![系統管理員檢視](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 使用者驗證您的使用者角色 {#verify-user-roles}

成功登入 Cloud Manager 後，您可以驗證您是否已被指派&#x200B;**業主**&#x200B;產品簡介。

1. 從窗口的右上角選擇您的個人資料。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 選擇&#x200B;**使用者角色**&#x200B;顯示指派給您的使用者的角色。

   ![使用者角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 該對話框應確認您的使用者擁有&#x200B;**業主**&#x200B;角色。

   ![使用者角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已成功以業主身份登入 Cloud Manager！如果您未指派&#x200B;**業主**&#x200B;角色，請聯絡您的系統管理員。

## 下一步 {#whats-next}

現在您可以作為系統管理員存取 Cloud Manager，您可以建立您的第一個程序了。

您應該透過下一次查看文件來繼續您的上線之旅[建立程序](create-program.md)您將在其中學習如何操作。

## 其他資源 {#additional-resources}

按照其他資源了解：

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 計畫和環境。
* [AEMas a Cloud Service團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)  — 了解AEMas a Cloud Service團隊和產品設定檔如何授予和限制您授權Adobe解決方案的存取權。
